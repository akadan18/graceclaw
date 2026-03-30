# Task Autonomy & Complexity Scoring — GraceClaw

## Why This Matters

Not every task needs your attention. An overdue FSA reimbursement needs you. A routine email triage doesn't. Autonomy levels auto-route tasks to the right handling depth.

## Five Levels

### Level 1 — Full Autonomous
**Complexity:** Low | **Human involvement:** None — cron handles it

- Routine scans, data logging, backup, context updates
- Agent handles end-to-end, reports only if something's wrong
- Examples: email triage (no action items), daily context keeper, git backups

**Signals:** repeatable, no judgment call, no external communication

---

### Level 2 — Autonomous with Summary
**Complexity:** Low-Medium | **Human involvement:** Read the summary

- Scans that surface information but don't act on it
- Agent does the work, delivers a summary, Artem reviews at leisure
- Examples: Morning Parliament, weekly infra scan, financial report

**Signals:** information delivery, no decisions needed from Artem in real-time

---

### Level 3 — Autonomous with Approval Gate
**Complexity:** Medium | **Human involvement:** Approve before action

- Agent researches, drafts, recommends — but waits for approval before executing
- Examples: Draft email replies, LinkedIn message drafts, purchase recommendations, skill installations

**Signals:** involves external communication, spending money, or system changes

---

### Level 4 — Guided by Artem
**Complexity:** High | **Human involvement:** Artem directs, agents assist

- Strategic decisions, career moves, relationship navigation
- Agents provide analysis and options, Artem makes the call
- Examples: Consulting engagement negotiations, investment decisions, content strategy

**Signals:** judgment required, high stakes, involves personal relationships or money

---

### Level 5 — Artem Only
**Complexity:** Very High | **Human involvement:** Only Artem can do this

- Personal conversations, creative expression, taste-dependent decisions
- Agents can prep context but can't act
- Examples: Burning Man planning replies, personal messages, final content voice

**Signals:** authenticity required, deeply personal, taste-driven

---

## Complexity Scoring

Score each task 1-5 on four dimensions. Sum = complexity score.

| Dimension | 1 (Low) | 3 (Medium) | 5 (High) |
|-----------|---------|------------|----------|
| **Scope** | Single agent, one action | Multi-agent, several steps | Cross-domain, many dependencies |
| **Judgment** | Rules-based, no ambiguity | Some interpretation needed | Requires taste/intuition |
| **Stakes** | Easily reversible, no impact | Affects schedule or money | Affects relationships or career |
| **Novelty** | Done this before | Similar pattern exists | No precedent |

### Score → Level Mapping

| Score | Level | Handling |
|-------|-------|----------|
| 4-6 | L1: Full Autonomous | Cron handles silently |
| 7-9 | L2: Autonomous + Summary | Delivered to channel, read at leisure |
| 10-13 | L3: Autonomous + Approval | Agent drafts, waits for PIN/go-ahead |
| 14-17 | L4: Guided | Artem directs, agents assist |
| 18-20 | L5: Artem Only | Context prep only |

### In tasks.yaml

```yaml
- id: task-99
  title: "Triage morning emails"
  complexity:
    scope: 1
    judgment: 1
    stakes: 1
    novelty: 1
    total: 4
    level: 1
  mode: auto

- id: task-100
  title: "Negotiate Instrumental consulting rate"
  complexity:
    scope: 3
    judgment: 5
    stakes: 5
    novelty: 3
    total: 16
    level: 4
  mode: guided
```

## Integration with Crons

| Level | Cron Behavior |
|-------|---------------|
| L1 | Run silently, log to state, no delivery |
| L2 | Run and deliver summary to appropriate channel |
| L3 | Run, draft output, hold for approval before external action |
| L4 | Surface in Morning Parliament with context + options |
| L5 | Surface in Morning Parliament as "needs Artem" |

## Auto-Classification

When a new task enters tasks.yaml (via email scan, cron, or manual creation):

1. Score each dimension based on title + context
2. Map to level
3. Set `mode:` field (auto / summary / approval / guided / manual)
4. Route to appropriate handling

Over time, the reflection protocol refines scoring. If an L2 task triggered a human intervention, it was probably L3. Log the learning.
