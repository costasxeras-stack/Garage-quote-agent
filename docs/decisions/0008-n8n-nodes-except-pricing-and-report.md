# 0008: n8n's own nodes everywhere, except the pricing rules and the weekly numbers

**Status:** Accepted · 22 November 2026

## Context

Version 0.1 had 11 Code nodes. Most of them did plumbing: turning a WhatsApp event, a form or a webhook into one lead, building the AI request, writing the customer message for each owner answer, choosing the next follow-up. On the canvas they were black boxes. A garage owner or an ops person opening the workflow could not see the steps without reading JavaScript.

## Decision

Replace the plumbing with n8n's own nodes:

- Each channel has its own step: **Lead from WhatsApp**, **Lead from web form**, **Lead from webhook**. WhatsApp events go through Filter and Split Out first, so status updates, photos and voice notes are dropped visibly.
- A Merge waits for the price book before the leads go on, and a Filter drops the owner's own daily "hi".
- The owner's answer goes through a Switch with four outputs: send the estimate, we will call you, decline, and no answer in time. Each writes its own customer message.
- Follow-ups use a Filter and two Edit Fields steps: work out the next step, then write the reminder.
- Setup uses a Filter for "no settings yet", and the sample price book is plain JSON split into rows.

Two Code nodes stay:

- **Price & route** (workflow 01). It holds the business rules: labour hours times rate, premium-brand multiplier, parts range, VAT, rounding to €5, and the confidence gate. As nodes this becomes a long chain of steps that hides the rules instead of showing them. One commented block that a reviewer can read top to bottom is the clearer choice. Decision 0002 (rules set the price) depends on these rules being easy to check.
- **Count the week** (workflow 04). The weekly report needs a median reply time, counts by status and channel, and the top 5 requests missing from the price book. As nodes that is five branches joined by a Merge, and the Merge stops if one branch has no data (for example a week with no gaps).

## Consequences

- Workflow 01 grew from 23 to 36 steps but reads left to right: channel, lead, AI, price, owner, reply.
- Code is used only where it is easier to read than nodes, and the README says so.
- Expressions inside the Edit Fields steps still contain small bits of JavaScript (a ternary, a `join`). The rule is that the step's purpose is clear from its name and fields.
