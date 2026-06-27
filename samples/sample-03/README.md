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

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time to build deck outline | 3.5 hr | 5 min (review + edit) |
| Decks per month | 3 (three teams) | 3 |
| Total time per month | 10.5 hr | 15 min |
| Hours saved per month | **10.25 hr** | — |
| Hours saved per year | **~123 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
