# Persistent Session Protocol

## Overview
Persistent agents are long-running sessions that accumulate context across multiple interactions.
Unlike ephemeral agents (spawn → task → die), persistent agents maintain conversation history
and develop working memory over time.

## Architecture

### Session Lifecycle
1. **Boot**: [Your agent name] spawns via `sessions_spawn(mode: "session", label: "{agent-key}")`
2. **Active**: Agent receives work via `sessions_send(label: "{agent-key}", message: "...")`
3. **Idle**: Agent retains context between messages
4. **Compaction**: Context window fills → system compacts → agent recovers via state file
5. **Death**: Explicit kill or system restart → [Your agent name] re-spawns on next need

### Compaction Protection (Critical)
Every persistent agent MUST:
1. **Maintain a personal state file** at `state/sessions/{agent-key}.md`
2. **Update state file after every significant interaction** — decisions, findings, active work
3. **On every message, check if context feels thin** — if yes, re-read state file + persona .md
4. **Never rely solely on conversation history** — always write durable state to files

### State File Format (`state/sessions/{agent-key}.md`)
```markdown
# {Agent Name} — Session State
Last updated: {timestamp}

## Active Work
- What I'm currently working on

## Recent Decisions
- Key decisions from recent conversations

## Context Threads
- Open questions, waiting-on items

## Accumulated Knowledge
- Facts learned across sessions that aren't in shared state files
```

### Communication Protocol
Persistent agents can:
- **Receive from [Your agent name]**: Primary dispatch channel. [Your agent name] sends tasks and questions.
- **Respond to [Your agent name]**: Results, findings, questions, status updates.
- **Message other agents**: Via `sessions_send(label: "{other-agent}", message: "...")` for cross-domain coordination.
- **Read/write shared state**: `state/tasks.yaml`, `state/project-memory.yaml`, `state/goals.yaml`
- **Read brain/**: Domain-specific knowledge in `data/brain/`
- **Write to memory/**: Daily notes, findings

### Communication Rules
1. **Always identify yourself** in inter-agent messages: "This is finance-creator. I need..."
2. **Be specific** about what you need — other agents have different context windows
3. **Write findings to shared state** — don't assume conversation history is durable
4. **Escalate to [Your agent name]** for anything requiring [Your name]'s approval or external action

## Persistent Roster

| Agent | Model | Thinking | Label |
|-------|-------|----------|-------|
| finance-creator | claude-opus-4-6 | high | finance-creator |
| work-creator | claude-opus-4-6 | high | work-creator |
| content-creator | claude-opus-4-6 | high | content-creator |
| research-creator | claude-sonnet-4-6 | high | research-creator |
| growth-creator | claude-opus-4-6 | high | growth-creator |
| body-creator | claude-sonnet-4-6 | default | body-creator |
| network-creator | claude-sonnet-4-6 | default | network-creator |

### Ephemeral (NOT persistent)
All validators remain ephemeral — they're stateless by design (grade one artifact, return score, die).

## Boot Prompt Template
Each persistent agent's boot prompt follows this structure:
1. Identity block (from .md frontmatter)
2. Full persona file content (methodology, KPIs, learned patterns)
3. Persistent session wrapper (compaction recovery, communication protocol)
4. Workspace paths (shared state, brain, tools)
