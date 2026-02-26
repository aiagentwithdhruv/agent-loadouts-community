# Agent Loadouts (Community Edition)

**Everyone has AI now. The difference is how you load it.**

A soldier with 10 guns who doesn't know how to load any of them loses to a soldier with 1 loaded gun. That's most people with AI right now.

**Agent Loadouts** are structured context packs that turn generic AI into YOUR personal expert — instantly.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

By [AiwithDhruv](https://www.linkedin.com/in/aiwithdhruv/) | [GitHub](https://github.com/aiagentwithdhruv)

---

## New: The AI Loadout Guide

**Go from Level 1 to Level 5 in 20 minutes.**

| Level | What They Do | Result |
|-------|-------------|--------|
| Level 1 | Use AI with no context | Generic answers, start from zero each time |
| Level 2 | Copy-paste prompts | Better, but no memory between sessions |
| Level 3 | Use CONTEXT.md | AI knows your project, starts at 50% |
| Level 4 | Use Skills | AI knows HOW to do specific tasks perfectly |
| **Level 5** | **Full Loadout** | **AI is a specialist that improves over time** |

| Resource | What You Get | Time |
|----------|-------------|------|
| **[The Concept](guide/README.md)** | Why loadouts matter, the 3-layer system, real examples | 5 min read |
| **[Starter Template](guide/STARTER-TEMPLATE.md)** | Copy-paste CONTEXT.md + SKILL.md + LOADOUT.md | 15 min setup |
| **[Real Example](guide/EXAMPLE-euri-api.md)** | Production Euri API loadout — before vs after | 3 min read |

---

## The Problem

Every AI agent starts as a blank slate. You give it a vague system prompt, and it gives generic answers.

**Your agent doesn't need a better model. It needs better context.**

## The Solution

Agent Loadouts are structured context packages that instantly give AI agents deep domain expertise:

- **Company context** — who you are, what you sell, your positioning
- **Market research** — industry size, trends, competitive landscape
- **Codebase maps** — architecture, file structure, technical recipes
- **Sales playbooks** — objection handling, buyer psychology, win patterns
- **Runbooks** — step-by-step procedures for deployment, configuration, troubleshooting
- **Test cases** — verify the agent actually knows what it should
- **Self-update rules** — keep context fresh automatically

**Result:** Agents that perform like domain experts, not generic chatbots.

---

## Quick Start

### 1. Copy a template

```bash
git clone https://github.com/aiagentwithdhruv/agent-loadouts-community.git
cp -r agent-loadouts-community/templates/ ./my-project-loadout/
```

### 2. Fill in the templates

```bash
# Start with the manifest
mv my-project-loadout/LOADOUT-TEMPLATE.md my-project-loadout/LOADOUT.md

# Create your master context
mkdir -p my-project-loadout/.claude
mv my-project-loadout/CONTEXT-TEMPLATE.md my-project-loadout/.claude/CLAUDE.md

# Add domain knowledge, runbooks, tests
```

### 3. Open with Claude Code

```bash
cd my-project-loadout
claude  # Agent auto-loads context, instantly knows your domain
```

---

## Loadout Structure

```
my-loadout/
├── LOADOUT.md              # Manifest (version, description, what's included)
├── .claude/
│   └── CLAUDE.md           # Auto-loaded master context
├── knowledge/              # Domain knowledge
│   ├── market-research.md
│   ├── competitors.md
│   └── glossary.md
├── skills/                 # System-specific deep context
│   └── system-name/
│       └── SKILL.md
├── runbooks/               # Step-by-step procedures
│   └── deploy.md
├── tests/                  # Validation test cases
│   └── system-tests.md
└── workflows/              # Automation exports
    └── *.json
```

---

## Templates Included

| Template | Purpose |
|----------|---------|
| [LOADOUT-TEMPLATE.md](templates/LOADOUT-TEMPLATE.md) | Loadout manifest — version, included files, quick start |
| [CONTEXT-TEMPLATE.md](templates/CONTEXT-TEMPLATE.md) | Master AI context — auto-loaded by Claude Code |
| [SKILL-TEMPLATE.md](templates/SKILL-TEMPLATE.md) | System skill — codebase map, recipes, domain knowledge |
| [RUNBOOK-TEMPLATE.md](templates/RUNBOOK-TEMPLATE.md) | Step-by-step procedures with verification |
| [TEST-TEMPLATE.md](templates/TEST-TEMPLATE.md) | Test cases to validate agent knowledge |

---

## Example Loadouts

### Included (Free)

| Loadout | Description |
|---------|-------------|
| [Euri API](examples/euri-api/) | AI gateway loadout — 24 models, code recipes, common mistakes, n8n integration |
| [SaaS Starter](examples/saas-starter/) | Generic SaaS company loadout — product, pricing, architecture |
| [Freelancer](examples/freelancer/) | Freelance developer loadout — services, pricing, proposals |

### Premium (Available Separately)

| Loadout | Description |
|---------|-------------|
| Construction SaaS Intelligence | Full construction management domain — market research, competitor analysis, sales playbook, AI agents |
| AI Sales Coach | SaaS sales coaching platform — product context, feature knowledge, deployment |
| Revenue Engine | Freelance revenue system — channel strategies, proposal templates, pipeline tracking |

[Get Premium Loadouts](https://www.linkedin.com/in/aiwithdhruv/)

---

## Cross-Platform Support

| Platform | How to Use |
|----------|-----------|
| **Claude Code** | Drop in project root — `.claude/CLAUDE.md` auto-loads |
| **Cursor** | Copy to `.cursor/rules/*.mdc` |
| **Codex / OpenAI** | Use as `AGENTS.md` format |
| **Any LLM** | Feed as system prompt / context |

---

## Self-Update Rules

The key innovation: loadouts include instructions that tell AI agents **when and how to update their own context**.

```markdown
## Self-Update Rules

### Auto-Update Triggers
| Event | Update | Section |
|-------|--------|---------|
| New feature built | Add to features list | What's Built |
| Pricing changed | Update pricing table | Product Info |
| Bug fixed | Mark resolved in Known Issues | Tech Debt |

### Verification Schedule
| Section | Verify Every | How |
|---------|-------------|-----|
| Pricing | Monthly | Check website |
| Competitors | Quarterly | Web search |
| Market data | Yearly | Check industry reports |
```

This means your agent context **never goes stale**.

---

## Why Not Just Use a System Prompt?

| Feature | System Prompt | Agent Loadout |
|---------|--------------|---------------|
| Auto-loaded | Manual copy-paste | Auto-loaded by Claude Code |
| Structured | Freeform text | Standardized format |
| Self-updating | Static, rots | Rules to keep it fresh |
| Verifiable | Hope it works | Test cases prove it |
| Multi-file | Single string | Context + skills + knowledge + runbooks + tests |
| Cross-platform | One tool only | Claude, Cursor, Codex, any LLM |
| Composable | Standalone | Loadouts can depend on other loadouts |

---

## Research

The [AGENTS.md standard](https://github.com/anthropics/agents-md) (Linux Foundation, co-founded by Anthropic/OpenAI) found structured agent context reduces runtime by **28.64%** and improves task completion. Agent Loadouts extend this with self-update rules, verification layers, and domain-specific knowledge packs.

---

## Contributing

1. Fork this repo
2. Create a loadout using the templates
3. Submit a PR with your loadout in `examples/`

---

## License

MIT — free to use, modify, and distribute.

---

## Built by [AiwithDhruv](https://www.linkedin.com/in/aiwithdhruv/)

Building AI systems that actually work. Premium loadouts, consulting, and custom agent development available.
