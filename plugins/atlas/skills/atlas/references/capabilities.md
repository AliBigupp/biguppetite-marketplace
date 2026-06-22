# ATLAS Capabilities — Detailed Workflows

> ⚠️ **DEPRECATED — DO NOT USE AS INSTRUCTION SOURCE**
> This file is an archived reference only. It contains outdated workflows that conflict with SKILL.md v0.4.0.
> The authoritative source for all ATLAS behaviour is `SKILL.md`. If anything in this file contradicts SKILL.md, SKILL.md wins.
> This file is kept for historical context only and will be removed in a future version.

## 1. Meeting Processor

### Step 1 — Identify the Client

1. Fetch the most recent Fireflies transcript, or the one specified by the user.
2. Extract all participant email addresses from the transcript metadata.
3. Match against `client_registry.md` emails (exact match first, then fuzzy).
4. If no email match: try matching the meeting title against client names in the registry.
5. If still no match: present the user with the closest candidates and ask them to confirm before proceeding.

### Step 2 — Analyse the Transcript

Extract and categorise:

- **Action items** — who, what, by when (explicit or implied)
- **Decisions made** — anything resolved or agreed upon
- **Blockers** — dependencies, waiting-on items, external constraints
- **Scope changes or new requests** — anything not previously on the board
- **Client emotional signals** — anxiety, excitement, frustration, confidence (for tone profile)
- **At-risk signals** — missed deadlines mentioned, delays flagged, expressed frustration

### Step 3 — Update the Tone Profile

1. Retrieve the existing `tone_profile` block for this client from `client_registry.md`.
2. From the transcript, extract:
   - How does the client communicate? (direct / anxious / detail-oriented / big-picture)
   - What specific language or phrases do they use?
   - What triggers stress or reassurance for them?
   - What does Jenna's communication style look like with this client specifically?
3. Append new observations to `tone_profile` with today's date stamp. Never overwrite previous entries.

### Step 4 — Update Trello

1. Fetch the client's Trello board.
2. Discover all lists dynamically — do not assume list names.
3. For each action item:
   - Search existing cards for a matching task (check name + description). If found: update (add comment, adjust due date, reassign if needed).
   - If not found: create a new card following the card standards below.

**Card creation standards** (also in `references/card-standards.md`):

- **Name prefix (priority emoji):**
  - 🔴 Urgent
  - 🟡 Medium
  - 🟢 Strategy
  - 🔵 Admin
- **Name format:** `🔴 [ASSIGNEE] Task description — Outcome`
- **Description:** Full context, not a summary. Include:
  - Jenna's exact request (if relevant)
  - What needs to be done (numbered list)
  - Blockers and open questions
  - Reference to related cards
  - `BLOCKED BY: [Card name]` at top if applicable
- **Due date:** Extract from transcript. If not stated: Urgent = 7 days, Medium = 14 days.
- **Assignee:** Match to Ahmed / Ali / Jenna by role. If unclear, flag for user.
- **Label:** Match to priority colour.

### Step 5 — Board Health Check

Run automatically after updating. Scan for:

- Cards with no due date → flag
- Cards with no assignee → flag
- Cards in "Doing" (or equivalent in-progress list) for more than 14 days → flag as potentially stuck
- Cards that appear to be blocked by another card → note the dependency

### Step 6 — Post-Session Summary

Output the summary in this format:

```
✅ CLIENT: [Name] | Week [X] of 12
📋 CARDS CREATED: [N]
✏️ CARDS UPDATED: [N]
⚠️ FLAGS: [list any health issues or scope flags]
🧠 TONE PROFILE: [one sentence on what was added/updated]
```

---

## 2. Board Health Monitor

For each board (or the specified board):

1. Count total cards by list.
2. List overdue cards (name, list, days overdue).
3. List cards with no owner.
4. List cards with no due date.
5. List cards stuck in Doing/Review for 14+ days.
6. Assess: given the client's `programme_week`, is progress proportional?

Output format:

```
🏥 BOARD HEALTH: [Client Name]
Week [X]/12 | Status: [On Track / At Risk / Critical]

⚠️ Issues found:
- [issue 1]
- [issue 2]

📌 Recommended actions:
- [action 1]
- [action 2]
```

**Status thresholds:**
- On Track: no overdue cards, no stuck cards, progress matches week number
- At Risk: 1-3 overdue or stuck cards, minor progress lag
- Critical: 4+ overdue cards, significant progress lag, or client hasn't been active in 14+ days

---

## 3. Scope Creep Detector

During Meeting Processor, for each new request identified in the transcript:

1. Search existing Trello cards for that task.
2. If it exists → not scope creep, proceed normally.
3. If it doesn't exist → assess whether it was in the original service agreement:
   - Would it require significant extra work?
   - Is it being assumed as included but was never explicitly sold?
4. If yes → raise a scope flag before creating the card:

```
🚨 SCOPE FLAG
New request detected: "[exact quote from transcript]"
This does not appear to be in the current scope.
Recommended action: Raise with Jenna before creating the card.
Confirm to proceed? [yes / no]
```

Wait for user confirmation. Do not create the card until confirmed.

---

## 4. Tone-Aware Content

Before generating any client-facing content (card descriptions, email drafts, update messages):

1. Load the client's `tone_profile` from `client_registry.md`.
2. If empty → use neutral, professional Australian English.
3. If populated → apply the documented communication preferences:
   - Match vocabulary and register
   - Honour documented sensitivities (e.g., "this client gets anxious about timelines — lead with certainty")
   - Apply Jenna's documented style with this specific client
4. Flag when tone_profile needs updating (e.g., first session with a new client, or behaviour has shifted).

---

## 5. Dependency Mapping

During card creation:

1. Review all action items from the transcript as a set.
2. Identify logical dependencies: if Task A cannot begin until Task B is complete, note it.
3. Also check existing board cards for upstream dependencies.
4. In Card A's description: add `BLOCKED BY: [Card name or description]` as the first line.
5. Note all dependencies in the post-session summary under ⚠️ FLAGS.
