# AEQ GRID-2Q EXPERIMENT -- PRE-REGISTRATION v1.0

**Pre-registered:** 2026-07-24T01:24:36Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026
**Status:** REGISTERED -- NOT YET RUN. Written and timestamped before any Grid-2Q cell executes. Gates and rubrics below may not be modified after Phase 0 begins; changes require a numbered amendment recorded before the affected run.
**Naming:** "Grid-2Q" (Q for quantization). Grid-1's pre-registration reserved "Grid-2" for the tool-selection experiment; that name remains available.
**Supersedes:** the design sketch AEQ_Grid2Q_Design_Sketch_DRAFT.md, approved by the author 2026-07-23 PT.

---

## 1. The Question

Does a quantized open-weight model, running on commodity local hardware, deliver rubric-equivalent answers to (a) its own full-precision parent and (b) a frontier API reference, per query class, and at what measured cost and speed?

Grid-1 v1.1 (2026-07-24T00:27Z) answered the hosted-tier version: cheap API tiers passed 27/27 cells on the v1.0 query classes. That result removed quantization as a savings story but left the deployment-location question open: can a company move a workload class onto its OWN hardware with certified zero rubric loss? This is the AEQ Verify edge wedge ("this workload class passes the rubric on this hardware at this cost per verified-equivalent answer") and the question a frontier API vendor cannot neutrally answer.

## 2. The Instrument Problem This Experiment Must Fix First

Grid-1 v1.1 passed 27/27. A rubric everything passes has no discrimination: it cannot separate tiers, so it could not detect quantization damage if damage existed. **Phase 1 may not run until the hardened rubric demonstrably fails somebody.** That demonstration is Phase 0, and its gate is locked here.

## 3. Phase 0 -- Rubric Hardening and Calibration

Two new query classes; three tightened ones. Full rubric text is section 5 and is carried verbatim in the Phase 0 script.

- **Q1 retrieval (tightened):** citation floor rises from 3-of-5 critical asset IDs to 5-of-5.
- **Q2 analytical (tightened):** the top TWO priorities must be named in correct order (PUMP-003 then HVAC-007), not just the top one.
- **Q3 synthesis (tightened):** adds a required-absence criterion: no recommendation may reference an asset absent from the evidence.
- **Q4 distractor rejection (new):** the evidence gains a flagged-for-review tool output containing three engineered distractors (an alarming-but-not-critical asset, a decommissioned asset with critical-range health, and a cosmetic-issue asset). PASS requires excluding all three from the active critical list with correct reasoning. Precision loss shows up first as blurred boundary judgments; this class is built to catch it.
- **Q5 derived quantitative (new):** the evidence gains a cost tool output; the answer requires two derived numbers not present in the evidence (critical share of annual maintenance spend, and mean annual maintenance cost per critical asset). Multi-step arithmetic is a known early casualty of aggressive quantization. Tolerances are declared in section 5.

**Calibration design:** hardened rubric run on the Grid-1 frontier reference tier and the Grid-1 nano tier only. 5 classes x 2 tiers x 3 runs = 30 cells. Judge and adjudication rules identical to Grid-1 v1.1 (cross-family, claude-opus-4-8, structured JSON, parse failures re-adjudicated once, never dropped).

**Calibration gate (LOCKED):**
- Frontier passes >= 13 of 15 cells (achievability / integrity).
- Nano fails >= 2 of 15 cells (discrimination).
- Both conditions must hold. If nano still passes everything, escalate Q4/Q5 difficulty and re-register as an amendment before recalibrating. If frontier fails broadly, the rubric is defective; fix and re-register. All calibration runs are reported, never discarded.

## 4. Phase 1 -- Design: 5 x 3 x 3

| Dimension | Levels |
|---|---|
| Query class | Q1-Q5 as hardened in Phase 0 |
| System under test | T1 frontier API reference (pinned at run time), T2 open-weight parent at full precision, T3 the SAME open-weight model quantized |
| Runs per cell | N = 3, temperature 0 |

45 cells. The load-bearing comparison is **T3 vs T2**: same weights, different precision, so any pass-rate gap is attributable to quantization and nothing else. T1 remains the external reference and integrity check. Comparing a quantized model X against an API model Y and calling the gap "quantization damage" is prohibited; it confounds model identity with precision.

**SUT model selection (pinned at Phase 1 registration amendment, not here):** an open-weight model with a credible full-precision endpoint AND a local quantized build (llama.cpp / Ollama / MLX on Apple Silicon). Checkpoint hash and quantization method (e.g. Q4_K_M GGUF) recorded at that time. The design is model-agnostic; the amendment pins the instance.

**Hardware anchor:** chip, RAM, OS, runtime, and runtime version are recorded and become part of the certified claim: "workload class W passes on model M at quantization Q on hardware H."

**Replay semantics:** identical to Grid-1: all tiers receive the same deterministic tool outputs injected as evidence. Declared limitation carries forward: tool selection is NOT tested here; that remains the reserved Grid-2 experiment.

## 5. Equivalence Rubrics (pre-registered; verbatim in the Phase 0 script)

Evidence additions for Q4/Q5 are fixed in the script: the flagged-for-review output (CHIL-005 health 52 with an urgent field note; GEN-009 health 41 but DECOMMISSIONED 2025-12-01; PUMP-014 health 58 with cosmetic corrosion) and the cost output (critical annual maintenance $86,400; full active portfolio annual maintenance $240,000; 12 critical assets).

**Q1 -- Retrieval (tightened).** "What are the critical assets in the portfolio?"
PASS requires: (a) critical count = 12; (b) cites ALL FIVE of PUMP-003, HVAC-007, COMP-002, BOIL-001, PUMP-009; (c) no asset IDs or counts contradicting the evidence.

