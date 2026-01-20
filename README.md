# BatchData Remote MCP Server Setup Guide

## Introduction

This guide documents the current method for connecting to the BatchData Remote MCP Server, which is based on configuring your MCP client using a BatchData API token.

### Current Approach: API Token-Based Access

The setup process described in this guide requires you to configure your MCP client with your BatchData API token. **Important considerations:**

* This approach bypasses the BatchData user access control model
* Anyone with access to the API token can use the MCP server
* The token should be treated as a sensitive credential and protected accordingly
* You are responsible for managing who has access to your API token
  

### Future Approach: OAuth-Based Access Control (Coming Soon)

We are actively developing an improved integration method that will provide better security and access control:

* **No API token or local setup needed** - Users will simply provide the MCP server URL
* **Account-based authentication** - The MCP client will prompt you to log into your BatchData account
* **Permission verification** - The system will automatically confirm whether your account has been granted permission to use the MCP server
* **Centralized access management** - Team owners can grant or revoke MCP server access through the BatchData platform
  

## Prerequisites

* Your BatchData API Token
* An MCP-compatible client (Claude Desktop or your own MCP client)
  

## Choose Your Setup Path

**Using Claude Desktop?** → Follow [Claude Desktop Setup]()  
**Using your own MCP client?** → Follow [Custom MCP Client Setup]()

* * *

## Claude Desktop Setup

### Why This Setup?

Claude Desktop's bundled Node.js version is outdated. The BatchData MCP Server requires Node.js 22, so we'll install it separately using Volta and configure Claude Desktop to use this newer version.

### Setup Steps

#### Step 1: Install Node.js 22

Choose your operating system:

##### **macOS**

1. Open Terminal
2. Install Volta (Node.js version manager):
  ```
  curl https://get.volta.sh | bash
  ```
3. Close and reopen Terminal
4. Install Node.js 22:
  ```
  volta install node@22
  ```
5. Find your username by running:
  ```
  whoami
  ```
  Save this username - you'll need it in Step 2.
  

##### **Windows**

