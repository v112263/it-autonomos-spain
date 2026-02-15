---
name: content-translate-article
description: "Translate approved Russian content to Ukrainian, English, and Spanish. Use when user asks to translate an article or content to other languages, or after an article has been approved in Russian."
argument-hint: "[article path or topic]"
allowed-tools: Read, Glob, Grep
---

# Translate Article

Translate approved Russian content to Ukrainian, English, and Spanish.

## Input

The user will specify what to translate: $ARGUMENTS

## CRITICAL: Prerequisites

**STOP if any of these are not met:**

1. Russian version MUST be approved by user first
2. User MUST explicitly request translation
3. NEVER translate automatically after writing Russian version

## Translation Order

Always translate FROM Russian. Never cross-translate (e.g., EN→ES).

1. Russian (source) → Ukrainian
2. Russian (source) → English
3. Russian (source) → Spanish

## Translation Rules

### Preserve Exactly
- Markdown structure and formatting
- All links (internal and external)
- Code blocks and technical markup
- Heading levels (H1, H2, H3, etc.)

### DO NOT Translate
- English/Spanish terms: autónomo, gestor, NIE, Hacienda, Seguridad Social, Modelo, SL, etc.
- URLs and link paths
- Code/technical identifiers
- Brand names

### Punctuation
- Use only short hyphen "-" in ALL languages
- Never use em dash "—" or en dash "–"

### Titles
- Use **Sentence case** in ALL languages
- CORRECT: "How to become autónomo in Spain"
- WRONG: "How To Become Autónomo In Spain"

### Tone
- Maintain the same conversational, personal tone as Russian original
- Don't make translations more formal or "proper"

## Language-Specific Rules

### Ukrainian (UA)
- Transliterate Spanish terms: gestor → хестор, cita → сіта, autónomo → аутономо
- Don't use Russian words - use Ukrainian equivalents

### English (EN)
- Keep Spanish terms in original: gestor (not "tax advisor"), autónomo (not "self-employed")
- Use American English spelling
- Keep conversational tone, don't make it sound like documentation

### Spanish (ES)
- Most natural since terms are already in Spanish
- Keep the informal, friendly tone (tú form, not usted)
- Don't over-formalize

## Link Formatting

### Internal Links
Use Jekyll liquid tags:
```markdown
{% raw %}{% link path/to/file.md %}{% endraw %}
```

### External Links
Use standard Markdown with target attribute:
```markdown
[Link text](https://example.com){:target="_blank"}
```

### Legacy Anchors
When translating content where a heading was renamed, preserve the legacy anchor:
```markdown
<span id="old-heading-id" class="legacy-anchor"></span>
## New Heading Name
```
Copy legacy anchors exactly as they appear in the Russian source.

## Telegram Links - LANGUAGE SPECIFIC!

**CRITICAL**: Use correct Telegram link for each language:

- **RU version**: `https://bit.ly/it-autonomos-es`
- **UA version**: `https://bit.ly/it-autonomos-es`
- **EN version**: `https://bit.ly/it-autonomos-spain-eng`
- **ES version**: `https://bit.ly/it-autonomos-spain-eng`
- **Channel (all)**: `https://bit.ly/autonomo-and-sl-channel`

## Partner Profiles - Language Ordering

**CRITICAL**: When translating partner/gestor/lawyer profiles, REORDER the "Languages" field for each site version.

Order by relevance to the audience:
- **RU site**: русский, украинский, английский, испанский
- **UA site**: українська, російська, англійська, іспанська
- **EN site**: English, Spanish, Russian, Ukrainian
- **ES site**: español, inglés, ruso, ucraniano

**DO NOT copy the same order to all versions!**

## Files to Update

### Article content in _includes/
- `_includes/ua/{same-path-as-ru}`
- `_includes/en/{same-path-as-ru}`
- `_includes/es/{same-path-as-ru}`

### Full articles in root language folders (if applicable)
- `ru/{article}/index.md` → `ua/{article}/index.md`, `en/{article}/index.md`, `es/{article}/index.md`

### Index files (Table of Contents)

**CRITICAL**: If the Russian article was added to `ru/index.md`, you MUST add it to ALL other language index files too!

