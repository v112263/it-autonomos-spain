# Fact-Check Article

Perform thorough fact-checking of an article before publication. Verify all claims, numbers, deadlines, conditions, and legal references against authoritative official sources.

## Input

$ARGUMENTS

The input should be a path to an article file (e.g., `_includes/ru/tax-optimization/rent.md`).

## Instructions

### Phase 1: Read and Extract Facts

1. **Read the article** from the specified path

2. **Extract all verifiable claims**, including:
   - **Numbers**: percentages, amounts, limits, thresholds (e.g., "IVA 21%", "315€/month", "60,000€ threshold")
   - **Deadlines**: filing dates, registration periods, waiting times (e.g., "quarterly by 20th", "within 30 days")
   - **Conditions**: eligibility requirements, prerequisites (e.g., "only for first-time autonomos", "requires 3 years of residence")
   - **Legal references**: laws, regulations, articles (e.g., "Ley 20/2007", "Art. 96 LIRPF")
   - **Procedures**: steps, requirements, document lists
   - **Rates and calculations**: tax rates, social security contributions, formulas
   - **Official terminology**: correct names of forms, institutions, programs

3. **Create a list of facts to verify** with context from the article

### Phase 2: Verify Against Official Sources

4. **Use WebSearch to verify each fact** against authoritative sources:

   **Primary sources (MUST use when relevant):**
   - **Agencia Tributaria** (sede.agenciatributaria.gob.es) - taxes, IVA, IRPF, models
   - **Seguridad Social** (seg-social.es) - contributions, quotas, benefits
   - **BOE** (boe.es) - laws, royal decrees, official regulations
   - **Ministerio de Trabajo** - labor regulations
   - **Banco de España** - banking regulations

   **Secondary sources (for additional context):**
   - Official bank websites
   - Professional associations (colegios profesionales)
   - Recognized legal/tax advisory firms with cited sources

5. **For each fact, document:**
   - The exact claim from the article
   - What the official source says
   - The URL of the source
   - Whether it matches, partially matches, or contradicts

### Phase 3: Legal Verification

6. **For any legal references:**
   - Verify the law/article number is correct
   - Check if it's still in force (not derogated or modified)
   - Confirm the interpretation in the article matches the legal text
   - Use BOE or official legal databases

7. **Check for outdated information:**
   - Tax rates and limits often change annually
   - Social security contributions update yearly
   - Verify current year values, not historical ones

### Phase 4: Generate Report

8. **Create a comprehensive fact-check report** with the following structure:

```markdown
## Fact-Check Report: [Article Name]

**Article path:** `[path]`
**Checked on:** [date]
**Total facts checked:** [number]

### Summary

- ✅ Verified: [number]
- ⚠️ Partial discrepancies: [number]
- ❌ Incorrect/outdated: [number]

---

### Detailed Results

#### ✅ Verified Facts

| Fact in Article | Verified Value | Source |
|-----------------|----------------|--------|
| IVA rate is 21% | 21% (general rate) | [Agencia Tributaria](url) |
| ... | ... | ... |

#### ⚠️ Partial Discrepancies

| Fact in Article | Official Source Says | Source | Comment |
|-----------------|---------------------|--------|---------|
| "Filing deadline is 20th" | "20th of month following quarter end" | [AT](url) | Missing detail about exceptions for weekends/holidays |
| ... | ... | ... | ... |

#### ❌ Incorrect or Outdated

| Fact in Article | Correct Information | Source | Recommended Action |
|-----------------|--------------------:|--------|-------------------|
| "Minimum base 294€" | "Minimum base 306€ in 2024" | [SS](url) | Update to current year value |
| ... | ... | ... | ... |

---

### Facts Unable to Verify

| Fact | Reason | Recommendation |
|------|--------|----------------|
| "In my experience, processing took 2 weeks" | Personal experience - cannot verify | Keep as personal anecdote, clearly marked |
| ... | ... | ... |

---

### Recommendations

1. [Specific action items based on findings]
2. ...
```

## Verification Standards

### What to Flag as ⚠️ Partial Discrepancy:
- Minor differences in wording that don't change meaning
- Missing details that could be helpful
- Simplifications that omit edge cases
- Rounding of numbers (e.g., "about 300€" when exact is 294.12€)

### What to Flag as ❌ Incorrect:
- Wrong numbers, rates, or percentages
- Outdated information (old rates, repealed laws)
- Incorrect deadlines
- Wrong form numbers or procedure steps
- Misinterpretation of legal requirements

### Personal Experience Claims:
- Mark as "Unable to verify - personal experience"
- Don't flag as incorrect unless they contradict official requirements
- Note if the experience seems atypical

## Output

Present the complete fact-check report. Be thorough - check EVERY verifiable claim in the article. The goal is to ensure 100% accuracy before publication.

After the report, if there are any ⚠️ or ❌ items, provide a summary of recommended changes to the article.
