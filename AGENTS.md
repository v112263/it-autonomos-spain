# Project Guide

This document contains essential guidelines for working on the Autónomo and SL Spain Documentation project.

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
│   ├── mortgage/              # Mortgage guide
│   └── versions/              # Document version history (1.0.md, 2.0.md, etc.)
├── ru/                         # Full-length articles
│   ├── mortgage/
│   └── versions/
├── ua/                         # Full-length articles
│   ├── mortgage/
│   └── versions/
├── es/                         # Full-length articles
│   ├── mortgage/
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
  - `mortgage/` - Mortgage guide
- Index files (`*/index.md`) serve as navigation hubs linking to all articles
- Common assets (CSS, forms) are in `_includes/common/`

## Code Standards

### CSS
- All styles in **one file**: `_includes/common/common.css`
- Centralized styling approach
- Use consistent naming conventions

## Related Projects

This project has a sibling project:

- **Spain Life Guide**: `../spain-life-guide/`
  - Guide about life in Spain (bureaucracy, documents, tips)
  - Same structure, same languages (but RU is default there)
  - When user asks to apply changes to both projects, check the sibling project and apply there too

**Project abbreviations**:
- **ITA** = IT Autonomos (this project)
- **SLG** = Spain Life Guide (sibling project)
