# Run All Tests

Run all automated checks for the project (both local and remote) and provide a unified summary.

## Test suites to run

1. `.claude/commands/run-local-tests.md` 
2. `.claude/commands/run-remote-tests.md`

## Instructions

1. Read each test suite command file listed above
2. Launch a separate Task agent for each test suite (run in parallel)
3. Wait for all agents to complete
4. Compile results into a unified report (see format below)

## Output Format

```
# All Checks Results

## Local Tests

### 1. Expected Anchors
[Summary from check-and-update-anchors]

### 2. Bit.ly Links
[Summary from check-bitly-links]

## Remote Tests

### 3. ITAutonomos Links (W3C)
[Summary from check-itautonomos-links]

---

## Overall Summary

| Test Suite | Checks | Status |
|------------|--------|--------|
| Local Tests | Anchors (8 pages), Bit.ly | ✅ / ❌ |
| Remote Tests | ITAutonomos Links (8 pages) | ✅ / ❌ |
| **TOTAL** | **All checks** | ✅ **All passed** / ❌ **Issues found** |
```

## Adding new checks

- To add a local check: add it to `run-local-tests.md`
- To add a remote check: add it to `run-remote-tests.md`

## Pages covered

All tests now cover the complete site content:
- 4 index pages: `/`, `/ru/`, `/ua/`, `/es/`
- 4 mortgage pages: `/en/mortgage/`, `/ru/mortgage/`, `/ua/mortgage/`, `/es/mortgage/`
