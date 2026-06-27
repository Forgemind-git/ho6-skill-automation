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

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time to extract actions per meeting | 20 min | 1 min (review) |
| Meetings per week | 8 | 8 |
| Total time per week | 2.7 hr | 8 min |
| Hours saved per week | **2.5 hr** | — |
| Hours saved per month | **~10 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
