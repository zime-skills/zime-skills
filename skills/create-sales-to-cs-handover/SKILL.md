---
name: create-sales-to-cs-handover
description: "Builds the Sales to CS handover doc for one deal or account. Covers stakeholders, why we won, open objections, commitments, and call history. Gives you the handover as markdown, ready to paste into a doc."
license: MIT
metadata:
  zime:skill-id: 0e82dc75-cffd-449c-b45f-ba8b00f94ea1
  zime:tag: workflow
  zime:roles: ae,cs
  zime:visibility: global
  zime:skill-version: "1"
  zime:marketplace-version: 0.1.20
---

# Sales → CS Handover

Before anything else, call the Zime connector tool `skill_used` with skill_id `0e82dc75-cffd-449c-b45f-ba8b00f94ea1`, skill_version `1` and skill_slug `create-sales-to-cs-handover`. It records which skill ran for Zime usage analytics. If the Zime connector is not available, skip this step and continue.

Fills the handover document CS uses to accept an account. Two kinds of field
live in it, and the difference is the whole skill:

1. **Fields Zime data can fill** — stakeholders, why we won, objections,
   commitments, call history, current state.
2. **Fields only the rep knows** — NDA links, drive folders, demo slots,
   client sensitivities, what not to say.

Category 2 is left as an explicit `[SALES TO FILL]` prompt. Never guessed.

## Why guessing is worse than blank here

CS accepts or rejects a handover based on this document. An invented client
sensitivity ("don't mention pricing") gets treated as real and changes how CS
talks to the customer. A blank field gets chased and filled. The template's own
rule is that CS pushes the start date rather than accepting an incomplete
handover — so a plausible-looking fabrication defeats the control the document
exists to provide.

## How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                   SALES → CS HANDOVER                            │
├─────────────────────────────────────────────────────────────────┤
│  STEP 1 — RESOLVE                                                │
│  ✓ list_deals (deal handover) or list_accounts (account)         │
├─────────────────────────────────────────────────────────────────┤
│  STEP 2 — GATHER                                                 │
│  + ask_zime — why we won, objections, commitments          │
│  + list_meetings — call history, cadence, last engagement        │
├─────────────────────────────────────────────────────────────────┤
│  STEP 3 — FILL, DON'T GUESS                                      │
│  ✓ Zime-backed fields filled with evidence + dates               │
│  ! Rep-only fields left as [SALES TO FILL]                       │
│  ✓ Open gaps listed at the top so CS sees them first             │
├─────────────────────────────────────────────────────────────────┤
│  STEP 4 — DELIVER                                                │
│  ✓ Hand back the filled handover as markdown, ready to paste     │
├─────────────────────────────────────────────────────────────────┤
│  LOCAL FALLBACK (no zime-mcp)                                    │
│  ~ Narrower draft from provided transcripts or CRM export        │
└─────────────────────────────────────────────────────────────────┘
```

## Usage

```
@create-sales-to-cs-handover <deal or account name>
```

In the ChatGPT desktop app you can also type `/create-sales-to-cs-handover`.

Build the handover for the deal or account the user named.

## Routing

- Deal strategy while still selling, or the account's CRM record alone →
  `review-account`.
- Just the open commitments → `actions-commitments`.
- An account review deck for a QBR → `create-sales-asset`.

## What I Need From You

The deal or account name. Also useful, and otherwise left blank:

- Who's handing over, and to whom
- Anything sensitive CS must not say or do
- Links (drive folder, NDA, charter) if you have them

Anything not supplied comes back as a `[SALES TO FILL]` prompt — that's the
design, not a shortfall.

## MCP mode (required when zime-mcp is connected)

**Required tools:** `list_deals` / `list_accounts` (resolve), `ask_zime`
(evidence), `list_meetings` (call history).

### Step 1 — resolve

```json
{ "query": "Acme" }
```

`multiple_matches` → show candidates, ask, pin. A handover written about the
wrong account is worse than none.

### Step 2 — gather, asking for dates and names

Name the deal or account in the question itself, since `ask_zime` has no
separate deal/account scoping argument:

```json
{ "question": "For the Acme deal: who are the stakeholders and what does each one care about, why did we win, what objections or blockers are still live, and what did we commit to delivering? Give the evidence, the speaker, and the date for each." }
```

Call history:

```json
{ "query": "Acme", "start_date": "2026-02-01", "end_date": "2026-08-13" }
```

Ask for speaker and date explicitly — a stakeholder motivation with no source
can't be validated by CS.

### Outcomes

Usual shapes — `resolved` / `multiple_matches` / `no_match`, or
`{"error": "<CODE>", "message": "<sentence>"}` (show the user the message;
`INTERNAL_ERROR` retry once; `TIMEOUT` narrow and retry; `CREDIT_LIMIT` stop
and relay the message; `UNAUTHORIZED` / `FORBIDDEN` means reconnect or lack
of access). A failed or empty evidence call means that section becomes a
`[SALES TO FILL]` prompt — it does not become a guess.

## Output

Follow [references/handover-template.md](references/handover-template.md) for
the full field list. Structure:

```markdown
# Sales → CS Handover: [Account]
_Drafted from Zime call and CRM data on [date]. Sections marked
[SALES TO FILL] need the rep before CS can accept._

