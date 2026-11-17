# BatchData MCP Server

This extension connects Gemini CLI to the hosted BatchData MCP server at `https://mcp.batchdata.com` (Streamable HTTP). It gives U.S. real estate data: property lookup, comparable sales, property search and lead lists, owner skip tracing, DNC and TCPA phone checks, address verification and geocoding, property datasets, and investor buy boxes.

- A BatchData account is required. If the `batchdata` tools are missing or return an authentication error, tell the user to run `/mcp auth batchdata` and sign in with their BatchData account in the browser.
- The server is a usage-based offering. Tool calls run against the user's BatchData account. `investor_buybox_count` bills for 1 record.
- To save context and usage, call a `*_count` or `*_preview` tool before a `*_page` tool. Do not use the deprecated `comparable_property` tool.
- Skip tracing must be enabled for the user's team by an admin.
- The server has no building permits tool. Permits are available only through the BatchData REST API.
