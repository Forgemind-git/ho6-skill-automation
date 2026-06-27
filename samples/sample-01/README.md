# Sample 01 — Weekly Client Status Report Skill

## Problem Statement

Account managers spend 30–45 minutes every Friday manually writing status reports for each client — pulling data from spreadsheets, rewriting bullet points, and formatting emails. With 10+ clients, that is half a workday lost to copy-paste work that Claude can do in under 60 seconds.

## What the Skill Does

The **Weekly Client Status Report Skill** takes a raw data table (pasted from a spreadsheet or CRM export) and produces a polished, client-ready status report with four sections:

1. **Summary** — one-paragraph overview of the week
2. **Highlights** — 3–5 bullet points of positive progress
3. **Blockers** — any issues requiring attention, with suggested owner
4. **Next Week Actions** — prioritised task list with owners and due dates

The output is formatted for direct copy-paste into an email or Notion page. No manual editing required for standard weeks.

## What the Automation Does

The `automation-playbook.md` describes how to connect this Skill to a Google Sheets trigger in Claude Cowork:

- Every Friday at 4 PM, a Cowork automation reads the weekly project data sheet
- Passes each client row to this Skill
- Outputs a formatted report per client into a shared Notion database
- Sends a Slack notification to the account manager with a link

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time per report | 35 min | 2 min (review only) |
| Reports per week | 12 | 12 |
| Total time per week | 7 hr | 24 min |
| Hours saved per week | **6.6 hr** | — |
| Hours saved per month | **~26 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
