# HO6 Sample 3 — Monthly Metrics Deck

## What you'll build
A reusable Claude **Skill** that takes a plain table of monthly numbers (actual vs target) and turns it into a complete 5-slide business-review deck outline — executive summary, a traffic-light KPI table, highlights, risks with mitigations, and next-month actions, all with speaker notes. Then you'll have Claude **Cowork** run it on the first of every month, so the deck practically builds itself.

## Use it with your Claude.ai subscription
No API key needed. Just your normal Claude.ai login (Pro or Team — these include Skills and Cowork).

**Try it once by hand (2 minutes):**
1. Open **Claude.ai** and start a new chat.
2. Copy **the example prompt** below and paste it into the chat. Press enter.
3. Claude returns a full 5-slide outline. That's what your Skill will produce every month.

**Turn it into a reusable Skill:**
1. In Claude.ai, open the **Skills** menu and click **Create Skill** (or **New Skill**).
2. Name it `Monthly Metrics Deck`.
3. Open the `skill.md` file in this folder, copy **everything** in it, paste it into the Skill instructions box, and click **Save**.
4. In any chat, type `/`, pick **Monthly Metrics Deck**, and paste your KPI table.

**Make it run automatically (Cowork):**
1. Open `automation-playbook.md` in this folder — it shows how to read your KPI Google Sheet and create the Notion outline + Google Slides deck on a schedule.
2. Follow it to get a finished deck on the first working day of each month, no copy-paste.

No API key needed at any step. Everything runs inside your Claude.ai subscription.

## The example prompt
Copy this exactly into Claude.ai to see the result right away:

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

## Make it your own
- Replace the Growth & Revenue numbers with your own team's KPIs.
- Add or remove slides in `skill.md` (e.g. a "Budget vs Spend" slide).
- Tell the Skill your audience (e.g. "the board" vs "the team") so it pitches the tone correctly.
