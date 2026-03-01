# Content Creator Playbook

> Turn AI into your content team — research, scripts, thumbnails, editing, and publishing.

---

## What This Gives You

- AI finds viral content ideas in your niche
- AI writes video scripts and titles
- AI generates thumbnail concepts
- AI edits videos (silence removal, transitions)
- AI manages your content calendar

---

## Setup (15 minutes)

### Step 1: Create Your Content Context

Create `.claude/CLAUDE.md`:

```markdown
# [Channel Name] — AI Content Assistant

## My Channel
- Platform: [YouTube / TikTok / Blog / All]
- Niche: [e.g., "AI automation tutorials"]
- Subscribers: [Current count]
- Upload schedule: [e.g., "2x/week, Tue and Fri"]

## My Style
- Video length: [8-12 min / 60 sec shorts / both]
- Tone: [Educational + entertaining / Pure tutorial / Storytelling]
- Signature phrases: [Things you always say]
- Never do: [What to avoid]

## What Performs Best
| Video | Views | Why It Worked |
|-------|-------|--------------|
| [Title] | [X] | [Reason] |
| [Title] | [X] | [Reason] |

## Competitors
| Channel | Subscribers | What They Do Well |
|---------|------------|-------------------|
| [Name] | [X] | [Strength] |

## Content Calendar
| Date | Topic | Status |
|------|-------|--------|
| | | |
```

### Step 2: Content Pipeline

```
content-loadout/
├── .claude/CLAUDE.md
├── skills/
│   ├── find-outliers/SKILL.md       ← Research viral content
│   ├── generate-titles/SKILL.md     ← A/B test title variants
│   ├── write-script/SKILL.md        ← Full video scripts
│   ├── thumbnail-concept/SKILL.md   ← Thumbnail ideas + prompts
│   └── edit-video/SKILL.md          ← Silence removal, transitions
└── LOADOUT.md
```

### Step 3: Research Skill Example

```markdown
# Find Outliers Skill

## Trigger
When I say "find viral ideas" or "what should I make next"

## Execution
1. Search YouTube for videos in my niche from the last 30 days
2. Find outliers: videos that got 10x more views than channel average
3. For each outlier, extract:
   - Title pattern (what made it clickable)
   - Hook (first 30 seconds)
   - Format (tutorial, reaction, comparison, etc.)
   - Why it went viral (controversy, trend, curiosity gap)
4. Cross-reference with my past performance
5. Suggest 5 video ideas adapted to MY style

## Output
- Table of outlier videos with analysis
- 5 video ideas ranked by potential
- Title + thumbnail concept for top idea
```

---

## Content Pipeline Chain

```
Find Outliers → Generate Titles → Write Script → Thumbnail Concept → Edit Video
```

Each step feeds the next. Start with research, end with a published video.

---

## Free Tools to Use

| Task | Free Tool | Notes |
|------|-----------|-------|
| Image generation | Flux (free tier) | For thumbnail mockups |
| Diagrams | Excalidraw | Architecture diagrams, free |
| Mermaid | GitHub README | Auto-renders, free |
| Video editing | FFmpeg | Silence removal, free |
| Research | YouTube API | 10K free units/day |
