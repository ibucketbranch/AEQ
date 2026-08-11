# AEQ DUAL-PROVIDER ARCHITECTURE EXPERIMENT -- PRE-REGISTRATION v1.0

**Pre-registered:** 2026-07-24T01:21:27Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026
**Status:** REGISTERED -- NOT YET RUN. Written and timestamped before execution. The prediction and analysis rules below may not be modified after the run begins.

---

## 1. The Question

Is the architecture-efficiency spread measured in the March 2026 AEQ experiment (optimized vs tutorial vs enterprise system prompts) a property of the architecture, or a quirk of one vendor's model? The March run measured prompt overhead of 2.0% / 4.7% / 9.2% and rising total tokens across the three architectures on gpt-4o-mini only. If the same ordering holds on a second vendor, the waste is architectural.

## 2. Declared Prediction (before run)

On BOTH providers, for the fixed query, total tokens and cost per query rank:

optimized < tutorial < enterprise

Secondary predictions: (a) tool selection is identical across architectures on both providers (1 call to query_assets, matching the March finding); (b) prompt overhead ratio preserves the same ordering on both providers; (c) all runs on all architectures deliver the equivalent business answer (12 critical assets) per the validation rubric in experiments/STUDY-DESIGN.md.

The prediction FAILS if either provider inverts any adjacent pair of the primary ordering on averaged totals.

## 3. Design

| Dimension | Levels |
|---|---|
| Provider | OpenAI (gpt-4o-mini, alias resolved at run time; pricing $0.15/$0.60 per MTok) . Anthropic (claude-haiku-4-5; pricing $1.00/$5.00 per MTok, verified against official page 2026-07-23) |
| Architecture | optimized . tutorial-style . enterprise-style (system prompts verbatim from the existing rig, unchanged from the March design) |
| Runs | N = 5 per architecture per provider, temperature 0, averaged |

Rig: `whitepaper/aeq_experiment_dual.py`, run in `--mode validate --providers openai anthropic --runs 5`, unmodified except where a pre-flight failure requires a model-id correction (which would be recorded here as an amendment before proceeding). Token and cost figures come from API usage fields, labeled measured; any tiktoken-derived figure is labeled estimated.

## 4. Why the pairing is deliberate

Both models are the vendor's budget tier, so the comparison isolates architecture rather than capability class. The OpenAI arm reuses the March model, making it a replication of the original single-provider result at N=5.

## 5. Analysis and Reporting Rules

1. Report per provider x architecture: mean total tokens, mean cost, tool calls, latency, prompt overhead ratio, answer excerpt.
2. The prediction is scored pass/fail against section 2 exactly as written. A partial hold (ordering holds on one provider only) is reported as a FAIL of the vendor-independence claim, not softened.
3. Failed or errored runs are logged, not dropped (integrity rules inherited from AEQ Spec v1.0 section 6 and the grid RUN_LOG practice).
4. Absolute costs are NOT compared across providers as a finding (the tiers have different sticker prices); only the within-provider ordering and ratios carry the claim.
5. Results are published regardless of outcome.

## 6. Estimated Cost and Time

30 total agent invocations (2 providers x 3 architectures x 5 runs) on budget-tier models with ~2.5K-token prompts: well under $1. Wall time under 15 minutes.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
