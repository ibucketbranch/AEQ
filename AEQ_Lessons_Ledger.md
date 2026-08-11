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

---

*Process note: entries L1-L6 each correspond to a recorded amendment or committed fix with a timestamp preceding the verifying run. That ordering is the point.*
