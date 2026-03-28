# Compaction Protection

Context windows have limits. When a session fills up, the system compacts — earlier conversation history is compressed or dropped. Without preparation, you lose context mid-task.

This protocol prevents that.

---

## BEFORE Compaction (when context feels full, or before a long task)

Run in this order:

**1. Run reflection protocol** (`agents/reflection-protocol.md`)
- Extract any learnings from this session
- Update tasks with latest status
- Append to daily notes

**2. Write your handoff note to `state/hot-context.md` → `## Last Session` section**
```markdown
## Last Session (compaction recovery + handoff)
**When:** [Date/time]
**What was happening:**
- [Task in progress]
- [Key decision made]
- [Information received]
**What matters NOW:**
1. [Most urgent item]
2. [Second most urgent]
```

**3. Write open tasks to `state/checkpoint.md`**
Update: what was done, what's in progress, what's blocked.

**4. Write any agent-specific state to `state/sessions/[agent-key].md`**
For persistent sessions: what you're currently working on, where you left off, any partial work product.

---

## AFTER Compaction (fresh session start, or when context feels thin)

Signs you've been compacted: you don't remember recent conversation, context feels sparse.

**1. Re-read `state/hot-context.md`**
The `## Last Session` section tells you what was JUST happening. This is your handoff note from pre-compaction you.

**2. Re-read your persona file** (`agents/[your-persona].md`)
Remind yourself who you are and what your mandate covers.

**3. Re-read `state/checkpoint.md`**
What's open? What's in progress? What's blocked?

**4. Resume from checkpoint — don't re-explain the loss**
Don't tell the user "I lost context." Just re-read the state, reconstruct, and continue. If something critical is missing, ask one targeted question.

---

## Persistent Session Specific

If you're a persistent agent (long-running session, receives work via sessions_send):

1. **Maintain `state/sessions/[agent-key].md`** — update after every significant interaction
2. **On every incoming message:** check if context feels thin. If yes, re-read your state file + persona before responding.
3. **Never rely solely on conversation history** — it can compact. Always write durable state to files.

State file format:
```markdown
# [Agent Name] — Session State
Last updated: [timestamp]

## Active Work
[What you're currently working on]

## Recent Findings
[Key things you've discovered this session]

## Open Questions
[Things you need to resolve or ask about]

## Key Decisions Made
[Decisions from this session that should persist]
```
