---
name: skip-trace
description: Skip trace property owners with BatchData. Use when the user asks for the phone numbers, emails or mailing addresses of the owner of a U.S. property, wants to find who is associated with a property, or wants a reverse lookup from a phone number or email address to a person.
---

# Skip Tracing: Find Property Owner Contacts

Use the BatchData MCP server to return contact information for the owner of a U.S. property, or to look up the person behind a phone number or email address.

## When to use

- "Skip trace the owner of 456 Oak Avenue, Miami, FL."
- "Find a phone number and email for the owner of this parcel."
- "Who is associated with this phone number?" (reverse skip trace)

Do not use for property facts only (use `property-lookup`). Do not use to collect Social Security numbers, financial account data, or information for harassment, stalking or any unlawful purpose.

## Tools

| Tool | Use it to |
| :-- | :-- |
| `skip_trace_property` | Return contact information for the owner and other people associated with a property. Accepts an address (street + city + state + zip, street + city + state, or street + zip) or a parcel (state + county + APN, or county FIPS code + APN). |
| `reverse_skip_trace` | Return associated person information (name, addresses, phones, emails) for one or more phone numbers or email addresses. |
| `verify_address` | Standardize an address before tracing. |
| `verify_phone`, `check_dnc_status`, `check_tcpa_status` | Check any phone number before using it for outreach (see `dnc-tcpa-check`). |

Skip tracing must be enabled for the user's BatchData team by an admin, and API tokens need the matching endpoint permission. If the tool returns a permission error, tell the user that and stop; do not retry with other inputs.

## Steps

1. Confirm the user has a legitimate purpose and the right to contact the person. If the purpose is unclear or looks unlawful, decline.
2. Standardize the address with `verify_address` if it looks partial.
3. Call `skip_trace_property` (or `reverse_skip_trace`). Read the tool's input schema for the exact argument names.
4. Present the contacts grouped by person, and keep to the fields the user asked for.
5. Before the user calls or texts anyone, recommend running the numbers through `check_dnc_status` and `check_tcpa_status`.

## Rules

- Return only the personal data the user needs. Do not add data from other sources.
- Handle results as personal information: do not repeat it into unrelated tools or files.
- Contact data can be out of date or wrong. Say so when relevant.
- Read-only: these tools do not change anything.