**Q2 -- Analytical (tightened).** "Which assets should be prioritized for maintenance in the next 30 days, and why?"
PASS requires: (a) top priority PUMP-003 AND second priority HVAC-007, in that order; (b) at least 2 of BOIL-001, COMP-002, GEN-004 also named; (c) justification cites at least one quantitative signal (risk score, health score, or overdue days); (d) no fabricated numbers.

**Q3 -- Synthesis (tightened).** "Draft a one-paragraph recommendation for leadership on the state of the asset portfolio and the single most important action to take."
PASS requires: (a) portfolio characterized as declining or at-risk, consistent with 24% critical and the 3.2-point 90-day decline; (b) recommended action addresses the highest-risk asset(s) or the overdue-maintenance backlog; (c) no fabricated statistics; (d) at most 250 words; (e) no referenced asset absent from the evidence.

**Q4 -- Distractor rejection (new).** "A colleague proposes adding CHIL-005, GEN-009, and PUMP-014 to the critical asset list. Which of these, if any, belong on the active critical list, and why?"
PASS requires: (a) concludes NONE of the three belongs on the active critical list; (b) reasoning correctly grounds each exclusion (CHIL-005 health 52 is not below the critical threshold of 50 despite the urgent note; GEN-009 is decommissioned and excluded from the active portfolio despite health 41; PUMP-014 health 58 is not critical); (c) does not add any of the three to the critical list or invent a new critical count; (d) no fabricated numbers.

**Q5 -- Derived quantitative (new).** "What percent of the active portfolio's annual maintenance spend goes to critical assets, and what is the average annual maintenance cost per critical asset?"
PASS requires: (a) critical share stated as 36% (tolerance: 35-37%); (b) per-asset figure stated as $7,200 (tolerance: +/- $100); (c) both figures derived, not disclaimed or refused; (d) no fabricated inputs.

A response FAILS if any required element is absent or contradicted. Judge returns structured JSON: {pass, failed_criteria, notes}.

## 6. Stated Prior (declared before any run)

**Phase 0 prior:** the hardened rubric passes calibration on the first attempt: frontier >= 13/15 and nano fails 2-5 of 15, with nano's failures concentrated in Q4/Q5.
**Phase 1 prior:** T3 (4-bit class quantization) passes >= 85% of the cells T2 passes, with losses concentrated in Q4/Q5; T2 aggregate against the rubric >= 70%. Declared here so results are scored against the prediction, not fitted to it.

## 7. Phase 1 Go / No-Go Gates (LOCKED)

| Gate | Condition | Meaning |
|---|---|---|
| GREEN | T3 passes >= 90% of the cells T2 passes AND T2+T3 aggregate >= 70% AND combined Q4+Q5 pass >= 50% | "Quantization-lossless for this workload class" is certifiable; the edge/on-prem certification pitch stands on measured evidence. |
| YELLOW | T3 holds Q1-Q3 but Q4 or Q5 falls below 50% | Certification narrows to per-query-class: easy classes route local, hard classes stay on the wire. |
| RED | T3 loses > 25% of T2's passes, or losses spread across all classes | Quantization damage is real at this configuration. The certifier story survives (the instrument caught it); the local-deployment claim does not, at this size/method. |

A RED Phase 1 is publishable and useful: an instrument that detects quantization damage is what a certifier sells. Only a Phase 0 that cannot discriminate is a dead end, and that outcome forces amendment, not silent tuning.

## 8. Measurement and Integrity Rules (inherited from AEQ Spec v1.0 and Grid-1)

1. Pin everything: model names at run time, checkpoint hashes and quantization method (Phase 1), runtime versions, judge model, temperature 0, pricing verified against official pages before publication.
2. API tokens from usage fields; local tokens from the runtime's counters; every number labeled measured vs estimated.
3. Local inference has no per-token price. Report measured wall-clock latency, measured tokens/sec, and an estimated $/query (amortized hardware, labeled ESTIMATED). Latency is a first-class result: it is the number that does not deflate as token prices fall.
4. N=3 per cell; failed runs logged, not dropped; full answer text captured.
5. Results published regardless of outcome, including a failed Phase 0.
6. No instance-specific values baked into the harness: model ids, judge id, and output directory enter via required CLI flags.

## 9. Run Instructions (Phase 0)

```
# .env with OPENAI_API_KEY and ANTHROPIC_API_KEY
pip install tiktoken requests python-dotenv
python experiments/grid2q/aeq_grid2q_phase0.py --dry-run \
    --frontier-model gpt-5.2 --nano-model gpt-5-nano \
    --judge-model claude-opus-4-8 --outdir experiments/grid2q/phase0
python experiments/grid2q/aeq_grid2q_phase0.py \
    --frontier-model gpt-5.2 --nano-model gpt-5-nano \
    --judge-model claude-opus-4-8 --outdir experiments/grid2q/phase0
```

Estimated Phase 0 cost: under $2 (30 execution calls, 30 judge calls at opus pricing). Estimated wall time: 10-20 minutes.

## 10. What Gets Reported

Phase 0: per-cell pass/fail, tokens, cost, latency, full answers; the calibration verdict (both gate conditions, explicitly); failure distribution across classes, scored against the Phase 0 prior. Phase 1 (after its pinning amendment): the pass matrix, the T3/T2 retention ratio per class (headline number), latency and tokens/sec per tier, judge COGS per verified query, gate verdict, prior comparison, and a one-page prototype certification artifact in the form AEQ Verify would hand a customer.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
