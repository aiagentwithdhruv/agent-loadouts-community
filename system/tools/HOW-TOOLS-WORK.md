# Tools — Infrastructure That Powers Your AI System

## What Are Tools?

Tools are the **infrastructure layer** — scripts and servers that let your AI system interact with the real world. While skills tell AI *what* to do, tools give AI *how* to do it programmatically.

---

## The 5 Core Tools

### 1. MCP Server (Model Context Protocol)

An MCP server exposes your loadout system as **tools that AI can call directly**.

Instead of AI reading files manually, it calls:
- `list_loadouts()` → get all available loadouts
- `get_skill("scrape-leads")` → load a specific skill
- `search_skills("email")` → find skills by keyword
- `route_task("I need to generate leads")` → AI picks the right skill

**How to set up:**

```json
// Claude Desktop or Cursor config
{
  "mcpServers": {
    "AgentLoadout": {
      "command": "python3",
      "args": ["path/to/loadout_mcp.py"],
      "env": {
        "LOADOUT_WORKSPACE": "/path/to/your/workspace"
      }
    }
  }
}
```

**Why it matters:** Without MCP, AI has to `cat` files and parse them. With MCP, AI calls structured tools and gets typed responses. 10x faster, zero errors.

---

### 2. CLI (Command Line Interface)

A CLI tool for humans to manage loadouts directly:

```bash
# List all loadouts
python3 tools/loadout_cli.py list

# Verify a loadout is complete
python3 tools/loadout_cli.py verify ./my-project/

# Search for skills by keyword
python3 tools/loadout_cli.py search "email"

# Show a skill's typed schema
python3 tools/loadout_cli.py schema scrape-leads

# Show composition chains
python3 tools/loadout_cli.py chains

# Full health check
python3 tools/loadout_cli.py doctor
```

---

### 3. Staleness Checker

Context goes stale. Pricing changes, competitors launch new products, team members leave. The staleness checker scans your loadouts and flags what needs updating.

```bash
# Check all loadouts for staleness
python3 tools/check_staleness.py

# Output as JSON (for automation)
python3 tools/check_staleness.py --json

# Auto-fix simple issues
python3 tools/check_staleness.py --fix

# Send alerts via Telegram
python3 tools/check_staleness.py --notify
```

**What it checks:**
- LOADOUT.md has a `last_verified` date
- Last verified date is not older than the configured threshold
- All referenced files actually exist
- Required sections are present

---

### 4. Schema Registry

Every skill has a **typed schema** — inputs, outputs, credentials, cost, and what other skills it composes with. The registry is a single JSON file that makes all skills machine-readable.

```json
{
  "scrape-leads": {
    "category": "lead-generation",
    "inputs": [
      { "name": "search_query", "type": "string", "required": true },
      { "name": "max_results", "type": "integer", "default": 100 }
    ],
    "outputs": [
      { "name": "leads_csv", "type": "file", "format": "csv" }
    ],
    "credentials": ["APIFY_TOKEN"],
    "composable_with": ["classify-leads", "casualize-names"],
    "cost_per_run": "$0.05-0.50"
  }
}
```

**Why schemas matter:**
- AI can validate inputs before running a skill
- AI can chain skills together automatically (output of one → input of next)
- Humans can browse all skills without reading every SKILL.md

---

### 5. Schema Updater (Batch Tool)

When you create new skills, this tool adds typed Schema sections to all SKILL.md files:

```bash
# Preview what would change
python3 tools/add_schemas_to_skills.py

# Actually apply changes
python3 tools/add_schemas_to_skills.py --apply
```

---

## Building Your Own Tools

### MCP Server Template

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("MyLoadout")

@mcp.tool()
def list_skills() -> str:
    """List all available skills."""
    # Read your skills directory
    # Return formatted list
    pass

@mcp.tool()
def get_skill(name: str) -> str:
    """Load a specific skill by name."""
    # Read SKILL.md
    # Return content
    pass

if __name__ == "__main__":
    mcp.run(transport="stdio")
```

### CLI Template

```python
import argparse
import os

def list_cmd(args):
    """List all loadouts."""
    for item in os.listdir(args.workspace):
        loadout = os.path.join(args.workspace, item, "LOADOUT.md")
        if os.path.exists(loadout):
            print(f"  {item}")

parser = argparse.ArgumentParser(description="Loadout Manager")
sub = parser.add_subparsers()

list_p = sub.add_parser("list")
list_p.set_defaults(func=list_cmd)

args = parser.parse_args()
args.func(args)
```

---

## When to Use Each Tool

| Situation | Use |
|-----------|-----|
| AI needs to find/load skills automatically | MCP Server |
| You want to manage loadouts from terminal | CLI |
| You want to keep context fresh | Staleness Checker |
| You're building skill pipelines | Schema Registry |
| You just created 10 new skills | Schema Updater |

---

## Installation

```bash
# Install MCP dependency
pip install "mcp[cli]"

# That's it. All tools are plain Python scripts.
```
