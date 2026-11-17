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

45 tools: 31 read and 14 that change something. An assistant only sees the tools for the
permissions you approve at sign-in. Every tool that changes something describes exactly what it
will do (recipient, text, number, campaign) and asks you to confirm first; previews come first
where a change is large (agent prompts, campaign launches).

### Calls

| Tool | What it does | Permission | Type |
|---|---|---|---|
| `call_list` | List the call log, filtered by date, type, status, dialled number or caller ID | `calls:read` | Read |
| `call_status` | One call's log and status | `calls:read` | Read |
| `call_transcript` | A call's turn-by-turn transcript and the agent's summary | `calls:read` | Read |
| `call_summary` | Call volume and duration totals over a date range, with a daily series | `calls:read` | Read |
| `calls_live` | Calls in progress right now (admin roles) | `calls:read` | Read |
| `caller_ids` | The numbers your organisation can call from | `calls:read` | Read |
| `directory` | Internal extensions a call can be transferred to | `calls:read` | Read |
| `outbound_call` | Place an outbound AI call from one of your numbers | `calls:originate` | Write |
| `hangup_call` | End a call in progress | `calls:manage` | Write |

### AI agents

| Tool | What it does | Permission | Type |
|---|---|---|---|
| `agent_list` | Your AI agents, whether enabled and whether live | `agents:read` | Read |
| `agent_detail` | One agent's lead-capture and CRM settings | `agents:read` | Read |
| `agent_update` | Change an agent's greeting or prompt (preview first) | `agents:write` | Write |

### Leads

| Tool | What it does | Permission | Type |
|---|---|---|---|
| `lead_list` | Leads captured from calls and chats, with filters | `leads:read` | Read |
| `lead_detail` | Everything captured for one lead, and whether it reached the CRM | `leads:read` | Read |
| `lead_insights` | Lead totals and breakdowns over a date range | `leads:read` | Read |
| `lead_export` | Export matching leads as CSV | `leads:read` | Read |
| `call_outcome` | What the agent captured on a call | `leads:read` | Read |
| `lead_create` | Add a lead by hand (walk-in, referral) | `leads:write` | Write |
| `lead_update` | Correct a lead's fields or set its pipeline status | `leads:write` | Write |

### Contacts

| Tool | What it does | Permission | Type |
|---|---|---|---|
| `contact_list` | List contacts, with filters | `contacts:read` | Read |
| `contact_search` | Search contacts by name or company | `contacts:read` | Read |
| `contact_by_phone` | Find a contact by phone number | `contacts:read` | Read |
| `contact_detail` | Everything on file for one contact | `contacts:read` | Read |
| `contact_timeline` | A contact's message history on a channel | `contacts:read` | Read |
| `contact_create` | Add a contact (checks for duplicates) | `contacts:write` | Write |
| `contact_update` | Change a contact's details or labels | `contacts:write` | Write |

### WhatsApp and campaigns

| Tool | What it does | Permission | Type |
|---|---|---|---|
| `whatsapp_send_text` | Send a WhatsApp message inside an open 24-hour session | `whatsapp:send` | Write |
| `whatsapp_send_template` | Send an approved WhatsApp template | `whatsapp:send` | Write |
| `whatsapp_message_status` | Delivery status of a sent message | `messages:read` | Read |
| `template_list` | Your WhatsApp templates and their Meta approval status | `campaigns:read` | Read |
| `template_detail` | One template in full, with its variables | `campaigns:read` | Read |
| `campaign_list` | Your WhatsApp campaigns and their status | `campaigns:read` | Read |
| `campaign_detail` | One campaign's template, schedule and counts | `campaigns:read` | Read |
| `campaign_insights` | How a campaign landed: sent, delivered, read, replied, failed | `campaigns:read` | Read |
| `campaign_create` | Create a campaign as a draft (nothing is sent) | `campaigns:send` | Write |
| `campaign_launch` | Launch or resume a campaign (preview first) | `campaigns:send` | Write |
| `campaign_pause` | Pause a running campaign | `campaigns:send` | Write |

### Do-not-contact

| Tool | What it does | Permission | Type |
|---|---|---|---|
| `dnd_check` | Whether a number is on your do-not-contact list | `dnd:manage` | Read |
| `dnd_add` | Add a number to your do-not-contact list for a channel | `dnd:manage` | Write |

### Reports and billing

| Tool | What it does | Permission | Type |
|---|---|---|---|
| `metrics_summary` | Dashboard and report totals for a day, week, month or range | `metrics:read` | Read |
| `wallet_balance` | Prepaid wallet balance and available credit | `billing:read` | Read |
| `billing_summary` | This month's usage and charges by channel | `billing:read` | Read |
| `invoice_list` | Your invoices and their status | `billing:read` | Read |
| `invoice_detail` | One invoice's line items, tax and balance due | `billing:read` | Read |
| `wallet_recharge_link` | A one-time payment link to top up the wallet (you open it yourself) | `billing:pay` | Write |

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
