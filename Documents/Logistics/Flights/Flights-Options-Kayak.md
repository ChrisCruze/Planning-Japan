# Flight Options Research - Kayak

**Research flights using Kayak URLs for all origins. Dates: Apr 2-11, 2026. Extract: Price, Route, Times, Duration, Value score, Booking URL, Research timestamp (YYYY-MM-DD HH:MM). Tool: Kayak. First search: Export all options to JSON/CSV.**

## Context

**Trip Dates**: April 2-11, 2026 (9 days, 7 nights in Japan)

**Travelers**:
- Chris (trip organizer, New York origin)
- Yalisa (Hershey, PA - may consider NYC departure)
- Karina, Keyla (trip organizer), Lylie (Atlanta origin)

**Constraints**:
- Cabin Class: Economy
- Maximum Stops: 1 stop preferred, 2 stops only if dramatically cheaper
- Maximum Duration: <30 hours per direction
- Passengers: 1 adult (NYC, PHL, MDT), 3 adults (ATL)

**Destination**: Tokyo
- **HND** (Haneda Airport) - Preferred (closer to Tokyo center)
- **NRT** (Narita Airport) - Acceptable alternative
- **TYO** (Kayak code for both HND and NRT)

## Round-Trip Flight URLs

### New York → Tokyo
https://www.kayak.com/flights/NYC-TYO/2026-04-02/2026-04-11?sort=bestflight_a

### Atlanta → Tokyo
https://www.kayak.com/flights/ATL-TYO/2026-04-02/2026-04-11?sort=bestflight_a

### Harrisburg, PA → Tokyo
https://www.kayak.com/flights/MDT-TYO/2026-04-02/2026-04-11?sort=bestflight_a

### Philadelphia → Tokyo
https://www.kayak.com/flights/PHL-TYO/2026-04-02/2026-04-11?sort=bestflight_a

## Multi-City / Open-Jaw Flight URLs

### NYC → Tokyo (HND), Tokyo (NRT) → NYC
*(Fly into Haneda, out of Narita)*
https://www.kayak.com/flights/MultiCity/NYC-HND/2026-04-02/TYO-NYC/2026-04-11?sort=bestflight_a

### NYC → Tokyo (HND), Osaka (KIX) → NYC
*(Good if you want Kyoto/Osaka at the end + depart there)*
https://www.kayak.com/flights/MultiCity/NYC-HND/2026-04-02/KIX-NYC/2026-04-11?sort=bestflight_a

### Atlanta → Tokyo (HND), Tokyo (NRT) → Atlanta
*(Open-jaw for ATL)*
https://www.kayak.com/flights/MultiCity/ATL-HND/2026-04-02/TYO-ATL/2026-04-11?sort=bestflight_a

### Harrisburg → Tokyo (HND), Tokyo (NRT) → Harrisburg
https://www.kayak.com/flights/MultiCity/MDT-HND/2026-04-02/TYO-MDT/2026-04-11?sort=bestflight_a

### Philadelphia → Tokyo (HND), Tokyo (NRT) → Philadelphia
https://www.kayak.com/flights/MultiCity/PHL-HND/2026-04-02/TYO-PHL/2026-04-11?sort=bestflight_a

## Instructions: Using Kayak URLs

### Tool
**Kayak**: https://www.kayak.com

### Search Process

1. **Click or navigate to each URL** above
2. **Wait for page to load** and results to display
3. **Extract data** from search results using common sense
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

**For multi-city/open-jaw flights**, extract:
- Outbound route and details
- Return route and details
- Total travel time (combined)

## Research Template: Round-Trip Flights

| Rank | Origin | Destination | Airline | Price | Route | Departure Time | Arrival Time | Duration | Value Score | Booking URL | Research Timestamp |
|------|--------|-------------|---------|-------|-------|----------------|--------------|----------|-------------|-------------|-------------------|
| 1 | NYC | TYO | | $ | Non-stop / 1-stop (city) | | | | /10 | | |
| 2 | | | | $ | | | | | /10 | | |
| 3 | | | | $ | | | | | /10 | | |

## Research Template: Multi-City / Open-Jaw Flights

| Rank | Origin | Arrival | Departure | Airline | Price | Outbound Route | Return Route | Outbound Duration | Return Duration | Value Score | Booking URL | Research Timestamp |
|------|--------|---------|-----------|---------|-------|----------------|--------------|-------------------|-----------------|-------------|-------------|-------------------|
| 1 | NYC | HND | KIX | | $ | Non-stop / 1-stop | Non-stop / 1-stop | | | /10 | | |
| 2 | | | | | $ | | | | | /10 | | |
| 3 | | | | | $ | | | | | /10 | | |

### Value Score Criteria (1-10)

**For Round-Trip Flights**:
- **Price** (40%): Lower price = higher score
- **Convenience** (30%): Non-stop > 1-stop, HND > NRT, reasonable times
- **Duration** (20%): Shorter total travel time = higher score
- **Schedule** (10%): Departure/arrival times that work well

**For Multi-City/Open-Jaw Flights**:
- **Price** (35%): Lower price = higher score (consider Shinkansen cost ~$100-150)
- **Convenience** (30%): Non-stop > 1-stop, HND > NRT, KIX > ITM, reasonable times
- **Duration** (20%): Shorter total travel time = higher score
- **Itinerary Efficiency** (15%): Open-jaw eliminates backtracking, saves time in Japan

## Next Steps

1. Export all flight options to JSON/CSV from first search
2. Compile findings into comparison tables above
3. Calculate value scores for top options
4. Compare round-trip vs. open-jaw options
5. Update this document with research results
6. Cross-reference with [[Flights-Options-Google-Flights]] for comparison

## Related Notes

- [[Logistics]] - Overall trip logistics and coordination
- [[Flights]] - Flight research overview and comparison framework
- [[Flights-Options-Google-Flights]] - Google Flights research comparison
- [[People]] - Traveler profiles and preferences

---
title: Flight Options Research - Kayak
date: 2026-01-12
tags: [#japan-trip, #logistics, #flights, #research, #kayak]
type: reference
status: draft
aliases: []
related: ["[[Logistics]]", "[[Flights]]", "[[Flights-Options-Google-Flights]]"]
---
