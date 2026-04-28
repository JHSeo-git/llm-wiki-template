# Changelog

All notable changes to this template repository will be documented in this file.

This changelog tracks changes to the template itself, not to repositories created from the template.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

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
