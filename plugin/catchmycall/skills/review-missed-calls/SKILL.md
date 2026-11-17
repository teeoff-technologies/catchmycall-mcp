---
name: review-missed-calls
description: Review missed or unanswered calls and what the AI phone agent captured. Use when the user asks about missed calls, yesterday's or today's calls, who called, call volume, or which calls produced leads.
---

To review calls with the CatchMyCall connector:

1. Settle the period first. "Yesterday" and "today" are in the business's own time zone; if unsure, ask once.
2. Get the totals with `call_summary` for the period, so the answer starts with the shape of the day: received, answered, missed, average duration.
3. List the calls with `call_list` for the same period. For missed calls, filter by status rather than reading every call.
4. For each answered call that matters, check `call_outcome` to see what the agent captured, and `call_transcript` only when the user wants to know what was said. An empty outcome can mean processing has not finished yet; say so instead of calling it a failure.
5. Present a short table: time, caller, duration, outcome (lead captured, no capture, missed). Mask nothing the user already sees in their portal, but do not paste raw API responses.
6. End with the follow-ups that need a person: missed callers with no capture, and leads marked incomplete.

Do not call anyone back from this skill. If the user wants to call or message someone, hand over to the follow-up workflow and confirm the recipient first.
