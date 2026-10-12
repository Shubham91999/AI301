---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

Is this pull request ready to submit to the maintainers?

A PR package contains: the PR title and description, the commits and diff on the branch, the test evidence showing the fix works, and the plan it claims to implement. The tool reads all of these against the issue thread, the repo's PR template, and the stated AI disclosure policy to decide whether the PR is faithful to the plan, contains no unrelated changes, includes sufficient evidence, and respects the repo's conventions.

## Inputs and modes

**Live mode** (grading your own PR before you open it):
- plan.md: your plan from Unit 3, including any Deviations
- diff: output of `git diff main...HEAD` (three dots), showing every committed change on your branch
- PR title and description: from pr_draft.md
- test evidence: from test_evidence.md (before/after reproduction steps, repo checks' output)
- issue thread: fetched from GitHub (the issue's description, comments, and maintainer signals)
- repo facts: CONTRIBUTING.md, PR template (.github/PULL_REQUEST_TEMPLATE.md), stated AI policy if present

A house-chain student reads the house plan and house repro pack instead of their own, and the house branch's diff instead of their own branch.

**Eval mode** (grading practice PR packages):
The bundle is the whole world. Every fact comes from the bundle; nothing is fetched from GitHub or elsewhere. Every check runs with the full verdict rule.

## The scope seam (live mode only)

Before grading in live mode, read scope.md and check the Repo: line. If it contains a placeholder (e.g., `<ORG>/<REPO>`), stop and tell the student to fill in their Path Review repo. Refuse to grade any PR outside the scoped repo. Eval mode ignores scope.md entirely.

## The voice seam (live mode only)

In live mode, read voice-guide.md and check the draft PR title and description against the stated rules. Report any rule the draft breaks in your per-check summary, but voice violations never change the verdict on their own unless the rubric contains a communication check. Eval mode ignores voice-guide.md entirely.

## Component reads

rubric.md defines the checks and the verdict rule that determines accept or reject. procedure.md is executed as written: follow the steps in order, and when the procedure is silent on a step, report the gap and do not improvise. references/evidence-guide.md maps where each evidence family lives in a PR package.

If rubric.md or procedure.md has no content beyond template comments, refuse to grade and explain that the tool cannot operate without these files.

## Verdict and output

The verdict is binary: `accept` (ready to submit) or `reject` (hold). End your reply with a fenced JSON block, valid and last, with nothing following it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first:** Every check decision is backed by a concrete fact or direct quote from the package, not an opinion.
- **Grade the thing, not the polish:** A terse faithful PR is ready; a polished one hiding drift is not.
- **The rubric decides:** If a check passes by its stated condition, it passes, even if something feels off. Fix the rubric, not the run.
- **The procedure decides how:** Follow procedure.md exactly; when it's silent on a step, report the gap and do not improvise.
- **Unclear defaults to fail:** When unclear is not addressed in the rubric's verdict rule, treat it as fail.
