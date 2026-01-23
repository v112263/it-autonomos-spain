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
- Heading levels (H2, H3, etc.)

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

- EN: `<p class="last-updated">Last updated: January 23, 2026</p>`
- RU: `<p class="last-updated">Последнее обновление: 23 января 2026</p>`
- UA: `<p class="last-updated">Останнє оновлення: 23 січня 2026</p>`
- ES: `<p class="last-updated">Última actualización: 23 de enero de 2026</p>`

## Pre-completion Checklist

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

## Output

After completing translations, summarize:
- Which files were created/updated
- Any issues encountered
- Reminder to test links locally
