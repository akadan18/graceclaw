# AGENTS.md — Session Protocols

## Every Session — Wake Protocol

1. Read `SOUL.md` — who you are
2. Read `state/checkpoint.md` — where you left off, open items
3. Read `state/system-overview.yaml` — current system state

## During Session — Checkpoint Protocol

After completing a significant task or before a risky operation:
- Update `state/checkpoint.md` with what was done and what's open
- Write decisions to `memory/decisions.md` (title + rationale + date)
- Write lessons to `memory/lessons.md` (what was learned + when to apply)

## End of Session — Sleep Protocol

1. Append key findings/outcomes to `memory/notes.md` with date
2. Update `state/checkpoint.md`: set status, summarize what was done, list open items
3. Update `state/system-overview.yaml` if anything changed

## Task Creation

Before creating a task, check if it already exists. Use a single task list:
`state/tasks.yaml`

Task schema:
```yaml
- id: "task-NNN"
  title: "Clear, actionable title"
  status: "open | in-progress | waiting | done"
  priority: "high | medium | low"
  owner: "[user name] | agent"
  created: "YYYY-MM-DD"
  due_date: "YYYY-MM-DD"  # optional
  next_action: "Who does what next"
  context: "Why this matters, any relevant background"
  complexity:            # optional — see docs/autonomy-levels.md
    scope: 1-5
    judgment: 1-5
    stakes: 1-5
    novelty: 1-5
    total: 4-20
    level: 1-5
  mode: "auto | summary | approval | guided | manual"
```

### Autonomy Levels

| Level | Score | Human Involvement | Handling |
|-------|-------|-------------------|----------|
| L1 | 4-6 | None — cron handles it | Silent, log only |
| L2 | 7-9 | Read the summary | Deliver to channel |
| L3 | 10-13 | Approve before action | Draft, hold for PIN |
| L4 | 14-17 | Human directs | Surface options, human decides |
| L5 | 18-20 | Human only | Context prep only |

Full scoring rubric: `docs/autonomy-levels.md`

## Memory System

- `memory/notes.md` — ongoing findings and observations (append-only, date each entry)
- `memory/decisions.md` — decisions made and why (title + rationale + date)
- `memory/lessons.md` — patterns learned (what works, what doesn't)
- `state/project-memory.yaml` — high-quality persistent learnings (see file for quality standard)

When to add to project-memory.yaml vs memory/notes.md:
- **notes.md**: anything you observe, even once, even if it might be temporary
- **project-memory.yaml**: only patterns you're confident will apply again (see 4-test filter in that file)

## Context-First Protocol (non-negotiable)

Before acting on ANY request:

1. **Match to tasks** — does this relate to something in tasks.yaml? Load the task context.
2. **Check existing knowledge** — search brain/, memory/ for relevant info. Don't ask the user what you can look up yourself.
3. **Load domain files** — use this lookup table:

| Request type | Files to load |
|-------------|--------------|
| Meeting prep | `data/brain/people/[person].md`, calendar event, `state/hot-context.md` |
| Work / consulting | `data/brain/projects/[project].md`, recent emails, `state/hot-context.md` |
| Content / writing | `data/brain/content/voice-dna-template.md`, relevant drafts |
| Task update | `state/tasks.yaml` (read the actual task), email/calendar for latest signal |
| Research | `data/brain/topics/[topic].md` if exists, then external sources |
| Infrastructure | `state/system-overview.yaml`, `TOOLS-AND-APPS.md`, `agents/agent-registry-template.yaml` |

4. **Then act.** Never ask "what do you want me to know about X?" if you can look it up.

---

## Compaction Protection

Before context window fills: run reflection protocol + write handoff note to `state/hot-context.md → ## Last Session`.
After compaction: re-read hot-context.md before responding.
Full protocol: `agents/compaction-protection.md`

---

## Execution Tiers

Every request gets classified before work begins:
- 🟢 **Light** — just do it, no pipeline
- 🟡 **Standard** — creator → critic (A- to ship)
- 🔴 **Critical** — process validator → domain critic → user

Full protocol: `agents/execution-protocol.md`
