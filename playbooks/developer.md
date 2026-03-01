# Developer Playbook

> Turn AI into your senior engineer — code review, testing, deployment, and documentation.

---

## What This Gives You

- AI reviews your code like a senior engineer (not a yes-man)
- AI writes tests for your codebase
- AI deploys to production (AWS, Docker, CI/CD)
- AI keeps your documentation in sync
- AI debugs issues with full project context

---

## Setup (10 minutes)

### Step 1: Create Your Project Context

Create `.claude/CLAUDE.md` in your project root:

```markdown
# [Project Name] — AI Development Assistant

## Architecture
- Frontend: [React / Next.js / Vue / etc.]
- Backend: [FastAPI / Express / Django / etc.]
- Database: [PostgreSQL / MongoDB / etc.]
- Hosting: [AWS / Vercel / Railway / etc.]

## Key Files
| File | Purpose |
|------|---------|
| src/main.py | Entry point |
| src/api/ | API routes |
| src/services/ | Business logic |
| tests/ | Test files |

## Conventions
- Branch naming: [feature/xxx, fix/xxx, etc.]
- Commit style: [conventional commits / free-form]
- Test framework: [pytest / jest / etc.]
- Linter: [eslint / ruff / etc.]

## Known Issues
| Issue | Status | Priority |
|-------|--------|----------|
| | | |

## Environment
- Node version: [X]
- Python version: [X]
- Docker: [yes/no]

## Self-Update Rules
- When a new endpoint is added → update the API routes table
- When a bug is fixed → remove from Known Issues
- When architecture changes → update the Architecture section
```

### Step 2: Add Development Skills

```
my-project/
├── .claude/CLAUDE.md
├── skills/
│   ├── code-review/SKILL.md     ← Unbiased code review
│   ├── write-tests/SKILL.md     ← Generate test cases
│   ├── deploy/SKILL.md          ← Deploy to production
│   └── debug/SKILL.md           ← Debug with full context
└── LOADOUT.md
```

### Step 3: Code Review Skill

```markdown
# Code Review Skill

## Trigger
When I say "review this" or "code review" or submit a PR

## Execution
1. Read the changed files
2. Check against project conventions (from CLAUDE.md)
3. Look for:
   - Security vulnerabilities (OWASP top 10)
   - Performance issues
   - Error handling gaps
   - Missing tests
   - Convention violations
4. Give a verdict: PASS or FAIL
5. If FAIL, list specific issues with line numbers

## Rules
- Be honest — don't say "looks great" if it doesn't
- Severity levels: CRITICAL (security), HIGH (bugs), MEDIUM (style), LOW (nit)
- Only FAIL on CRITICAL or HIGH issues
- Suggest fixes, not just problems
```

---

## Agent: Code Reviewer

For autonomous code review, use an **agent** instead of a skill:

```markdown
# Code Reviewer Agent

You are a senior engineer reviewing code. You are NOT the author's friend.

## Your Job
1. Read ALL changed files
2. Understand the intent of the changes
3. Check for bugs, security issues, and design problems
4. Give a clear PASS or FAIL verdict

## Verdict Rules
- PASS: No critical or high-severity issues
- FAIL: Any critical or high-severity issue found

## Output Format
### Verdict: [PASS/FAIL]
### Issues Found: [count]
[List each issue with file, line, severity, description, suggested fix]
```

The difference: a **skill** follows exact steps. An **agent** uses judgment and adapts.

---

## Deployment Skill Example

```markdown
# Deploy Skill

## Trigger
When I say "deploy" or "ship it"

## Prerequisites
- Docker installed
- AWS CLI configured (or Vercel/Railway CLI)
- CI/CD pipeline exists (.github/workflows/deploy.yml)

## Execution
1. Run tests: `npm test` or `pytest`
2. If tests pass → build Docker image
3. Push to container registry
4. Deploy to production
5. Verify health check responds
6. Report success/failure

## Rollback
If deployment fails:
1. Check logs for errors
2. Roll back to previous version
3. Report the failure with error details
```
