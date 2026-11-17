# Installing the CatchMyCall MCP server (for AI agents such as Cline)

CatchMyCall is a **hosted remote MCP server**. There is nothing to clone, build or run locally,
and no API key to configure.

1. Add a remote server to the MCP settings (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "catchmycall": {
      "type": "streamableHttp",
      "url": "https://mcp.catchmycall.ai/mcp"
    }
  }
}
```

2. On first use the server answers `401` with an OAuth challenge. The client discovers the
   authorization server from `https://mcp.catchmycall.ai/.well-known/oauth-protected-resource`,
   registers itself automatically (dynamic client registration) and opens the CatchMyCall
   sign-in page in the browser. The user signs in and approves the permissions; no password
   reaches the agent.
3. When connected, `tools/list` returns the tools for the permissions approved (up to 45).

Requirements: a CatchMyCall account (sign up at https://app.catchmycall.ai). Support:
support@catchmycall.ai.
