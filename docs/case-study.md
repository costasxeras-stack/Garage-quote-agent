# Case study: answering garage price requests in seconds without losing control

> **Status:** v0.1.0 is built and tested with sample data and stand-in services. No real garage has used it yet. Every number below is a [placeholder] until a pilot runs. Findings are labelled **confirmed** (seen in tests) or **hypothesis** (to be checked with real use).

## The question
How much of a garage's first reply to a price request can be automated safely, and where must the owner stay in control?

## Approach
- Split the problem in two: **understanding** a free-text message (a job for AI) and **pricing** it (a job for rules the owner controls).
- Put a **confidence gate** between them: automate only when every check passes, otherwise ask the owner with the reasons.
- Meet customers where they are: **WhatsApp first**, plus a web form and a webhook.
- Record every lead, routing decision and owner decision, so the garage can measure where leads are lost.

## Headline numbers
Source: [pilot garage, anonymised] · Period: [dates]

| Measure | Before | With the agent |
|---|---|---|
| Requests in period | [X] | [X] |
| Median time to first reply | [X] min | [X] min |
| Answered automatically | n/a | [X]% |
| Booking requests from estimates | [X]% | [X]% |
| Automatic estimates the owner later corrected | n/a | [X] |

## Findings

**1. The gate routes uncertain requests to the owner instead of guessing.** *Confirmed in testing.* Vague messages ("strange noise when I turn"), possible safety issues (smoke) and owner-only jobs (timing belt) all went to the owner with the reasons listed. Routine jobs with a known car were answered automatically. *Why it matters:* the owner only sees the requests that need judgement.

**2. Messaging rules shape the product, not just the integration.** *Confirmed by design.* WhatsApp allows free-form replies only within 24 hours of the customer's last message, so the follow-up is scheduled inside that window, and owner alerts go to the owner's WhatsApp, which only works while the owner keeps the 24-hour window open with a daily message.

**3. "Not in the price book" is a demand signal.** *Hypothesis.* The weekly report lists requests that matched no job. I expect these to show which services to price next.

**4. Most requests are routine enough to answer automatically.** *Hypothesis.* Expected share: [X]%. To be measured in a pilot.

## What my own approach got wrong
[To be written after the pilot. Candidates to watch: threshold too strict or too loose; price ranges too wide to be useful; customers ignoring the booking form and replying on WhatsApp instead.]

## What I would do next
- Ask a clarifying question on WhatsApp when the car is missing, instead of sending it to the owner
- Approved WhatsApp templates for reminders after 24 hours
- Greek replies
- Calendar slots in the booking form
- An evaluation set of real (anonymised) messages to tune the threshold

## What I learned as a PM
[To be written.]

## Limits
Sample garage, sample prices and stand-in services. See [testing.md](testing.md).
