---
name: commercial-policy
description: "Use when designing or revising a company s commercial policy — the rules of engagement governing discounts off list price, approver thresholds, exception flows, and the deal framework that Deal Desk and AEs operate under. Covers discount matrix design (ARR band x term length x payment terms x strategic value), commercial policy design, exception policy, discount governance, approval thresholds, deal framework structure, and policy linting (contradictions, gaps, cliff edges, gaming surfaces). For Head of Commercial, Head of Deal Desk, VP Sales, or RevOps at the policy-design moment — NOT per-deal application (that is deal-desk) and NOT pricing model selection (that is pricing-strategist)."
---

# commercial-policy

## Purpose

Design the **rules of engagement** that govern discounting off list price — the artifact that Deal Desk and AEs operate under. Three deterministic tools:

1. `discount_matrix_builder.py` — builds a 4-dimensional matrix (ARR band × term length × payment terms × strategic value tier), each cell carrying an approved discount band backed by current win-rate + NRR data, plus an approver tier (AE / Manager / Director / VP / CFO).
2. `exception_router.py` — when an asks-for-discount lands outside the matrix, routes it through the named approver chain, attaches required compensating commitments (multi-year prepay + named expansion path + reference commitment + MSA tightening), produces machine-readable audit-trail metadata, and flags precedent risk if 3+ similar exceptions have landed in the trailing quarter.
3. `policy_linter.py` — lints the matrix for governance defects: approver inversion, band inversion, margin-floor violation, coverage gaps, cliff edges, undefined strategic tiers, inconsistent margin floors, thin data backing.

The output is the **policy itself** (matrix + exception flow + lint report), not a per-deal application of it.

## When to use

- A new Head of Commercial or Head of Deal Desk is writing the company's first formal commercial policy
- The existing matrix is older than 6 months and discount drift is showing in margin reviews
- Reps are citing "Maria approved 28% on Acme last quarter" as precedent and you need to break the precedent loop
- Q-over-Q exception count is rising and you suspect the matrix bands are mispriced
- CFO has tightened the margin floor and the matrix needs to be rebuilt against the new constraint
- A board / exec is asking "why do we discount this much?" and you need a data-backed defensible policy

**Do NOT use this skill to:**
- Approve a specific deal — that's `commercial/skills/deal-desk`
- Set the pricing model + list price — that's `commercial/skills/pricing-strategist`
- Author a proposal / SOW / MSA prose — that's `business-growth/contract-and-proposal-writer`
- Make the strategic "when do we hire a VP Sales" call — that's `c-level-advisor/cro-advisor`

## Workflow

1. **Audit current discount distribution.** Pull the last 4 quarters of closed-won + closed-lost deals from CRM. Fill `assets/policy_design_template.md` (~20 minutes). Capture: `arr`, `discount_pct`, `term_months`, `payment_terms_days`, `strategic_value`, `win_lost`, `nrr_12mo` per deal.

2. **Design the data-backed matrix.** Run `scripts/discount_matrix_builder.py --input policy_intake.json --profile {saas|enterprise-software|api|marketplace|services}`. Output is a 4-dimensional matrix with approved discount band + approver tier + margin floor + observed win-rate + observed NRR per cell. Cells with `n  matrix.json

# Lint the matrix
python3 scripts/policy_linter.py --sample
python3 scripts/policy_linter.py --input matrix.json

# Walk the exception flow
python3 scripts/exception_router.py --sample
python3 scripts/exception_router.py --input request.json --output json
```

The sample matrix lints to **FAIL** with 4 BLOCKERs + 6 MAJORs + 2 MINORs — by design, to exercise every rule path. A real policy intake should lint to PASS or PASS_WITH_WARNINGS. The sample exception (42% on a $320K logo deal) routes to AE → Sales Manager → Director → VP Sales with 3 required compensating commitments (multi-year 36mo, prepay, named expansion path).
