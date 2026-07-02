# ATLAS — Trello Card Standards v2.0

## Priority Emoji Prefix

Every card name must begin with a **priority emoji** — not a decorative emoji. These four only:

| Emoji | Priority | Use for |
|-------|----------|---------|
| 🔴 | Urgent | Blocking progress, client-facing deadline, week-critical |
| 🟡 | Medium | Important but not blocking, 2-week window |
| 🟢 | Strategy | Planning, longer-horizon, thinking tasks |
| 🔵 | Admin | Internal coordination, housekeeping |

**Never** use any other emoji as the first character in a card name.

---

## Card Name Format

```
[PRIORITY EMOJI] [Task description that makes outcome clear]
```

- No assignee name in the title. The assignee lives in Trello's own member field, that's what it's for. A name prefix is redundant with the avatar already showing on the card.
- No em dash, no hyphen, no dash of any kind anywhere in the title. Write it as a plain clause instead.
- The task description must make the outcome obvious. Not just "write email" but "write email confirming scope so client has signed-off record".
- Max ~80 characters.

**Good examples:**
- `🔴 Build messaging hierarchy so every channel sounds like Steven`
- `🟡 Set up GHL pipeline so leads are auto-tagged on entry`
- `🟢 Map competitor positioning so we know where to play`
- `🔵 Schedule Week 6 check-in so progress is reviewed on time`

**Bad examples (do not create):**
- `Review deck` ← no emoji, no outcome
- `🌟 Write copy` ← decorative emoji, vague outcome
- `🔴 Jenna — Build messaging hierarchy` ← name prefix and dash, both banned
- `🔴 Ahmed - set up pipeline` ← hyphen used as a dash, unclear outcome

---

## Card Description Format

Keep every necessary specific — due dates, exact references, what changed, why it matters operationally. Never summarise those away. That said, apply the Real but Useful Filter (see SKILL.md, Voice & Tone Layer) to cut sentences that are factually true but don't change what the reader does — judgments about a person, restated assumptions, self-evident justifications. Every card must use this exact template:

```
WHAT WE'RE DOING
[1-2 sentences. What is this task and what prompted it? Reference the meeting or decision.]

THE OUTCOME
[1 sentence. What does "done" look like? Be specific — link, doc, conversation, deliverable.]

STEPS
1. [Step one]
2. [Step two]
3. [Step three]

WAITING ON
[Anything needed from the client or another team member before this can start. If nothing: "Nothing — clear to proceed."]

OPEN QUESTIONS
[Unresolved decisions or missing information. If none: "None."]

COMPLETION NOTE
[Assignee documents here when done: what was delivered, links, date completed.]
```

**If the card is blocked by another card, add this at the very top:**
```
⛔ BLOCKED BY: [Card name]
```

---

## Due Dates

Extract from transcript wherever possible. Default fallbacks if not stated:

| Priority | Default due |
|----------|-------------|
| 🔴 Urgent | 7 calendar days |
| 🟡 Medium | 14 calendar days |
| 🟢 Strategy | End of current programme fortnight |
| 🔵 Admin | 21 calendar days |

**Week-aware rule:** If the calculated due date falls after the programme end date (week 12 end), flag it:
```
⚠️ WEEK FLAG: This task is due in Week [X] but the programme ends after Week 12. Raise with [escalation contact from config] before creating.
```

---

## Card Quality Score (0–10)

Before committing any card, score it against this rubric. **Minimum score: 8. Do not create a card that scores 7 or below — fix it first.**

| Criterion | Points | Pass condition |
|-----------|--------|----------------|
| Priority emoji (🔴🟡🟢🔵) as first character | +2 | One of the four priority emojis, nothing else |
| No dash/hyphen anywhere in the title | +1 | Title reads as a plain clause, no em dash, no hyphen |
| Outcome clear from card name alone | +1 | A stranger reading the name understands what "done" looks like |
| WHAT WE'RE DOING section present | +1 | Not empty, not placeholder text |
| THE OUTCOME section present | +1 | Not empty, specific deliverable described |
| STEPS section has 2+ steps | +1 | At least 2 numbered steps |
| COMPLETION NOTE field present | +1 | Field exists (can be blank — that's fine) |
| Due date set | +1 | Explicit date on the card |
| Member assigned in Trello | +1 | At least one Trello member attached |

**Scoring:**
- **10/10** → Excellent — commit
- **8–9/10** → Good — commit
- **≤7/10** → Rejected — do not create. Fix all failing criteria and rescore before proceeding.

When a card fails, output:
```
🚫 CARD QUALITY FAIL — Score: [X]/10
Card: "[card name]"
Issues:
- [Missing criterion 1]
- [Missing criterion 2]
Fixing now...
```
Then fix and rescore before proceeding.

---

## Duplicate Prevention

Before creating any card, search the board for existing cards with:
- The same assignee and a similar task name
- Keywords from the action item

If a match is found: update the existing card (add comment, update due date) rather than creating a new one.

---

## Labels

Match the Trello label colour to the priority emoji:

| Emoji | Label colour |
|-------|-------------|
| 🔴 | Red |
| 🟡 | Yellow |
| 🟢 | Green |
| 🔵 | Blue |
