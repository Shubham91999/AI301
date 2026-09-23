# Rubric Calibration Worksheet (Solo)

**Name:** Shubham Kulkarni
**Date:** September 22, 2026

## The plan (40 minutes)

1. Grade the four issues — 10 min, solo, in this doc
2. Disagreement log + synthesis — 15 min, together, in the group doc
3. **Revision marks — 10 min, solo, in this doc**
4. Debrief — 5 min, together, in the group doc

---

## Phase 1: Grade the four issues

### Your checks

| Check 1 | Maintainer alive |
| --- | --- |
| Check 2 | Recent activity |
| Check 3 | Scope is bounded |

### Grading table

Apply each check to the issue bundles and write P (pass), F (fail), or ? (unclear).

| Issue | Check 1 | Check 2 | Check 3 | Verdict |
| --- | --- | --- | --- | --- |
| **calib-00 (example)** | **P** | **F** | **?** | **reject** |
| **calib-01 (p5.js)** | **P** | **P** | **P** | **accept** |
| **calib-02 (minikube)** | **F** | **P** | **P** | **reject** |
| **calib-03 (HTTPie)** | **F** | **F** | **P** | **reject** |
| **calib-04 (bat)** | **F** | **P** | **F** | **reject** |

#### Reasoning

**calib-01 (p5.js min/max):**
- Maintainer alive: Median response = 0.2 days (from {0.0, 0.2, 4.8}) ✓
- Recent activity: Last push 2026-08-04, release 2026-07-30 ✓
- Scope bounded: Specific function bug, reproduction provided ✓

**calib-02 (minikube nerdctl-bin):**
- Maintainer alive: Only 2 of 5 issues have response times; need ≥3 → FAIL
- Recent activity: Push 2026-08-03 (within 90 days) ✓
- Scope bounded: One-variable fix in makefile ✓

**calib-03 (HTTPie Windows guard):**
- Maintainer alive: Only 1 issue shown with "no comment" → fewer than 3 → FAIL
- Recent activity: Last push 2024-12-17 (~230 days ago) → FAIL (beyond 90 days)
- Scope bounded: Clear bug with exact line and reproduction ✓

**calib-04 (bat fallback syntax):**
- Maintainer alive: Only 2 of 5 responses → FAIL
- Recent activity: Push 2026-08-01 (within 90 days) ✓
- Scope bounded: Feature request open 6 years with ongoing design debate → FAIL (not settled)

---

## Phase 3: Revision marks

One block per change your rubric needs. Template: change type (add/drop/tighten/demote/promote), the check name, which disagreement motivated it.

### Mark 1

**Change (add / drop / tighten / demote / promote)**

| tighten |
| --- |

**Check**

| Maintainer alive |
| --- |

**Which disagreement motivated it (or gap plus the issue)**

| calib-02: The issue has "good first issue" label and clear scope (one-variable fix), but fails because only 2 of 5 response times are present. The problem may be the sample size (5) or the recency of the issues. Need to clarify: does "at least 3 of 5" mean only count those with recorded times, or does "no response" count as a data point? |
| --- |

### Mark 2

**Change**

| add |
| --- |

**Check**

| Issue age and thread activity |
| --- |

**Which disagreement motivated it**

| calib-04: Feature request open since 2020 (6 years). The thread has 23 comments but the maintainer initially closed it and only re-opened after community push. This reveals the "Scope is bounded" check doesn't catch old issues with ongoing design debate. Need a check that looks at issue open date and whether the design is still being debated. |
| --- |

### Mark 3

**Change**

| (optional—depends on group discussion) |
| --- |

**Check**

| (will fill if group surfaces a gap in the five families) |
| --- |

**Which disagreement motivated it**

| (pending group activity) |
| --- |
