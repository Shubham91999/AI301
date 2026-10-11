# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the **issue** first: title, description, and thread highlights. Note the maintainer signals (what they asked for, what they emphasized). Note any thread activity or maintainer tone.
2. Read the **repro evidence** block next: the environment, the steps, and the actual output/error. Note what specific failure mode or behavior the repro pins down (e.g., "AttributeError on redis_host" or "request headers not parsed").
3. Read the **candidate plan** sections in order: diagnosis, scope, files, approach, test plan. Note what the diagnosis claims to fix and how it maps (or doesn't map) to the repro failure.
4. Read the **plan comment** last: note how it addresses (or ignores) the thread and the repo's style.

This order matters because the checks compare the plan against the evidence. Knowing the evidence first makes it clear what the diagnosis should cite and what the test plan must verify.

## Evidence gathering

1. **For diagnosis check:** Pull the diagnosis section from the candidate plan. Pull the specific behavior/error/output named in the repro evidence block. Record: (1) what the diagnosis claims is broken, (2) what specific behavior or output from the repro evidence the diagnosis cites.

2. **For scope check:** Pull the scope section ("in scope / not in scope") and the files section from the candidate plan. Record: (1) each file or function named, (2) whether scope boundaries are explicit or vague, (3) whether the change appears to be one focused problem or multiple loosely-connected fixes.

3. **For approach check:** Pull the approach section from the candidate plan. Record: (1) whether each step names what code will be changed (e.g., "line 46 of health.py"), (2) whether order is clear, (3) whether concrete enough that a stranger could start without asking.

4. **For test plan check:** Pull the test plan section from the candidate plan and the steps/outputs from the repro evidence. Record: (1) each test step the plan names, (2) which repro step(s) it corresponds to, (3) what observable output it checks for (not just "run tests").

5. **For comment check:** Pull the plan comment text and the thread highlights from the package. Pull the repo-facts block (contribution style, templates). Record: (1) whether the comment addresses any questions or signals from the thread, (2) tone and length (boilerplate or specific), (3) whether it matches the repo's stated style.

## Check execution

Execute the checks in order:

1. **Diagnosis check:** Does the plan's stated root cause refer to a specific behavior or output in the repro evidence? Does it contradict anything the repro shows? Pass if: diagnosis names the observed failure and cites it directly. Fail if: diagnosis ignores the repro evidence, contradicts it, or is vague ("something is wrong with the code").

2. **Scope check:** Are the files specific and boundaries clear? Does the change stay focused on one problem or creep into others? Pass if: files are named explicitly, in/out boundaries are stated, no scope creep. Fail if: files are vague ("the system"), scope boundaries are missing, or the approach sounds like multiple unrelated fixes.

3. **Approach check:** Is each step concrete and in order? Could a stranger execute it? Pass if: each step names what code changes and roughly how, not just "fix it"; order is clear; specificity is high enough that a reader doesn't have to guess. Fail if: steps are abstract ("refactor the module"), or order is unclear, or a stranger would have to interpret vague language.

4. **Test plan check:** Does the test plan map directly to repro evidence and check observable results? Pass if: test plan names specific commands or outputs from the repro; checks something observable that proves the fix worked. Fail if: test plan is vague ("run tests"), doesn't map to the repro, or wouldn't actually verify the fix.

5. **Comment check:** Does the comment address the thread and match the repo's style? Pass if: comment is specific to this issue (not boilerplate), addresses maintainer signals from the thread (or acknowledges silence), tone matches the repo's contribution style. Fail if: comment is generic boilerplate, ignores the thread, or tone mismatches the repo.

Grade each check as pass, fail, or unclear. If evidence for a check is genuinely absent (e.g., no scope section in the plan), mark as fail.

## Verdict assembly

Apply the rubric's verdict rule: accept if all five checks pass; reject if any check is fail or unclear.

When a check is marked unclear, treat it as fail per the verdict rule. Record the first check that failed or was unclear as the deciding check in the output.

In the final verdict statement, quote the deciding check's name and the specific evidence that caused it to fail (e.g., "Diagnosis grounded in evidence: plan names 'tokenizer too strict' but repro shows 'argparse stops consuming positionals' — these don't match").
