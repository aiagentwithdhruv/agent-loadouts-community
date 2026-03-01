# How Agents Work

> Agents are autonomous AI roles that make judgments, not just follow steps.
> This document explains the agent system: what agents are, how they differ from skills, how to create them, and when to use each.

---

## What Is an Agent?

An agent is an **autonomous AI role** with domain expertise, judgment, and decision-making authority.

Where a skill follows a recipe step-by-step, an agent reads context, evaluates it, and makes a decision. Skills are deterministic. Agents are probabilistic.

| | Skill | Agent |
|-|-------|-------|
| **Nature** | Deterministic task | Autonomous role |
| **Follows** | Exact steps | Guidelines and judgment |
| **Output** | Predictable (same input = same output) | Variable (depends on context) |
| **Decides** | Nothing -- executes only | What to do, how to respond, whether to escalate |
| **Example** | "Scrape 100 leads from Google Maps" | "Review this code and decide: PASS or FAIL" |

Think of it this way:

- A **skill** is a recipe. Anyone can follow it and get the same dish.
- An **agent** is a chef. They read the recipe, look at the ingredients, taste as they go, and adjust.

### When You Need a Skill
- The task has clear inputs and outputs
- The steps are the same every time
- No judgment is required
- Example: "Send a welcome email to this list"

### When You Need an Agent
- The task requires evaluation or analysis
- The output depends on subjective judgment
- Different inputs might require different approaches
- Example: "Review this pull request and tell me if it's safe to merge"

---

## The Architecture

```
              User Request
                   |
                   v
           +---------------+
           |   AI Agent    |     <-- The main AI (Claude, GPT, etc.)
           | (Orchestrator)|
           +---------------+
              /    |    \
             v     v     v
        +------+ +------+ +------+
        |Skill | |Skill | |Agent |    <-- Skills execute, Agents think
        |      | |      | |(sub) |
        +------+ +------+ +------+
```

The main AI agent acts as an **orchestrator**. When it receives a request:

1. It checks if a **skill** exists for the task (deterministic, fast)
2. If the task requires judgment, it delegates to a **subagent** (specialized role)
3. The subagent operates autonomously within its domain, then reports back

Subagents are like hiring a specialist. You give them a brief, they do the work, you review the result.

---

## Built-In Agents

### 1. code-reviewer

**Role:** Unbiased code review with strict PASS/FAIL verdict.

**When it activates:**
- User asks to review code, a PR, or a diff
- User wants a quality check before merging

**What it does:**
- Reads the code/diff provided
- Evaluates: correctness, security, performance, readability, edge cases
- Returns a structured verdict: PASS or FAIL
- Lists specific issues with severity (critical, major, minor, nit)

**Key behavior:**
- Never says "looks good" without checking
- Always provides at least one actionable suggestion, even on PASS
- FAIL requires at least one critical or major issue
- Does NOT fix code -- only reviews (separation of concerns)

### 2. research

**Role:** Deep research agent that gathers comprehensive information on a topic.

**When it activates:**
- User asks to research a topic, technology, market, or competitor
- User needs a report with sources and analysis

**What it does:**
- Breaks the research question into sub-questions
- Searches across available sources (web, docs, files)
- Synthesizes findings into a structured report
- Cites sources for every claim

**Key behavior:**
- Depth over breadth -- goes deep on the most relevant threads
- Distinguishes fact from opinion
- Flags conflicting information rather than picking a side
- Always includes a "Confidence" rating per finding

### 3. qa

**Role:** Quality assurance agent that generates and runs tests.

**When it activates:**
- User asks to test a feature, function, or system
- User wants test cases generated for existing code

**What it does:**
- Reads the code under test
- Generates test cases: happy path, edge cases, error cases
- Runs tests if a test framework is available
- Reports coverage and results

**Key behavior:**
- Generates tests that ACTUALLY test behavior, not just pass
- Includes edge cases that developers typically miss
- Tests negative paths (what happens with bad input)
- Does not mock away the thing being tested

### 4. email-classifier

**Role:** Categorize and prioritize emails automatically.

**When it activates:**
- User needs emails sorted, categorized, or prioritized
- User wants to triage an inbox

**What it does:**
- Reads email content (subject, body, sender)
- Classifies into categories: urgent, action-required, informational, spam, personal
- Assigns priority (high, medium, low)
- Suggests next action (reply, forward, archive, delete)

**Key behavior:**
- Reads between the lines (an email saying "whenever you get a chance" is still action-required)
- Considers sender importance (boss vs newsletter)
- Detects urgency signals (deadlines, escalation language)
- Groups related threads together

---

## How to Create a Custom Agent

### Step 1: Define the Role

Ask yourself:
- What domain does this agent operate in?
- What decisions does it need to make?
- What does its output look like?
- What should it NEVER do?

### Step 2: Write the Agent File

Create `agents/{agent-name}/AGENT.md` using the [AGENT-TEMPLATE.md](AGENT-TEMPLATE.md):

```
agents/
  my-agent/
    AGENT.md          # Role definition, prompt, behavior rules
    examples/         # Example inputs and expected outputs
```

### Step 3: Define the Prompt

The agent prompt is the core. It has these parts:

```markdown
## System Prompt

You are a {role name}. Your job is to {primary responsibility}.

### Your Expertise
- {Domain knowledge 1}
- {Domain knowledge 2}

### Your Task
Given {input description}, you must:
1. {Step 1 -- what to analyze}
2. {Step 2 -- what to evaluate}
3. {Step 3 -- what to decide}

### Output Format
{Exact format the agent must use for its response}

### Rules
- ALWAYS {critical behavior}
- NEVER {prohibited behavior}
- When uncertain, {default behavior}
```

