## Purpose

- This repository is an LLM-maintained wiki template.
- `raw/` is the immutable source layer. Read-only.
- `wiki/` is the derived knowledge layer. The agent creates and updates it.

## Core Rules

- Page rules: `schema/conventions.md`
- Classification rules: `schema/categories.md`
- If behavior changes, update `schema/`, `AGENTS.md`, and `.agents/skills/` together
- Do not edit files under `raw/`
- When the wiki changes, update `wiki/index.md`, `wiki/log.md`, and `wiki/overview.md` when appropriate

## Default Workflows

- Source ingest: `/wiki-ingest`
- Wiki query: `/wiki-query`
- Wiki lint: `/wiki-lint`

## Customize First

- wiki language
- frontmatter schema
- category model
- index, log, and overview format
- skill behavior

The defaults in this template are examples. Adjust them before using the repo as your source of truth.
