---
name: property-comps
description: Find comparable sales (comps) for a U.S. property and estimate value per square foot with BatchData. Use when the user asks for comps, comparable properties, what similar homes sold for, an after-repair value (ARV) check, price per square foot, or a valuation sanity check for an address.
---

# Property Comps and Valuation Estimate

Use the BatchData MCP server to find comparable properties near a subject property and summarize the market evidence.

## When to use

- "Find comps for 789 Pine Road, Austin, TX."
- "What did similar homes nearby sell for in the last 6 months?"
- "What is the average price per square foot around this address?"

Do not use for owner or contact details (use `property-lookup` or `skip-trace`) or for lists of leads (use `property-search-lead-lists`).

## Tools

| Tool | Use it to |
| :-- | :-- |
| `comparable_property_count` | Return the total count of comparables plus aggregated metrics (estimatedValue, averagePrice, averagePricePerSqft) without individual records. Start here. |
| `comparable_property_preview` | Return the first 10 comparables with summary fields (address, price, square feet, beds and baths, sale date, distance), plus the total and aggregates. |
| `comparable_property_page` | Page through comparables with full detail, 10 per page. |
| `lookup_property` | Pull the subject property's own facts so the comps can be judged against it. |

Do not call `comparable_property` (deprecated). It returns every comparable and can overload the conversation.

## Steps

1. Call `lookup_property` for the subject address so you know its size, beds, baths and year built.
2. Call `comparable_property_count` with the subject and the user's criteria (distance, sale window, property type if given). Read the tool's input schema for the exact argument names.
3. Call `comparable_property_preview` to show the first 10. Only call `comparable_property_page` for more when the user asks.
4. Present a short table (address, sale price, sale date, square feet, price per square foot, distance) and the aggregate metrics from the count call.

## Rules

- Say which criteria were used (radius, dates, filters) so the user can reproduce the result.
- Treat `estimatedValue` and aggregates as data-derived estimates, not an appraisal. Do not present them as a formal valuation.
- Read-only: these tools do not change anything.
