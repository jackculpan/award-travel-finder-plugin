---
name: award-travel-finder
description: Search award flight availability across British Airways, Qatar Airways, and Cathay Pacific. Compare 14 loyalty program award charts. Uses the Award Travel Finder MCP server.
homepage: https://awardtravelfinder.com
---

# Award Travel Finder

Search award flight availability and compare loyalty program award charts via the Award Travel Finder MCP server. Find the best points and miles redemptions across British Airways, Qatar Airways, and Cathay Pacific.

## Setup

### Claude Code

```bash
claude mcp add awardtravelfinder --transport sse https://mcp.awardtravelfinder.com/mcp
```

With API key (paid, unlimited searches):

```bash
claude mcp add awardtravelfinder --transport sse -H "X-API-Key: YOUR_KEY" https://mcp.awardtravelfinder.com/mcp
```

### Claude Desktop / Cursor

Add to your MCP config:

```json
{
  "mcpServers": {
    "awardtravelfinder": {
      "url": "https://mcp.awardtravelfinder.com/mcp"
    }
  }
}
```

### mcporter

```bash
mcporter add awardtravelfinder --url https://mcp.awardtravelfinder.com/mcp
```

## Available Tools (7)

### Search & Availability

| Tool | Description |
|------|-------------|
| `search_availability` | Search award seats for a specific route and date. Returns cabin-by-cabin availability with points costs. |
| `search_monthly_availability` | Search an entire month for availability. Day-by-day results across all cabin classes. Up to 90s. |
| `get_pricing` | Get the award chart for a route. Points per cabin class, off-peak and peak. No date needed. |
| `get_airports` | List all airports served by an airline. Check if a route exists before searching. |
| `list_supported_airlines` | List airlines available for search with codes and currencies. |

### Loyalty Programs

| Tool | Description |
|------|-------------|
| `list_programs` | List all 14 loyalty programs with currencies, hubs, and destination counts. No auth needed. |
| `get_program_rates` | Get full award chart for a specific program. All destinations with points per cabin class. No auth needed. |

## Airlines

| Airline | Slug | Code | Currency |
|---------|------|------|----------|
| British Airways | `british_airways` | BA | Avios |
| Qatar Airways | `qatar_airways` | QR | Avios |
| Cathay Pacific | `cathay_pacific` | CX | Asia Miles |

## Loyalty Programs (14)

| Program | Slug | Currency |
|---------|------|----------|
| Virgin Atlantic | `virgin-atlantic` | Virgin Points |
| British Airways | `british-airways` | Avios |
| Qatar Airways | `qatar-airways` | Avios |
| Singapore Airlines | `singapore-airlines` | KrisFlyer Miles |
| Cathay Pacific | `cathay-pacific` | Asia Miles |
| Emirates | `emirates` | Skywards Miles |
| Etihad | `etihad` | Guest Miles |
| Flying Blue | `flying-blue` | Flying Blue Miles |
| Aeroplan | `aeroplan` | Aeroplan Points |
| Turkish Airlines | `turkish-airlines` | Miles&Smiles |
| ANA | `ana` | ANA Miles |
| JetBlue | `jetblue` | TrueBlue Points |
| Jet2 Emirates | `jet2-emirates` | Emirates Miles |
| Virgin Partners | `virgin-partners` | Virgin Points |

## Usage Examples

### Search Specific Date

> Find BA business class availability from LHR to JFK on April 15th 2026

Uses `get_pricing` then `search_availability` with `airline: british_airways`, `departure_code: LHR`, `arrival_code: JFK`, `date: 2026-04-15`.

### Search Flexible Dates

> Show me Qatar Airways availability from Doha to Singapore for all of May

Uses `search_monthly_availability` with `airline: qatar_airways`, `departure_code: DOH`, `arrival_code: SIN`, `date: 2026-05`.

### Check Pricing

> How many Avios for London to New York in first class?

Uses `get_pricing` with `airline: british_airways`, `departure_code: LHR`, `arrival_code: JFK`.

### Compare Programs

> Compare British Airways and Emirates award charts

Uses `get_program_rates` for `british-airways` and `emirates`, then compares points per cabin class by destination.

### Check Airport Coverage

> What airports does Cathay Pacific fly to?

Uses `get_airports` with `airline: cathay_pacific`.

## Rate Limits

- **Free tier**: 20 availability searches per session
- **Paid tier**: Unlimited (API key tracked monthly)
- `get_pricing`, `get_airports`, `list_programs`, `get_program_rates` are unlimited
- MCP server: 30 requests/min per IP

Get an API key at [awardtravelfinder.com/pricing](https://awardtravelfinder.com/pricing)

## Resources

- [Award Travel Finder](https://awardtravelfinder.com)
- [MCP Server Docs](https://mcp.awardtravelfinder.com)
- [Pricing & API Keys](https://awardtravelfinder.com/pricing)
