# NovaBuild AI -- Context

> Fictional example of a filled-out CONTEXT-TEMPLATE.md.
> NovaBuild is a 4-person AI automation startup. Use this as a reference when filling in your own.

---

## Identity

| Field | Detail |
|-------|--------|
| **Name** | Sarah Chen |
| **Role** | Founder & Lead Developer |
| **Company** | NovaBuild AI |
| **Industry** | B2B SaaS -- AI-powered project management |
| **Website** | https://novabuild.ai |
| **Location** | Austin, TX |
| **Timezone** | UTC-6 (CST) |

### Bio
I build AI tools that help construction companies manage projects without spreadsheet chaos. Former civil engineer who taught herself to code. I care about shipping fast, keeping things simple, and making money before making things perfect.

---

## Current Priorities

| Priority | Status | Deadline | Notes |
|----------|--------|----------|-------|
| 1. Close 3 pilot customers | Active | Mar 15 | Have 7 warm leads from LinkedIn outreach |
| 2. Ship invoice automation feature | Active | Mar 10 | Customers keep asking for this |
| 3. Fix onboarding flow drop-off | Active | Mar 8 | 60% drop-off at step 3 (project setup) |
| 4. Prepare for Y Combinator S26 app | Blocked | Apr 1 | Need traction numbers first |
| 5. Hire part-time frontend dev | Not started | Apr 15 | Budget: $3K/mo |

### This Week's Focus
Close at least 1 paid pilot customer -- everything else is secondary.

---

## Key Projects

### NovaBuild Platform (Active)

| Field | Detail |
|-------|--------|
| **What** | AI project management platform for construction companies |
| **Path** | `novabuild-platform/` / github.com/novabuild/platform |
| **Stack** | Next.js 14 + FastAPI + Supabase + OpenAI GPT-4o |
| **Revenue** | $0 MRR (pre-revenue, 3 free pilots running) |
| **Next step** | Ship invoice automation, convert pilots to paid |

### NovaBuild Marketing Site (Active)

| Field | Detail |
|-------|--------|
| **What** | Landing page + blog + demo booking |
| **Path** | `novabuild-marketing/` / novabuild.ai |
| **Stack** | Next.js + Tailwind + Vercel + Cal.com for booking |
| **Revenue** | Drives all inbound leads (~12/week) |
| **Next step** | Add case study from BuildCorp pilot |

### Lead Gen Pipeline (Active)

| Field | Detail |
|-------|--------|
| **What** | LinkedIn outreach + cold email to construction PMs |
| **Path** | `lead-gen/` |
| **Stack** | Apollo.io + Instantly.ai + Google Sheets |
| **Revenue** | 7 warm leads, 3 demos booked |
| **Next step** | Follow up with GreenBuild and UrbanEdge |

### Internal AI Agent (Maintenance)

| Field | Detail |
|-------|--------|
| **What** | Claude Code agent with loadouts for all company workflows |
| **Path** | `agent-setup/` |
| **Stack** | Claude Code + Agent Loadouts + 8 skills |
| **Revenue** | Internal -- saves ~10 hrs/week |
| **Next step** | Add skill for customer support replies |

---

## Tech Stack

### Primary Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| **Language** | TypeScript (frontend), Python 3.11 (backend) | Strict mode TS |
| **Frontend** | Next.js 14 (App Router) | Deployed on Vercel |
| **Backend** | FastAPI | Deployed on Railway |
| **Database** | Supabase (PostgreSQL + Auth + Storage) | Row-level security on |
| **AI/LLM** | OpenAI GPT-4o, GPT-4o-mini | Via official SDK |
| **Automation** | n8n (self-hosted on Railway) | 6 active workflows |
| **Deployment** | Vercel (frontend), Railway (backend + n8n) | GitHub Actions CI/CD |
| **Version Control** | GitHub | Main + feature branches, squash merge |

### Tools and Services

| Tool | Purpose | Account |
|------|---------|---------|
| Linear | Issue tracking | team@novabuild.ai |
| Slack | Team communication | novabuild.slack.com |
| Apollo.io | Lead sourcing | sarah@novabuild.ai |
| Instantly.ai | Cold email campaigns | sarah@novabuild.ai |
| Cal.com | Demo scheduling | sarah@novabuild.ai |
| Stripe | Payments (not live yet) | sarah@novabuild.ai |
| PostHog | Product analytics | self-hosted |

### Conventions

- TypeScript strict mode, no `any` types. If you're tempted to use `any`, define an interface.
- All API responses follow: `{ success: boolean, data: T | null, error: string | null }`
- Python functions use type hints. No bare `dict` returns -- use Pydantic models.
- Database queries go through the Supabase client, not raw SQL.
- Every PR needs a one-line description of why (not just what).
- No component libraries. We use Tailwind utility classes directly.

---

## Communication Preferences

### Tone
- Direct and concise. Get to the point.
- Technical when discussing code. Simple when I'm drafting client emails.
- Challenge my ideas if they don't make sense. I prefer being corrected now over being wrong later.

### Response Format
- Code first, explanation after.
- Use bullet points, not paragraphs, for technical answers.
- Always include file paths when referencing code.
- If a task has more than 3 steps, use a numbered list.

