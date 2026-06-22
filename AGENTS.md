# Project Guide

Operating manual for AI agents working on the IT Autónomos (ITA) documentation site.
`CLAUDE.md` and `GEMINI.md` are symlinks to this file — edit `AGENTS.md` only.

## Project Overview

A Jekyll site (Cloudflare Pages, theme `jekyll-theme-primer`) documenting how to be an
autónomo or SL in Spain, in four languages: **Russian (source)**, Ukrainian, English, Spanish.

- **Live site**: https://itautonomos.com
- **Russian is the source language** — all content is written in RU first, then translated.
- **English is the default**, served at root `/`. The others are prefixed: `/ru/`, `/ua/`, `/es/`.
- Ukrainian uses `lang: uk` in `_config.yml`/hreflang, but the directory and permalink are `/ua/`.

## How it renders

The whole guide is **one long page per language**, not many small pages. There is no
per-article routing — every "article" is a section/anchor on that single page.

- `index.md` (EN, at `/`) and `ru/index.md`, `ua/index.md`, `es/index.md` are the **only files
  with page frontmatter** and the only files Jekyll renders as pages. Each holds the
  frontmatter, a **hand-written table of contents**, and ~15 top-level `{% include %}` calls.
- Each section is assembled by an **orchestrator** file named `0_*.md`
  (e.g. `_includes/ru/gestor/0_gestor.md`): it writes the section's `#` heading, then
  `{% include %}`s its leaf fragments in display order. Some sections nest a second level
  (orchestrator → sub-orchestrator → leaf), e.g. `reliable-specialists/gestors/0_gestors.md`.
- **Fragments under `_includes/{lang}/` have NO frontmatter** — never add YAML to them.
- The page layout (`layout: default`) is **not in this repo** — it comes from the
  `jekyll-theme-primer` gem. To change page chrome / `<head>`, edit
  `_includes/head-custom.html`, *not* a local layout file.

## Project Structure

```
.
├── index.md                  # EN page (default, served at /) — frontmatter + TOC + 15 includes
├── {ru,ua,es}/index.md       # RU/UA/ES pages (permalink /ru/, /ua/, /es/)
├── {en,ru,ua,es}/
│   ├── versions/             # standalone release-note pages (have their own frontmatter)
│   └── mortgage/index.md     # redirect stubs → spainlifeguide.com (NOT content)
├── _includes/
│   ├── {ru,ua,en,es}/        # per-language section TREES (108 .md fragments each, kept identical)
│   │   └── <section>/        # e.g. gestor/, tax-optimization/, reliable-specialists/
│   │       ├── 0_*.md        #   section orchestrator (writes H1, includes leaf fragments)
│   │       └── *.md          #   leaf fragments (no frontmatter)
│   └── common/
│       ├── common.css        # the ONLY stylesheet (inlined per page)
│       ├── contact-forms/    # HubSpot embed HTML, one file per specialist × language
│       └── gtm-body.html
├── _resources/               # link databases (see "Data files to keep in sync")
├── _files/                   # example PDFs, shipped to the site via _config include
├── _layouts/                 # EMPTY — real layout comes from the jekyll-theme-primer gem
├── _img/                     # images and media
└── .agents/skills/           # 13 agent skills (see "Content workflow & skills")
```

`_posts/` and `_reports/` are empty. `_includes/{lang}/common/` and `_includes/ru/reusable/`
are empty placeholders.

## Editing content

- **Adding a fragment requires editing 2–3 places**, not just creating a file:
  1. the leaf fragment in `_includes/{lang}/<section>/`,
  2. an `{% include %}` line in that section's `0_*.md` orchestrator,
  3. a TOC entry in `{lang}/index.md`.
  A file that isn't included anywhere renders nothing.
- **Keep all four languages structurally identical**: same subdir names, same filenames,
  same include order, same heading levels (108 `.md` per language is the integrity check).
  Add a file in `ru/` → add the mirror in `ua/`, `en/`, `es/`.
- **Bump the last-updated date**: on any content change, update the `<p class="last-updated">`
  date in all four language versions.
- **Heading levels are positional**: orchestrators emit `#` (and sometimes `##` group
  headings); leaf fragments start at `##`/`###` by nesting depth. Mismatching a level shifts
  the hierarchy and breaks the manual TOC anchors.
