# Run Local Tests

Run all local validation checks that don't require network access to the live site.

## Checks to run

1. `.claude/commands/check-and-update-anchors.md` - Expected anchors validation (local _site/ files for all 8 pages: 4 index + 4 mortgage)
2. `.claude/commands/check-bitly-links.md` - Bit.ly redirects validation

## Prerequisites

The `_site/` directory must exist with compiled HTML files. If it doesn't exist, run:
```bash
bundle exec jekyll build
```

## Instructions

1. Read each command file listed above
2. Launch a separate Task agent for each check (run in parallel)
3. Wait for all agents to complete
4. Compile results into a unified report (see format below)

## Output Format

```
# Local Tests Results

## 1. Expected Anchors
[Summary from check-and-update-anchors]

## 2. Bit.ly Links
[Summary from check-bitly-links]

---

## Summary

| Check | Status |
|-------|--------|
| Expected Anchors | ✅ / ❌ |
| Bit.ly Links | ✅ / ❌ |
| **TOTAL** | ✅ **All local tests passed** / ❌ **Issues found** |
```
