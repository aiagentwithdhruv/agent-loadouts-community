# How Skills Work

> Skills are bundled capabilities that make AI superhuman at specific tasks.
> This document explains the entire skill system: what skills are, how they work, how to create them, and how to chain them into pipelines.

---

## What Is a Skill?

A skill is a **self-contained capability package** that teaches an AI agent how to perform a specific task perfectly, every time.

Without a skill, an AI guesses. With a skill, an AI executes.

| Without Skill | With Skill |
|---------------|-----------|
| "Help me scrape leads" -- AI improvises, misses steps | AI reads the skill, follows the exact recipe, delivers verified output |
| "Set up a cold email campaign" -- AI gives generic advice | AI knows the platform, templates, warmup rules, deliverability settings |
| "Edit this video" -- AI suggests tools | AI runs the pipeline: silence removal, transitions, export settings |

A skill is NOT a prompt. It is a structured bundle:

```
skills/
  scrape-leads/
    SKILL.md          # Instructions, triggers, execution steps, schema
    scripts/          # Actual code that runs
      scraper.py
      verify.py
    templates/        # Reusable templates (email copy, configs, etc.)
    examples/         # Sample inputs and outputs
```

**The SKILL.md is the brain. The scripts are the hands.**

---

## SKILL.md Anatomy

Every skill follows the same structure. This consistency is what lets AI agents discover and use skills automatically.

### 1. Trigger

```markdown
## Trigger
Use this skill when:
- User asks to scrape leads from Google Maps
- User mentions "lead generation" or "find prospects"
- User needs business contact information for outreach
```

The trigger tells the AI **when** to activate this skill. It works like pattern matching -- the AI scans incoming requests against all available triggers and picks the best match.

### 2. Prerequisites

```markdown
## Prerequisites
- API key: `APIFY_API_KEY` in `.env`
- Python 3.10+
- Packages: `apify-client`, `pandas`
- Access: Google Maps (no auth needed)
```

What must be in place before the skill can run. API keys, tools, packages, credentials, permissions.

### 3. Execution

```markdown
## Execution
1. Collect search parameters (industry, location, radius)
2. Run `scripts/scraper.py --query "{industry}" --location "{location}"`
3. Wait for Apify actor to complete (typical: 2-5 minutes)
4. Download results to `output/raw_leads.csv`
5. Run `scripts/verify.py --input output/raw_leads.csv` to deduplicate and verify
6. Output verified leads to `output/verified_leads.csv`
```

Step-by-step instructions. Deterministic. No ambiguity. An AI agent or a human can follow these steps and get the same result.

### 4. Output

```markdown
## Output
- `output/verified_leads.csv` — Columns: name, email, phone, website, address, rating, reviews
- Typical yield: 50-200 verified leads per run
- Quality: 85-95% email verification rate
```

What the skill produces. File paths, formats, expected quality.

### 5. Schema

```markdown
## Schema

### Inputs
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `query` | string | Yes | Industry or business type to search |
| `location` | string | Yes | City, state, or coordinates |
| `radius_km` | integer | No | Search radius in km (default: 10) |
| `max_results` | integer | No | Maximum leads to return (default: 100) |

### Outputs
| Name | Type | Description |
|------|------|-------------|
| `leads_csv` | file_path | Path to verified leads CSV |
| `lead_count` | integer | Number of verified leads found |
| `verification_rate` | float | Percentage of leads with verified email |

### Credentials
| Name | Source |
|------|--------|
| `APIFY_API_KEY` | .env |

### Composable With
`classify-leads`, `casualize-names`, `instantly-campaigns`

### Cost
~$5-15 per run (Apify actor usage)
```

The schema makes skills **machine-readable**. The Loadout MCP Server, CLI, and other tools use this section for:
- Auto-discovery (search skills by input/output types)
- Composition (chain skills where one's output matches another's input)
- Cost estimation (calculate pipeline costs before running)

### 6. Error Handling

```markdown
## Error Handling
| Error | Cause | Fix |
|-------|-------|-----|
| `APIFY_API_KEY not found` | Missing .env | Add key from apify.com/account |
| `0 results returned` | Too narrow query | Broaden location or industry |
| `Rate limit exceeded` | Too many concurrent runs | Wait 60s, reduce max_results |
```

### 7. Self-Update Rules

```markdown
## Self-Update Rules
- If a new field becomes available in scraper output, add to schema
- If error patterns emerge, add to Error Handling
- If execution steps change, update and bump LOADOUT.md version
```

