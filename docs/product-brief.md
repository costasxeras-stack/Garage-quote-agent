# Product brief: Garage Quote Agent

## Problem
Independent car-repair garages get price questions on WhatsApp, by phone and on their website all day. The people who can answer are working on cars. Replies come hours later, and by then many customers have asked another garage. Most questions are routine ("front pads, 2015 Yaris"). A minority genuinely need a mechanic ("strange noise when I brake").

## Users
| User | Situation | Needs |
|---|---|---|
| **Garage owner / head mechanic** | Hands busy, phone in pocket, decides prices | Routine questions handled without them; a fast, clear decision screen for the rest; no wrong prices sent in their name |
| **Customer** | Comparing a few garages, often on WhatsApp | A real price range quickly, an easy way to book, no pressure |
| **Front desk (if any)** | Juggling calls and walk-ins | One place to see every lead and its status |

## Goals for v0.1
1. Every request gets a first reply quickly, on the channel it came from.
2. No price is ever made up: prices come from the garage's own price book or from the owner.
3. The owner stays in control of anything uncertain, unsafe or expensive.
4. Every lead, decision and message is recorded, so the garage can see where leads are lost.

## Success measures (to be measured in a pilot)
| Measure | Baseline | Target |
|---|---|---|
| Median time to first reply | [X] min (before) | [X] min |
| Share of requests answered automatically | n/a | [X]% |
| Estimate → booking request rate | [X]% | [X]% |
| Owner decisions answered within 30 min | n/a | [X]% |
| Wrong automatic estimates (owner had to correct) | n/a | [X] per 100 |

## Scope (v0.1)
- Channels in: WhatsApp (text), web form, generic webhook
- AI extraction of car, jobs, safety, confidence (English, Greek, Greeklish)
- Rule-based price ranges from an editable price book
- Confidence gate with owner approval on Telegram, with a 30-minute fallback
- Booking request form with token-protected links
- Follow-ups within channel rules (WhatsApp 24-hour window, email with consent)
- Weekly owner report and error alerts
- English customer replies

## Non-goals (v0.1)
- Calendar availability or automatic appointment confirmation
- Payments or deposits
- Reading photos or voice notes
- Greek-language replies
- Parts-supplier price lookups (the price book is the source of truth)
- WhatsApp template messages (needed for messages after 24 hours)

## Risks
| Risk | Mitigation |
|---|---|
| AI misreads the car or job and a wrong price goes out | Rules price only known jobs; confidence threshold; owner-only jobs; price shown as a range with "confirmed after inspection" |
| Safety issue answered with a price | Safety flag always routes to the owner |
| Owner doesn't answer | 30-minute fallback holding message and owner reminder |
| Spam or forged WhatsApp events | WhatsApp trigger checks Meta's signature; booking links need a token |
| Messaging rules (Meta, GDPR) | Follow-ups only inside the 24-hour window or with email consent; data stays in the garage's own n8n |
