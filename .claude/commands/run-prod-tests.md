# Run Prod Tests

Run all validation checks that require network access to the live site (itautonomos.com).

## Checks to run

1. `.claude/commands/test-bitly-links.md` - Bit.ly redirects validation
2. `.claude/commands/test-prod-site-links.md` - PROD site links & anchors validation using lychee

## Instructions

1. Read each command file listed above
2. Launch a Task agent for each check (run in parallel)
3. Wait for all agents to complete
4. Compile results into a unified report (see format below)

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
