# Claude Code Project Guide

This document contains essential guidelines for working on the Autónomo and SL Spain Documentation project.

## Content Skills (USE THESE!)

For content work, use the dedicated skills:

- **`/content-write-article`** - Writing or editing articles (includes style guide, examples, checklist)
- **`/content-translate-article`** - Translating approved Russian content to UA/EN/ES

These skills contain detailed instructions, examples, and checklists. They are **auto-invocable** - Claude will automatically load them when the conversation context matches (e.g., when you ask to write or translate an article).

## Project Overview

A Jekyll-based multilingual documentation website about being an autónomo or SL in Spain, deployed on GitHub Pages. The site provides comprehensive guidance in four languages: Russian (primary source), Ukrainian, English (default at `/`), and Spanish.

**Live site**: https://itautonomos.com

**Note**: English is the default language served at root `/`, but Russian is the source language for all content.

## Project Structure

```
.
├── index.md                    # English index (main entry point, default)
├── ru/index.md                 # Russian index
├── ua/index.md                 # Ukrainian index
├── es/index.md                 # Spanish index
├── en/                         # Full-length articles
│   └── versions/              # Document version history (1.0.md, 2.0.md, etc.)
├── ru/                         # Full-length articles
│   └── versions/
├── ua/                         # Full-length articles
│   └── versions/
├── es/                         # Full-length articles
│   └── versions/
├── _includes/
│   ├── common/                 # Shared assets (CSS, forms)
│   │   └── common.css
│   ├── en/                    # English article includes
│   ├── ru/                    # Russian article includes
│   ├── ua/                    # Ukrainian article includes
│   └── es/                    # Spanish article includes
├── _layouts/                   # Jekyll layouts
└── _img/                       # Images and media assets
```

### Content Organization

- Each language maintains **identical structure and organization**
- **Primary content location**: `_includes/{lang}/` directories contain the majority of articles
- **Separately placed in root language directories** (`en/`, `ru/`, `ua/`, `es/`):
  - `versions/` - Document version history and past release notes
- Index files (`*/index.md`) serve as navigation hubs linking to all articles
- Common assets (CSS, forms) are in `_includes/common/`

## Code Standards

### CSS
- All styles in **one file**: `_includes/common/common.css`
- Centralized styling approach
- Use consistent naming conventions

### Best Practices
- Maintain separation of concerns between content and presentation
- Keep all common assets in `_includes/common/`
- Follow Jekyll best practices

## Related Projects

This project has a sibling project:

- **Spain Life Guide**: `../spain-life-guide/`
  - Guide about life in Spain (bureaucracy, documents, tips)
  - Same structure, same languages (but RU is default there)
  - When user asks to apply changes to both projects, check the sibling project and apply there too

**Project abbreviations**:
- **ITA** = IT Autonomos (this project)
- **SLG** = Spain Life Guide (sibling project)
