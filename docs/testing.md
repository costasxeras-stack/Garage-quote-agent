# Testing: v0.1.0

**How:** the six workflow files in this repo were imported into a local n8n **2.47.7** and published. Claude, Telegram, WhatsApp (Meta Graph API) and email (SMTP) were replaced by local stand-ins that record every request. Real customer traffic was sent through the real triggers: form submissions, signed WhatsApp webhook events and webhook calls. Date: 15 November 2026.

**What the stand-ins mean:** the n8n side (triggers, forms, data tables, routing, waiting, schedules, error handling) ran for real. The AI's answers came from a simple rule-based stand-in, so these tests say nothing about how well Claude reads real messages. That needs a pilot (see the case study).

## Results: 22 of 22 scenarios passed

| # | Scenario | Expected | Result |
|---|---|---|---|
| A1 | Web form, routine job, known car | Estimate emailed with per-job lines, total incl. VAT and booking link | Pass |
| A2 | Same | Owner gets an FYI on Telegram | Pass |
| A3 | Same, consent ticked | Lead saved as `quoted`, consent stored, follow-up scheduled | Pass |
| B1 | Owner-only job (timing belt), low confidence, special characters in message | Owner asked on Telegram with reasons; message still readable | Pass |
| B2 | Owner chooses "my price" with a note | Customer gets the owner's price and note | Pass |
| B3 | Same, no consent | Lead `quoted`, owner decision stored, no follow-up scheduled | Pass |
| C1 | Vague symptom, owner chooses "I will call" | Customer told we will call; lead `needs_call` | Pass |
| D1 | WhatsApp message (signed like Meta) in Greeklish | Estimate sent back on WhatsApp | Pass |
| D2 | Same | Follow-up scheduled inside the 24-hour window | Pass |
| D3 | WhatsApp event with a wrong signature | Ignored: no AI call, no reply | Pass |
| E1 | AI service fails | Lead goes to the owner with "AI could not read the message" | Pass (after the AI node's built-in retries, about 2 minutes) |
| E2 | Possible safety issue (smoke) | Lead goes to the owner | Pass |
| F1 | Booking link opened | Lead ID and token prefilled as hidden fields | Pass |
| F2 | Booking submitted | Lead `booking_requested`; owner told | Pass |
| F3 | Booking with a wrong token | Rejected and logged; owner not alerted | Pass |
| G1 | Email lead due a follow-up | Reminder 1 sent; stage 1 | Pass |
| G2 | Due again | Final reminder; stage 2 | Pass |
| G3 | Due again | No message; lead `lost_no_reply` | Pass |
| G4 | WhatsApp lead due a follow-up, twice | One reminder, then `lost_no_reply` (no messages after 24 h) | Pass |
| H1 | Weekly report | Telegram report with counts, rates and price-book gaps | Pass |
| T1 | Owner does not answer (time limit shortened for the test) | Customer gets a holding message; owner reminded; lead `needs_call` | Pass |
| X1 | Telegram fails while asking the owner | Error workflow alerts the owner with the failed step and run link | Pass |

Setup (00) was also run twice to confirm it does not duplicate settings or prices.

## Not yet tested
- Real Claude responses to real customer messages (extraction quality, confidence calibration)
- Real Meta WhatsApp Cloud API delivery, and the trigger's webhook registration with Meta
- Real Telegram and SMTP delivery
- n8n Cloud specifics (the editor, credentials screens and the published form URLs)
- Load: many messages arriving at once

## Known behaviour to watch
- If Claude is down, the AI node retries for about 2 minutes before the lead goes to the owner.
- If Telegram is down, owner questions fail and the error alert (also on Telegram) can fail too.
