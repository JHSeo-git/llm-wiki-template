---
name: wiki-query
description: Use when the user asks questions about wiki content, wants to explore a topic, or requests analysis, synthesis, or comparison based on the wiki
---

# Wiki Query

Workflow for finding information in the wiki and synthesizing an answer.

## Workflow

@schema/conventions.md

1. **Find relevant pages**:
   - Start with `wiki/index.md` to identify relevant pages.
   - If the index is not enough, search with `qmd query "keyword" wiki/`.
2. **Read pages**: Read the relevant pages and understand the content. If needed, follow the `sources` field back to the original files under `raw/`.
3. **Synthesize the answer**: Answer using the wiki as the source of truth. Cite supporting pages with `[[wiki-links]]`.
4. **Decide whether to save it**: If the answer has reusable value, such as comparison, synthesis, or a novel perspective, save it under `wiki/syntheses/`.
   - Do not save simple fact lookup answers.
   - Ask the user before saving: "Should I save this analysis to the wiki?"
5. **If saved**: Update `index.md`, append to `log.md`, and refresh `overview.md`.

## Search Strategy

| Situation | Method |
|------|------|
| Small wiki, index is enough | `index.md` only |
| Exact keyword search needed | `qmd search "keyword" wiki/` |
| Semantic or question-like retrieval | `qmd query "question" wiki/` |
