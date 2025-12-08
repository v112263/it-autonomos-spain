# Check Bit.ly Redirects

Verify that all bit.ly shortlinks redirect to the expected destinations.

## Instructions

1. Read the links configuration from `_resources/bitly_links.json`

2. For each link in the `links` array, check the redirect destination:
   ```bash
   curl -Ls -o /dev/null -w '%{url_effective}' "BITLY_URL"
   ```

3. Validate each link:
   - **URL check**: The final URL (without anchor part) must match `expected_url` EXACTLY
   - **Anchor check** (if `expected_anchor` is set): Perform additional anchor validation (see below)

4. Run checks in parallel where possible for efficiency

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

Create a report with TWO tables:

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

| Category | Checked | Status |
|----------|---------|--------|
| External Services | X links | ✅ All working / ❌ Y issues |
| ITAutonomos.com | X links | ✅ All working / ❌ Y issues |
| **TOTAL** | **X links** | ✅ **All working** / ❌ **Y issues** |
```

If all links work: "✅ ALL BIT.LY LINKS ARE WORKING CORRECTLY"
If problems exist: List each problem with actionable next steps.

## Important Notes

- ALL URLs must match EXACTLY (no partial matching)
- Anchor validation is critical - a missing anchor means users land on the wrong section
- Some external sites may block curl - note these but don't mark as errors
- External services: Telegram, Xolo, Revolut, Wise, GitHub, Instagram, YouTube, Buy Me a Coffee, Hacienda (petete.tributos)
- ITAutonomos links: all links containing "itautonomos.com"
