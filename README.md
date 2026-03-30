<p align="center">
  <picture>
    <source srcset="docs/logo-dark.svg" media="(prefers-color-scheme: dark)">
    <source srcset="docs/logo-light.svg" media="(prefers-color-scheme: light)">
    <img src="docs/logo-dark.svg" alt="GraceClaw" height="42">
  </picture>
</p>
<p align="center"><strong>Personal Agentic AI Operating System</strong></p>
<p align="center"><em>by <a href="https://linkedin.com/in/artemkroupenev">Artem Kroupenev</a> · <a href="https://substack.com/@artemkroupenev">Substack</a></em></p>
<p align="center">A battle-tested foundation for building a personal agentic AI OS on <a href="https://openclaw.ai">OpenClaw</a>.</p>

Built from a real production setup running daily — 14 agents, 15+ crons, hundreds of sessions worth of iteration.
Not a toy. This is the architecture that actually worked.

---

## What This Is

A complete workspace template that gives you:

- **Multi-agent pipeline** — creator agents produce work, critic agents stress-test it before it reaches you
- **Persistent memory** — 4-layer memory stack that compounds over time (semantic search, daily notes, structured learnings, live state)
- **Research methodology** — Deep Research Protocol (3-layer insight funnel) + Atom of Thought (structured reasoning with uncertainty disclosure)
- **Security built in** — hard rules for email, money, git, and irreversible actions. PIN guards. Prompt injection defense.
- **Brain vault** — Obsidian-compatible knowledge base for people, projects, topics, and your writing voice
- **Task architecture** — single task queue with goal ancestry, atomic checkout, and engagement tagging

---

## Quick Start

### 1. Install OpenClaw
```bash
npm install -g openclaw
openclaw init
```

### 2. Clone this kit into your workspace
```bash
git clone https://github.com/YOUR_USERNAME/grace-openclaw-kit.git
# Point your OpenClaw workspace at the cloned folder
```

### 3. Fill in USER.md (5 minutes)

### 4. Tell your agent:
> "Read SETUP.md and help me set up my OpenClaw instance"

The agent walks through setup interactively — personalizes your SOUL.md, installs recommended skills, sets up crons.

---

## What's In Here

```
grace-openclaw-kit/
├── SETUP.md              ← Agent reads this to run setup
├── USER.md               ← Fill in: who you are
├── SOUL.md               ← Your agent's identity (template)
├── AGENTS.md             ← Session protocols + context-first rules
├── SECURITY.md           ← Hard rules — email, money, git, privacy
├── MEMORY.md             ← Long-term semantic memory (grows over time)
├── TOOLS-AND-APPS.md     ← What to install and connect
│
├── agents/
│   ├── execution-protocol.md         ← 🟢🟡🔴 complexity gate
│   ├── creator-critic-pattern.md     ← Creator → Critic pipeline + grade system
│   ├── process-validator-template.md ← HOW auditor (Validator tier)
│   ├── agent-registry-template.yaml  ← Pipeline map with routing rules
│   ├── deep-research-protocol.md     ← 3-layer insight funnel methodology
│   ├── atom-of-thought.md            ← Structured reasoning with uncertainty
│   ├── edge-strategies.md            ← Context flow between agents
│   ├── network-creator-template.md   ← Relationship management agent
│   ├── reflection-protocol.md        ← Post-session learning extraction
│   ├── consolidation-protocol.md     ← Monthly memory maintenance
│   ├── session-end-protocol.md       ← Multi-agent context handoff
│   ├── compaction-protection.md      ← Context window survival
│   └── grading-protocol.md          ← A-/B+ quality gates
│
├── state/
│   ├── hot-context.md         ← Live grounding + compaction recovery
│   ├── checkpoint.md          ← Current status + open items
│   ├── tasks.yaml             ← Task queue (single source of truth)
│   ├── goals.yaml             ← Mission → goal → task hierarchy
│   ├── project-memory.yaml    ← Filtered persistent learnings
│   ├── system-overview.yaml   ← Current system state
│   ├── evals.yaml             ← Validator grade log
│   ├── activity-feed.yaml     ← Agent action audit trail
│   ├── contacts.yaml          ← Network relationship database
│   └── top-patterns.md        ← Cross-agent pattern aggregation
│
├── memory/
│   ├── notes.md               ← Append-only observations
│   ├── decisions.md           ← Key decisions + rationale
│   └── YYYY-MM-DD-template.md ← Daily notes template
│
└── data/brain/
    ├── README.md              ← How to use the brain vault
    ├── content/               ← Voice DNA + writing style
    ├── people/                ← Contact knowledge files
    ├── projects/              ← Active work files
    └── topics/                ← Concepts and frameworks
```

