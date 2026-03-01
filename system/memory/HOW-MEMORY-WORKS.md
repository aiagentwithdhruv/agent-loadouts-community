# How Memory Works

> The memory system gives AI persistent recall across sessions.
> Without memory, every conversation starts from zero.
> With memory, the AI remembers what happened yesterday, last week, and last month.

---

## Memory vs Context -- What's the Difference?

| | Context | Memory |
|---|---------|--------|
| **What it is** | Who you are and what you're working on NOW | What HAPPENED in past sessions |
| **Changes how often** | Weekly (priorities) to quarterly (stack) | Every session (new entries added) |
| **Format** | Structured template with fixed sections | Chronological log of events and decisions |
| **Size** | Stays under 300 lines (trim old projects) | Grows over time (organize by topic) |
| **Example** | "I use Next.js and Supabase" | "Mar 1: Migrated auth from JWT to Supabase Auth. Reason: session management was breaking on mobile." |
| **File** | `context/CONTEXT.md` | `memory/MEMORY.md` |

**Think of it this way:**
- Context = your resume (current state)
- Memory = your journal (history of what happened)

---

## What to Save in Memory

Save things the AI will need to recall in future sessions. Focus on decisions, outcomes, and hard-won knowledge.

### Save This

| Category | Example |
|----------|---------|
| **Decisions and why** | "Chose Supabase over Firebase because we need row-level security and Postgres queries." |
| **Problems solved** | "Fixed CORS error by adding `credentials: 'include'` to fetch calls AND setting `allow_credentials=True` in FastAPI middleware." |
| **Architecture choices** | "API uses path-based routing through ALB. Frontend must use relative URLs (empty string for API base URL, not localhost)." |
| **Client interactions** | "BuildCorp pilot: Tom said the dashboard loads too slowly (>3s). Needs to be under 1s before they'll pay." |
| **Deployment details** | "Deployed to Railway. Environment variables are in Railway dashboard, NOT .env file in production." |
| **Things that broke** | "n8n webhook stopped working because Railway reassigned the port. Fixed by using the Railway-provided PORT env var." |
| **Key numbers** | "Feb launch: 47 signups, 12 activated, 3 started pilot. Activation rate: 25%." |
| **Tool configurations** | "PostHog self-hosted on Railway. Dashboard at analytics.novabuild.ai. Project API key in 1Password." |
| **Conventions established** | "Team agreed: all database migrations go through Supabase CLI, never through the dashboard UI." |
| **Milestones** | "Mar 5: First paying customer (GreenBuild, $799/mo Pro plan). Lisa signed after 15-min demo." |

### Do NOT Save This

| Category | Why Not | Where It Goes Instead |
|----------|---------|----------------------|
| Generic knowledge | The AI already knows how React hooks work | Nowhere -- it's built-in |
| Temporary notes | "Remind me to call Lisa at 3pm" | Your calendar or todo app |
| Secrets and credentials | Security risk if the file is shared or committed | `.env` files, 1Password, vault |
| Opinions and speculation | Memory should be facts, not guesses | Your personal notes |
| Duplicate information | If it's already in Context, don't repeat it | `context/CONTEXT.md` |
| Entire code files | Memory is for decisions about code, not code itself | The actual source files |
| Step-by-step procedures | These belong in skills, not memory | `skills/<name>/SKILL.md` |

---

## How Memory Persists Across Sessions

### Claude Code
Claude Code has a built-in memory system. Memory files are stored at:
```
~/.claude/projects/<project-path>/memory/MEMORY.md
```
This file is auto-loaded at the start of every session for that project. You can also place memory files directly in your project:
```
your-project/memory/MEMORY.md
```

### Cursor
Cursor does not have a built-in memory system. To persist memory:
1. Create a `memory/MEMORY.md` in your project root
2. Add to `.cursorrules`: "Read memory/MEMORY.md at the start of every session."
3. Cursor will load it when referenced

### Codex / ChatGPT
1. Upload `memory/MEMORY.md` as a file in your ChatGPT project
2. Or paste key memory entries into Custom Instructions
3. Re-upload when the file changes

### Any Other LLM
1. Keep `memory/MEMORY.md` in your project
2. Paste relevant sections into the conversation when needed
3. Or include instructions in your system prompt: "Read memory/MEMORY.md before starting."

---

## How to Organize Memory

### Single-File Approach (Simple)

For most people, one `MEMORY.md` file is enough. Organize by topic with headers:

```markdown
# Project Memory

## Authentication (Last updated: Mar 1, 2026)
- Migrated from JWT to Supabase Auth on Feb 15
- Key learning: session tokens must be refreshed client-side every 55 minutes
- ...

## Deployment (Last updated: Feb 28, 2026)
- Railway config: ...
- ...

## Client Interactions (Last updated: Mar 1, 2026)
- BuildCorp: ...
- GreenBuild: ...
```

### Multi-File Approach (Growing Projects)

When a single file gets past 500 lines, split by domain:

```
memory/
  MEMORY.md                  -- Main memory (recent, cross-cutting)
  deployment-notes.md        -- All deployment history
  client-interactions.md     -- Client meetings, feedback, decisions
  architecture-decisions.md  -- Why we built things the way we did
  bug-fixes.md               -- Problems and their solutions
```

