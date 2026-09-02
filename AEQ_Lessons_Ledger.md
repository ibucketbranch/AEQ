# AEQ LESSONS LEDGER

**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026
**Purpose:** every defect the AEQ methodology has caught in itself, with how it was detected, what changed, and how the fix was verified. Each entry is a reusable rule for the next rubric, the next judge, the next engagement. The loop is: detect -> diagnose -> amend (recorded before rerun) -> verify. Improvements never touch a live run; that is what separates a self-improving instrument from goalpost-moving.

Entries are append-only. Date format UTC.

---

## L1. A rubric everything passes certifies nothing (2026-07-24)

**Broke:** Grid-1 v1.1 and Grid-2Q calibration run 1 saturated (27/27, then near-perfect). The exam could not distinguish a frontier model from a nano model.
**Detected by:** the calibration gate concept itself: requiring the weak tier to fail before the exam may certify anyone.
**Fix:** harder classes (Q4 traps, Q5 derivation), tightened Q1-Q3. Amendment v1.1.
**Verified:** run 2 produced frontier 14/15, nano 5/15: discrimination on merit.
**Reusable rule:** no rubric certifies until it has demonstrably failed a weaker system. Ship the calibration gate with every engagement.

## L2. Evidence must not contain the answer key (2026-07-24)

**Broke:** the v1.0 Q4 evidence ended with "Reminder: critical classification requires ACTIVE status and health < 50," turning a judgment task into a read-back task. Nano aced it.
**Detected by:** run 1 failure distribution: zero failures in the class built to discriminate.
**Fix:** removed the reminder; the rule must be inferred from the health-analysis block. Amendment v1.1.
**Verified:** run 2 and the five-model run: Q4 became the strongest discriminator in the exam.
**Reusable rule:** scan evidence for embedded rubric criteria before registering. If the pass condition is quotable from the evidence, the class tests reading, not judgment.

## L3. All-reject traps reward blanket rejection (2026-07-24)

**Broke:** v1.0 Q4's correct answer was "none of the three belongs," reachable by reflexively rejecting everything without per-item reasoning.
**Detected by:** design review during the v1.1 amendment, prompted by L1.
**Fix:** added FAN-012, an item that genuinely qualifies, so the correct answer is mixed: reject three, keep one.
**Verified:** five-model run: llama and qwen failed Q4 in both directions (added wrong items AND removed the right one), which an all-reject shape could never expose.
**Reusable rule:** every trap set needs at least one item where the correct action is the opposite of the majority, so no blanket strategy passes.

## L4. Judges contradict themselves; audit the verdict, not just the answer (2026-07-24)

**Broke:** run 1, Q2 nano: the opus judge returned FAIL while its own notes read "actually all criteria are met." Same failure class as the haiku judge's false rejections in Grid-1, lower frequency.
**Detected by:** reading the raw verdict notes against the pass flag instead of trusting the flag.
**Fix:** consistency instruction in the judge prompt, plus the fail-confirmation protocol: every FAIL re-adjudicated independently, majority on disagreement. PASS verdicts deliberately not re-checked (false FAILs corrupt discrimination; false PASSes are caught by the achievability floor). Amendment v1.1.
**Verified:** runs 2 and 3: 36 re-adjudications total, zero surviving self-contradictions.
**Reusable rule:** a judge is a measurement device and needs its own error model. Asymmetric confirmation is cheap: only fails re-judge.

## L5. Output caps silently zero out reasoning-tier models (2026-07-23, recurred 2026-07-24)

**Broke:** Grid-1 at 600 tokens, then Grid-2Q at 4,000: reasoning-tier models (gpt-5-mini/nano) consumed the entire completion budget on hidden reasoning and returned empty answers. Harder questions worsen it: nano returned zero words in 3 of 15 cells on the v1.1 rubric.
**Detected by:** empty answers with tokens_out exactly at the cap.
**Fix:** cap raised by amendment (600 -> 4,000); residual artifacts now logged and argued separately from substantive failures rather than hidden.
**Verified:** partially: 4,000 sufficed for most cells; the phenomenon persists on the hardest classes and is now reported as a finding, not a bug.
**Reusable rule:** for reasoning-tier SUTs, check tokens_out == cap on every empty answer, and report cap artifacts as their own failure category. An empty answer is not a wrong answer.

