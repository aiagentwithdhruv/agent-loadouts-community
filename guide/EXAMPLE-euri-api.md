# Real Example: Euri API Loadout
### See how a loadout works in practice

---

## The Scenario

You're a student working with the Euri API. You want your AI (Claude, Cursor, ChatGPT) to help you build projects with it — without explaining what Euri is every single time.

## Without a Loadout (Level 1)

Every conversation:
```
You: "I'm using Euri API, it's an AI gateway by Euron,
      the base URL is https://api.euron.one/api/v1/euri,
      I have 200K tokens per day, it's OpenAI compatible,
      here are the models I can use: gemini-2.5-flash,
      gpt-4.1-nano... [5 minutes of explaining]

      Now help me build a chatbot."

AI: "Sure! Let me help you build a chatbot with Euri API..."
```

**Every. Single. Time.** 5 minutes wasted before you even start.

## With a Loadout (Level 5)

```
You: "Build a chatbot using Euri."

AI: [Already knows the base URL, your API key location,
     all 24 models, which one to pick for chatbots,
     the TypeScript client code, common pitfalls]

     "I'll use gemini-2.5-flash for the chatbot since it's
     the best balance of speed and quality. Here's the code..."
```

**Zero explanation needed. AI starts building immediately.**

---

## The Files

Here's the exact loadout structure:

### 1. CONTEXT.md — What the AI Needs to Know

```markdown
# Euri API — AI Context

## What This Is
Euri is a unified AI gateway on the Euron platform.
OpenAI-compatible format, 24 models across 6 providers,
200K free tokens/day. Works as drop-in replacement for OpenAI SDK.

## Quick Reference
- Base URL: https://api.euron.one/api/v1/euri
- Auth: Authorization: Bearer <EURI_API_KEY>
- Daily limit: 200,000 tokens (resets midnight UTC)

## Best Models to Use
| Need | Model |
|------|-------|
| General | gemini-2.5-flash |
| Smart | gemini-2.5-pro |
| Cheap | gpt-4.1-nano |
| Images | gemini-3-pro-image-preview |

## Common Confusion
- Students use OpenAI key instead of Euri key → ERROR
- Students use OpenAI model names instead of Euri model IDs → ERROR
- Response content can be string OR array → Handle both
```

### 2. Skill: student-support/SKILL.md — How to Answer Doubts

```markdown
# Skill: student-support

## When to Use
- Student gets "incorrect API key" error
- Student confused about OpenAI vs Euri
- Student asks which model to use

## Reply Templates

### API Key Error
"Use your **Euri API key** (not OpenAI).
Set base URL to https://api.euron.one/api/v1/euri.
Use model IDs from Euri dashboard, not OpenAI names."

### Which Model?
"For general use: gemini-2.5-flash
For reasoning: gemini-2.5-pro
For speed: gpt-4.1-nano"

### Quick One-Liner
"Euri key + Euri model ID + base URL
https://api.euron.one/api/v1/euri. That's it."
```

### 3. Skill: euri-api/SKILL.md — How to Build With Euri

```markdown
# Skill: euri-api

## When to Use
- Building any project that calls an AI model via Euri
- Integrating Euri into Node.js, Python, or n8n

## Recipes

### Python (fastest)
pip install euriai
from euriai import EuriaiClient
client = EuriaiClient(api_key="key", model="gemini-2.5-flash")

### Python (OpenAI drop-in)
from openai import OpenAI
client = OpenAI(api_key="euri-key",
                base_url="https://api.euron.one/api/v1/euri")

### n8n (zero code)
1. Create OpenAI credential → API Key = Euri key
2. Set Base URL = https://api.euron.one/api/v1/euri
3. Done. All OpenAI nodes work with Euri.

## Common Mistakes
| Mistake | Fix |
|---------|-----|
| Using OpenAI key | Use Euri key from euron.one/euri |
| Not setting base_url | Must point to Euri, not OpenAI |
| Wrong model ID | Copy exact ID from Euri dashboard |
```

---

## The Result

| Metric | Without Loadout | With Loadout |
|--------|----------------|-------------|
| Time to first useful output | 5-10 min | 10 seconds |
| AI accuracy on first try | ~60% | ~95% |
| Need to correct AI | Constantly | Rarely |
| Scales to new tasks | No | Yes (add more skills) |
| Gets better over time | No | Yes (self-improving) |

---

## Try It Yourself

1. Copy the CONTEXT.md above into your Euri project
2. Start a new AI conversation
3. Ask it to "build a chatbot using Euri"
4. Watch the difference

**The AI already knows everything. You just loaded the gun.**

---

*From the [AI Loadout Guide](README.md) by [AiwithDhruv](https://github.com/aiagentwithdhruv)*
