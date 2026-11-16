# 0004: Start on WhatsApp, keep follow-ups inside the 24-hour window, reply in English

**Status:** Accepted · **Date:** 2026-11-15

## Context
Customers in the target market message garages on chat apps. Viber is widely used in Greece, but a Viber chatbot carries a monthly fee per bot, and the product should be demonstrable to an international audience. WhatsApp's Cloud API has a free test number and an official n8n node. WhatsApp only allows free-form messages within 24 hours of the customer's last message. After that, messages must use approved templates.

## Decision
- WhatsApp is the first chat channel and Viber is deferred. A web form and a generic webhook cover other sources.
- The one WhatsApp reminder is scheduled inside the 24-hour window (default 20 hours after the customer's message). No WhatsApp messages after the window in v0.1.
- Customer replies are in English. The AI still understands Greek and Greeklish input.

## Consequences
- Easy to demo with a free test number. No template approval needed for v0.1.
- Fewer follow-ups on WhatsApp than on email. Templates are a planned improvement.
- Greek-only customers get English replies until Greek templates are added.