---

## How AI Discovers and Uses Skills

### Auto-Discovery Pattern

When an AI agent receives a request, it follows this pattern:

```
1. User says: "Find me 100 dentists in Austin, Texas"

2. Agent checks skill index:
   → cat .context/claude-skills/INDEX.md | grep -i "lead"
   → Match: gmaps-leads (Google Maps leads with enrichment)

3. Agent reads the skill:
   → cat .context/claude-skills/.claude/skills/gmaps-leads/SKILL.md

4. Agent checks prerequisites:
   → Is APIFY_API_KEY set? Yes.
   → Is Python installed? Yes.

5. Agent executes the skill step-by-step:
   → Runs scraper with query="dentist" location="Austin, TX"
   → Downloads results
   → Runs verification
   → Returns verified_leads.csv

6. Agent reports output:
   → "Found 87 verified dentists in Austin. CSV saved to output/verified_leads.csv"
```

The AI never improvises. It follows the recipe.

### The Routing Layer

For workspaces with many skills, an `AI-ROUTING.md` file acts as a decision tree:

```markdown
## AI Routing

| User Says | Use Skill | Why |
|-----------|-----------|-----|
| "find leads", "scrape", "prospects" | scrape-leads | General lead scraping |
| "Google Maps", "local businesses" | gmaps-leads | Location-based leads |
| "score leads", "qualify", "classify" | classify-leads | Lead scoring |
| "send emails", "cold outreach" | instantly-campaigns | Email campaigns |
| "edit video", "remove silence" | video-edit | Video processing |
```

The AI reads this routing table before every task and picks the right skill.

---

## Skill Categories

Skills are organized into categories based on what they do:

### Lead Generation & Sales
| Skill | What It Does |
|-------|-------------|
| `scrape-leads` | Scrape leads from any source using Apify |
| `gmaps-leads` | Google Maps business scraping with enrichment |
| `classify-leads` | Score and classify leads using LLM |
| `casualize-names` | Format names for natural outreach |
| `create-proposal` | Generate professional proposals |
| `upwork-apply` | Automate Upwork job applications |

### Email & Campaigns
| Skill | What It Does |
|-------|-------------|
| `gmail-inbox` | Multi-account Gmail management |
| `gmail-label` | Auto-label and organize emails |
| `instantly-campaigns` | Set up cold email campaigns |
| `instantly-autoreply` | AI-powered email auto-replies |
| `welcome-email` | Welcome email sequences |

### Content & Video
| Skill | What It Does |
|-------|-------------|
| `video-edit` | Video editing with silence removal |
| `pan-3d-transition` | 3D video transitions |
| `recreate-thumbnails` | Face-swap thumbnails |
| `cross-niche-outliers` | Viral video research |
| `youtube-outliers` | Niche monitoring |
| `title-variants` | Title generation |

### Research & Community
| Skill | What It Does |
|-------|-------------|
| `skool-monitor` | Skool community monitoring |
| `skool-rag` | Skool RAG pipeline |
| `literature-research` | Academic research |

### Browser Automation
| Skill | What It Does |
|-------|-------------|
| `ghost-browser` | LinkedIn auto-post/engage/apply, web scraping, human-like automation |

### Infrastructure
| Skill | What It Does |
|-------|-------------|
| `add-webhook` | Create Modal webhooks |
| `modal-deploy` | Cloud deployment |
| `local-server` | Local orchestrator |
| `design-website` | Website design automation |

---

## How to Create Your Own Skill

### Step 1: Identify a Repeatable Task

Ask yourself:
- Do I do this task more than once a week?
- Does it follow the same steps every time?
- Could someone else follow written instructions to do it?

If yes to all three, it should be a skill.

### Step 2: Create the Folder Structure

```bash
mkdir -p skills/my-new-skill/scripts
mkdir -p skills/my-new-skill/templates
```

### Step 3: Write the SKILL.md

Use the [SKILL-TEMPLATE.md](SKILL-TEMPLATE.md) as your starting point. Fill in every section:

1. **Trigger** -- When should the AI use this skill?
2. **Prerequisites** -- What does it need to run?
3. **Execution** -- What are the exact steps?
4. **Output** -- What does it produce?
5. **Schema** -- What are the typed inputs and outputs?
6. **Error Handling** -- What can go wrong and how to fix it?
7. **Self-Update Rules** -- How does this skill stay current?

