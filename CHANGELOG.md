# Changelog

All notable changes to this template repository will be documented in this file.

This changelog tracks changes to the template itself, not to repositories created from the template.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [0.2.2] - 2026-04-30

### Changed

- `Wiki Link Resolution` rule in `schema/conventions.md` generalized: the `[[file-slug|Display Title]]` form is now required on **every page** (body text, `related:` frontmatter, source citations) — not just navigation hubs. The previous "Other pages may use the simpler `[[Title]]` form" allowance is removed because alias-based resolution lags Obsidian's metadata cache and breaks the backlinks pane in practice. Section renamed `Linking from navigation hubs` → `Link form (all pages)`. The `aliases` frontmatter (with `title` first) remains required as a search/autocomplete fallback only.
- Page-structure templates in `schema/conventions.md` (entity, concept, source, synthesis, meta) updated so every example link uses the pipe form.
- `Cross-References` section in `schema/conventions.md` updated to require `[[file-slug|Display Title]]`; plain `[[page name]]` is now forbidden.
- `wiki-lint` skill: `Navigation hub link form` check renamed to `Wiki link form (all pages)` and broadened to flag plain `[[Title]]` anywhere. `Orphans` and `Missing pages` checks reworded to specify slug-based resolution. `Title alias presence` description clarified to call aliases a search/autocomplete fallback. Auto-fix step now lists `[[Title]] → [[slug|Title]]` conversion as a safe automatic fix.
- `wiki-ingest` skill steps 3, 5, 6 updated: (a) alias requirement reframed as fallback, (b) every internal wiki link in body, `related:`, and source citations must use `[[file-slug|Display Title]]`.
- `wiki-query` skill steps 3 and 5 updated: chat-reply citations and any saved synthesis page (including its `related:` frontmatter and the index entry) must use `[[file-slug|Display Title]]`.

## [0.2.1] - 2026-04-28

### Added

- New `Wiki Link Resolution` section in `schema/conventions.md`:
  - Every page must include its `title` verbatim as the first entry of `aliases` so `[[Title]]` references resolve.
  - For navigation hubs (e.g., `wiki/index.md`), the explicit `[[file-slug|Display Title]]` form is recommended to guarantee backlinks regardless of Obsidian's alias cache state.
- New checks in the `wiki-lint` skill: `Title alias presence` and `Navigation hub link form`.

### Changed

- `wiki-ingest` skill steps 3, 4, and 6 now require: (a) including the `title` in `aliases` when creating any new page, and (b) using `[[file-slug|Display Title]]` form when updating `wiki/index.md`.
- Template meta pages (`wiki/index.md`, `wiki/overview.md`, `wiki/log.md`) backfilled with `title` aliases and converted their `related:` entries to the navigation hub link form.

## [0.2.0] - 2026-04-23

### Added

- Optional Quartz + GitHub Pages deployment setup under `.github/`.
- Quartz deployment workflow, config, layout, and deployment guide for publishing `wiki/` as a static site.

### Changed

- Expanded `README.md` to better explain template customization, optional deployment files, repository layout, and `raw/` storage rules.
- Added a concise root-level Quartz deployment section that links to the full guide in `.github/quartz/README.md`.

## [0.1.1] - 2026-04-23

### Changed

- Restructured `README.md` with `How It Works`, `Typical Usage`, and `Recommended Setup` sections covering the Obsidian Web Clipper → `raw/` → `wiki ingest` flow.

## [0.1.0] - 2026-04-21

### Added

- Initial GitHub template repository scaffold.
- Agent entry files: `AGENTS.md`, `CLAUDE.md`.
- Canonical wiki workflows under `.agents/skills/`.
- Wiki schema documents under `schema/`.
- Empty wiki structure under `raw/` and `wiki/`.
- Minimal portable Obsidian configuration.

### Changed

- Generalized template docs and agent instructions for broader reuse.
- Standardized repository-facing documentation in English.