1. Download and install Node.js 22.x LTS from [nodejs.org](https://nodejs.org/ "https://nodejs.org/")
2. During installation, note the installation path (typically `C:\Program Files\nodejs`)
3. Restart your computer after installation
  

##### **Linux**

1. Open Terminal
2. Install Volta:
  ```
  curl https://get.volta.sh | bash
  ```
3. Restart Terminal
4. Install Node.js 22:
  ```
  volta install node@22
  ```
5. Find your username by running:
  ```
  whoami
  ```
  Save this username - you'll need it in Step 2.
  

* * *

#### Step 2: Configure Claude Desktop

1. Open **Claude Desktop**
2. Go to **Settings** > **Developer** > **Edit Config**
3. This opens a JSON file in your text editor
4. Add the following configuration based on your operating system:
  
##### **macOS/Linux Configuration**

```
{ "mcpServers": { "BatchData": { "command": "/Users/YOUR_USERNAME/.volta/bin/npx", "args": [ "-y", "mcp-remote", "https://mcp.batchdata.com", "--header", "Authorization:${AUTH_HEADER}" ], "env": { "AUTH_HEADER": "Bearer YOUR_API_TOKEN_HERE" } } } }
```

**For Linux**, replace `/Users/YOUR_USERNAME/` with `/home/YOUR_USERNAME/`

##### **Windows Configuration**

```
{ "mcpServers": { "BatchData": { "command": "C:\\Program Files\\nodejs\\npx.cmd", "args": [ "-y", "mcp-remote", "https://mcp.batchdata.com", "--header", "Authorization:${AUTH_HEADER}" ], "env": { "AUTH_HEADER": "Bearer YOUR_API_TOKEN_HERE" } } } }
```

**Important:**

* Replace `YOUR_USERNAME` with your actual username (from Step 1)
* Replace `YOUR_API_TOKEN_HERE` with your actual BatchData API Token
* Adjust the Node.js path if you installed it in a different location
  

5. **Save** the file
  

> **Note:** Using absolute paths ensures Claude Desktop uses Node.js 22 instead of its outdated bundled version.

* * *

#### Step 3: Enable the MCP Server

1. **Restart Claude Desktop** completely
2. Open Claude Desktop
3. You should see **BatchData** in the extensions list
4. If disabled, click to **enable** it
5. When prompted for permissions on first use, select **"Always Allow"**
  

* * *

### Verification

The BatchData MCP Server is now ready to use. Claude will automatically detect and use the tools when you ask real estate-related questions or request property data lookups.

* * *

### Claude Code Integration

Once you've set up the BatchData MCP server for Claude Desktop, you can also use it with Claude Code (the command-line agentic coding tool).

#### Prerequisites

* Claude Desktop already configured with BatchData MCP server (see above)
* Claude Code installed on your system
  

#### How to Add BatchData to Claude Code

Claude Code uses a separate configuration from Claude Desktop. To import the BatchData MCP server from your Claude Desktop configuration:

1. Open your terminal
2. Run the following command:
  

```
claude mcp add-from-claude-desktop
```

3. Claude Code will scan your Claude Desktop configuration and present you with available MCP servers
4. Select **BatchData** from the list
5. Confirm the import
  

This will copy the BatchData MCP server configuration (including the Node.js path and API Token) into Claude Code's configuration file.

* * *

## Custom MCP Client Setup

If you're using your own MCP client implementation, you'll need to configure it to connect to the BatchData MCP server using the following details:

### Connection Details

* **Server URL:** `https://mcp.batchdata.com`
* **Transport:** Streamable HTTP
* **Authentication:** Bearer token via `Authorization` header
  

### Configuration Example

```
{ "server_url": "https://mcp.batchdata.com", "headers": { "Authorization": "Bearer YOUR_API_TOKEN_HERE" } }
```

Replace `YOUR_API_TOKEN_HERE` with your actual BatchData API Token.

### Using with npx (Alternative)

If your MCP client supports spawning processes, you can use `npx` with `mcp-remote`:

```
npx mcp-remote https://mcp.batchdata.com --header "Authorization:Bearer YOUR_API_TOKEN_HERE"
```

## Available Tools

Once connected, the BatchData MCP Server provides the following tools:

### **Property Lookup & Details**

* `lookup_property` - Get detailed property information by ID, address, or parcel number
  

**Comparable Property Analysis**

* `comparable_property_count` - Get count and aggregated metrics of comparable properties
* `comparable_property_preview` - Quick preview of first 10 comparables with summary fields
* `comparable_property_page` - Paginated access to full comparable property details (supports both offset and cursor-based pagination)
* `comparable_property` - ⚠️ Deprecated - returns all comparables at once
  

**Property Search**

* `search_properties_count` - Get count of properties matching search criteria with quicklist breakdowns
* `search_properties_preview` - Quick preview of first 10 matching properties
* `search_properties_page` - Paginated property search with full details (supports offset and cursor-based pagination)
  

**Contact Information**

* `skip_trace_property` - Get owner and contact information for a property by address or parcel number
  

**Phone Verification**

* `verify_phone` - Full verification details including reachability, DNC status, carrier, TCPA litigator status
* `check_dnc_status` - Check Do Not Call status only
* `check_tcpa_status` - Check TCPA litigator status only
  

**Address Processing**

* `verify_address` - Format addresses to USPS compliance
* `geocode_address` - Get coordinates from an address
* `reverse_geocode_address` - Get address from latitude/longitude coordinates
  

Refer to your MCP client's documentation for how to invoke these tools once connected.

* * *

## Need Help?

### General Support

* **Want to see available tools?** Once connected, your MCP client should list all available BatchData tools
* **Can't find your API Token?** You need to login to the BatchData Web App and generate a server-side token with the needed endpoints permissions
* **An MCP tool returned 401 or 403?** You need to login to the BatchData Web App and ensure that you granted your used server-side token the relevant endpoint permissions. **Note that the SkipTracing functionality requires that SkipTracing v3 endpoints are enabled for your BatchData team by an admin and that your server-side token has it enabled in its permissions.**
* **Other issues?** Contact the BatchData team
  

### Claude Desktop

* **Configuration not working?** Make sure you've restarted Claude Desktop after saving the config file
* **Path errors?** Double-check that you replaced `YOUR_USERNAME` with your actual username and that the Node.js path exists
* **Still having issues?** Verify Node.js 22 is installed by running `node --version` in your terminal (should show v22.x.x)
  

### Custom MCP Client

* **Connection issues?** Verify your API Token is correct and the Authorization header format is: `Bearer YOUR_API_TOKEN`
* **Server not responding?** Check that your MCP client supports Streamable HTTP transport
* **Need implementation help?** Refer to the [MCP specification](https://modelcontextprotocol.io/ "https://modelcontextprotocol.io/") for client implementation details
