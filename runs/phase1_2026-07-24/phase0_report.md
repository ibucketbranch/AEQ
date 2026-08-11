# AEQ GRID-2Q PHASE 0 -- CALIBRATION RESULTS
Run completed: 2026-07-24T06:05:11Z | Runs per cell: 3
Frontier: gpt-5.2 | Nano: None | Judge: claude-opus-4-8
Pricing verified against official pages: False  << VERIFY BEFORE PUBLICATION

## PASS MATRIX (query class x tier)
  Q1_retrieval     | frontier: 3/3 | t2_fp16: 0/3 | t3_q4: 0/3
  Q2_analytical    | frontier: 3/3 | t2_fp16: 0/3 | t3_q4: 0/3
  Q3_synthesis     | frontier: 3/3 | t2_fp16: 0/3 | t3_q4: 0/3
  Q4_distractor    | frontier: 0/2 | t2_fp16: 0/3 | t3_q4: 0/3
  Q5_quantitative  | frontier: 3/3 | t2_fp16: 0/3 | t3_q4: 3/3
  (tiers beyond frontier/nano are exploratory; the gate ignores them)

## CALIBRATION GATE (locked -- pre-registration section 3)
  (frontier integrity: 12/15 vs floor 13)
  >>> CALIBRATION N/A (no nano tier: Phase 1 / exploratory run) <<<
  [!] Rubric still cannot discriminate. Escalate Q4/Q5 difficulty,
      record an amendment, and recalibrate before Phase 1.
  [!] Frontier failed its own rubric too often. Rubric is defective;
      fix, record an amendment, and recalibrate.

## NANO FAILURE DISTRIBUTION (Phase 0 prior: failures concentrate in Q4/Q5)
  Q1_retrieval    : 0 failed run(s)
  Q2_analytical   : 0 failed run(s)
  Q3_synthesis    : 0 failed run(s)
  Q4_distractor   : 0 failed run(s)
  Q5_quantitative : 0 failed run(s)

