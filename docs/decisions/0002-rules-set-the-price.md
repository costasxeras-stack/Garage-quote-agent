# 0002: AI reads the message. Rules set the price

**Status:** Accepted · **Date:** 2026-11-15

## Context
An LLM can read "front pads on my 2015 yaris pls" in English, Greek or Greeklish far better than keyword rules. But a price sent to a customer is a commitment made in the garage's name, and LLMs can produce confident, wrong numbers.

## Decision
Claude only extracts structured facts: car, job codes from the garage's own list, unmatched requests, safety flag, confidence. A deterministic Code node prices the matched jobs from the price book (labour hours × rate × premium multiplier + parts range + VAT, rounded to €5). The AI never sees or states a price.

## Consequences
- Prices are predictable, explainable and controlled by the owner in a table.
- Jobs not in the price book cannot be quoted automatically. They become a weekly "add this to your price book" list.
- Ranges are wide by design. The reply says the final price is confirmed after inspection.
- The quality of the price list now limits the product, more than the quality of the AI.
