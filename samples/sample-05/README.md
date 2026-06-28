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

## Use it with your Claude.ai subscription

No API key needed — this runs entirely on your Claude.ai subscription (Pro or Team, which include Skills and Cowork).

1. **See it work first.** Open **Claude.ai**, start a new chat, and paste **the example prompt** below. Claude returns the full content package.
2. **Save it as a Skill.** Open the **Skills** menu → **Create Skill**, name it `Content Repurposer`, and paste in the full contents of `skill.md`. Save.
3. **Use it any time.** In a chat, type `/`, choose **Content Repurposer**, and paste your own article.
4. **Automate it (optional).** Follow `automation-playbook.md` to have Cowork run it when you publish and write every piece into a Notion content calendar.

## The example prompt

Copy this into Claude.ai to reproduce the worked example in `skill.md`:

```
You are a professional content strategist. Repurpose the article below into: THREE LinkedIn posts (Post 1 Insight angle, Post 2 Story angle, Post 3 Contrarian angle — each 150–250 words with a hook, value, a call to action, and 3–5 hashtags); ONE Twitter/X thread of 5 tweets (tweet 1 a scroll-stopping hook, tweets 2–4 one point each, tweet 5 a call to action — each under 280 characters, formatted [N/5]); and ONE newsletter blurb of exactly 150 words in a warm conversational tone ending with a [LINK] prompt. Keep the author's voice, do not invent facts, and reuse any real numbers from the article.

Article Title: Why Your Team's Productivity Drops After 3 PM (And What to Do About It)
Author: Sarah Chen

The afternoon slump is real. A 2023 University of Michigan study found cognitive performance in knowledge workers drops ~20% between 2 PM and 5 PM, regardless of sleep or caffeine. It's biology: our circadian rhythm dips core body temperature in the early afternoon, reducing alertness — the same mechanism behind the Mediterranean siesta. Yet most offices schedule their hardest meetings in the afternoon, producing longer meetings and worse decisions. Three fixes that work: (1) Do deep work in your 9–11 AM peak and move meetings to 11 AM–1 PM. (2) Take a 10–20 minute nap after lunch — NASA found a 40-minute nap improved pilot alertness by 54%. (3) Replace the 3 PM meeting with async updates via Loom or Slack. Teams that work with their biology outcompete teams that ignore it — not by working harder, but by working at the right times.
```

The full example output is in `skill.md` under **Example Output**.

## Make it your own

- Paste in one of your own recent articles instead of the sample.
- Change the platforms in `skill.md` (e.g. swap Twitter for an Instagram caption, or add a YouTube description).
- Add a line describing your brand voice (e.g. "punchy, no corporate jargon") so every post sounds like you.

## Time Savings Evidence

| Metric | Before | After |
|--------|--------|-------|
| Time to repurpose one article | 3 hr | 5 min (review + minor edit) |
| Articles published per month | 8 | 8 |
| Total time per month | 24 hr | 40 min |
| Hours saved per month | **23.3 hr** | — |
| Hours saved per year | **~280 hr** | — |

See `time-log.csv` for a running log template to track your own savings.
