# Modular Architecture for Agentic Flight Search

## Summary

A four-phase technical architecture for building a robust flight search backend using Apify Actors wrapped in Python for LLM consumption.

## Description

Technical architecture slide detailing the data flow from requirements to LLM integration.

## Insight

Wrapping existing commercial scrapers in a custom normalization Actor is superior to building raw Selenium scripts for resilient agentic workflows.

## Input

The cleanest Apify approach is: use an existing Google Flights Scraper Actor/API for data, then wrap it in your own Python Actor that standardizes results for your LLM/agent.[1][2][3][4][5]

## High-level phases (for agents)

- Requirements & tech spec  
- Data layer (Apify Flights Actor)  
- Orchestration & scheduling  
- LLM/agent integration  
- QA & monitoring

Below are concrete steps plus docs you can hand to different agents.

***

## 1) Requirements and tech spec

**Goal**: Build a flight-search backend that, given origin(s), Japan airports, and date windows, calls Apify’s Google Flights tooling and returns normalized JSON/CSV for an LLM to reason over.[2][3][5][1]

### Functional requirements (for a “Product/Spec” agent)

- Inputs:
  - Origin IATA or city groups, e.g. `["NYC","PHL","ATL"]`.  
  - Japan destinations, e.g. `["TYO","KIX","ITM","NGO","FUK","CTS"]`.  
  - Outbound date range and return date range (ISO `YYYY-MM-DD`).  
  - Trip type: round-trip, one-way, or multi-city/open-jaw.[3][5]
- Behavior:
  - For each origin–destination–date combo, query an Apify Google Flights Actor/API (e.g. `simpleapi/google-flights-scraper` or `johnvc/google-flights-data-scraper-flight-and-price-search`).[4][1][2][3]
  - Collect:
    - Price, currency.  
    - Airline(s), marketing vs operating carrier if available.  
    - Departure/arrival times, total duration.  
    - Number of stops and layover airports.  
    - URL/deep link to the original Google Flights result where provided.[1][2][3]
  - Normalize into a shared schema and persist to Apify Dataset + downloadable CSV.[6]
- Non-functional:
  - Handle rate limits (batch queries, respect `maximum` parameter).[2]
  - Fail fast when input parameters are invalid (bad IATA, malformed dates).  
  - Clear logging for each route/date run (origin, dest, dates, count of results).[6]

**Sample normalized schema**

```json
{
  "origin": "JFK",
  "destination": "HND",
  "tripType": "round-trip",
  "outboundDate": "2026-04-02",
  "returnDate": "2026-04-11",
  "price": 945.20,
  "currency": "USD",
  "airlines": ["Japan Airlines"],
  "alliances": ["oneworld"],
  "stopsOutbound": 0,
  "stopsReturn": 1,
  "durationOutboundMinutes": 840,
  "durationReturnMinutes": 900,
  "bookingLink": "https://www.google.com/travel/flights/...",
  "raw": {}
}
```

***

## 2) Data layer: choose and wrap an Apify Google Flights Actor

**Owner agent**: “Apify Integration” agent.

### Step 2.1 – Pick the base Actor/API

- Use an existing Google Flights Actor instead of writing Selenium yourself:[5][3][1][2]
  - Example: `simpleapi/google-flights-scraper` – JSON input with `departureIATA`, `arrivalIATA`, `departureDate`, `maximum`, etc.[2]
  - Example: `johnvc/google-flights-data-scraper-flight-and-price-search` for more advanced options (multi-city, filters, languages).[3][4]

**Common mistake to avoid**: Mixing multiple different store Actors in one app before you’ve standardized schemas—start with one and align your normalization on its output structure.[4][3][2]

### Step 2.2 – Create a thin Python wrapper Actor

Use the Python SDK + an Apify template:[7][6]

- Start from the empty Python template or a simple scraping template:[7]
- In `src/main.py`:
  - Read Actor input: `origins`, `destinations`, `outboundDates`, `returnDates`, `tripType`.  
  - For each combination, build the JSON required by the Flights Actor (e.g. `departureIATA`, `arrivalIATA`, `departureDate`, `returnDate`, `maximum`).[3][2]
  - Call the Flights Actor via Apify API client and capture results.[4][6]
  - Transform each record into your normalized schema and `Actor.push_data()` it.[6]

**Common mistakes & mitigations**

- Mistake: Not limiting the cartesian explosion.  
  - Mitigation: Hard-cap combinations per run (e.g., max 50 queries) and support pagination or multiple runs.  
- Mistake: Assuming all results have the same fields.  
  - Mitigation: Treat optional fields (`alliances`, `bookingLink`, baggage info) defensively; default to `null` if missing.[2][3]

***

## 3) Orchestration and scheduling

**Owner agent**: “Scheduler/DevOps” agent.

### Step 3.1 – Input model for a run

Define Actor input JSON like:

```json
{
  "origins": ["NYC", "PHL", "ATL"],
  "japanAirports": ["HND", "NRT", "KIX", "ITM", "NGO", "FUK", "CTS"],
  "outboundDateRange": ["2026-04-02", "2026-04-05"],
  "returnDateRange": ["2026-04-08", "2026-04-11"],
  "tripType": "round-trip",
  "maxQueries": 40
}
```

The Actor expands this to the underlying Google Flights Actor calls.

### Step 3.2 – Scheduling & rate limits

