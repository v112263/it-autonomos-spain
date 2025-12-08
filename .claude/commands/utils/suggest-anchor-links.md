# Add Anchor Links to Article

Analyze an article, find relevant internal anchor links, and automatically insert them into the file.

## Input

$ARGUMENTS

The input should be a path to an article file (e.g., `_includes/ru/some-article.md`).

## Instructions

1. **Read the article** from the specified path

2. **Determine article language and page type** from the path:
   - `_includes/ru/` or `ru/` → Russian, main page
   - `_includes/ua/` or `ua/` → Ukrainian, main page
   - `_includes/en/` or `en/` → English, main page
   - `_includes/es/` or `es/` → Spanish, main page
   - `*/mortgage/*` → mortgage page

3. **Load the correct anchors database**:
   - For main pages: `.claude/commands/_data/expected_anchors_main_{lang}.json`
   - For mortgage pages: `.claude/commands/_data/expected_anchors_mortgage_{lang}.json`
   - Where `{lang}` is: `ru`, `ua`, `en`, or `es`

4. **Understand what anchors represent**:
   - Each anchor is an ID of a heading/section in the document
   - The anchor name reflects the section topic (e.g., `надежные-хесторы` = section about reliable gestors)
   - Links format: `[visible text](#anchor-id)`

5. **Analyze the article content**:
   - Identify terms, concepts, and topics mentioned in the article
   - Look for mentions that correspond to existing document sections
   - Consider what additional reading would genuinely help the reader

6. **Match terms to anchors**:
   - Find phrases in the article that relate to available anchors
   - Use semantic matching - understand what each anchor's section is about
   - The anchor name itself describes the section topic

7. **Apply conservative linking rules**:
   - **Max 3-5 links per article** - quality over quantity
   - **One link per term** - if a term appears multiple times, link only the first meaningful occurrence
   - **No redundant links** - don't link terms already linked in the article
   - **No self-links** - don't link to the section the article itself belongs to
   - **Prefer early mentions** - link terms closer to the beginning of the article
   - **Context matters** - only link when it genuinely helps the reader
   - **Natural phrasing** - the linked text should read naturally in context

8. **Edit the file directly**:
   - Use the Edit tool to insert anchor links into the article
   - Apply each change one by one
   - Do NOT ask for confirmation - just make the edits

9. **Output summary**:
   After making edits, provide a brief summary:

   ## Added Links

   | Text linked | Anchor | Reason |
   |-------------|--------|--------|
   | phrase | #anchor-id | why this link helps the reader |

   ## Skipped

   - Terms considered but not linked (and why)

## Example

For a Russian article about tax optimization, after editing:

**Added Links:**

| Text linked | Anchor | Reason |
|-------------|--------|--------|
| хестору | #надежные-хесторы | Helps reader find verified gestors |
| IRPF | #irpf-подоходный-налог | Links to detailed tax explanation |
| Renta | #годовая-декларация-renta | Links to annual declaration info |

**Skipped:**
- "налоги" - too generic, multiple related sections
- "декларации" - already in context of Renta discussion
- "оптимизация налогов" - would be a self-link (article topic)
