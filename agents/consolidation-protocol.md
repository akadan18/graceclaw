# Consolidation Protocol

Run this monthly (or when project-memory.yaml has 20+ entries).
Keeps memory lean, accurate, and useful. Takes 15–30 minutes.

---

## Step 1: Read Everything

Read all of:
- `state/project-memory.yaml`
- `memory/notes.md`
- `memory/lessons.md`
- `memory/decisions.md`

---

## Step 2: Promote from Notes

Scan memory/notes.md for patterns that now meet the quality standard (4-test filter in project-memory.yaml). Promote them as new learnings.

---

## Step 3: Reinforce or Merge

For existing learnings in project-memory.yaml:
- If two learnings say the same thing differently → merge into one, keep the better wording
- If a learning was reinforced during the month → increment `times_reinforced`, update `last_verified`

---

## Step 4: Prune + Staleness Check

**Prune candidates** (do NOT auto-delete — flag for user to confirm):
- `confidence: hypothesis` + `times_reinforced: 0` + age > 60 days
- Reads like a fact or observation, not a behavioral pattern
- Superseded by a newer, better entry on the same topic

**Staleness flags** (re-verify, not delete):
- `last_verified` > 90 days ago + `times_reinforced < 2` → re-check if still accurate
- No `source_ref` field + age > 60 days → note as unverifiable

List all flagged entries in a consolidation report. Ask user to confirm deletions.

---

## Step 5: Produce Report

Post a short summary:
```
Consolidation complete — [date]
- Added: N new learnings from notes
- Merged: N duplicates
- Pruned: N stale entries (awaiting confirmation)
- Flagged for re-verification: N entries
- Total learnings: N
```
