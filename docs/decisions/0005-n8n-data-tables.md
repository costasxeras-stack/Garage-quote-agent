# 0005: Keep settings, prices and leads in n8n Data Tables

**Status:** Accepted · **Date:** 2026-11-15

## Context
The workflows need shared settings, a price book the owner edits, a lead record and an audit log. Options: Google Sheets, an external database, or n8n's built-in Data Tables.

## Decision
Use n8n Data Tables (`garage_settings`, `garage_price_book`, `garage_leads`, `garage_events`). Workflows find tables by name, and a setup workflow creates them with sample data.

## Consequences
- No extra account or credential; a single import works.
- Settings live in one table instead of being repeated in every workflow.
- Less familiar to owners than a spreadsheet, and harder to share outside n8n; a Google Sheets sync is a possible later addition.
- Tables are tied to the n8n instance; moving instances means exporting the tables as CSV.
