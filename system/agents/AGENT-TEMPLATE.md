# Agent: {agent-name}

> {One-line description of what this agent does and the judgment it provides.}

---

## Role

You are a **{role title}**. You specialize in {domain/expertise area}.

**Primary responsibility:** {What this agent is accountable for -- the core judgment it makes.}

**You are NOT:** {What this agent does not do -- clarify boundaries to prevent scope creep.}

---

## Trigger

Activate this agent when:
- {Condition 1 -- what the user says or asks for}
- {Condition 2 -- keywords or situational triggers}
- {Condition 3 -- when other skills/agents cannot handle the task}

Do NOT activate when:
- {Anti-pattern 1 -- when a skill is more appropriate}
- {Anti-pattern 2 -- when a different agent handles this better}

---

## Context

### What You Receive
| Input | Type | Description |
|-------|------|-------------|
| {input_1} | {string/file/object} | {What this input contains} |
| {input_2} | {string/file/object} | {What this input contains} |

### What You Know
- {Domain knowledge 1 -- what expertise this agent has}
- {Domain knowledge 2}
- {Domain knowledge 3}

### What You Have Access To
- {Resource 1 -- files, databases, APIs}
- {Resource 2}

---

## System Prompt

> This is the prompt sent to the AI when this agent is activated.
> Copy this section exactly when invoking the agent.

```
You are a {role title}. Your job is to {primary responsibility}.

CONTEXT:
{Describe the context the agent operates in. What does it know? What can it see?}

TASK:
Given the following {input type}, you must:
1. {Analysis step -- what to examine}
2. {Evaluation step -- what criteria to apply}
3. {Decision step -- what judgment to make}
4. {Output step -- how to format the response}

OUTPUT FORMAT:
{Define the exact structure. Example:}

## Verdict: {PASS | FAIL | NEEDS_REVIEW}

### Summary
{1-2 sentence summary of your assessment}

### Findings
| # | Finding | Severity | Details |
|---|---------|----------|---------|
| 1 | {finding} | {critical/major/minor/info} | {explanation} |

### Recommendation
{What should happen next}

RULES:
- ALWAYS {non-negotiable behavior 1}
- ALWAYS {non-negotiable behavior 2}
- NEVER {prohibited behavior 1}
- NEVER {prohibited behavior 2}
- WHEN UNCERTAIN: {what to do when the answer is not clear}

QUALITY BAR:
- {What "good" looks like for this agent}
- {Minimum standard for output}
```

---

## Decision Framework

### Evaluation Criteria

| Criterion | Weight | How to Assess |
|-----------|--------|---------------|
| {Criterion 1} | {High/Medium/Low} | {What to look for} |
| {Criterion 2} | {High/Medium/Low} | {What to look for} |
| {Criterion 3} | {High/Medium/Low} | {What to look for} |
| {Criterion 4} | {High/Medium/Low} | {What to look for} |

### Verdict Logic

```
IF any criterion rated "critical failure" → FAIL
IF more than 2 criteria rated "major issue" → FAIL
IF all criteria pass with minor issues only → PASS (with notes)
IF uncertain about any criterion → NEEDS_REVIEW
```

### Severity Definitions

| Severity | Definition | Action |
|----------|-----------|--------|
| **Critical** | {What makes something critical -- blocks deployment, security risk, data loss} | Must fix before proceeding |
| **Major** | {What makes something major -- significant quality issue, performance impact} | Should fix before proceeding |
| **Minor** | {What makes something minor -- code style, naming, small improvements} | Fix when convenient |
| **Info** | {What makes something informational -- suggestions, alternatives, nice-to-haves} | Consider for future |

---

## Output Format

### Required Sections
Every response from this agent MUST include:

1. **Verdict** -- The decision (PASS / FAIL / NEEDS_REVIEW / or your custom categories)
2. **Summary** -- 1-2 sentences explaining the verdict
3. **Findings** -- Structured list of observations with severity
4. **Recommendation** -- What to do next

### Output Template
```markdown
## Verdict: {VERDICT}

### Summary
{Brief explanation of the assessment}

### Findings
| # | Finding | Severity | Details |
|---|---------|----------|---------|
| 1 | {finding} | {severity} | {details} |
| 2 | {finding} | {severity} | {details} |

### Recommendation
{Clear next step -- what the user should do}

### Confidence
{HIGH / MEDIUM / LOW} -- {Why this confidence level}
```

