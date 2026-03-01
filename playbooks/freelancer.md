# Freelancer Playbook

> Turn AI into your business partner — proposals, pricing, clients, and outreach on autopilot.

---

## What This Gives You

- AI writes proposals in your voice with your pricing
- AI manages your client pipeline
- AI applies to Upwork/Fiverr jobs automatically
- AI handles email outreach and follow-ups
- AI generates reports for clients

---

## Setup (15 minutes)

### Step 1: Create Your Context

Create `.claude/CLAUDE.md` in your project root:

```markdown
# [Your Name] — AI Freelancer Assistant

## Who I Am
- Name: [Your name]
- Services: [What you sell — e.g., "AI automation, web scraping, chatbot development"]
- Experience: [Years, key clients, notable projects]
- Platforms: [Upwork, Fiverr, LinkedIn, direct outreach]

## Pricing
| Service | Price | Delivery |
|---------|-------|----------|
| [Service 1] | $[X] | [Y days] |
| [Service 2] | $[X] | [Y days] |
| [Service 3] | $[X] | [Y days] |

## My Voice
- Tone: [Professional but friendly / Technical / Casual]
- Proposal style: [Direct and results-focused]
- Never say: [List things to avoid]

## Current Pipeline
| Client | Project | Status | Value |
|--------|---------|--------|-------|
| | | | |

## Monthly Revenue Target: $[X]
```

### Step 2: Add Skills

Copy these skill templates to your project:

```
my-freelance-loadout/
├── .claude/CLAUDE.md          ← Your context (from Step 1)
├── skills/
│   ├── write-proposal/
│   │   └── SKILL.md           ← Proposal generation
│   ├── upwork-apply/
│   │   └── SKILL.md           ← Upwork job applications
│   ├── email-outreach/
│   │   └── SKILL.md           ← Cold email campaigns
│   ├── generate-report/
│   │   └── SKILL.md           ← Client deliverable reports
│   └── manage-pipeline/
│       └── SKILL.md           ← Pipeline tracking
└── LOADOUT.md                 ← Manifest
```

### Step 3: Create a Proposal Skill

Create `skills/write-proposal/SKILL.md`:

```markdown
# Write Proposal Skill

## Trigger
When I say "write a proposal for [client/project]"

## Execution
1. Read my pricing from CLAUDE.md
2. Analyze the client's requirements
3. Write a proposal with:
   - Understanding of their problem
   - My proposed solution
   - Timeline and milestones
   - Pricing (from my pricing table)
   - Why I'm the right fit (from my experience)
4. Format as a clean document
5. Include a clear call-to-action

## Output
- Complete proposal (markdown)
- Follow-up email draft

## Rules
- Always use my actual pricing, never make up numbers
- Reference relevant past projects from my context
- Keep proposals under 1 page unless the project requires more
- End with a specific next step (call, demo, start date)
```

### Step 4: Open With AI

```bash
cd my-freelance-loadout
claude  # or cursor, or paste CLAUDE.md into ChatGPT
```

Now say: "Write a proposal for a client who needs a chatbot for their e-commerce store"

The AI will use YOUR pricing, YOUR voice, YOUR experience.

---

## Skills to Build Over Time

| Week | Add This Skill | What It Does |
|------|---------------|--------------|
| Week 1 | write-proposal | Generate proposals in your voice |
| Week 2 | upwork-apply | Auto-apply to matching Upwork jobs |
| Week 3 | email-outreach | Cold email sequences |
| Week 4 | generate-report | Client deliverable reports |
| Month 2 | manage-pipeline | Track leads, clients, revenue |
| Month 3 | client-onboarding | Automate new client setup |

---

## Revenue Targets

| Milestone | Monthly Revenue | How |
|-----------|----------------|-----|
| Getting started | $1,000 | 2-3 small projects |
| Consistent | $3,000 | 5-6 projects + retainers |
| Scaling | $5,000+ | Retainers + premium pricing |
| Agency | $10,000+ | Subcontractors + systems |

---

## Pro Tips

1. **Update your context after every project** — add the client, what you built, and what you learned
2. **Let AI write the first draft** — you edit and personalize
3. **Track what wins** — note which proposal templates convert best
4. **Build skills from repetition** — if you do something 3+ times, make it a skill
