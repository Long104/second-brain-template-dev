---
title: "Solopreneur Workflow"
aliases:
  - "solopreneur workflow"
  - "indie hacker workflow"
tags:
  - type/area
  - para/area
  - topic/solopreneur
  - topic/workflow
created: 2026-06-07T22:19:00Z
updated: 2026-06-07T22:50:00Z
type: "area"
id: "202606072219"
---

# Solopreneur Workflow

> Ship fast, distribute harder. One person + AI agents = a studio.

## Overview

This is the operating system for building and selling internet products as a solopreneur. One person, AI agents, minimal overhead. Inspired by Pieter Levels — distribution > building.

## The Loop

```
┌─────────┐     ┌─────────┐     ┌─────────┐     ┌──────────────┐
│  IDEA   │────▶│  BUILD  │────▶│  SHIP   │────▶│ ITERATE/KILL │
│ 48h max │     │ 1-14d   │     │ Ongoing │     │ 60/90d check │
└─────────┘     └─────────┘     └─────────┘     └──────┬───────┘
     ▲                                                   │
     │              data says keep going                  │
     ◀───────────────────────────────────────────────────┘
                     │
                     │ data says stop
                     ▼
              ┌─────────────┐
              │   SELL/KILL │
              │  exit clean │
              └─────────────┘
```

## How to Use This (AI Skill Triggers)

> Just say the trigger phrase. The solopreneur skill handles the rest.

| Phase | Say This                         | What Happens                                        | Creates/Updates          |
| ----- | -------------------------------- | --------------------------------------------------- | ------------------------ |
| IDEA  | `"validate [idea]"`              | Research market + competition → GO/NO-GO            | `research.md`            |
| IDEA  | `"what should I build"`          | Scan trends + rank ideas by opportunity             | Prints to chat, you pick |
| IDEA  | `"what's trending"`              | What's selling on Trustmrr/Flippa/IH/X              | Prints to chat           |
| BUILD | `"init [product]"`               | Create project folder + all template files          | `wiki/1.project/[name]/` |
| SHIP  | `"ship [product]"`               | Research real examples → draft human-sounding posts | `marketing.md`           |
| SHIP  | `"market [product]"`             | Ongoing content calendar + SEO strategy             | Updates `marketing.md`   |
| KILL  | `"kill check [product]"`         | Pull data → ITERATE / SELL / KILL verdict           | `revenue.md`             |
| SELL  | `"how much is [X] worth"`        | Valuation based on MRR + comparable sales           | Updates `revenue.md`     |
| BUILD | `"add feature [X] to [product]"` | Log feature request, auto-prioritize                | `todo-feature.md`        |
| BUILD | `"done feature [X]"`             | Mark complete, update project state                 | `todo-feature.md`        |

### Quick Start

```
You: "what should I build"
AI: [scans trends, suggests 3-5 ideas]

You: "validate a Chrome extension for X"
AI: [researches, gives GO/NO-GO]

You: "init my-extension"
AI: [creates wiki/1.project/my-extension/ with all files]

You: [build it in 1-14 days]

You: "ship my-extension"
AI: [drafts X thread, PH listing, Reddit post — human voice, not AI slop]

You: [60 days later]
You: "kill check my-extension"
AI: [verdict: ITERATE / SELL / KILL]
```

## Step-by-Step Guide (Beginner)

> If you're new to this, follow these steps in order. Each step tells you exactly what to say and what happens.

### Step 1: Find an Idea

You need a product idea. You can either:

- **Get suggestions:** Say `"what should I build"` → AI scans trends and suggests 3-5 ideas ranked by opportunity
- **Check what's hot:** Say `"what's trending"` → AI shows what's selling on Trustmrr/Flippa/IH right now
- **Use your own idea:** Skip to Step 2 with any idea you have

### Step 2: Validate the Idea (48 hours max)

Before writing any code, check if people will actually pay for this.

```
You: "validate a Chrome extension that blocks AI-generated content"
```

