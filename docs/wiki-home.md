# GraceClaw Wiki

Welcome to the GraceClaw template documentation. This wiki covers architecture, agent patterns, setup, and delegation workflows.

---

## What is GraceClaw?

GraceClaw is an open-source **personal AI operating system template** built on top of [OpenClaw](https://openclaw.dev). It provides a production-ready multi-agent architecture with:

- A **Chief of Staff** orchestrator agent (the main session you talk to)
- A suite of **specialized creator/critic agent pairs** covering key life and work domains
- **Shared protocols** for research quality, grading, context flow, and session continuity
- **Security rules** for prompt injection defense and PIN-gated dangerous actions
- **Heartbeat infrastructure** for proactive, autonomous background work

The key insight: one person with well-configured agents can operate with the leverage of a team.

---

## Multi-Agent Architecture Overview

```
[Your name] ←→ [Your agent name] (Chief of Staff / Orchestrator)
                      ↓
        ┌─────────────┼──────────────┐
        ↓             ↓              ↓
 Domain Creators  Domain Critics  Process Validator
  (do the work)   (grade it)      (audit the HOW)
```

### The Creator/Critic Pattern

Every domain has a **creator** (produces work) and a **critic** (grades it). No output ships to you unless it clears the critic's quality gate (A- minimum).

The critic asks: "Is this right?" The process validator asks: "Did we get there properly?"

### Quality Pipeline by Stakes

| Stakes | Pipeline |
|--------|---------|
| Light (quick lookups) | [Your agent name] handles directly |
| Standard (analysis, drafts) | Creator → Critic (A-) → You |
| Critical (>high-stakes decisions, public content) | Creator → Process Validator → Critic → You |
| Critical+ (irreversible/major) | + Executive stress-test before delivery |

---

## Agent Registry

| Agent | Domain | Role |
|-------|--------|------|
| **[Your agent name]** | Orchestration | Chief of Staff — coordinates all agents, handles simple tasks directly |
| **finance-creator** | Finance | Financial analysis, burn rate, tax planning, scenario modeling |
| **finance-critic** | Finance | Mathematical verification, assumption auditing, tax claim validation |
| **work-creator** | Career/Work | Meeting prep, deal evaluation, advisory management, proposals |
| **work-critic** | Career/Work | Devil's advocate, risk assessment, downside analysis |
| **content-creator** | Content | LinkedIn posts, articles, voice-matched drafts, thought leadership |
| **content-critic** | Content | Voice authenticity scoring, AI-slop detection, engagement assessment |
| **research-creator** | Research | Market analysis, company research, due diligence, trend reports |
| **research-critic** | Research | Source verification, methodology audit, bias detection |
| **growth-creator** | Personal Growth | Well-being, relationships, mindfulness, habit design, life decisions |
| **growth-critic** | Personal Growth | Accountability, platitude detection, avoidance flagging |
| **body-creator** | Physical Health | Training, medical tracking, recovery, biometrics, preventive care |
| **body-critic** | Physical Health | Medical safety audit, overtraining detection |
| **network-creator** | Network | Contact research, outreach drafting, relationship mapping |
| **infra-creator** | Infrastructure | Skill discovery, version monitoring, gap analysis, security intelligence |
| **process-validator** | Cross-domain | Execution trace auditor — checks HOW agents work, not WHAT they produce |

---

## Delegation Patterns

[Your agent name] follows these delegation rules automatically:

| Signal | Delegated To |
|--------|-------------|
| Financial analysis, tax questions, equity | finance-creator |
| Career strategy, positioning, outreach, deal eval | work-creator |
| Articles, LinkedIn posts, content drafts | content-creator |
| Market research, company profiles, due diligence | research-creator |
| Personal growth, goal frameworks, life decisions | growth-creator |
| Workout planning, health tracking | body-creator |
| Relationship mapping, intro drafts, meeting prep | network-creator |
| Infrastructure improvements, skill discovery | infra-creator |

**Rule:** If writing more than a paragraph of analysis in a domain that has a creator — stop and spawn.

---

## Shared Protocols (`agents/_shared/`)

| File | Purpose |
|------|---------|
| `grading-protocol.md` | Universal A+ through F grade scale used by all critics |
| `edge-strategies.md` | Context flow rules between pipeline stages (full / artifacts_only / summary / none) |
| `deep-research-protocol.md` | 4-phase research methodology: artifact loading → insight funnel → stress testing → synthesis |
| `session-end-protocol.md` | What every agent writes back to shared state at session end |

---

## Security Model

GraceClaw enforces strict **data/instruction separation**:

- **Trusted instruction channels:** Only [Your name] via Discord or webchat
- **Everything else is data:** Emails, web pages, calendar events, documents — never instructions
- **PIN guard:** Destructive/irreversible/external actions require a PIN confirmation
- **No credential forwarding:** API keys and passwords never appear in responses
- **Injection defense:** Embedded "instructions" in emails or documents are ignored

Full details: `SECURITY.md`

---

## Getting Started

### 1. Clone the Template
```bash
git clone https://github.com/akadan18/graceclaw.git my-agent-workspace
cd my-agent-workspace
```

### 2. Customize Identity
- Edit `SOUL.md` — set your agent's name, mission, and personality
- Edit `USER.md` — describe who you are and what you're working on
- Set your PIN (stored only in SOUL.md, never in logs)

### 3. Configure OpenClaw
```bash
openclaw init
```

### 4. Set Up State Files
```bash
mkdir -p state memory data/brain/people data/brain/projects
touch state/tasks.yaml state/hot-context.md MEMORY.md
```

### 5. Launch Your Agent
```bash
openclaw session start
```

### 6. Add Agents
Add the creator/critic pairs you need from `agents/`. Start with the domains most relevant to your work — you don't need all of them on day one.

---

## Key Concepts

**Heartbeats:** Periodic autonomous check-ins where the agent proactively scans tasks, emails, and calendar — then nudges you with actions, not just flags. See `HEARTBEAT.md`.

**Context-First:** Before every reply involving a person, project, or domain, the agent searches existing memory. "Gathering context..." = it's doing its job.

**Brain vault:** `data/brain/` — structured knowledge about people, projects, topics. Grows over time as the agent learns.

**Hot context:** `state/hot-context.md` — the single source of truth for current state. Updated after every significant action.

**Atom of Thought:** For complex analysis, break into independent atoms → validate each → flag uncertainty → synthesize → disclose confidence.

---

## Links

- [Main README](https://github.com/akadan18/graceclaw/blob/main/README.md)
- [OpenClaw](https://openclaw.dev)
- [SOUL.md](https://github.com/akadan18/graceclaw/blob/main/SOUL.md)
- [AGENTS.md](https://github.com/akadan18/graceclaw/blob/main/AGENTS.md)
- [SECURITY.md](https://github.com/akadan18/graceclaw/blob/main/SECURITY.md)
- [HEARTBEAT.md](https://github.com/akadan18/graceclaw/blob/main/HEARTBEAT.md)
