---
name: property-search-lead-lists
description: Search U.S. properties and build lead lists with BatchData. Use when the user asks how many properties match criteria, wants to find absentee owners, vacant or high-equity properties, off-market leads, or a list of properties by location, owner type, equity, price, or property type. Counts first, then previews, then pages.
---

# Property Search and Lead Lists

Use the BatchData MCP server to search U.S. properties by location, ownership, equity, price and other filters.

## When to use

- "How many absentee-owner single-family homes are in ZIP 85032?"
- "Search for vacant properties in Miami, FL."
- "Build a list of high-equity owners in Maricopa County."

Do not use for one specific address (use `property-lookup`) or for sold comparables (use `property-comps`). To get phone numbers or emails for the owners in a list, hand off to `skip-trace`.

## Tools

| Tool | Use it to |
| :-- | :-- |
| `search_properties_count` | Return the total number of matches plus quicklist breakdowns. Always start here. |
| `search_properties_preview` | Return the first 10 matches with essential fields, plus the total. |
| `search_properties_page` | Page through matches with full details, 10 per page. |
| `list_property_datasets` | See the available datasets and sample fields. |
| `list_property_dataset_fields` | See every field path in a dataset, to build a precise filter. |

## Steps

1. Turn the request into filters. If you need an exact field name, call `list_property_datasets` and `list_property_dataset_fields` first. Read each tool's input schema for the exact argument names.
2. Call `search_properties_count`. Tell the user the total and how it breaks down. If the total is very large or zero, suggest tightening or loosening a filter before going further.
3. Call `search_properties_preview` to show the first 10 and confirm the filters give the right kind of property.
4. Only call `search_properties_page` for more records when the user asks, and keep to the pages they need. Do not page through the whole result set unprompted.
5. Present results as a compact table. Offer next steps: skip trace the owners, verify phones, or find comps.

## Rules

- Count, preview, then page. Never start with a page call.
- Repeat the filters used with every result so the list is reproducible.
- Read-only: these tools do not change anything.
