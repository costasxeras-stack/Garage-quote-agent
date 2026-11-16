# 0007: Send owner alerts and decisions to the owner's WhatsApp, not Telegram

**Status:** Accepted · Replaces the Telegram part of [0003](0003-confidence-gate-and-owner-approval.md) · **Date:** 2026-11-15

## Context
In 0003 the owner's console was Telegram, because WhatsApp messages started by the business need Meta-approved templates outside a 24-hour window. Garage owners already live in WhatsApp. Asking them to install and watch a second app is friction that a small garage will not accept.

## Decision
All owner messages (decision requests, automatic-reply updates, booking requests, the weekly report and error alerts) go from the garage's WhatsApp number to the owner's own WhatsApp, using n8n's WhatsApp send and wait for decisions. For v0.1 the owner keeps the 24-hour window open by sending the garage number any short message once a day. The workflow recognises the owner's number and does not treat those messages as leads.

## Consequences
- One app for the owner and one messaging credential for the whole product.
- If the owner forgets the daily message, owner alerts fail (and so does the error alert). The 30-minute fallback still sends the customer a holding message.
- Next step: Meta-approved utility templates for owner alerts, which remove the daily-message workaround.
