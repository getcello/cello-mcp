# Cello MCP Server

The official [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server for [Cello](https://cello.so), the referral and affiliate platform for SaaS companies.

Connect your AI coding agent or assistant (GitHub Copilot, Claude, Cursor, ChatGPT and any other MCP client) to your Cello account to set up and verify a referral program integration, and to ask about program performance in natural language, grounded in live Cello data.

This is a hosted remote server. This repository holds its documentation and registry metadata (`server.json`); there is nothing to install or run locally.

- **Server URL**: `https://mcp.cello.so/mcp`
- **Transport**: Streamable HTTP
- **Authentication**: OAuth (sign in to Cello in the browser window your client opens; no token to generate or paste)
- **Registry name**: `so.cello/mcp`
- **Docs**: https://docs.cello.so/mcp/introduction

## What it does

**For developers**

- Search the Cello docs, code examples and API references while you build
- Check the health of the four integration components: referral widget, attribution widget, signup tracking and purchase tracking
- Inspect recent webhook and API events with per-field validation (ucc, productUserId, email, customerId)

**For growth and partner managers**

- Program metrics, trends and industry benchmarks
- Find and rank referrers by revenue, signups, purchases or activity
- Prioritized best-practice recommendations for activation, sharing and conversion

## Tools

| Tool | Purpose |
|---|---|
| `cello_get_program_metrics` | Program metrics, trends and benchmarks in one call |
| `cello_get_referrers` | Find and sort referrers by engagement or performance |
| `cello_get_top_referrers` | Top referrers by net new ARR |
| `cello_get_integration_status` | Health of the four integration components |
| `cello_get_events` | Latest events feed with per-field validation |
| `cello_get_recommendations` | Prioritized best-practice recommendations |
| `search_cello` | Search the Cello knowledge base |
| `query_docs_filesystem_cello` | Read full doc pages and OpenAPI specs |

All tools are read-only. Which tools you see depends on your Cello role. Full reference: https://docs.cello.so/mcp/tools

## Prerequisites

1. A Cello account.
2. MCP enabled for your account: an admin turns it on in the [Cello Portal](https://app.cello.so/mcp) under **My account -> MCP Server**.

## Configuration

### GitHub Copilot in VS Code

Install Cello from the MCP server gallery in VS Code, or add it to `.vscode/mcp.json` in your workspace (or run **MCP: Add Server** from the Command Palette):

```json
{
  "servers": {
    "Cello": {
      "type": "http",
      "url": "https://mcp.cello.so/mcp"
    }
  }
}
```

Start the server. VS Code opens a browser window to sign in to Cello and authorize access. Then open Copilot Chat in **Agent** mode and the Cello tools are available.

### Copilot coding agent

In your repository go to **Settings -> Copilot -> Coding agent -> MCP configuration** and add:

```json
{
  "mcpServers": {
    "cello": {
      "type": "http",
      "url": "https://mcp.cello.so/mcp",
      "tools": ["*"]
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport http Cello https://mcp.cello.so/mcp
```

Then run `/mcp`, select **Cello** and choose **Authenticate**.

### Cursor

Click **Cursor** on the MCP Server page in the Cello Portal, or add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "Cello": {
      "url": "https://mcp.cello.so/mcp"
    }
  }
}
```

### Other MCP clients

Add a remote (Streamable HTTP) server with the URL `https://mcp.cello.so/mcp` and OAuth authentication. Setup guides for Claude, ChatGPT, Windsurf, Lovable, Replit and more: https://docs.cello.so/mcp/connect

## Usage

Example prompts:

- "Use Cello to check my integration status."
- "Add Cello referral tracking to this app."
- "Why are my signups not being attributed to referrers?"
- "Show me the latest events Cello received and flag any missing fields."
- "How is our referral program doing compared to industry benchmarks?"
- "Who are our top 10 referrers by net new ARR?"
- "What should we improve to get more referrers sharing?"

## Troubleshooting

| Issue | Solution |
|---|---|
| Tools return authentication errors | Disconnect and reconnect the server. Check that MCP is enabled under **My account -> MCP Server** in the portal. |
| You don't see the tools you expect | Available tools depend on your Cello role. Contact your Customer Success Manager. |
| `cello_get_integration_status` shows `notConnected` | Follow the integration guide for that component; ask `search_cello` for the setup docs. |

## Support

- Documentation: https://docs.cello.so
- Email: [support@cello.so](mailto:support@cello.so)
