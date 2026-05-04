---
name: tests-prod-test-bitly-links
description: "Verify bit.ly shortlinks redirect correctly and check for untracked links on the site."
user-invocable: false
allowed-tools: Read, Glob, Grep, Bash, WebFetch, Task
---

# Check Bit.ly Redirects

Verify that all bit.ly shortlinks redirect to the expected destinations AND that all bit.ly links on the site are tracked in the database.

## Instructions

### Part 1: Coverage Check (find untracked bit.ly links)

1. **Scan the PROD site** for all bit.ly links. Fetch these pages and extract all `bit.ly` URLs:
   - https://itautonomos.com/
   - https://itautonomos.com/ru/
   - https://itautonomos.com/ua/
   - https://itautonomos.com/es/

   ```bash
   # Example: extract all bit.ly links from a page
   curl -s "URL" | grep -oE 'https?://bit\.ly/[a-zA-Z0-9_-]+' | sort -u
   ```

2. **Read the database** from `_resources/bitly_links.json` and extract all `bitly` URLs.

3. **Compare**: Find any bit.ly links that are ON THE SITE but NOT IN THE DATABASE. These are "untracked" links that won't be validated.

4. **Report untracked links** (if any) - this is a WARNING, not a blocker, but should be fixed.

### Part 2: Redirect Validation (verify tracked links work)

5. Read the links configuration from `_resources/bitly_links.json`

6. For each link in the `links` array, check the redirect destination:
   ```bash
   curl -Ls -o /dev/null -w '%{url_effective}' "BITLY_URL"
   ```

7. Validate each link:
   - **URL check**: The final URL (without anchor part) must match `expected_url` EXACTLY
   - **Anchor check** (if `expected_anchor` is set): Perform additional anchor validation (see below)

8. Run checks in parallel where possible for efficiency

## URL Validation Logic

For all links, compare the final URL with `expected_url`:

```bash
FINAL_URL=$(curl -Ls -o /dev/null -w '%{url_effective}' "BITLY_URL")

# For links with anchors, compare base URL
BASE_URL="${FINAL_URL%%#*}"

if [ "$BASE_URL" != "$EXPECTED_URL" ]; then
    echo "ERROR: URL mismatch! Expected: $EXPECTED_URL, Got: $BASE_URL"
fi
```

## Anchor Validation Logic

For links with `expected_anchor`, perform TWO additional checks:

```bash
# Extract and decode anchor from URL
ACTUAL_ANCHOR=$(python3 -c "import urllib.parse; print(urllib.parse.unquote('${FINAL_URL#*#}'))")

# CHECK 1: Verify the anchor in URL matches expected_anchor
# This catches: bit.ly was changed to point to a different section
if [ "$ACTUAL_ANCHOR" != "$EXPECTED_ANCHOR" ]; then
    echo "ERROR: Anchor mismatch! Expected: $EXPECTED_ANCHOR, Got: $ACTUAL_ANCHOR"
fi

# CHECK 2: Verify the anchor actually exists on the page
# This catches: the section was renamed/removed on the website
if ! curl -s "$BASE_URL" | grep -q "id=\"$ACTUAL_ANCHOR\""; then
    echo "ERROR: Anchor '$ACTUAL_ANCHOR' does not exist on the page!"
fi
```

**Three failure modes this catches:**
1. **bit.ly redirect changed to wrong URL** -> base URL won't match `expected_url`
2. **bit.ly redirect changed to wrong section** -> anchor in URL won't match `expected_anchor`
3. **Website section renamed/removed** -> anchor won't exist in page HTML

## Output Format

Create a report with THREE sections:

### Section 0: Coverage Check (Untracked Links)

```
## Coverage Check

✅ **All bit.ly links on site are tracked** - X unique links found, all in database
```

OR

```
## Coverage Check

⚠️ **Untracked bit.ly links found** - These links are on the site but NOT in bitly_links.json:

| bit.ly URL | Found on page(s) |
|------------|------------------|
| https://bit.ly/example | /, /ru/ |

**Action required**: Add these links to `_resources/bitly_links.json` to enable validation.
```

### Section 1 & 2: Redirect Validation

### Table 1: External Services
Links that redirect to external services (Telegram, Xolo, Revolut, Wise, GitHub, Instagram, YouTube, Buy Me a Coffee, Hacienda consultas, etc.)

| bit.ly | Destination | Status |
|--------|-------------|--------|
| autonomo-and-sl-channel | t.me/autonomo_and_sl | ✅ or ❌ |
| xolosignup | xolo.io/... | ✅ or ❌ |
| ... | ... | ... |

### Table 2: ITAutonomos.com Links
Links that redirect to itautonomos.com (with anchor validation where applicable)

| bit.ly | Page | Anchor | Anchor exists | Status |
|--------|------|--------|---------------|--------|
| autonomo-manual | /ru/ | - | - | ✅ or ❌ |
| reliable-gestors-ru | /ru/ | надежные-хесторы | ✅ or ❌ | ✅ or ❌ |
| ... | ... | ... | ... | ... |

### Problems Found (if any)
```
[description]
  Bitly: bitly_url
  Expected URL: expected_url
  Expected anchor: expected_anchor (if applicable)
  Actual URL: actual_final_url
  Issue: [URL mismatch / anchor mismatch / anchor not found on page]
```

## Summary

End with a clear summary in this format:

```
## Summary

| Check | Result | Status |
|-------|--------|--------|
| Coverage (untracked links) | X on site, all tracked | ✅ / ⚠️ Y untracked |
| External Services | X links validated | ✅ All working / ❌ Y issues |
| ITAutonomos.com | X links validated | ✅ All working / ❌ Y issues |
| **TOTAL** | **X links** | ✅ **All passed** / ❌ **Issues found** |
```

If all checks pass: "✅ ALL BIT.LY CHECKS PASSED"
If untracked links found: "⚠️ UNTRACKED LINKS FOUND - add to database"
If redirect problems exist: "❌ REDIRECT ISSUES FOUND - fix immediately"

## Important Notes

- **Coverage check is critical**: bit.ly links are excluded from lychee checks, so untracked links would never be validated
- ALL URLs must match EXACTLY (no partial matching)
- Anchor validation is critical - a missing anchor means users land on the wrong section
- Some external sites may block curl - note these but don't mark as errors
- External services: Telegram, Xolo, Revolut, Wise, GitHub, Instagram, YouTube, Buy Me a Coffee, Hacienda (petete.tributos)
- ITAutonomos links: all links containing "itautonomos.com"
