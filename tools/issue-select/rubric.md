# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer alive | "maintainer first-response sample" under Repo facts: days to first owner/member/collaborator comment on 5 recently updated issues | Median response time ≤ 30 days (at least 3 of 5 issues have a response; if fewer than 3, median is unclear) | required |
| Recent activity | "last 5 default-branch commits" dates and "latest release" date under Repo facts | At least one commit within 90 days of the capture date, OR a release within 90 days | required |
| Scope is bounded | Issue title and body, comment thread for maintainer guidance | Not marked as umbrella/tracking, not a design debate with no settled answer, no maintainer comment saying "touches core internals"; and is not a pure support question ("how do I...") | required |
| No claim on it | "this issue: assignees:" and "linked PRs:" under Repo facts; Comments section for claim comments ("I'll take this", "working on this", "can I work on it") dated after issue open | No assignee; no open linked PR; no claim comment from anyone within 14 days of capture date | required |
| AI workflow allowed | "contribution policy" under Repo facts, referencing CONTRIBUTING.md, AI_USAGE_POLICY.md, AGENTS.md if present | Not explicitly banned ("we do not accept AI-generated code"); conditions (disclosure, understanding, testing, review) are acceptable terms, not blockers | required |

## Verdict rule

**Accept when:** all five required checks pass.

**Reject when:** any required check fails.

**Unclear handling:** if any required check is marked unclear (evidence genuinely missing from the bundle), treat it as fail. A first issue you cannot verify is not a first issue you should take.

**Why these thresholds:**

- **30 days for maintainer response:** slow response (months) means your PR will sit unreviewed, costing you the feedback cycle of a good first issue. 30 days is slow but survivable; faster is better but not required.
- **90 days for activity:** a repo last touched 6+ months ago is likely dormant. Three months is the practical cutoff for "is anyone home."
- **14 days for claim staleness:** two weeks of silence on an "I'll work on this" usually means the person moved on, and the issue is fair game again. Older claims are assumed abandoned.
- **No conditions are blockers:** repos that require disclosure, personal understanding, testing, and review of AI work are stating their standards, not rejecting AI-assisted contributions. We are equipped to meet those terms.
