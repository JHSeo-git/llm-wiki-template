# llm-wiki-template

Starter repository for an LLM-maintained wiki.

`raw/` holds immutable source material. An agent reads it and incrementally maintains `wiki/`.
The defaults are examples, not a fixed product shape. Customize them before using this repo as your source of truth.

## How It Works

- `raw/` — immutable source layer (read-only)
- `wiki/` — derived knowledge layer maintained by the agent
- `schema/` — page format and classification rules
- `.agents/skills/` — reusable wiki workflows
- `.github/` — optional Quartz + GitHub Pages deployment setup for publishing `wiki/`

If behavior changes, update `schema/`, `AGENTS.md`, and the skills together.

## Quick Start

### Clone as a starting point

```bash
git clone https://github.com/JHSeo-git/llm-wiki-template.git <your-wiki-repo>
cd <your-wiki-repo>
git remote remove origin
git remote add origin https://github.com/<your-org-or-user>/<your-wiki-repo>.git
```

### Or copy into an existing repository

Copy these paths:

- `AGENTS.md`
- `CLAUDE.md`
- `.agents/skills/`
- `.claude/skills`
- `.obsidian/`
- `schema/`
- `raw/`
- `wiki/`
- optional: `.github/`
- optional: `CHANGELOG.md`

Then:

1. Verify `.claude/skills -> ../.agents/skills`
2. Customize `AGENTS.md`, `schema/`, and `.agents/skills/` for your language, frontmatter, and category model
3. Add source files to `raw/`
4. If you want site deployment, keep `.github/` and update the Quartz settings
5. Run `/wiki-ingest`, `/wiki-query`, or `/wiki-lint`

## Deploy with Quartz

If you want to publish the derived `wiki/` as a static site, this template includes an optional Quartz + GitHub Pages setup under `.github/`.

For setup details, configuration notes, and the full deploy guide, see [`.github/quartz/README.md`](.github/quartz/README.md).

## Workflows

- `/wiki-ingest` — process sources from `raw/` into `wiki/`
- `/wiki-query` — answer questions from the wiki and save reusable syntheses
- `/wiki-lint` — audit links, frontmatter, and consistency

## Typical Usage

1. Clip web pages with Obsidian Web Clipper directly into `raw/`
2. Run `wiki ingest` in Claude Code or Codex to update `wiki/` automatically
3. Occasionally run `wiki lint` to check links, frontmatter, and consistency
4. Use `wiki query` to explore and synthesize stored knowledge

## Recommended Setup

- Install [qmd](https://github.com/tobi/qmd)
- Install the [Obsidian Web Clipper](https://chromewebstore.google.com/detail/obsidian-web-clipper/cnjifjpddelmedmihgijeibhnjfabmlf) extension
- In Obsidian, set **Settings → Files and links → Attachment folder path** to a fixed directory (e.g. `raw/assets/`)
- In **Settings → Hotkeys**, bind _Download attachments for current file_ (e.g. `Cmd+Shift+D`)
- Install the **Marp** and **Dataview** plugins
- Track the repository with Git
- If you want a published site, enable GitHub Pages and keep the Quartz files under `.github/`

## Layout

```text
.
├── .github/
│   ├── quartz/
│   └── workflows/
├── .agents/skills/
├── .claude/skills -> ../.agents/skills
├── raw/
│   └── assets/
├── schema/
└── wiki/
    ├── entities/
    ├── concepts/
    ├── sources/
    ├── syntheses/
    ├── index.md
    ├── log.md
    └── overview.md
```

## Notes

- `raw/` is read-only
- Store source files flatly under `raw/`; use `raw/assets/` for attachments
- `index.md`, `log.md`, and `overview.md` are starter meta pages
- Quartz deployment publishes `wiki/` by default
- `.obsidian/` contains only portable defaults
