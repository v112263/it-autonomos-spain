---
name: tests-run-all-tests
description: "Run all automated checks for the project (LOCAL + PROD) and provide a unified summary."
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash, Task
---

# Run All Tests

Run all automated checks for the project (both LOCAL and PROD) and provide a unified summary.

## Test suites to run

1. `/tests-local-run-local-tests` - All LOCAL validation checks
2. `/tests-prod-run-prod-tests` - All PROD validation checks

## Instructions

1. Launch both test suites in parallel using the Skill tool:
   - Call Skill tool with skill: `tests-local-run-local-tests`
   - Call Skill tool with skill: `tests-prod-run-prod-tests`
2. Wait for both to complete
3. Compile results into a unified report (see format below)

## Output Format

```
# All Checks Results

## LOCAL Tests

### 1. Internal Links
[Summary from test-and-update-internal-links]

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
| LOCAL Tests | Internal Links, LOCAL Site Links | ✅ / ❌ |
| PROD Tests | Bit.ly Links, PROD Site Links | ✅ / ❌ |
| **TOTAL** | **All checks** | ✅ **All passed** / ❌ **Issues found** |
```

## Adding new checks

- To add a LOCAL check: add it to the `tests-local-run-local-tests` skill
- To add a PROD check: add it to the `tests-prod-run-prod-tests` skill
