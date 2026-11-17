# CatchMyCall MCP server

The official [Model Context Protocol](https://modelcontextprotocol.io) server for
[CatchMyCall](https://app.catchmycall.ai), the AI voice and WhatsApp platform by Teeoff Technologies.
It lets an AI assistant (GitHub Copilot, Claude, Cursor, ChatGPT and others) work with your
CatchMyCall organisation: call records, contacts, leads, campaigns, WhatsApp and billing.

This is a **hosted remote server**. There is nothing to install or run, and this repository holds
documentation only.

| | |
|---|---|
| Endpoint | `https://mcp.catchmycall.ai/mcp` (Streamable HTTP) |
| Auth | OAuth 2.1 with dynamic client registration; no API key to copy |
| MCP Registry | `ai.catchmycall/cpaas` |

## What it can do

**Read**
- Calls: list and filter calls, live calls, call status, transcript, summary and outcome
- Contacts: list, search, look up by phone number, contact timeline
- Leads: list, detail, insights, export
- AI agents: list agents and their configuration
- Campaigns: list, detail and delivery insights
- WhatsApp: approved templates, message delivery status
- Caller IDs, the organisation directory, metrics summary, and billing (wallet, invoices)

**Act** (only with the permissions you grant; every write tool describes what it will do and asks
you to confirm first)
- Place an outbound AI call, or hang up a live call
- Send a WhatsApp text or approved template message
- Create and update contacts, add a number to the Do-Not-Disturb list
- Create campaign drafts

## Configure

### VS Code / GitHub Copilot

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "catchmycall": { "type": "http", "url": "https://mcp.catchmycall.ai/mcp" }
  }
}
```

### Claude, Cursor and other clients

Add a remote (HTTP) MCP server with the URL `https://mcp.catchmycall.ai/mcp`. For example, in
`~/.cursor/mcp.json`:

```json
{ "mcpServers": { "catchmycall": { "url": "https://mcp.catchmycall.ai/mcp" } } }
```

## Sign in

The first time your client connects, it opens a CatchMyCall sign-in page. You choose the
organisation and approve exactly which permissions the assistant gets (for example read calls,
send WhatsApp, write contacts). Your password never reaches the assistant or the MCP server, and
you can revoke access at any time from the CatchMyCall portal. You need a CatchMyCall account;
[sign up here](https://app.catchmycall.ai).

## Use

Ask in plain language, for example:

- "Show yesterday's unanswered calls and summarise why customers called."
- "Find the contact for +91 98xxxxxxxx and show their last three calls."
- "List this week's new leads from the website agent and export them."
- "Send the `appointment_reminder` WhatsApp template to Priya for tomorrow 10 am."
- "How is the Diwali campaign doing? Delivery and read rates, please."
- "Call +91 98xxxxxxxx with the booking agent to confirm the appointment."

## Links

- Documentation: https://app.catchmycall.ai/docs/connector
- Privacy policy: https://app.catchmycall.ai/privacy
- Terms: https://app.catchmycall.ai/terms
- Support: support@catchmycall.ai

© Teeoff Technologies Private Limited. The server is operated by CatchMyCall; its source is not
published.
