---
name: handle-opt-outs
description: Check and record do-not-contact requests. Use when someone asks not to be called or messaged again, when the user asks whether a number may be contacted, or before contacting a number the user has not contacted recently.
---

To handle opt-outs in CatchMyCall:

1. To check, use `dnd_check` with the number in international format and the channel (VOICE, WHATSAPP or SMS). Report whether it is blocked and why.
2. To record an opt-out, confirm the number and the channel with the user, then use `dnd_add`. An opt-out is permanent and recorded per channel: if the person asked to stop all contact, add VOICE and WHATSAPP (and SMS if the business sends SMS), one at a time.
3. Do not add the same number and channel twice; check first.
4. After recording, do not call or message that number on that channel, even if the user asks in the same conversation; explain that the number has opted out.
