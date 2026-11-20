# Team Plan: MyCookbook

> **How to use this file.** It's a template: replace every `___` and `TBD`. Each member fills in their own rows and API card through a PR (see *Plan first* in the [README](README.md)). The first full version must be **approved by every member** and merged **before any feature PR**. Don't edit the owner's `PLAN.md`; this is a separate file.

## 1. Pitch

*One paragraph:* We're adding ___ to MyCookbook so that ___.

## 2. Who builds what

| Member (GitHub) | API | Feature as a user story | Est. hours |
|---|---|---|---|
| `sachibajaj` (app owner) | TBD | As a ___, I want ___, so that ___. | TBD |
| `roshininarayanan-cmd` | TBD | As a ___, I want ___, so that ___. | TBD |
| `borisbelyavskiy-edu` | TBD | As a ___, I want ___, so that ___. | TBD |
| Henry (`___`) | TBD | As a ___, I want ___, so that ___. | TBD |

Rules: a different API per member; at most one AI/LLM API in the group; OAuth APIs only after talking to the GSI (flag them here).

## 3. APIs

One API card per member: a one-minute vendor review of the service we're about to depend on. Candidates are listed in the [README](README.md#api-candidates).

### API card: ___ (owner: ___)

| Field | Answer |
|---|---|
| API and link to its docs | ___ |
| What it gives us | ___ |
| Key needed? | Yes / No |
| Free limit | ___ |
| Cost at 1,000 users | ___ |
| What we store vs. fetch fresh | ___ |
| If it disappeared tomorrow | ___ |

*How we use it:* which server route calls it, when, and with what input.

<!-- Copy the card above once per member. -->

## 4. Database changes

New tables or columns each feature needs, with types.

| Feature (owner) | Table | Column | Type | Notes |
|---|---|---|---|---|
| ___ | ___ | ___ | ___ | ___ |

## 5. Tests

One test per member, about the feature (not the API), written as *Given ___, when ___, then ___*.

| Member | Test |
|---|---|
| ___ | Given ___, when ___, then ___. |

## 6. Done when

What the reviewer checks before approving each feature.

| Feature (owner) | Main path | One edge case |
|---|---|---|
| ___ | ___ | ___ |

---

## Plan vs. Reality

*Filled in at the end. Don't rewrite the plan above; just complete this table.*

| Member | API feature | Shipped / Changed / Cut | Est. hrs | Actual hrs | Reviews given | What changed and why (one line) |
|---|---|---|---|---|---|---|
| ___ | ___ | ___ | ___ | ___ | ___ | ___ |
