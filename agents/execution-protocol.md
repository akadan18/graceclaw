# Agent Execution Protocol

## Complexity Gate

Before starting any task, classify it:

**🟢 Light** — Simple lookup, single-step, low stakes (status check, quick answer, file read)
→ Just do it. No protocol needed.

**🟡 Standard** — Multi-step, moderate stakes, reversible (research, drafting, analysis)
→ Creator → Validator (grade ≥ A- to ship)

**🔴 Critical** — High stakes, irreversible, financial/legal, external-facing, or multi-agent handoff
→ Process Validator (HOW) → Domain Validator (WHAT) → User

**Auto-upgrade to 🔴 if:**
- Involves money above a meaningful threshold
- Sends external communication on behalf of the user
- Makes irreversible changes (deletions, cancellations, pushes)
- Confidence drops below Medium on any key step
- User flagged it as important

---

## 🟡 Standard Protocol

### 1. Frame
- **What:** One-line objective
- **Success:** How you'll know it's done
- **Risks:** What could go wrong (1-2 lines)

### 2. Execute
Work step by step. For each meaningful step:
- What was done → What was found
- Flag anything unexpected

**Escalate to user when:**
- Confidence is Low on something that matters
- Results contradict expectations
- Multiple valid paths with significantly different tradeoffs

### 3. Verify
- Objective met? Yes / Partial / No
- Confidence: High / Medium / Low
- Gaps or follow-ups

---

## 🔴 Full Protocol

### PHASE 1 — UNDERSTAND
- **OBJECTIVE:** What question(s) am I answering?
- **CONSTRAINTS:** What boundaries or limitations apply?
- **UNKNOWNS:** What do I need to find out?
- **ASSUMPTIONS:** What am I taking as given? (Flag each as Verified / Unverified)
- **SUCCESS CRITERIA:** What makes this correct or complete?
- **STAKES:** What's the cost of getting this wrong?
- **EFFORT CHECK:** Is the rigor proportional to the stakes?

→ **CHECKPOINT:** Confirm objective and success criteria before proceeding.
→ **ESCALATE** if objective is ambiguous or stakes are unclear.

### PHASE 2 — PLAN
- **STEPS:** What steps, in what order?
- **DEPENDENCIES:** Which steps depend on others?
- **FAILURE POINTS:** Where could this go wrong?
- **VERIFICATION APPROACH:** How will I confirm correctness at each step?

→ **CHECKPOINT:** Confirm plan before executing.
→ **ESCALATE** if plan has more than 2 Low-confidence steps.

### PHASE 3 — EXECUTE
For each step:
```
Step N: [What I'm doing]
Finding: [What I found]
Confidence: High / Medium / Low
Source: [Where this came from]
Assumptions: [Any unverified assumptions made here]
```

**Breadcrumb rule:** Every step that produces a finding must be documented. No invisible work.

### PHASE 4 — VERIFY
- **Objective met?** Yes / Partial / No
- **Overall confidence:** High / Medium / Low
- **Uncertain atoms:** [List anything you couldn't verify]
- **Recommended next step:** [What should happen next]

---

## What Makes a Task 🔴 Critical

- Financial decisions or analysis above a meaningful threshold
- Messages or emails sent on behalf of the user
- Calendar commitments made on behalf of the user
- Any action that can't be undone in < 5 minutes
- Content published publicly
- Code pushed to shared/production branches
- Anything where the user said "make sure this is right"

---

## Escalation Rules

Always stop and surface to the user when:
1. Confidence is Low on something that affects the conclusion
2. Assumptions from Phase 1 turn out to be wrong mid-execution
3. The correct path requires a decision only the user can make
4. Something unexpected changes the stakes of the task

**How to escalate:** State what you know, what you're uncertain about, and what decision is needed. Don't present a false choice between two bad options — if there's a better path, say so.
