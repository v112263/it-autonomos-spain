---
name: tests-local-test-local-site-links
description: "Check all links and anchors on the LOCAL development server using lychee link checker."
disable-model-invocation: true
user-invocable: false
allowed-tools: Read, Glob, Grep, Bash, Task
---

# Check Local Site Links

Check all links and anchors on the **LOCAL** development server (http://localhost:4000) using lychee link checker.

## Prerequisites

1. **lychee** must be installed:
   ```bash
   brew install lychee
   ```

2. **LOCAL Jekyll server must be running**:
   ```bash
   bundle exec jekyll serve
   ```
   The server should be accessible at http://localhost:4000

## URLs to check

### Main pages (index)
1. http://localhost:4000/ (English)
2. http://localhost:4000/ru/ (Russian)
3. http://localhost:4000/ua/ (Ukrainian)
4. http://localhost:4000/es/ (Spanish)

## Instructions

1. **Check if lychee is installed**:
   ```bash
   which lychee || echo "lychee not found - install with: brew install lychee"
   ```

2. **Check if LOCAL server is running**:
   ```bash
   curl -s -o /dev/null -w "%{http_code}" http://localhost:4000/ || echo "LOCAL server not running - start with: bundle exec jekyll serve"
   ```

3. **Run lychee for each page** with anchor fragment checking enabled:
   ```bash
   lychee --include-fragments --exclude "ec.europa.eu/taxation_customs/vies" --exclude "bit.ly" "URL" 2>&1
   ```

   The `--exclude` flags skip:
   - EU VIES VAT validation page (uses JavaScript routing - false positive)
   - bit.ly links (tested separately in `/tests-prod-test-bitly-links` to avoid inflating Bitly analytics)

4. **Run all 4 checks in parallel** using the Task tool for efficiency, or run sequentially:
   ```bash
   # Example for one page:
   lychee --include-fragments --exclude "ec.europa.eu/taxation_customs/vies" --exclude "bit.ly" "http://localhost:4000/ru/" 2>&1
   ```

5. **Parse the output** for each page:
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
## LOCAL Site Link Check Results

| Page | Total | OK | Redirects | Excluded | Errors | Status |
|------|-------|-----|-----------|----------|--------|--------|
| EN Index (/) | 150 | 138 | 10 | 2 | 0 | ✅ |
| RU Index (/ru/) | 171 | 158 | 10 | 3 | 0 | ✅ |
| UA Index (/ua/) | 165 | 152 | 10 | 3 | 0 | ✅ |
| ES Index (/es/) | 150 | 138 | 10 | 2 | 0 | ✅ |
```

**Note**: Total = OK + Redirects + Excluded + Errors

### Errors Report (if any)

```
## ❌ Errors Found

### RU Index (/ru/)
1. [ERROR] http://localhost:4000/ru/#broken-anchor | Cannot find fragment
2. [ERROR] https://broken-link.com | Network error

### Action Required
- Fix broken links listed above
- For anchor errors: verify the target section exists on the page
```

## Final Status

End with a clear summary:

```
## Final Status

✅ **ALL LOCAL LINKS VALID** - All 4 pages passed (X total links, Y anchors verified)
```

OR

```
## Final Status

❌ **LOCAL ISSUES FOUND** - X broken link(s) across Y page(s)

Action required: Fix the errors listed above before deploying.
```

## Important Notes

- `--include-fragments` enables anchor/fragment checking (critical for internal navigation)
- lychee downloads full HTML to verify anchors exist on pages
- Exit code 0 = all OK, exit code 2 = errors found
- Some JavaScript-rendered anchors cannot be validated (known limitation)
- External sites may rate-limit or block requests - retry if needed
- **LOCAL server must be running** at http://localhost:4000 before running this check
- **Important**: Use `localhost` (not `127.0.0.1`) to match Jekyll's generated URLs and get accurate link counts
- Use this to validate changes BEFORE deploying to PROD