## FAILED CELLS
  Q4_distractor x frontier run 1: (a) rejects adding CHIL-005, (e) concludes the critical count remains 12 -- The candidate approves adding CHIL-005 (health 52 is above the critical threshold of 50, so it should be rejected) and c
  Q4_distractor x frontier run 2: (a) rejects adding CHIL-005 because health 52 is not below critical threshold, (e) concludes critical count remains 12 -- The candidate approves adding CHIL-005 (rubric requires rejection because health 52 is above the critical threshold of 5
  Q4_distractor x frontier run 3: no_answer -- 
  Q1_retrieval x t2_fp16 run 1: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradictions, but never states the critical asset count of 12.
  Q1_retrieval x t2_fp16 run 2: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradictions, but never states the critical asset count of 12,
  Q1_retrieval x t2_fp16 run 3: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradictions, but never states the critical asset count of 12,
  Q2_analytical x t2_fp16 run 1: (a) top priority is PUMP-003 AND second priority is HVAC-007 in that order -- The candidate lists BOIL-001 first and COMP-002 second, explicitly excludes PUMP-003 from the 30-day window, and omits H
  Q2_analytical x t2_fp16 run 2: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate ranks BOIL-001 first and COMP-002 second, explicitly excluding PUMP-003 from the 30-day window and omittin
  Q2_analytical x t2_fp16 run 3: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate lists BOIL-001 and COMP-002 as top priorities and explicitly excludes PUMP-003 from the 30-day window, fai
  Q3_synthesis x t2_fp16 run 1: (a) portfolio characterized as declining or at-risk -- The candidate addresses the overdue critical assets and cites accurate stats within word limit, but never characterizes 
  Q3_synthesis x t2_fp16 run 2: (a) portfolio characterized as declining or at-risk -- The candidate addresses the overdue critical assets and highest-risk assets (b), uses accurate statistics (c), stays und
  Q3_synthesis x t2_fp16 run 3: (a) portfolio characterized as declining or at-risk -- The candidate addresses the overdue critical assets (b), uses accurate statistics (c), stays under 250 words (d), and re
  Q4_distractor x t2_fp16 run 1: (d) rejects REMOVING FAN-012, (e) concludes the critical count remains 12, (f) no fabricated numbers -- The candidate wrongly approves removing FAN-012 (health 48 is critical), does not conclude the count stays at 12, and fa
  Q4_distractor x t2_fp16 run 2: (d) rejects REMOVING FAN-012, (e) critical count remains 12, (f) no fabricated numbers -- The candidate wrongly approves removing FAN-012 (which is active with health 48, qualifying as critical), does not concl
  Q4_distractor x t2_fp16 run 3: (d) rejects REMOVING FAN-012, (e) concludes the critical count remains 12, (f) no fabricated numbers -- The candidate approves removing FAN-012 (which is critical at health 48), incorrectly concludes the list drops to 8 asse
  Q5_quantitative x t2_fp16 run 1: a, b, c, e -- The candidate fabricated per-asset costs and stated overdue average $6,500, non-overdue $9,000, and ratio 0.72, none of 
  Q5_quantitative x t2_fp16 run 2: a, b, c, e -- The candidate fabricated per-asset costs and produced incorrect averages ($6,500 and $9,000) and ratio (0.72) instead of
  Q5_quantitative x t2_fp16 run 3: a, b, c, e -- The candidate fabricated per-asset costs and reported incorrect averages ($6,500 and $9,000) and ratio (0.72) instead of
  Q1_retrieval x t3_q4 run 1: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradictions but never states the critical asset count of 12.
  Q1_retrieval x t3_q4 run 2: (a) states the critical asset count = 12 -- The candidate cites all five required asset IDs with no contradictions, but never states the critical asset count of 12,
  Q1_retrieval x t3_q4 run 3: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradicting data, but never explicitly states the critical ass
  Q2_analytical x t3_q4 run 1: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate omits PUMP-003 and HVAC-007 entirely, failing the required top-two priority ordering.
  Q2_analytical x t3_q4 run 2: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate omits PUMP-003 and HVAC-007 entirely, failing to name the required top two priorities in order.
  Q2_analytical x t3_q4 run 3: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate omits PUMP-003 and HVAC-007 entirely, failing to name the required top two priorities in order.
  Q3_synthesis x t3_q4 run 1: c -- The claim that this action reduces annual maintenance cost from $86,400 to $0 is a fabricated statistic not supported by
  Q3_synthesis x t3_q4 run 2: (c) no fabricated statistics -- The claim that fixing PUMP-003 reduces annual maintenance cost for critical assets 'from $86,400 to $0' is a fabricated/
  Q3_synthesis x t3_q4 run 3: c -- The claim that this action will reduce annual maintenance cost 'from $86,400 to $0' is a fabricated statistic not suppor
  Q4_distractor x t3_q4 run 1: c, d, e, f -- Candidate wrongly adds PUMP-014 (health 58), wrongly agrees to remove FAN-012, concludes count is 10 not 12, and fabrica
  Q4_distractor x t3_q4 run 2: (a) rejects adding CHIL-005, (c) rejects adding PUMP-014, (d) rejects removing FAN-012, (e) critical count remains 12, (f) no fabricated numbers -- The candidate wrongly adds PUMP-014, agrees to remove FAN-012, includes CHIL-005 in the final list despite saying it wou
  Q4_distractor x t3_q4 run 3: (a) rejects CHIL-005, (c) rejects PUMP-014, (d) rejects removing FAN-012, (e) critical count remains 12 -- The candidate incorrectly recommends adding PUMP-014, agrees to remove FAN-012 (which is active with health 48, still cr

## PER-TIER ECONOMICS (local models have no per-token price; latency is the cost)
  frontier    : pass 12/14 | mean $0.005223/query | 3.7s latency | 272 out-tokens
  t2_fp16     : pass 0/15 | mean $0.000000/query | 15.2s latency | 189 out-tokens
  t3_q4       : pass 3/15 | mean $0.000000/query | 6.6s latency | 202 out-tokens

Mean judge COGS per cell: $0.024128
Cells re-adjudicated (fail-confirmation protocol, v1.1): 29 of 45
Full answers and per-cell data: phase0_raw.json
Author: Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026