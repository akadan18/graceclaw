# Session End Protocol

Run this after any session that produced meaningful output.
Takes 2 minutes. Without it, multi-agent context evaporates.

## When to Run
- After producing: analysis, drafts, recommendations, decisions, or new information
- After any session where state changed
- NOT after trivial single-question exchanges

## When NOT to Run
- Trivial exchanges (< 2 turns, no work produced)
- Pure read-only sessions (looked something up, no new findings)

---

## Step 1: Append to `state/hot-context.md` → Active Threads

Find the relevant thread (or create one) and append:

```markdown
**[Agent Name] — [YYYY-MM-DD HH:MM]**
- What was discussed/produced
- Key decisions or outputs
- What other agents need to know
- Open loops / next steps
```

---

## Step 2: Append to `memory/YYYY-MM-DD.md` (today's daily notes)

```markdown
## [Agent Name] Session — [HH:MM]
- [Brief summary of work done]
- [Key output or file produced, if any]
- [Anything to remember or follow up on]
```

---

## Step 3: Update `state/tasks.yaml`

If a task was worked on:
- Update `status`, `notes`, `next_action`, `due_date` as needed
- If completed: add `resolution: "What happened, when, outcome"` before marking done

---

## Step 4: Update `state/activity-feed.yaml`

Append one entry per meaningful action taken:
```yaml
- id: "act-NNN"
  timestamp: "YYYY-MM-DDTHH:MM:SS"
  agent: "[your agent name]"
  task_id: "task-NNN"
  action: "What was done"
  output: "What was produced"
  status: "completed | partial | escalated"
```

---

## What NOT to Write
- Don't dump the full conversation transcript
- Skip routine status already captured in tasks.yaml
- Skip if session was truly trivial

## Why This Matters
Agent sessions are isolated. The main agent can't see your conversation history. The only shared memory is the file system. If you don't write back, your work disappears from the system's awareness.

**Rule:** If your session mattered, write it down. If you wouldn't want the main agent to miss it, write it down.