### Things to Avoid
- Don't suggest MongoDB. We use Supabase. Always.
- Don't suggest Redux or Zustand. We use React Server Components and URL state.
- Don't add "nice to have" features I didn't ask for.
- Don't over-abstract. One function that does the thing is better than three layers of abstraction.
- Don't apologize. Just fix it.

---

## Decision-Making Framework

### Priorities (Ordered)
1. Revenue first -- does this help close a customer or keep one?
2. Speed over perfection -- ship today, polish next week.
3. Simplicity -- if a junior dev can't understand it, it's too complex.
4. Reuse -- check if a skill, template, or past solution exists before building.
5. Measure -- if we can't tell whether it worked, don't build it.

### When Making Technical Decisions
- Prefer boring, proven technology. Next.js, FastAPI, PostgreSQL. Not the framework that launched last week.
- Build for 10x current scale. We have 3 users. Build for 30, not 30,000.
- Optimize for developer speed. We're 4 people. Our time is the bottleneck, not the server.

### When Making Business Decisions
- Talking to customers beats building features. Always.
- One paying customer is worth more than 100 free users.
- Distribution (outreach, content, demos) before product work, unless customers are blocked.

---

## Key Contacts

| Name | Role | Context |
|------|------|---------|
| Marcus Rivera | Co-founder, Sales | Handles all demos and customer calls. Knows construction industry deeply. |
| Priya Patel | Backend Developer | Part-time (20 hrs/week). Owns FastAPI backend and database schema. |
| Jake Kim | Frontend Developer | Part-time (20 hrs/week). Owns Next.js frontend and UI components. |
| Tom Bradley | Pilot Customer (BuildCorp) | Construction PM, 15-person team. Most active pilot user. Good for case study. |
| Lisa Nguyen | Warm Lead (GreenBuild) | VP Operations, 80-person firm. Demo booked for March 5. Could be first paid customer. |
| David Rho | Advisor | Former CTO of PlanGrid (acquired by Autodesk). Monthly calls. Intro'd us to 3 leads. |

---

## Revenue & Business Goals

### Current Revenue
| Source | Amount | Status |
|--------|--------|--------|
| Platform subscriptions | $0/mo | Pre-revenue (3 free pilots) |
| Consulting/setup fees | $2,400/mo | 2 construction firms paying for setup help |
| Freelance (Sarah) | $1,500/mo | Winding down to focus on NovaBuild |

### Revenue Targets
| Timeframe | Target | Strategy |
|-----------|--------|----------|
| This month (Mar) | $3,000 MRR | Convert 3 pilots to $499/mo + close 1 new at $799 |
| This quarter (Q2) | $8,000 MRR | 12 paying customers, mix of Standard ($499) and Pro ($799) |
| This year | $50,000 MRR | 80 customers, launch Enterprise tier at $1,999 |

### Active Pipeline
| Lead / Opportunity | Value | Stage | Next Step |
|-------------------|-------|-------|-----------|
| GreenBuild (Lisa Nguyen) | $799/mo | Demo booked Mar 5 | Marcus running demo, Sarah on standby for technical Q's |
| UrbanEdge Construction | $499/mo | Discovery call done | Send proposal by Mar 3 |
| Apex Builders | $499/mo | Cold outreach replied | Schedule intro call this week |
| BuildCorp (Tom Bradley) | $499/mo | Pilot user, converting | Send pricing email after invoice feature ships |
| Metro Civil Partners | $1,999/mo | Referral from David | Intro email sent, waiting for reply |
| Cornerstone Dev Group | $799/mo | LinkedIn DM conversation | Share case study once BuildCorp one is ready |
| Summit Contractors | $499/mo | Discovery call scheduled | Marcus handling, Mar 7 |

---

## Self-Update Rules

### Auto-Update Triggers

| Event | Action | Section to Update |
|-------|--------|-------------------|
| New project started | Add to Key Projects | Key Projects |
| Project completed or killed | Move to memory, remove from here | Key Projects |
| Priority changed | Reorder the list | Current Priorities |
| New tool adopted | Add to stack and services | Tech Stack |
| Revenue milestone | Update numbers | Revenue & Business Goals |
| Lead status changed | Update pipeline | Active Pipeline |
| Team member joined or left | Update contacts | Key Contacts |
| Convention changed | Update rules | Conventions |

### Verification Schedule

| Section | Review Every | Last Verified |
|---------|-------------|---------------|
| Current Priorities | Weekly | 2026-03-01 |
| Key Projects | Bi-weekly | 2026-03-01 |
| Revenue & Goals | Monthly | 2026-03-01 |
| Active Pipeline | Weekly | 2026-03-01 |
| Tech Stack | Quarterly | 2026-03-01 |
| Key Contacts | Quarterly | 2026-03-01 |

### Staleness Warning
When reading a section where `Last Verified` is older than the review cadence, flag it:
"This section may be stale (last verified: {date}). Verify before relying on it."

---

*This is a fictional example for NovaBuild AI. Copy CONTEXT-TEMPLATE.md and fill in your own details.*
