# ATLAS Configuration
_This file is the single source of truth for ATLAS settings. Update it here — never edit SKILL.md to change team names, roles, or settings._

---

## Agency
- **Name:** Big Uppetite
- **GitHub Repo:** AliBigupp/atlas-nerve-centre
- **Branch:** main

---

## Team

| Name | Role | Notes |
|------|------|-------|
| Ali | Project Manager | Escalation contact. Receives all flags and alerts. |
| Jenna | Strategist | Account lead. Receives client pulse briefings. |
| Ahmed | Technical | Delivery. Receives daily focus and blockers. |

**Assignee rule:** Use first name only on all Trello cards (Ali / Jenna / Ahmed).

---

## Programme Settings
- **Duration:** 12 weeks (84 days)
- **Escalation Contact:** Ali
- **Sentiment Escalation Threshold:** 3 consecutive cautious or negative sessions

---

## Board Structure

Lists in order (every client board uses this structure):

| List Name | Canonical State | Cards here are… |
|-----------|----------------|-----------------|
| TO DO | to_do | Not yet started |
| DOING | doing | Actively in progress |
| WAITING | waiting | Blocked on someone else |
| BLOCKED | blocked | Formally blocked — see card for BLOCKED BY |
| DONE | done | Finished — do not include in active reports |

**Done rule:** A card is done if and only if it is in the DONE list. The Trello `dueComplete` field and checklist completion status are irrelevant to done status. List position is the only source of truth.

---

## Card Quality
- **Minimum score to create:** 8 out of 10
- **Rejected below:** 7 or lower — fix and rescore before creating

---

## GitHub Folder Structure

```
atlas-nerve-centre/
├── config.md                          ← this file
├── client_registry.md                 ← all client data (programme dates, board IDs, tone profiles)
└── clients/
    └── [client-slug]/
        ├── scope-baseline.md          ← created on first session
        ├── sentiment-log.md           ← one entry per session
        └── sessions/
            └── YYYY-MM-DD.md          ← session log after every processed meeting
```

**client-slug format:** firstname-lastname, lowercase, hyphens (e.g. `steven-sahyoun`)
