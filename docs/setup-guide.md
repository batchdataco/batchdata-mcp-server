# BatchData Remote MCP Server Setup Guide

* 1 [Introduction](#Introduction)
* 2 [Authentication Methods](#Authentication-Methods)
  * 2.1 [OAuth Authentication (Recommended)](#OAuth-Authentication-\(Recommended\))
  * 2.2 [API Token Authentication (Alternative)](#API-Token-Authentication-\(Alternative\))
* 3 [Future Enhancement: OAuth Access Control (Coming Soon)](#Future-Enhancement%3A-OAuth-Access-Control-\(Coming-Soon\))
* 4 [OAuth Setup (Recommended)](#OAuth-Setup-\(Recommended\))
  * 4.1 [Prerequisites](#Prerequisites)
  * 4.2 [Claude Setup (Desktop, Web & Mobile)](#Claude-Setup-\(Desktop%2C-Web-%26-Mobile\))
    * 4.2.1 [Step 1: Add the BatchData Connector](#Step-1%3A-Add-the-BatchData-Connector)
    * 4.2.2 [Step 2: Authenticate](#Step-2%3A-Authenticate)
    * 4.2.3 [Step 3: Enable the Connector](#Step-3%3A-Enable-the-Connector)
    * 4.2.4 [Step 4: Approve Initial Tool Use](#Step-4%3A-Approve-Initial-Tool-Use)
    * 4.2.5 [Using on Mobile](#Using-on-Mobile)
    * 4.2.6 [Subsequent Connections](#Subsequent-Connections)
  * 4.3 [Cursor Setup](#Cursor-Setup)
  * 4.4 [Claude Code Setup](#Claude-Code-Setup)
  * 4.5 [ChatGPT Setup (Developer Mode)](#ChatGPT-Setup-\(Developer-Mode\))
    * 4.5.1 [Prerequisites](#Prerequisites.1)
    * 4.5.2 [Step 1: Enable Developer Mode](#Step-1%3A-Enable-Developer-Mode)
    * 4.5.3 [Step 2: Create the BatchData Connector](#Step-2%3A-Create-the-BatchData-Connector)
    * 4.5.4 [Step 3: Authenticate](#Step-3%3A-Authenticate)
    * 4.5.5 [Using BatchData Tools in ChatGPT](#Using-BatchData-Tools-in-ChatGPT)
    * 4.5.6 [Managing the Connection](#Managing-the-Connection)
  * 4.6 [Verification](#Verification)
* 5 [API Token Setup (Alternative)](#API-Token-Setup-\(Alternative\))
  * 5.1 [Prerequisites](#Prerequisites.2)
  * 5.2 [Claude Desktop Setup with API Token](#Claude-Desktop-Setup-with-API-Token)
    * 5.2.1 [Step 1: Install Node.js 22](#Step-1%3A-Install-Node.js-22)
    * 5.2.2 [Step 2: Configure Claude Desktop](#Step-2%3A-Configure-Claude-Desktop)
  * 5.3 [Custom MCP Client Setup](#Custom-MCP-Client-Setup)
* 6 [Migrating from API Token to OAuth](#Migrating-from-API-Token-to-OAuth)
  * 6.1 [Claude Desktop](#Claude-Desktop)
  * 6.2 [Claude Code](#Claude-Code)
  * 6.3 [ChatGPT](#ChatGPT)
  * 6.4 [Benefits of Migrating](#Benefits-of-Migrating)
* 7 [Available Tools](#Available-Tools)
  * 7.1 [Property](#Property)
  * 7.2 [Comps](#Comps)
  * 7.3 [Search](#Search)
  * 7.4 [Skip trace and contact](#Skip-trace-and-contact)
  * 7.5 [Phone compliance](#Phone-compliance)
  * 7.6 [Address](#Address)
  * 7.7 [Datasets and investor buy box](#Datasets-and-investor-buy-box)
* 8 [Troubleshooting](#Troubleshooting)
  * 8.1 [OAuth Issues](#OAuth-Issues)
  * 8.2 [ChatGPT Issues](#ChatGPT-Issues)
  * 8.3 [API Token Issues](#API-Token-Issues)
  * 8.4 [General Issues](#General-Issues)
  * 8.5 [Getting Help](#Getting-Help)

## Introduction

This guide documents how to connect to the BatchData Remote MCP Server using your MCP-compatible client.

## Authentication Methods

The BatchData MCP Server supports two authentication methods:

| Method | Setup Complexity | Security | Recommended For |
| :-- | :-- | :-- | :-- |
| OAuth (Recommended) | Simple | High | Most users |
| API Token | Manual configuration | Moderate | Custom MCP clients, debugging |

### OAuth Authentication (Recommended)

OAuth provides a streamlined connection experience:

* **No API token configuration needed** — Just provide the server URL
* **Browser-based login** — Authenticate with your BatchData account credentials
* **Automatic token management** — Access tokens refresh automatically
* **Familiar login experience** — Use email/password or Google Sign-In
  

### API Token Authentication (Alternative)

For users who prefer direct API token configuration or are using custom MCP clients that don't support OAuth:

* Requires obtaining and configuring your BatchData API token manually
* Token must be managed and protected as a sensitive credential
* Useful for debugging, automation scripts, or clients without OAuth support
  

## Future Enhancement: OAuth Access Control (Coming Soon)

We are developing enhanced access control features for OAuth authentication:

* **Permission verification** — OAuth login will automatically verify whether your account has been granted permission to use the MCP server
* **Centralized access management** — Team owners will be able to grant or revoke MCP server access for team members through the BatchData platform
  

* * *

## OAuth Setup (Recommended)

### Prerequisites

* A BatchData account with valid credentials
* An MCP-compatible client (Claude Desktop/Web/Mobile, ChatGPT, Cursor, Claude Code, or similar)
  

### Claude Setup (Desktop, Web & Mobile)

Claude supports MCP servers through the desktop app, web interface, and mobile app.

> **Mobile Note**: Connectors cannot be added from the mobile app. Add the connector on Desktop or Web first, and it will automatically be available on mobile for the same account.

> **Teams/Enterprise Note**: Workspace admins must first add the BatchData connector to the list of available connectors before team members can configure it. Contact your admin if you don't see the connector in your list.

#### Step 1: Add the BatchData Connector

1. Open Claude (Desktop or Web)
2. Go to **Settings → Connectors** (or **Settings → MCP Servers**)
3. Click **Add Connector** (or **Add Server**)
4. Enter the server URL:
  ```
  https://mcp.batchdata.com
  ```
5. Click **Add** or **Connect**
  

#### Step 2: Authenticate

1. Your browser will open to the BatchData login page
2. Sign in using either:
  * **Email and password** — Enter your BatchData account credentials
  * **Google Sign-In** — Click the Google button to authenticate
3. After successful login, you'll be redirected back to Claude
  

#### Step 3: Enable the Connector

Connectors are **not enabled by default** after adding them. Enable it once and the setting is saved:

1. Open any chat
2. Click the **+** button (or connectors icon) in the chat input area
3. Find **BatchData** in the list of available connectors
4. Toggle it **on** to enable it
  

The connector will now be available in all your conversations.

#### Step 4: Approve Initial Tool Use

The first time Claude uses any BatchData tool, you'll be asked to approve it:

1. When Claude attempts to use a tool, a permission prompt will appear
2. Review the tool and action being requested
3. Click **Allow** to approve
4. Select **"Always allow"** if you want to skip approval for future uses of that tool
  

> **Note**: After initial approval (or selecting "Always allow"), subsequent tool uses won't require additional confirmation.

#### Using on Mobile

Once you've added and authenticated the connector on Desktop or Web:

* Open the Claude mobile app with the same account
* The BatchData connector will be available in your connector list
* If not already enabled, toggle it on via the **+** button in the chat input (setting syncs across devices)
* Tool approvals granted on Desktop/Web carry over to mobile
* All tools work the same as on Desktop/Web
  

#### Subsequent Connections

After initial authentication:

* Access tokens are cached and refresh automatically across all devices
* You won't need to log in again unless your session expires (typically after 14 days of inactivity)
* If prompted to re-authenticate, simply log in again through your browser (on Desktop or Web)
  

### Cursor Setup

1. Open Cursor Settings
2. Navigate to the MCP configuration section
3. Click **Add MCP Server**
4. Enter the server URL:
  ```
  https://mcp.batchdata.com
  ```
5. On first use, authenticate through the browser popup
  

### Claude Code Setup

Add the BatchData MCP server directly via the CLI:

```
claude mcp add --transport http batchdata https://mcp.batchdata.com
```

On first use, you'll be prompted to authenticate through your browser.

### ChatGPT Setup (Developer Mode)

ChatGPT supports MCP servers through [Developer Mode](https://platform.openai.com/docs/guides/developer-mode "https://platform.openai.com/docs/guides/developer-mode"), which provides full [Model Context Protocol](https://platform.openai.com/docs/mcp "https://platform.openai.com/docs/mcp") client support.

#### Prerequisites

* A ChatGPT Plus or Pro subscription
* For Business/Enterprise: Admin must enable developer mode in Workspace Settings
  

#### Step 1: Enable Developer Mode

1. Open [ChatGPT](https://chatgpt.com/ "https://chatgpt.com/")
2. Go to **Settings → Apps & Connectors → Advanced settings**
3. Toggle **Developer mode** to on
  

**For Business/Enterprise workspaces:**

* Admins must first enable developer mode from **Workspace Settings → Permissions & Roles → Connected Data → Developer mode / Create custom MCP connectors**
  

#### Step 2: Create the BatchData Connector

1. In ChatGPT, go to **Settings → Connectors**
2. Click **Create**
3. Enter the following details:
  * **Connector name**: `BatchData`
  * **MCP Server URL**: `https://mcp.batchdata.com`
4. Click **Create**
  

#### Step 3: Authenticate

1. After creating the connector, ChatGPT will prompt you to authenticate
2. Your browser will open to the BatchData login page
3. Sign in using either:
  * **Email and password** — Enter your BatchData account credentials
  * **Google Sign-In** — Click the Google button to authenticate
4. After successful login, you'll be redirected back to ChatGPT
5. The BatchData connector is now ready to use
  

#### Using BatchData Tools in ChatGPT

Once connected, you can use BatchData tools in conversations:

1. Start a new chat
2. Click the **+** button, then select your connector from the **More** menu
3. Alternatively, choose **Developer mode** from the **Plus menu** and select BatchData
4. Ask property-related questions — ChatGPT will use the appropriate tools
  

**Example prompts:**

* "Look up the property at 123 Main Street, Los Angeles, CA"
* "Find comparable properties for 456 Oak Avenue"
* "Skip trace the owner of 789 Pine Road, Miami, FL"
  

#### Managing the Connection

* **To disconnect**: Go to **Settings → Connectors**, click BatchData, and disconnect
* **To reconnect**: Click the connector and re-authenticate
* **Session expiry**: If your session expires (typically after 14 days), you'll be prompted to reconnect
  

### Verification

Once connected, simply ask about property data or skip-tracing and the LLM will automatically use the BatchData tools.

**Example prompts:**

* "Look up the property at 123 Main Street, Los Angeles, CA"
* "Skip trace the owner of 456 Oak Avenue, Miami, FL"
* "Find comparable properties for 789 Pine Road, Austin, TX"
* "Search for vacant properties in Miami, FL"
* "Verify this phone number: 555-123-4567"
* "Verify and standardize this address: 100 main st los angeles ca"
* "Get the coordinates for 200 Park Avenue, New York, NY"
  

Claude or ChatGPT will recognize the intent and use the appropriate BatchData tools to fetch the information.

* * *

## API Token Setup (Alternative)

Use this method if:

* Your MCP client doesn't support OAuth
* You need to debug or automate MCP server connections
* You prefer explicit token management
  

### Prerequisites

* Your BatchData API Token (obtain from the BatchData Web App)
* An MCP-compatible client
* Node.js 22+ (for Claude Desktop)
  

### Claude Desktop Setup with API Token

#### Step 1: Install Node.js 22

Claude Desktop's bundled Node.js is outdated. Install Node.js 22 separately:

**macOS/Linux:**

```
# Install Volta (Node.js version manager)
curl https://get.volta.sh | bash
# Restart terminal, then install Node.js 22
volta install node@22
# Find your username for the config below
whoami
```

**Windows:**

Download and install Node.js 22.x LTS from [nodejs.org](https://nodejs.org/ "https://nodejs.org/")

#### Step 2: Configure Claude Desktop

1. Open Claude Desktop
2. Go to **Settings > Developer > Edit Config**
3. Add the following configuration:
  

**macOS Configuration:**

```
{ "mcpServers": { "BatchData": { "command": "/Users/YOUR_USERNAME/.volta/bin/npx", "args": [ "-y", "mcp-remote", "https://mcp.batchdata.com", "--header", "Authorization:${AUTH_HEADER}" ], "env": { "AUTH_HEADER": "Bearer YOUR_API_TOKEN_HERE" } } } }
```

**Linux Configuration:**

```
{ "mcpServers": { "BatchData": { "command": "/home/YOUR_USERNAME/.volta/bin/npx", "args": [ "-y", "mcp-remote", "https://mcp.batchdata.com", "--header", "Authorization:${AUTH_HEADER}" ], "env": { "AUTH_HEADER": "Bearer YOUR_API_TOKEN_HERE" } } } }
```

**Windows Configuration:**

```
{ "mcpServers": { "BatchData": { "command": "C:\\Program Files\\nodejs\\npx.cmd", "args": [ "-y", "mcp-remote", "https://mcp.batchdata.com", "--header", "Authorization:${AUTH_HEADER}" ], "env": { "AUTH_HEADER": "Bearer YOUR_API_TOKEN_HERE" } } } }
```

4. Replace `YOUR_USERNAME` with your actual username
5. Replace `YOUR_API_TOKEN_HERE` with your BatchData API Token
6. Save the file and restart Claude Desktop
  

### Custom MCP Client Setup

For custom MCP client implementations:

**Connection Details:**

| Setting | Value |
| :-- | :-- |
| Server URL | https://mcp.batchdata.com |
| Transport | Streamable HTTP |
| Authentication | Bearer token via Authorization header |

**Configuration Example:**

```
{ "server_url": "https://mcp.batchdata.com", "headers": { "Authorization": "Bearer YOUR_API_TOKEN_HERE" } }
```

**Using npx:**

```
npx mcp-remote https://mcp.batchdata.com --header "Authorization:Bearer YOUR_API_TOKEN_HERE"
```

* * *

## Migrating from API Token to OAuth

If you previously set up BatchData using the API token method and want to switch to OAuth for a simpler experience, follow these steps:

### Claude Desktop

1. Open Claude Desktop
2. Go to **Settings → Developer → Edit Config**
3. Remove the existing BatchData configuration (the entire block with `command`, `args`, and `env`)
4. Save and close the config file
5. Follow the [Claude Setup (Desktop, Web & Mobile)](#Claude-Setup-\(Desktop,-Web-&-Mobile\) "#Claude-Setup-(Desktop,-Web-&-Mobile)") instructions to add the connector via the UI
6. Authenticate with your BatchData account when prompted
  

**Before (API Token):**

```
{ "mcpServers": { "BatchData": { "command": "/Users/YOUR_USERNAME/.volta/bin/npx", "args": ["-y", "mcp-remote", "https://mcp.batchdata.com", "--header", "Authorization:${AUTH_HEADER}"], "env": { "AUTH_HEADER": "Bearer YOUR_API_TOKEN" } } } }
```

**After (OAuth):** Configured via UI — no JSON editing required.

### Claude Code

1. Remove the existing configuration:
  ```
  claude mcp remove BatchData
  ```
2. Add it back using OAuth:
  ```
  claude mcp add --transport http batchdata https://mcp.batchdata.com
  ```
3. Authenticate through your browser when prompted
  

### ChatGPT

If you were using a workaround with API tokens, simply:

1. Remove any existing BatchData connector from **Settings → Connectors**
2. Follow the [ChatGPT Setup](#ChatGPT-Setup-\(Developer-Mode\) "#ChatGPT-Setup-(Developer-Mode)") instructions to create a new connector
3. Authenticate with your BatchData account
  

### Benefits of Migrating

| Aspect | API Token | OAuth |
| :-- | :-- | :-- |
| Setup | Manual JSON editing | Simple UI flow |
| Token management | Manual rotation | Automatic refresh |
| Security | Token stored in config file | Tokens managed by client |
| Multi-device | Configure each device | Syncs across devices |

* * *

## Available Tools

Once connected, the BatchData MCP Server registers the following 21 tools:

### Property

| Tool | Description |
| :-- | :-- |
| lookup_property | Returns property details for a real-estate property based on its propertyId or its address as (street + city + state + zip) or its parcel number as (countyFipsCode + APN). |

### Comps

| Tool | Description |
| :-- | :-- |
| comparable_property_count | Returns the total count of comparable properties and aggregated metrics (estimatedValue, averagePrice, averagePricePerSqft) without returning individual comparable records. |
| comparable_property_preview | Returns a quick preview of the first 10 comparable properties with summary fields (address, price, sqft, beds/baths, sale date, distance), plus total count and aggregated metrics. |
| comparable_property_page | Paginated access to comparable properties with full details (page size: 10). |
| comparable_property | **Deprecated.** Use comparable_property_count, comparable_property_preview, or comparable_property_page instead. Returns all comparables, which can overload context windows. |

### Search

| Tool | Description |
| :-- | :-- |
| search_properties_count | Returns total count of properties matching search criteria and quicklist breakdowns. |
| search_properties_preview | Returns a quick preview of the first 10 properties with essential fields, plus total count. |
| search_properties_page | Paginated property search with full details (page size: 10). |

### Skip trace and contact

| Tool | Description |
| :-- | :-- |
| skip_trace_property | Returns contact information for the property owner and any other people associated with a real-estate property based on its address as (street + city + state + zip) or (street + city + state) or (street + zip) or its parcel number as (state + county + APN) or (countyFipsCode + APN). |
| reverse_skip_trace | Returns associated person information (name, addresses, phones, emails) for one or more phone numbers or email addresses. |

### Phone compliance

| Tool | Description |
| :-- | :-- |
| verify_phone | Returns full verification details of a phone number including reachability, DNC status, carrier info, TCPA litigator status, and more. |
| check_dnc_status | Checks only the DNC (Do Not Call) status of a phone number. |
| check_tcpa_status | Checks only the TCPA litigator status of a phone number. |

### Address

| Tool | Description |
| :-- | :-- |
| verify_address | Accepts a property address in the format of street + city + state + zip, or street + city + state, or street + zip and returns an address formatted to comply with USPS conventions. |
| geocode_address | Accepts a property address in the format of a single text string representing the street + city + state + zip, or street + city + state, or street + zip and returns the geo-coordinates for the requested address. |
| reverse_geocode_address | Accepts geo-coordinates in the form of latitude and longitude values and returns the address at those coordinates. |

### Datasets and investor buy box

| Tool | Description |
| :-- | :-- |
| list_property_datasets | Returns all available property datasets with field counts and sample fields. |
| list_property_dataset_fields | Returns the full list of field paths for a specific property dataset. |
| investor_buybox_count | Returns the total count of investors matching the buy box criteria and aggregate result metadata, without returning individual investor records. This is not free: it bills for 1 record. |
| investor_buybox_preview | Returns a quick preview of the first 10 ranked investor profiles matching the buy box criteria, plus total count and aggregate result metadata. |
| investor_buybox_page | Paginated access to investors matching the buy box criteria with full details (page size: 10). |

* * *

## Troubleshooting

### OAuth Issues

| Issue | Solution |
| :-- | :-- |
| Browser doesn't open for login | Ensure pop-ups are allowed. Check that your default browser is set correctly. |
| Login page shows "Session expired" | Remove and re-add the connector, then authenticate again. |
| "Too many login attempts" error | Wait 15 minutes before trying again. |
| Google Sign-In not working | Ensure pop-ups are allowed and try using email/password instead. |
| Connection fails after login | Check your internet connection. The redirect back to the MCP client may have failed. Try removing and re-adding the connector. |

### ChatGPT Issues

| Issue | Solution |
| :-- | :-- |
| Can't create connectors | Ensure Developer Mode is enabled in Settings → Apps & Connectors → Advanced settings. |
| Developer Mode toggle missing | For Business/Enterprise, your workspace admin must enable it in Workspace Settings first. |
| Authentication fails | Ensure pop-ups are allowed for https://chatgpt.com . Try disconnecting and reconnecting the connector. |
| Tools not being used | Be explicit in your prompt: "Use the BatchData connector to...". Add the connector via the + button before prompting. |
| Connector not responding | Go to Settings → Connectors → BatchData → Refresh to update metadata. The server may be temporarily unavailable. |
| Wrong tools being called | Specify: "Do not use built-in browsing or other tools; only use the BatchData connector." |

### API Token Issues

| Issue | Solution |
| :-- | :-- |
| 401 Unauthorized | Verify your API token is correct and has not expired. |
| 403 Forbidden | Ensure your token has the required endpoint permissions in the BatchData Web App. |
| Node.js path errors | Verify the path to npx exists by running which npx (macOS/Linux) or checking the install path (Windows). |
| Configuration not loading | Restart your MCP client after saving the configuration file. |

### General Issues

| Issue | Solution |
| :-- | :-- |
| Tools not appearing | Verify the MCP server is enabled in your client's extensions list. |
| SkipTracing returns 403 | SkipTracing v3 must be enabled for your team by an admin, and your token needs the permission. |
| Slow responses | Check your internet connection. The server proxies requests to BatchData APIs. |

### Getting Help

* **API Token issues**: Log into the BatchData Web App to manage your server-side tokens
* **Permission issues**: Contact your BatchData team administrator
* **Technical issues**: support@batchservice.com
  

* * *

© BatchData 2025