### Step 4: Add Examples

Provide 2-3 examples of inputs and expected outputs. This grounds the agent's behavior:

```markdown
## Example 1

**Input:**
{Sample input}

**Expected Output:**
{What the agent should produce}

**Why:**
{Explanation of the reasoning}
```

### Step 5: Test with Edge Cases

The best agents are tested with adversarial inputs:
- Ambiguous inputs (where the right answer is not obvious)
- Inputs that try to override the agent's rules
- Empty or malformed inputs
- Inputs at the boundary between two categories

---

## Agent vs Skill: Decision Matrix

Use this table to decide whether you need a skill or an agent:

| Question | If Yes -> | If No -> |
|----------|-----------|----------|
| Does the task have a fixed, repeatable recipe? | Skill | Agent |
| Does the task require subjective judgment? | Agent | Skill |
| Should the same input always produce the same output? | Skill | Agent |
| Does the task involve evaluating quality? | Agent | Skill |
| Is the task a pipeline (input -> transform -> output)? | Skill | Agent |
| Does the task require reading between the lines? | Agent | Skill |
| Can you write a flowchart with no decision diamonds? | Skill | Agent |
| Does the task need to adapt to unexpected input? | Agent | Skill |

### Gray Area: Hybrid Tasks

Some tasks need both. For example:

**"Find leads and decide which ones are worth contacting"**
- Step 1: `scrape-leads` skill (deterministic: scrape the data)
- Step 2: `classify-leads` skill (deterministic: score by criteria)
- Step 3: Agent judgment (probabilistic: review edge cases, override scores, add context)

In hybrid scenarios, use skills for the deterministic parts and agents for the judgment parts.

---

## Agent Prompt Template

This is the minimal structure every agent prompt should follow:

```markdown
# Agent: {name}

## Role
You are a {role}. You specialize in {domain}.

## Context
You will receive {description of input}. You have access to {resources/knowledge}.

## Task
1. {What to analyze or evaluate}
2. {What criteria to apply}
3. {What decision to make or output to produce}

## Output Format
{Structured format -- verdict, categories, scores, report sections}

## Rules
- ALWAYS: {non-negotiable behaviors}
- NEVER: {prohibited behaviors}
- WHEN UNCERTAIN: {fallback behavior}
- EDGE CASES: {how to handle ambiguity}

## Quality Bar
{What "good" looks like for this agent's output}
```

---

## How the Orchestrator Routes to Agents

When the main AI receives a request, it follows this routing logic:

```
1. Parse the user's request

2. Check skill triggers first:
   → Does a skill match? Execute it (fast, deterministic)

3. If no skill matches, or task requires judgment:
   → Check agent routing table
   → Find the best-fit agent
   → Delegate with context

4. Agent processes and returns result

5. Orchestrator reviews agent output:
   → Passes directly to user (if confident)
   → Augments with additional context (if needed)
   → Flags for human review (if uncertain)
```

### Routing Table Format

```markdown
| User Says | Route To | Type |
|-----------|----------|------|
| "review this code" | code-reviewer | Agent |
| "scrape leads from" | scrape-leads | Skill |
| "research {topic}" | research | Agent |
| "classify these emails" | email-classifier | Agent |
| "send welcome emails" | welcome-email | Skill |
| "test this feature" | qa | Agent |
```

---

## Advanced: Agent Composition

Just like skills chain together, agents can coordinate:

### Sequential Agent Chain
```
research-agent → code-reviewer-agent → qa-agent
```
Research a topic, build a solution, review the code, then test it.

### Parallel Agent Evaluation
```
code-reviewer-agent-1 ─┐
                        ├─→ Orchestrator compares verdicts
code-reviewer-agent-2 ─┘
```
Two reviewers evaluate the same code independently. Orchestrator resolves conflicts.

### Agent-Skill Hybrid
```
scrape-leads (skill) → classify-leads (skill) → outreach-advisor (agent)
```
Deterministic pipeline feeds into an agent that makes the final judgment call on messaging strategy.

---

## Key Principles

### 1. Separation of Concerns
Agents judge. Skills execute. Never mix the two in one file.

### 2. Explicit Boundaries
Every agent has clear rules about what it does and does not do. A code-reviewer does not fix code. A research agent does not make business decisions.

### 3. Structured Output
Agent responses follow a defined format. No freeform essays. Structured output is parseable, composable, and actionable.

### 4. Fail-Safe Defaults
When an agent is uncertain, it should say so rather than guess. "I'm not confident in this assessment because..." is better than a wrong verdict.

### 5. Testable
Every agent should have examples that define correct behavior. If you cannot write examples, the agent's role is not clear enough.

---

## Summary

| Concept | What It Is |
|---------|-----------|
| **Agent** | An autonomous AI role with judgment and decision-making authority |
| **Skill** | A deterministic task with fixed steps and predictable output |
| **Subagent** | An agent delegated to by the main orchestrator |
| **Routing** | The process of matching a request to the right skill or agent |
| **Agent Prompt** | The structured instruction set that defines an agent's behavior |
| **Composition** | Chaining agents and skills together for complex workflows |

---

*Next: [AGENT-TEMPLATE.md](AGENT-TEMPLATE.md) -- Start building your own agent.*
