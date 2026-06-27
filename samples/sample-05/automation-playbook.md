# Automation Playbook — Content Repurposer

## Overview

This playbook connects the Content Repurposer Skill to your CMS publishing workflow. When you publish a new article, the automation generates the full social media package and routes each piece to your content calendar in Notion, ready for the social media manager to review and schedule.

## Prerequisites

- [ ] Claude Cowork account with Automation module enabled
- [ ] CMS connected: WordPress (via webhook/REST API), Webflow, or Ghost
- [ ] Notion connected with a `Content Calendar` database
- [ ] Slack connected (for team notifications)
- [ ] Buffer or Hootsuite connected (optional, for direct scheduling)
- [ ] The `skill.md` uploaded to Cowork Skill Library as `Content Repurposer`

## Content Calendar Database Setup (Notion)

Create a Notion database called `Content Calendar` with these properties:

| Property | Type | Options |
|----------|------|---------|
| Title | Title | — |
| Platform | Select | LinkedIn, Twitter/X Thread, Newsletter |
| Angle | Select | Insight, Story, Contrarian, Thread, Blurb |
| Status | Select | Draft, Needs Review, Approved, Scheduled, Published |
| Source Article | URL | — |
| Publish Date | Date | — |
| Assigned To | Person | — |
| Word Count | Number | — |

## Step-by-Step Setup

### Step 1: Upload the Skill

1. Cowork > **Skill Library** > **+ New Skill**
2. Name: `Content Repurposer`
3. Paste contents of `skill.md`
4. Click **Save & Publish**

### Step 2: Connect Your CMS

**Option A — WordPress:**
1. In your WordPress admin, go to **Settings** > **Webhooks** (install WP Webhooks plugin if needed)
2. Create a webhook for the `publish_post` event
3. Paste your Cowork webhook URL (you'll get this in Step 4)
4. Payload will include: `post_title`, `post_content`, `post_url`, `post_author`

**Option B — Ghost:**
1. In Ghost Admin, go to **Settings** > **Integrations** > **Add Custom Integration**
2. Under Webhooks, add a `Post published` webhook pointing to your Cowork URL
3. Payload includes: `post.title`, `post.html`, `post.url`, `post.authors[0].name`

**Option C — Webflow:**
1. In Webflow > **Project Settings** > **Integrations** > **Webhooks**
2. Add webhook for `collection_item_published`
3. Filter to your Blog collection

### Step 3: Connect Notion

1. **Integrations** > **Notion** > **Connect**
2. Select the `Content Calendar` database
3. Save connection

### Step 4: Create the Automation

1. **Automations** > **+ New Automation**
2. Name: `Content Repurposer — New Article Published`
3. **Trigger:** Webhook — Incoming
4. Copy the webhook URL and add it to your CMS (Step 2)
5. **Action 1 — Run Skill:**
   - Action type: `Run Skill`
   - Skill: `Content Repurposer`
   - Input prompt:
     ```
     Article Title: {{webhook.post_title}}
     Author: {{webhook.post_author}}

     {{webhook.post_content | strip_html | truncate_words(1500)}}
     ```
   - Store result as: `{{content_package}}`

   Note: `truncate_words(1500)` prevents excessively long inputs. Most articles under 3,000 words will not need truncation.

6. **Action 2 — Extract LinkedIn Post 1 (Insight):**
   - Action type: `Extract Text Between Markers`
   - Source: `{{content_package}}`
   - Start marker: `### LinkedIn Post 1 — Insight Angle`
   - End marker: `---`
   - Store as: `{{li_insight}}`

7. **Action 3 — Extract LinkedIn Post 2 (Story):**
   - Same as Action 2 but start marker: `### LinkedIn Post 2 — Story Angle`
   - Store as: `{{li_story}}`

8. **Action 4 — Extract LinkedIn Post 3 (Contrarian):**
   - Start marker: `### LinkedIn Post 3 — Contrarian Angle`
   - Store as: `{{li_contrarian}}`

9. **Action 5 — Extract Twitter Thread:**
   - Start marker: `### Twitter/X Thread`
   - Store as: `{{twitter_thread}}`

10. **Action 6 — Extract Newsletter Blurb:**
    - Start marker: `### Newsletter Blurb`
    - Store as: `{{newsletter_blurb}}`

11. **Action 7 — Create LinkedIn Post 1 in Notion:**
    - Action type: `Notion — Create Page`
    - Database: `Content Calendar`
    - Title: `{{webhook.post_title}} — LinkedIn (Insight)`
    - Platform: `LinkedIn`
    - Angle: `Insight`
    - Status: `Needs Review`
    - Source Article: `{{webhook.post_url}}`
    - Body: `{{li_insight}}`

12. **Actions 8–11:** Repeat for Story, Contrarian, Twitter Thread, and Newsletter Blurb with appropriate property values

13. **Action 12 — Slack Notification:**
    - Action type: `Slack — Send Message`
    - Channel: `#content-team`
    - Message:
      ```
      New content package ready for review! :pencil:

      Article: *{{webhook.post_title}}*

      5 pieces created in Notion Content Calendar:
      - 3 LinkedIn posts (Insight, Story, Contrarian angles)
      - 1 Twitter/X thread (5 tweets)
      - 1 Newsletter blurb (150 words)

      Review and approve here: [Content Calendar link]
      ```

14. Click **Save** and **Activate**

### Step 5: Test the Automation

1. Send a test webhook with a sample article payload:
   ```bash
   curl -X POST https://cowork.app/webhooks/your-webhook-id \
     -H "Content-Type: application/json" \
     -d '{
       "post_title": "Test Article: How to Run Better Meetings",
       "post_author": "Test Author",
       "post_url": "https://yoursite.com/test-article",
       "post_content": "Meetings waste time. Here are three ways to fix them. First, send an agenda 24 hours before. Second, keep meetings under 30 minutes. Third, assign action items before the call ends."
     }'
   ```
2. Check Automation Log for each extraction step
3. Verify 5 Notion pages were created in the Content Calendar
4. Check Slack for the notification message
5. Review each piece for quality and formatting

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Skill output is missing posts | Article too long, truncated | Adjust `truncate_words` limit or pass a summary instead of full content |
| Notion pages have empty body | Extraction markers not matching | Check skill output includes exact marker text `### LinkedIn Post 1 — Insight Angle` |
| HTML tags in article content | `strip_html` filter not applied | Ensure `post_content | strip_html` is in the input template |
| Webhook never fires | CMS not saving URL | Re-check CMS webhook settings; test with webhook.site first |
| Twitter tweets over 280 chars | Skill instructions not followed | Add a validation step and re-run the skill with a note to shorten tweets |

## Going Further

- Add a Buffer or Hootsuite step (Action 13+) to schedule each LinkedIn post for specific times across the following week
- Build an A/B test workflow: run the skill twice with different temperature settings and present both versions to the social manager for selection
- Add a performance tracking step: after 7 days, pull engagement metrics from LinkedIn and feed them back into a learning doc to improve future angles
