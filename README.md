# llm-wiki-template

Starter repository for an LLM-maintained wiki.

`raw/` holds immutable source material. An agent reads it and incrementally maintains `wiki/`.

## How It Works

- `raw/` — immutable source layer (read-only)
- `wiki/` — derived knowledge layer maintained by the agent
- `schema/` — page format and classification rules
- `.agents/skills/` — reusable wiki workflows

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
- optional: `CHANGELOG.md`

Then:

1. Verify `.claude/skills -> ../.agents/skills`
2. Customize `AGENTS.md`, `schema/`, and `.agents/skills/`
3. Add source files to `raw/`
4. Run `/wiki-ingest`, `/wiki-query`, or `/wiki-lint`

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
- In **Settings → Hotkeys**, bind *Download attachments for current file* (e.g. `Cmd+Shift+D`)
- Install the **Marp** and **Dataview** plugins
- Track the repository with Git

## Layout

```text
.
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
- `index.md`, `log.md`, and `overview.md` are starter meta pages
- `.obsidian/` contains only portable defaults
