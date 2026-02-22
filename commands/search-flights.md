---
description: Search award flight availability across airlines
argument-hint: "[airline] [from] [to] [date-or-month]"
allowed-tools:
  - mcp__awardtravelfinder__list_supported_airlines
  - mcp__awardtravelfinder__search_availability
  - mcp__awardtravelfinder__search_monthly_availability
  - mcp__awardtravelfinder__get_pricing
  - mcp__awardtravelfinder__get_airports
---

# Search Award Flights

The user wants to search for award flight availability.

## Arguments

The user invoked this command with: $ARGUMENTS

Parse the arguments to extract:
- **Airline**: BA/British Airways, QR/Qatar Airways, CX/Cathay Pacific
- **From**: Departure airport (city name or IATA code)
- **To**: Arrival airport (city name or IATA code)
- **Date**: Specific date (YYYY-MM-DD) or month (YYYY-MM)

Map airline names to slugs: `british_airways`, `qatar_airways`, `cathay_pacific`

## Process

1. If airline is not specified, check which airlines serve the route using `get_airports` for each airline.
2. Get pricing with `get_pricing` to show the points cost.
3. If a specific date is given, use `search_availability`. If a month is given, use `search_monthly_availability`. If no date, ask the user.
4. Present results in a clean table: Date | Cabin | Seats | Points Required
5. Highlight the best value options.

## Examples

```
/atf:search-flights BA LHR JFK 2026-04-15
/atf:search-flights qatar DOH SIN 2026-05
/atf:search-flights cathay HKG NRT 2026-06-01
```
