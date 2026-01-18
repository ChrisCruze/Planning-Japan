# Flight Options Research - Google Flights

**Research flights using Google Flights for all origins. Dates: Apr 2-11, 2025. Extract: Price, Route, Times, Duration, Value score, Booking URL, Research timestamp (YYYY-MM-DD HH:MM). Tool: Google Flights. First search: Export all options to JSON/CSV.**

## Context

**Trip Dates**: April 2-11, 2025 (9 days, 7 nights in Japan)

**Travelers**:
- Chris (trip organizer, New York origin)
- Yalisa (Hershey, PA - may consider NYC departure)
- Karina, Keyla (trip organizer), Lylie (Atlanta origin)

**Constraints**:
- Cabin Class: Economy
- Maximum Stops: 1 stop preferred, 2 stops only if dramatically cheaper
- Maximum Duration: <30 hours per direction

**Destination**: Tokyo
- **HND** (Haneda Airport) - Preferred (closer to Tokyo center)
- **NRT** (Narita Airport) - Acceptable alternative

## Instructions: Google Flights Research

### Tool
**Google Flights**: https://www.google.com/travel/flights

### Search Process

1. **Navigate to Google Flights**
2. **Enter search parameters** for each origin (see sections below)
3. **Wait for results to load** before extracting data
4. **First search**: Export all flight options to structured format (JSON/CSV) for initial data capture

### Data Extraction

For each flight option, extract:
- Airline name
- Price (total round-trip or open-jaw in USD)
- Route: Non-stop or single-stop (specify connection cities)
- Departure time (local time at origin)
- Arrival time (local time at destination)
- Return departure time (for round-trip)
- Return arrival time (for round-trip)
- Duration: Total flight time outbound and return
- **Booking URL** (for validation)
- **Research timestamp** (YYYY-MM-DD HH:MM - when research was conducted)

**Validate**: Prices numeric, dates valid, required fields not empty, times in correct time zones.

## New York (Chris)

### Round-Trip Flights

**Traveler**: Chris (trip organizer, New York origin)

**Origin**: New York (Google Flights auto-shows JFK, EWR, LGA options)

**Search**: Round-trip flights from New York to Tokyo (HND or NRT), departing April 2, 2025 and returning April 11, 2025, for 1 adult in economy class.

| Rank | Origin | Destination | Airline | Price | Route | Departure Time | Arrival Time | Duration | Value Score | Booking URL | Research Timestamp |
|------|--------|-------------|---------|-------|-------|----------------|--------------|----------|-------------|-------------|-------------------|
| 1 | New York | HND | | $ | Non-stop / 1-stop (city) | | | | /10 | | |
| 2 | | | | $ | | | | | /10 | | |
| 3 | | | | $ | | | | | /10 | | |

### Open-Jaw Flights (Tokyo → Osaka)

**Open-Jaw Benefit**: Tokyo and Osaka are 250-300 miles apart, connected by efficient Shinkansen (2.5-3 hours). Flying into Tokyo and out of Osaka eliminates backtracking, allowing you to see more of Japan efficiently.

**Arrival (Tokyo)**:
- **HND** (Haneda Airport) - Preferred
- **NRT** (Narita Airport) - Acceptable

**Departure (Osaka)**:
- **KIX** (Kansai International Airport) - Primary option
- **ITM** (Osaka Itami Airport) - Alternative (limited international)

**Search**: Multi-city flights from New York to HND/NRT departing April 2, 2025, and from KIX/ITM to New York departing April 11, 2025, for 1 adult in economy class.

**Note**: Use Google Flights "Multi-city" option to search both legs simultaneously, or search each leg separately and combine results.

| Rank | Origin | Arrival | Departure | Airline | Price | Outbound Route | Return Route | Outbound Duration | Return Duration | Value Score | Booking URL | Research Timestamp |
|------|--------|---------|-----------|---------|-------|----------------|--------------|-------------------|-----------------|-------------|-------------|-------------------|
| 1 | New York | HND | KIX | | $ | Non-stop / 1-stop | Non-stop / 1-stop | | | /10 | | |
| 2 | | | | | $ | | | | | /10 | | |
| 3 | | | | | $ | | | | | /10 | | |

## Atlanta (Karina, Keyla, Lylie)

**Travelers**: Karina, Keyla (trip organizer), Lylie (Atlanta origin)

**Origin**: ATL (Hartsfield-Jackson Atlanta International Airport)

**Search**: Round-trip flights from ATL to Tokyo (HND or NRT), departing April 2, 2025 and returning April 11, 2025, for 1 adult in economy class. Then repeat search for 3 adults to check group pricing.

