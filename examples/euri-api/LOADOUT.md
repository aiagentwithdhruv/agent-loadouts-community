---
name: euri-api
version: 1.0.0
description: Euri AI Gateway — 24 models, 6 providers, 200K free tokens/day, OpenAI-compatible
author: AiwithDhruv
tier: free
last_verified: 2026-02-26
---

# Euri API — Agent Loadout

> Drop-in AI gateway. 24 models from Google, OpenAI, Meta, Groq, Alibaba, Together. OpenAI-compatible format. 200K free tokens/day. No credit card.

---

## Quick Reference

| Key | Value |
|-----|-------|
| **Base URL** | `https://api.euron.one/api/v1/euri` |
| **Auth** | `Authorization: Bearer <EURI_API_KEY>` |
| **Daily Limit** | 200,000 tokens (resets midnight UTC) |
| **Get API Key** | https://euron.one/euri |
| **Python SDK** | `pip install euriai` |

## Best Models

| Need | Model ID | Why |
|------|----------|-----|
| General purpose | `gemini-2.5-flash` | Best speed + quality balance |
| Complex reasoning | `gemini-2.5-pro` | 2M context, strongest reasoning |
| Fast & cheap | `gpt-4.1-nano` | Cheapest tokens, ultra-fast |
| Code generation | `gpt-4.1-mini` | Good at code tasks |
| Web search | `groq/compound` | Built-in web search |
| Embeddings | `gemini-embedding-001` | Best quality vectors |
| Images | `gemini-3-pro-image-preview` | Text-to-image |

---

## Skills

### euri-api (Build with Euri)

**When to use:** Building any project that needs AI model calls.

#### Python (euriai SDK)
```python
from euriai import EuriaiClient
client = EuriaiClient(api_key="your-key", model="gemini-2.5-flash")
response = client.generate_completion(prompt="Hello!", temperature=0.7, max_tokens=500)
print(response["choices"][0]["message"]["content"])
```

#### Python (OpenAI drop-in)
```python
from openai import OpenAI
client = OpenAI(api_key="your-euri-key", base_url="https://api.euron.one/api/v1/euri")
response = client.chat.completions.create(
    model="gemini-2.5-flash",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

#### TypeScript
```typescript
import OpenAI from 'openai';
const client = new OpenAI({
  apiKey: process.env.EURI_API_KEY,
  baseURL: 'https://api.euron.one/api/v1/euri'
});
const response = await client.chat.completions.create({
  model: 'gemini-2.5-flash',
  messages: [{ role: 'user', content: 'Hello!' }]
});
```

#### cURL
```bash
curl -X POST https://api.euron.one/api/v1/euri/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -d '{"messages": [{"role":"user","content":"Hello!"}], "model": "gemini-2.5-flash"}'
```

#### n8n (zero code)
1. Create "OpenAI" credential -> API Key = your Euri key
2. Set Base URL = `https://api.euron.one/api/v1/euri`
3. All OpenAI nodes now route through Euri

---

## Common Mistakes

| Mistake | Symptom | Fix |
|---------|---------|-----|
| Using OpenAI API key | "incorrect API key" | Use Euri key from euron.one/euri |
| Not setting base_url | Requests go to OpenAI | Set `base_url` to Euri endpoint |
| Wrong model ID | "model not found" | Copy exact ID from table above |
| Not handling response format | Content parsing fails | `content` can be string OR array `[{type:"text", text:"..."}]` |
| Hitting daily limit | 429 error after heavy use | Use cheaper models, lower max_tokens |

---

## Endpoints

| Endpoint | Purpose |
|----------|---------|
| `POST /chat/completions` | Text generation (20 models) |
| `POST /embeddings` | Vector embeddings (3 models) |
| `POST /images/generations` | Image generation (1 model) |

---

## Self-Update Rules

| Event | Update |
|-------|--------|
| New model added | Add to Best Models table |
| Model deprecated | Remove from table, add note |
| Token limit changed | Update Quick Reference |
| New endpoint | Add to Endpoints table |
| New common mistake found | Add to Common Mistakes |
