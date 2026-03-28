# SETUP.md — OpenClaw Starter Kit

## What This Is

A battle-tested foundation for a personal AI assistant built on OpenClaw.
Developed from a real production setup running 14 agents and 15 crons.

**Give this folder to your OpenClaw agent and ask it to run through this file.**

---

## Step 1: Read the Kit

Before doing anything, read these files in order:

1. `USER.md` — who you are (pre-filled by the person who gave you this kit)
2. `SOUL.md` — your identity and mandate (template, needs personalization)
3. `AGENTS.md` — your session protocols (mostly universal, minimal changes)
4. `SECURITY.md` — hard rules that protect the user (do not modify)

---

## Step 2: Personalize SOUL.md

Ask the user these questions and fill in SOUL.md from their answers:

1. What should I call you, and what do you want me to call myself?
2. What are the 3–5 most important domains of your life right now? (work, health, family, money, etc.)
3. What's your single biggest priority this quarter?
4. What are your hard rules — things you'd never want me to do without asking first?
5. How do you like to communicate? (brief, detailed, casual, formal?)
6. What does a good day look like for you?

---

## Step 3: Set Up State Files

Create or initialize these files:

- `state/checkpoint.md` — your current status, what was last done, what's open
- `state/project-memory.yaml` — persistent learnings (starts empty, grows over time)
- `state/system-overview.yaml` — current system state (tools, agents, integrations)

Use the templates in this kit. The agent fills them in based on conversation.

---

## Step 4: Install Recommended Skills

Run these via `clawhub install`:

```
clawhub install gog          # Google Workspace (Gmail, Calendar, Drive, Sheets, Docs)
clawhub install github       # GitHub — PRs, issues, CI
clawhub install himalaya     # Email via IMAP/SMTP (if not using gog)
clawhub install git-ops      # Push/pull git repos via chat
clawhub install weather      # Weather lookups
clawhub install apple-notes  # Apple Notes integration
```

Authenticate gog after install:
```
gog auth setup
gog auth login
```

---

## Step 5: Set Up Recommended Crons

After SOUL.md is finalized, suggest these crons to the user:

1. **Daily digest** (8 AM) — summarize today's calendar + top 3 priorities → post to Discord/Telegram
2. **Weekly review** (Sunday 6 PM) — review what got done, what didn't, update checkpoint
3. **Agent heartbeat** (every 4h) — confirm agent is alive, nothing blocked

---

## Step 6: Build Your Brain

Create a `data/brain/` folder structure:

```
data/brain/
├── topics/     — concepts, frameworks, ideas you work with
├── people/     — contacts, relationships, context
├── projects/   — active work, engagements, initiatives
└── content/    — articles, newsletters, reference material
```

Add files over time as the agent encounters relevant info. The agent should:
- Create a file whenever a new important person/concept/project appears
- Add YAML frontmatter to each file (see brain/README.md)
- Link related files with `[[wikilinks]]`

---

## Step 7: Done

Once setup is complete:
- Update `state/checkpoint.md` with status: "setup complete"
- Confirm all crons are active
- Ask the user: "What's the most useful thing I could do for you today?"
