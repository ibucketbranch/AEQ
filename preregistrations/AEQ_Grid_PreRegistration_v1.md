# AEQ 3×3×3 GRID EXPERIMENT, PRE-REGISTRATION v1.0

**Pre-registered:** 2026-07-22T08:49:29Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D © 2026
**Status:** REGISTERED, NOT YET RUN. This document is written and timestamped BEFORE the experiment executes. Gates below may not be modified after the run begins.

---

## 1. The Question

Does a cheaper model tier deliver a rubric-equivalent answer when given the same query and the same evidence as a frontier tier, and at what pass rate, per query class?

This is the load-bearing assumption of the AEQ Verify concept. The published routing literature suggests high pass rates on benchmark traffic (RouteLLM: 95% of GPT-4 quality with 14–26% strong-model calls, ICLR 2025; FrugalGPT: up to 98% cost reduction at matched performance, Chen et al. 2023, arXiv:2305.05176). None of that literature uses pre-registered equivalence rubrics or cross-family adjudication on enterprise-agent-style queries. This experiment does.

## 2. Stated Prior (declared before run)

**Founder prior: 75–80% aggregate rubric pass rate** for the mid tier, lower for nano. Declared here so the result can be scored against the prediction, not fitted to it.

## 3. Design, 3 × 3 × 3

| Dimension | Levels |
|---|---|
| **Query class** | Q1 Simple retrieval · Q2 Analytical multi-signal · Q3 Judgment/synthesis |
| **Model tier** | T1 Frontier (reference) · T2 Mid · T3 Nano, pinned versions recorded at run time |
| **Runs per cell** | N = 3 (temperature 0; latency and minor variance still averaged) |

**Replay semantics (deliberate design choice):** All tiers receive identical evidence, the same deterministic tool outputs injected as context. This isolates the tier-equivalence variable and mirrors the AEQ Verify shadow-lane mechanism (replay same query + same retrieved data on a cheaper configuration).

**Declared limitation:** This design does NOT test tool-selection ability across tiers. Whether a nano-tier model *chooses* the right tools is a separate experiment (Grid-2, future). Do not generalize Grid-1 results to full autonomous orchestration.

**Adjudication:** Cross-family validator (Anthropic Claude judging OpenAI system-under-test outputs). No self-grading, the same independence rule AEQ v1.0 imposes on customers is imposed here. Judge renders a structured verdict against the rubric plus the frontier reference answer. Judge model version pinned at run time.

**Judge cost is recorded separately** as "verification overhead per verified query", this is the COGS of certification and a product-relevant number in its own right.

## 4. Equivalence Rubrics (pre-registered per query class)

**Q1, Simple retrieval.** "What are the critical assets in the portfolio?"
PASS requires: (a) states the critical asset count = 12; (b) cites at least 3 of the 5 named critical asset IDs present in the evidence (PUMP-003, HVAC-007, COMP-002, BOIL-001, PUMP-009); (c) contains no asset IDs or counts that contradict the evidence.

**Q2, Analytical multi-signal.** "Which assets should be prioritized for maintenance in the next 30 days, and why?"
PASS requires: (a) top priority is PUMP-003 (highest risk score 91.2 in evidence); (b) at least 2 of the remaining top-5 risk assets named (HVAC-007, BOIL-001, COMP-002, GEN-004); (c) justification references at least one quantitative signal from the evidence (risk score, health score, or overdue days); (d) no fabricated numbers.

**Q3, Judgment/synthesis.** "Draft a one-paragraph recommendation for leadership on the state of the asset portfolio and the single most important action to take."
PASS requires: (a) portfolio characterized as declining or at-risk (consistent with 24% critical, −3.2 pt 90-day trend in evidence); (b) recommended action addresses the highest-risk asset(s) or the overdue-maintenance backlog; (c) no fabricated statistics; (d) length ≤ 250 words (leadership-appropriate).

A response FAILS if any required element is absent or contradicted. The judge must return structured JSON: `{pass, failed_criteria, notes}`.

## 5. Go / No-Go Gates (LOCKED)

| Gate | Condition | Consequence for AEQ Verify |
|---|---|---|
| **GREEN** | Aggregate pass rate (T2+T3 vs rubric) ≥ 70% AND effective cost delta ≥ 5x AND Q3 (hardest class) pass ≥ 50% | Full pitch stands. "Certified verified savings" story proceeds to design-partner outreach. |
| **YELLOW** | Aggregate 40–70%, or GREEN numbers but Q3 < 50% | Company exists but repositions: "auditable routing with a billing-grade ledger," differentiation shifts to certification, not savings magnitude. |
| **RED** | Aggregate < 40%, OR passes concentrated only in Q1 | Savings pool does not support gainshare at target ICP. Pivot AEQ IP toward consulting / benchmark tooling. |

Secondary integrity checks (reported, not gated): frontier reference must itself pass its own rubric ≥ 8/9 runs (else rubric is defective, fix rubric, re-register as v1.1, re-run); any judge JSON parse failure is logged and re-adjudicated once, never silently dropped.

## 6. Measurement & Integrity Rules (inherited from AEQ Spec v1.0 §6)

1. Pin everything: model versions, temperature 0, pricing at run date (verify at platform.openai.com and anthropic.com pricing pages before publication, defaults in the script are placeholders from third-party sources and MUST be re-verified).
2. Input tokens measured exactly (tiktoken); output tokens from API usage fields. All numbers in publication labeled measured vs. estimated.
3. N=3 per cell; failed runs logged, not dropped.
4. Full answer text captured for every cell for qualitative audit.
5. Results published regardless of outcome. A RED result is publishable, "we pre-registered, we ran it, here is what the rubric actually says" is itself a credibility asset.

## 7. Run Instructions

```
# In the AgentSaaSy_EAM repo (or standalone dir), with .env containing:
#   OPENAI_API_KEY=...
#   ANTHROPIC_API_KEY=...
pip install tiktoken requests python-dotenv
python aeq_grid_experiment.py                # full grid
python aeq_grid_experiment.py --dry-run      # token/cost estimate only, no API calls
```

Estimated total API cost: **under $5** (27 execution calls on small prompts + ≤ 60 judge calls). Estimated wall time: 10–20 minutes.

## 8. What Gets Reported

Per-cell: pass/fail, tokens, cost, latency, full answer. Aggregate: pass-rate matrix (class × tier), cost-delta matrix, gate verdict (GREEN/YELLOW/RED) computed automatically against §5, verification overhead per query, and a comparison of the measured pass rate against the §2 declared prior.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*

