# Automation Playbook — Weekly Client Status Report

## Overview

This playbook connects the Weekly Client Status Report Skill to a Google Sheets data source via Claude Cowork. Every Friday at 4 PM the automation reads your project tracker sheet, runs the Skill for each client row, and posts the formatted reports to Notion.

## Prerequisites

Before starting:

- [ ] Claude Cowork account with Automation module enabled
- [ ] Google Sheets with your weekly project tracker (see column format below)
- [ ] Notion integration connected in Cowork (Settings > Integrations > Notion)
- [ ] Slack webhook URL (optional, for notifications)
- [ ] The `skill.md` from this folder uploaded to your Cowork Skill Library

## Google Sheets Column Format

Your tracker sheet must have these columns in order (add them if missing):

| Column | Header | Example |
|--------|--------|---------|
| A | client_name | Apex Logistics |
| B | project_name | WMS v2 |
| C | week_start | 2025-06-23 |
| D | week_end | 2025-06-27 |
| E | completed_tasks | Migrated 3 DBs; UAT sign-off received |
| F | in_progress_tasks | 2 DB migrations (60%); Training materials (40%) |
| G | blockers | VPN credentials missing [High, Apex IT]; Room booking delayed [Low] |
| H | next_week_planned | Complete migrations Jun 30; Submit materials Jul 1 |
| I | report_status | PENDING (leave as PENDING; automation will update to DONE) |

Separate multiple items in columns E–H with a semicolon (`;`).

## Step-by-Step Setup in Claude Cowork

### Step 1: Upload the Skill

1. Open Claude Cowork and navigate to **Skill Library** (left sidebar)
2. Click **+ New Skill**
3. Name it: `Weekly Client Status Report`
4. Paste the full contents of `skill.md` into the Skill editor
5. Click **Save & Publish**
6. Note the Skill ID shown in the URL (e.g., `skill_abc123`) — you will need it in Step 4

### Step 2: Connect Google Sheets

1. Go to **Integrations** > **Google Sheets**
2. Click **Connect** and authorise with your Google account
3. Select your project tracker spreadsheet
4. Select the sheet tab (e.g., `Weekly Tracker`)
5. Click **Save Connection** — Cowork will auto-detect the columns

### Step 3: Connect Notion (Output)

1. Go to **Integrations** > **Notion**
2. Click **Connect** and authorise with your Notion workspace
3. Select the database where reports should be posted (e.g., `Client Status Reports`)
4. Map fields: `Client` → `client_name`, `Week` → `week_start`, `Report` → (full text output)
5. Click **Save Connection**

### Step 4: Create the Automation

1. Navigate to **Automations** > **+ New Automation**
2. Set the name: `Weekly Status Reports — Friday Run`
3. **Trigger:** Scheduled
   - Frequency: Weekly
   - Day: Friday
   - Time: 16:00 (your timezone)
4. **Action 1 — Read Sheet:**
   - Action type: `Google Sheets — Get Rows`
   - Filter: `report_status = PENDING`
   - Store result as: `{{client_rows}}`
5. **Action 2 — Loop:**
   - Action type: `For Each`
   - Collection: `{{client_rows}}`
   - Variable: `{{row}}`
6. **Action 3 — Run Skill (inside loop):**
   - Action type: `Run Skill`
   - Skill: `Weekly Client Status Report`
   - Input prompt:
     ```
     Client: {{row.client_name}}
     Project: {{row.project_name}}
     Week: {{row.week_start}} to {{row.week_end}}

     COMPLETED THIS WEEK:
     {{row.completed_tasks}}

     IN PROGRESS:
     {{row.in_progress_tasks}}

     BLOCKERS:
     {{row.blockers}}

     PLANNED NEXT WEEK:
     {{row.next_week_planned}}
     ```
   - Store result as: `{{report_output}}`
7. **Action 4 — Write to Notion (inside loop):**
   - Action type: `Notion — Create Page`
   - Database: your connected database
   - Title: `{{row.client_name}} — Week of {{row.week_start}}`
   - Body: `{{report_output}}`
8. **Action 5 — Update Sheet (inside loop):**
   - Action type: `Google Sheets — Update Cell`
   - Row: current row
   - Column I: `DONE`
9. **Action 6 — Slack Notification (optional, outside loop):**
   - Action type: `Slack — Send Message`
   - Channel: `#account-managers`
   - Message: `Weekly status reports are ready in Notion. {{client_rows.length}} reports generated.`
10. Click **Save** and then **Activate**

### Step 5: Test the Automation

1. Add one test row to your Google Sheet with `report_status = PENDING`
2. In the Automation editor, click **Run Now** (manual trigger)
3. Watch the Automation Log for each action step
4. Check your Notion database for the new report page
5. Verify the report format matches the skill output template
6. If the test row processed correctly, change `report_status` back to `PENDING` to re-run, or delete the test row

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| No rows picked up | Filter not matching | Check column I says exactly `PENDING` (case-sensitive) |
| Skill output is empty | Skill not published | Go to Skill Library and confirm status is Published |
| Notion page not created | Auth expired | Re-connect Notion integration in Settings |
| Report health is wrong | Blocker format mismatch | Ensure blockers include `[High]` or `[Medium]` tags |
| Loop runs 0 times | Sheet connection wrong tab | Re-select the correct sheet tab in the integration |

## Going Further

- Add an email action (Action 7) to send each report directly to the client contact stored in a column J `client_email`
- Add a conditional branch: if `health = Blocked`, send an additional Slack alert to the delivery director
- Schedule a second run on Monday morning to catch any rows added over the weekend