## Open gaps — blocking acceptance
- [ ] [field] — [SALES TO FILL]

## 1. Deal and commercial status
| Field | Value | Source |
|---|---|---|
| Deal | [name] · [stage] · [amount] | CRM |
| Close date | [date] | CRM |
| NDA / charter links | [SALES TO FILL] | — |

## 2. Client context
[what they do, team shape, tooling — evidence + date, or SALES TO FILL]

## 3. Stakeholders
| Name | Title | Role | What they care about | Source |
|---|---|---|---|---|
| [name] | [title] | [champion / DM / economic buyer] | [motivation] | [call, date] |

## 4. Why we won
- **[hook]** — [evidence] — [speaker, date]

## 5. Objections and blockers still live
| Objection | Raised by | Date | Status |
|---|---|---|---|

## 6. Commitments made
| Commitment | Owner | Due | Source |
|---|---|---|---|

## 7. Call history
| Date | Meeting | Type | Attendees |
|---|---|---|---|

**Last engagement:** [date] · **Cadence:** [observed pattern]

## 8. Marching orders for CS
[first actions, from what the calls indicate]

## 9. What NOT to do — client sensitivities
[SALES TO FILL] — not inferable from call data

## 10. Open questions for CS to chase
- [unresolved item] — [source]
```

Present the finished handover as plain markdown: short sections with labelled
lines, status written as words (at risk, needs attention, on track), any
commentary in the chat around it, and gaps kept visible as "not stated" or
`[SALES TO FILL]`.

## Deliver

Hand back the filled-in markdown above as the finished handover, ready for
the user to paste into Docs or another editor and share with CS. Say plainly
that the paste is a manual step, so the user knows it's needed.

### Rules

- **`[SALES TO FILL]` is mandatory** for: NDA and charter links, drive folder,
  demo/kickoff slots, client sensitivities, what-not-to-say, post-POC
  commercial terms. Never infer these — none are reliably in call data.
- **Every Zime-filled row carries a source** (call + date). CS validates the
  handover; unsourced claims can't be validated.
- **Lead with Open gaps.** CS reads that first and knows immediately whether
  this handover is acceptable.
- **A stakeholder needs a real source.** No inferring a champion from who
  talked most.
- **Never invent an owner or a due date** on a commitment. "not stated" is
  correct.
- If the account has almost no call history, say so plainly at the top — a
  thin handover honestly labelled is useful; a padded one is not.

## Tips

1. **Supply the links up front** — they're the most common blockers to
   acceptance.
2. **Sensitivities are yours to write** — the calls rarely contain them and
   guessing them is the most dangerous fabrication in this document.
3. **Widen the call-history window** — handovers want the whole relationship,
   not the last 90 days.
4. **Chase the gaps with `actions-commitments`** before handing over.

## Local mode (only when no zime-mcp server is connected)

If the user provides transcripts or a CRM export, draft from those files only.
Open with one line saying the draft covers only the provided files, so
stakeholder motivations and objections from other calls are missing by
construction. Expand `[SALES TO FILL]` to cover everything the files don't
carry.

## What this sends where

MCP mode sends query words (to `list_deals`/`list_accounts`), the evidence
question naming the deal or account (to `ask_zime`), and query words
plus dates (to `list_meetings`). Local mode reads only the provided files.
At the start, the skill calls the Zime connector tool `skill_used`, which
records the skill's id, version and name with your user and session in
Zime's usage log.

## Related Skills

- **actions-commitments** — close the gaps before handing over
- **review-account** — the pre-handover view of the same deal
- **create-sales-asset** — the account review deck CS will run later
