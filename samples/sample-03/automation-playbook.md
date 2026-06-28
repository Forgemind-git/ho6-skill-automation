# Automation Playbook — Monthly Metrics Deck

## Overview

This playbook runs the Monthly Metrics Deck Skill on the first working day of each month. It reads your KPI sheet, generates the full deck outline, writes it to Notion, and pre-populates a Google Slides deck with slide titles ready for your team to present.

## Prerequisites

- [ ] Claude Cowork account with Automation module enabled
- [ ] Google Sheets with your monthly KPI tracker (format below)
- [ ] Google Slides connected in Cowork (for deck creation)
- [ ] Notion connected (for the narrative outline)
- [ ] Email integration connected (for stakeholder notification)
- [ ] The `skill.md` uploaded to Cowork Skill Library as `Monthly Metrics Deck`

## Google Sheets KPI Tracker Format

Create a sheet called `Monthly KPIs` with these columns:

| Column | Header | Example |
|--------|--------|---------|
| A | team_name | Growth & Revenue |
| B | month_year | June 2025 |
| C | kpi_name | New MRR |
| D | target | 120000 |
| E | actual | 129600 |
| F | prior_month | 111000 |
| G | unit | $ (use %, x, score, or $ ) |
| H | processed | NO |

Each KPI is one row. Multiple rows share the same `team_name` and `month_year`.

## Step-by-Step Setup

### Step 1: Upload the Skill

1. Cowork > **Skill Library** > **+ New Skill**
2. Name: `Monthly Metrics Deck`
3. Paste contents of `skill.md`
4. Click **Save & Publish**

### Step 2: Connect Google Sheets

1. **Integrations** > **Google Sheets** > **Connect**
2. Select your KPI tracker spreadsheet and `Monthly KPIs` sheet
3. Save the connection

### Step 3: Connect Google Slides

1. **Integrations** > **Google Slides** > **Connect**
2. Authorise with the same Google account
3. Select a template presentation (create a blank 5-slide deck as your template)
4. Note the template presentation ID from the URL

### Step 4: Create the Automation

1. **Automations** > **+ New Automation**
2. Name: `Monthly Metrics Deck Builder`
3. **Trigger:** Scheduled
   - Frequency: Monthly
   - Day: First Monday of month (or Day 1)
   - Time: 08:00
4. **Action 1 — Get Distinct Teams:**
   - Action type: `Google Sheets — Get Unique Values`
   - Column: `team_name`
   - Filter: `month_year = {{current_month_year}}` AND `processed = NO`
   - Store as: `{{teams}}`
5. **Action 2 — Loop over teams:**
   - Action type: `For Each`
   - Collection: `{{teams}}`
   - Variable: `{{team}}`
6. **Action 3 — Get Team KPIs (inside loop):**
   - Action type: `Google Sheets — Get Rows`
   - Filter: `team_name = {{team}}` AND `month_year = {{current_month_year}}`
   - Store as: `{{kpi_rows}}`
7. **Action 4 — Format KPI Table (inside loop):**
   - Action type: `Set Variable`
   - Variable: `{{kpi_table}}`
   - Value (template):
     ```
     Team: {{team}}
     Month: {{current_month_year}}

     KPI Data:
     Metric | Target | Actual | Prior Month
     {{kpi_rows[*].kpi_name}} | {{kpi_rows[*].target}} | {{kpi_rows[*].actual}} | {{kpi_rows[*].prior_month}}
     ```
8. **Action 5 — Run Skill (inside loop):**
   - Action type: `Run Skill`
   - Skill: `Monthly Metrics Deck`
   - Input: `{{kpi_table}}`
   - Store as: `{{deck_outline}}`
9. **Action 6 — Write to Notion (inside loop):**
   - Action type: `Notion — Create Page`
   - Database: `Monthly Decks`
   - Title: `{{team}} — {{current_month_year}} Business Review`
   - Body: `{{deck_outline}}`
10. **Action 7 — Create Google Slides (inside loop):**
    - Action type: `Google Slides — Copy Template`
    - Template ID: [your template presentation ID]
    - New name: `{{team}} — {{current_month_year}} Monthly Review`
    - Replace slide 1 title: Extract first `## Slide 1` headline from `{{deck_outline}}`
    - Replace slide 2 title: `KPIs vs Target`
    - Replace slide 3 title: `Highlights`
    - Replace slide 4 title: `Risks & Watch Items`
    - Replace slide 5 title: `Next Month Focus`
    - Store presentation URL as: `{{slides_url}}`
11. **Action 8 — Send Email (inside loop):**
    - Action type: `Email — Send`
    - To: `{{team_lead_email}}` (store in a lookup column in the sheet)
    - Subject: `{{team}} Monthly Review Deck Ready — {{current_month_year}}`
    - Body: `Your monthly metrics deck is ready.\n\nDeck outline (Notion): {{notion_page_url}}\nGoogle Slides: {{slides_url}}\n\nPlease review and present by the end of this week.`
12. **Action 9 — Mark Processed (inside loop):**
    - Action type: `Google Sheets — Update Rows`
    - Filter: `team_name = {{team}}` AND `month_year = {{current_month_year}}`
    - Set column H: `YES`
13. Click **Save** and **Activate**

## Step 5: Test the Automation

1. Populate 5–7 KPI rows for one team in your sheet with the current month
2. Ensure column H says `NO`
3. Click **Run Now** in the Automation editor
4. Check the Automation Log for any errors at each step
5. Verify the Notion page was created with a complete 5-slide outline
6. Verify the Google Slides deck was created with slide titles populated
7. Check the notification email was received

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Loop finds 0 teams | Month/year format mismatch | Ensure `month_year` in sheet matches `{{current_month_year}}` format exactly (e.g., `June 2025`) |
| KPI table is malformed | Row iteration template wrong | Preview the `{{kpi_table}}` variable in the log and compare to expected input format |
| Slides deck not created | Template ID wrong | Copy the presentation ID from the Google Slides URL bar |
| Skill output truncated | Too many KPIs | Split into two runs or reduce KPI count to 10 or fewer per team |
| Email not sent | Team lead email column missing | Add column J `team_lead_email` to your sheet |

## Going Further

- Add a PDF export action (Google Slides — Export as PDF) and attach it directly to the email
- Build a comparison slide that pulls in the same month from last year using a second sheet tab
- Add a team-level confidence score question before the automation runs, asking the lead to rate the data quality 1–5, and include it in the Executive Summary
