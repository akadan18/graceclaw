# Session End Protocol — All Agents

Every agent session that produces meaningful output MUST write a brief summary back to shared state before ending. This is how context flows between isolated sessions — without it, [Your agent name] and other agents are blind to what happened.

## When to Run
- After any session that produced: analysis, drafts, recommendations, decisions, or new information
- NOT after trivial exchanges (quick lookups, single-question answers)
- ALWAYS after: substantive conversations, multi-turn work, anything that changes state

## What to Write

### 1. Append to `state/hot-context.md` → Active Threads section

Find the relevant thread (or create one) and append:
```markdown
**[Agent Name] — [YYYY-MM-DD HH:MM]**
- What was discussed/produced
- Key decisions or outputs
- What [Your agent name] or other agents need to know
- Open loops / next steps
```

### 2. Append to `memory/YYYY-MM-DD.md` (today's daily notes)

```markdown
## [Agent Name] Session — [HH:MM]
- [Brief summary of work done]
- [Key output/file produced, if any]
- [Anything to remember]
```

### 3. Update `state/tasks.yaml` (if a task was worked on)
- Update `status`, `notes`, `due_date` as needed
- Add resolution note if completed

## What NOT to Write
- Don't dump the full conversation transcript
- Don't include personal/sensitive details unnecessarily
- Skip routine status that's already in tasks.yaml
- Skip if session was truly trivial (<2 exchanges, no work produced)

## Why This Matters
Agent sessions are isolated — [Your agent name] can't see your conversation history. The only shared memory is the file system. If you don't write back, your work disappears from the system's awareness. Context Keeper sweeps hot-context.md 3x/day, but it can only synthesize what's been written down.

**The rule:** If your session mattered, write it down. If you wouldn't want [Your agent name] to miss it, write it down.
