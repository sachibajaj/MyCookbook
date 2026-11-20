# Context for AI coding agents

Read this file before doing anything in this repo. It applies to every agent (Claude Code, Codex, Cursor, Replit Agent, etc.).

## What this project is

MyCookbook is an app for tracking easy weeknight recipes and keeping a grocery list. A team of classmates is extending it for the **Team App** assignment of the Haas course *Intro to Coding for MBAs*.

- **Full assignment (source of truth):** [`docs/assignment/team-app-assignment.pdf`](docs/assignment/team-app-assignment.pdf). If this file and the PDF disagree, the PDF wins.
- **Team rules:** [`CONTRIBUTING.md`](CONTRIBUTING.md).
- **Owner's plan:** `PLAN.md` (don't edit it). **Team plan:** `TEAM-PLAN.md`.
- **App owner:** `sachibajaj` (owner of this repo).

## The assignment in short

The team takes one member's solo app and makes it smarter with external APIs. **Each member adds one feature powered by a different API.** All work happens in this shared repo the way a product team works: every change is a reviewed pull request.

**Deadline:** Wednesday, December 2, before class (4 p.m.). That day the team demos the live app to the class (5 minutes plus 1 minute of Q&A, with every API shown working).

### Hard requirements for every API feature

1. One API feature per member, each with a different API.
2. The API is **called from the server**. The browser never talks to the external API directly, and API keys never reach the client.
3. The feature **stores something in the database** (e.g. nutrition numbers, a photo URL, a sent-email record, a generated summary).
4. It goes through the reviewed workflow: no commits to `main`, a teammate approval on every PR, tests in CI.
5. It works on the **live URL** by the deadline.

At most **one AI/LLM API** per group. APIs that log in as the user (OAuth) are allowed but must be flagged in the team plan and cleared with the GSI first.

### Files the team must produce

| File | What it is |
|---|---|
| `TEAM-PLAN.md` | Merged (approved by every member) **before any feature PR**. Six sections: Pitch, Who builds what, APIs (with an API card per API), Database changes, Tests (Given/When/Then), Done when. At the end, a *Plan vs. Reality* table is added (the plan itself isn't rewritten). |
| `prompts/<feature>.md` | Each member's key prompts for their feature. |
| `REFLECTION.md` | Added by PR at the end: each member's own story of building on an API (with the prompt trail and the PR/commit links), plus a joint section on reviews that mattered and building in someone else's code. |
| GitHub Actions workflow | Runs the whole test suite on every PR. |

### Per-member minimums

- 2 merged PRs as author: the onboarding PR (name in the README Team section) and the API feature **with its test in the same PR**.
- 2 reviews, each with a specific comment, on PRs by 2 different teammates.

### How it is graded (one grade for the whole team)

API features 35, Reflection 30, Tests 15, Reviews 10, `TEAM-PLAN.md` 10.

## How to work in this repo (agent checklist)

- **Start of every session:** read `PLAN.md`, `TEAM-PLAN.md`, `CONTRIBUTING.md` and this file. Ask the human which feature they are building today.
- **Plan first.** Don't write integration code for an API that isn't in the merged `TEAM-PLAN.md`. If it's missing, help the human propose it there in a separate PR first.
- **Branch, never `main`.** Branch from the latest `main` (e.g. `api/nutrition`), commit there, open a PR. Never push to `main` and never merge without a teammate's approval and green CI.
- **Keys:** read them from environment variables on the server. Never hard-code a key, put it in client code, commit a `.env` file, or print it in logs.
- **Tests:** write at least one test for the feature in the same PR. Test what *our app* does with the API's answer (what it saves, calculates, shows or protects) using a mocked response. No real network calls in tests. Never delete, skip or weaken another member's test to make CI pass.
- **PR description:** what changed, `closes #N`, a screenshot, a plain-English explanation of the test, and one sentence on what would break it.
- **Save prompts:** remind the human to add the key prompts to `prompts/<feature>.md`.
- **Pull `main` often** and resolve conflicts carefully; mention any conflict in the PR description.