---

## Key Principles

**Memory that compounds.** The brain vault + 4-layer memory stack means your agent gets smarter over time. Every important fact has a source. Every lesson passes a 4-test quality filter before it's stored.

**Security is explicit.** Hard rules prevent the most common agent mistakes — sending emails without review, auto-accepting financial actions, force-pushing git. These aren't suggestions; they're enforced at the identity layer.

**Creator → Critic → Validator pipeline.** Every creator has an adversarial critic. Hard A- ship threshold. 3-round iteration cap, then escalates to you. Process validator checks HOW agents work; domain critics check WHAT they produced.

**Research methodology built in.** Deep Research Protocol prevents lazy AI research (load real artifacts, 3-layer insight funnel, stress test). Atom of Thought prevents confident hallucination (decompose → validate → label → disclose uncertainty).

**Tasks as source of truth.** Everything open lives in tasks.yaml. Agents don't hold context between sessions — they read the file. Nothing gets lost.

---

## Recommended Stack

| Tool | Purpose |
|------|---------|
| [OpenClaw](https://openclaw.ai) | Runtime |
| [Claude Code](https://docs.anthropic.com/claude-code) | Coding agent |
| [Obsidian](https://obsidian.md) | Brain vault UI (open `data/brain/` as vault) |
| `gog` (clawhub) | Google Workspace — Gmail, Calendar, Drive |
| `gh` (brew) | GitHub CLI |
| 1Password CLI | Secret management |
| Discord or Telegram | Agent communication channel |

Full install guide: [TOOLS-AND-APPS.md](TOOLS-AND-APPS.md)

---

## Lessons Baked In

This kit encodes real lessons from production use:

- **AGENTS.md kept under 15K chars** — OpenClaw silently truncates at 20K. Extract large sections to separate files that agents `Read` on demand.
- **Memory search tuned** — MMR (lambda 0.7) + temporal decay (30-day half-life) reduce duplicate snippets and favor recent context.
- **Cron timeouts sized for thinking** — If using `thinking: high`, budget 300-600s timeouts. Sonnet handles most cron workloads fine without extended thinking.
- **PIN at the identity layer** — Security rules in shared files don't propagate to creator agents. Put PIN rules in each agent's SOUL.md, not a shared SECURITY.md.
- **Daily notes during sessions, not after** — Don't wait for a nightly reflection cron. Write raw material during the session so the cron has something to distill.
- **Verify before claiming** — Agents hallucinate infrastructure facts confidently. Always check the actual config/file before stating "you already have X configured."

---

## Post-Setup Recommendations

After your first week:

1. **Run `openclaw doctor`** — catches config drift and warns about bootstrap file size limits
2. **Set up nightly git backup** — cron that commits and pushes workspace changes
3. **Enable memory search** — configure embedding provider in openclaw.json for semantic recall
4. **Create a reflection cron** — nightly learning extraction compounds fast

---

## ⚠️ Privacy Notice

Once you fill in USER.md, SOUL.md, MEMORY.md, and daily notes with personal data, **keep this repo private**. The `.gitignore` excludes the most sensitive files, but always review before any push.

---

## License

MIT — see [LICENSE](LICENSE)
