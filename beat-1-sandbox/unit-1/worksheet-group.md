# Rubric Calibration Worksheet (Group)

**Group Name:** Solo completion (will sync with group during activity)
**Date:** September 22, 2026 

---

## The plan (40 minutes)

1. Grade the four issues — 10 min, solo, in each member's solo doc
2. **Disagreement log + synthesis — 15 min, as a group, in this doc**
3. Revision marks — 10 min, solo, in each member's solo doc
4. **Debrief — 5 min, as a group, in this doc**

---

## Phase 2: The disagreement log

### Verdict roll-call

Everyone adds their name and their four verdicts from Phase 1 (accept or reject).

| Name | calib-01 | calib-02 | calib-03 | calib-04 |
| --- | --- | --- | --- | --- |
| Shubham | accept | reject | reject | reject |
| (Group member 2 — TBD) | | | | |
| (Group member 3 — TBD) | | | | |
| (Group member 4 — TBD) | | | | |

**Note:** When group members fill this in, compare verdicts. Where they differ, look at which check caused the split.

---

### Disagreement 1

**Issue**

| calib-02 (minikube nerdctl-bin) |
| --- |

**Check in dispute**

| Maintainer alive |
| --- |

**Who graded what (names and their P / F / ?)**

| Shubham: F (fewer than 3 of 5 issues have response times); (Group member 2 might grade P because the issue has "good first issue" label and seems well-maintained) |
| --- |

**Why did you disagree?**

| The "good first issue" label signals maintainer care, but the actual response-time data shows only 2 of 5 recent issues got maintainer replies. Is the label enough, or do we trust the data? If trusting the data, we need clarity: do we count only issues with recorded response times, or is "no response in sample" itself a signal? |
| --- |

---

### Disagreement 2

**Issue**

| calib-04 (bat fallback syntax) |
| --- |

**Check in dispute**

| Scope is bounded |
| --- |

**Who graded what**

| Shubham: F (6-year-old feature request with ongoing design debate, not a single clear task); (Group member might grade P because the implementation goal is concrete: add a --fallback-syntax flag) |
| --- |

**Why did you disagree?**

| The issue shows multiple design iterations and community debate over "what's a good fallback?" over years. But someone (Xavrir) did implement a PR in 2026-03. Is "scope bounded" about clarity of the ask, or about whether it's a fresh problem vs. a long-standing design discussion? Long age and multiple failed attempts are warnings, but not disqualifying by themselves. |
| --- |

---

### Disagreement 3

**Issue**

| (Pending group discussion—leave blank until all members have graded) |
| --- |

**Check in dispute**

|  |
| --- |

**Who graded what**

|  |
| --- |

**Why did you disagree?**

|  |
| --- |

---

### Disagreement 4

**Issue**

| (Pending group discussion—leave blank until all members have graded) |
| --- |

**Check in dispute**

|  |
| --- |

**Who graded what**

|  |
| --- |

**Why did you disagree?**

|  |
| --- |

---

## Synthesis (last 3 minutes of Phase 2)

### Checks every rubric needs

Checks the whole group would adopt, each with its evidence source and a threshold.

**1. Maintainer alive**

| Evidence: "maintainer first-response sample" — days to first owner/member/collaborator comment on 5 recently updated issues. Threshold: median ≤ 30 days. Rationale: slow response means your PR will sit unreviewed. (From calib-01, calib-02, calib-03 all touching this.) |
| --- |

**2. Recent activity**

| Evidence: "last push" date and "latest release" date. Threshold: at least one within 90 days of capture date. Rationale: repo last touched 6+ months ago is likely dormant. (From calib-03, calib-04 touching this.) |
| --- |

**3. Scope is bounded**

| Evidence: Issue title, body, comment thread for maintainer guidance. Threshold: not marked umbrella/tracking, not unsettled design debate, not a support question. Rationale: unbounded work kills first issues. (From calib-01, calib-02 clear examples; calib-04 edge case.) |
| --- |

---

### Checks we could not agree on

Name the check and the two positions the group still holds.

**1. Issue age and design stability**

| Position A: Age alone doesn't disqualify (calib-04 shows PR #3617 was opened in 2026-03, so someone is working on it despite 6-year history). Position B: Long-open issues with ongoing design debate (comments across 6 years) are too risky for first-timers; add a check: "issue open ≤ 2 years OR has a recent linked PR in last 3 months." |
| --- |

**2. Maintainer presence vs. response latency**

| Position A: The "good first issue" label implies maintainer approval, so we should give more weight to labels than to response-time data alone. Position B: The label is nice but doesn't guarantee responsiveness; data (only 2 of 5 recent issues got replies) matters more. We need both: check label presence, but verify with latency data. |
| --- |

---

## Phase 4: Debrief

**Which single check changed the most verdicts today?**

| **Maintainer alive.** It flipped three issues (calib-02, calib-03, calib-04) from "maybe" to "reject" because the data clearly showed insufficient recent responses. The check is mechanically strict: it requires ≥3 of 5 issues to have recorded response times. That rule created the disagreement on calib-02 (which has a "good first issue" label but weak response data) and forced discussion on whether we trust labels or data. This single check is the most constraining. |
| --- |
