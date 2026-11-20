# How we work on MyCookbook

These are our team rules for the Team App project. They follow the course brief: every change is reviewed by a teammate, tests run in CI, and nothing reaches `main` without a pull request.

## 1. Ground rules

- **Never push to `main`.** Every change goes through a pull request (PR).
- **Every PR needs at least 1 teammate approval** and **green CI** before it is merged. You can't approve your own PR.
- **The author merges** their own PR once it is approved and the tests pass.
- **No secrets in the repo.** API keys live in environment variables (a local `.env` that is git-ignored, plus the host's secret settings). If a key is ever committed, tell the team right away and rotate the key.
- **APIs are called from the server only.** The browser never talks to an external API directly.
- **Pull `main` often.** Four people are changing one app. If you hit a merge conflict, resolve it (your agent can help) and mention it in the PR description.

## 2. Plan first: no integration without a plan entry

Before anyone writes code for an API integration, the integration must be **proposed and approved in [`TEAM-PLAN.md`](TEAM-PLAN.md)**. Leave the owner's original `PLAN.md` alone; `TEAM-PLAN.md` is the team's file.

1. **Propose.** Open a PR that changes only `TEAM-PLAN.md` and adds your part:
   - your row in *Who builds what*: the API, the feature as a user story ("As a ___, I want ___, so that ___") and estimated hours;
   - your **API card**: docs link, what it gives us, key needed?, free limit, cost at 1,000 users, what we store vs. fetch fresh, what happens if it disappeared tomorrow;
   - the **database changes** your feature needs (tables or columns, with types);
   - your **test** written as "Given ___, when ___, then ___";
   - **Done when**: the main path and one edge case.
2. **Check against the team rules** before proposing:
   - each member uses a **different** API (check the plan first);
   - **at most one AI/LLM API** (OpenAI, Gemini, etc.) per group;
   - APIs that log in as the user (OAuth: Spotify, Strava, Google Calendar) are "hard mode": flag them in the plan and talk to the GSI first.
3. **Get it approved.** The first version of `TEAM-PLAN.md` must be approved by **every member** and merged before any feature PR. Later changes to your part need at least 1 teammate approval.
4. **Only then build.** Open the feature Issue and branch (section 3) after your plan entry is merged.

**Changing course?** If you switch APIs or the feature changes a lot, update `TEAM-PLAN.md` in a PR first, then change the code. Don't rewrite history in the plan: at the end we add a *Plan vs. Reality* table instead.

**Reviewers:** don't approve a feature PR whose API isn't in the merged `TEAM-PLAN.md`.

## 3. Feature workflow

1. **Issue.** Open a GitHub Issue for your feature, paste the user story from `TEAM-PLAN.md`, and assign it to yourself.
2. **Branch.** Branch from the latest `main`, named for the feature, e.g. `api/nutrition`.
3. **Build.** Build it with your agent on that branch. Save your key prompts in `prompts/<feature>.md`. Start each agent session with: *"Read PLAN.md and TEAM-PLAN.md. Today I'm building ___."*
4. **Pull request.** Open a PR into `main`. The description includes:
   - what changed;
   - `closes #N`;
   - a screenshot of the feature working;
   - **Plain-English test explanation**: what the test sets up, does, and checks;
   - **What would break it**: one real change that would make the test fail.
5. **Review.** A teammate reviews (section 5). Fix what they find and push again to the same branch.
6. **Merge.** Once it is approved and CI is green, the author merges.
7. **Deploy.** The live URL must stay current after every merge (auto-deploy from `main`, or the owner deploys).

## 4. Tests and CI

- **CI runs every test on every PR.** A GitHub Actions workflow runs the whole test suite on each pull request. A PR with red CI is not merged.
- **Each API feature ships with its test in the same PR.** No "tests later" PRs.
- **Test the feature, not the API.** Assume the API answered correctly (use a mocked or fixed response), then check what *our app* does with it: what it saves, calculates, shows, or protects. A test that only checks "the API returned something" doesn't count.
  - Weak: *the nutrition API returns calories.*
  - Strong: *Given a recipe has 4 servings and 2,000 total calories, when I view it, then it shows 500 per serving.*
  - Good places to look: duplicates, edits after the data was fetched, filters, totals and stats.
- **No real API calls in CI.** Tests use mocked responses, so CI needs no API keys and doesn't fail because a service is slow or rate-limited.
- **If your PR breaks someone else's test, fix your PR.** Never delete, skip, or weaken a teammate's test to get CI green. If you think their test is wrong, raise it in the PR and agree on it with them.
- **Run the tests locally** before you push.

## 5. Reviews

- On the PR, click **Files changed → Review changes** and leave **at least one specific comment, question, or suggestion** ("LGTM" alone doesn't count).
- Before approving a feature PR, **run its *Done when* checks**: the main path and the edge case from `TEAM-PLAN.md`.
- Check that the API is in the merged plan, the test is in the same PR, CI is green, and no keys are in the code.
- Each member gives **2+ reviews on 2 different teammates' PRs**.

## 6. API candidates

A starting point for choosing our APIs. Claim one by proposing it in `TEAM-PLAN.md` (section 2); the first merged plan entry wins. Before you claim one, check its current terms and fill in the full API card: free tiers change.

### Preferred by the app owner (Sachi)

| API | Feature idea for MyCookbook | Key? | Watch out for |
|---|---|---|---|
| [Spoonacular](https://spoonacular.com/food-api/docs) | Nutrition information for a recipe (calories, macros), stored with the recipe | Free key | Small daily quota: store the result, don't refetch on every page view |
| [Unsplash](https://unsplash.com/documentation) | Add a photo to a recipe that doesn't have one | Free key | Attribution required: store and show the photographer's name and link |
| [Resend](https://resend.com/docs) | Email a grocery list or a weekly meal plan | Free key | You must verify a sending address; log each sent email in the database |

### Offered by a teammate (Henry): self-hosted AI API

Henry offered the team access to an AI model he runs on his own server (Qwen3.6 27B via Ollama, hosted in California). Possible features: Q&A about a recipe, recipe summaries, writing help (e.g. cleaning up instructions).

Proposed limits for a dedicated team key:

- 500 requests per day for the whole team;
- up to 8 requests per minute, **one request processed at a time**;
- up to 2,048 output tokens per response;
- access until December 10 or 17, 11:59 p.m. Pacific Time.

Things to know before claiming it:

- It is an **AI/LLM API**, so it uses the group's only LLM slot: if we pick it, no one else adds OpenAI, Gemini, etc.
- Requests are handled one at a time, so a reply can be slow when several people use it. Show a loading state, set a timeout, and store the generated text in the database so the demo doesn't depend on a live call.
- The key is a shared secret: server-side environment variable only, never in the code, the browser, or a chat message. Henry shares it directly with the person who claims the API.
- If the server is down, the app must still work: recipes save, and the AI feature shows a clear "not available right now" message.
- Don't send personal data (emails, names) to it; recipe text only.
