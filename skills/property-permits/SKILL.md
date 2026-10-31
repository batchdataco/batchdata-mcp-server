---
name: property-permits
description: Explain how to get building permit history for a U.S. property from the BatchData REST API. Use when the user asks for permits, renovation or remodel history, or permit details for an address. The BatchData MCP server has no permits tool, so this skill points to the API route.
---

# Building Permits Lookup (REST API route)

**There is no permits tool in the BatchData MCP server today.** The 21 MCP tools cover property lookup, comps, search, skip tracing, phone and address checks, datasets and investor buy box. Do not call an MCP tool for permits and do not pretend one exists.

Permit history is available from the BatchData REST API:

- Route: `POST https://api.batchdata.com/api/v2/property/get-property-permits`
- Auth: `Authorization: Bearer <BatchData API token>` (the user's own token, created in their BatchData account; never ask the user to paste it into chat if they can run the call themselves)
- Body: a JSON object with a `request` object that identifies the property, by address fields (house number, street, city, state, zip), by `propertyId`, or by `countyFipsCode` and `apn`. See the API reference for the full schema.
- Response: the permits on record for the property. The `resultCount` in the response meta says how many permits were returned.

## When to use

- "Show permit history for 123 Main St."
- "Has this house had a roof or HVAC permit?"

## Steps

1. Tell the user clearly that permits are not available through the MCP connector yet, and that the REST route above provides them.
2. If the user wants to proceed and can run requests, help them write the request (for example a `curl` command with a placeholder for the token) and read the response once they share the permit data.
3. For everything else about the property, use `property-lookup` through the MCP tools.

## Rules

- Never invent permit data or fall back to guessing from other fields.
- Never write a real API token into a file or message; use a placeholder such as `$BATCHDATA_API_TOKEN`.
