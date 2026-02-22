---
name: award-travel
description: This skill should be used when the user asks about "award flights", "points", "miles", "avios", "asia miles", "loyalty programs", "flight availability", "award search", "redemptions", "business class availability", "first class availability", mentions specific airlines (British Airways, Qatar Airways, Cathay Pacific), or discusses using points/miles for flights. Provides guidance for using the Award Travel Finder MCP tools.
version: 1.0.0
---

# Award Travel Finder

Search award flight availability across airlines using points and miles.

## Available MCP Tools

### search_availability
Search award seats for a specific route and date.

**Parameters:**
- `airline`: `british_airways` | `qatar_airways` | `cathay_pacific`
- `departure_code`: 3-letter IATA code (e.g. LHR)
- `arrival_code`: 3-letter IATA code (e.g. JFK)
- `date`: YYYY-MM-DD

Returns cabin-by-cabin availability with points costs.

### search_monthly_availability
Search an entire month for availability. Best for finding flexible dates. Can take up to 90 seconds.

**Parameters:**
- `airline`: `british_airways` | `qatar_airways` | `cathay_pacific`
- `departure_code`: 3-letter IATA code
- `arrival_code`: 3-letter IATA code
- `date`: YYYY-MM or YYYY-MM-DD (uses the month)

### get_pricing
Get the award chart for a route. Shows points per cabin class, off-peak and peak. No date needed.

**Parameters:**
- `airline`: `british_airways` | `qatar_airways` | `cathay_pacific`
- `departure_code`: 3-letter IATA code
- `arrival_code`: 3-letter IATA code

### get_airports
List all airports an airline serves. Check route existence before searching.

**Parameters:**
- `airline`: `british_airways` | `qatar_airways` | `cathay_pacific`

### list_supported_airlines
List airlines available for search. No parameters.

### list_programs
List all 14 loyalty programs with award chart data. No parameters.

### get_program_rates
Get full award chart for a loyalty program.

**Parameters:**
- `program`: Program slug (e.g. `british-airways`, `emirates`, `aeroplan`)

## Workflow: Finding Award Flights

1. **Confirm route and airline.** Convert city names to IATA codes. If unsure which airline, check `get_airports` or suggest based on the route.
2. **Check pricing first** with `get_pricing` to show what the route costs in points per cabin class.
3. **Search availability** with `search_availability` for a specific date, or `search_monthly_availability` for flexible dates.
4. **Present results clearly.** Format as a table showing date, cabin class, seats available, and points required.

## Workflow: Comparing Programs

1. Use `list_programs` to show all available programs.
2. Use `get_program_rates` for each program the user wants to compare.
3. Focus comparison on the route/region they care about.
4. Highlight which program offers the best value per cabin class.

## API Key (Required)

An API key is required. Add it to `~/.claude/mcp.json`:

```json
{
  "mcpServers": {
    "awardtravelfinder": {
      "type": "url",
      "url": "https://mcp.awardtravelfinder.com/mcp",
      "headers": {
        "X-API-Key": "your-api-key"
      }
    }
  }
}
```

Or via CLI:
```
claude mcp add awardtravelfinder --transport sse -H "X-API-Key: your-api-key" https://mcp.awardtravelfinder.com/mcp
```

Get your API key at https://awardtravelfinder.com/pricing
