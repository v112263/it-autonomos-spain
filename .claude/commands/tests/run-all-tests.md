# Run All Tests

Run all automated checks for the project (both LOCAL and PROD) and provide a unified summary.

## Test suites to run

1. `.claude/commands/tests/local/run-local-tests.md`
2. `.claude/commands/tests/prod/run-prod-tests.md`

## Instructions

1. Read each test suite command file listed above
2. Launch a separate Task agent for each test suite (run in parallel)
3. Wait for all agents to complete
4. Compile results into a unified report (see format below)

## Output Format

```
# All Checks Results

## LOCAL Tests

### 1. Expected Anchors
[Summary from test-and-update-anchors]

### 2. LOCAL Site Links (lychee)
[Summary from test-local-site-links]

## PROD Tests

### 1. Bit.ly Links
[Summary from test-bitly-links]

### 2. PROD Site Links (lychee)
[Summary from test-prod-site-links]

---

## Overall Summary

| Test Suite | Checks | Status |
|------------|--------|--------|
| LOCAL Tests | Anchors (8 pages), LOCAL Site Links | ✅ / ❌ |
| PROD Tests | Bit.ly Links, PROD Site Links (8 pages) | ✅ / ❌ |
| **TOTAL** | **All checks** | ✅ **All passed** / ❌ **Issues found** |
```

## Adding new checks

- To add a LOCAL check: add it to `run-local-tests.md`
- To add a PROD check: add it to `run-prod-tests.md`
