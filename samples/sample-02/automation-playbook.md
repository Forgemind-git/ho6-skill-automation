# Automation Playbook — Inbox Triage & Draft

## Overview

This playbook connects the Inbox Triage & Draft Skill to your support email inbox via Claude Cowork. When a new email arrives, the automation classifies it, drafts a reply, and routes it to the right place — all before a human opens it.

## Prerequisites

- [ ] Claude Cowork account with Automation module enabled
- [ ] Gmail or Outlook inbox connected in Cowork (Settings > Integrations)
- [ ] CRM or ticketing tool connected (Zendesk / HubSpot / Notion — choose one)
- [ ] Slack workspace connected (for Priority-1 alerts)
- [ ] The `skill.md` from this folder uploaded to your Cowork Skill Library as `Inbox Triage & Draft`

## Step-by-Step Setup in Claude Cowork

### Step 1: Upload the Skill

1. Open Cowork > **Skill Library** > **+ New Skill**
2. Name it: `Inbox Triage & Draft`
3. Paste the full contents of `skill.md` into the editor
4. Click **Save & Publish**

### Step 2: Connect Your Support Inbox

1. Go to **Integrations** > **Gmail** (or Outlook)
2. Authorise with the support email account (e.g., support@yourcompany.com)
3. Create a label/folder called `triage-pending` in your inbox
4. In Cowork, set the trigger to watch for emails arriving in that label
5. Click **Save Connection**

**Tip:** Set up a Gmail filter to auto-label incoming emails to `support@yourcompany.com` as `triage-pending`. This way only support emails trigger the automation.

### Step 3: Connect Your CRM / Ticketing Tool

Option A — Zendesk:
1. Go to **Integrations** > **Zendesk**
2. Enter your Zendesk subdomain and API token
3. Set it to create a new ticket per processed message

Option B — Notion:
1. Go to **Integrations** > **Notion**
2. Select a database called `Support Inbox` with columns: ID, Category, Priority, Draft, Escalate, Status

### Step 4: Create the Automation

1. **Automations** > **+ New Automation**
2. Name: `Support Inbox Triage`
3. **Trigger:** Gmail/Outlook — New Email in label `triage-pending`
   - Variables available: `{{email.from}}`, `{{email.subject}}`, `{{email.body}}`, `{{email.id}}`
4. **Action 1 — Generate Message ID:**
   - Action type: `Set Variable`
   - Variable: `{{msg_id}}`
   - Value: `MSG-{{email.id}}`
5. **Action 2 — Run Skill:**
   - Action type: `Run Skill`
   - Skill: `Inbox Triage & Draft`
   - Input prompt:
     ```
     {{msg_id}}
     From: {{email.from}}
     Subject: {{email.subject}}

     {{email.body}}
     ```
   - Store result as: `{{triage_result}}`
6. **Action 3 — Parse JSON:**
   - Action type: `Parse JSON`
   - Input: `{{triage_result}}`
   - Extract fields: `category`, `priority`, `draft_reply`, `escalate`
   - Store as: `{{triage.category}}`, `{{triage.priority}}`, `{{triage.draft}}`, `{{triage.escalate}}`
7. **Action 4 — Create CRM Record:**
   - Action type: `Zendesk — Create Ticket` (or Notion — Create Page)
   - Subject: `{{email.subject}}`
   - Requester: `{{email.from}}`
   - Priority: `{{triage.priority}}`
   - Tags: `{{triage.category}}`
   - Internal note: `TRIAGE DRAFT:\n{{triage.draft}}\n\nESCALATE: {{triage.escalate}}`
8. **Action 5 — Conditional Branch:**
   - Condition: `{{triage.priority}} = 1 OR {{triage.escalate}} = yes`
   - **If true — Action 5a — Slack Alert:**
     - Action type: `Slack — Send Message`
     - Channel: `#support-urgent`
     - Message: `PRIORITY 1 — New ticket requires immediate attention.\nFrom: {{email.from}}\nSubject: {{email.subject}}\nCategory: {{triage.category}}\nEscalate: {{triage.escalate}}`
9. **Action 6 — Remove Label (Gmail):**
   - Action type: `Gmail — Remove Label`
   - Label: `triage-pending`
   - Add label: `triage-done`
10. Click **Save** and **Activate**

### Step 5: Test the Automation

1. Send a test email to your support inbox with the subject: `Test: API returning errors`
2. Check the email has the `triage-pending` label applied
3. In Cowork, click **Run Now** on the automation
4. Verify the Zendesk/Notion record was created with the draft reply
5. If priority was 1, check Slack for the alert
6. Send a second test email that is clearly `general` category and confirm no Slack alert fires

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Automation never fires | Label not applied to email | Check Gmail filter is correctly routing to `triage-pending` |
| JSON parse fails | Skill outputting extra text | Verify skill instructions say "Do not include any text outside the JSON block" |
| All emails become Priority 1 | Overly sensitive escalation | Review the urgency keyword list in skill.md instructions |
| Draft reply is too short | Token limit hit | Split large email bodies into first 500 words only |
| Slack alert fires for every email | Condition wrong | Check condition logic: priority = 1 OR escalate = yes (not AND) |

## Going Further

- Add Action 7: auto-create a draft reply in Gmail using `{{triage.draft}}` so the agent just clicks Send
- Add a daily digest automation that runs at 9 AM, pulls all Priority-2 and -3 records from the CRM, and posts a summary to Slack
- Build a feedback loop: when an agent edits the draft significantly before sending, log the edit and use it to improve the Skill instructions over time
