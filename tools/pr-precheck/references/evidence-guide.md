# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives:**
- Plan: scope section (in-scope / out-of-scope), files section, Deviations if present
- PR: diff (list of files/changes), description's Changes section

**What good looks like:**
Every file in diff is in plan's files or noted in Deviations. No extra fixes, refactors, or scope creep. Description Changes section lists every modified file with its purpose.

## Test evidence (harness category: not-tested)

**Where it lives:**
- Plan: test plan section
- PR: test-evidence section (before/after output, check results)

**What good looks like:**
Before and after output both present. Repo checks (make test-unit, make lint, make typecheck) run and output shown. Results match plan's expectations.

## Diff quality (harness category: unreviewable)

**Where it lives:**
- PR: diff and commits, description's Changes section and Title

**What good looks like:**
No debug lines, commented code, or unrelated changes. Claims in description match the diff. Title is specific, not generic.

## Standards and comms (harness category: standards-wall)

**Where it lives:**
- Repo facts: PR template, policy
- PR: description sections, title

**What good looks like:**
All mandatory template items addressed. AI disclosure present if required. Title specific. Format matches repo's template.
