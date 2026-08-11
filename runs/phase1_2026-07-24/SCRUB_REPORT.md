# HARNESS SCRUB — Phase 1 quantization inversion (ledger D1)
**Date:** 2026-08-09 | **Scrubbed by:** forensic audit of run artifacts + harness source (Cowork session)
**Claim under audit:** a 4-bit quantized 3B passed 3 rubric cells where its fp16 parent passed 0, identical rubric (white paper §3.3; CLAIM_LEDGER D1).
**Prior status:** UNSUPPORTED-PENDING-SCRUB — "bug until proven otherwise."

## Verdict: SURVIVES SCRUB (with one residual local check)

The inversion is real model behavior on this workload and rubric, not a harness artifact. Each of the four registered suspects was tested against the run artifacts:

### Suspect 1 — Chat template mismatch: CLEARED, with direct evidence
Both SUTs are Ollama library tags of the same model: `llama3.2:3b-instruct-fp16` (t2_fp16) and `llama3.2:3b` (t3_q4, Ollama default Q4 quant of the same instruct model). Decisive: **per-class `tokens_in` values are identical across the two tiers** (808, 817, 823, 832, 851). Template tokens are counted in `prompt_tokens`; a differing template between tags would produce differing counts. Identical counts across all five classes means both models received the same prompt through the same template.

### Suspect 2 — Sampling config drift: CLEARED
Both tiers were called through the same `call_openai()` path in `aeq_grid2q_phase0.py` with an identical request body: `temperature: 0` explicit (overriding any per-tag Modelfile default), same `max_completion_tokens`, same system prompt and user message construction. Behavioral confirmation: every failure and pass repeated exactly 3/3 within each tier — including the fp16 model fabricating the *same* wrong numbers ($6,500 / $9,000 / 0.72) on all three Q5 runs. Deterministic, stable behavior is inconsistent with sampling drift.

### Suspect 3 — Stop/EOS token handling: CLEARED
No answer in the raw JSON contains raw template tokens (`<|...|>`, `[INST]`, `<<SYS>>`: zero matches across 45 rows). Failed answers are complete, well-formed prose that miss rubric elements (e.g., fp16 Q1 lists all five required asset IDs correctly but never states the count of 12 — three runs in a row), not truncations. One `no_answer` occurred, on the *frontier* tier (Q4 run 3), unrelated to the local pair.

### Suspect 4 — Different inference stacks: CLEARED
Both tiers were served by the same local OpenAI-compatible endpoint (Ollama), invoked by the same harness function with the same headers, timeout, and retry logic, in the same run session.

### The behavior itself, characterized precisely
- **Q5 (quantitative derivation), where the inversion lives:** the Q4 model performed the correct derivation from the evidence three times ($46,800 / 5 = $9,360; $39,600 / 7 = $5,714; ratio ≈ 1.65). The fp16 model **confabulated a fake tool-output block** ("TOOL OUTPUT -- calculate_tco(...)") with invented per-asset costs, identically, three times.
- **Q1–Q3:** both tiers failed, largely on the same rubric elements (Q1: neither states the count; both list correct IDs). The inversion is concentrated in Q5, which is exactly what the white paper claims: capability is per-class, and precision did not order it.

### Residual check (local machine, 2 minutes, non-blocking)
Run `ollama show llama3.2:3b --template` and `ollama show llama3.2:3b-instruct-fp16 --template` and confirm the manifests match (the identical tokens_in already imply it), and record the Ollama version. Append the output to this report.

### Ledger effect
- **D1 → REPRODUCIBLE (scrubbed 2026-08-09).** White paper §3.3 sentence stands as written.
- **D2** (7B fabricating where 3B computed, across separate runs) is a different evidence base (multimodel/localmodels runs) and keeps its pending flag until given the same treatment.

*No original run artifacts were modified. This report is additive.*

---

## Addendum, 2026-08-09: residual local check attempted

