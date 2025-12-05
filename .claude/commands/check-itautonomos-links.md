# Check Links on itautonomos.com

Check all links and anchors on the deployed website using W3C Link Checker.

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

For each URL above:

1. Use WebFetch to check the W3C Link Checker results:
   - URL pattern: `https://validator.w3.org/checklink?uri=<encoded-url>`
   - Extract: number of anchors found, broken links, errors

2. Run all 8 checks in parallel using the Task tool for efficiency.

3. Create a summary table with:
   - Page type (Index / Mortgage)
   - Language
   - Anchors count
   - Broken links (if any)
   - Errors (if any)

4. Report any broken links or errors that need attention.

## Expected output

A clear summary showing the health of all 8 pages (4 index + 4 mortgage), highlighting any issues that need fixing.

**Important**: Explicitly state whether all anchor links are valid across all pages. Example:
- "✅ All anchor links are valid in all 8 pages (4 index + 4 mortgage)" (if no issues)
- "Broken anchor links found in: [list pages and specific broken anchors]" (if issues exist)
