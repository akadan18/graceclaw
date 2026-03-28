# Brain Vault

Your personal knowledge base. Built incrementally as the agent encounters relevant information.

## Structure

```
data/brain/
├── topics/     — concepts, frameworks, ideas, methodologies
├── people/     — contacts, relationships, professional context
├── projects/   — active work, engagements, initiatives
└── content/    — articles, newsletters, reference material
```

## File Format

Every brain file should have YAML frontmatter for fast scanning:

```yaml
---
title: "File Title"
type: topic | person | project | content
description: "One sentence — specific and agent-scannable"
tags: [relevant, tags]
related: ["[[Related File]]", "[[Another File]]"]
---
```

Then the content in whatever format makes sense.

## Wikilinks

Link related files with `[[wikilinks]]` embedded in prose:

> "His work on [[PMF-GTM-Methodology]] applies directly here."

Not as standalone references — woven into sentences so the connection carries meaning.

## When to Create a File

**People:** Any person who appears more than twice in conversations, emails, or meetings. Include: role, company, relationship to you, last interaction, key context.

**Topics:** Any framework, methodology, or concept you reference regularly. Include: definition, how you apply it, relevant examples.

**Projects:** Any active engagement, initiative, or work stream. Include: goal, status, key people, next steps.

**Content:** Articles, papers, or resources worth referencing again. Include: key insight, why it matters, where it applies.

## Growth Pattern

- Start with the 3–5 most active projects and 10–15 most important people
- Add topics as they come up in conversation
- Let the agent create files proactively as new context surfaces
- Review quarterly — archive stale projects, update outdated people files
