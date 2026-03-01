# Project Memory

> Persistent knowledge that carries across AI sessions.
> Add entries after significant decisions, fixes, milestones, and learnings.
> Keep entries factual and specific. Include dates, file paths, and the "why" behind decisions.
> See HOW-MEMORY-WORKS.md for the full guide on what to save and how to organize.

---

## Architecture & Technical Decisions

(Record major technical choices and why you made them. These prevent the AI from re-debating settled decisions.)

### {Decision Title} ({Date})
- **What:** {What was decided}
- **Why:** {The reasoning -- what alternatives were considered, why this one won}
- **Key detail:** {The specific config, setting, or implementation detail to remember}
- **Files:** {Relevant file paths}

<!-- Example:
### Database Choice (Jan 15, 2026)
- **What:** Chose Supabase (PostgreSQL) over MongoDB
- **Why:** Need relational queries for reporting, row-level security for multi-tenant, and real-time subscriptions. MongoDB would require more application-level joins.
- **Key detail:** Using Supabase JS client v2 with autoRefreshToken enabled. Connection pooling via Supavisor.
- **Files:** `src/lib/supabase.ts`, `supabase/migrations/`
-->

---

## Problems Solved

(Document bugs, errors, and tricky issues along with their solutions. The AI will reference these when similar problems occur.)

### {Problem Title} ({Date})
- **Symptom:** {What went wrong -- error message, unexpected behavior}
- **Root cause:** {Why it happened}
- **Fix:** {What you did to resolve it}
- **Key detail:** {The specific thing to remember so this never happens again}
- **Files:** {Relevant file paths}

<!-- Example:
### CORS Error on Mobile (Feb 3, 2026)
- **Symptom:** API calls from mobile browser returned `Access-Control-Allow-Origin` error
- **Root cause:** FastAPI CORS middleware had `allow_credentials=False` and fetch calls were missing `credentials: 'include'`
- **Fix:** Set `allow_credentials=True` in CORSMiddleware config AND added `credentials: 'include'` to all fetch calls
- **Key detail:** When using cookies for auth, BOTH the server and client must explicitly opt in to credentials
- **Files:** `backend/main.py` (CORS config), `frontend/src/lib/api.ts` (fetch wrapper)
-->

---

## Deployments & Infrastructure

(Record deployment configurations, environment details, and infrastructure changes.)

### {Deployment Event} ({Date})
- **What:** {What was deployed or changed}
- **Environment:** {Production / Staging / Development}
- **Key detail:** {Config values, URLs, or settings to remember}
- **Files:** {Relevant file paths}

<!-- Example:
### Initial Railway Deployment (Jan 20, 2026)
- **What:** Deployed FastAPI backend to Railway
- **Environment:** Production
- **Key detail:** Railway assigns PORT dynamically via env var. Never hardcode ports. Health check at /health required for zero-downtime deploys. Custom domain: api.novabuild.ai
- **Files:** `Dockerfile`, `railway.toml`, `.github/workflows/deploy.yml`
-->

---

## Client & User Interactions

(Record feedback, feature requests, pain points, and outcomes from real users.)

### {Client/User Name} -- {Topic} ({Date})
- **What:** {Summary of the interaction}
- **Feedback:** {What they said, specific quotes if important}
- **Action:** {What you decided to do about it}
- **Status:** {Done / In progress / Backlogged}

<!-- Example:
### Tom (BuildCorp) -- Dashboard Performance (Feb 22, 2026)
- **What:** Pilot user reported dashboard takes >3 seconds to load
- **Feedback:** "I open this every morning and wait. My old spreadsheet was faster."
- **Action:** Implement pagination (10 projects per page) and lazy-load project details
- **Status:** Fixed Mar 1 -- load time now under 800ms
-->

---

## Conventions & Patterns

(Record team agreements, coding conventions, and established patterns.)

### {Convention} ({Date Established})
- {Description of the rule or pattern}

<!-- Example:
### Git Workflow (Jan 10, 2026)
- Feature branches: `feat/short-description`
- Bug fixes: `fix/short-description`
- Squash merge to main (no merge commits)
- PR descriptions must include "Why" section
- All PRs need at least 1 review

### API Response Format (Jan 12, 2026)
- All endpoints return: `{ success: boolean, data: T | null, error: string | null }`
- HTTP status codes: 200 (success), 400 (client error), 401 (unauthorized), 500 (server error)
- Never return raw error messages to clients -- log the full error server-side, return a user-friendly message
-->

---

## Milestones & Key Events

(Record significant achievements, launches, and turning points.)

### {Milestone} ({Date})
- **What:** {What happened}
- **Impact:** {Why it matters}
- **Lesson:** {What you learned, if anything}

<!-- Example:
### First Paying Customer (Mar 5, 2026)
- **What:** GreenBuild signed Pro plan ($799/mo)
- **Impact:** First revenue. Validates the product and pricing.
- **Lesson:** Lead with time-saving ("2 hours to 10 seconds"), not technology ("AI-powered"). Customers buy outcomes, not features.
-->

---

## Tools & Integrations

(Record tool configurations, API quirks, and integration details.)

### {Tool Name} ({Date Added/Updated})
- **Purpose:** {What you use it for}
- **Key detail:** {Config, quirks, or gotchas to remember}

<!-- Example:
### Instantly.ai (Feb 1, 2026)
- **Purpose:** Cold email campaigns to construction PMs
- **Key detail:** Daily send limit is 50/account. Using 3 warmed accounts for 150/day total. Warmup takes 14 days before sending real campaigns. Reply tracking only works if IMAP is connected (not just SMTP).
-->

---

## Archive (No Longer Active)

(Move old entries here when they stop being relevant. Don't delete -- you might need them later.)

<!-- Example:
### Slack Bot Experiment (Killed Jan 2026)
- Built a Slack bot for customer support triage
- Killed after 2 weeks: customers preferred email, Slack had <10% adoption
- Lesson: Validate the channel before building the feature
-->

---

<!--
MAINTENANCE NOTES:
- Add new entries at the TOP of each section (most recent first)
- Move entries to Archive when no longer relevant
- Split into multiple files if this exceeds 500 lines (see HOW-MEMORY-WORKS.md)
- Review quarterly: remove duplicates, update outdated entries
-->
