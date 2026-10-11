# Plan: Fix health check Redis configuration (issue #62)

## Diagnosis

The health check code in `api/routes/health.py` (lines 46–51) references `settings.redis_host` and `settings.redis_port`, but the Settings class in `core/config.py` only defines a single `redis_url` field with the default value `"redis://localhost:6379/0"`. This mismatch causes an AttributeError when the health check executes: `'Settings' object has no attribute 'redis_host'`.

The reproduced evidence shows:
- Health check endpoint returns HTTP 503 with redis marked unhealthy
- Server logs show: `redis_health_check_failed error='Settings' object has no attribute 'redis_host'`
- The Settings class explicitly defines only `redis_url`, not separate host/port fields

## Scope

**In scope:**
- Fix the health check Redis connection in `api/routes/health.py` (lines 46–51)
- Use the Settings class's existing `redis_url` field to create the Redis connection
- Update the health check to parse or use the URL directly

**Not in scope:**
- Refactoring the Settings class or its configuration
- Changes to Redis client library version or wrapper code
- Improvements to error handling or logging beyond the immediate fix
- Other health checks or dependencies

## Files

- `api/routes/health.py` — the health check endpoint and Redis connection code (lines 46–51)
- `tests/test_health.py` — test the health check endpoint after the fix (if it exists)

## Approach

1. Examine the current code in `api/routes/health.py` lines 46–51 and confirm the AttributeError
2. Replace the Redis connection code to use `redis.from_url(settings.redis_url)` instead of passing host and port separately
3. Verify the health check endpoint returns HTTP 200 with `"redis": "healthy"` after the change
4. Run any existing tests to ensure no regressions

## Test plan

Re-run the reproduction steps from the Unit 2 repro report:

1. Start Redis via Docker Compose: `docker compose up -d`
2. Start the FastAPI server: `python -m uvicorn api.main:app --reload --host 0.0.0.0 --port 8000`
3. Call the health check endpoint: `curl http://localhost:8000/health`

**Expected behavior after the fix:**
- Health check returns HTTP 200 with status: "healthy"
- dependencies.redis is "healthy" (not "unhealthy")
- No AttributeError in server logs

**Before fix:** HTTP 503 with redis: "unhealthy" and error in logs
**After fix:** HTTP 200 with redis: "healthy" and no errors

## Risks and unknowns

- The exact Redis library API for URL-based connections (will confirm from redis-py documentation)
- Whether other parts of the codebase depend on the current Redis initialization pattern
- No direct experience with this FastAPI + Redis setup pattern, but the fix is mechanical

## Deviations

No deviations from the plan. The implementation matched the approach exactly: replaced `redis.Redis(host=settings.redis_host, port=settings.redis_port, ...)` with `redis.from_url(settings.redis_url, decode_responses=True)` on line 46 of `api/routes/health.py`.