## L6. Connection-level errors need the same retry discipline as HTTP errors (2026-07-24)

**Broke:** the first v1.1 recalibration attempt died mid-grid on an SSL bad-record-MAC exception that bypassed the HTTP-status retry loop, wasting a third of a run.
**Detected by:** run crash with a clean traceback.
**Fix:** requests-level exceptions now back off and retry like a 5xx on every caller (SUT, judge, both families).
**Verified:** all subsequent runs completed through at least one transient network event.
**Reusable rule:** the retry loop must wrap the transport, not just the response code.

## L7. Failures at temperature 0 are stable, which makes certification durable (2026-07-24)

**Observed, not broken:** across the five-model run, every failing model failed the same way 3/3 times: llama fabricated the identical "$86,400 to $0" claim each run; qwen produced the identical wrong $58,500/$27,900/2.10 triple each run.
**Implication:** pass/fail is a stable property of the (model, query class) pair. A certified route stays certified between model version changes; recertification triggers on version bumps, not on every query.
**Reusable rule:** N=3 at temperature 0 is enough to establish a class verdict for a pinned model version; spend the sample budget across classes, not within them.

## L8. Grounding fails before arithmetic does (2026-07-24)

**Observed:** qwen2.5:7b computed a perfectly consistent ratio on inputs it invented (it split the correct $86,400 total into a fabricated $58,500/$27,900 and reported totals as averages), while the smaller llama3.2:3b pulled the right inputs and did the ugly division correctly.
**Implication:** "can it do math" is the wrong question for rubric design; "does it bind the right evidence values to the right roles" is the discriminating one. Capability is per-class, not per-size.
**Reusable rule:** quantitative rubric criteria must pin exact derived values with tolerances. Internal consistency of an answer proves nothing about groundedness.

## L9. Boundary judgment under narrative pressure is the sharpest known discriminator (2026-07-24)

**Observed:** the CHIL-005 trap (urgent-sounding field note on an asset at health 52, just above the critical threshold of 50) fooled every tier at least once: frontier 1/3, haiku 3/3, qwen 3/3, llama 3/3.
**Implication:** models over-weight emotionally salient text against numeric thresholds. This failure mode spans families and sizes, and it is exactly the class of error that costs real money in production agents.
**Reusable rule:** every engagement's rubric should include at least one just-above-threshold item dressed in urgent language. Cheap to author, brutally effective.

## L10. Deprecation calendars are part of experimental validity (2026-07-24)

**Broke:** the entire Grid series ran on gpt-5.2 / gpt-5-mini / gpt-5-nano. A pricing-verification pass found all three deprecated, gpt-5.2 with a shutdown 17 days out, and none with publicly listed prices, making the headline results unreproducible and their dollar figures unciteable within weeks of any publication.
**Detected by:** attempting to verify the PRICING table against the official page before publication, per the measurement rules.
**Fix:** amendment v1.3 pinned current-generation replacements (gpt-5.6-sol/luna) with prices verified same-day; the harness now records pricing verification per model and refuses to bless legacy rows.
**Verified:** the refresh run (in progress at entry time) re-establishes every headline number on reproducible models.
**Reusable rule:** before any run intended for publication, check the SUT's deprecation status and public pricing FIRST. A result on a model a reader cannot access or price is a demo, not evidence. Local pinned weights are immune; hosted models rot.

## L11. A trap that catches the reference model needs its own accounting (2026-07-24)

**Broke:** once the CHIL-005 trap became hard enough to catch gpt-5.2 regularly, the frontier integrity floor (>= 13/15 across all classes) started failing for a reason that had nothing to do with rubric achievability.
**Detected by:** frontier self-pass 12/15 in the Phase 1 run, driven entirely by Q4.
**Fix:** v1.3 splits the signals: achievability is computed on non-trap classes only (>= 11/12), and frontier trap performance is reported as a standalone finding.
**Reusable rule:** deliberately adversarial classes must be excluded from instrument-health checks, or the instrument reports itself broken every time the trap works.

## L12. A boundary that truncates silently returns a confident wrong answer (2026-08-25)

