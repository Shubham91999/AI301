# Unit 2 Submission: Claim and Reproduce

## Claim comment

**Link to claim comment:** https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62#issuecomment-5923175083

**Comment text:**

Hi! I'd like to take this issue as my first PathReview contribution. I can see the bug clearly: the health check code references `settings.redis_host` and `settings.redis_port`, but the `Settings` class only defines `redis_url`. I have reproduced this on the current codebase (steps below) and will follow up with a full reproduction report and a fix proposal.

## Quick reproduction

Environment: macOS 14.6, Python 3.11, Redis running via Docker Compose (default config from `docker-compose.yml`)

Steps:
1. Clone the repo and run `docker compose up -d` to start Redis
2. Run the FastAPI server with `make run` or `python -m uvicorn api.main:app --reload`
3. Call the health check endpoint: `curl http://localhost:8000/health`

Expected: `"redis": "healthy"` in the response

Actual: `"redis": "unhealthy"`, with `redis_health_check_failed` and an `AttributeError: redis_host` in the logs

The issue is in `api/routes/health.py`, which should use `settings.redis_url` instead of the nonexistent `settings.redis_host` and `settings.redis_port`.

I'll follow up with the full reproduction package and test verification shortly.

---

## Repro comment

**Link to repro comment:** https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62#issuecomment-5925366888

**Comment text:**

# Reproduction Report: Health check references nonexistent Redis settings

## Environment

**System:** macOS 14.6 (arm64)
**Python:** 3.11.6
**Redis:** 7.0 (via Docker Compose from docker-compose.yml)
**Date of test:** 2026-09-30

The issue was filed against the current main branch; reproduction confirmed on the same codebase.

## Analysis: Code examination

**Location of the bug:** `api/routes/health.py`, lines 46–51

```python
r = redis.Redis(
    host=settings.redis_host,    # ← BUG: redis_host does not exist
    port=settings.redis_port,    # ← BUG: redis_port does not exist
    db=0,
    decode_responses=True,
)
```

**What Settings actually defines:** `core/config.py`, line 14

```python
redis_url: str = Field(default="redis://localhost:6379/0")
```

The Settings class defines a single `redis_url` field, not separate `redis_host` and `redis_port` fields. The health check code is referencing nonexistent attributes.

## Steps to reproduce

1. **Start Redis via Docker Compose:**
   ```bash
   cd pathreview
   docker compose up -d
   ```

2. **Install dependencies and start the FastAPI server:**
   ```bash
   pip install -e .
   python -m uvicorn api.main:app --reload --host 0.0.0.0 --port 8000
   ```

3. **Call the health check endpoint:**
   ```bash
   curl http://localhost:8000/health
   ```

## Expected behavior

The health check should return HTTP 200 with all dependencies healthy:

```json
{
  "status": "healthy",
  "dependencies": {
    "postgres": "healthy",
    "redis": "healthy",
    "vector_db": "healthy"
  },
  "safety_events_last_hour": 0,
  "timestamp": "2026-09-30T..."
}
```

## Actual behavior

The health check fails with HTTP 503 Service Unavailable. The response reports:
```json
{
  "status": "unhealthy",
  "dependencies": {
    "postgres": "healthy",
    "redis": "unhealthy",
    "vector_db": "healthy"
  }
}
```

**Server logs show:** `redis_health_check_failed error='Settings' object has no attribute 'redis_host'`

## Root cause

The health check code was written to use host/port parameters, but Settings was configured to use a connection URL instead. This mismatch means:
- `settings.redis_host` → AttributeError
- `settings.redis_port` → AttributeError
- `settings.redis_url` → "redis://localhost:6379/0" ✓ (exists, but code doesn't use it)

The fix requires either parsing `redis_url` to extract host and port, or using a Redis client that accepts URL strings directly (e.g., `redis.from_url(settings.redis_url)`).

## Confirmation

This bug is reproducible on the current main branch and is deterministic—not dependent on OS or Python version, only on the attribute mismatch in the code.

---

## Evaluation run

### Run history

**Initial full run (20 packages):**
- Result: 18/20 agreement (meets the bar), but disclosure category floor unmet (0/1)
- Problem: pkg-20 (ghostty repo requiring AI disclosure) was incorrectly accepted
- Root cause: "Comms respect conventions" was marked `preferred`, not required, so disclosure violations didn't block acceptance

**Revision 1: Made disclosure check explicit and required**
- Changed: "Comms respect conventions" → from preferred to required
- Added new check: "AI disclosure (if required)" as required check
- Updated: "Steps are followable" evidence guide to clarify what counts as followable (references with params are followable)
- Tested on pkg-12 and pkg-20 with `--only` flag

**Final full run (20 packages, single worker):**
- **Result: 18/20 agreement (PASS) + disclosure category 1/1 (PASS)**
- Agreement: 18 of 20 scored packages match gold labels
- Categories: clear-accept 6/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4
- Disagreements: pkg-05 and pkg-12 on "Steps are followable" (within acceptable margin)

### Package analysis

**pkg-20 (ghostty issue #13604):**
- Gold label: reject
- Your rubric decision: reject
- Agreement: YES ✓
- Why: The repo's contribution policy (AI_POLICY.md) explicitly requires "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance." The candidate repro report does not disclose AI assistance. The "AI disclosure (if required)" check correctly identified this violation and caused rejection.

### Check rationale

Quoting the checks as they appear in the submitted rubric.md (exactly matching the file):

**Environment recorded (required):** "Names tool version, OS, and any other version-specific dependencies the issue targets. Versions named match the issue's stated target, or the difference is explicitly called out."

**Steps are followable (required):** "A stranger who has never seen this repo could start from the stated environment and re-run the steps without guessing. Each step names the command or action taken, in order."

**Behavior matches the issue (required):** "The observed behavior (output, error, panic) matches what the issue describes—same error type, same trigger condition. Not a related failure or adjacent bug."

**Outcome stated honestly (required):** "The report says what actually happened: either 'bug reproduced' with evidence, or 'cannot reproduce' with a clear explanation of what was tried. Does not claim success beyond what the evidence shows."

**AI disclosure (if required) (required):** "If the repo policy requires disclosure of AI usage, the disclosure is present in the comment. If the policy does not require disclosure, this check passes."

**Comms respect conventions (required):** "Comment tone and structure match the repo's stated conventions. No boilerplate, specific to this issue."

### Trade-offs

**What the rubric gained:**
- Category floor is now met: disclosure violations are caught reliably (pkg-20 now correctly rejects)
- The explicit AI disclosure check makes the requirement unmissable and machine-graded consistently
- All six checks are now required; no "soft" preferred checks that let violations slide

**What the rubric lost:**
- The rubric is stricter: a package with perfect reproduction and honesty but a missing disclosure statement (in a repo that requires it) is now rejected entirely, even if the core reproduction work is excellent
- This trades flexibility for consistency with the course's academic integrity requirement (AI work must be disclosed where policy requires it)
- One borderline trade-off: we're treating disclosure as binary (present/absent) rather than graduated by quality or detail

---

## GitHub username

Shubham91999
