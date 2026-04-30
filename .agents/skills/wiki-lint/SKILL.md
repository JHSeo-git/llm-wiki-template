---
name: wiki-lint
description: Use when the user wants to check wiki health, find inconsistencies, audit structure, or review the overall quality of the wiki
---

# Wiki Lint

Workflow for checking the wiki's consistency and overall health.

## Workflow

@schema/conventions.md
@schema/categories.md

1. **Scan everything**: Read every page under `wiki/`.
2. **Check the following**:
   - **Contradictions**: Look for conflicting claims across pages.
   - **Freshness**: Check whether older claims have been superseded by newer sources.
   - **Orphans**: Find pages with no inbound wiki links. Resolution is by **filename slug** (the left side of `[[slug|Title]]`), so match on slug — not on display title.
   - **Missing pages**: Find `[[slug|...]]` links whose slug does not correspond to an existing file. The slug must match a real `.md` filename under `wiki/`.
   - **Missing cross-references**: Identify closely related pages that are not linked to each other.
   - **Frontmatter validation**: Check for missing required fields or invalid `type`, `domain`, or `status` values.
   - **Title alias presence**: Every page must include its `title` verbatim as the first entry in `aliases` (per "Wiki Link Resolution" in `conventions.md`). Required as a search/autocomplete fallback even though `[[...]]` links no longer rely on alias resolution.
   - **Wiki link form (all pages)**: Every `[[...]]` link on every page — body text, `related:` frontmatter, source citations — must use the explicit `[[file-slug|Display Title]]` form. Plain `[[Title]]` is brittle: alias-based resolution lags Obsidian's metadata cache and frequently breaks the backlinks pane. Flag any plain `[[Title]]` occurrences for conversion to `[[slug|Title]]`.
   - **Empty sections**: Find sections that exist but have no content.
3. **Report findings**: Report findings to the user by category.
4. **Fix what can be fixed**: After user approval, apply safe automatic fixes — frontmatter completion, added cross-references, and converting any plain `[[Title]]` occurrences to `[[slug|Title]]`. Discuss content-level changes with the user first.
5. **Write the log**: Append to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] lint | routine audit
   - Fixed: (list of updated pages)
   - Found: (list of unresolved issues)
   ```
6. **Suggest improvements**: Recommend topics to research next, new sources to ingest, or pages worth expanding.
