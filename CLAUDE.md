# Claude Code Project Guide

This document contains essential guidelines for working on the Autónomo and SL Spain Documentation project.

## CRITICAL FOR AI - READ FIRST

**BEFORE any content work, read this:**

### IRON RULE FOR CONTENT WORKFLOW

**STEP 1: Create/Modify ONLY Russian version**
1. **MANDATORY**: Read 3-4 similar articles from `_includes/ru/`
2. **MANDATORY**: Analyze style, phrases, sentence structures
3. **MANDATORY**: Write/modify ONLY Russian version matching author's style
4. **MANDATORY**: Wait for user approval

**STEP 2: Translation (ONLY after approval!)**
- **FORBIDDEN** to translate before Russian version is approved
- **FORBIDDEN** to translate automatically without request
- Translate only when user explicitly asks
- Translate to UA/EN/ES from approved Russian version

### Why this is critical?

- Russian is the single source of truth
- Author's style must be identical across all articles
- User approves Russian version before translation
- Without analyzing existing articles, style will differ

**THIS RULE HAS THE HIGHEST PRIORITY!**

## Content Creation & Translation Protocol

### Creating or Modifying Content (RUSSIAN ONLY)

**Step 1: Analyze Existing Style**
```
Read 3-4 similar articles from `_includes/ru/` and analyze the distinctive voice:
- Conversational, practical, experience-based tone
- Personal experience sharing approach
- Direct, actionable guidance with real-world examples
- Balance of friendliness and professionalism
- Common phrases, expressions, and sentence patterns
- How technical terms are explained
- Level of formality and characteristic author's patterns
```

**Step 2: Write/Modify ONLY Russian Version**
- Write in Russian matching analyzed style
- Match personal, experience-based tone
- Use similar expressions and patterns
- Maintain identical formality level
- Replicate author's explanation approach

**Step 3: STOP and Wait for Approval**
- Present ONLY Russian version to user
- Wait for explicit approval or changes
- Do NOT translate or update other languages

**Goal**: New/modified content must be indistinguishable from existing articles in writing style.

### Translation Workflow (AFTER Russian Approval)

**ONLY proceed when user explicitly requests translation!**

**When user approves Russian version and asks to translate:**

1. Translate to Ukrainian (from approved RU)
2. Translate to English (from approved RU)
3. Translate to Spanish (from approved RU)
4. Update all 4 index files if structure changed
5. Verify all navigation and links work

**Translation rules:**
- Keep the same structure and content for each language
- Use the same tone and style as in the original Russian text
- Preserve markdown markup exactly as in the Russian original
- Never create cross-translations (e.g., EN→ES or UA→EN) - always from Russian
- DO NOT translate English/Spanish terms - keep them as-is

**Files to sync:**
- `_includes/en/**/*`
- `_includes/ru/**/*`
- `_includes/ua/**/*`
- `_includes/es/**/*`
- `index.md`, `ru/index.md`, `ua/index.md`, `es/index.md` (if structure changed)

## Project Overview

A Jekyll-based multilingual documentation website about being an autónomo or SL in Spain, deployed on GitHub Pages. The site provides comprehensive guidance in four languages: Russian (primary), Ukrainian, English, and Spanish.

**Live site**: https://itautonomos.com

## Project Structure

```
.
├── index.md                    # English index (main entry point)
├── ru/index.md                 # Russian index
├── ua/index.md                 # Ukrainian index
├── es/index.md                 # Spanish index
├── en/                         # English article pages
├── ru/                         # Russian article pages
├── ua/                         # Ukrainian article pages
├── es/                         # Spanish article pages
├── _includes/
│   ├── common/                 # Shared assets (CSS, JS, forms)
│   │   ├── common.css         # All site styles
│   │   └── scripts.js         # All site scripts
│   ├── en/                    # English article includes
│   ├── ru/                    # Russian article includes
│   ├── ua/                    # Ukrainian article includes
│   └── es/                    # Spanish article includes
├── _layouts/                   # Jekyll layouts
└── _img/                       # Images and media assets
```

### Content Organization

- Each language maintains **identical structure and organization**
- Articles are stored in `_includes/{lang}/` directories, organized by topic
- Index files (`*/index.md`) serve as navigation hubs linking to all articles
- Common assets (CSS, JS, forms) are in `_includes/common/`

