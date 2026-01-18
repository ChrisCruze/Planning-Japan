# Engineering a Robust Flight Scraper: From Selenium Automation to LLM Analysis

## Summary

A technical blueprint for building a stable Google Flights scraper using Selenium and Apify, detailing specific DOM selectors and production workflows.

## Description

Technical architecture slide detailing the implementation of a Python/Selenium flight scraper.

## Insight

Targeting stable accessibility attributes like 'aria-label' rather than volatile CSS classes is the key to maintaining scraper longevity against frequent frontend updates.

## Input

LLMs like ChatGPT/Perplexity/Gemini are great for *strategy* and transforming flight data, but they cannot reliably surface every live fare or replicate historical prices; you need them orchestrating real search engines (Google Flights, Skyscanner, Kayak, etc.), not replacing them.[1][2]

Below is a practical way to combine them and which platforms to lean on when you’re optimizing across multiple airports.

## Why LLMs miss good or “historical” prices

LLMs:
- Do not have direct GDS/airline API access in consumer UIs, so they mostly reason *about* flights instead of querying full inventories.[2][1]
- Tend to default to “safe” patterns (major hubs, obvious routes), a form of collapse where you keep seeing the same 3–5 options and mid‑range prices.[3]
- Are not guaranteed to be trained on, or have tools connected to, the *exact* historical price traces you remember for a period.[4][3]

So use them as:
- Constraint solvers (“given this dump of options, rank by X,Y,Z”).  
- Macro‑strategy advisors (“which days/airports/alliances to target”).  
- Script generators (e.g., generate scraping/automation code against flight tools).[5][6]

## Best engines for multi‑airport / flexible search

When you care about *deterministic* coverage and multiple airports, these tend to work best:

| Need | Best tools | Why they’re strong |
| --- | --- | --- |
| Fast baseline, multiple airports, decent price history | **Google Flights**, **KAYAK** | Google is very fast, strong filters, good calendar/date grid; Kayak supports multiple departure airports and color‑coded fare calendars. [7][8][9] |
| “Everywhere” / flexible region + dates | **Skyscanner**, **FlightsFinder**, **Kiwi** | “Everywhere” destination search, whole‑month or year calendars, and region‑level search (country/continent), great for broad scanning. [7][8][9] |
| Very flexible routes, stitched itineraries | **Kiwi**, **PanFlights** | Can stitch non‑partner carriers and flexible multi‑city routes, including remote airports and route optimization. [10][9] |
| Deep control / power user | **ITA Matrix** (backing Google Flights) | Advanced routing language and fare construction; often used after Google Flights to lock in a specific construction. [11][8] |

For someone doing multi‑airport optimization around NYC, a strong stack is:
- Google Flights (primary grid/explore).[7][9]
- Skyscanner or FlightsFinder/“flexible dates” for everywhere + obscure combos.[9][7]
- Kiwi or PanFlights when you’re willing to self‑connect.[10][9]

## How to use an LLM *with* these tools

Treat the LLM as a meta‑layer over your manual/automated searches:

1. **Query design / search strategy**
   - Ask it to propose a search plan across tools: which origin airports to bundle, which date windows to scan, and which engines to use for each step (baseline vs. edge routes).[8][7][9]
   - Example: “Given NYC and possible destinations X/Y/Z, propose search steps on Google Flights + Skyscanner to minimize total cost with max 1 stop.”

2. **Parsing and ranking exported data**
   - Export or copy search results (date grids, CSV exports, scraped data) and have the LLM:
     - Normalize carriers, stops, and total travel time.  
     - Score options given your utility function (e.g., minimize cost subject to arrival before 10am, no <90‑min connections, prefer alliances).[5]

3. **Agentic workflows**
   - Use tools like LangChain/LangGraph or browser‑automation agents that:
     - Call Google Flights / Skyscanner / Kiwi with different airport/date combos.  
     - Pull results into a table.  
     - Have the LLM run reasoning on that table to pick candidates and suggest “next queries” (e.g., tighten date window where heat‑map shows dips).[6][5]

4. **Retrospective / “historical” sanity checks**
   - For a past period where you *know* prices were lower, you won’t get exact historical fares, but you can:
     - Use the LLM to infer likely causes (seasonality, fuel, demand, route cuts).[12][2]
     - Ask it to define guardrail ranges (e.g., “on NYC–LON, off‑peak economy under \$X one‑way is historically ‘good’ vs. ‘great’ vs. ‘unicorn’”) and then compare to current grids you see in Google Flights.[7][8][12]

