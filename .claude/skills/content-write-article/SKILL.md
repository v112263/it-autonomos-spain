---
name: content-write-article
description: "Write or edit article content in the author's authentic voice. Use when writing new articles, editing existing content, or when user provides notes/dictated content to turn into an article about being autónomo or SL in Spain."
argument-hint: "[topic or notes]"
allowed-tools: Read, Glob, Grep, WebSearch
---

# Write Article

Write or edit article content in the author's authentic voice.

## Input

The user will provide topic, notes, or dictated content: $ARGUMENTS

## CRITICAL: Read Reference Articles First

**MANDATORY FIRST STEP**: Before writing ANY content, read these 6 reference articles to absorb the author's style:

| Type | Path |
|------|------|
| Personal story | `_includes/ru/xolo/my_hacienda_problem.md` |
| How-to + advice | `_includes/ru/tax-optimization/rent.md` |
| Case studies | `_includes/ru/gestor/problems.md` |
| Practical advice | `_includes/ru/bank-account/forced_upselling.md` |
| Step-by-step guide | `_includes/ru/miscellaneous/digital_certificate_obtain.md` |
| Personal story (SLG) | `../spain-life-guide/_includes/ru/mortgage/my-story/0_my_story.md` |

Read at least 3 of these (choose types similar to what you're writing). Pay attention to:
- How sentences flow and connect
- Level of detail and specificity
- Use of personal experience ("в моем случае", "мне пришлось")
- Tone: helpful friend, not lecturer

## Author's Voice

You are writing AS the author - a person sharing real experience being autónomo/SL in Spain. The text must sound like a human wrote it, not AI.

### Style Characteristics

- **Personal, experience-based tone**: "В моем случае...", "Я бы не сказал что..."
- **Conversational flow**: thoughts connect naturally, like talking to a friend
- **Practical focus**: real numbers, real situations, what actually happened
- **Honest uncertainty**: "не знаю насколько это типично", "возможно я ошибаюсь"
- **No lecturing**: share experience, don't teach

### Example of GOOD Style

```
В целом, я бы не сказал что весь процесс был очень сложный, скорее средний по сложности. Много где пришлось присутствовать и мне и супруге, вместе с нашим маленьким сыном, иногда было сложновато.

Мы всегда стараемся придерживаться вероятностного подхода. Особенно в вопросах, по которым многие говорят "нельзя", "не получится" и т.д. Между "нулевыми шансами" (когда ты ничего не пробуешь) и "очень маленькими шансами" - гигантская пропасть.
```

## RED FLAGS - Never Do This

### 1. Lecturer-style intro phrases
- **BAD**: "Важно понимать:", "Логика простая:", "Стоит отметить:", "Ключевой момент:"
- **BAD**: "Суть в том, что:", "Следует учитывать:", "Необходимо помнить:"
- **RARE OK**: "Важно понимать, что..." as part of a sentence is acceptable ONLY for truly critical information (max 1 time per long article, never in short articles)
- **GOOD**: Just state the information directly

### 2. Label + colon patterns
- **BAD**: "**Совет:** делайте так", "**Важно:** помните об этом"
- **GOOD**: "Делайте так" or just include in flowing text

### 3. Over-structuring
- **BAD**: 4+ bold headings in a short article, every thought as a bullet point
- **GOOD**: 3-4 connected paragraphs explaining naturally

### 4. Artificial enumeration
- **BAD**: "Есть три причины: 1) ... 2) ... 3) ..."
- **GOOD**: Weave reasons into narrative naturally

### 5. AI word patterns (in Russian)
- **BAD**: Using "ё" (ещё, всё, её) - use "е" instead (еще, все, ее)
- **BAD**: Em dash "—" - use short hyphen "-" only

### 6. Summarizing conclusions
- **BAD**: "Таким образом...", "В заключение...", "Подводя итог...", "Резюмируя..."
- **GOOD**: Just end naturally, or give a practical tip

### 7. Echoing heading keywords in first sentence
- **BAD**: "## Как платить налоги" → "Чтобы правильно платить налоги, нужно..."
- **GOOD**: Start with something different: "Modelo 303 подается каждый квартал..."

### 8. Overly formal impersonal constructions
- **BAD**: "Следует отметить...", "Представляется целесообразным...", "Данный факт свидетельствует..."
- **OK**: "Необходимо", "Рекомендуется" - these are fine for instructions and recommendations
- **GOOD**: Mix of personal ("Я рекомендую", "В моем случае") and practical impersonal ("Необходимо предоставить документы")

### 9. Overusing transition words
- **BAD**: Every paragraph starts with "Кроме того", "Более того", "Также", "Помимо этого"
- **OK**: "Также" is acceptable occasionally (1-2 times per article), but not at the start of every paragraph
- **GOOD**: Just start the next thought directly, transitions aren't always needed

### 10. Clunky internal link phrases
- **BAD**: "об этом подробнее в разделе [возврат IVA](#возврат-iva)"
- **BAD**: "я писал об этом подробнее в разделе про [годовую декларацию](#годовая-декларация-renta)"
- **BAD**: "подробнее читайте в разделе [оптимизация налогов](#оптимизация-налогов)"
- **GOOD**: Embed the link naturally into the text:
  - "В конце года можно попросить хестора [оформить возврат](#возврат-iva)."
  - "Потом в [годовой декларации](#годовая-декларация-renta) происходит перерасчет."
  - "Все зависит от того, как расход [связан с вашей деятельностью](#принципы-вычетов)."

### Example of BAD Style (AI-generated)

```
### Как зарегистрироваться

**Логика простая:**

1. Соберите документы
2. Запишитесь на cita
3. Подайте заявку

**Важно понимать:** процесс занимает время.

**Ключевой момент:** не забудьте про страховку.
```

### Same Content in GOOD Style

```
Сначала нужно собрать документы, потом записаться на cita и подать заявку. Процесс занимает время - у меня ушло около двух недель. И не забудьте про страховку, без нее не примут.
```

## Heading Level Rules

Heading level depends on where the content sits in the site hierarchy:

- **Top-level sections** (0_*.md section headers like "Хестор", "Разное", "Банковский счет для аутономо") → **H1** (`#`)
- **Articles within sections** (like "Проблемы с хесторами", "Выбор банка") → **H2** (`##`)
- **Sub-articles within articles** (3rd nesting level, like "Региональные вычеты", "Удержания (retenciones)") → **H3** (`###`)
- **Sub-sub-articles** (4th nesting level, like "Как работает вычет", "Вычет на детей") → **H4** (`####`)

**Exception**: "Надежные специалисты" section - its sub-sections ("Надежные хесторы", "Надежные миграционные юристы") are also **H1**, and individual specialist profiles within them are **H2**.

Rule: internal headings within a file must always be at a lower level than the file's top heading. If the file starts with H2, its internal headings must be H3/H4/etc.

## Structure Guidelines

- Use flowing paragraphs as primary format
- Bullet lists ONLY for genuine enumerations (list of documents, step-by-step instructions)
- H3 subheadings only when section truly needs subdivision (5+ paragraphs)
- Target: no more than 10-15% structural elements to plain text
- Max 2-3 H3 subheadings per short article

## Formatting Rules

### Terms - DO NOT translate
- Keep English/Spanish terms as-is: autónomo, gestor, NIE, Hacienda, Seguridad Social, Modelo, etc.
- Transliterate for pronunciation hints: gestor → хестор, cita → сита, autónomo → аутономо

### Titles
- Use **Sentence case**: "Как стать аутономо в Испании"
- NOT Title Case: "Как Стать Аутономо В Испании"

### Links
- Internal: `{% raw %}{% link path/to/file.md %}{% endraw %}`
- External: `[text](https://example.com){:target="_blank"}`
- Telegram (RU/UA): `https://bit.ly/it-autonomos-es`
- Telegram (EN/ES): `https://bit.ly/it-autonomos-spain-eng`
- Telegram channel: `https://bit.ly/autonomo-and-sl-channel`

### Legacy anchors
When renaming a heading that may have been shared publicly:
```markdown
<span id="old-heading-id" class="legacy-anchor"></span>
## New Heading Name
```

## Fact-Checking

All information I provide has been verified with specialists, but the agent MUST additionally verify facts in authoritative sources.

### Requirements
- Cross-check key facts in 2-3 reliable sources
- Preferred sources:
  - Official government: Agencia Tributaria (sede.agenciatributaria.gob.es), Seguridad Social, BOE (Boletín Oficial del Estado)
  - Banking: official bank websites, Banco de España
  - Professional resources
- Use WebSearch tool for verification

### If discrepancies found
**MANDATORY**: Report ANY discrepancy to the user, even minor ones:
- What exactly differs
- What sources say vs what user provided
- Suggest options: update content, keep user version with note, request clarification

## Workflow

1. **Read reference articles** (see "Read Reference Articles First" section above)
2. **Write ONLY Russian version** matching the author's voice
3. **If NEW article**: add entry to Russian index file (`ru/index.md`)
4. **Verify facts with WebSearch** (MANDATORY - even for editing existing articles)
   - Use WebSearch to verify key claims in 2+ authoritative sources
   - Report any discrepancies immediately
5. **Self-check against RED FLAGS** before presenting
6. **MANDATORY: Complete the Pre-submission Checklist and show verification tables**
   - Go through EVERY item in the checklist
   - Create verification table with columns: Item | Status | Comment
   - DO NOT present article to user until tables are complete
7. **Present to user for approval** (with verification tables)
8. **DO NOT translate** until user explicitly approves and requests translation

## Index Files (Table of Contents)

**CRITICAL**: When adding a NEW article or section, you MUST add it to the Russian index file.

### For new content in `_includes/ru/`

The heading goes INSIDE the included file, NOT in index. The index file only has the `{% raw %}{% include %}{% endraw %}` tag.

**New top-level section** (e.g., a new category like "Страхование"):
1. Create `_includes/ru/insurance/0_insurance.md` starting with `# Страхование` (H1)
2. Add to `ru/index.md`: `{% raw %}{% include ru/insurance/0_insurance.md %}{% endraw %}`

**New article within existing section** (e.g., a new article under "Хестор"):
1. Create `_includes/ru/gestor/new_article.md` starting with `## Article Title` (H2)
2. Add the `{% raw %}{% include %}{% endraw %}` inside the section's `0_gestor.md` file

**Note**: Index updates for other languages (UA/EN/ES) will be done during translation phase via `/content-translate-article`.

## Pre-submission Checklist (MANDATORY - show results to user)

**CRITICAL**: You MUST go through EVERY item below and show the user a verification table before presenting the article. Do not skip any items. Format: table with columns "Item | Status (✅/❌/⚠️) | Comment".

Before presenting the article, verify:

**Preparation:**
- [ ] Read at least 3 reference articles from the list above

**Style & Tone:**
- [ ] No "lecturer phrases" (Важно понимать, Логика простая, Стоит отметить, etc.)
- [ ] No "**Label:**" patterns (Совет:, Важно:, etc.)
- [ ] No letter "ё" - only "е"
- [ ] Only short hyphen "-", no em dash "—"
- [ ] No summarizing conclusions (Таким образом, В заключение, Подводя итог)
- [ ] First sentence doesn't echo keywords from heading
- [ ] No overly formal impersonal (Следует отметить, Представляется целесообразным)
- [ ] No overuse of transitions (Кроме того, Более того, Также)
- [ ] Sounds like personal experience, not a textbook
- [ ] Would pass as human-written text

**Structure:**
- [ ] Paragraphs flow naturally, not fragmented into bullets
- [ ] Bullet lists ONLY for genuine enumerations (documents, steps)
- [ ] Max 2-3 H3 subheadings per article

**Content:**
- [ ] Key facts verified in 2+ authoritative sources (report any discrepancies)
- [ ] EN/ES terms not translated

**Formatting:**
- [ ] Titles in Sentence case
- [ ] Internal links use `{% link path %}` format
- [ ] External links have `{:target="_blank"}`
- [ ] Telegram links use `bit.ly/it-autonomos-es` for RU
- [ ] Legacy anchor added if renaming existing heading

**Index:**
- [ ] **If NEW article**: added to Russian index file (`ru/index.md`)

## Required Output Format

Your response MUST include these sections in order:

1. **Checklist Verification Table** - table showing status of EVERY checklist item
2. **Fact-Check Results Table** - sources checked and any discrepancies found
3. **Proposed Content/Edits** - the article or changes
4. **Discrepancies Summary** - if any facts don't match sources

**Example format:**

```
## Checklist Verification

| Item | Status | Comment |
|------|--------|---------|
| No lecturer phrases | ✅ | None found |
| No "ё" letter | ✅ | Checked |
| Facts verified | ✅ | See fact-check table |
...

## Fact-Check Results

| Claim | Status | Source |
|-------|--------|--------|
| IVA rate 21% | ✅ | Agencia Tributaria |
...

## Proposed Content

[article or edits here]
```

Do NOT skip the tables - they prove you completed the checklist.

## Output

Present ONLY the Russian version and wait for approval before any translation.
