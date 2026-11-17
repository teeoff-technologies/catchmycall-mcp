---
name: follow-up-leads
description: Find, correct, export and follow up on leads captured by the AI phone agent. Use when the user asks about new leads, leads from a city or campaign, fixing a lead's details, exporting leads, or calling or messaging a lead back.
---

To work with leads in CatchMyCall:

1. Find the leads with `lead_list` (filters: date range, origin, sync status, or a captured field such as City). Use `lead_insights` when the user asks "how many" rather than "which".
2. Open one lead with `lead_detail` before changing it. To fix a misheard value or set a pipeline status, use `lead_update` with only the fields that change, and show the user each field's current and new value before saving. If the lead is already in their CRM, tell them the CRM copy is not updated.
3. To export, use `lead_export` with the same filter and give the user the CSV block. It is capped at 500 rows; say when it was cut short.
4. To follow up:
   - Check `dnd_check` for the number and channel first. If it is blocked, stop and say so.
   - Inside a 24-hour WhatsApp session, `whatsapp_send_text`; otherwise an APPROVED template via `whatsapp_send_template` (find it with `template_list`).
   - For a call, pick the caller ID with `caller_ids`, then `outbound_call`.
   - Before any send or call, show the user the recipient, the number used, and the exact text or template with its variables, and wait for a clear yes. Use `dryRun: true` first when the user wants to see the result.
5. Report what was done with its id (message id or call id) so the user can check it later with `whatsapp_message_status` or `call_status`.