Check `ru/index.md` for any new includes/sections, then add the same structure to:
- `index.md` (EN - default) - with translated heading and `{% raw %}{% include en/... %}{% endraw %}`
- `ua/index.md` - with translated heading and `{% raw %}{% include ua/... %}{% endraw %}`
- `es/index.md` - with translated heading and `{% raw %}{% include es/... %}{% endraw %}`

**This is NOT optional** - all 4 index files must have identical structure.

## Last Updated Date

Update on ALL 4 index pages when content changes:

- EN: `<p class="last-updated">Last updated: February 7, 2026</p>`
- RU: `<p class="last-updated">Последнее обновление: 7 февраля 2026</p>`
- UA: `<p class="last-updated">Останнє оновлення: 7 лютого 2026</p>`
- ES: `<p class="last-updated">Última actualización: 7 de febrero de 2026</p>`

## Workflow

1. **Verify prerequisites** - Russian version approved, user explicitly requested translation
2. **Read the Russian source** - understand content, note any special terms or formatting
3. **Translate to UA** from Russian (not from other translations)
4. **Translate to EN** from Russian
5. **Translate to ES** from Russian
6. **Check Telegram links** - CRITICAL: use correct links per language (RU/UA vs EN/ES)
7. **Check partner profiles** - if translating profiles, reorder languages per site version
8. **Update index files** - if new section in RU index, add to ALL other indexes
9. **Update Last Updated date** - on all 4 index pages
10. **MANDATORY: Complete the Pre-completion Checklist and show verification table**
    - Go through EVERY item in the checklist
    - DO NOT present translations until table is complete

## Pre-completion Checklist (MANDATORY - show results to user)

**CRITICAL**: You MUST go through EVERY item below and show the user a verification table before presenting the translations. Do not skip any items. Format: table with columns "Item | Status (✅/❌/⚠️/N/A) | Comment".

**Translations completed:**
- [ ] Translated to UA from approved RU
- [ ] Translated to EN from approved RU
- [ ] Translated to ES from approved RU

**Language-specific rules:**
- [ ] UA: no Russian words used (Ukrainian equivalents only)
- [ ] EN: American English spelling
- [ ] ES: tú form used (not usted)
- [ ] Conversational tone preserved in all versions (not more formal than RU)

**Terms & formatting:**
- [ ] EN/ES terms NOT translated in any version
- [ ] Only short hyphen "-" used (no em dash)
- [ ] All markdown formatting preserved exactly

**Links:**
- [ ] Internal links preserved as `{% link path %}` format
- [ ] Correct Telegram links per language (RU/UA vs EN/ES)
- [ ] All links working in all versions

**Special cases:**
- [ ] Partner profiles: language order adjusted per site version

**Index & dates:**
- [ ] Last-updated date updated on all 4 index pages
- [ ] **Index files**: if new section in RU index → added to EN/UA/ES indexes too

## Required Output Format

Your response MUST include these sections in order:

1. **Checklist Verification Table** - table showing status of EVERY checklist item
2. **Files Updated** - list of all files created or modified
3. **Translation Content** - the actual translations (UA, EN, ES)

**Example format:**

```
## Checklist Verification

| Item | Status | Comment |
|------|--------|---------|
| Translated to UA | ✅ | Done |
| Translated to EN | ✅ | Done |
| Translated to ES | ✅ | Done |
| UA: no Russian words | ✅ | Checked, all Ukrainian |
| Telegram links correct | ✅ | RU/UA: bit.ly/it-autonomos-es, EN/ES: bit.ly/it-autonomos-spain-eng |
| Partner profile languages reordered | N/A | Not a profile translation |
| Index files updated | ✅ | Added to all 4 indexes |
| Last-updated date | ✅ | Updated on all 4 pages |
...

## Files Updated

- `_includes/ua/section/article.md` (created)
- `_includes/en/section/article.md` (created)
- `_includes/es/section/article.md` (created)
- `ua/index.md` (updated - added new section)
- `index.md` (updated - added new section)
- `es/index.md` (updated - added new section)
```

Do NOT skip the verification table - it proves you completed the checklist.

## Output

After completing translations, summarize:
- Which files were created/updated
- Any issues encountered
- Reminder to test links locally