**Broke:** three times, at three points in the same call, each returning output indistinguishable from a real result. A 6,401 token prompt was silently cut to the served context window and the model answered fluently from the tail, naming the single healthiest asset when asked for the worst. A completion hit its cap and returned an empty string, which the scorer recorded as a wrong answer and which read as a capability failure. And a generation ran past the window that prompt and completion share, at 8,377 in plus 8,007 out against 16,384, returning nothing while stopping 185 tokens short of the cap, so the cap guard never fired.
**Detected by:** comparing tokens sent against tokens the server reported receiving, which is the only place the first loss is visible. The second and third were caught only because the guard tested for an empty answer as well as a cap hit. Written on the cap alone, as the obvious version would have been, it would have published the wasteful variant as answering that query incorrectly.
**Fix:** four conditions void a cell rather than scoring it: prompt ratio below a declared floor, any call reaching max_tokens, an empty answer, and a pre-flight check refusing the cell when the prompt leaves less headroom than max_tokens. A voided cell is recorded as an error and retried, never scored. The guard's own advice was also wrong and was corrected: it said to raise max_tokens, which could not work, because there was no room for a larger cap.
**Verified:** the prompt guard fires on the unpinned model and passes at 0.99 on the pinned one. The empty-answer guard caught the case the cap guard missed. At a 32,768 context the previously failing cell passes at 12,900 total tokens. One cell in a 90-cell arm voided at the cap and was reported rather than scored.
**Reusable rule:** every boundary in a model call fails silently and each fails differently. Compare what you sent against what the server says it received, refuse to score any answer that is empty or truncated, and check before the call that the prompt leaves room for the completion, because prompt and completion share one window. A cell that hit a boundary is a broken cell, not a wrong answer, and scoring it as wrong understates capability while looking exactly like data.

## L13. Score the answer, not the derivation (2026-08-25)

**Broke:** six of ten scoring keys demanded values computed along the way rather than what the question asked. Asked for a combined annual cost, the model answered 9284, which was exactly right, and was marked wrong for not also listing the three assets it had summed. Queries naming an asset required the model to echo that identifier back, which measures instruction-following rather than retrieval, and the lean variant was instructed to reply with the figure only, complied, and was scored a failure for complying.
**Detected by:** smoke testing the golden set against a real model before the measured run, rather than by reviewing the keys.
**Fix:** each query declares an `answer_shape` of ids, figures, or both, and only that is scored. Values computed along the way are recorded as `figures_not_scored` or `asset_ids_not_scored` so they stay visible without being required. Identifiers appearing in the question text are removed from the required set and recorded separately.
**Verified:** re-scoring answers already collected under the corrected key moved one model from fail to pass on the affected query and left the weaker model unchanged at 4 of 10, so that model's failures were real capability rather than a scoring artifact.
**Reusable rule:** requiring a model to show its working turns a correct terse answer into a failure. The key contains what the question asks for and nothing else.

## L14. Before calling hidden reasoning overhead, switch it off and rerun (2026-08-25)

**Broke:** hidden completion tokens were treated as a distortion to be disclosed or corrected across three separate findings, on the assumption they were preamble. Nobody checked whether they could simply be disabled.
**Detected by:** Michael asking whether conceding a third of the framework defeated the point of a three-layer metric. It was the right question and the assumption had never been tested.
**Fix:** disable reasoning and rerun the same workload. Measured across ten queries on one model: eight held their answers at roughly a tenth of the completion tokens, and the two that broke were the only two requiring chained operations rather than a single pass over the data. The tokens were not padding, they were performing the second step.
**Verified:** with reasoning disabled, three runs of the same cell produced identical completion counts, so the layer that had been reversing sign became deterministic and interpretable.
**Reusable rule:** if accuracy holds without the hidden tokens they were overhead, and if accuracy drops they were work, and the token count was the price of the answer rather than waste. Test it before reporting either way.

## L15. A metric that changes sign between two valid runs is unreported, not noisy (2026-08-25)