## Translation Standards

### Language-Specific Guidelines

**CRITICAL RULE**: **Do not translate English and Spanish terms or phrases**

This is a universal rule that applies to ALL English and Spanish terminology, not just the examples below. Keep them in the original language across all site versions.

### Standard Terminology Examples

Common terms you'll encounter (transliterate in Russian/Ukrainian):

- **gestor/gestors** → хестор/хесторы (RU), хестор (UA)
- **autónomo** → аутономо (RU/UA)
- **cita** → сита (RU), сіта (UA)

But remember: ALL English and Spanish terms should remain untranslated according to the rule above.

### Title Formatting

Use **Sentence case** for all titles in all languages:
- CORRECT: "This is an example of sentence case"
- WRONG: "This Is An Example Of Title Case"

Apply consistently across all language versions.

## Link Formatting

### Internal Links

**Always use Jekyll liquid tags** for internal links:

```markdown
{% raw %}{% link path/to/file.md %}{% endraw %}
```

### External Links

Use standard Markdown with target attribute (always include `{:target="_blank"}` for external links):

```markdown
[Link text](https://example.com){:target="_blank"}
```

### Telegram Links

The site uses **different Telegram links for different languages**:

- **English/Spanish chat:** `https://bit.ly/it-autonomos-spain-eng`
- **Russian/Ukrainian chat:** `https://bit.ly/it-autonomos-es`
- **Channel (all languages):** `https://bit.ly/autonomo-and-sl-channel`

Always use the correct link for the language version you're working on.

## Code Standards

### CSS
- All styles in **one file**: `_includes/common/common.css`
- Centralized styling approach
- Use consistent naming conventions
- Ensure cross-browser compatibility

### JavaScript
- All scripts in **one file**: `_includes/common/scripts.js`
- Keep code organized and well-commented
- Follow modern JavaScript best practices
- Ensure cross-browser compatibility

### Best Practices
- Maintain separation of concerns between content, presentation, and behavior
- Keep all common assets in `_includes/common/`
- Never create separate CSS/JS files - always use the centralized files

## Partner Profile Language Ordering

When displaying partner/gestor/lawyer profiles, order languages by relevance to the current site version's audience:

1. **First**: Current site language (if partner speaks it)
2. **Then**: Linguistically/geographically close languages (e.g., Russian for Ukrainian site)
3. **Finally**: Other languages, with global lingua francas last

**Example for Ukrainian site:**
- Partner speaks EN, ES, RU → Order: UA (if spoken), RU (linguistically close), EN, ES
- Partner doesn't speak UA → Order: RU (most relevant), EN, ES

Apply consistently across all partners; don't hardcode exceptions.

## Development Standards

### Content Quality
- Provide accurate, up-to-date information about Spanish autonomo and SL
- Maintain professional tone with clear explanations
- Include practical examples and real-world guidance
- Use conversational, practical, experience-based voice
- Ensure responsive design and accessibility
- Optimize for search engines and user experience

### Technical Quality
- Follow Jekyll best practices
- Maintain clear separation between content and presentation
- Ensure responsive design works across all devices

## Content Update Checklist

### For New/Modified Content (Russian Only)

- [ ] Read 3-4 similar articles from `_includes/ru/`
- [ ] Analyzed author's writing style and patterns
- [ ] Written/modified ONLY Russian version
- [ ] Matched author's tone and style
- [ ] EN/ES terms remain untranslated
- [ ] Titles use Sentence case
- [ ] Internal links use `{% raw %}{% link path.md %}{% endraw %}`
- [ ] External links have `{:target="_blank"}`
- [ ] Correct Telegram links for Russian version
- [ ] Markdown formatting correct
- [ ] **STOPPED - waiting for user approval**

### For Translation (After RU Approval)

- [ ] User explicitly approved Russian version
- [ ] User explicitly requested translation
- [ ] Translated to UA from approved RU
- [ ] Translated to EN from approved RU
- [ ] Translated to ES from approved RU
- [ ] EN/ES terms remain untranslated in all versions
- [ ] All formatting preserved exactly
- [ ] Correct Telegram links for each language
- [ ] Updated all 4 index files (if structure changed)
- [ ] All navigation links work in all languages
