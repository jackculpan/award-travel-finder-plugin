# Award Travel Finder — Claude Code Plugin & MCP Server

Search award flight availability, compare loyalty programs, and find the best points redemptions — all from Claude Code. This plugin connects to the [Award Travel Finder](https://awardtravelfinder.com) MCP server to give Claude real-time access to award flight data.

**Works with Claude Code CLI, Claude Desktop, and any MCP-compatible client.**

## Quick Install

### Claude Code Plugin (recommended)

```bash
claude plugin add award-travel-finder
```

### Manual MCP Server Setup

Add to your `~/.claude/mcp.json` or Claude Desktop config:

```json
{
  "mcpServers": {
    "awardtravelfinder": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.awardtravelfinder.com/mcp"]
    }
  }
}
```

### With API Key (for unlimited searches)

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

Get your API key at [awardtravelfinder.com/pricing](https://awardtravelfinder.com/pricing).

## What You Can Do

### Search Award Flights

Ask Claude naturally or use slash commands:

```
"Find business class from London to New York using Avios"
"Search for first class availability on Qatar Airways from Doha to Singapore in June"
"Are there any award seats on Cathay Pacific HKG-LHR next month?"
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

## MCP Tools

| Tool | Description | Auth Required |
|------|-------------|---------------|
| `search_availability` | Search award seats for a route and date | Yes |
| `search_monthly_availability` | Search an entire month for availability | Yes |
| `search_hybrid` | Search multiple airlines at once | Yes |
| `get_pricing` | Get award chart pricing for a route | No |
| `get_airports` | List airports an airline serves | No |
| `list_supported_airlines` | List searchable airlines | No |
| `list_programs` | List all 14 loyalty programs | No |
| `get_program_rates` | Get full award chart for a program | No |
| `get_portfolio` | View your points portfolio | Yes |
| `list_points_balances` | List your points balances | Yes |
| `get_buy_points_pricing` | Check buy points deals | No |
| `get_status_matches` | Find airline status match opportunities | No |
| `search_hotels` | Search hotel award availability | Yes |
| `get_hotel_availability` | Check hotel points pricing | Yes |

## Supported Airlines

| Airline | Code | Award Currency |
|---------|------|----------------|
| British Airways | BA | Avios |
| Qatar Airways | QR | Avios |
| Cathay Pacific | CX | Asia Miles |
| Iberia | IB | Avios |
| Alaska Airlines | AS | Mileage Plan Miles |
| American Airlines | AA | AAdvantage Miles |
| Virgin Atlantic | VS | Virgin Points |
| Emirates | EK | Skywards Miles |
| Qantas | QF | Qantas Points |

*+ 10 more airlines via hybrid search*

## Loyalty Programs (14)

| Program | Slug | Currency |
|---------|------|----------|
| British Airways | `british-airways` | Avios |
| Virgin Atlantic | `virgin-atlantic` | Virgin Points |
| Qatar Airways | `qatar-airways` | Avios |
| Cathay Pacific | `cathay-pacific` | Asia Miles |
| Singapore Airlines | `singapore-airlines` | KrisFlyer Miles |
| Emirates | `emirates` | Skywards Miles |
| Etihad | `etihad` | Guest Miles |
| Flying Blue | `flying-blue` | Flying Blue Miles |
| Aeroplan | `aeroplan` | Aeroplan Points |
| Turkish Airlines | `turkish-airlines` | Miles&Smiles |
| ANA | `ana` | ANA Miles |
| JetBlue | `jetblue` | TrueBlue Points |
| Virgin Partners | `virgin-partners` | Virgin Points |
| Jet2 Emirates | `jet2-emirates` | Emirates Miles |

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

This plugin connects Claude Code to the [Award Travel Finder MCP server](https://mcp.awardtravelfinder.com), which provides real-time award flight availability data. The MCP (Model Context Protocol) server runs on Cloudflare Workers and queries airline APIs to find available award seats.

## Links

- [Award Travel Finder](https://awardtravelfinder.com) — Full web app with 19 airline searches
- [MCP Server](https://mcp.awardtravelfinder.com) — API documentation
- [Transfer Bonus Tracker](https://awardtravelfinder.com/transfer-bonuses) — Current transfer bonuses with predictions
- [Pricing](https://awardtravelfinder.com/pricing) — API key for unlimited searches

## License

MIT
