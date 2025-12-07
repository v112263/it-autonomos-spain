# Run Local Tests

Run all LOCAL validation checks that don't require network access to the live site.

## Checks to run

1. `.claude/commands/tests/local/test-and-update-anchors.md` - Expected anchors validation (LOCAL _site/ files for all 8 pages: 4 index + 4 mortgage)
2. `.claude/commands/tests/local/test-local-site-links.md` - LOCAL site links & anchors validation (requires LOCAL server running)

## Instructions

1. Read each command file listed above
2. Launch a separate Task agent for each check (run in parallel)
3. Wait for all agents to complete
4. Compile results into a unified report (see format below)

## Output Format

```
# Local Tests Results

## 1. Expected Anchors
[Summary from test-and-update-anchors]

## 2. LOCAL Site Links (lychee)
[Summary from test-local-site-links]

---

## Summary

| Check | Status |
|-------|--------|
| Expected Anchors | ✅ / ❌ |
| LOCAL Site Links | ✅ / ❌ |
| **TOTAL** | ✅ **All LOCAL tests passed** / ❌ **Issues found** |
```