`ollama show <tag> --template` was run on the original machine (Ollama 0.32.4): both model tags return "not found" — the models were removed locally sometime after the 2026-07-24 run. The template check therefore cannot be executed against the original installs. Assessment: the verdict stands unchanged, because (a) the identical per-class `tokens_in` across tiers is direct artifact evidence of identical prompt+template, and (b) both tags are upstream Ollama library manifests whose templates are fixed at the registry, not locally editable. Full closure option remains open: re-pull both tags (~8 GB) and diff the templates; doing so also enables a live reproduction of the Q5 inversion for the public reproduction repo. **Follow-up for aeq-reproduce: record model digests alongside tags in all future local runs, precisely because local installs are ephemeral — this check would have been instant with digests on file.**

## Addendum 2, 2026-08-09: full closure executed (Path B)

Both tags re-pulled from the Ollama library on the original machine (Ollama 0.32.4) and `ollama show --template` run on each. **The two templates are character-for-character identical** (standard Llama 3.2 chat template: system header with knowledge-cutoff preamble, tool-calling clauses, message loop, `<|start_header_id|>`/`<|eot_id|>` markers). Suspect 1 is closed by direct inspection, corroborating the tokens_in evidence.

Digests on file per the new rule (from pull manifests): `llama3.2:3b` primary blob `dde5aa3fc5ff`; `llama3.2:3b-instruct-fp16` primary blob `e2f46f5b501c`. Note the models re-pulled in August 2026 resolve to the library's current manifests; the July 24 run predates this re-pull, which is exactly why digest recording is now mandatory at run time.

Remaining optional exhibit: live replay of the Q5 cell via `experiments/grid2q/replay_q5_inversion.py` (both tags, temperature 0, harness-identical prompts). To be appended when run.

## Addendum 3, 2026-08-09: LIVE REPRODUCTION — inversion confirmed on fresh weights

`replay_q5_inversion.py` executed on the original machine (Ollama 0.32.4), 3 runs per tag, temperature 0, harness-identical prompts. Model digests: `llama3.2:3b` = a80c4f17acd5; `llama3.2:3b-instruct-fp16` = 195a8c01d91e (freshly pulled 2026-08-09).

**Q4 (`llama3.2:3b`): 3/3 correct, character-identical to the 2026-07-24 recorded answer.** $46,800 / 5 = $9,360; $86,400 - $46,800 = $39,600; $39,600 / 7 = $5,714; ratio ~1.65. 98 out-tokens each run, 2.45-6.51 s latency.

**fp16 (`llama3.2:3b-instruct-fp16`): 3/3 confabulation, structurally identical to the recorded failure.** Each run produced the same fake "TOOL OUTPUT -- calculate_tco(scope='maintenance')" block with invented per-asset costs and derived figures ($6,300 / $7,000 / 0.89 this install). 171 out-tokens each run, 12.03-58.23 s latency.

**tokens_in = 832 for every run on both tags**, matching the 2026-07-24 recorded value for Q5 — identical prompt and template, verified live.

Honest nuance, recorded rather than smoothed: the fp16's *invented values* differ between the July install ($6,500 / $9,000 / 0.72) and the August re-pull ($6,300 / $7,000 / 0.89), while its *fabrication behavior and output structure* are exactly stable within each install (3/3, byte-similar). The Q4's correct answer, by contrast, is character-identical across installs 16 days apart. A harness artifact could not produce this asymmetry; a model-level failure mode does.

Secondary observation: the Q4 model was also ~5x faster per answer than its fp16 parent on this hardware (2.5 s vs 12-58 s) at 98 vs 171 out-tokens — cheaper, faster, and correct where the parent fabricates.

**Final status: D1 CLOSED. Original finding, forensic audit, template verification, digest capture, and live reproduction on fresh weights all agree. White paper Section 3.3 stands.**

Digests also captured for the 2026-07-29 exploratory run models still installed: qwen3.5 = 6488c96fa5fa (ctx8k = 5c7620e9c5d3, ctx64k = c445296b892e); gemma4:12b = 10273ec8327c (ctx8k = 49c3c8d09b98). These retroactively pin the D3 open-weight evidence base.
