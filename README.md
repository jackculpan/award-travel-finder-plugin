# Award Travel Finder — Claude Code Plugin & MCP Server

Search award flight availability, compare loyalty programs, and find the best points redemptions — all from Claude Code. This plugin connects to the [Award Travel Finder](https://awardtravelfinder.com) MCP server to give Claude real-time access to award flight data across **19 airlines and 14 loyalty programs**.

**Works with Claude Code CLI, Claude Desktop, and any MCP-compatible client.** Learn more at [awardtravelfinder.com/claude](https://awardtravelfinder.com/claude).

## Quick Install

### Claude Code Plugin (recommended)

Inside Claude Code:

```
/plugin marketplace add jackculpan/award-travel-finder-plugin
/plugin install award-travel-finder
```

On first plugin use, Claude opens awardtravelfinder.com in your browser to sign you up via OAuth. Takes about 30 seconds — free, no credit card. Tokens auto-refresh after that.

Free tier: **50 searches/month** per account. Paid tiers (150/month and up) at [awardtravelfinder.com/pricing](https://awardtravelfinder.com/pricing) for power users.

### Manual MCP Server Setup (Claude Desktop, Cursor, etc.)

Add to your MCP client config:

```json
{
  "mcpServers": {
    "awardtravelfinder": {
      "type": "url",
      "url": "https://mcp.awardtravelfinder.com/mcp"
    }
  }
}
```

The server publishes `/.well-known/oauth-authorization-server`, so OAuth-aware clients sign you in on first call automatically. For clients without native OAuth, use `npx mcp-remote https://mcp.awardtravelfinder.com/mcp`.

### X-API-Key (legacy / server-to-server)

Header-based auth is still supported for users who configured it pre-OAuth, or for agents that don't run a browser:

```json
{
  "mcpServers": {
    "awardtravelfinder": {
      "type": "url",
      "url": "https://mcp.awardtravelfinder.com/mcp",
      "headers": {
        "X-API-Key": "atf_..."
      }
    }
  }
}
```

Generate a key at [awardtravelfinder.com/pricing](https://awardtravelfinder.com/pricing).

## What You Can Do

### Search Award Flights

Ask Claude naturally or use slash commands:

```
"Find business class from London to New York using Avios"
"Search for first class availability on Qatar Airways from Doha to Singapore in June"
"Pull a monthly calendar of LHR→HND business class for May 2027"
"Cheapest way to fly business JFK→NRT in November under 100k points?"
```

Or use the command:

```
/atf:search-flights BA LHR JFK 2026-06-15
/atf:search-flights qatar DOH SIN 2026-07
```

### Compare Loyalty Programs

```
"Compare British Airways Avios vs Emirates Skywards for flights to Dubai"
"Which program has the cheapest business class to Tokyo?"
"For LHR→HND in business, compare Avios, Aeroplan, Flying Blue, and Virgin"
```

```
/atf:compare-programs british-airways emirates
/atf:compare-programs aeroplan flying-blue
```

### Check Award Pricing

```
"How many Avios do I need for London to New York in business?"
"Show me the Qatar Airways award chart"
```

## MCP Tools (21)

Verified against the live MCP server source.

### Flight search

| Tool | Description |
|------|-------------|
| `search_availability` | Award seats for one route + date across all supported airlines. |
| `search_monthly_availability` | Calendar view for a whole month, one airline. Up to 90s. |
| `search_all_airlines` | Fan out a single date across every supported airline at once. |
| `search_hybrid` | Cash + points side-by-side, with hub/connection logic for split-ticket journeys. |
| `get_pricing` | Price a route in any of 14 loyalty programs, including taxes and fuel surcharges. |

### Loyalty programs

| Tool | Description |
|------|-------------|
| `get_program_rates` | Award chart for one program (zones, cabin pricing, partner rules). |
| `get_buy_points_pricing` | Current "buy miles" promotions, in case it's cheaper than redeeming. |
| `get_status_matches` | Which programs will status-match a given tier, and how long it lasts. |

### Hotels

| Tool | Description |
|------|-------------|
| `search_hotels` | Find hotels by city/area for a date range. |
| `get_hotel_availability` | Award nights at a specific property. |
| `monitor_hotel_price` | Watch a property and ping you on price drops. |
| `list_hotel_bookings` | Track hotel award reservations. |
| `get_hotel_booking` | Fetch a single saved hotel booking. |

### Trip portfolio (per user)

| Tool | Description |
|------|-------------|
| `add_flight_booking` / `list_flight_bookings` / `get_flight_booking` | Track flight bookings across programs. |
| `update_flight_booking` / `delete_flight_booking` | Edit or remove tracked bookings. |
| `update_points_balance` / `list_points_balances` / `get_portfolio` | Track miles balances and total portfolio value. |

## Supported Airlines (19)

Full availability and award charts for the airlines below. Some airlines (BA, Qatar, Cathay, Virgin, Iberia, Qantas) have full availability + monthly calendars; others (American, Alaska, JetBlue, Etihad, Emirates) have a subset.

**Oneworld** — British Airways (BA), Cathay Pacific (CX), Iberia (IB), Qatar Airways (QR), American Airlines (AA), Alaska Airlines (AS), Qantas (QF), Japan Airlines (JL)

**SkyTeam** — Air France / KLM, Korean Air

**Star Alliance** — Singapore Airlines, ANA, Turkish Airlines, Aeroplan / Air Canada

**Non-aligned / partners** — Virgin Atlantic (VS), Emirates (EK), Etihad (EY), JetBlue (B6), Frontier (F9)

## Loyalty Programs (14)

| Program | Slug | Currency |
|---------|------|----------|
| British Airways | `british-airways` | Avios |
| Iberia | `iberia` | Avios |
| Qatar Airways | `qatar-airways` | Avios |
| Aer Lingus | `aer-lingus` | Avios |
| Virgin Atlantic | `virgin-atlantic` | Virgin Points |
| Aeroplan | `aeroplan` | Aeroplan Points |
| Flying Blue | `flying-blue` | Flying Blue Miles |
| Cathay Pacific | `cathay-pacific` | Asia Miles |
| Singapore Airlines | `singapore-airlines` | KrisFlyer Miles |
| Emirates | `emirates` | Skywards Miles |
| Etihad | `etihad` | Guest Miles |
| Turkish Airlines | `turkish-airlines` | Miles & Smiles |
| ANA | `ana` | Mileage Club |
| JetBlue | `jetblue` | TrueBlue Points |

## Skills

This plugin includes an `award-travel` skill that activates automatically when you mention award flights, points, miles, loyalty programs, or specific airlines. No slash command needed — just ask Claude.

## Plugin Structure

```
award-travel-finder-plugin/
  .claude-plugin/
    plugin.json          # Plugin metadata
    marketplace.json     # Marketplace listing
  .mcp.json              # MCP server connection config
  commands/
    search-flights.md    # /atf:search-flights command
    compare-programs.md  # /atf:compare-programs command
  skills/
    award-travel/
      SKILL.md           # AI skill for natural language queries
      references/
        airlines.md      # Airline reference data
        programs.md      # Loyalty program reference data
```

## How It Works

This plugin connects Claude Code to the [Award Travel Finder MCP server](https://mcp.awardtravelfinder.com), which provides real-time award flight availability data. The MCP (Model Context Protocol) server runs on Cloudflare Workers and queries airline APIs to find available award seats. Some airlines are cached up to 4 hours to avoid bot-blocking; cached results are marked in the response.

## Links

- [Award Travel Finder for Claude Code](https://awardtravelfinder.com/claude) — Plugin landing page with example prompts
- [Award Travel Finder](https://awardtravelfinder.com) — Full web app
- [MCP Server](https://mcp.awardtravelfinder.com) — API documentation
- [Transfer Bonus Tracker](https://awardtravelfinder.com/transfer-bonuses) — Current transfer bonuses with predictions
- [Pricing](https://awardtravelfinder.com/pricing) — Free tier (50/mo) and paid tiers

## License

MIT
