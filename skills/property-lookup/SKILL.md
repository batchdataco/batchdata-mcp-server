---
name: property-lookup
description: Look up U.S. property records with BatchData. Use when the user asks who owns a property, its valuation or estimated value, mortgage and equity, last sale, taxes, or building facts (beds, baths, square feet, year built) for a U.S. address, parcel number (APN) or property ID. Also standardizes and geocodes addresses.
---

# Property Lookup: U.S. Real Estate Data

Use the BatchData MCP server (`https://mcp.batchdata.com`, tools appear under the `batchdata` server) to pull facts for one U.S. property.

## When to use

- "Who owns 123 Main St, Phoenix AZ 85004?" or "What was the last sale price?"
- Estimated value, mortgage, equity, tax, ownership and building details for an address, parcel (county FIPS code + APN) or property ID.
- Cleaning up a messy address, or converting between an address and coordinates.

Do not use for comparable sales (use `property-comps`), searching many properties (use `property-search-lead-lists`), or owner phone numbers and emails (use `skip-trace`).

## Tools

| Tool | Use it to |
| :-- | :-- |
| `lookup_property` | Return property details for a property ID, a full address (street, city, state, zip), or a parcel (county FIPS code + APN). |
| `verify_address` | Standardize an address to USPS conventions (accepts street + city + state + zip, street + city + state, or street + zip). Run it first when the user's address looks incomplete or misspelled. |
| `geocode_address` | Return latitude and longitude for an address. |
| `reverse_geocode_address` | Return the address at a latitude and longitude. |
| `list_property_datasets` | List the available property datasets with field counts and sample fields. |
| `list_property_dataset_fields` | List every field path in one dataset, to find the exact field a user asks about. |

## Steps

1. If the address is ambiguous or partial, call `verify_address` and confirm the standardized address with the user when more than one match is plausible.
2. Call `lookup_property` with the address, parcel, or property ID. Read the tool's input schema for the exact argument names.
3. If the user asks about a specific attribute you cannot find in the result, call `list_property_datasets`, then `list_property_dataset_fields` for the relevant dataset, and look there.
4. Summarize the answer in plain language first (owner, estimated value, last sale, mortgage, key building facts), then offer the full detail.

## Rules

- Report only what the tool returns. If a field is empty, say it is not available; do not estimate or guess.
- State the data source is BatchData and that records can lag county filings.
- Read-only: these tools do not change anything.
