---
name: collab-proof
description: "Use when you want to understand what Claude contributed vs what you drove in a session. Triggers on: /collab-proof, session retrospective, ai contribution analysis, collaboration evidence, what did claude do."
---

# collab-proof

Surfaces AI collaboration evidence the developer didn't consciously record.
Vela 3-layer pipeline × ADHD 4-frame reasoning — prompt-native, zero dependencies.

---

## Layer 01 — Signal detection

Run `git log --oneline -10` and `git diff --stat HEAD~3..HEAD` first.

Classify signal level using this rubric (pick the highest that matches):

**HIGH** → full artifacts (DECISIONS.md + session-history + WORKLOG + HTML)
- New file created, OR
- 4+ files modified, OR
- Explicit option comparison in conversation ("vs", "instead of", "chose X over Y"), OR
- Design discussion lasted 15+ exchanges, OR
- **Bug with root cause diagnosis** — conversation contains WHY the bug happened
  (not just "fixed X" but "the bug was caused by Y because Z")

**BUG_FIXING special rule** — override file count:
Even if only 1 file changed, classify as HIGH if the conversation contains:
- Root cause explanation ("the bug was...", "this happened because...", "the issue is...")
- Diagnosis process ("I checked...", "turned out...", "the problem was...")
- Fix rationale ("chose this approach because...", "instead of X, used Y because...")
File count doesn't matter for bugs — a well-diagnosed single-file fix is more valuable
than a 10-file feature with no discussion.

**MEDIUM** → WORKLOG only
- 1–3 files modified with no root cause discussion, OR
- Minor feature added, no tradeoffs discussed

**LOW** → silence, tell user "Routine session — nothing recorded."
- No code changes, only planning/discussion, OR
- Single trivial change with no context ("change this text", "fix typo", "rename variable")

Show the user: `Signal: HIGH / MEDIUM / LOW — [one-line reason]`

---

## Layer 02 — WorkIntentClassifier

Run all four frames simultaneously against conversation context + git diff.
Score each frame 0.0–1.0 using the rubric below. Then apply pruning and classification rules.

### Frame scoring rubric

**Frame A — Technical** (code churn complexity)
- `1.0` New module/file created, complex logic added (state machine, Lua script, novel algorithm)
- `0.5` Existing function logic modified, simple API endpoint added
- `0.1` Typo fix, comment change, plain text edit

**Frame B — Uncertainty** (developer doubt signals)
- `1.0` Code written then fully rolled back, explicit doubt expressed ("이게 맞나?", "동작 안 하네"), `git revert`
- `0.5` Advice sought from Claude mid-implementation, 2+ revision requests on same area
- `0.0` Uninterrupted directive execution — developer knew exactly what to build

**Frame C — Fork** (decision branch presence)
- `1.0` Two or more alternatives explicitly compared in conversation (A vs B)
- `0.5` No explicit comparison but tradeoff mentioned (performance vs readability)
- `0.0` Single standard approach applied, no alternatives considered

**Frame D — AI contribution** (Claude's actual impact)
- `1.0` Claude identified a bug/edge case the developer hadn't noticed and proposed the fix
- `0.6` Claude generated structural boilerplate/skeleton that significantly accelerated execution
- `0.2` Claude reformatted or transcribed developer-directed code without independent contribution

---

### Pruning rule

Prune any frame scoring = 0.8` AND `Frame D = 0.6`, do NOT prune and do NOT silence the session,
even if Frame B = 0.0 and Frame C = 0.0.
This is a boilerplate-heavy FEATURE_BUILDING session. Classify immediately as `FEATURE_BUILDING` with `HIGH` signal.
Rationale: zero uncertainty in a fast-moving session is a feature, not a reason to discard it.

---

### Intent classification

| Surviving frames | Dominant intent | Meaning |
|---|---|---|
| A high + D mid-high (B, C low) | `FEATURE_BUILDING` | High-velocity feature generation, Claude scaffolding |
| B high + A/D high | `BUG_FIXING` or `STUCK` | Active debugging or unresolved looping |
| C high + A high | `REFACTORING` or `EXPLORING` | Architecture exploration, weighing alternatives |
| All frames  session-history/YYYY-MM-DD-HHMM-proof.html  'HTMLEOF'

... (full HTML with inline CSS, no external resources)
HTMLEOF
```

After writing, show: `open session-history/YYYY-MM-DD-HHMM-proof.html`

---

### If MEDIUM signal

Append one line to `WORKLOG.md` only:
```
YYYY-MM-DD HH:MM | [intent] | MEDIUM | D:[score] | cache:[hit%]% | tok:[total] | 
```

---

### If LOW signal

Tell user: "Signal: LOW — Routine session, nothing recorded."

---

## Honesty rules

- Never invent decisions not in the conversation or implied by the diff
- "inferred:" prefix when reasoning is reconstructed
- Frame D must be calibrated — neither overclaim nor dismiss
- If all frames score  0.4 → write nothing

---

## PreCompact snapshot (context compaction defence)

When context compaction is about to happen (triggered by the PreCompact hook),
run a lightweight mid-session checkpoint before context is lost:

1. Compute current Layer 01 signal level from available context
2. Score all four frames against what's visible now
3. Write a snapshot to `session-history/.tmp-TIMESTAMP.json`:

```json
{
  "timestamp": "YYYY-MM-DD HH:MM:SS",
  "trigger": "pre-compact",
  "signal": "HIGH / MEDIUM / LOW",
  "frames": { "technical": 0.0, "uncertainty": 0.0, "fork": 0.0, "ai_contribution": 0.0 },
  "intent": "FEATURE_BUILDING",
  "key_moments": [
    "one-line description of the most important decision or finding so far"
  ]
}
```

When `/collab-proof` runs at session end:
- Read all `session-history/.tmp-*.json` files
- Merge frame scores (take max per frame across all snapshots)
- Combine `key_moments` arrays — these preserve tradeoff discussions that were compacted away
- Delete `.tmp-*.json` files after merging
