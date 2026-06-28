# HO6 Sample 2 — Inbox Triage & Draft

## What you'll build
A reusable Claude **Skill** that reads a pile of incoming support messages and, for each one, decides the category, the priority, whether a human needs to escalate it, and writes a ready-to-send draft reply. Then you'll have Claude **Cowork** run it on new emails automatically, so your morning inbox is pre-sorted with drafts waiting — you just review and send.

## Use it with your Claude.ai subscription
No API key needed. Just your normal Claude.ai login (Pro or Team — these include Skills and Cowork).

**Try it once by hand (2 minutes):**
1. Open **Claude.ai** and start a new chat.
2. Copy **the example prompt** below and paste it into the chat. Press enter.
3. Claude returns each message triaged, with a draft reply. That's the output your Skill will produce.

**Turn it into a reusable Skill:**
1. In Claude.ai, open the **Skills** menu and click **Create Skill** (or **New Skill**).
2. Name it `Inbox Triage & Draft`.
3. Open the `skill.md` file in this folder, copy **everything** in it, paste it into the Skill instructions box, and click **Save**.
4. In any chat, type `/`, pick **Inbox Triage & Draft**, and paste in a batch of messages.

**Make it run automatically (Cowork):**
1. Open `automation-playbook.md` in this folder — it walks you through connecting your support inbox and routing the drafts.
2. Follow it to have new emails triaged the moment they arrive, with Priority-1 items pinged to Slack.

No API key needed at any step. Everything runs inside your Claude.ai subscription.

## The example prompt
Copy this exactly into Claude.ai to see the result right away:

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

## Make it your own
- Replace the three sample messages with real (anonymised) ones from your own queue.
- Add your company's tone and a real signature by editing the draft rules in `skill.md`.
- Change the categories (e.g. add `sales` or `partnerships`) to match how your team routes work.
