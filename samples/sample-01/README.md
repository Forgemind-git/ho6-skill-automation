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

## Use it with your Claude.ai subscription

No API key needed — this runs entirely on your Claude.ai subscription (Pro or Team, which include Skills and Cowork).

1. **See it work first.** Open **Claude.ai**, start a new chat, and paste **the example prompt** below. Claude returns a finished status report immediately.
2. **Save it as a Skill.** Open the **Skills** menu → **Create Skill**, name it `Weekly Client Status Report`, and paste in the full contents of `skill.md`. Save.
3. **Use it any time.** In a chat, type `/`, choose **Weekly Client Status Report**, and paste your own client's data.
4. **Automate it (optional).** Follow `automation-playbook.md` to have Cowork read your Google Sheet every Friday and post reports to Notion automatically.

## The example prompt

Copy this into Claude.ai to reproduce the worked example in `skill.md`:

```
You are a professional account manager writing a weekly client status report. Read the project data below and produce a report with four sections: a 2–4 sentence Summary (state overall health: On Track / At Risk / Blocked), 3–5 Highlights (each starting with a past-tense verb), Blockers (each with an owner and impact level, plus a resolution step for High-impact ones), and Next Week Actions (each with an owner and due date, sorted by date). Do not invent data — if something is missing, write [To be confirmed].

Client: Apex Logistics
Project: Warehouse Management System v2
Week: June 23–27, 2025

COMPLETED THIS WEEK:
- Migrated 3 of 5 warehouse databases to new schema (Dev Team)
- UAT sign-off received for inventory module (QA, June 25)
- Resolved API timeout errors in dispatch module (Backend, June 26)

IN PROGRESS:
- Remaining 2 database migrations (Dev Team, 60% done)
- Staff training materials being drafted (Content Team, 40% done)

BLOCKERS:
- Apex IT team has not provided VPN credentials for production (Impact: High, Owner: Apex IT)
- Training room booking delayed by client facilities team (Impact: Low, Owner: Apex Facilities)

PLANNED NEXT WEEK:
- Complete remaining database migrations (Dev Team, Jun 30)
- Submit training materials for client review (Content Team, Jul 1)
- Schedule go-live dry run (PM, Jul 2)
```

The full example output is in `skill.md` under **Example Output**.

## Make it your own

- Swap the Apex Logistics data for one of your own (anonymised) client projects.
- Add a section your clients expect — e.g. **Budget status** or **Hours used** — by editing `skill.md`.
- Adjust the tone in `skill.md` to match how you talk to your clients.

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time per report | 35 min | 2 min (review only) |
| Reports per week | 12 | 12 |
| Total time per week | 7 hr | 24 min |
| Hours saved per week | **6.6 hr** | — |
| Hours saved per month | **~26 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
