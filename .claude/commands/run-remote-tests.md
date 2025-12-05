# Run Remote Tests

Run all validation checks that require network access to the live site (itautonomos.com).

## Checks to run

1. `.claude/commands/check-itautonomos-links.md` - W3C link checker for all site pages

## Instructions

1. Read each command file listed above
2. Launch a Task agent for each check
3. Wait for all agents to complete
4. Compile results into a unified report (see format below)

## Output Format

```
# Remote Tests Results

## 1. ITAutonomos Links (W3C)
[Summary from check-itautonomos-links]

---

## Summary

| Check | Status |
|-------|--------|
| ITAutonomos Links | ✅ / ❌ |
| **TOTAL** | ✅ **All remote tests passed** / ❌ **Issues found** |
```

## Notes

- These tests check the LIVE site at https://itautonomos.com
- Make sure changes are deployed before running remote tests
- Network issues may cause false negatives - retry if needed
