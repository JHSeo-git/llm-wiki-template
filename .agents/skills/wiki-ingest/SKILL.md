---
name: wiki-ingest
description: Use when the user adds new source files to raw/ and wants them processed into the wiki, or asks to ingest, read, or integrate a source into the wiki
---

# Wiki Ingest

Workflow for reading source files and integrating them into the wiki.

## Modes

- **Automatic (default)**: Read the source and update the wiki immediately.
- **Interactive**: If the user wants to review it together first, discuss the key points before writing to the wiki.

## Workflow

@schema/conventions.md
@schema/categories.md

1. **Read the source**: Read files under `raw/`. If a Markdown file references images, read the text first and inspect the referenced images separately.
2. **Check for interactive mode**: In interactive mode, summarize the source for the user and get feedback before writing wiki changes.
3. **Create a source summary**: Create `wiki/sources/YYYY-MM-DD-source-title.md` using the source page structure and frontmatter rules from `conventions.md`.
4. **Update entities and concepts**: For major entities and concepts mentioned in the source:
   - If a page already exists, add or update the new information and refresh `updated`.
   - If a page does not exist, create it using the classification rules in `categories.md`.
   - If the new source conflicts with existing content, mark the contradiction explicitly.
5. **Add cross-references**: Make sure related pages are connected with `[[wiki-links]]` and `related` frontmatter entries.
6. **Update the index**: Reflect created or changed pages in `wiki/index.md`.
7. **Write the log**: Append to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] ingest | source title
   - Source: raw/path/file.md
   - Created: wiki/sources/summary-page.md
   - Updated: wiki/entities/..., wiki/concepts/...
   ```
8. **Refresh the overview**: Update the stats in `wiki/overview.md` such as total sources and page counts.

## Batch Ingest

If the user asks to ingest multiple files at once, repeat this workflow for each source sequentially. Write a separate log entry for each source.
