# Changelog

All notable changes to Garage Quote Agent. Versions follow [docs/versioning.md](docs/versioning.md).

## [0.1.1] - 2026-11-16

### Changed
- Documentation wording only: shorter sentences, fewer semicolons and less bold text, so the docs read more plainly. No change to how the workflows run.

## [0.1.0] - 2026-11-15

### Added
- Lead intake and instant quote (01): one flow for WhatsApp, a web form and a generic webhook, so every request is handled the same way whatever channel it arrives on.
- AI request reader: Claude extracts car, jobs, safety risk and confidence from English, Greek or Greeklish messages, and maps jobs only to codes in the garage's price book.
- Rule-based pricing: labour hours × rate, parts range, premium-brand multiplier and VAT, rounded to €5, so prices are predictable and never invented by AI.
- Confidence gate: routine requests are answered automatically. Anything uncertain, unsafe, unpriced or owner-only goes to the owner with the reasons listed.
- Owner decision on WhatsApp: send the estimate, send a custom price, call the customer, or decline, from a phone. If the owner does not answer in 30 minutes, the customer gets a holding message and the owner gets a reminder.
- Booking requests (02): booking form linked from each estimate, protected by a one-time token, with an owner alert.
- Follow-ups (03): one WhatsApp reminder inside Meta's 24-hour window. Up to two email reminders with consent. Then the lead is marked lost.
- Weekly owner report (04): leads by channel, automation share, median first-reply time, bookings, lost leads and missing price-book jobs.
- Error alerts (99) to the owner on WhatsApp.
- One app for the owner: all owner messages (decisions, updates, booking requests, weekly report, errors) go to the owner's own WhatsApp. The owner's daily "hi" to the garage number is not treated as a lead.
- Setup workflow (00) that creates the data tables with sample settings and a sample price book, safe to re-run.
- Product docs: brief, case study outline, seven decision records, setup guide and test report.