AI will:

1. Research who has this problem and where they hang out
2. Find competitors and what they charge
3. Check if you can reach 100 potential users in a week
4. Give you a **GO** or **NO-GO** verdict with reasons

**If NO-GO** → kill it, go back to Step 1. You saved 2 weeks.
**If GO** → move to Step 3.

Read the full checklist: [[idea]]

### Step 3: Create the Project

```
You: "init ai-blocker"
```

AI creates `wiki/1.project/ai-blocker/` with 5 files:

| File              | What It's For                                          |
| ----------------- | ------------------------------------------------------ |
| `plan-project.md` | What is this, why it exists, current state, tech stack |
| `research.md`     | Market research from Step 2 (already filled)           |
| `marketing.md`    | Launch posts — filled when you ship                    |
| `revenue.md`      | MRR tracking — filled over time                        |
| `todo-feature.md` | Feature backlog — filled as users request things       |

### Step 4: Build the MVP (1-14 days)

Build the **smallest version** that solves the problem. Rules:

- Only build the ONE thing people pay for
- Add payment from day 1 (Stripe or LemonSqueezy)
- Skip beautiful design — function over form
- Add email capture (newsletter/waitlist) — those launch visitors leave tomorrow
- Add a feedback box — users who see their feedback shipped become promoters
- If you can't finish in 14 days → scope is too big, cut features

**Pro tip: Fake door validation.** Before building a feature, put a "Buy" button on the landing page for it. If people click → build it. If nobody clicks → don't waste time. Pieter Levels once built a fake Stripe checkout just to test if people would pay.

Read the full build guide: [[build]]

**Track features as you go:**

```
You: "add feature 'dark mode' to ai-blocker"
AI: [logs it in todo-feature.md with auto-priority]

You: "done feature 'dark mode'"
AI: [marks complete, updates project state]
```

### Step 5: Ship It (Launch Day)

```
You: "ship ai-blocker"
```

AI will:

1. Research **real** X posts, PH launches, and Reddit posts from similar products
2. Study what tone and structure works (no ChatGPT-slop)
3. Write in YOUR voice:
   - **X thread** (5-8 tweets with hook, context, proof, CTA)
   - **Product Hunt** listing (title, tagline, description, first comment)
   - **Reddit** post for r/SideProject (story-driven, not salesy)
   - **Indie Hackers** story (honest numbers, failures included)
   - **10 DM messages** to send directly to people you know
4. Save everything to `marketing.md`

**Launch ALL channels on the same day.** PH + Reddit + X + HN all at once. One big spike beats 5 small launches.

Read the full distribution guide: [[ship]]

### Step 6: Build in Public (Ongoing)

After launch day, keep posting. This is where most people fail — they launch once and disappear.

| When             | What to Post                                               |
| ---------------- | ---------------------------------------------------------- |
| Every 2-3 days   | Build update on X: "Just shipped [feature]. [Screenshot]"  |
| Weekly           | Revenue screenshot: "Week X: $[amount] MRR"                |
| Monthly          | Honest story on Indie Hackers with real numbers            |
| Every 2-3 months | **Re-launch** — ship a feature, post on PH/HN/Reddit again |

Re-launching is critical. Pieter Levels re-launches Nomad List every year on PH. Each time = new wave of users.

### Step 7: Measure and Decide (60/90-day check)

```
Day 30: Soft check — any paying users? Any signups?
         YES → keep going, push harder on distribution
         NO → keep going, but try new channels

Day 60: Real check — $100+ MRR?
         YES → full send, scale up
         NO → last push: price cut, new channel, re-launch

Day 90: Hard kill — still no traction?
         SELL on Trustmrr/Flippa (if any revenue)
         or KILL it and move to next idea
```

```
You: "kill check ai-blocker"
AI: [reviews your data, gives ITERATE / SELL / KILL verdict]
```

Read the full decision guide: [[iterate-kill]]

### Step 8: Exit (Kill, Sell, or Keep)