- **Anchors are fragile.** The TOC in `index.md` is hand-written; the theme auto-generates
  anchors from heading text. Duplicate heading text yields a `-1` suffix (e.g. `#gestor-1`,
  `#xolo-1`). When you rename or move a heading, keep its old anchor alive with
  `<span id="old-anchor" class="legacy-anchor"></span>` above it — otherwise public bit.ly
  links and the internal-links test break. Update the matching TOC link in `index.md` in lockstep.
- **Specialist profiles** pair a Markdown fragment with HubSpot form HTML under
  `_includes/common/contact-forms/<type>/` (`gestors`, `immigration-lawyers`, `tax-analysts`),
  one file per specialist × language (`{specialist}_form_{lang}.html`). The profile renders a
  toggle button (`class="btn-contact-specialist"`) and each form embeds the shared per-language
  fallback under `contact-forms/fallback-message/`. Adding a specialist means the profile
  fragment in all 4 languages **plus** 4 form HTML files.

## Content workflow & skills

The editorial pipeline is automated by skills in `.agents/skills/` (discoverable via the
harness or by listing the dir). **Order is strict:**

1. `content-write-article` — writes **RU only**, in the author's voice, then **stops for approval**.
2. `content-finalize-article` — after approval, runs `content-add-internal-links-to-article`
   + `content-fact-check-article` in parallel.
3. `content-translate-article` — translates **RU → UA/EN/ES** (always from Russian; never
   cross-translate). Updates all 4 `index.md` includes/TOC + last-updated dates.

Each skill owns its detailed spec — the author's voice and typography rules, the link/markup
conventions, the fact-check sources. **Don't reproduce those rules here; read the skill.**
Validation runs through the `tests-*` skills (`tests-run-all-tests` wraps the local/prod splits);
see **Build & test** for the network distinction.

## Build & test

- Ruby **3.3.4** (pinned in `.ruby-version`).

```
bundle install
bundle exec jekyll serve     # local preview at http://localhost:4000 (SLG sibling uses 4001)
bundle exec jekyll build     # writes _site/ (needed before the internal-links test)
```

- Link checks use **lychee** (`brew install lychee`), invoked with `--include-fragments`.
- **LOCAL vs PROD** split is about network:
  - **LOCAL** tests need no internet but require a fresh `_site/` build and a running
    `jekyll serve` at `http://localhost:4000`.
  - **PROD** tests hit the live site `https://itautonomos.com` (and bit.ly).
- **Deployment** is via **Cloudflare Pages** (build config lives in the Cloudflare dashboard, not in-repo). There is **no CI** in `.github/` (only `FUNDING.yml`) and `_site/` is gitignored.

## Data files to keep in sync

- `_resources/internal_links_{ru,ua,en,es}.json` — per-language anchor databases for the
  single index page. After changing content, run `bundle exec jekyll build` then
  `tests-local-test-and-update-internal-links`: it adds new anchors and **flags missing ones
  as a hard stop** (fix with a `legacy-anchor` span + rebuild).
- `_resources/bitly_links.json` — tracks legacy bit.ly shortlinks for the prod link tests;
  being phased out, see the migration note below.

> **Migration in progress:** the `remove-bitly` effort moves the site off bit.ly shortlinks
> toward direct URLs. Do not add new bit.ly links. The `bitly_links.json` database and the
> `utils-add-bitly-links-to-database` / `tests-prod-test-bitly-links` skills are legacy and
> being removed; site content (includes, `index.md`, README) has already been migrated to
> direct URLs.

## Code Standards

### CSS
- All styles live in **one file**: `_includes/common/common.css` (inlined per page).
  Don't create new stylesheets. Language pages may carry a tiny page-specific `<style>` tweak
  in their own frontmatter (e.g. `ru/index.md` hides a duplicate first `<h1>`).

## Git workflow

One topic per short-lived feature branch off `main`, merged via a GitHub PR. Do not commit directly to `main`.

## Related Projects

Sibling project — **Spain Life Guide (SLG)**: `../spain-life-guide/`
- Guide about life in Spain (bureaucracy, documents, housing, taxes, healthcare). Same
  structure and languages, but **RU is the default** (served at `/`) and it renders as **multiple
  full-length pages** (home, mortgage, why-valencia) rather than one long page.
- The `content-add-internal-links-to-article` skill reads SLG's
  `_resources/internal_links_{lang}.json` for cross-links.
- When asked to apply changes to both projects, check the sibling and apply there too.

**Abbreviations**: **ITA** = IT Autónomos (this project) · **SLG** = Spain Life Guide.
