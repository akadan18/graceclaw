# Cross-Repo Learning Sync — GraceClaw ↔ GraceWork CPD

## The Problem

Learnings in GraceWork CPD (product development) don't reach GraceClaw (personal OS), and vice versa. When you learn a pattern building a product, that pattern might apply to how you manage your personal tasks. And when Grace learns something about your communication style, that should inform how CPD agents draft things on your behalf.

## Sync Architecture

```
┌──────────────┐                    ┌──────────────┐
│  GraceClaw   │                    │ GraceWork CPD│
│              │                    │              │
│ project-     │ ──── sync ──────▶  │ project-     │
│ memory.yaml  │ ◀──── sync ─────  │ memory.yaml  │
│              │                    │              │
│ brain/       │ ──── export ────▶  │ knowledge/   │
│              │                    │              │
└──────────────┘                    └──────────────┘
```

## What Syncs

### GraceClaw → CPD (personal insights that help product work)
- **Communication patterns** — how Artem writes, what tone works, his voice DNA
- **Decision-making patterns** — how he evaluates options, risk tolerance, speed preferences
- **Work habits** — when he's most productive, how he handles context switches
- **Anti-patterns** — mistakes that repeat across domains

### CPD → GraceClaw (product patterns that help personal ops)
- **Quality process learnings** — what makes good output (grading insights, iteration patterns)
- **Research methodology** — what search strategies work, source reliability
- **Automation patterns** — what to cron, what needs human touch
- **Agent coordination patterns** — how multi-agent handoffs work best

### What Doesn't Sync
- Project-specific facts (competitor data, user research) — stay in CPD
- Personal information (health, relationships, finance) — stay in GraceClaw
- Credentials, API keys — never sync anywhere

## Sync Format

Learnings that cross repos use a shared tag:

```yaml
# In project-memory.yaml
- id: learn-042
  text: "When drafting external emails, Artem prefers to lead with the ask, not context. Recipients skim — put the action item first."
  confidence: high
  tags: [communication, cross-repo]
  source: "GraceClaw: email scan pattern, observed 5+ times"
  synced_to: ["gracework-cpd"]
  synced_at: "2026-03-30"
```

## Sync Methods

### Option A: Manual Monthly (recommended to start)
During monthly memory consolidation:
1. Filter learnings tagged `cross-repo` or high-confidence behavioral patterns
2. Review for relevance to the other repo
3. Copy applicable learnings with source attribution
4. Tag as `synced_to: [repo-name]` to prevent re-syncing

### Option B: Shared Learnings File (for scaling)
A single shared file that both repos read:

```
~/.openclaw/workspace/shared-context/cross-repo-learnings.yaml
```

Both systems append to it. Both systems read it on wake. Deduplication happens during monthly consolidation.

### Option C: Git Submodule (for automation)
A shared git repo mounted as a submodule in both projects. Automated sync via git.

**Start with Option A.** Move to B when volume justifies it. Move to C only if you have 3+ repos sharing learnings.

## Implementation in GraceClaw

Add to the monthly consolidation cron:

```
After consolidating project-memory.yaml:
1. Filter learnings with confidence=high and tags containing 'behavioral' or 'process'
2. Check each against GraceWork CPD's project-memory — already there?
3. For new ones: append with source="GraceClaw" and date
4. Update synced_to tag in source
```

## Implementation in GraceWork CPD

Add to the weekly reflection:

```
After reflection:
1. Filter new learnings that are transferable beyond this project
2. Tag with cross-repo if applicable
3. During monthly consolidation: review cross-repo tagged items for GraceClaw sync
```
