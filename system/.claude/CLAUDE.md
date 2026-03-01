# Agent Loadout System -- AI Master Instructions

> This file is auto-loaded by Claude Code when you open any project.
> It teaches the AI how your workspace is organized and how to use your skills, context, and memory system.
> Customize it to fit your workflow. Works with Claude Code, Cursor, Codex, ChatGPT, and any LLM.

---

## Core Principle: Reuse Before Rebuild

Before doing ANYTHING -- building, designing, coding, researching, automating, or creating:

1. **Check the skills library first** -- `skills/` or `.claude/skills/`
2. **Search for existing patterns** -- look at skill names, read the relevant SKILL.md
3. **Adapt what exists** instead of starting from scratch
4. **Only build new** if nothing in the library matches

This applies to every task: code, automation, content, research, deployment, client work, analysis. No exceptions.

**Why this matters:**
- 5x faster execution (proven patterns, not guesswork)
- Zero wasted effort (never rebuild what already works)
- Compound learning (every skill builds on the last)
- The AI gets smarter every time you add a skill

---

## How the System Works

### Three Layers

```
Layer 1: Context       -- WHO you are, WHAT you're working on
Layer 2: Skills        -- HOW to do specific tasks (step-by-step recipes)
Layer 3: Memory        -- WHAT happened before (persists across sessions)
```

**Context** gives the AI your identity, projects, and preferences.
**Skills** give the AI repeatable procedures it can execute perfectly.
**Memory** gives the AI history so it never forgets past decisions, fixes, or learnings.

Together, they turn a generic AI into your personal expert that improves over time.

### File Locations

