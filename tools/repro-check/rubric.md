# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment block (first section after title) | Names tool version, OS, and any other version-specific dependencies the issue targets. Versions named match the issue's stated target, or the difference is explicitly called out. | required |
| Steps are followable | The repro report's execution section (reproduction steps) | A stranger who has never seen this repo could start from the stated environment and re-run the steps without guessing. Each step names the command or action taken, in order. | required |
| Behavior matches the issue | The repro report's output/behavior section and issue description | The observed behavior (output, error, panic) matches what the issue describes—same error type, same trigger condition. Not a related failure or adjacent bug. | required |
| Outcome stated honestly | The repro report's conclusion and the claim comment | The report says what actually happened: either "bug reproduced" with evidence, or "cannot reproduce" with a clear explanation of what was tried. Does not claim success beyond what the evidence shows. | required |
| AI disclosure (if required) | The claim comment and repro report against the repo's contribution policy (CONTRIBUTING.md, AI_POLICY.md, or issue template) | If the repo policy requires disclosure of AI usage, the disclosure is present in the comment. If the policy does not require disclosure, this check passes. | required |
| Comms respect conventions | The claim comment and repro report against the repo's CONTRIBUTING.md and issue template | Comment tone and structure match the repo's stated conventions. No boilerplate, specific to this issue. | required |

## Verdict rule

Accept (ready to post) only if every required check passes. Preferred checks never change the verdict. Unclear (?) counts as fail.