### Step 4: Add Scripts (if needed)

If the skill involves code execution, add scripts to `scripts/`:

```python
# skills/my-new-skill/scripts/run.py
import argparse

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("--input", required=True)
    parser.add_argument("--output", default="output/result.csv")
    args = parser.parse_args()

    # Your logic here
    print(f"Processed {args.input} -> {args.output}")

if __name__ == "__main__":
    main()
```

### Step 5: Add Templates (if needed)

Reusable templates go in `templates/`:

```
skills/my-new-skill/templates/
  email-template.md
  config-template.json
  report-template.md
```

### Step 6: Register in INDEX.md

Add your skill to the skills index so the AI can discover it:

```markdown
| my-new-skill | What it does | Lead Gen / Email / Content / etc. |
```

### Step 7: Test It

Run through the execution steps yourself. Then ask the AI to do it. Compare outputs. Fix any gaps.

---

## Composition Chains

The real power of skills is **chaining them together**. One skill's output becomes the next skill's input, creating an automated pipeline.

### How Chains Work

```
[Skill A] --output--> [Skill B] --output--> [Skill C]
    |                     |                     |
  Scrape leads        Classify them         Format names
```

The Schema section in each SKILL.md declares:
- **Outputs** -- what this skill produces
- **Composable With** -- which skills it chains with

The system matches output types to input types automatically.

### Pre-Defined Chains

#### 1. Full Client Onboarding
```
gmaps-leads → classify-leads → casualize-names → instantly-campaigns → welcome-email
```
- **What it does:** Find leads, score them, format names, send cold emails, onboard replies
- **Time saved:** 4-6 hours per campaign (manual) to 15 minutes (automated)
- **Use case:** New client acquisition for any B2B service

#### 2. Content Pipeline
```
cross-niche-outliers → title-variants → recreate-thumbnails → video-edit
```
- **What it does:** Research viral content, generate titles, create thumbnails, edit video
- **Time saved:** 3-4 hours per video to 30 minutes
- **Use case:** YouTube content creation at scale

#### 3. Lead Enrichment
```
scrape-leads → classify-leads → casualize-names
```
- **What it does:** Scrape raw leads, score them by fit, format names for outreach
- **Time saved:** 2 hours per batch to 5 minutes
- **Use case:** Pre-qualifying leads before any outreach

#### 4. Inbox Management
```
gmail-inbox → gmail-label
```
- **What it does:** Fetch emails from multiple accounts, auto-label and organize
- **Time saved:** 30 minutes daily to zero (fully automated)
- **Use case:** Managing multiple client email accounts

### Creating Custom Chains

To create a new chain, define it in your routing file:

```markdown
## Chains

### my-custom-chain
| Step | Skill | Input | Output |
|------|-------|-------|--------|
| 1 | scrape-leads | query, location | raw_leads.csv |
| 2 | classify-leads | raw_leads.csv | scored_leads.csv |
| 3 | create-proposal | scored_leads.csv | proposals/ |
```

The AI agent reads this chain definition and executes each step in sequence, passing outputs forward.

---

## Key Principles

### 1. Deterministic Over Probabilistic
Skills contain **exact steps**, not vague instructions. The AI follows a recipe, not a suggestion.

### 2. Self-Updating
Every skill has rules for when and how to update itself. When the AI encounters a new error, it adds it to the error handling table. When a step changes, it updates the execution section.

### 3. Composable
Skills are designed to chain. Their schemas define typed inputs and outputs so the system can automatically connect them.

### 4. Reuse Before Rebuild
Before creating a new skill, check the index. The skill you need might already exist, or you might only need to adapt an existing one.

### 5. Machine-Readable
The Schema section is not just documentation -- it is structured data that tools (MCP Server, CLI, composition engine) parse and use programmatically.

---

## Summary

| Concept | What It Is |
|---------|-----------|
| **Skill** | A bundled capability with instructions + scripts + context |
| **SKILL.md** | The instruction file -- trigger, execution, output, schema |
| **Schema** | Typed inputs/outputs that enable auto-discovery and chaining |
| **Chain** | Multiple skills linked in sequence, output-to-input |
| **Auto-Discovery** | AI scans triggers and routing tables to pick the right skill |
| **Self-Update** | Skills include rules for keeping themselves current |

---

*Next: [SKILL-TEMPLATE.md](SKILL-TEMPLATE.md) -- Start building your own skill.*
