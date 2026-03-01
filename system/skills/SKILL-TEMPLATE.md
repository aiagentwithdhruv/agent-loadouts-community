# Skill: {skill-name}

> {One-line description of what this skill does.}

---

## Trigger

Use this skill when:
- {Condition 1 -- what the user says or asks for}
- {Condition 2 -- keywords or phrases that activate this skill}
- {Condition 3 -- situational trigger}

Do NOT use this skill when:
- {Anti-pattern 1 -- when a different skill is more appropriate}
- {Anti-pattern 2 -- when prerequisites are not met}

---

## Prerequisites

### Tools & Runtime
| Tool | Version | Install |
|------|---------|---------|
| {Python/Node/etc.} | {3.10+/18+/etc.} | {brew install python3 / nvm install 18} |
| {Package 1} | {latest} | {pip install package-name} |
| {Package 2} | {latest} | {npm install package-name} |

### Credentials
| Name | Where to Get It | Store In |
|------|----------------|----------|
| `{API_KEY_NAME}` | {URL or description} | `.env` |
| `{SECRET_NAME}` | {URL or description} | `.env` |

### Files Required
| File | Purpose |
|------|---------|
| `scripts/{script-name}.py` | {What this script does} |
| `templates/{template-name}.md` | {What this template is for} |

### Pre-Checks
Before running, verify:
1. {Check 1 -- e.g., "API key is set: `echo $API_KEY_NAME`"}
2. {Check 2 -- e.g., "Input file exists: `ls input/data.csv`"}
3. {Check 3 -- e.g., "Network access to api.example.com"}

---

## Execution

### Step 1: {Action Name}
```bash
{Command or code to run}
```
**Expected result:** {What should happen}
**If it fails:** {What to do}

### Step 2: {Action Name}
```bash
{Command or code to run}
```
**Expected result:** {What should happen}
**If it fails:** {What to do}

### Step 3: {Action Name}
```bash
{Command or code to run}
```
**Expected result:** {What should happen}
**If it fails:** {What to do}

### Step 4: {Action Name}
```bash
{Command or code to run}
```
**Expected result:** {What should happen}

<!-- Add as many steps as needed. Each step should be atomic and verifiable. -->

---

## Output

### Deliverables
| Deliverable | Format | Location |
|-------------|--------|----------|
| {Primary output} | {CSV/JSON/PDF/etc.} | `output/{filename}` |
| {Secondary output} | {Format} | `output/{filename}` |
| {Log/report} | {Format} | `output/{filename}` |

### Quality Criteria
- {Criterion 1 -- e.g., "All emails verified with >85% deliverability"}
- {Criterion 2 -- e.g., "No duplicate entries in output"}
- {Criterion 3 -- e.g., "All required fields populated"}

### Sample Output
```
{Example of what the output looks like -- a few rows of CSV, a JSON snippet, etc.}
```

---

## Schema

> Typed schema for programmatic discovery and composition.
> This section is required. Used by the Loadout MCP Server, CLI, and composition engine.

### Inputs
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `{param_1}` | string | Yes | -- | {What this parameter does} |
| `{param_2}` | string | Yes | -- | {What this parameter does} |
| `{param_3}` | integer | No | {default} | {What this parameter does} |
| `{param_4}` | boolean | No | false | {What this parameter does} |

### Outputs
| Name | Type | Description |
|------|------|-------------|
| `{output_1}` | file_path | {What this output contains} |
| `{output_2}` | integer | {What this output contains} |
| `{output_3}` | object | {What this output contains} |

### Credentials
| Name | Source | Required |
|------|--------|----------|
| `{ENV_VAR_1}` | .env | Yes |
| `{ENV_VAR_2}` | .env / Modal dashboard | No |

### Composable With
Skills that chain well with this one:

| Direction | Skill | How |
|-----------|-------|-----|
| **Input from** | `{skill-name}` | {This skill's output feeds our input} |
| **Output to** | `{skill-name}` | {Our output feeds this skill's input} |

### Cost
| Component | Cost |
|-----------|------|
| {API calls} | {$X per Y} |
| {Compute} | {Free / $X per run} |
| **Total per run** | **{$X - $Y typical}** |

---

## Error Handling

| Error | Cause | Fix |
|-------|-------|-----|
| `{error message or code}` | {Why it happens} | {Exact fix -- command, config change, or workaround} |
| `{error message or code}` | {Why it happens} | {Exact fix} |
| `{error message or code}` | {Why it happens} | {Exact fix} |

### Common Mistakes
| Mistake | Why It Happens | Prevention |
|---------|---------------|------------|
| {Mistake 1} | {Root cause} | {How to avoid} |
| {Mistake 2} | {Root cause} | {How to avoid} |

### Retry Logic
- **Transient failures** (network, rate limit): Retry up to {3} times with {exponential backoff / 30s delay}
- **Permanent failures** (auth, bad input): Do not retry. Report error and stop.
- **Partial results**: {Save what you have / discard and retry from scratch}

---

## Templates

<!-- Include any reusable templates this skill uses -->

### {Template 1 Name}
```
{Template content -- email copy, config file, API request body, etc.}
```

### {Template 2 Name}
```
{Template content}
```

---

## Examples

### Example 1: {Scenario Name}

**Input:**
```json
{
  "param_1": "value",
  "param_2": "value"
}
```

**Command:**
```bash
{Exact command to run}
```

**Output:**
```
{What the output looks like}
```

### Example 2: {Scenario Name}

**Input:**
```json
{
  "param_1": "different value",
  "param_2": "different value"
}
```

**Output:**
```
{What the output looks like}
```

---

## Self-Update Rules

### After Every Run
1. If a new error pattern emerges, add to Error Handling table
2. If output format changes, update Output section and Schema
3. If a step becomes unnecessary, remove it and note why

### After API/Tool Changes
1. If the API version changes, update Prerequisites and Execution steps
2. If rate limits change, update Error Handling and Cost
3. If new fields become available, add to Schema outputs

### After Composition
1. If this skill is used in a new chain, add to Composable With
2. If input/output types change, update Schema to maintain compatibility

### Cross-File Updates
When updating this file, also check:
- `../../LOADOUT.md` -- version, changelog
- `../../.claude/CLAUDE.md` -- if skill triggers changed
- `../INDEX.md` -- if skill name or description changed

---

## Changelog

| Date | Change | By |
|------|--------|-----|
| {YYYY-MM-DD} | Initial skill creation | {author} |
