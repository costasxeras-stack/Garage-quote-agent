# 0003: Gate automatic replies, and put the owner's decisions on Telegram

**Status:** Accepted · **Date:** 2026-11-15

## Context
Full automation risks wrong or unsafe answers. Asking the owner about every request recreates the original delay. The owner works with their hands, so decisions must take a few taps on a phone.

## Decision
- An estimate goes out automatically only if all checks pass: confidence ≥ threshold, every job priced and allowed for auto-quoting, car known, no safety flag, a reply channel exists. Otherwise the owner gets the request with the exact failed checks.
- The owner decides through n8n's Telegram send and wait with a short form: send as calculated, send my price, I will call, decline.
- Telegram rather than WhatsApp for the owner, because WhatsApp messages the business starts need Meta-approved templates and paid conversations, while a Telegram bot is free and supports n8n's built-in waiting.
- Default threshold 0.75, editable in settings.

## Consequences
- The share of automatic replies is a tunable setting, and every routing decision is logged with its reasons, so the threshold can be tuned with data.
- The owner needs Telegram as well as WhatsApp.
- A slow owner still delays the reply. See 0006.
