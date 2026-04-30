# Wiki Conventions

## Language

All wiki pages should be written in English by default.
If a project needs another language, update this file and `AGENTS.md` together.

## File Naming

- Use lowercase English, with hyphens (`-`) between words.
- If another writing system is needed, use it consistently across the repository.
- Examples: `reinforcement-learning.md`, `vannevar-bush.md`, `reinforcement-learning-vs-supervised-learning.md`
- Source summary pages: `YYYY-MM-DD-source-title.md` (example: `2026-04-07-attention-is-all-you-need.md`)

## Wiki Link Resolution

Obsidian resolves `[[...]]` links by **filename** (case-insensitive) or **`aliases`** in frontmatter — not by the `title` field. Because filenames use hyphens (e.g., `reinforcement-learning.md`) while wiki links typically use the natural title with spaces (e.g., `[[Reinforcement Learning]]`), aliases bridge the gap.

### `aliases` rules

Required:
- The `title` value, verbatim, as the **first** entry in `aliases`. Without this, `[[Title]]` from other pages will not resolve.
- For source pages with date-prefixed filenames (e.g., `2026-04-07-attention-is-all-you-need.md`), the title alias is what makes references work.

Optional (recommended when relevant):
- Cross-language form (e.g., `Agent Memory` ↔ `에이전트 메모리`)
- Abbreviations or alternate names users may search for
- Hyphenated slug if frequently typed

Example:

```yaml
title: Reinforcement Learning
aliases:
  - Reinforcement Learning   # required: matches title exactly
  - RL                       # optional: abbreviation for search
```

### Link form (all pages)

Every internal wiki link, on every page, must use the explicit `[[file-slug|Display Title]]` form — not just navigation hubs. This applies to:

- Body links: `[[reinforcement-learning|Reinforcement Learning]] — description`
- `related:` frontmatter entries: `"[[2026-04-07-attention-is-all-you-need|Attention Is All You Need]]"`
- Source citations inside body text: `[[2026-04-07-attention-is-all-you-need|Attention Is All You Need]]`

```markdown
- [[reinforcement-learning|Reinforcement Learning]] — description
- [[2026-04-07-attention-is-all-you-need|Attention Is All You Need]] — description
```

Why: alias-based resolution lags Obsidian's metadata cache and breaks the backlinks pane in practice — not just in hubs. Plain `[[Title]]` resolves through the title alias when the cache is fresh, but backlinks frequently miss entries. The pipe form resolves directly via filename and guarantees backlinks regardless of indexing state.

The `aliases` frontmatter (with `title` as the first entry) remains required as a search/autocomplete fallback, but is not the primary resolution path for `[[...]]` links anymore.

## YAML Frontmatter

Every wiki page must include the following frontmatter:

### Common Fields

| Field | Required | Value | Description |
|------|------|----|------|
| title | O | string | Page title |
| type | O | entity, concept, source, synthesis, meta | Page type |
| tags | O | array | Subcategory tags |
| aliases | - | array | Aliases for Obsidian auto-linking |
| domain | O | personal, research, reading, business | Wiki domain |
| status | O | draft, active, archived | Page status |
| sources | - | array | Supporting raw file paths |
| related | - | array | Related wiki page links |
| created | O | YYYY-MM-DD | Creation date |
| updated | O | YYYY-MM-DD | Last updated date |

### Additional Fields for `source` Pages

| Field | Required | Value | Description |
|------|------|----|------|
| author | - | string | Original author |
| url | - | URL | Original URL |
| source_type | O | article, book, paper, note, video, podcast, data | Source type |
| date_published | - | YYYY-MM-DD | Original publication date |

## Page Structure

### `entity` Page

```
# {title}

## Overview
One-paragraph summary.

## Details
Key information. Cite supporting sources with `[[YYYY-MM-DD-source-slug|Source Title]]` links.

## Related Pages
- [[related-slug-1|Related Page 1]]
- [[related-slug-2|Related Page 2]]
```

### `concept` Page

```
# {title}

## Definition
One-paragraph definition.

## Key Points
Detailed explanation, with examples where useful.

## Related Concepts
- [[related-concept-slug|Related Concept 1]]

## Source References
- [[YYYY-MM-DD-source-slug|Source Summary 1]]
```

### `source` Summary Page

```
# {title}

## Summary
3-5 sentence summary.

## Key Points
- Key point 1
- Key point 2
- ...

## Insights
Why this source matters, and how it connects to or contradicts existing knowledge.

## Related Pages
- [[entity-slug|Entity Title]] — relationship note
- [[concept-slug|Concept Title]] — relationship note
```

### `synthesis` Page

```
# {title}

## Question or Goal
What this synthesis is trying to answer.

## Analysis
Comparison, synthesis, or a new perspective, with cited support.

## Conclusion

## References
- [[YYYY-MM-DD-source-slug-1|Source 1]]
- [[YYYY-MM-DD-source-slug-2|Source 2]]
```

### `meta` Page

```
# {title}

## Purpose
What this document does for the wiki.

## Content
Operational information such as indexes, logs, and summaries.

## Related Documents
- [[related-doc-slug-1|Related Document 1]]
- [[related-doc-slug-2|Related Document 2]]
```

## Cross-References

- When mentioning another wiki page, always use the explicit `[[file-slug|Display Title]]` form (per "Link form (all pages)" above). Plain `[[Title]]` is forbidden.
- When a new entity or concept appears, create a page or update the existing one.
- When citing a raw source, record its path in the `sources` frontmatter field.

## `raw/` Rules

- **Never edit files here.** Read-only.
- Store source files flatly directly under `raw/` with no subfolders.
- Store attachments such as images under `raw/assets/`.
- Record source metadata such as author and URL in the frontmatter of the summary page under `wiki/sources/`.
