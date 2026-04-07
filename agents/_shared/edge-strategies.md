# Edge Strategies — Context Flow Between Agents

When work passes between pipeline stages (creator → critic → validator → operator), be explicit about what context flows. This saves tokens, prevents bias, and improves output quality.

## Four Strategies

### `full` — Everything
Pass the complete output including reasoning, sources, alternatives considered, and final deliverable.

**Use when:** Validator needs to assess the thinking, not just the result. Domain validators reviewing creator work.

### `artifacts_only` — Just the Deliverable
Pass only the final output/deliverable. Strip reasoning, drafts, and process notes.

**Use when:** Next agent should judge the work product on its own merits. Operators executing on approved work. Cross-domain handoffs.

### `summary` — Decisions Only
Pass a brief summary: what was decided, key constraints, and the deliverable reference. No supporting material.

**Use when:** Agent needs to know WHAT was decided but not HOW. Lightweight context for coordination. Status updates.

### `none` — Blind Review
Pass only the task description and the deliverable. No context about who created it, what the constraints were, or prior feedback.

**Use when:** Independent validation. Fact-checking. Testing (prevent curse of knowledge). Second opinions.

## Pipeline Defaults

| Transition | Default Strategy | Rationale |
|-----------|-----------------|-----------|
| Creator → Domain Validator | `full` | Validator needs reasoning to assess quality |
| Creator → Process Validator | `artifacts_only` | Process validator checks protocol compliance, not domain content |
| Validator → Creator (iterate) | `full` | Creator needs detailed feedback to improve |
| Creator → Operator | `artifacts_only` | Operator executes the deliverable, doesn't need the thinking |
| Any → [Your name] (escalate) | `summary` + link | [Your name] gets the decision point, not a wall of text |
| Research → Analysis | `full` | Analysis needs the complete evidence base |
| Analysis → Content | `summary` | Content needs the conclusions, not the methodology |

## How to Apply

When spawning a sub-agent or passing work between stages, include in the prompt:

```
Context strategy: [full|artifacts_only|summary|none]
```

For `artifacts_only`: explicitly say "You are receiving only the deliverable. You have no context about the creation process. Evaluate it on its own merits."

For `none`: explicitly say "This is a blind review. Evaluate without any context about the author, constraints, or prior feedback."

## Anti-Patterns

- **Dumping everything by default** — Wastes tokens, can bias validators
- **Giving operators the full reasoning** — They don't need it and it confuses execution
- **Blind-reviewing with context leaking in the prompt** — If you say "none" but include creator reasoning in the task description, it's not actually blind
