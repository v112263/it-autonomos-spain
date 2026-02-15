---
name: tests-prod-run-prod-tests
description: "Run all PROD validation checks that require network access to the live site (itautonomos.com)."
allowed-tools: Read, Glob, Grep, Bash, Task
---

# Run Prod Tests

Run all validation checks that require network access to the live site (itautonomos.com).

## Checks to run

1. `/tests-prod-test-bitly-links` - Bit.ly redirects validation
2. `/tests-prod-test-prod-site-links` - PROD site links & anchors validation using lychee

## Instructions

1. Launch both checks in parallel using the Skill tool:
   - Call Skill tool with skill: `tests-prod-test-bitly-links`
   - Call Skill tool with skill: `tests-prod-test-prod-site-links`
2. Wait for both to complete
3. Compile results into a unified report (see format below)

## Output Format

```
# Prod Tests Results

## 1. Bit.ly Links
[Summary from test-bitly-links]

## 2. Prod Site Links (lychee)
[Summary from test-prod-site-links]

---

## Summary

| Check | Status |
|-------|--------|
| Bit.ly Links | ✅ / ❌ |
| Prod Site Links | ✅ / ❌ |
| **TOTAL** | ✅ **All PROD tests passed** / ❌ **Issues found** |
```
