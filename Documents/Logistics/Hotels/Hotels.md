# Hotels Research Overview

> Define hotel selection criteria, comparison framework, and research methodology for finding accommodations in Tokyo that meet group needs and budget.

## Purpose

This document establishes the criteria, framework, and instructions for researching hotels in Tokyo. It provides the foundation for comparing hotel options and making informed booking decisions.

## Context

### Group Details
- **Group Size**: 5-7 travelers (depending on final participation)
- **Room Requirements**: 2-3 rooms needed
- **Trip Dates**: April 2-11, 2025 (7 nights)
- **Check-in**: Thursday, April 2, 2025
- **Check-out**: Friday, April 11, 2025

### Budget Considerations
- **Total Budget**: ~$2,500 per person (includes round-trip flight + hotel)
- **Flight Target**: $700-1,200 per person
- **Hotel Target**: Remaining budget after flights (~$1,300-1,800 per person for 7 nights)
- **Per Night Target**: ~$185-260 per person, or ~$370-520 per room (assuming 2 people per room)

## Hotel Selection Criteria (Priority Order)

### 1. Location > Room Size
- **Priority**: Location is more important than room size
- **Rationale**: Low friction = high enjoyment. Prioritize location over luxury.

### 2. Close to Public Transit
- **Target**: <5 minute walk to train/subway station
- **Rationale**: Essential for daily travel in Tokyo
- **Key Transit Lines**: JR Lines, Tokyo Metro, Toei Subway

### 3. Neighborhood Preferences
- **Akasaka**: Ideal for first-timers - clean, central, safe, family-friendly dining
- **Shimbashi**: Best for connectivity (JR Lines), authentic local nightlife (Izakayas)
- **Asakusa**: Traditional neighborhood, hotel location option
- **Other Options**: Consider other central neighborhoods with good transit access

### 4. Business Hotels Target Category
- **Target**: Business hotels in central hubs for optimal value
- **Examples**: Tokyu Stay, Sotetsu Fresa chains
- **Characteristics**: Clean, modern, but small rooms. Excellent value for groups prioritizing exploration over room size.

### 5. Walkability and Safety
- Safe and walkable neighborhood
- Local restaurants and amenities nearby
- Balance of convenience and local experience

## Comparison Framework

When evaluating hotels, consider:

1. **Location Score** (40%):
   - Distance to public transit (<5 min = excellent, 5-10 min = good, >10 min = poor)
   - Neighborhood quality (Akasaka/Shimbashi/Asakusa = excellent)
   - Walkability to key areas

2. **Price Score** (30%):
   - Total cost for stay (7 nights)
   - Cost per person
   - Value relative to location and amenities

3. **Amenities Score** (20%):
   - Room size (adequate for 2 people)
   - Basic amenities (WiFi, AC, private bathroom)
   - Business hotel features

4. **Group Suitability** (10%):
   - Multiple room availability
   - Group booking options
   - Family-friendly features (if applicable)

## Instructions: Booking.com Research

### Tool
Use **Booking.com**: https://www.booking.com

### Search Specification Best Practices

**Provide explicit, structured parameters:**

1. **Dates**:
   - Check-in: April 2, 2025
   - Check-out: April 11, 2025
   - Duration: 7 nights

2. **Location**:
   - Primary: Tokyo, Japan
   - Specific neighborhoods to search:
     - Asakusa, Tokyo
     - Akasaka, Tokyo
     - Shimbashi, Tokyo
   - Search each neighborhood separately for focused results

3. **Guests and Rooms**:
   - Number of guests: 5 adults (or 7 if all travelers confirmed)
   - Number of rooms: 2-3 rooms
   - Search for both configurations to compare options

4. **Filter Preferences**:
   - Property type: Hotels
   - Price range: Consider total budget (~$370-520 per room per night)
   - Star rating: 3-4 stars (business hotels typically in this range)
   - Distance from city center: Within reasonable distance
   - Facilities: WiFi (essential), Air conditioning (essential)

**Use natural language that mirrors human interaction:**

