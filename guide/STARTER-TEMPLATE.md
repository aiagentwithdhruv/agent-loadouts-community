# AI Loadout — Starter Template
### Copy this. Fill it in. Your AI becomes a specialist.

---

## Step 1: Copy this as `CONTEXT.md` in your project root

```markdown
# [Your Project Name] — AI Context

## What This Is
[One paragraph. What does this project do? Who is it for?]

## Tech Stack
- Language: [Python / TypeScript / etc.]
- Framework: [Next.js / FastAPI / Flask / etc.]
- Database: [Supabase / PostgreSQL / MongoDB / etc.]
- Deployment: [Vercel / Railway / AWS / etc.]

## Folder Structure
| Folder | What's Inside |
|--------|--------------|
| `src/` | Main source code |
| `src/api/` | API routes |
| `src/components/` | UI components |
| `tests/` | Test files |
| `.env` | Environment variables (never commit) |

## Key Files
| File | Purpose |
|------|---------|
| `src/main.py` | Entry point |
| `src/config.py` | Configuration |
| `.env.example` | Required env vars |

## My Rules
- [Convention 1, e.g., "Use TypeScript strict mode"]
- [Convention 2, e.g., "All API responses: {success, data, error}"]
- [Convention 3, e.g., "No class-based components, only functions"]

## Common Tasks
1. **Run locally** → `npm run dev` or `python main.py`
2. **Add new feature** → [where to create files, what pattern to follow]
3. **Deploy** → [your deploy command or process]
4. **Debug** → [where to look first when something breaks]

## Environment Variables
| Variable | Where to Get It |
|----------|----------------|
| `API_KEY` | [Dashboard URL or description] |
| `DATABASE_URL` | [How to find this] |
```

---

## Step 2: Copy this as `.claude/skills/[your-task]/SKILL.md`

```markdown
# Skill: [task-name]

> [One line: what does this skill do?]

## When to Use
- [Situation 1 that triggers this skill]
- [Situation 2]

## Recipe
1. [First step — be specific]
2. [Second step]
3. [Third step]
4. [Fourth step]

## Templates

### Template 1: [Name]
[Copy-paste template, code snippet, or prompt]

### Template 2: [Name]
[Another template]

## Common Mistakes
| Mistake | Fix |
|---------|-----|
| [What goes wrong] | [How to prevent/fix it] |
| [Another common error] | [The solution] |

## Files This Skill Uses
| File | Purpose |
|------|---------|
| `path/to/file` | [Why this file matters] |
```

---

## Step 3: Copy this as `LOADOUT.md` in your project root

```markdown
---
name: [project-name]
version: 1.0.0
description: [One line description]
author: [Your name]
last_verified: [Today's date]
---

# [Project Name] — Loadout

> [One paragraph: what this project is and what the AI needs to know]

## What's Included

| File | Type | Purpose |
|------|------|---------|
| `CONTEXT.md` | Context | Project overview, stack, structure |
| `.claude/skills/[skill]/SKILL.md` | Skill | [What this skill does] |

## Quick Reference
[The 3-5 most important things your AI needs to know — endpoints, commands, credentials location]

## Self-Update Rules

| When This Happens | Update This File |
|-------------------|-----------------|
| New feature added | CONTEXT.md (folder structure + key files) |
| New repeated task found | Create a new skill in .claude/skills/ |
| Bug pattern discovered | Add to skill's Common Mistakes |
| Dependency changed | CONTEXT.md (tech stack) |
| New team member | Share this LOADOUT.md |
```

---

## That's It. 3 Files.

```
your-project/
  LOADOUT.md           ← The manifest (what's included)
  CONTEXT.md           ← The brain (project knowledge)
  .claude/skills/
    [task]/SKILL.md    ← The muscle (how to do specific tasks)
```

**Time to set up:** 15-20 minutes
**Time saved per AI session:** 5-15 minutes
**Sessions per week:** 20+
**Time saved per week:** 2-5 hours

The math is simple. Do it once, benefit forever.

---

## Quick Wins: First Skills to Create

Not sure what skill to create first? Pick whichever you do most:

| If You Often... | Create This Skill |
|----------------|-------------------|
| Answer customer/student questions | `customer-support` — templates + common Q&A |
| Write API endpoints | `api-builder` — your patterns + boilerplate |
| Debug errors | `debugger` — your logs location + common fixes |
| Deploy code | `deployer` — exact commands + checklist |
| Write emails | `email-writer` — your tone + templates |
| Create content | `content-creator` — your style + formats |
| Onboard clients | `onboarding` — steps + templates + timelines |

**Start with 1. Add more as you go. Your AI compounds.**

---

*From the [AI Loadout Guide](README.md) by [AiwithDhruv](https://github.com/aiagentwithdhruv)*
