# Student Playbook

> Turn AI into your study partner — research, notes, projects, and learning on autopilot.

---

## What This Gives You

- AI organizes your coursework and deadlines
- AI does literature review for your papers
- AI helps build projects with proper structure
- AI explains complex topics in simple language
- AI tracks what you've learned and what's next

---

## Setup (5 minutes)

### Step 1: Create Your Student Context

Create `.claude/CLAUDE.md`:

```markdown
# [Your Name] — AI Study Assistant

## About Me
- Level: [Undergraduate / Graduate / Self-learning]
- Major: [Computer Science / Business / etc.]
- Current semester: [e.g., Spring 2026]
- Learning style: [Visual / Reading / Hands-on / Video]

## Current Courses
| Course | Professor | Key Topics | Grade Goal |
|--------|-----------|------------|------------|
| | | | |

## Projects
| Project | Deadline | Status | Tech Stack |
|---------|----------|--------|------------|
| | | | |

## What I Know Well
- [List your strong topics]

## What I'm Learning
- [List topics you're actively studying]

## Rules for AI
- Explain things simply first, then add technical depth
- Always cite sources when doing research
- Help me understand, don't just give me answers
- When I'm stuck, give hints before full solutions
```

### Step 2: Add Study Skills

```
my-study-loadout/
├── .claude/CLAUDE.md
├── skills/
│   ├── literature-review/SKILL.md   ← Research papers
│   ├── explain-topic/SKILL.md       ← ELI5 any concept
│   ├── project-scaffold/SKILL.md    ← Set up projects
│   └── study-plan/SKILL.md          ← Create study schedules
└── LOADOUT.md
```

### Step 3: Literature Review Skill

```markdown
# Literature Review Skill

## Trigger
When I say "research [topic]" or "find papers about [topic]"

## Execution
1. Search for recent papers and articles on the topic
2. For each source, extract:
   - Title, authors, year
   - Key findings (2-3 sentences)
   - Methodology
   - Relevance to my work
3. Organize by theme, not by date
4. Identify gaps in the research
5. Suggest how my project/paper could contribute

## Output
- Summary table of 10-15 sources
- Thematic analysis (3-4 themes)
- Research gap identification
- Suggested citations in APA format
```

---

## Study Skill Chain

```
Research Topic → Explain Simply → Create Notes → Build Project → Review & Test
```

---

## Free Tools

| Need | Tool | Cost |
|------|------|------|
| AI Assistant | Claude Code / ChatGPT | Free tier |
| Diagrams | Excalidraw / Mermaid | Free |
| Notes | Markdown files | Free |
| Code | VS Code + extensions | Free |
| Research | Google Scholar | Free |
