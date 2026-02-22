---
description: Compare loyalty program award charts and rates
argument-hint: "[program1] [program2]"
allowed-tools:
  - mcp__awardtravelfinder__list_programs
  - mcp__awardtravelfinder__get_program_rates
  - mcp__awardtravelfinder__get_pricing
---

# Compare Loyalty Programs

The user wants to compare loyalty program award charts.

## Arguments

The user invoked this command with: $ARGUMENTS

Parse arguments for program names or slugs. If none provided, list all programs and ask which to compare.

Program slugs: virgin-atlantic, virgin-partners, british-airways, qatar-airways, singapore-airlines, cathay-pacific, emirates, etihad, flying-blue, aeroplan, turkish-airlines, ana, jetblue, jet2-emirates

## Process

1. Use `list_programs` to show available programs if needed.
2. Use `get_program_rates` for each requested program.
3. If a route or region is mentioned, filter results to that area.
4. Present a comparison table: Destination/Region | Program A (Economy/Biz/First) | Program B
5. Highlight which program offers the best value for each cabin class.
6. Note any off-peak vs peak pricing differences.

## Examples

```
/atf:compare-programs british-airways emirates
/atf:compare-programs aeroplan flying-blue
/atf:compare-programs all
```
