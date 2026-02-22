# Award Travel Finder — Claude Code Plugin

Search award flight availability across British Airways, Qatar Airways, and Cathay Pacific directly from Claude Code. Compare 14 loyalty program award charts.

## Install

```
claude plugin add --marketplace jackculpan/award-travel-finder-plugin
```

## Commands

| Command | Description |
|---------|-------------|
| `/atf:search-flights` | Search award availability for a route and date |
| `/atf:compare-programs` | Compare loyalty program award charts |

### Examples

```
/atf:search-flights BA LHR JFK 2026-04-15
/atf:search-flights qatar DOH SIN 2026-05
/atf:compare-programs british-airways emirates
```

## Skills

The `award-travel` skill activates automatically when you ask about award flights, points, miles, or loyalty programs. Just ask naturally:

> "Find me business class from London to New York using Avios"

## API Key (Required)

Get your API key at [awardtravelfinder.com/pricing](https://awardtravelfinder.com/pricing) and add it to `~/.claude/mcp.json`:

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

## Supported Airlines

| Airline | Code | Currency |
|---------|------|----------|
| British Airways | BA | Avios |
| Qatar Airways | QR | Avios |
| Cathay Pacific | CX | Asia Miles |

## Loyalty Programs (14)

Virgin Atlantic, British Airways, Qatar Airways, Singapore Airlines, Cathay Pacific, Emirates, Etihad, Flying Blue, Aeroplan, Turkish Airlines, ANA, JetBlue, and more.

## Links

- [Award Travel Finder](https://awardtravelfinder.com)
- [MCP Server Docs](https://mcp.awardtravelfinder.com)
- [Pricing](https://awardtravelfinder.com/pricing)
