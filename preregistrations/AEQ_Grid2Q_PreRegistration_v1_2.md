# AEQ GRID-2Q EXPERIMENT -- PRE-REGISTRATION v1.2 (PHASE 1 PINNING AMENDMENT)

**Amended:** 2026-07-24T05:41:57Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026
**Status:** REGISTERED -- recorded BEFORE any Phase 1 cell executes.
**Supersedes:** nothing structural. This amendment pins the Phase 1 system under test, hardware, and adapted prior, as v1.0 section 4 requires. Rubrics (v1.1), gates (v1.0 section 7), and all measurement rules carry forward UNCHANGED.

---

## Phase 1 instance pinned

| Parameter | Value |
|---|---|
| SUT family | Llama 3.2 3B Instruct (open weights, Meta) |
| T2 (full-precision parent) | ollama `llama3.2:3b-instruct-fp16`, digest `195a8c01d91e` (FP16 GGUF, 6.4 GB) |
| T3 (quantized) | ollama `llama3.2:3b`, digest `a80c4f17acd5` (Q4_K_M GGUF, 2.0 GB) |
| T1 (frontier reference) | `gpt-5.2` via OpenAI API, as in all prior runs |
| Judge | `claude-opus-4-8`, fail-confirmation protocol per v1.1 |
| Hardware | Mac mini, Apple M4, 16 GB unified memory, macOS 26.3.1, ollama 0.18.1 |
| Serving | Ollama OpenAI-compatible endpoint, localhost, temperature 0, MAX_OUTPUT_TOKENS 4000 |

Both tiers are the same Meta checkpoint at different precisions, so any pass-rate gap between T3 and T2 is attributable to quantization alone. Design: 5 query classes x 3 tiers x 3 runs = 45 cells, v1.1 rubric, locked.

## Why this family and not a larger one

Disk constraint, declared honestly: the machine had ~13 GiB free; the FP16 parent of a 7B-class model (~15 GB) does not fit. The 3B family fits both precisions simultaneously. Consequence, stated before the run: the five-model exploratory run (2026-07-24T05:32Z) measured this Q4 model at 3/15 against the frontier-calibrated rubric, so FLOOR EFFECTS are expected: T2 will likely also fail many cells, and the v1.0 section 7 GREEN gate (T2+T3 aggregate >= 70%) is not realistically reachable at this size class. The registered headline number is therefore the **T3/T2 retention ratio per class** and the expected gate verdict is YELLOW or RED. This instance certifies quantization retention for the 3B class on this workload. It does NOT certify the local-deployment pitch at production scale; that requires a 7B+ instance on a machine with more disk, or a hosted fp16 endpoint, as a future amendment.

## Adapted prior (declared before the run)

1. T2 (fp16) aggregate against the rubric: 20-40% (floor effects at 3B).
2. T3 (Q4_K_M) passes >= 85% of the cells T2 passes (the v1.0 prior, carried).
3. Any retention losses concentrate in Q1-Q4 (language/judgment); Q5 arithmetic holds at both precisions (the Q4 model already passed Q5 3/3 in the exploratory run).

## Execution note

The calibration nano tier is omitted (the harness reports the calibration gate as not applicable); the discrimination requirement was already satisfied by the v1.1 recalibration (2026-07-24T04:23Z). Estimated cost: ~$0.60, dominated by judge COGS. Wall time dominated by the fp16 tier on-device.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
