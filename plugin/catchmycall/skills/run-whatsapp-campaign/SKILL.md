---
name: run-whatsapp-campaign
description: Plan, check, launch, pause and report on a WhatsApp campaign. Use when the user wants to message a list of customers, send a promotion or reminder to many people, or asks how a campaign performed.
---

To run a WhatsApp campaign in CatchMyCall:

1. Pick the template. List APPROVED templates with `template_list` and open the chosen one with `template_detail` to see its variables. A template that is not APPROVED by Meta cannot be sent; say so and stop.
2. Build the recipient list with the user: numbers in international format, with per-recipient variables where the template needs them. Remove numbers on the do-not-contact list (`dnd_check` on the WHATSAPP channel) and tell the user how many were removed.
3. Create the campaign as a draft with `campaign_create`. Nothing is sent at this step.
4. Preview the launch with `campaign_launch` and `dryRun: true`. Show the user exactly: how many people, which template, from which number. Wait for a clear yes, then launch with `dryRun: false`.
5. If the user wants to stop it, `campaign_pause`; messages already sent stay sent.
6. To report, use `campaign_insights`: sent, delivered, read, replied, failed. Lead with the delivery and reply rates, then call out failures.

Never launch without the preview and an explicit confirmation in the same conversation.
