# Sales Team Playbook

> Turn AI into your best SDR — lead generation, qualification, outreach, and pipeline management.

---

## What This Gives You

- AI finds and qualifies leads automatically
- AI writes personalized outreach emails
- AI manages follow-up sequences
- AI scores leads and routes to the right rep
- AI generates pipeline reports

---

## Setup (20 minutes)

### Step 1: Create Your Sales Context

Create `.claude/CLAUDE.md`:

```markdown
# [Company] — AI Sales Assistant

## What We Sell
- Product: [Your product/service]
- ICP: [Ideal Customer Profile — industry, size, role, pain points]
- ACV: [Average Contract Value]
- Sales cycle: [Average days from lead to close]

## Pricing
| Plan | Price | Features |
|------|-------|----------|
| Starter | $[X]/mo | [Key features] |
| Growth | $[X]/mo | [Key features] |
| Enterprise | Custom | [Key features] |

## Objection Handling
| Objection | Response |
|-----------|----------|
| "Too expensive" | [Your response] |
| "We use [competitor]" | [Your response] |
| "Not the right time" | [Your response] |

## Competitors
| Competitor | Their Price | Our Advantage |
|-----------|-------------|---------------|
| [Name] | $[X] | [Why we're better] |

## Sales Team
| Rep | Territory | Quota |
|-----|-----------|-------|
| | | |
```

### Step 2: Build Your Skill Pipeline

```
sales-loadout/
├── .claude/CLAUDE.md
├── skills/
│   ├── scrape-leads/SKILL.md      ← Find leads from any source
│   ├── classify-leads/SKILL.md    ← Score and qualify leads
│   ├── email-outreach/SKILL.md    ← Personalized cold emails
│   ├── follow-up/SKILL.md         ← Automated follow-up sequences
│   └── pipeline-report/SKILL.md   ← Weekly pipeline reports
└── LOADOUT.md
```

### Step 3: Lead Generation Skill

Create `skills/scrape-leads/SKILL.md`:

```markdown
# Scrape Leads Skill

## Trigger
When I say "find leads for [industry/location/criteria]"

## Execution
1. Search for businesses matching the criteria
2. Extract: company name, website, email, phone, industry, size
3. Verify emails are valid
4. Score leads based on ICP fit (from CLAUDE.md)
5. Output as CSV with columns: name, company, email, phone, score, reason

## Output
- CSV file with scored leads
- Summary: total found, qualified count, top 10 recommendations

## Schema
### Inputs
| Field | Type | Required |
|-------|------|----------|
| search_query | string | yes |
| location | string | no |
| max_results | integer | no (default: 50) |

### Outputs
| Field | Type |
|-------|------|
| leads_csv | file (csv) |
| summary | text |
```

### Step 4: Composition Chain

Skills chain together:

```
Find Leads → Score Leads → Write Emails → Send Outreach → Follow Up
(scrape)     (classify)    (outreach)     (send)          (follow-up)
```

Each skill's output feeds the next skill's input automatically.

---

## Metrics to Track

| Metric | Target | How AI Helps |
|--------|--------|-------------|
| Leads/week | 50+ | Automated scraping |
| Email open rate | 40%+ | Personalized subject lines |
| Reply rate | 5-10% | Relevant, researched emails |
| Demos/week | 5+ | Qualification scoring |
| Close rate | 20%+ | Objection handling context |

---

## Skill Composition Chains

### Full Pipeline
```
scrape-leads → classify-leads → casualize-names → email-outreach → follow-up
```

### Lead Enrichment Only
```
scrape-leads → classify-leads → casualize-names
```

### Outreach Only
```
email-outreach → follow-up → pipeline-report
```
