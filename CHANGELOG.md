# Changelog

All notable changes to Garage Quote Agent. Versions follow [docs/versioning.md](docs/versioning.md).

## [0.2.0] - 2026-11-22

### Changed
- 9 of 11 Code nodes are replaced with n8n's own nodes (Filter, Split Out, Edit Fields, Merge, Switch). Each channel now has its own visible "Lead from ..." step, and the owner's four possible answers are a Switch with one step each. Decision 0008 explains why two stay in Code: the pricing rules (workflow 01) and the weekly numbers (workflow 04).
- Email replies and reminders use n8n's Gmail node instead of SMTP, so setup is "Sign in with Google" instead of an app password.
- `package.json` said owner approval happens on Telegram. It happens on WhatsApp since 0.1.0. Fixed.

### Upgrade
- Re-import workflows 00 to 03, then connect a Gmail credential (setup guide, step 3). Data tables do not change.

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
