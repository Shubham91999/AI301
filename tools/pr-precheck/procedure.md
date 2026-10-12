# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Read the **plan.md** first (or house plan), including Deviations if present. Note the scope (in-scope / out-of-scope), the files named, and the test plan.
2. Read the **PR title and description**, noting each section (Summary, Issue, Changes, Testing, Notes).
3. Read the **diff** against the plan's scope and files. Note what each file changes.
4. Read the **test evidence**, matching it against the plan's test plan (before/after repro output, check results).
5. Read the **repo facts** (PR template, policy) to verify the description meets standards.

This order matters because the side-by-side checks compare: diff against plan scope, evidence against test plan, description against diff and template. Knowing what the plan promised before reading the diff lets you spot silent drift.

## Evidence gathering

1. **For diff faithfulness:** Extract scope + files from plan.md; list all files touched by the diff; compare. Record: files in diff, files in plan, any mismatch.
2. **For test evidence:** Read plan's test plan (e.g., "re-run issue script, expect X"); compare to evidence block. Record: whether before/after repro output is present, whether results match expectations, whether checks (make test-*, make lint, make typecheck) are reported.
3. **For description precision:** Line-by-line compare Changes section against diff file list; compare Issue section against plan's issue number; check Testing boxes. Record: each claim in description, whether it matches the diff.
4. **For standards:** Cross-reference description against repo-facts PR template and policy. Record: each mandatory template item, whether it's addressed in description.
5. **For debris:** Scan diff for debug lines, comments, unrelated whitespace. Record: any non-essential lines found.

## Check execution

Run checks in rubric order (Diff faithful, Test evidence, Description, Standards, Debris). For each:
1. Grade pass, fail, or unclear based on the gathered evidence and the check's pass condition
2. If evidence is genuinely absent (no test output when evidence section exists but is empty), mark fail
3. Quote the specific fact or line from the evidence that decided the grade

## Verdict assembly

Apply verdict rule: accept if all required checks pass; reject if any is fail or unclear. Unclear counts as fail.

The deciding check is the first required check (in rubric order) that failed or was unclear. Quote that check's name and evidence in the output JSON.
