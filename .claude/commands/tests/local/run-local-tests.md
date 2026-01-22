# Run Local Tests

Run all LOCAL validation checks that don't require network access to the live site.

## Checks to run

1. `.claude/commands/tests/local/test-and-update-internal-links.md` - Internal links validation (LOCAL _site/ files)
2. `.claude/commands/tests/local/test-local-site-links.md` - LOCAL site links & anchors validation (requires LOCAL server running)

## Instructions

1. Read each command file listed above
2. Launch a separate Task agent for each check (run in parallel)
3. Wait for all agents to complete
4. Compile results into a unified report (see format below)

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