| Outcome  | What to Do                                                                                                         |
| -------- | ------------------------------------------------------------------------------------------------------------------ |
| **Keep** | Keep building what users request. Re-launch every 2-3 months. Grow MRR.                                            |
| **Sell** | List on Trustmrr or Flippa. Say `"how much is ai-blocker worth"` to get a valuation. Typical: 2-4x annual revenue. |
| **Kill** | Write a post-mortem. Share the failure on X (builds credibility). Move project folder to archive. Go to Step 1.    |

Pieter Levels killed 70+ projects. Only 4 made real money ($200K+/month). That's normal. Kill fast, try again.

```
You: "how much is ai-blocker worth"
AI: [researches comparable sales, estimates: $X at Yx multiple]
```

---

### Full Flow at a Glance

```
"What should I build?"     → Get ideas
"Validate [idea]"          → GO or NO-GO (48h)
"Init [product]"           → Project folder created
Build it yourself           → 1-14 days
"Ship [product]"            → Launch posts generated
Post everywhere same day    → Big traffic spike
Build in public             → X posts every 2-3 days
"Kill check [product]"     → ITERATE / SELL / KILL (60/90d)
"How much is [X] worth?"   → Get valuation if selling
Repeat.                     → ~5% of products succeed. Keep swinging.
```

---

## Phase Files

| Phase        | File             | Timebox             | Key Question                           |
| ------------ | ---------------- | ------------------- | -------------------------------------- |
| IDEA         | [[idea]]         | 48h max             | "Will someone pay for this?"           |
| BUILD        | [[build]]        | 1-14 days           | "What's the smallest useful version?"  |
| SHIP         | [[ship]]         | Ongoing             | "Who needs to know this exists?"       |
| ITERATE/KILL | [[iterate-kill]] | 60d soft / 90d hard | "Is the data good enough to continue?" |

## Rules

1. **Idea to shipped in 14 days max** — if you can't ship it, scope is too big
2. **Distribution > Product** — a mediocre product with great distribution beats a great product with no distribution
3. **Revenue is the only metric** — likes, stars, upvotes don't pay bills
4. **Kill at 90 days** — 60-day soft check (review data), 90-day hard kill if no revenue traction
5. **One at a time** — no parallel projects until the current one ships
6. **AI does the work** — you direct, AI agents code/write/design
7. **Sell when plateaued** — list on Trustmrr/Flippa when MRR flatlines
8. **Subscription > one-time** — recurring revenue compounds. $75/mo sub = $2M in 5 years vs $183K one-time
9. **Fake door first** — put a payment button on the landing page BEFORE building. If people click → build. If not → saved yourself 2 weeks
10. **Launch everywhere same day** — PH + HN + Reddit + X all on one day. One big spike beats 5 small launches
11. **Capture emails from day 1** — newsletter, waitlist, alerts. Those 10K launch-day visitors are gone tomorrow. Keep them
12. **Re-launch every 2-3 months** — new feature = new PH post, new X thread. Don't launch once and disappear

## Tech Stack (Minimal)

```
VPS (Hetzner/DigitalOcean)
  ├── Cloudflare (DNS + CDN)
  ├── Hono / Next.js (app)
  ├── SQLite / Turso (DB)
  └── Stripe / LemonSqueezy (payments)
```

## Exit Paths

| Signal                    | Action                                  |
| ------------------------- | --------------------------------------- |
| MRR growing, you enjoy it | Keep, iterate                           |
| MRR growing, you hate it  | Sell on Trustmrr/Flippa (2-4x multiple) |
| MRR flat 60+ days         | Cut price, last push, re-launch         |
| MRR flat 90+ days         | Sell or kill. Move on                   |
| MRR $0 after 90 days      | Kill. Archive. Next idea                |

## References

- [[me]] — who you are as a solopreneur
- [[idea]] — idea validation phase
- [[build]] — build phase
- [[ship]] — shipping & distribution phase
- [[iterate-kill]] — iterate or kill decision phase