**Note**: Check group pricing vs. individual. Some airlines offer group discounts.

| Rank | Origin | Destination | Airline | Price (1p) | Price (3p) | Route | Departure Time | Arrival Time | Duration | Value Score | Booking URL | Research Timestamp |
|------|--------|-------------|---------|------------|------------|-------|----------------|--------------|----------|-------------|-------------|-------------------|
| 1 | ATL | HND | | $ | $ | Non-stop / 1-stop (city) | | | | /10 | | |
| 2 | | | | $ | $ | | | | | /10 | | |
| 3 | | | | $ | $ | | | | | /10 | | |

## Philadelphia (Yalisa)

**Traveler**: Yalisa (Hershey, PA - may also consider NYC departure for convenience)

**Origin**: PHL (Philadelphia International Airport)

**Search**: Round-trip flights from PHL to Tokyo (HND or NRT), departing April 2, 2025 and returning April 11, 2025, for 1 adult in economy class.

**Note**: Compare to New York options if PHL prices are high.

| Rank | Origin | Destination | Airline | Price | Route | Departure Time | Arrival Time | Duration | Value Score | Booking URL | Research Timestamp |
|------|--------|-------------|---------|-------|-------|----------------|--------------|----------|-------------|-------------|-------------------|
| 1 | PHL | HND | | $ | Non-stop / 1-stop (city) | | | | /10 | | |
| 2 | | | | $ | | | | | /10 | | |
| 3 | | | | $ | | | | | /10 | | |

## Harrisburg (Yalisa)

**Traveler**: Yalisa (Hershey, PA - may also consider NYC departure for convenience)

**Origin**: MDT (Harrisburg International Airport) - Smaller airport, may require multiple connections

**Search**: Round-trip flights from MDT to Tokyo (HND or NRT), departing April 2, 2025 and returning April 11, 2025, for 1 adult in economy class.

**Note**: MDT is a smaller regional airport and may have limited options or require multiple connections. Compare results to New York and Philadelphia options.

| Rank | Origin | Destination | Airline | Price | Route | Departure Time | Arrival Time | Duration | Value Score | Booking URL | Research Timestamp |
|------|--------|-------------|---------|-------|-------|----------------|--------------|----------|-------------|-------------|-------------------|
| 1 | MDT | HND | | $ | Non-stop / 1-stop (city) | | | | /10 | | |
| 2 | | | | $ | | | | | /10 | | |
| 3 | | | | $ | | | | | /10 | | |

## Value Score Criteria (1-10)

### Round-Trip Flights
- **Price** (40%): Lower price = higher score
- **Convenience** (30%): Non-stop > 1-stop, HND > NRT, reasonable times
- **Duration** (20%): Shorter total travel time = higher score
- **Schedule** (10%): Departure/arrival times that work well

### Open-Jaw Flights
- **Price** (35%): Lower price = higher score (consider Shinkansen cost ~$100-150)
- **Convenience** (30%): Non-stop > 1-stop, HND > NRT, KIX > ITM, reasonable times
- **Duration** (20%): Shorter total travel time = higher score
- **Itinerary Efficiency** (15%): Open-jaw eliminates backtracking, saves time in Japan

### Atlanta Group Flights
- **Price** (40%): Lower price = higher score (consider both individual and group pricing)
- **Convenience** (30%): Non-stop > 1-stop, HND > NRT, reasonable times
- **Duration** (20%): Shorter total travel time = higher score
- **Schedule** (10%): Departure/arrival times that work well for group

## Next Steps

1. Export all flight options to JSON/CSV from first search
2. Compile findings into comparison tables above
3. Calculate value scores for top options
4. Compare round-trip vs. open-jaw options (for New York)
5. Compare individual vs. group pricing (for Atlanta)
6. Compare across origins to identify best overall value
7. Update this document with research results
8. Cross-reference with [[Flights-Options-Kayak]] for comparison

## Related Notes

- [[Logistics]] - Overall trip logistics and coordination
- [[Flights]] - Flight research overview and comparison framework
- [[Flights-Options-Kayak]] - Kayak research comparison
- [[Chris]] - Traveler profile and preferences
- [[Keyla]] - Trip organizer profile and preferences
- [[Karina]] - Traveler profile and preferences
- [[Lylie]] - Traveler profile and preferences
- [[Yalisa]] - Traveler profile and preferences

---
title: Flight Options Research - Google Flights
date: 2026-01-12
tags: [#japan-trip, #logistics, #flights, #research, #google-flights]
type: reference
status: draft
aliases: []
related: ["[[Logistics]]", "[[Flights]]", "[[Flights-Options-Kayak]]"]
---
