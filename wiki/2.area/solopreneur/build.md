---
title: "BUILD Phase"
aliases:
  - "build phase"
  - "mvp build"
tags:
  - type/area
  - para/area
  - topic/solopreneur
  - topic/build
created: 2026-06-07T22:19:00Z
updated: 2026-06-07T22:19:00Z
type: "area"
id: "202606072219"
---

# BUILD Phase

> Ship the smallest thing that solves the problem. Everything else is procrastination.

## Overview

1-14 days. You're not building a startup. You're building a weekend project that makes money. AI agents do the heavy lifting — you direct.

## Timebox Rules

| Scope                 | Time       | Example                                         |
| --------------------- | ---------- | ----------------------------------------------- |
| Tiny (1 feature)      | 1-3 days   | Single-purpose tool, API wrapper, template pack |
| Small (2-3 features)  | 5-7 days   | Micro-SaaS, Chrome extension, directory site    |
| Medium (full product) | 10-14 days | SaaS with auth, payments, dashboard             |

**If it takes longer than 14 days, scope is too big.** Cut features, not timeline.

## Process

```
Scope MVP ──▶ Setup (1d) ──▶ Core Feature (3-5d) ──▶ Payment (1d) ──▶ Landing Page (1d) ──▶ SHIP
     │              │               │                    │                │
     │         VPS + domain    Main value prop      Stripe/LemonSqsy  Copy + CTA
     │         Auth (if needed)  Working end-to-end  Test purchase     Screenshots
     │              │               │                    │                │
     ▼              ▼               ▼                    ▼                ▼
  Cut until         Skip if         Skip if             Skip if         Skip if
  it fits 14d       not essential   it doesn't          not ready       perfect
                                      deliver value                     design
```

## MVP Rules

### What to Build

- The ONE thing people pay for
- Payment integration (day 1 if possible)
- A working end-to-end flow
- Basic error handling

### What to Skip

- Beautiful design (function > form, always)
- Mobile app (web first, always)
- Social login (email+password is fine)
- Admin dashboard (use the DB directly)
- Analytics (add later if it survives)
- Tests (AI agents can write these, but not day 1)
- Multi-tenant (single user first)
- Email notifications (unless core feature)

## AI Agent Workflow

```
You (director) ──▶ Claude Code ──▶ Code
     │                  │
     │             Build features
     │             Fix bugs
     │             Write tests
     │             Refactor
     │
     └──▶ You review, test manually, decide scope
```

### Typical AI Session

1. Describe what to build in plain English
2. AI scaffolds the project
3. AI builds core feature
4. You test manually in browser
5. AI fixes bugs you find
6. Repeat until it works end-to-end
7. AI adds payment integration
8. You do a test purchase
9. Ship it

## Tech Stack

| Layer     | Choice                   | Why                                                       |
| --------- | ------------------------ | --------------------------------------------------------- |
| Hosting   | Hetzner/DigitalOcean VPS | Cheap ($5/mo), full control                               |
| DNS/CDN   | Cloudflare               | Free, fast, DDoS protection                               |
| Framework | Hono or Next.js          | Hono for API/tools, Next for web apps                     |
| Database  | SQLite (Turso for prod)  | Simple, no server, scales to $10k MRR                     |
| Auth      | Better Auth or Clerk     | Better Auth = self-hosted free, Clerk = easier            |
| Payments  | Stripe or LemonSqueezy   | Stripe = more control, LemonSqueezy = easier tax handling |
| Email     | Resend                   | Simple API, generous free tier                            |

## Pre-Ship Checklist

Before moving to [[ship]]:

- [ ] Core feature works end-to-end
- [ ] Payment processes real money (test with real card)
- [ ] Landing page explains value in < 5 seconds
- [ ] **Email capture on landing page** (newsletter / waitlist) — those launch-day visitors are gone tomorrow
- [ ] **Feedback box on every page** — users who see their feedback shipped become ambassadors
- [ ] Works on mobile (responsive, not native app)
- [ ] Basic error handling (no white screens of death)
- [ ] Domain + SSL configured
- [ ] You can explain it in one sentence

## Fake Door Validation (Before Building)

Pieter Levels' strongest pattern — test demand with zero code:

1. **Landing page + pricing button** before you build anything
2. If people click "buy" → build it
3. If nobody clicks → saved yourself 2 weeks
4. He once built a fake Stripe checkout that said "You didn't actually pay, but now I know you would"

```
Landing page ──▶ "Buy $9/mo" button ──▶ Click? ──YES──▶ BUILD IT
                                           │
                                           NO
                                           │
                                           ▼
                                      Don't build. Next idea.
```

## Subscription vs One-Time

Always prefer subscription. Pieter's math:

| Model               | Year 1 | Year 5     | Year 10   |
| ------------------- | ------ | ---------- | --------- |
| One-time $75        | $75K   | $183K      | $283K     |
| Subscription $75/mo | $75K   | **$1.95M** | **$6.4M** |

Recurring revenue compounds. Every month a user stays = free money. One-time = you start from zero every month.

## References

- [[workflow]] — main solopreneur workflow
- [[idea]] — previous phase (you should have validated already)
- [[ship]] — next phase (time to tell the world)
