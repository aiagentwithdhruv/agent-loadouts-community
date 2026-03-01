# Your Context -- AI Identity & Working Memory

> This file tells the AI who you are, what you're working on, and how you think.
> Fill in every section. Delete the instructions in parentheses when done.
> Keep this file under 300 lines. Link to separate files for deep dives.

---

## Identity

(Who are you? This is the foundation the AI uses for every interaction.)

| Field | Detail |
|-------|--------|
| **Name** | {Your Name} |
| **Role** | {Your Role -- e.g., Founder, Developer, Freelancer, Manager} |
| **Company** | {Company or Project Name} |
| **Industry** | {Industry -- e.g., SaaS, E-commerce, Agency, Education} |
| **Website** | {URL} |
| **Location** | {City, Country} |
| **Timezone** | {e.g., UTC-5, IST, CET} |

### Bio (2-3 sentences)
{What you do, what you're known for, what drives you. The AI uses this to match your tone and goals.}

---

## Current Priorities

(What matters RIGHT NOW. Ordered by importance. Update this weekly or when priorities shift.)

| Priority | Status | Deadline | Notes |
|----------|--------|----------|-------|
| 1. {Most important thing} | {Active / Blocked / Done} | {Date or "Ongoing"} | {Brief context} |
| 2. {Second priority} | {Status} | {Date} | {Notes} |
| 3. {Third priority} | {Status} | {Date} | {Notes} |
| 4. {Fourth priority} | {Status} | {Date} | {Notes} |
| 5. {Fifth priority} | {Status} | {Date} | {Notes} |

### This Week's Focus
{One sentence: what is the single most important outcome this week?}

---

## Key Projects

(List every active project. Include enough detail that the AI can jump into any of them.)

### {Project 1 Name} ({Status: Active / Paused / Maintenance})

| Field | Detail |
|-------|--------|
| **What** | {One-line description} |
| **Path** | {Local path or repo URL} |
| **Stack** | {Key technologies} |
| **Revenue** | {Revenue impact or "Internal"} |
| **Next step** | {What needs to happen next} |

### {Project 2 Name} ({Status})

| Field | Detail |
|-------|--------|
| **What** | {Description} |
| **Path** | {Path or URL} |
| **Stack** | {Technologies} |
| **Revenue** | {Impact} |
| **Next step** | {What's next} |

### {Project 3 Name} ({Status})

| Field | Detail |
|-------|--------|
| **What** | {Description} |
| **Path** | {Path or URL} |
| **Stack** | {Technologies} |
| **Revenue** | {Impact} |
| **Next step** | {What's next} |

(Add more projects as needed. Remove completed ones -- move them to memory.)

---

## Tech Stack

(What technologies you use. This prevents the AI from suggesting tools you don't use.)

### Primary Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| **Language** | {Python / TypeScript / Go / etc.} | {Version if it matters} |
| **Frontend** | {React / Next.js / Vue / etc.} | {Hosting: Vercel, Netlify, etc.} |
| **Backend** | {FastAPI / Express / Django / etc.} | {Hosting: Railway, AWS, etc.} |
| **Database** | {PostgreSQL / MongoDB / Supabase / etc.} | {Provider} |
| **AI/LLM** | {OpenAI / Claude / Gemini / local} | {Models used} |
| **Automation** | {n8n / Make / Zapier / custom} | {Where it runs} |
| **Deployment** | {Docker / Vercel / AWS / etc.} | {CI/CD setup} |
| **Version Control** | {GitHub / GitLab / etc.} | {Branching strategy} |

### Tools and Services

| Tool | Purpose | Account |
|------|---------|---------|
| {Tool 1} | {What you use it for} | {Account name or "personal"} |
| {Tool 2} | {Purpose} | {Account} |
| {Tool 3} | {Purpose} | {Account} |

### Conventions

(Rules the AI must follow when writing code or content for you.)

- {Convention 1 -- e.g., "Use TypeScript strict mode, no `any` types"}
- {Convention 2 -- e.g., "API responses always return {success, data, error}"}
- {Convention 3 -- e.g., "All functions must have JSDoc comments"}
- {Convention 4 -- e.g., "Use snake_case for Python, camelCase for TypeScript"}
- {Convention 5 -- e.g., "No class components, only functional with hooks"}

---

## Communication Preferences

(How you want the AI to talk to you. Be specific.)

### Tone
- {e.g., "Direct and concise. No filler words. No emojis unless I use them first."}
- {e.g., "Technical when discussing code, simple when explaining to clients."}
- {e.g., "Challenge my ideas if they're wrong. Don't just agree."}

### Response Format
- {e.g., "Use bullet points over paragraphs for technical answers."}
- {e.g., "Show code first, explain after."}
- {e.g., "Include file paths when referencing code."}
- {e.g., "Keep responses under 500 words unless I ask for detail."}

### Things to Avoid
- {e.g., "Don't apologize unnecessarily."}
- {e.g., "Don't ask if I want help -- just help."}
- {e.g., "Don't suggest tools I don't use (see Tech Stack above)."}
- {e.g., "Don't add unnecessary abstractions or over-engineer."}

---

## Decision-Making Framework

(How you make decisions. This helps the AI align with your thinking.)

### Priorities (Ordered)
1. {e.g., "Revenue first -- does this make money or save money?"}
2. {e.g., "Speed over perfection -- ship fast, iterate later."}
3. {e.g., "Simplicity -- the simplest solution that works is the best solution."}
4. {e.g., "Reuse -- never build what already exists."}
5. {e.g., "Documentation -- if it's not documented, it doesn't exist."}

### When Making Technical Decisions
- {e.g., "Prefer proven, boring technology over cutting-edge."}
- {e.g., "Build for 10x current scale, not 1000x."}
- {e.g., "Optimize for developer speed, not server speed (until it matters)."}

### When Making Business Decisions
- {e.g., "Revenue-generating work before feature work."}
- {e.g., "Client work before internal projects."}
- {e.g., "Distribution (marketing/sales) before building new products."}

---

## Key Contacts

(People the AI should know about. Keep it to the important ones.)

| Name | Role | Context |
|------|------|---------|
| {Name 1} | {Role -- e.g., Co-founder, Client, Manager} | {What the AI needs to know about them} |
| {Name 2} | {Role} | {Context} |
| {Name 3} | {Role} | {Context} |

(Do NOT include private contact details like phone numbers or emails here unless this is a private repo.)

---

## Revenue & Business Goals

(Financial context so the AI can prioritize revenue-impacting work.)

### Current Revenue
| Source | Amount | Status |
|--------|--------|--------|
| {Source 1 -- e.g., Freelancing} | {Monthly amount} | {Growing / Stable / Declining} |
| {Source 2 -- e.g., SaaS product} | {Monthly amount} | {Status} |
| {Source 3 -- e.g., Consulting} | {Monthly amount} | {Status} |

### Revenue Targets
| Timeframe | Target | Strategy |
|-----------|--------|----------|
| This month | {Amount} | {How} |
| This quarter | {Amount} | {How} |
| This year | {Amount} | {How} |

### Active Pipeline
| Lead / Opportunity | Value | Stage | Next Step |
|-------------------|-------|-------|-----------|
| {Lead 1} | {Amount} | {Discovery / Proposal / Negotiation / Closed} | {What to do next} |
| {Lead 2} | {Value} | {Stage} | {Next step} |

---

## Self-Update Rules

(When and how this context file should be updated.)

### Auto-Update Triggers

| Event | Action | Section to Update |
|-------|--------|-------------------|
| New project started | Add to Key Projects | Key Projects |
| Project completed | Move to memory, remove from here | Key Projects |
| Priority changed | Reorder priorities | Current Priorities |
| New tool adopted | Add to tech stack | Tech Stack |
| Revenue milestone hit | Update numbers | Revenue & Business Goals |
| New team member or contact | Add to contacts | Key Contacts |
| Convention changed | Update rules | Conventions |

### Verification Schedule

| Section | Review Every | Last Verified |
|---------|-------------|---------------|
| Current Priorities | Weekly | {YYYY-MM-DD} |
| Key Projects | Bi-weekly | {YYYY-MM-DD} |
| Revenue & Goals | Monthly | {YYYY-MM-DD} |
| Tech Stack | Quarterly | {YYYY-MM-DD} |
| Key Contacts | Quarterly | {YYYY-MM-DD} |

### Staleness Warning

When reading a section where `Last Verified` is older than the review cadence, flag it:
"This section may be stale (last verified: {date}). Verify before relying on it."

---

*Template from the [Agent Loadout System](https://github.com/aiagentwithdhruv/agent-loadouts-community). Fill in, delete instructions, and make it yours.*
