# HO6 Sample 5 — Content Repurposer

## What you'll build
A reusable Claude **Skill** that takes one long article and spins it into a full social package — 3 LinkedIn posts (each a different angle), a 5-tweet thread, and a 150-word newsletter blurb — all in your voice and ready to post. Then you'll have Claude **Cowork** run it the moment you publish, so every article reaches five times as far without five times the work.

## Use it with your Claude.ai subscription
No API key needed. Just your normal Claude.ai login (Pro or Team — these include Skills and Cowork).

**Try it once by hand (2 minutes):**
1. Open **Claude.ai** and start a new chat.
2. Copy **the example prompt** below and paste it into the chat. Press enter.
3. Claude returns the full content package. That's what your Skill will produce every time.

**Turn it into a reusable Skill:**
1. In Claude.ai, open the **Skills** menu and click **Create Skill** (or **New Skill**).
2. Name it `Content Repurposer`.
3. Open the `skill.md` file in this folder, copy **everything** in it, paste it into the Skill instructions box, and click **Save**.
4. In any chat, type `/`, pick **Content Repurposer**, and paste your article.

**Make it run automatically (Cowork):**
1. Open `automation-playbook.md` in this folder — it connects your CMS (WordPress, Ghost, or Webflow) and writes every piece into a Notion content calendar.
2. Follow it so each new post you publish automatically produces a package ready for review.

No API key needed at any step. Everything runs inside your Claude.ai subscription.

## The example prompt
Copy this exactly into Claude.ai to see the result right away:

```
You are a professional content strategist. Repurpose the article below into: THREE LinkedIn posts (Post 1 Insight angle, Post 2 Story angle, Post 3 Contrarian angle — each 150–250 words with a hook, value, a call to action, and 3–5 hashtags); ONE Twitter/X thread of 5 tweets (tweet 1 a scroll-stopping hook, tweets 2–4 one point each, tweet 5 a call to action — each under 280 characters, formatted [N/5]); and ONE newsletter blurb of exactly 150 words in a warm conversational tone ending with a [LINK] prompt. Keep the author's voice, do not invent facts, and reuse any real numbers from the article.

Article Title: Why Your Team's Productivity Drops After 3 PM (And What to Do About It)
Author: Sarah Chen

The afternoon slump is real. A 2023 University of Michigan study found cognitive performance in knowledge workers drops ~20% between 2 PM and 5 PM, regardless of sleep or caffeine. It's biology: our circadian rhythm dips core body temperature in the early afternoon, reducing alertness — the same mechanism behind the Mediterranean siesta. Yet most offices schedule their hardest meetings in the afternoon, producing longer meetings and worse decisions. Three fixes that work: (1) Do deep work in your 9–11 AM peak and move meetings to 11 AM–1 PM. (2) Take a 10–20 minute nap after lunch — NASA found a 40-minute nap improved pilot alertness by 54%. (3) Replace the 3 PM meeting with async updates via Loom or Slack. Teams that work with their biology outcompete teams that ignore it — not by working harder, but by working at the right times.
```

## Make it your own
- Paste in one of your own recent articles instead of the sample.
- Change the platforms in `skill.md` (e.g. swap Twitter for an Instagram caption, or add a YouTube description).
- Add a line describing your brand voice (e.g. "punchy, no corporate jargon") so every post sounds like you.
