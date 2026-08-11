# AEQ GRID-2Q EXPERIMENT -- PRE-REGISTRATION v1.3 (AMENDMENT)

**Amended:** 2026-07-24T19:47:12Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026
**Status:** REGISTERED -- recorded BEFORE the model-refresh runs execute.
**Supersedes:** v1.1 for the achievability accounting and reporting details only. The rubrics (v1.1), the discrimination gate, the Phase 1 gates (v1.0 section 7), and all measurement rules otherwise carry forward UNCHANGED.

---

## 1. The CHIL-005 trap: reviewed and AFFIRMED unchanged

Across four runs, the Q4 boundary trap (an urgent-sounding field note on an asset at health 52, two points above the explicit critical threshold) has caught every tier tested, including the frontier reference in 4 of 8 counted runs. The author reviewed the ambiguity question and affirms the trap verbatim: the classification rule is stated plainly in the evidence (health < 50, active status), and a model that lets narrative urgency override a stated numeric policy is committing a materially costly production error, not exposing a rubric defect. Frontier fragility on this trap is a finding, and is reported as one.

## 2. Achievability accounting changed: Q4 excluded from the integrity floor

The v1.0/v1.1 achievability check (frontier passes >= 13 of 15 cells) conflated two distinct signals once Q4 became hard enough to catch the reference model: rubric achievability and genuine frontier weakness. As of v1.3, the achievability floor is computed on the NON-TRAP classes only: **frontier must pass >= 11 of 12 cells across Q1, Q2, Q3, and Q5.** Frontier performance on Q4 is reported separately as a finding and no longer gates anything. The discrimination gate (nano fails >= 2 of 15, post fail-confirmation) is unchanged and continues to count all 15 cells.

## 3. Model refresh: the deprecated SUTs are replaced

Verified against official pages on 2026-07-24: gpt-5.2 is deprecated with a shutdown date of 2026-08-10; gpt-5-mini and gpt-5-nano shut down 2026-12-11; none of the three retain publicly listed pricing. Results published on those models would be unreproducible within weeks. The refresh runs therefore pin:

| Role | v1.1 runs | v1.3 refresh | Verified price (per MTok in/out, official page 2026-07-24) |
|---|---|---|---|
| T1 frontier reference | gpt-5.2 | **gpt-5.6-sol** | $5.00 / $30.00 |
| T3 nano (discrimination probe) | gpt-5-nano | **gpt-5.6-luna** | $1.00 / $6.00 |
| Anthropic SUT (exploratory) | claude-haiku-4-5-20251001 | unchanged | $1.00 / $5.00 (Anthropic docs) |
| Judge (OpenAI + local cells) | claude-opus-4-8 | unchanged | $5.00 / $25.00 (Anthropic docs) |
| Judge (Anthropic cells) | gpt-5.2 | **gpt-5.6-sol** | as above |
| Local SUTs (exploratory) | qwen2.5:7b Q4, llama3.2:3b Q4 | unchanged | $0 (local) |

All prices for models used in the refresh runs are verified; the harness now records verification per model rather than as a single global flag. Note declared before running: the verified cheap-tier price ($1.00/$6.00 for gpt-5.6-luna) is far above the unverifiable placeholder rates of the deprecated nano, so measured cost deltas will compress relative to earlier runs. That is a market fact worth reporting, not an artifact.

## 4. What the refresh consists of

One combined run on the hardened v1.1 rubric: frontier + nano (calibration gate, under the section 2 accounting) + the two local models + the Anthropic SUT (exploratory, cross-family judged in both directions). This refreshes both the calibration evidence and the five-model comparison on reproducible, priceable models. The Phase 1 quantization result (llama3.2:3b fp16 vs Q4) is NOT re-run: its models are pinned local weights that do not deprecate.

## 5. Prior for the refresh (declared before running)

Frontier (gpt-5.6-sol) passes >= 11/12 non-trap cells; nano (gpt-5.6-luna) fails 2-6 of 15 with at least one substantive (non-artifact) failure; per-class pass patterns for the locals and haiku are consistent with the 2026-07-24 five-model run (deterministic failures should reproduce); frontier Q4 performance remains imperfect (the trap keeps catching it).

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
