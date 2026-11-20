# MyCookbook
An app to track those easy weeknight recipes and stay organized with your grocery list
## Team
- @roshininarayanan-cmd
- @borisbelyavskiy-edu

---

## The assignment: Team App

*Summary of the "(H) Team App" assignment from bCourses (Intro to Coding for MBAs). The full text is on [bCourses](https://bcourses.berkeley.edu/courses/1555569/assignments/9130764); if this summary and bCourses disagree, bCourses wins.*

The team takes one member's solo app (MyCookbook, owner: `sachibajaj`) and makes it smarter with external APIs. **Each member adds one feature powered by a different API.** We work like a product team: every change is a pull request reviewed by a teammate.

**Deadline:** Wednesday, December 2, before class (4 p.m.). That day we demo the live app to the class: 5 minutes plus 1 minute of Q&A, one driver and at least one narrator, with every API shown working.

**Every API feature must:**

1. use a different API than the other members' features;
2. call the API **from the server** (the browser never talks to the external API, keys never reach the client);
3. **save something to the database** (nutrition numbers, a photo URL, a sent-email record, a generated summary…);
4. go through the reviewed workflow (no commits to `main`, a teammate approval on every PR, tests in CI);
5. work on the **live URL** by the deadline.

At most **one AI/LLM API** per group. APIs that log in as the user (OAuth: Spotify, Strava, Google Calendar) are allowed but must be flagged in the plan and cleared with the GSI first.

**What we deliver:**

| What | Details |
|---|---|
| [`TEAM-PLAN.md`](TEAM-PLAN.md) | Approved by **every member** and merged **before any feature PR**. Six sections plus an API card per API; a *Plan vs. Reality* table is added at the end (the plan itself isn't rewritten). The owner's original `PLAN.md` stays untouched. |
| `prompts/<feature>.md` | Each member's key prompts for their feature. |
| `REFLECTION.md` | Added by PR at the end. **Q1** (each member, 200–300 words): the moment your API or agent surprised you, with the prompt trail and a link to the PR or commit with the fix. **Q2** (together, 300–500 words): the two review comments that changed the code most, and what was hardest about building in someone else's app (including the owner's view). |
| CI workflow | GitHub Actions runs the whole test suite on every PR. |
| Submission (one per group) | Private repo URL (with the instructors added) and the live app URL. |

**Each member's minimums:** 2 merged PRs as author (the onboarding PR and your API feature **with its test in the same PR**) and 2 reviews with a specific comment on PRs from 2 different teammates.

**Grading (one grade for the whole group, 100 points):** API features 35 · Reflection 30 · Tests 15 · Reviews 10 · `TEAM-PLAN.md` 10.

---

## Team rules

### Setup to-do for the app owner (Sachi)

Only the repo owner can do these (repo **Settings**):

- [ ] **Make the repo private** (Settings → General → Danger Zone → Change visibility). The assignment requires a private repo, and it is public right now.
- [ ] Add every teammate as a collaborator (Settings → Collaborators).
- [ ] Add the instructors as collaborators: `joewadcan` and `prakharj282`.
- [ ] Protect `main` (Settings → Branches → Add rule for `main`): require a pull request, require 1 approval, require status checks (CI) to pass.
- [ ] Push the solo app's code and the original `PLAN.md` (check that no passwords or API keys were ever committed).
- [ ] Add the GitHub Actions workflow that runs the tests on every PR (any agent can write it once the code is in).
- [ ] Set the host to deploy automatically from `main`, and share the live URL with the team.

### Ground rules

- **Never push to `main`.** Every change goes through a pull request.
- **Every PR needs at least 1 teammate approval** and **green CI** before it is merged. You can't approve your own PR.
- **The author merges** their own PR once it is approved and the tests pass.
- **No secrets in the repo.** API keys live in environment variables (a git-ignored `.env` locally, the host's secret settings in production). If a key is ever committed, tell the team right away and rotate it.
- **APIs are called from the server only.**
- **Pull `main` often.** If you hit a merge conflict, resolve it (your agent can help) and mention it in the PR description.

### Plan first: no integration without a plan entry

Before anyone writes code for an API integration, it must be **proposed and approved in [`TEAM-PLAN.md`](TEAM-PLAN.md)**.

1. **Propose.** Open a PR that changes only `TEAM-PLAN.md` and fills in your part: your row in *Who builds what*, your API card, your database changes, your Given/When/Then test, and your *Done when*.
2. **Check the rules first:** a different API from everyone else's, at most one AI/LLM API per group, OAuth only after talking to the GSI.
3. **Get it approved.** The first version of `TEAM-PLAN.md` needs approval from **every member** and is merged before any feature PR. Later changes to your part need at least 1 teammate approval.
4. **Only then build** (next section).

**Changing course?** If you switch APIs or the feature changes a lot, update `TEAM-PLAN.md` in a PR first, then change the code.
**Reviewers:** don't approve a feature PR whose API isn't in the merged `TEAM-PLAN.md`.

### Feature workflow

1. **Issue.** Open a GitHub Issue for your feature, paste the user story from `TEAM-PLAN.md`, and assign it to yourself.
2. **Branch.** Branch from the latest `main`, named for the feature, e.g. `api/nutrition`.
3. **Build.** Build it with your agent on that branch. Save your key prompts in `prompts/<feature>.md`. Start each agent session with: *"Read PLAN.md and TEAM-PLAN.md. Today I'm building ___."*
4. **Pull request** into `main`. The description includes what changed, `closes #N`, a screenshot of the feature working, a **plain-English explanation of the test** (what it sets up, does and checks), and **what would break it** (one real change that would make the test fail).
5. **Review.** A teammate reviews. Fix what they find and push again to the same branch.
6. **Merge.** Once it is approved and CI is green, the author merges.
7. **Deploy.** The live URL stays current after every merge.

### Tests and CI

- **CI runs every test on every PR.** Red CI means no merge.
- **Each API feature ships with its test in the same PR.**
- **Test the feature, not the API.** Use a mocked API response, then check what *our app* does with it: what it saves, calculates, shows or protects. A test that only checks "the API returned something" doesn't count.
  - Weak: *the nutrition API returns calories.*
  - Strong: *Given a recipe has 4 servings and 2,000 total calories, when I view it, then it shows 500 per serving.*
  - Good places to look: duplicates, edits after the data was fetched, filters, totals and stats.
- **No real API calls in CI.** CI then needs no keys and doesn't fail because a service is slow or rate-limited.
- **If your PR breaks someone else's test, fix your PR.** Never delete, skip or weaken a teammate's test to make CI green; if you think their test is wrong, agree on it with them in the PR.
- **Run the tests locally** before you push.

### Reviews

- On the PR, click **Files changed → Review changes** and leave **at least one specific comment, question or suggestion** ("LGTM" alone doesn't count).
- Before approving a feature PR, **run its *Done when* checks** from `TEAM-PLAN.md`: the main path and the edge case.
- Check that the API is in the merged plan, the test is in the same PR, CI is green, and there are no keys in the code.

---

## API candidates

A starting point for choosing our APIs. Claim one by proposing it in `TEAM-PLAN.md`; the first merged plan entry wins. Check the current terms before you claim it: free tiers change.

### Preferred by the app owner (Sachi)

| API | Feature idea for MyCookbook | Key? | Watch out for |
|---|---|---|---|
| [Spoonacular](https://spoonacular.com/food-api/docs) | Nutrition information for a recipe (calories, macros), stored with the recipe | Free key | Small daily quota: store the result, don't refetch on every page view |
| [Unsplash](https://unsplash.com/documentation) | Add a photo to a recipe that doesn't have one | Free key | Attribution required: store and show the photographer's name and link |
| [Resend](https://resend.com/docs) | Email a grocery list or a weekly meal plan | Free key | You must verify a sending address; log each sent email in the database |

### Offered by a teammate (Henry): self-hosted AI API

Henry offered access to an AI model he runs on his own server (Qwen3.6 27B via Ollama, hosted in California). Possible features: Q&A about a recipe, recipe summaries, writing help (e.g. cleaning up instructions).

Proposed limits for a dedicated team key: 500 requests per day for the whole team; up to 8 requests per minute, **one request processed at a time**; up to 2,048 output tokens per response; access until December 10 or 17, 11:59 p.m. Pacific Time.

Before claiming it:

- It is an **AI/LLM API**, so it uses the group's only LLM slot.
- Requests are handled one at a time, so replies can be slow. Show a loading state, set a timeout, and store the generated text in the database so the demo doesn't depend on a live call.
- The key is a shared secret: server-side environment variable only, never in the code, the browser or a chat message. Henry shares it directly with whoever claims the API.
- If the server is down, the app must still work: recipes save, and the AI feature shows a clear "not available right now" message.
- Send recipe text only, no personal data (emails, names).

---

## For AI coding agents

[`AGENTS.md`](AGENTS.md) (and [`CLAUDE.md`](CLAUDE.md) for Claude Code) tells any coding agent to read this README and follow the rules above.
