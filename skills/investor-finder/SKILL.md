---
name: investor-finder
description: Find active real estate investors that match a buy box with BatchData. Use when the user asks which investors buy a property type in a county, city or ZIP, wants cash buyers or investor profiles for a deal, or wants to match a property to investors who buy that kind of asset.
---

# Real Estate Investor Finder

Use the BatchData MCP server to find ranked investor profiles that match a buy box (location, property type, price range and similar criteria).

## When to use

- "Which investors buy duplexes in Maricopa County?"
- "Which investors match the buy box for 123 Main Street, Los Angeles, CA?"
- "Find active buyers for a single-family flip in ZIP 85032."

Do not use to look up a property's owner (use `property-lookup` or `skip-trace`).

## Tools

| Tool | Use it to |
| :-- | :-- |
| `investor_buybox_count` | Return the total number of matching investors and aggregate result metadata, without individual records. Run it once per set of criteria. |
| `investor_buybox_preview` | Return the first 10 ranked investor profiles plus the total and aggregates. |
| `investor_buybox_page` | Page through matching investors with full details, 10 per page. |
| `lookup_property` | Pull the subject property's facts when the buy box is derived from a specific address. |

## Steps

1. Build the buy box from the user's request. If it comes from a specific property, call `lookup_property` first and use its location and type.
2. Call `investor_buybox_count` once. Tell the user the total and the aggregate metadata. If the count is zero or too broad, suggest changing the criteria.
3. Call `investor_buybox_preview` to show the top 10 ranked profiles.
4. Only call `investor_buybox_page` for more when the user asks.
5. Present a compact table of the investor profiles returned. Read each tool's input schema for the exact argument names.

## Rules

- Do not re-run the count call needlessly. Reuse its result.
- Investor profiles can include contact details of individuals; share only what the tool returns and keep it for the user's stated purpose. Before calling or texting, suggest the `dnc-tcpa-check` skill.
- Read-only: these tools do not change anything.
