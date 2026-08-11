# AEQ GRID-2Q EXPERIMENT -- PRE-REGISTRATION v1.1 (AMENDMENT)

**Amended:** 2026-07-24T02:49:19Z (UTC)
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026
**Status:** REGISTERED -- amendment recorded BEFORE the recalibration run executes.
**Supersedes:** AEQ_Grid2Q_PreRegistration_v1.md for the Q4/Q5 rubrics, the Q4/Q5 evidence blocks, the adjudication protocol, and the Phase 0 prior. The calibration gate thresholds, Q1-Q3 rubrics, Phase 1 design, Phase 1 gates, and all other v1.0 rules carry forward UNCHANGED.

---

## Why this amendment exists

Calibration run 1 (2026-07-24T01:38:33Z) returned a nominal PASS: frontier 15/15 (achievability OK), nano 2/15 failed (discrimination nominally OK at the minimum). The author treats this as a FAILED calibration, for three reasons, all reported per the publish-regardless rule:

1. **Adjudication noise.** One of nano's two failures (Q2_analytical run 2) is a self-contradicting judge verdict: the judge's notes state "actually all criteria are met" while returning pass=false. Counting that cell as a pass, true discrimination is 1/15, below the locked gate of 2. This is the same failure class as the haiku judge errors in Grid-1 v1.0, now observed in claude-opus-4-8 at lower frequency. An adjudication protocol fix is required, not just a stronger judge.
2. **The purpose-built classes did not bite.** The Phase 0 prior predicted nano failures concentrated in Q4 (distractor rejection) and Q5 (derived quantitative). Nano passed both 3/3. Diagnosis: the Q4 evidence contained an explicit reminder of the critical-classification rule, reducing the task to reading it back; and Q4's correct answer ("none of the three belongs") was reachable by blanket rejection without discriminating among distractors. Q5's arithmetic produced round numbers in two steps.
3. **Margin.** Even counting both failures, 2/15 is the bare gate minimum, and neither failure came from the classes designed to discriminate.

## Changes in v1.1

| Item | v1.0 | v1.1 | Reason |
|---|---|---|---|
| Q4 evidence | 3 distractors + explicit rule reminder line | 4 flagged assets, NO reminder line; decommissioned status stated as an offline order (DC-114), not the word "excluded"; adds FAN-012 (health 48, active, already on the critical list, proposed for REMOVAL) | Remove the read-back shortcut; defeat blanket-rejection: the correct answer is now mixed (reject three proposals, keep FAN-012) |
| Q4 query and rubric | "Which of these, if any, belong?" / PASS = none belong | Evaluate three proposed ADDITIONS and one proposed REMOVAL; PASS requires rejecting all three additions with correct per-asset grounds AND rejecting the removal (FAN-012 qualifies at health 48, active), critical count stays 12 | A model must apply the h<50 + active rule per asset in both directions |
| Q5 evidence | critical $86,400 / portfolio $240,000 | adds: "of which the 5 maintenance-overdue critical assets: $46,800" | Enables a three-step derivation with non-round intermediate values |
| Q5 query and rubric | share of spend (36%) and mean per critical asset ($7,200) | average annual maintenance cost of overdue critical assets ($9,360, accept $9,300-9,400) vs non-overdue critical assets ($5,657, accept $5,600-5,720), and their ratio (1.65x, accept 1.6-1.7) | Three derivations; the second is a non-round division ($39,600 / 7); arithmetic under pressure is the class's purpose |
| Adjudication protocol | single judge verdict per cell | (a) judge prompt gains an explicit consistency instruction ("if every rubric element is satisfied, pass MUST be true; notes must agree with the flag"); (b) every FAIL verdict triggers one independent re-adjudication; if the two disagree, a third call breaks the tie (majority rules); all verdicts logged | Calibration run 1 shows a single-shot FAIL can be self-contradicting noise; PASS verdicts are not re-adjudicated (asymmetric by design: false FAILs corrupt the discrimination count, false PASSes are caught by the achievability check) |
| Phase 0 prior | nano fails 2-5 of 15, concentrated in Q4/Q5 | nano fails 2-6 of 15, with at least half the failures in Q4/Q5 | Re-declared for the recalibration; run 1 scored 2 nominal / 1 confirmed, concentrated in Q1/Q2, so the v1.0 prior MISSED and is recorded as such |

Calibration gate thresholds are UNCHANGED: frontier >= 13/15, nano fails >= 2/15, both required, failures now counted only after the confirmation protocol.

## Cost note

Re-adjudication triggers only on FAIL verdicts; expected added judge cost is under $0.10. Recalibration total estimate remains under $1.

## Run 1 disposition

Run 1 outputs are preserved at experiments/grid2q/phase0/ (report and raw JSON committed unaltered). They are reported as a failed calibration under this amendment's reasoning, not discarded.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
