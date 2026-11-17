# CatchMyCall

The `catchmycall` MCP server gives access to the signed-in organisation's CatchMyCall account:
calls and transcripts, leads captured by the AI phone agent, contacts and their message history,
WhatsApp templates and campaigns, do-not-contact lists and billing figures.

- On first use the server asks you to sign in. A browser opens the CatchMyCall sign-in page;
  approve the organisation and permissions there. No API key is needed.
- Calls, WhatsApp messages and campaign launches reach real people. Show the recipient and the
  exact content and get the user's confirmation before using them. Each takes `dryRun: true`
  for a preview.
- Check the do-not-contact list (`dnd_check`) before contacting a number.
