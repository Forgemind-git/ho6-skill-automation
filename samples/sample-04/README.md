# HO6 Sample 4 — Meeting Action Extractor

## What you'll build
A reusable Claude **Skill** that reads messy meeting notes and pulls out every real action item — rewritten clearly, with an owner, a due date, and a priority — as a tidy table plus a JSON list you can drop straight into a task tool. Then you'll have Claude **Cowork** run it on every meeting transcript automatically, so follow-ups never get lost again.

## Use it with your Claude.ai subscription
No API key needed. Just your normal Claude.ai login (Pro or Team — these include Skills and Cowork).

**Try it once by hand (2 minutes):**
1. Open **Claude.ai** and start a new chat.
2. Copy **the example prompt** below and paste it into the chat. Press enter.
3. Claude returns a clean action table and a JSON list. That's what your Skill will produce.

**Turn it into a reusable Skill:**
1. In Claude.ai, open the **Skills** menu and click **Create Skill** (or **New Skill**).
2. Name it `Meeting Action Extractor`.
3. Open the `skill.md` file in this folder, copy **everything** in it, paste it into the Skill instructions box, and click **Save**.
4. In any chat, type `/`, pick **Meeting Action Extractor**, and paste your notes.

**Make it run automatically (Cowork):**
1. Open `automation-playbook.md` in this folder — it connects your transcription tool (Fireflies, Otter, or Zoom) and creates the tasks for you.
2. Follow it so that the moment a meeting ends, the actions appear in Linear or Notion and a summary posts to Slack.

No API key needed at any step. Everything runs inside your Claude.ai subscription.

## The example prompt
Copy this exactly into Claude.ai to see the result right away:

```
You are an expert meeting coordinator. From the notes below, extract EVERY genuine action item someone committed to. Ignore general discussion. Rewrite each action as a clear, verb-first task. For each, find the owner (use the team name if no person, or [Owner TBC] if unknown), the due date (keep relative dates like "by Friday" exactly as stated; use TBC if none — never invent a date), and a priority (High = blocking/customer-facing/urgent, Medium = important, Low = nice to have). Return a Markdown table first (columns: #, Action, Owner, Due Date, Priority), then an identical JSON array.

Meeting: Product Sprint Review + Planning
Date: June 25, 2025
Attendees: Riya (PM), Carlos (Backend), Nina (Frontend), Jake (Design), Tom (QA)

Notes:
- Reviewed sprint 14 — 8/10 tickets done.
- Carlos flagged the payment gateway is timing out under load. He'll investigate connection pooling and send Riya an update by end of day Thursday.
- Nina said the mobile nav has a bug on iOS 16 — she'll fix it and push a PR by tomorrow EOD.
- Jake will share the updated onboarding designs in Figma by end of this week; they need Riya's sign-off before dev starts.
- Tom raised the regression suite hasn't been updated since March; he'll add coverage for the billing module by next Wednesday.
- ACTION: Riya to schedule the Q3 roadmap planning session next week.
- The team discussed a new testing framework but agreed to defer the decision. No action needed.
- Carlos to review Jake's designs in Figma and leave comments by Friday.
```

## Make it your own
- Paste in your own real meeting notes — the messier, the better a test.
- Add a column your team needs (e.g. **Project** or **Linear label**) by editing `skill.md`.
- Tell the Skill to ignore certain owners (e.g. external clients) so only internal tasks come through.
