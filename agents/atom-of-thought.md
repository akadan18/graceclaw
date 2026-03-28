# Atom of Thought Protocol (AoT)

A structured reasoning methodology for complex analysis where being wrong has real consequences.

Pairs with the Deep Research Protocol:
- **Deep Research** controls the *questioning strategy* — what to ask and in what sequence
- **Atom of Thought** controls the *reasoning rigor* — how each claim is validated independently

---

## When to Use

**Use AoT for:**
- Financial analysis above meaningful thresholds
- Career or business decisions
- Multi-thread strategic connections ("X connects to Y which means Z")
- Opportunity evaluations
- Any advice where an incorrect answer causes real harm

**Skip AoT for:**
- Simple lookups or status reports
- Routine task updates
- Casual conversation
- Single-fact questions

---

## The 5 Steps

### 1. DECOMPOSE
Break the problem into independent logical atoms. Each atom should be verifiable on its own.

If atoms have dependencies, identify them explicitly. Solve leaf atoms (no dependencies) first, then use their validated results to solve parent atoms.

❌ "The market is growing and they have product-market fit, so this is a good investment"
✅ Three atoms:
- Atom A: Is the market growing? (verify independently)
- Atom B: Do they have PMF? (verify independently)
- Atom C: Does A+B → good investment? (synthesize only after A and B are validated)

---

### 2. VALIDATE
Check each atom independently against real sources — files, email, documents, external data.

**Rule:** Don't let one atom's confidence bleed into another. If Atom A is weak, Atom B doesn't inherit its strength just because they feel related.

For each atom, answer:
- What evidence supports this?
- What evidence contradicts this?
- How confident am I on a 1-5 scale?

---

### 3. FLAG
Label each atom explicitly:

| Label | Meaning |
|-------|---------|
| `[verified]` | Confirmed against a specific source — cite it |
| `[inference]` | Logical conclusion from verified atoms |
| `[assumption]` | Unverified — working hypothesis |
| `[unknown]` | Couldn't verify — flag as a gap |

If connecting two threads: verify the connection has strategic substance, not just surface similarity. "Both involve AI" is surface similarity. "Both require the same enterprise sales motion" is strategic substance.

---

### 4. SYNTHESIZE
Build the answer from validated atoms only.

- Verified atoms → state as fact with citation
- Inference atoms → state as inference ("this suggests…")
- Assumption atoms → state as assumption ("assuming X…")
- Unknown atoms → state as gap ("we don't know whether…")

Do not bury uncertain atoms in a confident-sounding synthesis.

---

### 5. DISCLOSE
Tell the user explicitly which parts are solid vs uncertain.

**Format:**
```
SOLID: [list of verified atoms you're confident in]
UNCERTAIN: [list of assumptions/unknowns that affect the conclusion]
RECOMMENDATION: [conclusion, with confidence level]
GAPS: [what you'd want to verify before higher confidence]
```

---

## Example

**Question:** "Should I take this advisory engagement?"

**Atoms:**
- A: What's the time commitment? `[verified]` — 2 calls/month per email on file
- B: What's the comp? `[verified]` — $2K/month + 0.1% equity from term sheet
- C: Is the company fundable? `[inference]` — Series A metrics look strong but no confirmation
- D: Does this conflict with current work? `[assumption]` — Assumed no conflict, not checked
- E: Will this generate leads? `[unknown]` — No evidence either way

**Disclosure:**
```
SOLID: Time commitment and comp terms confirmed from documents
UNCERTAIN: Conflict check not done (Atom D). Lead gen is speculation (Atom E).
RECOMMENDATION: Terms are reasonable. Sign if conflict check passes. Medium confidence.
GAPS: Check employment contract for advisory restrictions. Ask founder about typical deal size.
```

---

## Integration with Validators

When work produced using AoT goes to a critic, the critic should:
1. Check that the DECOMPOSE step actually produced independent atoms (not one argument dressed as many)
2. Verify that labeled sources exist and support the claims
3. Flag any inference atom that's doing too much work in the synthesis

An AoT disclosure section with no unknowns is a red flag — most complex analyses have gaps.
