# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis grounded in evidence | Plan's diagnosis section read against repro-evidence block: the stated root cause refers to specific behavior or output the repro evidence actually shows | Diagnosis names the observed failure mode from repro evidence; does not contradict it; cites the specific line or output it points to | required |
| Scope clearly bounded | Plan's scope section (in-scope / not-in-scope / files named) read against the repro evidence's described problem | Scope is explicit (names specific files or functions, not "the whole system"); boundaries between in and out are clear; no scope creep (one problem, one fix, not a drive-by improvement) | required |
| Approach is executable | Plan's approach section read for whether steps are concrete and ordered | Each step names what will be changed and why (not just "fix the regex" but "rewrite regex at line N to match pattern X"); order is clear; a stranger could start without asking the author | required |
| Test plan is decisive | Plan's test plan section read against repro-evidence block: the test names specific outputs, commands, or failures it will verify | Test plan re-runs steps from repro evidence or checks their output directly; names the observable result that proves the fix worked (not "run tests" but "run test case 1 and expect header to parse") | required |
| Comment respects thread and conventions | Plan comment read against thread highlights and repo-facts block (contribution style, templates, stated conventions) | Comment addresses maintainer signals or questions from the thread (or acknowledges there are none); tone matches repo's stated style; specific to this issue, not boilerplate | required |

## Verdict rule

Accept if all five required checks pass; reject if any fails or is unclear. Unclear counts as fail.