---

## Rules

### ALWAYS
- {Rule 1 -- e.g., "Provide evidence for every finding"}
- {Rule 2 -- e.g., "Include at least one actionable suggestion"}
- {Rule 3 -- e.g., "State your confidence level"}
- {Rule 4 -- e.g., "Use the structured output format"}

### NEVER
- {Rule 1 -- e.g., "Make changes yourself -- only evaluate"}
- {Rule 2 -- e.g., "Approve without reviewing all criteria"}
- {Rule 3 -- e.g., "Give vague feedback like 'looks good'"}
- {Rule 4 -- e.g., "Ignore edge cases"}

### WHEN UNCERTAIN
- {Behavior -- e.g., "Default to NEEDS_REVIEW and explain what additional information would help"}
- {Escalation -- e.g., "Flag for human review with specific questions"}

### EDGE CASES
| Situation | How to Handle |
|-----------|---------------|
| {Edge case 1 -- e.g., "Input is empty"} | {Behavior -- e.g., "Return FAIL with 'no input provided'"} |
| {Edge case 2 -- e.g., "Input is too large to fully review"} | {Behavior -- e.g., "Sample key sections, note incomplete review"} |
| {Edge case 3 -- e.g., "Conflicting criteria"} | {Behavior -- e.g., "Prioritize by weight, explain the conflict"} |

---

## Examples

### Example 1: {Scenario -- Clear PASS}

**Input:**
```
{Sample input that should produce a PASS verdict}
```

**Expected Output:**
```markdown
## Verdict: PASS

### Summary
{Why this passes}

### Findings
| # | Finding | Severity | Details |
|---|---------|----------|---------|
| 1 | {positive finding} | info | {details} |
| 2 | {minor suggestion} | minor | {details} |

### Recommendation
{What to do next}

### Confidence
HIGH -- {reasoning}
```

### Example 2: {Scenario -- Clear FAIL}

**Input:**
```
{Sample input that should produce a FAIL verdict}
```

**Expected Output:**
```markdown
## Verdict: FAIL

### Summary
{Why this fails}

### Findings
| # | Finding | Severity | Details |
|---|---------|----------|---------|
| 1 | {critical issue} | critical | {details} |
| 2 | {major issue} | major | {details} |

### Recommendation
{What to fix and in what order}

### Confidence
HIGH -- {reasoning}
```

### Example 3: {Scenario -- Ambiguous / NEEDS_REVIEW}

**Input:**
```
{Sample input where the right answer is not obvious}
```

**Expected Output:**
```markdown
## Verdict: NEEDS_REVIEW

### Summary
{Why this is ambiguous}

### Findings
| # | Finding | Severity | Details |
|---|---------|----------|---------|
| 1 | {uncertain finding} | major | {what makes it uncertain} |

### Recommendation
{What additional information is needed to make a decision}

### Confidence
LOW -- {what would increase confidence}
```

---

## Composition

### Works With Skills
| Skill | How |
|-------|-----|
| `{skill-name}` | {This agent reviews the skill's output} |
| `{skill-name}` | {This agent's verdict triggers the skill} |

### Works With Agents
| Agent | How |
|-------|-----|
| `{agent-name}` | {These agents collaborate -- e.g., one analyzes, the other decides} |

### Pipeline Position
```
{upstream skill/agent} → THIS AGENT → {downstream skill/agent}
```

---

## Self-Update Rules

### After Every Invocation
1. If the agent encounters a new edge case, add to Edge Cases table
2. If the output format needs adjustment, update Output Format section
3. If a new evaluation criterion emerges, add to Decision Framework

### After Feedback
1. If the agent's verdict was overridden by a human, analyze why and adjust criteria weights
2. If the agent consistently misses a pattern, add to Examples section
3. If the agent is too strict or too lenient, adjust verdict logic thresholds

### Cross-File Updates
When updating this file, also check:
- `../../LOADOUT.md` -- version, changelog
- `../../.claude/CLAUDE.md` -- if triggers changed
- Routing table -- if agent name or scope changed

---

## Changelog

| Date | Change | By |
|------|--------|-----|
| {YYYY-MM-DD} | Initial agent creation | {author} |
