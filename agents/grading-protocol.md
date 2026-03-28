# Grading Protocol — All Critics

Every critic review MUST end with a structured grade block. No exceptions.

## Grade Block Format

```
---
GRADE: [A+|A|A-|B+|B|B-|C|F]
SCORE: [0-100]
RATIONALE: [One sentence explaining the grade]
TOP_ISSUE: [Single most important thing to fix, or "None" if A- or above]
---
```

## Grade Scale

| Grade | Score | Meaning | Action |
|-------|-------|---------|--------|
| A+ | 97-100 | Exceptional — exceeds requirements | Ship |
| A | 93-96 | Strong — meets all requirements | Ship |
| A- | 90-92 | Adequate — meets requirements with minor gaps | Ship (minimum threshold) |
| B+ | 87-89 | Close — 1-2 meaningful issues | Iterate with feedback |
| B | 83-86 | Needs work — several issues | Iterate with feedback |
| B- | 80-82 | Significant gaps | Iterate urgently, flag to user |
| C | 70-79 | Major problems | Escalate to user |
| F | 0-69 | Fundamental rework needed | Escalate to user immediately |

## Threshold Rules

- **Ship threshold: A- (90)** — Output can go to user or next pipeline stage
- **Iteration budget: 3 rounds max** — If still below A- after 3 iterations, escalate
- **Auto-escalate: Below B-** — Don't iterate, go straight to user
- **The orchestrator decides** whether to iterate or escalate. Validators grade, they don't decide.

## Grading Principles

1. **Grade the output, not the effort.** A brilliant attempt that misses the mark is still a B.
2. **Grade against the task requirements.** An A+ research report might be a C pitch deck.
3. **Be honest, not generous.** Inflated grades defeat the purpose. If it's a B+, say B+.
4. **TOP_ISSUE must be actionable.** "Could be better" is not a top issue. "Missing financial projections for Year 2" is.
5. **Don't grade on a curve.** Every output is judged against absolute quality standards.
6. **Provenance matters.** For research and financial outputs: every factual claim should be traceable to a source ([found], [calculated], [inferred], [estimated], [external]). Unsourced claims in research/finance deliverables are flagged as TOP_ISSUE. This doesn't apply to casual analysis or brainstorming — only formal deliverables.

## Edge Strategies (What Context to Grade Against)

Validators receive context differently depending on the review type:

| Review Type | Context Strategy | Why |
|-------------|-----------------|-----|
| Creator output review | `full` | Validator needs full reasoning + output to assess quality |
| Cross-domain handoff review | `artifacts_only` | Validator should judge the deliverable, not the creator's process |
| Independent validation | `none` | Validator should evaluate blind (e.g., fact-checking without seeing sources) |
| Operator execution review | `summary` | Just confirm execution matched the plan |

When spawning a critic sub-agent, the orchestrator specifies which strategy applies.

## Eval Logging (mandatory)

After every grade, the orchestrator (main agent) appends an entry to `state/evals.yaml`:

```yaml
- id: eval-NNN
  timestamp: "2026-02-19T14:30:00-08:00"
  task_id: task-042  # if applicable
  agent: finance-creator
  critic: finance-critic
  category: finance
  grade: A-
  score: 91
  iterations: 1
  rationale: "Accurate analysis but missed Q4 projections"
  top_issue: "None"
  outcome: shipped
```

**Rules:**
- Every graded output gets logged — no exceptions
- `outcome` is one of: `shipped` (≥A-), `iterated` (sent back), `escalated` (to user)
- The orchestrator logs this, not the critic (critics grade, orchestrator records)
- Daily Reflection aggregates stats nightly

## Integration

- All critics reference this file: `Read agents/_shared/grading-protocol.md`
- The orchestrator uses the grade to decide: ship / iterate / escalate
- Grades are logged in `state/evals.yaml` for quality tracking over time
- Daily Reflection computes grade distribution, per-agent averages, escalation rate
- Morning Briefing flags: any agent with avg score dropping, escalation rate >20%, or 2+ consecutive sub-A- grades
- Patterns from grades feed into `state/project-memory.yaml` via reflection
