# HO6 Sample 1 — Weekly Client Status Report

## What you'll build
A reusable Claude **Skill** that turns a few rough bullet points about a client project into a polished, client-ready status report — every single time, in the same format. Then you'll have Claude **Cowork** run it for you automatically, so the Friday report writes itself. By the end you'll have stopped doing 30 minutes of copy-paste formatting per client.

## Use it with your Claude.ai subscription
No API key needed. Just your normal Claude.ai login (Pro or Team — these include Skills and Cowork).

**Try it once by hand (2 minutes):**
1. Open **Claude.ai** and start a new chat.
2. Copy **the example prompt** below and paste it into the chat. Press enter.
3. Claude returns a finished status report. That's the output your Skill will produce every time.

**Turn it into a reusable Skill:**
1. In Claude.ai, open the **Skills** menu (left sidebar) and click **Create Skill** (or **New Skill**).
2. Name it `Weekly Client Status Report`.
3. Open the `skill.md` file in this folder, copy **everything** in it, and paste it into the Skill instructions box. Click **Save**.
4. Now in any chat just type `/` and pick **Weekly Client Status Report**, then paste your client's data. The report comes out formatted.

**Make it run automatically (Cowork):**
1. Open `automation-playbook.md` in this folder — it is a complete, step-by-step recipe.
2. Follow it to connect your Google Sheet of client data and schedule a Friday 4 PM run in Cowork.

No API key needed at any step. Everything runs inside your Claude.ai subscription.

## The example prompt
Copy this exactly into Claude.ai to see the result right away:

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

## Make it your own
- Swap the Apex Logistics data for one of your own (anonymised) client projects.
- Add a section your clients expect — e.g. **Budget status** or **Hours used** — by editing `skill.md`.
- Change the tone in `skill.md` (e.g. "warmer and less formal") to match how you talk to your clients.