**Broke:** the output-efficiency layer put a deliberately wasteful variant at 0.88x the optimized variant's output tokens on one query while that variant cost 1.82x in total. Read as a ranking, the layer named the wasteful architecture the efficient one. Averaging across queries would have replaced the reversal with a plausible single number.
**Detected by:** comparing the layer against the total on the same cells instead of reporting it alone.
**Fix:** report the spread across runs alongside the statistic, and compare each variant pairwise against the baseline per unit of work rather than testing a global spread across all variants.
**Verified:** the first version of that check compared the maximum-minus-minimum spread against the largest standard deviation. The most verbose variant dominated the spread, the check reported the difference as real, and it hid the wasteful variant sitting below the baseline on half the queries. The pairwise version names all three inverted cells and correctly reports none in the arm where reasoning was disabled.
**Reusable rule:** never test for a sign reversal with an aggregate that spans the things being compared, or the largest magnitude will swamp the reversal. An aggregate computed across a sign change reports a number and loses the fact.

## L16. An architecture comparison measures the specification unless granularity is held fixed (2026-08-27)

**Broke:** builder-gauge reported a stateful planner 6.36x cheaper than a stateless loop. Same task, same engine, same pinned starting commit, same held-out suite, three repeats, and the gap cleanly exceeded the spread. Every safeguard the run had said the number was real. It was a property of how the PRD was written, not of the two architectures.
**Detected by:** asking why the smaller task cost more than the larger one, which no architectural story explained. The two PRDs differed in size and in decomposition at the same time, and nothing in the matrix separated the two.
**Fix:** a branch identical to the original except that six `- [ ]` checkboxes collapsed into one covering the same work, tests byte-identical, verified by diff. Pre-registered before collection, with the control stated in advance: the planner's cost should not move, and if it did the effect belonged to the model or the task rather than the architecture.
**Verified:** the stateless loop moved 4.78x, finer being dearer, with the gap clear of the spread. The planner did not move, gap $0.17 against its own spread of $0.22. Holding the work constant and writing the specification coarsely took the arm-to-arm difference from 6.36x to 1.06x, under five cents. The original headline survived only as a statement about one PRD.
**Reusable rule:** when comparing architectures that consume a specification, the specification's structure is an independent variable, and an uncontrolled one gets attributed to the architecture. Vary it deliberately with the work held constant, and register a control arm whose cost should not move. Without that control a granularity effect and an architecture effect are the same measurement. Note the direction this cuts: the finer decomposition came from following the tool's own documented best practice, so the guidance and the benchmark were confounded together.

## L17. An unpriced model must raise, never default to zero (2026-08-27)

**Broke:** the single most expensive cell in the matrix refused to book, because its transcript named a model the price table did not rate. The obvious convenience, treating an unknown rate as zero, would have booked that cell at a small fraction of its real cost and reported a clean number.
**Detected by:** the ledger raising on the unrated model instead of defaulting it, which was written in before any cell ran for exactly this reason.
**Fix:** inspected the transcript rather than guessing. The unrated name was an engine placeholder carrying zero in every token field, emitted when a run is interrupted. It was rated at zero because it is measurably zero, verified against the transcript, and the cell rebooked.
**Verified:** the cell rebooked at $11.16. Reported cumulative spend went from $23.70 to $35.70, so the ledger had been understating by 32 percent, and the budget ceiling had been enforced against the understated figure the whole time.
**Reusable rule:** an unknown rate is missing information, not a zero. Any accounting instrument must refuse to price what it cannot price, because a defaulted zero is indistinguishable from a genuinely free call and silently biases every total that contains it. The same applies to the ceiling: a budget guard enforced against an incomplete total is not a guard.

---

*Process note: entries L1-L6 each correspond to a recorded amendment or committed fix with a timestamp preceding the verifying run. That ordering is the point.*

*Process note: L12-L15 come from the Blueberry AEQ Showcase, 2026-08-25, 180 measured cells across two arms under a pre-registration frozen before the first cell. Repository ibucketbranch/Blueberry, private. The gap between L11 (July) and L12 (August) is a phase boundary, not a dormant period: the Grid series and the showcase were separate pieces of work.*

*Process note: L16 and L17 come from builder-gauge, 2026-08-26 to 2026-08-27, a two-arm builder benchmark of 18 measured cells under a pre-registration frozen before the first cell, with a second pre-registration frozen before the granularity isolation in L16. Repository ibucketbranch/Blueberry, private; the benchmark target is ibucketbranch/loop-bench, also private, pinned by commit. Both entries are cost-accounting lessons rather than rubric lessons, which is a change of subject for this ledger and the reason they are numbered here rather than kept in the project that produced them.*
