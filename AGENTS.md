# Instructions for AI coding agents

This applies to every agent (Claude Code, Codex, Cursor, Replit Agent, etc.).

**Before doing anything, read [`README.md`](README.md).** It has the assignment (the Team App brief from bCourses), the team rules, and the API candidates. Also read `PLAN.md` (the owner's plan; never edit it) and [`TEAM-PLAN.md`](TEAM-PLAN.md) (the team plan). Then ask the human which feature they are building today.

Never break these rules:

- **Plan first.** Don't write integration code for an API that isn't in the merged `TEAM-PLAN.md`. If it's missing, help the human propose it there in a separate PR first.
- **Never commit to `main`.** Branch from the latest `main` (e.g. `api/nutrition`), commit there, and open a PR. Never merge without a teammate's approval and green CI.
- **Keys stay on the server.** Read them from environment variables. Never hard-code a key, put it in client code, commit a `.env` file, or print it in logs. The browser never calls an external API directly.
- **Every API feature saves something to the database.**
- **The test goes in the same PR as the feature.** Test what our app does with the API's answer (what it saves, calculates, shows or protects) using a mocked response. No real network calls in tests. Never delete, skip or weaken another member's test to make CI pass.
- **PR description:** what changed, `closes #N`, a screenshot, a plain-English explanation of the test, and one sentence on what would break it.
- **Save prompts:** remind the human to add the key prompts to `prompts/<feature>.md`.
