# llm-wiki-template

Starter repository for an LLM-maintained wiki.

`raw/` stores immutable source material. The agent reads it and incrementally maintains `wiki/`.

## Quick Start

### Clone as a starting point

```bash
git clone https://github.com/<owner>/llm-wiki-template.git <your-wiki-repo>
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
4. Use `/wiki-ingest`, `/wiki-query`, `/wiki-lint`

## Source of Truth

- `raw/`: immutable source layer
- `wiki/`: derived knowledge layer maintained by the agent
- `schema/`: page format and classification rules
- `.agents/skills/`: reusable wiki workflows

If behavior changes, update `schema/`, `AGENTS.md`, and skills together.

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

## Workflows

- `/wiki-ingest`: process sources from `raw/` into `wiki/`
- `/wiki-query`: answer questions from the wiki and save reusable syntheses
- `/wiki-lint`: audit links, frontmatter, and consistency

## Notes

- `raw/` is read-only
- `index.md`, `log.md`, and `overview.md` are starter meta pages
- `.obsidian/` contains only portable defaults
