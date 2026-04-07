# HEARTBEAT.md

## Mission Filter (every heartbeat)
> **Mission:** [Your mission statement — what are you working toward?]
> Every action should pass: "Does this move [Your name] closer to the goal?"

## Chief of Staff — PROACTIVE NUDGES (every heartbeat)
**Don't just flag. Push.** A real chief of staff doesn't say "task X is overdue." They say "task X is overdue — want me to draft the email / do the research / schedule the call?"

- **Task scanner**: Read `state/tasks.yaml` — any tasks newly overdue? **Send a direct nudge with a proposed action**, not a passive flag buried in a briefing.
- **Open loop check**: Read `state/hot-context.md` Proactive Watch List — anything due in <48 hours? **Nudge with specifics**.
- **Revenue thread staleness**: If a revenue-track thread hasn't had activity in >3 days, **nudge directly** with a proposed action.
- **Meeting auto-prep**: Scan calendar for meetings in next 3 hours with external attendees. If no prep doc exists, **build it now and push it** — don't wait to be asked.
- **Pattern matching**: Cross-reference recent emails/calendar against active threads. If something connects, suggest agent activation.
- **Overnight work review**: If any autonomous cron produced output, mention it briefly.
- **Agent dispatch**: Use the signal→agent table below.

### Signal → Agent Dispatch Table
| Signal Source / Keywords | Agent | Action |
|---|---|---|
| Finance, tax, equity, options, budget, insurance | finance-creator | Spawn for analysis |
| Strategy, deals, proposals, engagements, positioning | work-creator | Spawn for strategy |
| Due diligence, market research, new company | research-creator | Spawn for research |
| Article, LinkedIn post, content idea, draft | content-creator | Spawn for drafting |
| New market question, competitor, industry trend | research-creator | Spawn for research |
| Calendar event with external attendee in <3 hours, no prep doc | work-creator | Auto-prep brief |
| Workout, health, medical, fitness | body-creator | Update body state |
| New skill, infra improvement, security advisory | infra-creator | Evaluate and recommend |
| Connection request, intro, relationship cold >30 days | network-creator | Relationship intelligence |

## Context Keeper — Agent Channel Sweep (3x daily: configure times to your preference)

Agent channel sessions run in isolation. They write back to `state/hot-context.md` via the session-end protocol, but Context Keeper closes the loop by actively sweeping and synthesizing.

**Each sweep:**
1. Read `state/hot-context.md` — note current Active Threads state
2. Scan `memory/YYYY-MM-DD.md` for any agent session summaries added since last sweep
3. Cross-reference: are there agent outputs not yet reflected in hot-context.md Active Threads?
4. If gaps found → update the relevant thread in hot-context.md
5. Update `## Last Updated` timestamp in hot-context.md

## Validator Activation Rules (non-negotiable)

Validators only add value if they actually fire. These are hard triggers — not suggestions.

### Auto-Route to Validator BEFORE delivering to [Your name]:

| Condition | Validator | Why |
|-----------|-----------|-----|
| Any finance-creator output involving large amounts, tax implications, equity, or investment advice | finance-critic | Catches errors before they reach the user |
| Any content-creator output destined for publication | content-critic | Voice drift catches before it ships |
| Any work-creator strategic recommendation (deal evaluation, positioning, proposal) | work-critic | Stress-test the upside before [Your name] acts |
| Any research-creator output used as basis for a major decision | research-critic | Source verification catches phantom citations |
| Any task marked Critical AND multi-step execution | process-validator | Audits HOW, not WHAT — catches process failures |

### When validators are optional (agent's judgment):
- Routine finance summaries with no decision point
- Body routine updates (no strategic stakes)
- Quick research lookups (single factual question)
- Network outreach drafts where [Your name] will review anyway

### If a critic flags grade < B-:
1. Send back to creator with specific feedback (max 2 iterations)
2. If still < B- after 2 rounds → escalate to [Your name] with the grade and the gap
3. Never ship sub-B- output silently

## Infra & Services (rotate, 1-2x daily)
- **Service health:** Check that key services are running (task board, tunnel, etc.)
- **Disk/memory:** Quick check if anything is bloated

## Security
- Covered by regular security review cron — no manual check needed here

## Agent Quality (daily, morning)
- Read `state/evals.yaml` stats section
- Flag if any agent avg_score < 88 or 2+ consecutive sub-A- grades
- Flag if escalation_rate > 20%
- Include in morning briefing summary

## Cost Awareness (weekly)
- Check how many sub-agents were spawned in the past week
- Flag if any cron job is failing repeatedly
- Note if token usage seems disproportionate to value delivered

## Weekly: Platform Update Check
- Check current version of OpenClaw (or equivalent platform)
- If newer version available, notify [Your name] via current channel
- Don't auto-update — just inform

## Task Hygiene (every heartbeat — non-negotiable)

### 1. Process Triggers
- Check `state/triggers/` for any `.json` files
- For each trigger: apply changes to tasks.yaml immediately
- Delete trigger file after processing
- Log to `memory/YYYY-MM-DD.md`

### 2. Staleness Sweep
- Scan all open/in_progress tasks in tasks.yaml
- **Overdue >3 days with no recent notes:** Nudge [Your name] with proposed action
- **Overdue >7 days with no activity:** Escalate — ask if still relevant or should archive
- **Revenue tasks quiet >3 days:** Direct nudge

### 3. Archive Sweep
- Any task with `status: done` or `status: archived` still in main tasks.yaml → move to `state/tasks-archive.yaml`

### 4. Date Hygiene
- Tasks with due_date in the past and status still `open` → either update the date or flag for [Your name]'s call

## Proactive Intelligence (every heartbeat)
- **Meeting auto-prep**: Scan calendar for meetings in next 3 hours with external attendees. If no prep doc exists, build one automatically and push to [Your name].
- **Signal detection**: Scan emails, calendar, tasks for signals that connect to active threads.
- **Suggestion logging**: Log every proactive suggestion to `state/suggestions.yaml` with signal, action, and confidence.
- **Learning extraction**: Check `state/proactive-learnings.yaml` before acting — apply known patterns.

## Email→Task Reconciliation (2-3x daily)

### Email Triage Protocol (MANDATORY — no shortcuts)
1. Fetch recent emails
2. For EACH email before flagging:
   a. **Dedup check:** Was this email already reviewed today?
   b. **Read the body** — NEVER flag based on subject line alone
   c. **Action test:** Does [Your name] need to DO something? (reply, decide, pay, sign, schedule)
      - If NO action needed → do not flag, do not mention
      - If YES → flag with the SPECIFIC action required
3. **WRITE TO TASKS.YAML IN THE SAME TURN** — not later:
   a. Match email against open tasks
   b. If match found → append to that task's `notes:` with date + signal summary
   c. If status changed → update `status:`
   d. If new deadline surfaced → update `due_date:`
   e. If no task match but actionable → create new task
4. Apply routine updates silently
5. Only flag TO [Your name] emails that pass ALL three checks (dedup + body read + action required)

### Traceability Rule
Every email scan must produce either:
- Task updates written to tasks.yaml, OR
- Explicit "no task-relevant emails found" logged to daily notes

**No silent scans.** If you scanned email, there's a paper trail.
