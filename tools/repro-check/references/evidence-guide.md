# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives:** The repro report's first section (often labeled "Environment" or "Setup"), or an explicit block at the top.

**What good looks like:** The environment statement names the tool/library version, operating system, and any version-specific dependencies (language version, package manager version, compiler flags). If the issue specifies a target version or OS, the report either uses that version or notes the difference and explains why (e.g., "issue filed against v4.53.2, I tested v4.53.3 to check if it's fixed").

## Steps

**Where it lives:** The repro report's execution section (after environment), labeled something like "Reproduction steps," "How to reproduce," or "Execution."

**What good looks like:** Each step is an action a stranger can take without guessing. Commands are shown in full (not "run the test" but "`pytest test_foo.py`"). File paths and inputs are exact, or clearly referenced with their parameters named. The sequence is in order, starting from a clean or stated starting state. A stranger in the stated environment could understand what to do and execute each step, even if they need to look up the referenced code in the issue.

## Behavior shown

**Where it lives:** The repro report's output section (the "what actually happened" part), often labeled "Actual behavior," "Output," or "Result."

**What good looks like:** The output shown (error message, panic, log excerpt, screenshot) is the actual text or image from the command run, not a summary. If comparing to expected behavior, both actual and expected are shown. The artifact matches the issue's stated failure—same error type, same class of problem, same trigger condition. Not a related failure (e.g., if the issue is "panic on non-string keys," the report shows a panic on non-string keys, not a different parsing error).

## Honesty

**Where it lives:** Across the entire report—the claims in the issue comment, and the evidence in the repro report that backs them.

**What good looks like:** If the bug reproduced: the report shows the exact failure from the issue, with environment and steps that would trigger it in the reader's setup. If the bug did NOT reproduce: the report says that clearly and explains what was tried and why the author cannot reproduce it (e.g., "I tested both 4.53.2 and 4.53.3 with the exact input from the issue, and got a different error, suggesting the issue may be version- or environment-specific"). No claim that goes beyond the evidence shown. An honest "cannot reproduce" with clear reasoning earns full marks.

## AI disclosure (if required)

**Where it lives:** The repo's contribution policy (CONTRIBUTING.md, AI_POLICY.md, or issue template, listed in Repo facts under "contribution policy"), and the claim comment and repro report.

**What good looks like:** If the repo policy does NOT mention AI usage requirements, this check passes automatically. If it DOES require disclosure (phrases like "All AI usage must be disclosed," "state the tool used," "disclose AI assistance"), then the comment must include a statement naming the AI tool(s) used and the extent of assistance. An example: "This report was drafted with Claude AI assistance for organizing the reproduction steps." If the policy forbids AI usage, no disclosure language can make a pass—the work must be AI-free.

## Comms

**Where it lives:** The claim comment (posted on the issue), the repro report structure and tone, and any statements about AI assistance or methodology.

**What good looks like:** The claim comment is specific to this issue—it names the issue's core problem, not generic ("I'd like to help with a bug" is not it). Tone matches the repo's conventions (formal, casual, technical detail level). If the repo's CONTRIBUTING.md or issue template requires disclosure of AI assistance, it is present. The repro report uses the repo's template structure if one exists. No boilerplate; every sentence refers to this specific issue or reproducer.
