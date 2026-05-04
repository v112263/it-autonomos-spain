---
name: tests-local-run-local-tests
description: "Run all LOCAL validation checks that don't require network access to the live site."
allowed-tools: Read, Glob, Grep, Bash, Task
---

# Run Local Tests

Run all LOCAL validation checks that don't require network access to the live site.

## Checks to run

1. `/tests-local-test-and-update-internal-links` - Internal links validation (LOCAL _site/ files)
2. `/tests-local-test-local-site-links` - LOCAL site links & anchors validation (requires LOCAL server running)

## Instructions

1. Launch both checks in parallel using the Skill tool:
   - Call Skill tool with skill: `tests-local-test-and-update-internal-links`
   - Call Skill tool with skill: `tests-local-test-local-site-links`
2. Wait for both to complete
3. Compile results into a unified report (see format below)

## Output Format

```
# Local Tests Results

## 1. Internal Links
[Summary from test-and-update-internal-links]

## 2. LOCAL Site Links (lychee)
[Summary from test-local-site-links]

---

## Summary

| Check | Status |
|-------|--------|
| Internal Links | ✅ / ❌ |
| LOCAL Site Links | ✅ / ❌ |
| **TOTAL** | ✅ **All LOCAL tests passed** / ❌ **Issues found** |
```
