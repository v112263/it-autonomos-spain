# Add Bit.ly Links to Database

Add new bit.ly links to the database file.

## Input

$ARGUMENTS

Parse the input in any format - extract the essential information:
- **bitly** - the bit.ly short link
- **expected_url** - where it should redirect to
- **description** - what this link is for
- **expected_anchor** (optional) - if URL contains `#anchor`, split it out

## Instructions

1. Read current database from `.claude/commands/_data/bitly_links.json`

2. **IMPORTANT: Analyze existing entries in the database to understand the format patterns for all fields (URL format, description style, etc.). New entries MUST follow the same format as similar existing entries.**

3. Parse user input intelligently - it may be in any format (list, free text, etc.)

4. For each link found:
   - Normalize bitly to `https://bit.ly/...` format
   - If URL has `#anchor`, split into `expected_url` + `expected_anchor`
   - Check for duplicates in database

5. Add new links to the end of the `links` array (keep 2-space indentation)

6. Save updated JSON

7. Show summary table of added links

8. Remind user to run `/check-bitly-links` to verify
