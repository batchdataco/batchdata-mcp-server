# BatchData MCP Server

[BatchData](https://batchdata.io/) is an API-first U.S. real estate data platform. The **BatchData MCP Server** is a hosted [Model Context Protocol](https://modelcontextprotocol.io) server that lets AI assistants and agents look up properties, pull comparables, search properties, skip trace owners and contacts, check phone compliance, verify and geocode addresses, and use property datasets and investor buy boxes, using plain-language requests.

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

The server registers 21 tools.

| Area | Tool | What it does |
| :-- | :-- | :-- |
| Property | `lookup_property` | Returns property details for a real-estate property based on its propertyId or its address as (street + city + state + zip) or its parcel number as (countyFipsCode + APN). |
| Comps | `comparable_property_count` | Returns the total count of comparable properties and aggregated metrics (estimatedValue, averagePrice, averagePricePerSqft) without returning individual comparable records. |
| Comps | `comparable_property_preview` | Returns a quick preview of the first 10 comparable properties with summary fields (address, price, sqft, beds/baths, sale date, distance), plus total count and aggregated metrics. |
| Comps | `comparable_property_page` | Paginated access to comparable properties with full details (page size: 10). |
| Comps | `comparable_property` | **Deprecated.** Use comparable_property_count, comparable_property_preview, or comparable_property_page instead. Returns all comparables, which can overload context windows. |
| Search | `search_properties_count` | Returns total count of properties matching search criteria and quicklist breakdowns. |
| Search | `search_properties_preview` | Returns a quick preview of the first 10 properties with essential fields, plus total count. |
| Search | `search_properties_page` | Paginated property search with full details (page size: 10). |
| Skip trace and contact | `skip_trace_property` | Returns contact information for the property owner and any other people associated with a real-estate property based on its address as (street + city + state + zip) or (street + city + state) or (street + zip) or its parcel number as (state + county + APN) or (countyFipsCode + APN). |
| Skip trace and contact | `reverse_skip_trace` | Returns associated person information (name, addresses, phones, emails) for one or more phone numbers or email addresses. |
| Phone compliance | `verify_phone` | Returns full verification details of a phone number including reachability, DNC status, carrier info, TCPA litigator status, and more. |
| Phone compliance | `check_dnc_status` | Checks only the DNC (Do Not Call) status of a phone number. |
| Phone compliance | `check_tcpa_status` | Checks only the TCPA litigator status of a phone number. |
| Address | `verify_address` | Accepts a property address in the format of street + city + state + zip, or street + city + state, or street + zip and returns an address formatted to comply with USPS conventions. |
| Address | `geocode_address` | Accepts a property address in the format of a single text string representing the street + city + state + zip, or street + city + state, or street + zip and returns the geo-coordinates for the requested address. |
| Address | `reverse_geocode_address` | Accepts geo-coordinates in the form of latitude and longitude values and returns the address at those coordinates. |
| Datasets and investor buy box | `list_property_datasets` | Returns all available property datasets with field counts and sample fields. |
| Datasets and investor buy box | `list_property_dataset_fields` | Returns the full list of field paths for a specific property dataset. |
| Datasets and investor buy box | `investor_buybox_count` | Returns the total count of investors matching the buy box criteria and aggregate result metadata, without returning individual investor records. This is not free: it bills for 1 record. |
| Datasets and investor buy box | `investor_buybox_preview` | Returns a quick preview of the first 10 ranked investor profiles matching the buy box criteria, plus total count and aggregate result metadata. |
| Datasets and investor buy box | `investor_buybox_page` | Paginated access to investors matching the buy box criteria with full details (page size: 10). |

Skip tracing (v3) must be enabled for your team by an admin, and API tokens need the matching endpoint permissions.

## Example prompts

- "Look up the property at 123 Main Street, Los Angeles, CA."
- "Find comparable properties for 789 Pine Road, Austin, TX."
- "Search for vacant properties in Miami, FL."
- "Skip trace the owner of 456 Oak Avenue, Miami, FL."
- "Verify this phone number and tell me whether it is on the Do Not Call list."
- "Verify and standardize this address: 100 main st los angeles ca."
- "Reverse skip trace the owner behind this phone number."
- "Which investors match the buy box for 123 Main Street, Los Angeles, CA?"

## Support

Questions or problems: **support@batchservice.com**. For API reference, see [developer.batchdata.com](https://developer.batchdata.com/).

## License

This repository contains documentation and configuration only, and is MIT licensed. The BatchData MCP server at mcp.batchdata.com, the BatchData API, and its data are proprietary and are governed by the BatchData terms of service.

© BatchData
