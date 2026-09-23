# Unit 1 — Issue Selection Rubric

The checks that decide whether `issue-select` accepts or rejects a candidate issue.

**Rubric location:** This copy is for submission. The canonical version, used by the skill and the eval harness, lives at `~/.claude/skills/issue-select/rubric.md`. Keep them in sync.

---

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer alive | "maintainer first-response sample" under Repo facts: days to first owner/member/collaborator comment on 5 recently updated issues | Median response time ≤ 30 days (at least 3 of 5 issues have a response; if fewer than 3, median is unclear) | required |
| Recent activity | "last 5 default-branch commits" dates and "latest release" date under Repo facts | At least one commit within 90 days of the capture date, OR a release within 90 days | required |
| Scope is bounded | Issue title and body, comment thread for maintainer guidance | Not marked as umbrella/tracking, not a design debate with no settled answer, no maintainer comment saying "touches core internals"; and is not a pure support question ("how do I...") | required |
| No claim on it | "this issue: assignees:" and "linked PRs:" under Repo facts; Comments section for claim comments ("I'll take this", "working on this", "can I work on it") dated after issue open | No assignee; no open linked PR; no claim comment from anyone within 14 days of capture date | required |
| AI workflow allowed | "contribution policy" under Repo facts, referencing CONTRIBUTING.md, AI_USAGE_POLICY.md, AGENTS.md if present | Not explicitly banned ("we do not accept AI-generated code"); conditions (disclosure, understanding, testing, review) are acceptable terms, not blockers | required |

---

## Verdict rule

**Accept when:** all five required checks pass.

**Reject when:** any required check fails.

**Unclear handling:** if any required check is marked unclear (evidence genuinely missing from the bundle), treat it as fail. A first issue you cannot verify is not a first issue you should take.

**Why these thresholds:**

- **30 days for maintainer response:** slow response (months) means your PR will sit unreviewed, costing you the feedback cycle of a good first issue. 30 days is slow but survivable; faster is better but not required.
- **90 days for activity:** a repo last touched 6+ months ago is likely dormant. Three months is the practical cutoff for "is anyone home."
- **14 days for claim staleness:** two weeks of silence on an "I'll work on this" usually means the person moved on, and the issue is fair game again. Older claims are assumed abandoned.
- **No conditions are blockers:** repos that require disclosure, personal understanding, testing, and review of AI work are stating their standards, not rejecting AI-assisted contributions. We are equipped to meet those terms.

---

## Calibration log (class activity)

Four issues, graded with the rubric above, then argued out in the group.

| Issue | My verdict | Group verdict | Disagreed on | What I changed |
|---|---|---|---|---|
| | | | | |

**Changes made after calibration, and what each cost:** (none yet—this section fills during the activity and revision phase)

---

## Eval run — 20 labelled issues

Agreement with the instructor's labels.

- **Agreed:** _/20
- **Disagreed:** _/20

### Disagreements

The graded part. One entry per disagreement.

**Issue <n>:** tool said <verdict>, instructor said <verdict>.
- **Which check drove it:**
- **Who was right, and why:**
- **What I changed (or why I left it):**
- **What that change traded away:**

---

## Chosen first issue

From the Path Review repo. Run the skill on 2–3 candidates; pick from the accepted ones.

| Candidate | Tool verdict | Score |
|---|---|---|
| | | |

**Picked:** <issue link>
**Tool's verdict on it:** <verdict + score>
**Why this one over the other accepted candidates:**

> Claiming happens in **Unit 2**. Do not comment on the issue this week.
