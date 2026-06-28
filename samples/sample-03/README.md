# Sample 03 — Monthly Metrics Deck Skill

## Problem Statement

Every month, managers and analysts spend 3–5 hours building slide decks from metrics spreadsheets. They extract numbers, write commentary, identify trends, and design slides — all repetitive work that follows the same pattern each month. Claude can turn a metrics table into a complete, narrative slide deck outline in under 90 seconds, ready to paste into PowerPoint or Google Slides.

## What the Skill Does

The **Monthly Metrics Deck Skill** takes a raw metrics table (actual vs target values for the month) and produces a complete 5-slide deck outline:

1. **Executive Summary** — one headline number and a 2-sentence verdict
2. **KPIs vs Target** — a formatted comparison table with RAG status for each metric
3. **Highlights** — the top 3 wins with context explaining why they matter
4. **Risks** — the top 2–3 risks with recommended mitigations
5. **Next Month Focus** — 3 prioritised actions with owners

Each slide includes a suggested title, speaker notes, and a one-line chart/visual recommendation.

## What the Automation Does

The `automation-playbook.md` describes how to connect this Skill to a scheduled monthly trigger in Claude Cowork:

- On the first working day of each month, the automation reads the metrics from a Google Sheet
- Passes the data to this Skill
- Writes the deck outline to a Notion document
- Creates a Google Slides deck with the slide titles pre-filled
- Notifies the team lead via email

## Use it with your Claude.ai subscription

No API key needed — this runs entirely on your Claude.ai subscription (Pro or Team, which include Skills and Cowork).

1. **See it work first.** Open **Claude.ai**, start a new chat, and paste **the example prompt** below. Claude returns a full 5-slide outline.
2. **Save it as a Skill.** Open the **Skills** menu → **Create Skill**, name it `Monthly Metrics Deck`, and paste in the full contents of `skill.md`. Save.
3. **Use it any time.** In a chat, type `/`, choose **Monthly Metrics Deck**, and paste your own KPI table.
4. **Automate it (optional).** Follow `automation-playbook.md` to have Cowork read your KPI sheet and build the Notion outline + Google Slides deck on the first of each month.

## The example prompt

Copy this into Claude.ai to reproduce the worked example in `skill.md`:

```
You are a senior business analyst. Turn the KPI table below into a 5-slide monthly business review outline: (1) Executive Summary with one headline metric and a 2-sentence verdict; (2) KPIs vs Target table with % vs target ((actual-target)/target*100, 1 decimal), a month-on-month arrow, and a RAG status (Green = at/above target, Amber = within 10% below, Red = more than 10% below); (3) top 3 Highlights, each with one sentence of business context; (4) top 2–3 Risks, each with a concrete mitigation; (5) Next Month Focus — 3 prioritised actions, each with an owner. Add 2–3 sentences of speaker notes and a one-line chart suggestion per slide. Do not invent metrics.

Team: Growth & Revenue
Month: June 2025

KPI Data:
Metric               | Target  | Actual  | Prior Month
New MRR              | $120,000| $129,600| $111,000
Churn Rate           | <2%     | 2.8%    | 2.1%
Trial-to-Paid Conv.  | 18%     | 21.4%   | 17.5%
CAC (blended)        | $320    | $298    | $335
NPS Score            | 45      | 43      | 41
Support CSAT         | 90%     | 94%     | 92%
Pipeline Coverage    | 3.5x    | 2.9x    | 3.2x
```

The full example output is in `skill.md` under **Example Output**.

## Make it your own

- Replace the Growth & Revenue numbers with your own team's KPIs.
- Add or remove slides in `skill.md` (e.g. a "Budget vs Spend" slide).
- Tell the Skill your audience (e.g. "the board" vs "the team") so it pitches the tone correctly.

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time to build deck outline | 3.5 hr | 5 min (review + edit) |
| Decks per month | 3 (three teams) | 3 |
| Total time per month | 10.5 hr | 15 min |
| Hours saved per month | **10.25 hr** | — |
| Hours saved per year | **~123 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
