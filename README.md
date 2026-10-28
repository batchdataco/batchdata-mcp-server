# BatchData MCP Server

[BatchData](https://batchdata.io/) is an API-first U.S. real estate data platform. The **BatchData MCP Server** is a hosted [Model Context Protocol](https://modelcontextprotocol.io) server that lets AI assistants and agents look up properties, pull comparables, search listings, skip trace owners, and verify phone numbers and addresses, using plain-language requests.

| | |
| :-- | :-- |
| **Server URL** | `https://mcp.batchdata.com` |
| **Transport** | Streamable HTTP (remote, hosted by BatchData; nothing to install or run locally) |
| **Authentication** | OAuth 2.1 browser sign-in with your BatchData account (PKCE, dynamic client registration), or a BatchData API token sent as `Authorization: Bearer <token>` |
| **Account** | A BatchData account is required. The MCP server is a usage-based offering; see [pricing](https://batchdata.io/pricing) or contact sales for access details. |
| **MCP Registry name** | `io.github.batchdataco/batchdata-mcp-server` |
| **Docs** | [batchdata.io/mcp-server](https://batchdata.io/mcp-server) · [developer.batchdata.com](https://developer.batchdata.com/) |
| **Support** | support@batchservice.com |

## Quick start

### Claude (Desktop and Web; connectors cannot be added from mobile)

1. Open **Settings → Connectors → Add custom connector**.
2. Enter the URL `https://mcp.batchdata.com` and click **Add**.
3. Sign in with your BatchData account when the browser opens.
4. In a chat, click **+** and toggle the **BatchData** connector on.

### Claude Code

```bash
claude mcp add --transport http batchdata https://mcp.batchdata.com
```

Then run `/mcp` inside Claude Code and choose **batchdata** to sign in.

### Cursor

[Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=batchdata&config=eyJ1cmwiOiJodHRwczovL21jcC5iYXRjaGRhdGEuY29tIn0=)

Or add this to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "batchdata": {
      "url": "https://mcp.batchdata.com"
    }
  }
}
```

Cursor opens a browser window to sign in the first time a tool is used.

### VS Code (GitHub Copilot)

Add this to `.vscode/mcp.json` in your workspace (or run **MCP: Add Server** from the Command Palette):

```json
{
  "servers": {
    "batchdata": {
      "type": "http",
      "url": "https://mcp.batchdata.com"
    }
  }
}
```

Or from a terminal:

```bash
code --add-mcp '{"name":"batchdata","type":"http","url":"https://mcp.batchdata.com"}'
```

### ChatGPT (Developer Mode)

Go to **Settings → Apps & Connectors → Advanced settings**, enable **Developer mode**, then **Create** a connector named `BatchData` with MCP Server URL `https://mcp.batchdata.com` and sign in with your BatchData account.

### Claude Desktop with an API token (clients without OAuth)

Claude Desktop can also reach the server through [`mcp-remote`](https://www.npmjs.com/package/mcp-remote) with your BatchData API token. Requires Node.js 22+.

```json
{
  "mcpServers": {
    "BatchData": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://mcp.batchdata.com",
        "--header",
        "Authorization:${AUTH_HEADER}"
      ],
      "env": {
        "AUTH_HEADER": "Bearer YOUR_API_TOKEN_HERE"
      }
    }
  }
}
```

Any other MCP client: point it at `https://mcp.batchdata.com` using the Streamable HTTP transport and, if it does not support OAuth, send the header `Authorization: Bearer YOUR_API_TOKEN_HERE`.

Step-by-step guides, migration from API tokens to OAuth, and troubleshooting are in [docs/setup-guide.md](docs/setup-guide.md).

## Tools

| Area | Tool | What it does |
| :-- | :-- | :-- |
| Property lookup | `lookup_property` | Detailed property information by property ID, address, or parcel number |
| Comparables | `comparable_property_count` | Count and aggregate metrics of comparable properties |
| Comparables | `comparable_property_preview` | Quick preview of the first 10 comparables with summary fields |
| Comparables | `comparable_property_page` | Paginated full comparable details (offset or cursor pagination) |
| Comparables | `comparable_property` | **Deprecated.** Returns all comparables at once. Use `comparable_property_preview` or `comparable_property_page`. |
| Property search | `search_properties_count` | Count of properties matching search criteria, with quicklist breakdowns |
| Property search | `search_properties_preview` | Quick preview of the first 10 matching properties |
| Property search | `search_properties_page` | Paginated property search with full details (offset or cursor pagination) |
| Contact information | `skip_trace_property` | Owner and contact information for a property by address or parcel number |
| Phone verification | `verify_phone` | Full verification: reachability, Do Not Call status, carrier, TCPA litigator status |
| Phone verification | `check_dnc_status` | Do Not Call status only |
| Phone verification | `check_tcpa_status` | TCPA litigator status only |
| Address processing | `verify_address` | Standardize and verify an address to USPS format |
| Address processing | `geocode_address` | Coordinates for an address |
| Address processing | `reverse_geocode_address` | Address for latitude/longitude coordinates |

Skip tracing (v3) must be enabled for your team by an admin, and API tokens need the matching endpoint permissions.

## Example prompts

- "Look up the property at 123 Main Street, Los Angeles, CA."
- "Find comparable properties for 789 Pine Road, Austin, TX."
- "Search for vacant properties in Miami, FL."
- "Skip trace the owner of 456 Oak Avenue, Miami, FL."
- "Verify this phone number and tell me whether it is on the Do Not Call list."
- "Verify and standardize this address: 100 main st los angeles ca."

## Support

Questions or problems: **support@batchservice.com**. For API reference, see [developer.batchdata.com](https://developer.batchdata.com/).

© BatchData
