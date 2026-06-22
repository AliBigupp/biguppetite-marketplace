# ATLAS — Intelligent Project Builder

**Version:** 0.1.0  
**Author:** Big Uppetite  
**Language:** Australian English

ATLAS is the project intelligence engine for Big Uppetite. It processes Fireflies meeting transcripts, manages Trello boards, maintains client tone profiles, and keeps 12-week client programmes on track.

---

## Components

| Component | Type | Purpose |
|-----------|------|---------|
| `atlas` | Skill | Full ATLAS identity — meeting processor, board health, scope detection, tone-aware content, dependency mapping |
| `.mcp.json` | MCP | Trello + GitHub integrations |
| `client_registry.md` | Reference | Local copy only — live registry lives on GitHub at `AliBigupp/atlas-nerve-centre` |

---

## Setup

### 1. Trello API Credentials

This plugin connects to Trello via the `mcp-server-trello` npm package. You need two environment variables set in your Claude environment:

```
TRELLO_API_KEY=your_api_key_here
TRELLO_TOKEN=your_token_here
```

To get these:
1. Go to https://trello.com/app-key — copy your API key
2. Click the "Generate a Token" link on that page — copy your token

Set them in Claude's environment settings (Settings → Environment Variables).

### 2. GitHub Personal Access Token

ATLAS reads and writes the live client registry from a private GitHub repo (`AliBigupp/atlas-nerve-centre`). The PAT with `repo` scope is already baked into `.mcp.json`. To rotate it: go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic), generate a new one with `repo` scope, and update the `GITHUB_PERSONAL_ACCESS_TOKEN` value in `.mcp.json`.

### 3. Client Registry

The live registry is at `https://github.com/AliBigupp/atlas-nerve-centre/blob/main/client_registry.md`. Edit it directly on GitHub (or via ATLAS) to add clients. ATLAS fetches it fresh at the start of every session — all team members always see the same data.

Required fields per client:
- `email` — used to match Fireflies participants to clients
- `trello_board` — used to match clients to their Trello board

### 3. Fireflies

Fireflies is connected separately as a standalone MCP connector. ATLAS uses it automatically if it's connected.

---

## Usage

### Triggering ATLAS

Say any of:
- "Process the latest meeting"
- "Run the startup sequence"
- "Health check on [Client] board"
- "Check all boards"
- "Update Trello from today's call"

### After Installing

1. Edit `client_registry.md` with your active clients — replace the template with real data.
2. Set `TRELLO_API_KEY` and `TRELLO_TOKEN` environment variables.
3. Start a new session — ATLAS will load the registry and confirm readiness.

---

## File Reference

```
atlas/
├── .claude-plugin/plugin.json     # Plugin manifest
├── skills/atlas/
│   ├── SKILL.md                   # ATLAS core instructions
│   └── references/
│       ├── capabilities.md        # Detailed step-by-step workflows
│       ├── business-rules.md      # Non-negotiable operating rules
│       ├── card-standards.md      # Trello card formatting standards
│       └── team.md                # Team member roles and assignment logic
├── hooks/hooks.json               # SessionStart hook
├── .mcp.json                      # Trello MCP server config
└── client_registry.md             # Live client data (edit this)
```
