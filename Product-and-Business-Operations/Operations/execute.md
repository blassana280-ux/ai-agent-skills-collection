---
name: execute
description: "/cs:execute — Generate a 90-day execution plan with weekly milestones, DRIs, and check-in cadence from an approved decision. Use when a logged decision needs to become an operating plan — e.g. turning an approved market-entry call into weekly milestones with DRIs."
---

# /cs:execute — 90-Day Execution Plan

**Command:** `/cs:execute `

Turns an approved decision into a 90-day plan with weekly milestones, named DRIs, and a check-in cadence. Where most decisions die: between "we decided" and "what's next Monday?"

## Pipeline Position

```
/cs:office-hours  →  /cs:brief  →  /cs:boardroom  →  /cs:decide  →  /cs:execute  →  /cs:post-mortem
                                                                       ↑ you are here
```

## Input

An approved decision record (output of `/cs:decide`).

## Output Plan Format

Saved to `~/.claude/execution/YYYY-MM-DD-.md`:

```markdown
# Execution Plan: 
**Decision:** 
**Owner (Sponsor):** 
**Start:** YYYY-MM-DD
**Checkpoint:** YYYY-MM-DD (90d)

## Outcome (binding)
[Copied from decision: success + kill criteria]

## Workstreams
| Workstream | DRI | Success Metric | Status |
|---|---|---|---|
|  |  |  | Not started |
|  |  |  | Not started |
|  |  |  | Not started |

## Weekly Milestones
| Week | Milestone | DRI | Definition of Done |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 | ... | | |
| 12 |  |  |  |

## Cadence
- **Weekly:** Owner reviews status (15 min)
- **Bi-weekly:** Cross-functional sync (30 min)
- **Day 30 / 60 / 90:** Checkpoint with cs-chief-of-staff

## Dependencies
- Internal: 
- External: 

## Risk Register
| Risk | Likelihood | Impact | Owner | Mitigation |
|---|---|---|---|---|
|  | M | H |  |  |

## Kill Criteria Watch
[Copied from decision; reviewed at every checkpoint]
- 
```

## Workflow

1. Read the decision record
2. Decompose the chosen option into 3-6 workstreams
3. Name a DRI for each workstream
4. Reverse-engineer 12 weekly milestones from the checkpoint date
5. Set the cadence (weekly + bi-weekly + 30/60/90 checkpoints)
6. Build the risk register (cross-reference original Phase 4 devil's-advocate concerns)
7. Save and notify DRIs

## Why 90 Days

- Long enough to show real signal (not just activity)
- Short enough to course-correct before damage compounds
- Matches quarterly OKR cycle, fundraise sprints, and most board cadences

## Routing

- `/cs:post-mortem ` — at day 90 (or earlier if kill criteria trigger)
- `/cs:boardroom` — if a checkpoint reveals a need to re-decide

## Related

- Skills: [`coo-advisor`](../../../skills/coo-advisor/SKILL.md), [`strategic-alignment`](../../../skills/strategic-alignment/SKILL.md), [`change-management`](../../../skills/change-management/SKILL.md)
- Agent: [`cs-coo-advisor`](../../agents/cs-coo-advisor.md)

---

**Version:** 1.0.0
