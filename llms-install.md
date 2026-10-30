# BatchData MCP Server: installation instructions for AI coding agents

BatchData is a hosted (remote) MCP server. There is nothing to clone, build or run locally.

- **Server URL:** `https://mcp.batchdata.com`
- **Transport:** Streamable HTTP
- **Authentication:** OAuth 2.1 browser sign-in with a BatchData account (PKCE, dynamic client registration). Clients that do not support OAuth can send the header `Authorization: Bearer <BatchData API token>`.
- **Account:** A BatchData account is required. Ask the user to sign in, or to provide an API token, if they do not have one yet. Never invent or guess a token.

## Add the server to the MCP settings file

Add this entry to the MCP servers configuration of your client (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "batchdata": {
      "type": "streamableHttp",
      "url": "https://mcp.batchdata.com",
      "disabled": false
    }
  }
}
```

If the client has no OAuth support, add a header with the user's token:

```json
{
  "mcpServers": {
    "batchdata": {
      "type": "streamableHttp",
      "url": "https://mcp.batchdata.com",
      "headers": { "Authorization": "Bearer YOUR_API_TOKEN_HERE" },
      "disabled": false
    }
  }
}
```

Clients that use a different JSON shape (for example `"type": "http"`) should keep the same URL and header.

## Verify

After connecting, the server exposes 21 tools, for example `lookup_property`, `search_properties_preview`, `skip_trace_property`, `verify_phone` and `verify_address`. A good first call is `verify_address` with a US street address. See the [README](README.md) for the full tool list and `docs/setup-guide.md` for troubleshooting.

Support: support@batchservice.com
