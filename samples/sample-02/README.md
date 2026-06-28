# Sample 02 — Inbox Triage & Draft Skill

## Problem Statement

Support teams and customer-facing staff spend 2–3 hours daily reading incoming messages, deciding which are urgent, routing them to the right person, and writing first-draft replies. Most messages fall into predictable categories with predictable responses. Claude can classify and draft all of them in seconds, leaving the human to review and send — not write from scratch.

## What the Skill Does

The **Inbox Triage & Draft Skill** processes a batch of incoming support messages and for each one produces:

- **Category** — `billing`, `technical`, `general`, or `urgent`
- **Priority** — `1` (respond within 1 hour), `2` (respond today), `3` (respond within 48 hours)
- **Draft reply** — a complete, professional response ready to send after a quick human review
- **Escalate** — `yes` or `no` indicating whether a human lead needs to review before sending

The output is a structured JSON array, making it easy to feed into a ticketing system or CRM via automation.

## What the Automation Does

The `automation-playbook.md` describes how to connect this Skill to an email inbox trigger in Claude Cowork:

- New emails arriving in a designated support inbox trigger the automation
- Each email is passed to this Skill
- The triage output is written back to the CRM (HubSpot / Zendesk / Notion)
- Priority-1 messages trigger an immediate Slack alert to the on-call agent
- Priority-2 and -3 drafts are queued in a review dashboard for the team

## Use it with your Claude.ai subscription

No API key needed — this runs entirely on your Claude.ai subscription (Pro or Team, which include Skills and Cowork).

1. **See it work first.** Open **Claude.ai**, start a new chat, and paste **the example prompt** below. Claude returns each message triaged with a draft reply.
2. **Save it as a Skill.** Open the **Skills** menu → **Create Skill**, name it `Inbox Triage & Draft`, and paste in the full contents of `skill.md`. Save.
3. **Use it any time.** In a chat, type `/`, choose **Inbox Triage & Draft**, and paste a batch of your own (anonymised) messages.
4. **Automate it (optional).** Follow `automation-playbook.md` to have Cowork triage new emails the moment they arrive and ping Priority-1 items to Slack.

## The example prompt

Copy this into Claude.ai to reproduce the worked example in `skill.md`:

```
You are an experienced customer support specialist. For each message below, return a JSON array with one object per message containing: id, category (billing / technical / general / urgent), priority (1 = within 1 hour, 2 = today, 3 = within 48 hours), a complete professional draft_reply (open with empathy if the customer is frustrated, give a clear next step, 80–200 words, sign off as "The Support Team"), and escalate (yes / no — yes if urgent or it mentions legal/data breach/major revenue loss). Output only the JSON, nothing else.

MSG-001
From: james.carter@acmecorp.com
Subject: Charged twice for this month??
Hi, I just noticed two charges of $299 on my card this month — one on June 1st and one on June 3rd. I only have one account. Can you refund the duplicate? I've been a customer 3 years and this is really frustrating. James

MSG-002
From: priya.s@startupxyz.io
Subject: API returning 500 errors
Since this morning our integration with your API has been returning 500 errors on the /orders/create endpoint. We process ~200 orders/hour and they're all failing. This is causing real revenue impact. Please fix ASAP. Priya, Lead Engineer

MSG-003
From: dan.howell@personalmail.com
Subject: How do I add a second user?
Hey team, how can I invite a colleague to share my account? I'm on the Business plan. Thanks, Dan
```

The full example output is in `skill.md` under **Example Output**.

## Make it your own

- Replace the three sample messages with real (anonymised) ones from your own queue.
- Add your company's tone and a real signature by editing the draft rules in `skill.md`.
- Change the categories (e.g. add `sales` or `partnerships`) to match how your team routes work.

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time per message (read + draft) | 8 min | 1 min (review only) |
| Messages per day | 40 | 40 |
| Total time per day | 5.3 hr | 40 min |
| Hours saved per day | **4.6 hr** | — |
| Hours saved per month (20 working days) | **~92 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
