# Check and Update Internal Links

Verify internal links database integrity and update with new pages/anchors. This command:

1. **Checks** for missing anchors (in database but not in HTML) - indicates broken links
2. **Finds** new anchors (in HTML but not in database) - can be added to tracking
3. **Updates** the database with new entries (after confirmation)

The internal links database (`internal_links_{lang}.json`) tracks:
- **Main pages**: `/` (EN), `/ru/`, `/ua/`, `/es/`
- **Anchors** - section IDs within each main page (e.g., `#reliable-gestors`, `#надежные-хесторы`)

**Note**: ITA has one main index page per language. All content is organized as sections (anchors) on these pages.

Run this after adding/modifying content or before deploying to ensure all internal links work.

## Configuration Files

- `_resources/internal_links_en.json` - English (default)
- `_resources/internal_links_ru.json` - Russian
- `_resources/internal_links_ua.json` - Ukrainian
- `_resources/internal_links_es.json` - Spanish

## File Format (internal_links_{lang}.json)

```json
{
  "description": "All internal links for Russian version",
  "language": "ru",
  "generated_at": "2025-01-21",
  "pages": [
    {
      "path": "/ru/",
      "url": "https://itautonomos.com/ru/",
      "title": "Autónomo - Полное Руководство",
      "description": "Main page with all sections about autónomo in Spain",
      "anchors": ["надежные-хесторы", "регистрация-autónomo-пошагово", ...]
    }
  ]
}
```

## Path to HTML Mapping

Convert `path` from JSON to HTML file:
- `/` → `_site/index.html`
- `/ru/` → `_site/ru/index.html`
- `/ua/` → `_site/ua/index.html`
- `/es/` → `_site/es/index.html`

## Excluded ID Patterns

The following ID patterns are **excluded** from anchor tracking (technical IDs, not content anchors):

| Pattern | Description |
|---------|-------------|
| `*-contact-form` | Contact form element IDs |
| `hs-script-loader` | HubSpot script loader ID |
| UUID patterns | Auto-generated IDs like `f47ac10b-58cc-4372-a567-0e02b2c3d479` |

## Prerequisites

**IMPORTANT**: The `_site/` directory must exist with compiled HTML files. If it doesn't exist, run:
```bash
bundle exec jekyll build
```

## Instructions

1. **Check if _site/ exists**
   ```bash
   ls _site/index.html
   ```
   If files don't exist, inform the user to run `bundle exec jekyll build` first.

2. **For each language**, read `internal_links_{lang}.json`

3. **For each page in the `pages` array**:
   - Convert `path` to HTML file path
   - Extract anchors from HTML using:
     ```bash
     grep -oE 'id="[^"]+"' HTML_FILE | sed 's/id="//;s/"$//' | grep -v -E '(-contact-form$|^hs-script-loader$|^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$)' | sort -u
     ```
   - Compare with `anchors` array for that page
   - Identify NEW anchors (in HTML but not in database)
   - Identify REMOVED anchors (in database but not in HTML)

4. **Run all page scans in parallel** using the Task tool for efficiency.

## Output Format

### Summary Table

```
## Anchor Check & Update Results

### English (internal_links_en.json)

| Page | In Database | In HTML | New | Removed |
|------|-------------|---------|-----|---------|
| / (main) | 150 | 150 | 0 | 0 |

### Russian (internal_links_ru.json)

| Page | In Database | In HTML | New | Removed |
|------|-------------|---------|-----|---------|
| /ru/ (main) | 151 | 153 | 2 | 0 |
```

### Missing/Removed Anchors Report (if any)

**IMPORTANT**: Missing anchors indicate potential broken links!

```
## ❌ Missing Anchors (in database but NOT in HTML)

These anchors may have been renamed without adding legacy anchors. URLs pointing to them will break!

### RU - /ru/ (1 missing)

1. `старое-название`
   - URL: https://itautonomos.com/ru/#старое-название
   - Fix: Add legacy anchor before renamed heading:
     ```markdown
     <span id="старое-название" class="legacy-anchor"></span>
     ## Новое Название
     ```
```

### New Anchors Report (if any)

```
## 🆕 New Anchors Found (in HTML but not in database)

These can be added to the database for future tracking.

### RU - /ru/ (2 new)

1. `новый-раздел`
2. `дополнительная-информация`
```

## Update Process

After showing the report:

1. **If missing anchors found**: Stop and warn the user. These need legacy anchors BEFORE proceeding.

2. **If new anchors found** (and no missing): Ask user if they want to add them to the database

3. **If user confirms**: Update the JSON files:
   - Find the page object in `pages` array
   - Add new anchors to that page's `anchors` array
   - Sort the array alphabetically
   - Update `generated_at` to current date

## Final Summary

```
## Final Status

✅ **ALL CHECKS PASSED** - No missing anchors, database is up to date.
```

OR

```
## Final Status

✅ **DATABASE UPDATED** - All checks passed.

Updated files:
- _resources/internal_links_ru.json: /ru/ (+2 anchors)
- _resources/internal_links_ua.json: /ua/ (+1 anchor)
```

OR

```
## Final Status

❌ **MISSING ANCHORS FOUND** - X anchor(s) missing across Y page(s).

Action required: Add legacy anchors for the missing IDs listed above, then rebuild and re-run this command.
```

## Important Notes

- This command ADDS new anchors to the database, it does NOT remove existing ones
- Missing/removed anchors need manual review (may need legacy anchors)
- Always rebuild (`bundle exec jekyll build`) before running this command
- New anchors should be reviewed to ensure they're intentional
