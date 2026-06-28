# Sample 04 — Meeting Action Extractor Skill

## Problem Statement

After every meeting, someone has to scroll through notes, highlight action items, figure out who owns each one, decide deadlines, and paste them into a task manager. This takes 15–25 minutes per meeting and the result is often incomplete — vague actions with no owner or no date. Claude can extract every action item from raw meeting notes in seconds, producing a clean, structured table ready to import into any task tool.

## What the Skill Does

The **Meeting Action Extractor Skill** reads raw meeting notes (transcript excerpt, bullet notes, or prose) and returns a structured table of action items with:

- **Action** — clear, specific task starting with a verb
- **Owner** — the person or team responsible
- **Due Date** — extracted from notes or inferred as [next meeting / end of week / TBC]
- **Priority** — `High`, `Medium`, or `Low` based on context signals in the notes

The output is a Markdown table and a JSON array so it can be used directly in task management tools (Linear, Jira, Asana, Notion, etc.).

## What the Automation Does

The `automation-playbook.md` describes how to connect this Skill to a meeting tool trigger in Claude Cowork:

- When a meeting recording is transcribed (via Otter.ai, Fireflies, or a Zoom webhook), the transcript is passed to this Skill
- Extracted actions are automatically created as tasks in Linear or Notion
- A Slack summary is posted to the meeting attendees channel
- The meeting host receives an email with the full action table

## Use it with your Claude.ai subscription

No API key needed — this runs entirely on your Claude.ai subscription (Pro or Team, which include Skills and Cowork).

1. **See it work first.** Open **Claude.ai**, start a new chat, and paste **the example prompt** below. Claude returns a clean action table and a JSON list.
2. **Save it as a Skill.** Open the **Skills** menu → **Create Skill**, name it `Meeting Action Extractor`, and paste in the full contents of `skill.md`. Save.
3. **Use it any time.** In a chat, type `/`, choose **Meeting Action Extractor**, and paste your own meeting notes.
4. **Automate it (optional).** Follow `automation-playbook.md` to have Cowork read each transcript (Fireflies, Otter, or Zoom) and create tasks in Linear or Notion automatically.

## The example prompt

Copy this into Claude.ai to reproduce the worked example in `skill.md`:

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

The full example output is in `skill.md` under **Example Output**.

## Make it your own

- Paste in your own real meeting notes — the messier, the better a test.
- Add a column your team needs (e.g. **Project** or **Linear label**) by editing `skill.md`.
- Tell the Skill to ignore certain owners (e.g. external clients) so only internal tasks come through.

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time to extract actions per meeting | 20 min | 1 min (review) |
| Meetings per week | 8 | 8 |
| Total time per week | 2.7 hr | 8 min |
| Hours saved per week | **2.5 hr** | — |
| Hours saved per month | **~10 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
