# Add Internal Links to Article

Analyze an article, find relevant internal links from BOTH projects (ITA and SLG), and automatically insert them into the file.

Internal links include:
- **Page links** - links to standalone pages (e.g., `/ru/`, `/ru/mortgage/`)
- **Anchor links** - links to sections within pages (e.g., `#надежные-хесторы` or `/ru/mortgage/#неделя-1-первый-поход-в-банк-и-поиск-квартиры`)

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
   - **Anchor links**: point to a section on a page (e.g., `#надежные-хесторы` or `/ru/mortgage/#документы-для-ипотеки`)
   - **Page links**: point to standalone pages (e.g., `/ru/mortgage/`)
   - Internal links format: `[text](#anchor)` or `[text](/path/)`
   - External links format: `[text](https://site.com/path/){:target="_blank"}` or `[text](https://site.com/path/#anchor){:target="_blank"}`

### Phase 2: Internal Links (Current Project - ITA)

4. **Load ITA links database**:
   - `_resources/internal_links_{lang}.json` - contains all pages with anchors

5. **Understand the internal_links_{lang}.json structure**:
   ```json
   {
     "pages": [
       {
         "path": "/",
         "url": "https://itautonomos.com/",
         "title": "IT Autonomos Spain - Complete Guide",
         "description": "Main page with all sections about autónomo and freelancing in Spain",
         "anchors": ["reliable-gestors", "autónomo-registration-step-by-step", ...]
       },
       {
         "path": "/en/mortgage/",
         "url": "https://itautonomos.com/en/mortgage/",
         "title": "Obtaining a mortgage in Spain as autónomo",
         "description": "Personal experience of obtaining a mortgage in Spain as autónomo",
         "anchors": ["week-1-first-visit-to-the-bank-and-apartment-search", ...]
       }
     ]
   }
   ```
   - Each page has a path, url, title, description, and list of anchors
   - Use path + anchor to create links like `/en/mortgage/#week-1-first-visit-to-the-bank-and-apartment-search`
   - For main page (EN default), just use `#anchor`

6. **ITA base URLs by language**:
   - Russian: `/ru/`
   - Ukrainian: `/ua/`
   - English: `/` (default language)
   - Spanish: `/es/`

7. **Analyze the article content** for ITA-relevant topics:
   - Autónomo/freelancer topics: taxes, gestors, invoicing, business registration
   - Look for mentions that correspond to existing ITA sections
   - Consider what additional reading would genuinely help the reader

8. **Match terms to ITA pages and anchors**:
   - Find phrases that relate to available pages or anchors
   - Use semantic matching based on page/anchor titles and descriptions
   - Can link to: page only (`/ru/mortgage/`), anchor on main page (`#надежные-хесторы`), or anchor on subpage (`/ru/mortgage/#неделя-1-первый-поход-в-банк-и-поиск-квартиры`)

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
