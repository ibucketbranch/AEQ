# Proposed amendment to AEQ_Specification_v1.1, 2026-08-25

Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026

Status: APPLIED as v1.2 on 2026-08-25, by Michael's decision. This file is kept as
the reasoning behind the amendment, including what the evidence does not claim. The
applied text is in AEQ_Specification_v1.2.md; where the two differ in wording, the
spec is authoritative and this is the working note.

Written before the decision, when the mechanism was still open between a v1.2, an
in-place dated errata block, and a standalone amendment note cited alongside v1.1.
v1.2 was chosen, matching the versioned-files-side-by-side pattern already used by
the Grid2Q pre-registration series. v1.1 stays in place and citable.

Evidence: the Blueberry AEQ Showcase, 180 measured cells across two arms, run
2026-08-25 under a pre-registration frozen before the first cell. Repository
github.com/ibucketbranch/Blueberry (private), results in results/, findings 13 and
14 in PHASE0_FINDINGS.md.

Scope of the evidence, stated plainly: one model (gemma4 12B served at 32,768
context), one workload, three architecture variants, eight queries where value was
constant, three runs per cell. It is a single-model result. It is enough to
contradict a universal claim, which is what both changes below do, and not enough to
establish the general magnitude of the effect.

---

## Change 1. Section 4 opening paragraph

**Currently reads:**

> AEQ decomposes architectural waste into three independently addressable layers.
> Fixing one does not require touching the others: orchestration can be fixed
> without changing the model, and the prompt can be fixed without changing the
> tools.

**The problem.** Both examples in that sentence are still true, and the claim of
independent *addressability* holds. What the measurement contradicts is a reading
the sentence invites: that the layers are independent *measurements* which decompose
the total additively. They are not. Intervening on one layer moves the measured
value of another.

**Measured 2026-08-25.** Variant B's defined waste is a duplicated tool call, so it
carries the same evidence twice. On all four large-evidence queries B produced FEWER
completion tokens than the optimized variant A, by 554, 561 and 115 tokens on Q01,
Q04 and Q07, each larger than twice the run-to-run standard deviation. On all four
small-evidence queries it produced more. The extra context did part of the model's
reasoning, so Layer 1 waste reduced Layer 3.

In the opposite direction, variant C makes three model calls where A makes one, so
it pays the per-call reasoning cost three times. Its mean completion went from 748
tokens with reasoning disabled to 3,714 with it enabled, and its AEQ ratio rose from
2.14x to 2.91x while B's fell from 1.99x to 1.75x.

**Proposed replacement:**

> AEQ decomposes architectural waste into three independently addressable layers:
> orchestration can be fixed without changing the model, and the prompt can be fixed
> without changing the tools.
>
> Addressable independently does not mean measurable independently. An intervention
> on one layer can move the measured value of another, and the effect has been
> observed running in both directions. Prompt bloat that carries redundant evidence
> can reduce output tokens, because context the model would otherwise have to derive
> is already present. Orchestration bloat multiplies output cost, because every
> additional model call pays whatever the model spends per call. On a reasoning-tier
> model these two effects moved two variants' totals in opposite directions in the
> same study (Blueberry, 2026-08-25).
>
> **Consequence for reporting.** AEQ is defined on total tokens. The three layers
> are diagnostics that locate waste and rank fixes; they are not addends that sum to
> the total, and a single layer read in isolation can rank two architectures the
> wrong way round. Report the total as the metric and the layers as attribution.

## Change 2. Section 4, Layer 3

**Currently reads:**

> **Definition:** Response verbosity beyond what the answer requires.
>
> **Measurement:** Output tokens vs. a capped baseline delivering equivalent
> content. Reference values: ~95 tokens (capped) vs. ~520 tokens (uncapped) for the
> same substantive answer, same conclusion, 5x the words.

**The problem.** The definition assumes completion tokens are the visible response.
On reasoning-tier models they are mostly not. Measured on the same study: a 4-token
answer arriving behind 476 completion tokens, and one query where the model spent
2,635 completion tokens to emit the string CHIL-134. Under the stated definition,
Layer 3 on such a model measures reasoning rather than verbosity, and output length
stops tracking answer length, which is the condition the layer needs to mean
anything.

This is measurable rather than merely arguable. With reasoning disabled the same
eight queries fell from 24.5 to 476.6 mean completion tokens for variant A, held
their answers, and Layer 3 produced identical counts across three runs. With
reasoning enabled it produced the sign inversion described in Change 1.

**Proposed addition after the Measurement paragraph:**

> **Applicability.** This layer assumes completion tokens are the response. On
> models that spend completion budget on reasoning the caller never sees, that
> assumption fails and output length stops tracking answer length. Measured
> 2026-08-25: a four-token answer behind 476 completion tokens, and 2,635 completion
> tokens spent to emit a single asset identifier.
>
> Before reporting Layer 3 on such a model, establish which of the three cases
> applies. If reasoning can be disabled and the workload still passes its
> equivalence rubric, measure Layer 3 with it disabled and say so. If disabling it
> costs equivalence, the reasoning is doing work rather than padding, and its tokens
> are the price of the answer rather than waste; report Layer 3 with its spread
> across runs and draw no ranking from it. If reasoning cannot be disabled at all,
> Layer 3 is not measurable on that model and should be reported as withheld with
> the evidence, not estimated.
>
> A fixed per-call overhead is not a safe correction. Measuring one and subtracting
> it was tried and rejected: the overhead was not fixed, ranging 66 to 2,547 tokens
> per call across ten queries on one model, and it correlated with prompt size, which
> is the variable architecture variants differ in. Subtracting it would bury a
> confound inside a corrected-looking number.

## Change 3. Section 12, Version History

Added, since the mechanism chosen was a version bump:

> | 1.2 | August 2026 | First change to validated Section 4. Layers stated as
> independently addressable but not independently measurable, with the
> cross-layer interaction measured in both directions (Blueberry, 2026-08-25, 180
> cells). Layer 3 gains an applicability note for reasoning-tier models, where
> completion tokens are not the response. AEQ remains defined on total tokens;
> layers are attribution, not addends. Sections 1-3 and 5-8 unchanged. |

---

## What this does not claim

It does not put a number on the general magnitude of cross-layer interaction. One
model, one workload. The direction was measured in both senses and the sign
inversion was reproducible across three runs, which is enough to retire a universal
claim of independence and not enough to replace it with a coefficient.

It does not revise the reference values in Layer 1 or Layer 3. Those came from the
original reference experiment on a non-reasoning model and remain accurate for it.

## Applying this

Both copies must change together, preserving each one's local pointers. The two
files differ deliberately in five lines: figure paths are relative to each file's
directory, the reference-implementation line names the other repository, and the
footer cites its own repo. The specification text is otherwise identical, and
letting it diverge is a documented past failure.

- ~/Projects/AEQ/spec/AEQ_Specification_v1.1.md (public repo)
- ~/Projects/AgentSaaSy/whitepaper/AEQ_Specification_v1.1.md
- ~/Projects/Blueberry/spec/ is a symlink to the first and needs nothing.

The PDF at ~/Projects/AEQ/spec/AEQ_Specification_v1.1.pdf is stale the moment the
markdown changes and would need regenerating.
