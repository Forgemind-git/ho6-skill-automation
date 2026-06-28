# Automation Playbook — Meeting Action Extractor

## Overview

This playbook connects the Meeting Action Extractor Skill to your meeting transcription tool. When a meeting ends and the transcript is ready, the automation extracts all actions and creates tasks directly in your project management tool — no copy-pasting required.

## Prerequisites

- [ ] Claude Cowork account with Automation module enabled
- [ ] Meeting transcription tool connected: Otter.ai, Fireflies.ai, or Zoom cloud recording with auto-transcription
- [ ] Task management tool connected: Linear, Notion, Asana, or Jira
- [ ] Slack connected (for team notifications)
- [ ] The `skill.md` uploaded to Cowork Skill Library as `Meeting Action Extractor`

## Supported Transcription Tool Connections

### Option A: Fireflies.ai (Recommended)
Fireflies has a native webhook that fires when a meeting transcript is ready. In Fireflies Settings > Webhooks, add your Cowork webhook URL and select the `transcript_ready` event.

### Option B: Otter.ai
Otter does not have native webhooks. Use a Zapier/Make.com connector between Otter and Cowork, triggering when a new transcript appears in your Otter workspace.

### Option C: Zoom
Enable Zoom cloud recording auto-transcription in your Zoom account settings. Use Zoom's webhook to fire a `recording.transcript_completed` event to your Cowork automation webhook URL.

## Step-by-Step Setup

### Step 1: Upload the Skill

1. Cowork > **Skill Library** > **+ New Skill**
2. Name: `Meeting Action Extractor`
3. Paste contents of `skill.md`
4. Click **Save & Publish**

### Step 2: Get Your Cowork Webhook URL

1. **Automations** > **+ New Automation**
2. Set trigger type to **Webhook — Incoming**
3. Copy the generated webhook URL (e.g., `https://cowork.app/webhooks/abc123xyz`)
4. You will use this URL in Steps 3a, 3b, or 3c below

### Step 3a: Connect Fireflies.ai

1. Open Fireflies.ai > **Settings** > **Integrations** > **Webhooks**
2. Add New Webhook: paste your Cowork webhook URL
3. Select event: `transcript_ready`
4. Click **Save**. Fireflies will now POST to Cowork when each transcript completes.

Fireflies webhook payload includes:
```json
{
  "meetingTitle": "Product Sprint Review",
  "date": "2025-06-25",
  "transcript": "Full transcript text here...",
  "participants": ["Riya", "Carlos", "Nina"]
}
```

### Step 4: Connect Linear (or Notion)

**Linear:**
1. **Integrations** > **Linear** > **Connect**
2. Authorise with your Linear workspace
3. Select the default team where meeting tasks should be created
4. Set default label: `meeting-action`

**Notion (alternative):**
1. **Integrations** > **Notion** > **Connect**
2. Select a database called `Action Items` with columns: Title, Owner, Due Date, Priority, Source Meeting, Status

### Step 5: Build the Automation

1. **Automations** > open the automation you created in Step 2
2. Name: `Meeting Action Extractor`
3. **Trigger:** Webhook — Incoming (already set)
4. **Action 1 — Run Skill:**
   - Action type: `Run Skill`
   - Skill: `Meeting Action Extractor`
   - Input prompt:
     ```
     Meeting: {{webhook.meetingTitle}}
     Date: {{webhook.date}}
     Attendees: {{webhook.participants | join(", ")}}

     Notes:
     {{webhook.transcript}}
     ```
   - Store result as: `{{extraction_result}}`
5. **Action 2 — Parse JSON actions:**
   - Action type: `Extract JSON from Text`
   - Source: `{{extraction_result}}`
   - JSON path: find the array after `### JSON (for task tool import)`
   - Store as: `{{actions}}`
6. **Action 3 — Loop over actions:**
   - Action type: `For Each`
   - Collection: `{{actions}}`
   - Variable: `{{action}}`
7. **Action 4 — Create task (inside loop):**
   - Action type: `Linear — Create Issue` (or Notion — Create Page)
   - Title: `{{action.action}}`
   - Assignee: (map owner name to Linear member — set up a lookup table in Cowork for name → email)
   - Due date: `{{action.due_date}}`
   - Priority: Map High→Urgent, Medium→Medium, Low→Low
   - Label: `meeting-action`
   - Description: `Source meeting: {{webhook.meetingTitle}} ({{webhook.date}})`
8. **Action 5 — Send Slack Summary (outside loop, after):**
   - Action type: `Slack — Send Message`
   - Channel: `#team-actions` (or use a lookup to find the meeting attendees' Slack channel)
   - Message:
     ```
     Meeting actions extracted from *{{webhook.meetingTitle}}* ({{webhook.date}})

     {{extraction_result | extract_markdown_table}}

     Tasks have been created in Linear. Total: {{actions | length}} actions.
     ```
9. Click **Save** and **Activate**

### Step 6: Test the Automation

1. Trigger a test by sending a POST request to your webhook URL with sample data:
   ```bash
   curl -X POST https://cowork.app/webhooks/abc123xyz \
     -H "Content-Type: application/json" \
     -d '{
       "meetingTitle": "Test Meeting",
       "date": "2025-06-25",
       "participants": ["Alice", "Bob"],
       "transcript": "Alice will send the proposal by Thursday. Bob to review the budget by end of week."
     }'
   ```
2. Check the Automation Log for each step
3. Verify Linear tasks were created for both actions
4. Check Slack for the summary message
5. Confirm action phrasing, owner, and priority are correct

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Webhook never fires | Fireflies not connected | Re-check webhook URL is saved in Fireflies Settings |
| Skill returns no actions | Transcript is empty or too short | Ensure the transcript body is in `{{webhook.transcript}}` not a URL |
| JSON not parsed | Skill output format changed | Verify Skill instructions still say to output the JSON block after `### JSON` |
| Linear tasks not assigned | Name lookup failing | Build a lookup table: name → Linear member ID in Cowork Variables |
| Slack message not formatted | Markdown table extract failing | Fall back to posting the raw `{{extraction_result}}` text |

## Going Further

- Add a Cowork variable lookup table that maps common nicknames to full names (e.g., "Car" → "Carlos") to improve owner matching
- Add a daily digest: at 9 AM, pull all Linear issues with label `meeting-action` created yesterday and post a summary to the team lead
- Connect to your calendar: when a meeting invite is created in Google Calendar, auto-create a placeholder action in Linear with a reminder to run the extractor after the meeting