Example search instructions:
- "Search for hotels in Asakusa, Tokyo, checking in April 2, 2025 and checking out April 11, 2025, for 5 adults, 2-3 rooms"
- "Search for hotels in Akasaka, Tokyo, checking in April 2, 2025 and checking out April 11, 2025, for 5 adults, 2-3 rooms"
- "Search for hotels in Shimbashi, Tokyo, checking in April 2, 2025 and checking out April 11, 2025, for 5 adults, 2-3 rooms"

### Technical Implementation Considerations

**Handle dynamic content loading:**
- Wait for JavaScript to fully render hotel listings and availability before extracting data
- Booking.com loads results progressively - ensure all hotel cards are visible before data extraction
- Wait for price displays and availability indicators to load

**Implement proper wait conditions:**
- Use explicit waits for specific elements:
  - Hotel cards/result items
  - Price displays (per night and total)
  - Availability indicators
  - Star ratings
  - Distance/neighborhood information
- Avoid fixed timeouts - wait for actual elements to appear

**Plan for anti-bot measures:**
- Rotate user agents between searches
- Implement reasonable delays between actions (2-5 seconds)
- Avoid patterns signaling automation:
  - Don't search too quickly
  - Vary search order
  - Use natural mouse movements if simulating

**Build error recovery:**
- Monitor for CAPTCHAs - pause and handle if detected
- Watch for IP blocks - implement delays or proxy rotation if needed
- Handle page structure changes - use flexible selectors
- Implement fallback strategies if initial search fails
- Handle multilingual content: Booking.com may display differently based on location or session state

### Data Extraction and Validation

**Extract structured data fields systematically:**

For each hotel option, extract:
- **Hotel name**
- **Location/neighborhood** (Asakusa, Akasaka, Shimbashi, etc.)
- **Price information**:
  - Price per night
  - Total price for 7 nights
  - Price per person (if applicable)
- **Room types available**:
  - Room size
  - Bed configuration
  - Number of rooms available
- **Amenities**:
  - WiFi (essential)
  - Air conditioning (essential)
  - Private bathroom
  - Other relevant amenities
- **Distance from public transit** (if available)
- **Star rating**
- **Availability status** (available for all dates)
- **Booking link**

**Validate extracted data immediately:**
- Verify prices are numeric and reasonable
- Verify dates are valid (check-in April 2, check-out April 11)
- Verify required fields aren't empty
- Check for dynamic availability changes
- Handle multilingual content variations
- Verify room availability for group size

### Research Process

1. **Search each neighborhood separately**:
   - Start with Akasaka (ideal for first-timers)
   - Then Shimbashi (best connectivity)
   - Then Asakusa (traditional neighborhood)

2. **For each neighborhood, search both room configurations**:
   - 5 adults, 2 rooms
   - 5 adults, 3 rooms
   - (Adjust if group size changes)

3. **Apply filters**:
   - Property type: Hotels
   - Price range: Within budget
   - Star rating: 3-4 stars
   - Essential facilities: WiFi, AC

4. **Review and extract top 10-15 options** from each neighborhood

5. **Compare across neighborhoods** to identify best overall value

6. **Verify transit access** for top options (distance to nearest station)

## Next Steps

Once research framework is established:

1. **Use this document** as reference for conducting hotel research
2. **Record findings** in [[Hotel-Options]] document
3. **Compare options** using the framework above
4. **Identify top 5-10 recommendations** for group review
5. **Cross-reference** with [[Logistics]] for final booking decisions

## Related Notes

- [[Logistics]] - Overall trip logistics and coordination
- [[Hotel-Options]] - All hotel options being considered
- [[Activities]] - Location-based needs for hotel selection
- [[People]] - Group size and preferences

## References

- Booking.com: https://www.booking.com
- Trip dates: April 2-11, 2025 (7 nights)
- Budget target: ~$2,500 per person (flight + hotel)
- Neighborhood priorities: Akasaka, Shimbashi, Asakusa
- Target: Business hotels with excellent transit access

---
title: Hotels Research Overview
date: 2026-01-12
tags: [#japan-trip, #logistics, #hotels, #research]
type: guide
status: draft
aliases: []
related: ["[[Logistics]]", "[[Hotel-Options]]"]
---
