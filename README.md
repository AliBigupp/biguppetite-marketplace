# Big Uppetite Plugin Marketplace

Internal Claude plugins for the Big Uppetite team.

## Plugins

| Plugin | Description |
|--------|-------------|
| **ATLAS** | Meeting processor — Fireflies → Trello, tone profiles, scope detection |
| **PULSE** | Business intelligence — board health, risk radar, client reports |

---

## Setup for New Team Members

### Step 1 — Add the marketplace

In Claude (Cowork or Claude Code), run:

```
/plugin marketplace add AliBigupp/biguppetite-marketplace
```

### Step 2 — Install the plugins

```
/plugin install atlas@biguppetite
/plugin install pulse@biguppetite
```

### Step 3 — Set environment variables

ATLAS requires two sets of credentials. Add these to your Claude environment (Settings → Environment Variables):

**Trello:**
```
TRELLO_API_KEY=your_key_here
TRELLO_TOKEN=your_token_here
```
Get them at: https://trello.com/app-key

**GitHub (for atlas-nerve-centre):**
```
GITHUB_PERSONAL_ACCESS_TOKEN=your_pat_here
```
Create at: GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
Required scope: `repo`

### Step 4 — Connect Fireflies

Fireflies is a separate MCP connector. Connect it via Claude's connector settings. ATLAS uses it automatically once connected.

---

## Updating Plugins

When a new version is published:

```
/plugin marketplace update biguppetite
/plugin update atlas@biguppetite
/plugin update pulse@biguppetite
```

---

## Repo Structure

```
biguppetite-marketplace/
├── .claude-plugin/
│   └── marketplace.json      ← marketplace catalog
├── plugins/
│   ├── atlas/                ← ATLAS plugin
│   │   ├── .claude-plugin/plugin.json
│   │   ├── skills/atlas/SKILL.md
│   │   ├── hooks/hooks.json
│   │   ├── .mcp.json
│   │   ├── client_registry.md
│   │   └── README.md
│   └── pulse/                ← PULSE plugin
│       ├── .claude-plugin/plugin.json
│       ├── skills/pulse/SKILL.md
│       ├── hooks/hooks.json
│       └── .mcp.json
└── README.md
```

---

## Maintaining This Marketplace

- Bump `version` in `.claude-plugin/marketplace.json` AND in the plugin's own `plugin.json` to push updates to the team
- Keep the live client registry at `AliBigupp/atlas-nerve-centre` — don't edit `client_registry.md` in this repo directly
