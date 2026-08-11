# AEQ 3x3x3 GRID EXPERIMENT -- PRE-REGISTRATION v1.1 (AMENDMENT)

**Amended:** 2026-07-24T00:16:00Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026
**Status:** REGISTERED -- amendment recorded BEFORE the v1.1 run executes.
**Supersedes:** AEQ_Grid_PreRegistration_v1.md for run configuration only. All gates, rubrics, query classes, evidence, the declared prior (75-80%), and the integrity rules of v1.0 carry forward UNCHANGED.

---

## Why this amendment exists

Two v1.0 runs were executed on 2026-07-23. Both were invalidated by the pre-registration's own integrity checks, for infrastructure reasons rather than rubric defects:

1. **Run 1:** every judge call failed with an Anthropic credit-balance error (judge COGS $0.000000). No adjudication occurred. Credits were added afterward.
2. **Run 2:** the judge ran, but the frontier reference self-passed only 7/9 (below the required 8/9), so per v1.0 section 5 the result cannot stand. Diagnosis of the two failed frontier cells (both Q1_retrieval) showed the judge model (claude-haiku-4-5) rejecting a correct answer with an arithmetically false note ("GEN-004 (health 46) does not meet the critical threshold of health < 50" -- 46 is below 50, and the evidence classifies critical as h<50 with 7 of 12 assets unshown). The rubric was judged sound; the judge model erred. Separately, in both runs the T2 (gpt-5-mini) and T3 (gpt-5-nano) tiers consumed the entire 600-token completion budget on internal reasoning and returned zero visible answer text, making their 0% pass rate an artifact of the output cap, not a measurement.

## Changes in v1.1 (approved by the author, 2026-07-23 PT)

| Parameter | v1.0 | v1.1 | Reason |
|---|---|---|---|
| MAX_OUTPUT_TOKENS (SUT completion cap) | 600 | 4000 | gpt-5-mini/nano are reasoning-tier models; the 600-token budget was consumed entirely by reasoning tokens, leaving empty answers |
| JUDGE_MODEL | claude-haiku-4-5-20251001 | claude-opus-4-8 | Haiku judge produced two arithmetically false rejections of correct frontier answers; a stronger judge reduces adjudication error |
| Judge pricing entry | $1.00 / $5.00 per MTok | $5.00 / $25.00 per MTok | Matches claude-opus-4-8 official pricing |

No other edits. The judge request shape is unchanged (max_tokens 300, no sampling parameters), the gates in section 5 remain locked, and the rubrics in section 4 are verbatim from v1.0.

## Cost note

Judge cost rises roughly 5x versus the haiku run (measured haiku judge total: $0.017). Estimated v1.1 judge total: under $0.15. Total run estimate remains under $1.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
