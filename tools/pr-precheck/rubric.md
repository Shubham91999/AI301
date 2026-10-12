# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff faithful to plan | PR diff vs. plan.md (scope + files sections); Deviations section if present | Each commit's changes fit within the plan's stated scope and files, or are explicitly documented in Deviations; no silent drift (no extra fixes, refactors, or unrelated changes hiding in the same commit) | required |
| Test evidence decisive | PR test evidence section vs. plan's test plan; evidence shows observable before/after | Issue repro re-run on both main and branch, with actual output pasted; repo checks (make test-unit, make lint, make typecheck) run and output shown; every check result present, even if a test fails (hidden failures are drift) | required |
| Description precise | PR title and description vs. the diff; section by section | Title is specific to the issue (not boilerplate); Changes section names every file in the diff; Testing section ticked accurately and test results pasted; no omitted or misrepresented changes | required |
| Standards met | Repo facts (PR template, disclosure policy) vs. PR description sections | All mandatory template items addressed (closes #<issue>, testing checkboxes ticked, AI disclosure present if required by policy); description format matches repo's stated template | required |
| Debris-free implementation | Diff itself: all lines | No debug lines, commented code, unrelated whitespace changes, or scratch files; changes are minimal and surgical to the scope | required |

## Verdict rule

Accept if all five required checks pass; reject if any check is fail or unclear. Unclear counts as fail per the stated grading discipline.
