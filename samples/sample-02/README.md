# Sample 02 — Inbox Triage & Draft Skill

## Problem Statement

Support teams and customer-facing staff spend 2–3 hours daily reading incoming messages, deciding which are urgent, routing them to the right person, and writing first-draft replies. Most messages fall into predictable categories with predictable responses. Claude can classify and draft all of them in seconds, leaving the human to review and send — not write from scratch.

## What the Skill Does

The **Inbox Triage & Draft Skill** processes a batch of incoming support messages and for each one produces:

- **Category** — `billing`, `technical`, `general`, or `urgent`
- **Priority** — `1` (respond within 1 hour), `2` (respond today), `3` (respond within 48 hours)
- **Draft reply** — a complete, professional response ready to send after a quick human review
- **Escalate** — `yes` or `no` indicating whether a human lead needs to review before sending

The output is a structured JSON array, making it easy to feed into a ticketing system or CRM via automation.

## What the Automation Does

The `automation-playbook.md` describes how to connect this Skill to an email inbox trigger in Claude Cowork:

- New emails arriving in a designated support inbox trigger the automation
- Each email is passed to this Skill
- The triage output is written back to the CRM (HubSpot / Zendesk / Notion)
- Priority-1 messages trigger an immediate Slack alert to the on-call agent
- Priority-2 and -3 drafts are queued in a review dashboard for the team

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time per message (read + draft) | 8 min | 1 min (review only) |
| Messages per day | 40 | 40 |
| Total time per day | 5.3 hr | 40 min |
| Hours saved per day | **4.6 hr** | — |
| Hours saved per month (20 working days) | **~92 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
