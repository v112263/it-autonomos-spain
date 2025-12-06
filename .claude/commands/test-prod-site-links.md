# Check Prod Site Links

Check all links and anchors on the **PROD** website (https://itautonomos.com) using lychee link checker.

## Prerequisites

**lychee** must be installed:
```bash
brew install lychee
```

## URLs to check

### Main pages (index)
1. https://itautonomos.com/ (English)
2. https://itautonomos.com/ru/ (Russian)
3. https://itautonomos.com/ua/ (Ukrainian)
4. https://itautonomos.com/es/ (Spanish)

### Mortgage pages
5. https://itautonomos.com/en/mortgage/ (English)
6. https://itautonomos.com/ru/mortgage/ (Russian)
7. https://itautonomos.com/ua/mortgage/ (Ukrainian)
8. https://itautonomos.com/es/mortgage/ (Spanish)

## Instructions

1. **Check if lychee is installed**:
   ```bash
   which lychee || echo "lychee not found - install with: brew install lychee"
   ```

2. **Run lychee for each page** with anchor fragment checking enabled:
   ```bash
   lychee --include-fragments --exclude "ec.europa.eu/taxation_customs/vies" "URL" 2>&1
   ```

   The `--exclude` flag skips the EU VIES VAT validation page which uses JavaScript routing (false positive).

3. **Run all 8 checks in parallel** using the Task tool for efficiency, or run sequentially:
   ```bash
   # Example for one page:
   lychee --include-fragments --exclude "ec.europa.eu/taxation_customs/vies" "https://itautonomos.com/ru/" 2>&1
   ```

4. **Parse the output** for each page:
   - Total links checked
   - OK links (✅)
   - Errors (❌) - broken links or missing anchors
   - Excluded (👻) - mailto links, etc.
   - Redirects (🔀)

## Known Exclusions

Some links may show errors but are false positives:
- **JavaScript-based anchors** (e.g., `https://ec.europa.eu/taxation_customs/vies/#/vat-validation`) - these use client-side routing and cannot be validated by lychee
- **Rate-limited sites** - some external sites may temporarily block requests

## Output Format

### Summary Table

```
## PROD Site Link Check Results

| Page | Total | OK | Errors | Excluded | Status |
|------|-------|-----|--------|----------|--------|
| EN Index (/) | 150 | 148 | 0 | 2 | ✅ |
| RU Index (/ru/) | 171 | 168 | 0 | 3 | ✅ |
| UA Index (/ua/) | 165 | 162 | 0 | 3 | ✅ |
| ES Index (/es/) | 150 | 148 | 0 | 2 | ✅ |
| EN Mortgage | 45 | 44 | 0 | 1 | ✅ |
| RU Mortgage | 45 | 44 | 0 | 1 | ✅ |
| UA Mortgage | 45 | 44 | 0 | 1 | ✅ |
| ES Mortgage | 45 | 44 | 0 | 1 | ✅ |
```

### Errors Report (if any)

```
## ❌ Errors Found

### RU Index (/ru/)
1. [ERROR] https://example.com/page#section | Cannot find fragment
2. [ERROR] https://broken-link.com | Network error

### Action Required
- Fix broken links listed above
- For anchor errors: verify the target section exists on the page
```

## Final Status

End with a clear summary:

```
## Final Status

✅ **ALL PROD LINKS VALID** - All 8 pages passed (X total links, Y anchors verified)
```

OR

```
## Final Status

❌ **PROD ISSUES FOUND** - X broken link(s) across Y page(s)

Action required: Fix the errors listed above and re-deploy.
```

## Important Notes

- `--include-fragments` enables anchor/fragment checking (critical for internal navigation)
- lychee downloads full HTML to verify anchors exist on remote pages
- Exit code 0 = all OK, exit code 2 = errors found
- Some JavaScript-rendered anchors cannot be validated (known limitation)
- External sites may rate-limit or block requests - retry if needed
- This checks the LIVE PROD site - ensure changes are deployed first