## Concrete workflow for “best determinant across many airports”

For something like NYC + BOS + PHL + maybe WAS to Europe/Asia:

1. **Wide scan**
   - In Google Flights: use multiple departure airports and a destination region, view month‑wide calendar + date grid to see low‑fare days by origin.[9][7]
   - In Skyscanner / FlightsFinder / Kiwi: run “Everywhere” or region searches from an airport group and flexible dates (month/year).[7][9]

2. **Data capture**
   - Screenshot or copy the cheapest round‑trip prices by origin and date buckets into a small sheet (or export if supported).[9]
   - Include columns: origin airport, destination (city/region), date range, fare, carrier, stops, total duration.

3. **Send to LLM for optimization**
   - Paste that structured data and ask:
     - “Find Pareto‑optimal itineraries minimizing price and total travel time.”  
     - “Rank the airports by effective ‘value’ when you factor in my ground‑travel penalty (e.g., add \$50 cost for BOS vs. JFK).”[5]

4. **Refine**
   - Use the LLM’s ranking to focus on 1–2 best origin airports + tight date ranges, then re‑run focused searches directly in Google Flights / Skyscanner to confirm and book.[8][7][9]

If helpful, a next step could be drafting a concrete schema and LLM prompt template for you (e.g., JSON columns + scoring function) so you can drop in exports from Google Flights/Skyscanner and have an agent consistently choose the best airport/date combo.

Sources
[1] When LLMs Hit Their Limit And Why You Need Agents https://aipmguru.substack.com/p/when-llms-hit-their-limit-and-why
[2] The Rise of AI Flight Search Engines: Could LLMs Reshape Airlines ... https://pros.com/learn/blog/rise-ai-flight-search-engines-could-llms-reshape-airlines-traffic-acquisition-trends/
[3] Escaping LLM Collapse: Why AI Keeps Recommending the Same 3 ... https://www.ottotheagent.com/tech-blog-posts/escaping-llm-collapse-why-ai-keeps-recommending-the-same-3-flights-and-how-we-broke-it
[4] Fine-Tuning LLMs vs. RAG: How to Solve LLM Limitations - Memgraph https://memgraph.com/blog/llm-limitations-fine-tuning-vs-rag
[5] Searching flights just got better with the power of LLM (and a bit of ... https://www.reddit.com/r/ChatGPT/comments/1mim0b2/searching_flights_just_got_better_with_the_power/
[6] Building a Secure Flight Booking System with LLM Agent in Langflow https://dev.to/permit_io/building-a-secure-flight-booking-system-with-llm-agent-in-langflow-3ml
[7] Google Flights vs Skyscanner: Honest Comparison in 2026 - Going https://www.going.com/guides/google-flights-vs-skyscanner
[8] 10 best flight booking solutions in 2026 - COAX Software https://coaxsoft.com/blog/10-best-flight-booking-solutions
[9] Flexible Flights, Flexible Dates Flight Search | FlightsFinder https://www.flightsfinder.com/flexible-dates
[10] PanFlights: Flexible flight search, fare calendar and reverse ... https://panflights.com
[11] TravelArrow vs Google Flights vs Skyscanner… what's actually ... https://www.reddit.com/r/travel/comments/1qax1ll/travelarrow_vs_google_flights_vs_skyscanner_whats/
[12] The 10 Best (and Cheapest) Airfare Search Sites for ... https://www.frommers.com/tips/airfare/the-10-best-and-cheapest-airfare-search-sites-for-2026/
[13] Comparing Language Models (LLM & LCM) in Modern Airport ... https://www.linkedin.com/pulse/comparing-language-models-llm-lcm-modern-airport-burak-da%C4%9Fdeviren-9peof
[14] How to search for multi-city (aka open-jaw) flights with flexible ... https://www.reddit.com/r/Shoestring/comments/156x7q7/how_to_search_for_multicity_aka_openjaw_flights/
[15] Why is finding the nearest airport using LLMs so complex? https://stories.riafy.me/why-is-finding-the-nearest-airport-using-llms-so-complex-76bca0ace1d5

