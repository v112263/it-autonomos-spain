# Add Internal Links to Article

Analyze an article, find relevant internal links from BOTH projects (ITA and SLG), and automatically insert them into the file.

## Input

$ARGUMENTS

The input should be a path to an article file (e.g., `_includes/ru/some-article.md`).

## Instructions

### Phase 1: Setup

1. **Read the article** from the specified path

2. **Determine article language** from the path:
   - `_includes/ru/` or `ru/` → Russian
   - `_includes/ua/` or `ua/` → Ukrainian
   - `_includes/en/` or `en/` → English
   - `_includes/es/` or `es/` → Spanish

3. **Understand link types**:
   - **ITA internal links**: anchor links to sections on main page (e.g., `#надежные-хесторы`). Format: `[text](#anchor)`
   - **SLG external links**: links to SLG pages or sections. Format: `[text](https://spainlifeguide.com/...){:target="_blank"}`

### Phase 2: Internal Links (Current Project - ITA)

**Note**: ITA has one main index page per language with all content as sections (anchors). There are no standalone article pages.

4. **Load ITA links database**:
   - `_resources/internal_links_{lang}.json` - contains anchors for the main page

5. **Understand the internal_links_{lang}.json structure**:
   ```json
   {
     "pages": [
       {
         "path": "/ru/",
         "url": "https://itautonomos.com/ru/",
         "title": "Autónomo - Полное Руководство",
         "anchors": ["надежные-хесторы", "регистрация-autónomo-пошагово", ...]
       }
     ]
   }
   ```

6. **ITA anchor format by language**:
   - Russian: `[text](#anchor)` (resolves to `/ru/#anchor`)
   - Ukrainian: `[text](#anchor)` (resolves to `/ua/#anchor`)
   - English: `[text](#anchor)` (resolves to `/#anchor`)
   - Spanish: `[text](#anchor)` (resolves to `/es/#anchor`)

7. **Analyze the article content** for ITA-relevant topics:
   - Autónomo/freelancer topics: taxes, gestors, invoicing, business registration
   - Look for mentions that correspond to existing ITA sections
   - Consider what additional reading would genuinely help the reader

8. **Match terms to ITA anchors**:
   - Find phrases that relate to available anchors
   - Use semantic matching based on anchor names
   - Link format: `[text](#anchor-name)`

9. **Apply conservative linking rules for internal links**:
   - **Max 3-5 internal links per article** - quality over quantity
   - **One link per term** - link only the first meaningful occurrence
   - **No redundant links** - don't link terms already linked
   - **No self-links** - don't link to the current article/section
   - **Prefer early mentions** - link terms closer to the beginning
   - **Context matters** - only link when it genuinely helps the reader

10. **Edit the file** to add internal links

### Phase 3: External Links (Sibling Project - SLG)

11. **Load SLG links database** from sibling project:
    - `../spain-life-guide/_resources/internal_links_{lang}.json` - contains all pages with anchors

12. **Understand the internal_links_{lang}.json structure**:
    ```json
    {
      "pages": [
        {
          "path": "/",
          "url": "https://spainlifeguide.com/",
          "title": "Main page title",
          "description": "What this page is about",
          "anchors": ["anchor1", "anchor2"]
        },
        {
          "path": "/ru/mortgage/",
          "url": "https://spainlifeguide.com/ru/mortgage/",
          "title": "Ипотека в Испании",
          "anchors": ["документы-для-ипотеки", "пошаговая-инструкция", ...]
        }
      ]
    }
    ```
    - Each page has a path, url, title, description, and list of anchors
    - Use `url` + `#anchor` to create external links

13. **Analyze the article for SLG-relevant topics**:
    - Life in Spain topics: housing, healthcare, documents, legal matters, immigration
    - Use page titles/descriptions from internal_links_{lang}.json for semantic matching
    - Look for mentions that SLG covers but ITA doesn't
    - Consider what SLG-specific info would help the reader

14. **Apply conservative linking rules for external links**:
    - **Max 2-3 external links per article** - even more selective than internal
    - **Only link truly relevant topics** - SLG is about general life in Spain, not business
    - **Don't duplicate** - if topic is covered in ITA, prefer internal link
    - **Skip generic terms** - only link specific SLG topics like immigration lawyers, housing, healthcare, mortgage
    - Can link to: page only (`https://spainlifeguide.com/ru/mortgage/`) or page with anchor (`https://spainlifeguide.com/ru/mortgage/#документы-для-ипотеки`)

15. **Edit the file** to add external links with `{:target="_blank"}`

### Phase 4: Summary

16. **Output summary**:

    ## Added Internal Links (ITA)

    | Text linked | Link | Reason |
    |-------------|------|--------|
    | phrase | #anchor-id | why this link helps |

    ## Added External Links (SLG)

    | Text linked | Full URL | Reason |
    |-------------|----------|--------|
    | phrase | https://spainlifeguide.com/... | why this link helps |

    ## Skipped

    - Terms considered but not linked (and why)

## Example

For an English article about tax optimization, after editing:

**Added Internal Links (ITA):**

| Text linked | Link | Reason |
|-------------|------|--------|
| gestor | #reliable-gestors | Helps reader find verified gestors |
| IRPF | #irpf-income-tax | Links to detailed tax explanation |

**Added External Links (SLG):**

| Text linked | Full URL | Reason |
|-------------|----------|--------|
| my mortgage experience | https://spainlifeguide.com/en/mortgage/ | Personal mortgage experience |
| mortgage documents | https://spainlifeguide.com/en/mortgage/#mortgage-documents | List of required mortgage documents |

**Skipped:**
- "taxes" - too generic, multiple related sections
- "declarations" - already in context of Renta discussion
- "tax optimization" - would be a self-link (article topic)
