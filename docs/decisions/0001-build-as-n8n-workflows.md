# 0001: Build the product as n8n workflows, not a coded app

**Status:** Accepted · **Date:** 2026-11-15

## Context
My portfolio apps normally use Node/Express on Render's free plan. This product is mostly orchestration: triggers on several channels, waiting for a person's decision, schedules, retries and error alerts. It also has to be something a garage owner (or their IT helper) can open and change. Render's free plan sleeps and has no persistent disk, which breaks waiting executions and stored data.

## Decision
Build it as six n8n workflows using standard nodes, with logic in a few small, commented Code nodes. Host it on n8n Cloud (or self-hosted n8n), not Render.

## Consequences
- Human-in-the-loop, forms, schedules, retries and the run history come from n8n, not from custom code.
- Anyone can open the canvas and see the flow; the README diagram matches what runs.
- It needs an n8n instance, which costs money after the trial; the portfolio repo stays usable because the workflow files can be imported anywhere.
- No server.js or Render service, a deliberate deviation from my default stack.
