---
name: post-mortem
description: "/cs:post-mortem — Honest retrospective on an executed decision, scored against original assumptions and dissent. Closes the strategic sprint loop. Use when a decision hits its 90-day review checkpoint or its kill criteria trigger — e.g. scoring last quarter s pricing change against its pre-committed success metrics."
---

# /cs:post-mortem — Honest Retrospective

**Command:** `/cs:post-mortem `

Closes the strategic sprint loop. Scores a decision against the success and kill criteria written **before** the decision (not retro-fitted) and revisits the preserved dissent. This is the rigor that compounds over time.

## Pipeline Position

```
/cs:office-hours  →  /cs:brief  →  /cs:boardroom  →  /cs:decide  →  /cs:execute  →  /cs:post-mortem
                                                                                       ↑ you are here
```

## When to Run

- At the 90-day checkpoint (auto-scheduled by `/cs:decide`)
- When a kill criterion triggers
- After a major decision is reversed
- Quarterly on all decisions of the past quarter

## Inputs

- The decision record (output of `/cs:decide`)
- The execution plan (output of `/cs:execute`)
- Actual outcomes (metrics, events, customer signals)

## Output: Post-Mortem Record

Saved to `~/.claude/postmortems/YYYY-MM-DD-.md`:

```markdown
# Post-Mortem: 
**Decision date:** YYYY-MM-DD
**Post-mortem date:** YYYY-MM-DD
**Status:** WIN / PARTIAL / LOSS / MIXED

## Outcome Scoring (against pre-committed criteria)

| Success Criterion | Threshold | Actual | Met? |
|---|---|---|---|
|  |  |  | ✅ / ❌ |
|  |  |  | ✅ / ❌ |

| Kill Criterion | Threshold | Actual | Triggered? |
|---|---|---|---|
|  |  |  | ✅ / ❌ |

**Overall:** WIN / PARTIAL / LOSS / MIXED

## What We Got Right
- 
- 

## What We Got Wrong
- 
- 

## Preserved Dissent — Revisited
[Original dissent from the boardroom memo, scored:]

- **:** 
  - **Did it materialize?** YES / NO / PARTIAL
  - **Cost if YES:** 
  - **Lesson:** 

## Assumption Audit
[Original brief's assumptions, scored:]

- **Assumption 1:** 
  - **Held?** YES / NO / PARTIAL
  - **Why:** 

## Process Lessons
- **Phase 2 isolation worked?** YES / NO
- **Devil's advocate concerns played out?** YES / NO / PARTIAL
- **Cadence was right?** YES / TOO LOOSE / TOO TIGHT

## Forward Actions
- [ ] 
- [ ] 
- [ ] 

## Status
- WIN → archive, log lesson
- LOSS → schedule follow-up boardroom: `/cs:brief` for the next call
```

## Why Pre-Committed Criteria Matter

The biggest temptation in post-mortems is retroactive justification: "we always knew X, that's why we did Y." Pre-committed criteria, signed at `/cs:decide` time, eliminate that move. The numbers either matched or they didn't.

## Why Revisit Dissent

The dissent column from `/cs:boardroom` is the single most useful piece of organizational memory. Most of the time, the dissenter was directionally right. Revisiting and scoring it builds calibration over years.

## Routing

- `/cs:brief` — if the post-mortem surfaces a new decision
- `/cs:freeze` — if the post-mortem reveals a process gap that needs cooldown enforcement
- Updates to company-context.md via `cs-onboard`

## Related

- Skill: [`decision-logger`](../../../skills/decision-logger/SKILL.md)
- Agent: [`cs-chief-of-staff`](../../agents/cs-chief-of-staff.md)
- Sibling: [`/em:postmortem`](../../../executive-mentor/skills/postmortem/SKILL.md) — adversarial single-decision post-mortem

---

**Version:** 1.0.0
