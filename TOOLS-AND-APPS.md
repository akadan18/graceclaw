# Tools & Apps — Recommended Stack

What to install, connect, and configure. Ordered by priority.

---

## 🔴 Core (Install First)

### OpenClaw
The runtime. Everything else runs through it.
```bash
npm install -g openclaw
openclaw start
```
https://openclaw.ai

### Claude Code (Anthropic)
Coding agent that runs in your terminal. Spawned by your agent for any code/build tasks.
```bash
npm install -g @anthropic-ai/claude-code
```
Usage: Your main agent runs `claude --print "..."` for coding tasks. Never let it run in your main workspace — always spawn in a project directory.
https://docs.anthropic.com/claude-code

### Discord
Primary channel for agent communication (or Telegram — pick one, be consistent).
- Create a server with dedicated channels per agent: #main, #work, #research, #finance, #infra
- Connect in openclaw.json: `channel: discord`
- One channel per creator agent = clean separation of context

---

## 🟡 High Value (Install in Week 1)

### Google Workspace CLI (gog)
Gives agents access to Gmail, Calendar, Drive, Sheets, Docs via CLI.
```bash
clawhub install gog
gog auth setup
gog auth login
```
Enables: email triage, calendar briefings, Drive search, Sheets read/write.

### GitHub CLI (gh)
Code ops: PRs, issues, CI status, repo management.
```bash
brew install gh
gh auth login
```
```bash
clawhub install github
```

### Obsidian
The human-facing UI for your brain vault. The `data/brain/` folder IS an Obsidian vault — just point Obsidian at it.
- Download: https://obsidian.md (free, no account needed)
- Open vault: `File → Open Folder as Vault → data/brain/`

**What you get immediately:**
- Every person, project, and topic file your agent has written is browsable
- Wikilinks (`[[file]]`) resolve automatically — click any `[[Person Name]]` and jump to their file
- Graph View shows the relationship map of your entire knowledge base — visually see how people, projects, and topics connect
- Full-text search across everything your agent has ever written

**Recommended plugins (Community → Browse):**
- **Dataview** — query your notes like a database: "show all people tagged [investor] sorted by last-contact"
- **Templates** — standardize new brain file creation
- **Calendar** — navigate daily notes by date

**The workflow:** Agents write files, you read and navigate in Obsidian. It's the windshield for the brain vault — agents build it in the background, you explore it visually. Over time the graph becomes genuinely useful as your knowledge compounds.

### 1Password CLI (op)
Secret management. Agents can read credentials without storing them in plaintext.
```bash
brew install 1password-cli
op signin
```
```bash
clawhub install 1password
```
Usage: Store API keys in 1Password. Agents call `op read "op://vault/item/field"` instead of hardcoding secrets.

---

## 🟡 Communication (Connect What You Use)

### Telegram Bot (alternative to Discord)
Lighter than Discord, works well on mobile. Good if you don't want a full Discord server.
- Create bot via @BotFather
- Connect in openclaw config

### iMessage (macOS only)
```bash
clawhub install imsg
```
Lets agents send/read iMessages. Useful for personal contacts who use iMessage.

### Gmail / Email
Already covered by `gog`. If you use a non-Google email provider:
```bash
clawhub install himalaya   # IMAP/SMTP for any email provider
```

---

## 🟡 Productivity Integrations

### Apple Reminders
```bash
clawhub install apple-reminders
```
Agents can create, list, and complete reminders.

### Apple Notes
```bash
clawhub install apple-notes
```
Quick notes without opening an app.

### Google Calendar
Included in `gog`. No separate install needed.

---

## 🟢 Research & Intelligence

### Web Search (Brave API)
Built into OpenClaw. Agents use `web_search` automatically.
- No setup needed — configured in openclaw.json

### blogwatcher
```bash
clawhub install blogwatcher
```
Monitor RSS/Atom feeds. Useful for: tracking industry news, monitoring competitor blogs, research sources.

### Gemini CLI
Fast, free AI for lightweight tasks. Good for triaging with gemini-flash before using Claude.
```bash
clawhub install gemini
```

---

## 🟢 Developer Tools

### Git / GitHub
```bash
xcode-select --install   # macOS: installs git
```
Agents should NEVER `git push --force`. See SECURITY.md.

### Node.js / npm
Required for OpenClaw and many skills.
```bash
brew install node
```

### Python 3
Required for some scripts.
```bash
brew install python3
```

### Homebrew (macOS)
Package manager. Install everything above via `brew`.
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

## 🟢 Optional but Powerful

### LiteLLM (only if rate limits become an issue)
Routes requests across multiple AI providers (Gemini, Groq, Mistral, OpenRouter).
Only add this if you're hitting Anthropic rate limits with multiple crons running.
```bash
pip install litellm
```
Not needed at the start. Add when you have 10+ active crons.

### Peekaboo (macOS screenshot/UI automation)
```bash
clawhub install peekaboo
```
Agents can take screenshots and automate macOS UI. Useful for: capturing state, navigating apps without APIs.

### Eight Sleep CTL (if you have an Eight Sleep pod)
```bash
clawhub install eightctl
```

### Weather
```bash
clawhub install weather
```
Built on wttr.in. No API key. Good for crons that mention outdoor plans.

---

## Recommended Crons (after setup)

| Cron | Schedule | What it does |
|------|----------|-------------|
| Daily digest | 8 AM Mon-Fri | Calendar + top 3 priorities → Discord |
| Email triage | 7 AM Mon-Fri | Unread inbox → URGENT/REVIEW/PERSONAL/NOISE |
| Weekly review | Sunday 6 PM | What got done, update checkpoint |
| Security audit | Weekly | Check OpenClaw version, npm updates, exposed ports |
| Heartbeat | Every 4h | Confirm agent is alive, nothing blocked |
| Daily reflection | 10 PM | Distill daily notes into learnings |
| Context Keeper | 3x/day | Sweep hot-context.md, keep state current |

---

## Model Choices

| Task | Recommended Model | Why |
|------|------------------|-----|
| Main agent | claude-sonnet (latest) | Balance of quality + speed |
| Complex analysis | claude-opus (latest) | Financial, career decisions |
| Financial critic | claude-opus (latest) | Accuracy matters more here |
| Lightweight crons | gemini-flash (latest) | Free tier, fast, good enough |
| Code tasks (Claude Code) | claude-sonnet (latest) | Default in claude code |

Rule: Use Opus only where getting it wrong costs real money or opportunity.
Use Gemini/Groq for crons and tasks where 80% quality is fine.

---

## Memory Search (Gemini Embeddings — recommended)

Memory search (`memory_search`) requires an embedding provider. Gemini is free and easy:

1. Go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey) → Create API Key
2. Add to your `openclaw.json`:

```json5
agents: {
  defaults: {
    memorySearch: {
      provider: "gemini",
      model: "gemini-embedding-001",
      remote: {
        apiKey: "YOUR_GEMINI_API_KEY"
      }
    }
  }
}
```

3. Restart gateway: `openclaw gateway restart`

Free tier: 1,500 requests/day — more than enough for personal use. Enables hybrid search (semantic + keyword), temporal decay (recent memories rank higher), and MMR (deduplicates similar results).

**Alternative:** Set `provider: "openai"` with an OpenAI API key if you prefer.
