# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where evidence lives:**
- In eval bundles: the "Diagnosis" section under "Candidate plan" (what the plan claims is broken); the "Actual behavior" or specific error output in the "Repro evidence" section (what actually failed).
- In live mode: the student's posted plan comment on the issue thread; the student's posted repro comment from Unit 2 (the actual error and output).

**What good looks like:**
The diagnosis section quotes or directly names a specific behavior, output, or error from the repro evidence (e.g., "health check fails with AttributeError: redis_host" matches a repro that says "AttributeError: redis_host" in the logs). The diagnosis does not contradict the repro (e.g., it doesn't claim the bug is in Redis itself when the repro shows it's an attribute mismatch in Python code). The diagnosis identifies the root cause, not a symptom (e.g., "the health check code uses redis_host" rather than "the health check fails").

## Scope

**Where evidence lives:**
- In eval bundles: the "Scope" section under "Candidate plan" (in-scope / not-in-scope boundaries); the "Files" section (what files will be touched).
- In live mode: the student's plan comment or plan.md file, explicitly stating what will be changed and what won't.

**What good looks like:**
The scope section explicitly names specific files, functions, or areas (e.g., "health.py lines 46-51" or "redis initialization only, not Redis client wrapping"). Boundaries between in-scope and out-of-scope are stated clearly (e.g., "in scope: fix the health check; not in scope: rewrite the Redis client library"). Changes are focused on one problem, not multiple loosely-related fixes (e.g., not "fix redis check AND refactor logging AND improve error handling").

## Executability

**Where evidence lives:**
- In eval bundles: the "Approach" section under "Candidate plan" (the ordered steps to implement the fix).
- In live mode: the student's plan comment or plan.md, describing how the fix will be made.

**What good looks like:**
Each step in the approach names what code will be changed and how (e.g., "replace redis.Redis(host=..., port=...) with redis.from_url(settings.redis_url)" instead of just "fix the redis call"). Steps are in order and each builds on the previous one. Specificity is high enough that a stranger unfamiliar with the codebase could start working without asking questions (e.g., lines are cited, function names are given). The approach is about implementation, not about problem-solving (it assumes the diagnosis is already decided).

## Test plan

**Where evidence lives:**
- In eval bundles: the "Test plan" section under "Candidate plan" (how the fix will be verified); the "Steps" section under "Repro evidence" (what was failing before).
- In live mode: the student's plan comment or plan.md; the Unit 2 repro comment posted earlier.

**What good looks like:**
The test plan describes concrete, observable checks that prove the fix worked (e.g., "re-run the health check endpoint: curl http://localhost:8000/health, expect HTTP 200 with redis: healthy" instead of "run tests"). The test plan maps onto the repro evidence (e.g., it re-runs the exact commands or checks that were failing before). Observable results are named (e.g., "expect the output to include", "expect the error to disappear", not just "verify it works").

## Honesty

**Where evidence lives:**
- In eval bundles: the "Risks and unknowns" section of the candidate plan (if present); the "Approach" section (whether risks are mentioned or hidden).
- In live mode: the student's plan comment or plan.md, especially where uncertainty or unfamiliar code is discussed.

**What good looks like:**
The plan acknowledges risks or unknowns explicitly (e.g., "I haven't worked with this library before" or "the Redis version might matter"). Unknowns are not dressed up as certainties (e.g., "this is definitely a timeout issue" when the repro only hints at timeouts). Mid-build deviations from the plan are noted and the plan is updated or explained in a comment (not silently ignored).

## Comms

**Where evidence lives:**
- In eval bundles: the "Candidate plan comment" text; the "Thread highlights" section (what maintainers said); the "Repo facts" section (stated contribution style and policies).
- In live mode: the student's posted plan comment on the GitHub issue; earlier comments in the thread; the repo's CONTRIBUTING.md or issue template.

**What good looks like:**
The plan comment is specific to this issue (references the issue number, the stated problem, the reproduced behavior) rather than generic boilerplate (e.g., "I would like to help" without saying how). The tone matches the repo's stated style (e.g., casual and direct if the thread is casual; formal if the repo's CONTRIBUTING guide is formal). The comment acknowledges maintainer signals from earlier in the thread (e.g., responding to a question a maintainer asked, or addressing a label they applied). The comment follows the repo's stated contribution conventions (e.g., if the repo asks for "minimum example to reproduce," the comment links to one; if it asks for a linked issue, the comment names it).
