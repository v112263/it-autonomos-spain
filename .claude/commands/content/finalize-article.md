# Finalize Article

Prepare an article for publication by running all pre-publication checks. This command runs internal link addition and fact-checking in parallel for efficiency.

## Input

$ARGUMENTS

The input should be a path to an article file (e.g., `_includes/ru/tax-optimization/rent.md`).

## Workflow Context

This command is part of the article publishing workflow:

1. **Write article** - `/content:write-article` - Create or edit content
2. **Finalize article** - `/content:finalize-article` - (THIS COMMAND) Add links + fact-check
3. **Review & fix** - User reviews reports, makes corrections if needed
4. **Translate** - `/content:translate-article` - Translate to other languages

## Instructions

### Phase 1: Run Checks in Parallel

1. **Launch both checks in parallel** using the Skill tool:

   **Check A: Add Internal Links**
   - Call Skill tool with skill: `content:add-internal-links-to-article` and args: `[article path]`
   - This will analyze the article and add relevant internal/external links
   - Returns a summary of links added

   **Check B: Fact-Check Article**
   - Call Skill tool with skill: `content:fact-check-article` and args: `[article path]`
   - This will verify all facts against official sources
   - Returns a detailed fact-check report

2. **Wait for both to complete**

### Phase 2: Compile Results

3. **Present combined report** with the following structure:

```markdown
## Finalization Report: [Article Name]

**Article path:** `[path]`
**Finalized on:** [date]

---

### Part 1: Internal Links Added

[Output from add-internal-links-to-article]

---

### Part 2: Fact-Check Results

[Output from fact-check-article]

---

### Action Items

Based on the results above:

#### Required Changes (from Fact-Check)
- [ ] [List any facts that need correction]

#### Optional Improvements (from Links)
- [ ] [Any link suggestions that weren't auto-added]

---

### Next Steps

If there are no ❌ critical issues:
→ Article is ready for translation via `/content:translate-article`

If there are ❌ issues to fix:
1. Make the required corrections
2. (Optional) Re-run `/content:finalize-article` to verify fixes
3. Then proceed with `/content:translate-article`
```

## Important Notes

- **Internal links are added directly to the file** during this process
- **Fact-check is read-only** - it only reports issues, doesn't fix them
- If fact-check finds ❌ issues, user should fix them before translation
- The article is considered "finalized" only if fact-check shows no ❌ items

## Output

Present the combined finalization report with clear action items and next steps.
