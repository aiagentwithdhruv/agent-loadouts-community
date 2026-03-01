# Agency Owner Playbook

> Turn AI into your operations team — client onboarding, project management, reporting, and scaling.

---

## What This Gives You

- AI onboards new clients with templates and checklists
- AI generates proposals with your pricing
- AI creates client reports automatically
- AI manages multiple projects without dropping context
- AI handles follow-ups and renewals

---

## Setup (20 minutes)

### Step 1: Create Your Agency Context

Create `.claude/CLAUDE.md`:

```markdown
# [Agency Name] — AI Operations Assistant

## Services
| Service | Price | Delivery | Margin |
|---------|-------|----------|--------|
| [Service 1] | $[X] | [Y days] | [Z%] |
| [Service 2] | $[X] | [Y days] | [Z%] |

## Active Clients
| Client | Service | MRR | Start Date | Health |
|--------|---------|-----|------------|--------|
| | | | | |

## Team
| Person | Role | Capacity |
|--------|------|----------|
| | | |

## Processes
- Onboarding: [Link to onboarding checklist]
- Reporting: [Monthly / Weekly]
- Communication: [Slack / Email / Both]

## Revenue
- Current MRR: $[X]
- Target MRR: $[X]
- Churn rate: [X%]
```

### Step 2: Agency Skill Pipeline

```
agency-loadout/
├── .claude/CLAUDE.md
├── skills/
│   ├── create-proposal/SKILL.md      ← Generate client proposals
│   ├── onboarding/SKILL.md           ← New client setup
│   ├── generate-report/SKILL.md      ← Client deliverable reports
│   ├── pipeline-tracker/SKILL.md     ← Track leads and deals
│   └── renewal-reminder/SKILL.md     ← Contract renewal alerts
├── clients/
│   ├── client-a/CONTEXT.md           ← Per-client context
│   └── client-b/CONTEXT.md
└── LOADOUT.md
```

### Step 3: Client Onboarding Skill

```markdown
# Client Onboarding Skill

## Trigger
When I say "onboard [client name]" or "new client setup"

## Execution
1. Create a client folder with CONTEXT.md
2. Fill in from the proposal/contract:
   - Company name, industry, size
   - Service purchased, pricing, start date
   - Key contacts (name, email, role)
   - Project scope and deliverables
   - Communication preferences
3. Create project milestones
4. Draft welcome email using our template
5. Set up reporting schedule

## Output
- Client CONTEXT.md (filled)
- Welcome email draft
- Project milestone timeline
- First report template
```

---

## Scaling Pattern

```
Single freelancer → 2-3 subcontractors → Agency with processes → AI-powered operations
```

Each stage adds more skills:

| Stage | Add These Skills |
|-------|-----------------|
| Solo | write-proposal, generate-report |
| Small team | onboarding, pipeline-tracker |
| Agency | renewal-reminder, team-assignment, capacity-planning |
| Scaled | white-label, multi-client dashboards |
