# Reflection Protocol

Run this after completing any significant workflow or at the end of a session.
Takes 2–5 minutes. Keeps your memory system useful over time.

---

## When to Reflect

- After completing a multi-step task
- After a mistake or unexpected outcome
- After a workflow that could repeat (same pattern likely to occur again)
- At the end of a long session
- When explicitly asked

---

## Step 1: What Happened?

Write 2–3 sentences in memory/notes.md:
- What was the goal?
- What was done?
- What was the outcome?

Format:
```
## [Date] — [Brief title]
[Goal]: ...
[Done]: ...
[Outcome]: ...
```

---

## Step 2: Was There a Lesson?

Ask: "Is there a pattern here that would help in a future situation?"

A lesson is worth capturing if it's:
1. **Transferable** — applies beyond this exact situation
2. **Insightful** — not obvious from existing docs or common sense
3. **Behavioral** — about what works/fails, not just how things are configured
4. **Durable** — won't be irrelevant in a month

If yes → go to Step 3.
If no → append to memory/notes.md and stop.

---

## Step 3: Extract the Learning

Write it as a concise, actionable pattern statement (not an observation):

❌ "The user's email was unclear about the recipient"
✅ "Ambiguous recipient emails require explicit confirmation before drafting — default to most recent thread context"

Add to `state/project-memory.yaml`:

```yaml
- id: "learn-NNN"        # use next available number
  type: "process_pattern"
  insight: "Your pattern statement here"
  source:
    workflow: "which workflow"
    observation: "what triggered this"
    date: "YYYY-MM-DD"
  source_ref: "task-NNN | memory/YYYY-MM-DD.md"
  first_observed: "YYYY-MM-DD"
  last_verified: "YYYY-MM-DD"
  times_reinforced: 0
  confidence: "hypothesis"  # start as hypothesis, upgrade to verified after 2+ reinforcements
  applicable_to: ["domain"]
```

**On reinforce:** If you see the same pattern again, increment `times_reinforced` and update `last_verified`. After 2+ reinforcements, upgrade confidence to `verified`.

---

## Step 4: Update Checkpoint

Update `state/checkpoint.md`:
- Mark completed items done
- Add any new open items surfaced during the workflow
- Note any blockers or waiting items