| File | Purpose | Loaded When |
|------|---------|-------------|
| `.claude/CLAUDE.md` | Master instructions (this file) | Every session (auto) |
| `context/CONTEXT.md` | Your identity, projects, priorities | Read at session start |
| `skills/<name>/SKILL.md` | Task-specific recipes and templates | Read when task matches |
| `memory/MEMORY.md` | Persistent learnings and history | Read at session start |
| `LOADOUT.md` | Project manifest (what's included) | Read on demand |

---

## How to Use Skills

### Auto-Discovery Pattern

When a task comes in, follow this sequence:

1. **Identify the task type** -- What category? (code, email, research, deployment, etc.)
2. **Search for a matching skill:**
   ```bash
   ls skills/
   # or
   ls .claude/skills/
   ```
3. **Read the skill:**
   ```bash
   cat skills/<skill-name>/SKILL.md
   ```
4. **Follow the recipe** -- execute the steps in order
5. **If no skill exists** -- do the task, then consider creating a skill for next time

### Skill Structure

Every skill follows this format:

```
skills/<skill-name>/
  SKILL.md          -- When to use, recipe, templates, common mistakes
  scripts/          -- (optional) Automation scripts
  templates/        -- (optional) Copy-paste templates
```

### Creating New Skills

When you notice a repeated task (done 3+ times), create a skill:

1. Create `skills/<task-name>/SKILL.md`
2. Document: trigger conditions, step-by-step recipe, templates, common mistakes
3. Add any helper scripts to `skills/<task-name>/scripts/`
4. Test the skill by running through it once

---

## Session Workflow

### At the Start of Every Session

1. **Read context** -- `context/CONTEXT.md` (who you are, what matters now)
2. **Read memory** -- `memory/MEMORY.md` (what happened in past sessions)
3. **Check priorities** -- what's the most important thing right now?

### When Asked to Build Something

1. **Search skills library** -- does a skill for this exist?
2. **Reuse existing patterns** -- adapt the skill recipe to this specific case
3. **Only build from scratch** if no skill matches
4. **After building** -- consider: should this become a new skill?

### When Asked to Automate Something

1. **Check for automation skills** -- deployment, email, scraping, reporting, etc.
2. **Look for composable chains** -- can you combine 2-3 skills to solve this?
3. **Execute the recipe** -- follow the skill's steps exactly
4. **Log the result** in memory if it's significant

### At the End of a Session

1. **Update memory** with any important decisions, fixes, or discoveries
2. **Update skills** if you found a better way to do something
3. **Update context** if priorities or projects changed

---

## The Self-Annealing Loop

When something goes wrong, the system improves itself:

```
Error occurs
    --> Diagnose the root cause
    --> Fix the issue
    --> Update the relevant skill's "Common Mistakes" section
    --> Update memory with what happened and why
    --> System is now smarter for next time
```

This means:
- The same mistake never happens twice
- Skills get better with every use
- The AI accumulates real-world fixes, not just theory

### What to Update and Where

| What Happened | Update This |
|---------------|-------------|
| Found a bug pattern | Skill's "Common Mistakes" table |
| Discovered a better approach | Skill's "Recipe" section |
| Made a significant decision | `memory/MEMORY.md` |
| Project priorities changed | `context/CONTEXT.md` |
| New tool or service added | Context + relevant skill |
| Completed a major milestone | Memory + context |

---

## Memory System

Memory persists across sessions. It is how the AI remembers what happened yesterday, last week, or last month.

### What Goes in Memory

- Decisions made and why
- Problems solved (especially tricky ones)
- Architecture choices
- Client interactions and outcomes
- Things that broke and how they were fixed
- Key dates, milestones, deadlines

### What Does NOT Go in Memory

- Generic knowledge (the AI already knows this)
- Temporary information (use scratch files)
- Secrets, passwords, API keys (use .env files)
- Opinions or speculation (only facts and outcomes)

### Memory Format

```markdown
## Topic Name (Date)
- **What:** Brief description of what happened
- **Decision:** What was decided and why
- **Key detail:** The specific thing to remember
- **Files:** Relevant file paths
```

See `memory/HOW-MEMORY-WORKS.md` for the full guide.

---

## Context System

Context tells the AI who you are and what you're working on right now.

### What Goes in Context

- Your identity (name, role, company)
- Current projects and their status
- Tech stack and conventions
- Communication preferences
- Decision-making framework
- Active priorities

### Keeping Context Fresh

Context has self-update rules. When something changes, the AI updates the relevant section:

| Event | Update |
|-------|--------|
| New project started | Add to projects list |
| Project completed | Move to completed, add outcome |
| Priority changed | Update priorities section |
| Tech stack changed | Update stack section |
| New team member | Update contacts |

See `context/CONTEXT-TEMPLATE.md` for the full template.

---

## Architecture Pattern

### The 3-Layer Stack

```
+---------------------------+
|     Skills Layer          |  SKILL.md files with recipes,
|     (Capabilities)        |  templates, and scripts
+---------------------------+
|     Orchestration Layer   |  AI reads context + memory,
|     (Decision-Making)     |  picks the right skill, adapts
+---------------------------+
|     Shared Utilities      |  Common scripts, templates,
|     (Infrastructure)      |  tools used across skills
+---------------------------+
```

**Skills Layer:** Bundled capabilities. Each skill is self-contained with its own recipe, templates, and scripts.

**Orchestration Layer:** The AI itself. It reads your context, understands the request, selects the right skill, and adapts the recipe to the specific situation.

**Shared Utilities:** Common code, templates, and tools that multiple skills use. Avoids duplication.

### Key Design Principle

> Separate probabilistic AI (decision-making, understanding, adapting) from deterministic code (scripts, templates, fixed procedures).

The AI decides WHAT to do. The skills define HOW to do it. This maximizes reliability.

---

## Cross-Platform Usage

This system works with any AI tool. Here is how to set it up:

| Platform | Setup |
|----------|-------|
| **Claude Code** | Drop `.claude/CLAUDE.md` in your project root. It auto-loads every session. |
| **Cursor** | Copy content to `.cursor/rules/loadout.mdc` or `.cursorrules` |
| **Codex / OpenAI** | Use as `AGENTS.md` in your repo root (Linux Foundation standard) |
| **ChatGPT** | Paste into Custom Instructions or upload as a file in a project |
| **Any LLM** | Feed as system prompt or attach as context at the start of conversation |

### Platform-Specific Notes

**Claude Code:**
- `.claude/CLAUDE.md` is auto-loaded at project level
- Memory files go in `~/.claude/projects/<project>/memory/`
- Skills go in `.claude/skills/<name>/SKILL.md`

**Cursor:**
- Use `.cursorrules` at project root for auto-loading
- Or `.cursor/rules/*.mdc` for multiple context files
- Reference skills with `@file` mentions

**Codex / AGENTS.md:**
- Place `AGENTS.md` at repo root
- Include key context inline (Codex reads the full file)
- Reference skills by relative path

**ChatGPT / General LLMs:**
- Paste the most critical sections (context + active skills) into the system prompt
- For long contexts, upload as files to a ChatGPT project
- Refresh context manually at the start of each session

---

## Quick Commands

```bash
# List all skills
ls skills/

# Read a specific skill
cat skills/<skill-name>/SKILL.md

# Check memory
cat memory/MEMORY.md

# Check context
cat context/CONTEXT.md

# Search for a skill by keyword
grep -ri "keyword" skills/
```

---

## Principles to Follow

1. **Reuse before rebuild** -- always check skills library first
2. **Update as you go** -- keep memory and context current
3. **Self-anneal on errors** -- fix, document, improve
4. **Compound over time** -- every session should make the system smarter
5. **Keep it simple** -- a 20-line skill that works beats a 200-line one that doesn't
6. **Facts over opinions** -- memory stores what happened, not what might happen

---

*Part of the [Agent Loadout System](https://github.com/aiagentwithdhruv/agent-loadouts-community). Customize this file for your workflow.*
