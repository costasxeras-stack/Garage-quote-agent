# 0006: If the owner doesn't answer in 30 minutes, reply anyway

**Status:** Accepted · **Date:** 2026-11-15

## Context
The point of the product is a fast first reply. Requests sent to the owner can sit unanswered while they work.

## Decision
The owner's decision waits at most 30 minutes. If there is no answer, the customer gets a short holding message ("a mechanic needs to look at your request, we will contact you personally"), the lead becomes `needs_call`, and the owner gets a reminder with the customer's contact details.

## Consequences
- Every customer hears back within about half an hour, even in the worst case.
- A holding message is weaker than an estimate; the weekly report counts `needs_call` leads so the owner can see the cost.
- The 30-minute limit is fixed in the node; making it a setting is a small follow-up.
