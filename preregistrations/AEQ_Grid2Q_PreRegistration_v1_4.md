# AEQ GRID-2Q EXPERIMENT -- PRE-REGISTRATION v1.4 (AMENDMENT)

**Amended:** 2026-07-29T05:53:22Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026. This amendment was drafted and registered by his coding agent at his direction on the same date, before the run it governs.
**Status:** REGISTERED -- recorded BEFORE the local-model comparison run executes.
**Supersedes:** v1.3 for the local SUT roster only. The rubrics (v1.1), the discrimination gate, the v1.3 achievability accounting (non-trap floor), and all measurement rules otherwise carry forward UNCHANGED.

---

## 1. Purpose of this arm

The question this run answers: does a current-generation open-weight model running on consumer hardware (Apple Silicon, Q4 quantization, no per-token price) pass the same workload rubric as the paid frontier reference? The v1.1/v1.3 runs carried local SUTs (qwen2.5:7b Q4, llama3.2:3b Q4) as exploratory arms. Those weights are no longer installed on the machine; this arm replaces them with the two models currently on disk, pinned by digest.

## 2. Local SUT roster (pinned before running)

| Local SUT | Ollama digest | Parameters | Quantization | Endpoint |
|---|---|---|---|---|
| qwen3.5:latest | 6488c96fa5fa | 9.7B | Q4_K_M | http://localhost:11434/v1/chat/completions |
| gemma4:12b | 4eb23ef187e2 | 11.9B | Q4_K_M | http://localhost:11434/v1/chat/completions |

Both are exploratory and excluded from the calibration gate, consistent with the harness's handling of --extra-sut tiers. The ":latest" tag is resolved by the digest above; the digest, not the tag, is the pinned identity. Pre-run verification confirmed both models return populated content (not reasoning-only truncation) through the harness's exact call path at the registered MAX_OUTPUT_TOKENS of 4000.

## 3. Full run roster

| Role | Model | Price basis |
|---|---|---|
| T1 frontier reference | gpt-5.6-sol | $5.00 / $30.00 per MTok, carried verified from v1.3 (2026-07-24); re-verify if the run report is published standalone |
| T3 nano (discrimination probe) | gpt-5.6-luna | $1.00 / $6.00, carried as above |
| Local SUTs (exploratory) | per section 2 | no per-token price; marginal API cost $0. Hardware amortization and energy are out of scope and stated as such in any report |
| Judge (OpenAI + local cells) | claude-opus-4-8 | $5.00 / $25.00 (Anthropic docs) |

No Anthropic-family SUT in this arm: the question is open-weight local vs paid API, and the minimal roster that answers it with an intact calibration gate is the four rows above. Temperature 0, three runs per cell, cross-family judging with fail re-adjudication, all per the carried-forward rules.

## 4. Prior (declared before running)

Extrapolating from the 2026-07-24 five-model refresh and the earlier local-SUT arms:

1. Each local model passes at least 3 of the 4 non-trap classes (at least 9 of 12 non-trap cells each). The quantitative class (Q5) is the most likely local failure, the fabrication failure mode seen in the 7B-class arm.
2. The Q4 distractor trap catches at least one of the two local models 3 out of 3; a local model beating the frontier's 0/3 on the trap would repeat the v1.3 finding that trap resistance does not track price or size.
3. Frontier and nano reproduce their 2026-07-24 refresh patterns (frontier >= 11/12 non-trap; nano 12/12 non-trap with trap failures), since models and rubric are unchanged.
4. Local latency is one to two orders of magnitude above API latency (pre-run spot checks: ~40 s and ~125 s for a short prompt vs ~1-9 s API end-to-end). Latency is reported as a finding, not gated.

## 5. What would falsify the substitution-relevant claim

If both local models fail 2 or more non-trap classes, the open-weight-on-consumer-hardware tier is not certifiable for this workload and the white paper's cost argument correctly continues to rest on the cheap API tier. If at least one local model matches the nano tier's non-trap record, the certified-menu floor price for this workload drops to $0 marginal, which strengthens the substitution thesis and will be reported with the latency caveat attached.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
