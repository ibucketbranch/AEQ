# AEQ GRID-2Q PHASE 0 -- CALIBRATION RESULTS
Run completed: 2026-07-30T00:21:20Z | Runs per cell: 3
Frontier: gpt-5.6-sol | Nano: gpt-5.6-luna | Judge: claude-opus-4-8
Pricing verified (official pages 2026-07-24) for: claude-opus-4-8, gpt-5.6-luna, gpt-5.6-sol  << UNVERIFIED: gemma4-ctx8k, qwen3.5-ctx8k -- do not publish their dollar figures

## PASS MATRIX (query class x tier)
  Q1_retrieval     | frontier: 3/3 | nano: 1/3 | qwen3.5-9.7b-q4: 3/3 | gemma4-12b-q4: 0/3
  Q2_analytical    | frontier: 3/3 | nano: 3/3 | qwen3.5-9.7b-q4: 0/3 | gemma4-12b-q4: 0/3
  Q3_synthesis     | frontier: 3/3 | nano: 3/3 | qwen3.5-9.7b-q4: 3/3 | gemma4-12b-q4: 3/3
  Q4_distractor    | frontier: 0/3 | nano: 1/2 (1 err) | qwen3.5-9.7b-q4: 0/3 | gemma4-12b-q4: 0/3
  Q5_quantitative  | frontier: 3/3 | nano: 3/3 | qwen3.5-9.7b-q4: 3/3 | gemma4-12b-q4: 3/3
  (tiers beyond frontier/nano are exploratory; the gate ignores them)

## CALIBRATION GATE (locked -- pre-registration section 3)
  Achievability : frontier passed 12/12 non-trap cells (needs >= 11; v1.3 accounting, Q4 excluded)  -> OK
  Frontier on Q4 (reported as a finding, not gated): 0/3
  Discrimination: nano failed 3/15 (needs >= 2)  -> OK
  >>> CALIBRATION PASS <<<

## NANO FAILURE DISTRIBUTION (Phase 0 prior: failures concentrate in Q4/Q5)
  Q1_retrieval    : 2 failed run(s)
  Q2_analytical   : 0 failed run(s)
  Q3_synthesis    : 0 failed run(s)
  Q4_distractor   : 1 failed run(s)
  Q5_quantitative : 0 failed run(s)

## FAILED CELLS
  Q4_distractor x frontier run 1: (a) rejects adding CHIL-005, (e) concludes the critical count remains 12 -- The candidate adds CHIL-005 (rubric requires rejection because health 52 is not below the critical threshold of 50) and 
  Q4_distractor x frontier run 2: a, e -- The candidate adds CHIL-005 despite its health of 52 being above the critical threshold of 50, which the rubric requires
  Q4_distractor x frontier run 3: (a) rejects adding CHIL-005, (e) concludes the critical count remains 12 -- The candidate adds CHIL-005 and concludes 13 critical assets, but the rubric requires rejecting CHIL-005 (health 52 not 
  Q1_retrieval x nano run 2: judge_parse_failure -- Checking rubric criteria against candidate.

(a) states count = 12 ✓
(b) cites all five: PUMP-003, HVAC-007, COMP-002, B
  Q1_retrieval x nano run 3: judge_parse_failure -- Let me check the rubric criteria.

(a) states critical count = 12: Yes.
(b) cites all five IDs PUMP-003, HVAC-007, COMP-
  Q4_distractor x nano run 1: no_answer -- 
  Q4_distractor x nano run 2: (a) rejects adding CHIL-005 -- The rubric requires rejecting CHIL-005 because health 52 is not below the critical threshold of 50, but the candidate ad
  Q2_analytical x qwen3.5-9.7b-q4 run 1: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- Candidate ranks BOIL-001 as #1, HVAC-007 as #2, and PUMP-003 as #3, violating the required ordering of PUMP-003 first an
  Q2_analytical x qwen3.5-9.7b-q4 run 2: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate ranks BOIL-001 first, HVAC-007 second, and PUMP-003 third, violating the required ordering of PUMP-003 fir
  Q2_analytical x qwen3.5-9.7b-q4 run 3: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate ranks BOIL-001 first, HVAC-007 second, and PUMP-003 third, violating the required order of PUMP-003 first 
  Q4_distractor x qwen3.5-9.7b-q4 run 1: no_answer -- 
  Q4_distractor x qwen3.5-9.7b-q4 run 2: no_answer -- 
  Q4_distractor x qwen3.5-9.7b-q4 run 3: no_answer -- 
  Q1_retrieval x gemma4-12b-q4 run 1: (a) states the critical asset count = 12 -- The candidate lists critical asset IDs including all five required (PUMP-003, HVAC-007, COMP-002, BOIL-001, PUMP-009), b
  Q1_retrieval x gemma4-12b-q4 run 2: (a) states the critical asset count = 12 -- The candidate cites all five required asset IDs (PUMP-003, HVAC-007, COMP-002, BOIL-001, PUMP-009) with no contradicting
  Q1_retrieval x gemma4-12b-q4 run 3: (a) states the critical asset count = 12 -- The candidate cites all five required asset IDs and no contradicting IDs, but it never states the critical asset count i
  Q2_analytical x gemma4-12b-q4 run 1: (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- Candidate names PUMP-003 first and HVAC-007 second correctly with valid quantitative signals and no fabricated numbers, 
  Q2_analytical x gemma4-12b-q4 run 2: (b) at least 2 of BOIL-001, COMP-002, GEN-004 are also named -- PUMP-003 and HVAC-007 are correctly first and second, but only BOIL-001 is named from the required set of three (BOIL-00
  Q2_analytical x gemma4-12b-q4 run 3: (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- PUMP-003 and HVAC-007 are correctly first and second with quantitative justification and no fabricated numbers, but only
  Q4_distractor x gemma4-12b-q4 run 1: (a), (d) -- The candidate adds CHIL-005 (violating rubric (a) which requires rejection because health 52 is above the threshold) and
  Q4_distractor x gemma4-12b-q4 run 2: (a) rejects adding CHIL-005, (d) rejects removing FAN-012, (e) concludes count remains 12 -- Candidate wrongly adds CHIL-005 (health 52, not critical) and wrongly removes FAN-012 (health 48 qualifies as critical),
  Q4_distractor x gemma4-12b-q4 run 3: (a) rejects adding CHIL-005, (d) rejects removing FAN-012, (e) critical count remains 12 -- The candidate adds CHIL-005 (rubric requires rejection since health 52 is above threshold) and removes FAN-012 (rubric r

## PER-TIER ECONOMICS (local models have no per-token price; latency is the cost)
  frontier    : pass 12/15 | mean $0.015261/query | 7.7s latency | 374 out-tokens
  nano        : pass 11/14 | mean $0.003119/query | 4.1s latency | 386 out-tokens
  qwen3.5-9.7b-q4: pass 9/15 | mean $0.000000/query | 335.0s latency | 4356 out-tokens
  gemma4-12b-q4: pass 6/15 | mean $0.000000/query | 279.5s latency | 1569 out-tokens

Mean judge COGS per cell: $0.017131
Cells re-adjudicated (fail-confirmation protocol, v1.1): 18 of 60
Full answers and per-cell data: phase0_raw.json
Author: Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026