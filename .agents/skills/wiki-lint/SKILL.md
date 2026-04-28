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
   - **Orphans**: Find pages with no inbound `[[wiki-links]]`.
   - **Missing pages**: Find `[[wiki-links]]` that point to pages that do not exist.
   - **Missing cross-references**: Identify closely related pages that are not linked to each other.
   - **Frontmatter validation**: Check for missing required fields or invalid `type`, `domain`, or `status` values.
   - **Title alias presence**: Every page must include its `title` verbatim as the first entry in `aliases` (per "Wiki Link Resolution" in `conventions.md`). Pages missing this break `[[Title]]` resolution from other pages.
   - **Navigation hub link form**: In `wiki/index.md`, every `[[...]]` link should use the explicit `[[file-slug|Display Title]]` form. Plain `[[Title]]` in the index hub is brittle when Obsidian's alias cache lags.
   - **Empty sections**: Find sections that exist but have no content.
3. **Report findings**: Report findings to the user by category.
4. **Fix what can be fixed**: After user approval, apply safe automatic fixes such as frontmatter completion or added cross-references. Discuss content-level changes with the user first.
5. **Write the log**: Append to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] lint | routine audit
   - Fixed: (list of updated pages)
   - Found: (list of unresolved issues)
   ```
6. **Suggest improvements**: Recommend topics to research next, new sources to ingest, or pages worth expanding.
