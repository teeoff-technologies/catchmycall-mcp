# CatchMyCall plugin for Claude

Work your business phone and WhatsApp from a conversation with Claude. The plugin pairs the
CatchMyCall connector (`https://mcp.catchmycall.ai/mcp`) with four skills that teach Claude how
a business uses it day to day.

## Use it

- **Review missed calls:** "Which calls did we miss yesterday, and did the AI agent capture a lead from any of them?"
- **Follow up on leads:** "List leads from Pune this week and send each the appointment reminder template."
- **Run a WhatsApp campaign:** "Send the Diwali offer template to these 200 customers", then "how did it do?"
- **Respect opt-outs:** "This caller asked not to be contacted again; record it."

In Claude Code:

```
/plugin install catchmycall --marketplace teeoff-technologies/catchmycall-mcp
```

On claude.ai, add the plugin from the directory. Then connect CatchMyCall from the plugin's Connectors tab and sign in with your
CatchMyCall account. You need a CatchMyCall account (sign up at app.catchmycall.ai). Claude
shows the recipient and content and asks before any call, message or campaign launch.

## Data

The plugin itself stores nothing and sends nothing on its own. Through the connector, Claude
reads and changes data in your own CatchMyCall organisation only: calls, transcripts, leads,
contacts, WhatsApp templates and campaigns, do-not-contact entries and billing figures. Messages
go out through Meta's WhatsApp Business API and calls through CatchMyCall's telephony carriers,
only when you ask. Privacy policy: https://app.catchmycall.ai/privacy

## Support

support@catchmycall.ai · https://app.catchmycall.ai/docs/connector
