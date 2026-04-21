# Category Classification

## Folder Classification

### wiki/entities/
Concrete **named entities**: people, organizations, places, products, services, projects, events.
- A target identifiable as a proper noun
- Examples: Elon Musk, OpenAI, GPT-4, Seoul, WWDC 2026

### wiki/concepts/
Abstract **concepts, theories, frameworks, methodologies**.
- A general concept rather than a proper noun
- Examples: reinforcement learning, cognitive dissonance, agile methodology, compound growth

### wiki/sources/
**Per-source summary pages**. One page under `wiki/sources/` for each file in `raw/`.
- Filename: `YYYY-MM-DD-source-title.md`
- Summarize the raw file and record metadata

### wiki/syntheses/
**Synthesis, comparison, and analysis pages**. Connect multiple sources/pages to present a new perspective.
- Query results, comparative analysis, topic-level synthesis
- Examples: `reinforcement-learning-vs-supervised-learning`, `2026-q1-reading-review`

### wiki/*.md (top-level)
**Meta pages**. Operational and navigational pages about the wiki itself.
- Examples: `wiki/index.md`, `wiki/log.md`, `wiki/overview.md`
- Use `type: meta`

## Tags

Assign tags freely through the frontmatter `tags` field. Tags are an axis independent from folders.

### Recommended Tag Examples

| Category | Example Tags |
|----------|----------|
| Domain | AI, psychology, economics, health, software |
| Form | person, company, tool, paper, book |
| Status | debated, verified, hypothesis |
| Personal | goals, habits, reflection |

Tags can be added and extended freely. For consistency, check the existing tag set, for example with a Dataview query, and avoid duplicates or near-duplicates.

## Decision Rules

| Question | → Classification |
|------|--------|
| Is it a proper noun? | entities/ |
| Is it an abstract concept or theory? | concepts/ |
| Is it a summary of a specific source? | sources/ |
| Is it an analysis connecting multiple pages? | syntheses/ |
| Is it about operating or navigating the wiki itself? | meta |
| If none of the above fits? | Use the closest folder and supplement with tags |

## `domain` Field

| Value | Usage |
|----|------|
| personal | Personal goals, health, psychology, self-development |
| research | Deep investigation of a topic, papers, technology |
| reading | Knowledge derived from reading books and articles |
| business | Work, teams, projects, business analysis |