- Use Apify’s built-in scheduler to run:
  - On demand (triggered via API)  
  - Or on cron (e.g., daily 03:00 UTC to update prices).[6]
- Respect:
  - The `maximum` parameter on Flights Actors, which controls how many itineraries per search are scraped.[2]
  - Your cost limits (Apify usage + store Actor pricing).[1][2]

**Common mistakes**

- Firing too many Actors concurrently with same parameters → duplicated data and higher costs.  
- Forgetting to tag runs with an ID (e.g., `searchId`) to group results for the same logical search.

***

## 4) LLM/agent integration layer

**Owner agent**: “Reasoning/Selection” agent.

Responsibilities:

- Receive search parameters from user/LLM frontend.  
- Trigger the Apify wrapper Actor with those parameters.[6]
- Wait for completion (via webhooks or polling the run status).  
- Fetch Dataset items (JSON) and:
  - Filter out dominated options (Pareto front by price vs duration).  
  - Apply user-specific utilities (e.g., penalize non-NYC airports, prefer certain alliances).  

**Common mistakes**

- Letting the LLM directly form random Google Flights parameters; instead, validate/normalize into your spec first.  
- Not capturing the `searchId` in every row, which makes it hard to join multiple runs later.

***

## 5) Common pitfalls with Apify + Google Flights

- **DOM/behavior changes** are handled by the store Actor maintainer, but you still must:
  - Watch for sudden drops in result counts or obviously wrong prices.[3][2]
- **Input validation**:
  - Bad IATA codes or impossible dates will often just return zero results; your Actor should treat that as an error state/log event, not “success”.[2]
- **Open-jaw / multi-city**:
  - Not all Google Flights scrapers support full multi-city in one call; you might need to:
    - Call one-way twice (US → Japan, Japan → US from a different airport).  
    - Or use the more advanced multi-city scraper (e.g., John’s actor) that advertises multi-city support.[4][3]

***

## Documents you can hand to agents

### A. Product requirements doc (PRD)

- Problem: Automate multi-airport, multi-city Japan flight search for power users.  
- Users: You + future advanced travelers.  
- Scenarios:
  - “Compare NYC/PHL/ATL → Japan between Apr 2–11 for best value.”  
  - “Find open-jaw itineraries into Tokyo, out of Osaka.”  
- Success metrics:
  - Time saved vs manual Google Flights use.  
  - Number of times per week you use the tool.  
  - % of searches returning at least N high-quality options.

### B. Technical design doc

- Architecture:
  - Client/Agent → “Search Orchestrator” service → Apify wrapper Actor → Store Flights Actor(s) → Apify Dataset → LLM Ranking Layer.[3][6][2]
- Key components:
  - Apify wrapper Actor (Python, uses Apify SDK).[7][6]
  - Flight schema module shared between orchestrator and LLM.  
  - Monitoring: Apify run logs, dataset counts, alert if 0 results.[6]

### C. Implementation checklist per agent

- **Apify Integration agent**:
  - Choose base Flights Actor.  
  - Implement wrapper Actor with normalization and push_data.  
  - Test with a single NYC→TYO date pair.  

- **Scheduler/Infra agent**:
  - Configure scheduler and webhooks.  
  - Set environment secrets (Apify token).  
  - Implement run-status polling endpoint.  

- **LLM/Reasoning agent**:
  - Define strict JSON schema for results.  
  - Author prompts that assume that schema, not raw Google Flights HTML.  
  - Implement Pareto and custom scoring logic.

If you want, the next step can be a concrete `src/main.py` skeleton for the Apify wrapper Actor that calls a specific Google Flights scraper (e.g., `simpleapi/google-flights-scraper`) and emits your normalized schema.

Sources
[1] Google Flights Scraper API in Python - Apify https://apify.com/simpleapi/google-flights-scraper/api/python
[2] Google Flights Scraper - Apify https://apify.com/simpleapi/google-flights-scraper
[3] Google Flights Scraper - Apify https://apify.com/johnvc/google-flights-data-scraper-flight-and-price-search
[4] Google Flights API in Python - Apify https://apify.com/canadesk/google-flights/api/python
[5] Google Flights API - Apify https://apify.com/api/google-flights-api
[6] Introduction | SDK for Python - Apify Documentation https://docs.apify.com/sdk/python/docs/overview/introduction
[7] Empty Python project · Template - Apify https://apify.com/templates/python-empty
[8] Scrape Google Flights with Python - Apify Blog https://blog.apify.com/how-to-scrape-google-flights/
[9] Using Selenium | SDK for Python - Apify Documentation https://docs.apify.com/sdk/python/docs/guides/selenium
[10] How to use Selenium for web scraping (Python guide) - Apify Blog https://blog.apify.com/web-scraping-with-selenium-and-python/
[11] Google Flights OpenAPI definition - Apify https://apify.com/canadesk/google-flights/api/openapi
[12] Python browser automation with Selenium (2025 guide) - Apify Blog https://blog.apify.com/python-browser-automation-with-selenium/
[13] Flight Award & Itinerary Scraper – Miles, Taxes & Cabins - Apify https://apify.com/igolaizola/flight-award-scraper
[14] manifest.json - apify/actor-templates - GitHub https://github.com/apify/actor-templates/blob/master/templates/manifest.json
[15] Selenium + Chrome · Template - Apify https://apify.com/templates/python-selenium