Reference these from the main MEMORY.md:
```markdown
## Deployment
See `memory/deployment-notes.md` for full history.
Recent: Switched from Vercel to Railway for backend (Feb 20, 2026).
```

---

## How to Search Past Context

When you need to find something from memory:

### By Topic
```bash
grep -i "authentication" memory/MEMORY.md
```

### By Date
```bash
grep "Feb.*2026\|Mar.*2026" memory/MEMORY.md
```

### By Keyword Across All Memory Files
```bash
grep -ri "supabase" memory/
```

### Ask the AI
You can also just ask: "Check memory -- what did we decide about the authentication approach?" The AI will search its loaded memory and respond.

---

## Memory Entry Format

Every memory entry should answer: **What happened, when, and why does it matter for future sessions?**

### Standard Format

```markdown
## Topic Name (Date)
- **What:** Brief description of what happened
- **Decision:** What was decided (if applicable)
- **Why:** The reasoning behind it
- **Key detail:** The specific technical thing to remember
- **Files:** Relevant file paths (if applicable)
- **Status:** Current state (if ongoing)
```

### Compact Format (For Quick Entries)

```markdown
## Topic (Date)
- One-liner about what happened. Key detail: the specific thing. Files: `path/to/file.ts`
```

### Example Entries

Here are real-world examples of good memory entries:

```markdown
## Supabase Auth Migration (Feb 15, 2026)
- **What:** Migrated from custom JWT auth to Supabase Auth
- **Decision:** Use Supabase Auth with PKCE flow for all clients
- **Why:** Custom JWT had session management bugs on mobile (tokens not refreshing). Supabase handles refresh automatically.
- **Key detail:** Must set `autoRefreshToken: true` and `persistSession: true` in Supabase client config
- **Files:** `src/lib/supabase.ts`, `src/middleware.ts`

## BuildCorp Pilot Feedback (Feb 22, 2026)
- **What:** Tom (PM) gave feedback after 2 weeks of use
- **Positives:** Loves the AI schedule suggestions, daily summary email
- **Issues:** Dashboard takes >3s to load (needs <1s), wants to export reports as PDF
- **Decision:** Prioritize dashboard performance this sprint. PDF export goes to backlog.
- **Key detail:** Dashboard slow because it loads all projects at once. Need pagination or lazy loading.

## Railway Port Bug (Feb 18, 2026)
- **What:** n8n webhook endpoint returned 502 after Railway redeployment
- **Root cause:** Railway assigns a dynamic port via PORT env var. Our n8n config was hardcoded to 5678.
- **Fix:** Changed n8n docker command to use $PORT. Added health check endpoint.
- **Key detail:** ALWAYS use process.env.PORT on Railway, never hardcode port numbers.
- **Files:** `docker-compose.yml`, `n8n/Dockerfile`

## First Paying Customer (Mar 5, 2026)
- **What:** GreenBuild signed Pro plan at $799/mo
- **How:** Lisa (VP Ops) saw LinkedIn post, booked demo, signed same day
- **Key detail:** Lisa's main pain point was "I spend 2 hours every Monday compiling project status from 6 different spreadsheets." Our AI summary feature solved this instantly.
- **Lesson:** Lead with the time-saving angle ("2 hours to 10 seconds"), not the AI/tech angle.

## Conventions Established (Feb 10, 2026)
- All database migrations through Supabase CLI (`supabase db push`), never through dashboard UI
- API versioning: /api/v1/ prefix on all routes. No breaking changes without version bump.
- Error logging: use structured JSON logs with `request_id` field for tracing
- Git: squash merge to main, feature branches named `feat/description` or `fix/description`
```

---

## Maintaining Memory Over Time

### When to Add
- After solving a hard problem
- After making a significant decision
- After a client meeting with actionable feedback
- After a deployment (especially if something went wrong)
- After establishing a new convention or pattern
- After hitting a milestone

### When to Clean Up
- When memory exceeds 500 lines in a single file, split by topic
- When an entry is no longer relevant (project killed, tool abandoned), move it to an archive section at the bottom or delete it
- When entries contradict each other, keep the latest and delete the old one
- Quarterly: skim the full file and remove anything that no longer matters

### Archive Pattern
```markdown
---

## Archive (No Longer Active)

### Old Project X (Killed Jan 2026)
- Built a Slack bot for customer support. Killed because customers preferred email.
- Lesson: Always validate the channel preference before building.
```

---

## Common Questions

**Q: How big should my memory file get?**
A: Keep the main MEMORY.md under 500 lines. Split into topic files when it gets bigger. There is no upper limit on the total number of files.

**Q: Should I include code in memory?**
A: Only small, critical snippets (config values, one-liners that fix bugs). Full code belongs in the codebase, not memory.

**Q: What if memory contradicts context?**
A: Memory is more recent and should take priority. Then update context to match.

**Q: Can the AI update memory on its own?**
A: Yes. In Claude Code, you can tell the AI "save this to memory" and it will write to the memory file. In other tools, you may need to manually copy the AI's suggested entry.

**Q: How is this different from just reading old chat logs?**
A: Chat logs are noisy -- 95% of a conversation is exploration, false starts, and generic responses. Memory is the distilled 5% that actually matters for future work.

---

*Part of the [Agent Loadout System](https://github.com/aiagentwithdhruv/agent-loadouts-community). See MEMORY-TEMPLATE.md to get started.*
