# AEQ GRID-2Q EXPERIMENT -- PRE-REGISTRATION v1.4.1 (SERVING-CONFIG NOTE)

**Amended:** 2026-07-29 (UTC), before any counted local-SUT cells executed.
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026. Drafted and registered by his coding agent at his direction.
**Supersedes:** v1.4 for the local serving configuration only. Roster, prior, and all measurement rules carry forward UNCHANGED.

---

## Why this note exists

Two run attempts under v1.4 aborted before producing any counted results. First, the qwen3.5 weights were found removed from the host between registration and execution (restored by re-pull; the registry digest matched the v1.4 pin exactly, 6488c96fa5fa, so the pinned identity is unchanged). Second, the host's Ollama server (0.32.4) defaults these models to a 65,536-token context, which pushed the predicted load footprint (8.1 GiB for qwen3.5) past available memory on the 16 GB host; the scheduler refused the load and every local request errored with zero output tokens. Those zero-token cells are load failures, not model failures, and no judge saw them.

## The change

Both local SUTs are served through derived Modelfile wrappers that pin num_ctx to 8192 and change nothing else. The rubric needs well under 8192 tokens (about 800 in, 4000 max out). Weights, quantization, and parameters are byte-identical to the v1.4 pins.

| Serving name | Wrapper ID | Base (v1.4 pin) |
|---|---|---|
| qwen3.5-ctx8k | 5c7620e9c5d3 | qwen3.5:latest 6488c96fa5fa |
| gemma4-ctx8k | 49c3c8d09b98 | gemma4:12b 4eb23ef187e2 |

Any report from this run states the 8192 serving context alongside the model identity. All v1.4 declarations, including the prior, are unmodified.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
