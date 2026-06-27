# Sample 05 — Content Repurposer Skill

## Problem Statement

Content teams write long-form articles and blog posts that reach one audience on one channel. Repurposing each article into LinkedIn posts, a Twitter thread, and a newsletter blurb takes a skilled writer 2–4 hours per piece — and it usually does not happen because of time pressure. Claude can repurpose any article into a full social media package in under 2 minutes, dramatically increasing the reach of every piece of content created.

## What the Skill Does

The **Content Repurposer Skill** takes one long-form article (pasted in full or as a summary) and produces a complete social media package:

- **3 LinkedIn posts** — each from a different angle (insight, story, and contrarian/challenge), each 150–250 words with a call to action
- **1 Twitter/X thread** — 5 tweets, starting with a hook tweet and ending with a call to action, each under 280 characters
- **1 Newsletter blurb** — exactly 150 words, in a warm conversational tone, with a clear link prompt

Each piece is ready to copy-paste and publish with at most minor edits.

## What the Automation Does

The `automation-playbook.md` describes how to connect this Skill to a content publishing workflow in Claude Cowork:

- When a new article is published to your CMS (WordPress, Webflow, or Ghost), a webhook triggers the automation
- The article body is passed to this Skill
- All five outputs are written to a Notion content calendar database, one row per output
- A Slack notification tells the social media manager the package is ready to review
- Optionally, posts are scheduled directly in Buffer or Hootsuite

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time to repurpose one article | 3 hr | 5 min (review + minor edit) |
| Articles published per month | 8 | 8 |
| Total time per month | 24 hr | 40 min |
| Hours saved per month | **23.3 hr** | — |
| Hours saved per year | **~280 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
