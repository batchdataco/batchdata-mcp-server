---
name: dnc-tcpa-check
description: Check phone numbers for Do Not Call (DNC) status and TCPA litigator risk, and verify phone numbers, with BatchData. Use when the user asks whether a number is on the DNC list, is a known TCPA litigator, is reachable or a mobile line, or wants to screen a call or text list before outreach.
---

# Phone Check: DNC and TCPA Compliance

Use the BatchData MCP server to screen U.S. phone numbers before calling or texting.

## When to use

- "Is (555) 555-0100 on the DNC list?"
- "Is this number a TCPA litigator?"
- "Verify these phone numbers before we dial."

## Tools

| Tool | Use it to |
| :-- | :-- |
| `verify_phone` | Return full verification details: reachability, DNC status, carrier information, TCPA litigator status and more. Use when the user wants the whole picture. |
| `check_dnc_status` | Check only the Do Not Call status. Use when the user asks only about DNC. |
| `check_tcpa_status` | Check only the TCPA litigator status. Use when the user asks only about TCPA. |

## Steps

1. Normalize each number to a standard U.S. format (10 digits, or with country code +1).
2. Choose the narrowest tool that answers the question. Use `verify_phone` when the user wants reachability or carrier details as well.
3. Read each tool's input schema for the exact argument names. Check numbers one at a time unless the schema accepts a list.
4. Report each number with a clear result: clear, on the DNC list, flagged as a TCPA litigator, or could not be checked. Keep the flagged numbers at the top.

## Rules

- A "clear" result is a data check at the time of the lookup, not legal advice or a guarantee of compliance. Remind the user that calling and texting rules also cover consent, time-of-day limits, state laws and their own internal do-not-call lists, and that they should consult their compliance counsel.
- Recommend that flagged numbers are not contacted.
- Do not guess a result when a check fails; say it could not be checked.
- Read-only: these tools do not change anything.
