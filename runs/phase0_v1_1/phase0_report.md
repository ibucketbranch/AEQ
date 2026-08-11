# AEQ GRID-2Q PHASE 0 -- CALIBRATION RESULTS
Run completed: 2026-07-24T04:23:54Z | Runs per cell: 3
Frontier: gpt-5.2 | Nano: gpt-5-nano | Judge: claude-opus-4-8
Pricing verified against official pages: False  << VERIFY BEFORE PUBLICATION

## PASS MATRIX (query class x tier)
  Q1_retrieval     | frontier: 3/3 | nano: 3/3
  Q2_analytical    | frontier: 3/3 | nano: 1/3
  Q3_synthesis     | frontier: 3/3 | nano: 2/3
  Q4_distractor    | frontier: 2/3 | nano: 0/2
  Q5_quantitative  | frontier: 3/3 | nano: 3/3

## CALIBRATION GATE (locked -- pre-registration section 3)
  Achievability : frontier passed 14/15 (needs >= 13)  -> OK
  Discrimination: nano failed 5/15 (needs >= 2)  -> OK
  >>> CALIBRATION PASS <<<

## NANO FAILURE DISTRIBUTION (Phase 0 prior: failures concentrate in Q4/Q5)
  Q1_retrieval    : 0 failed run(s)
  Q2_analytical   : 2 failed run(s)
  Q3_synthesis    : 1 failed run(s)
  Q4_distractor   : 2 failed run(s)
  Q5_quantitative : 0 failed run(s)

## FAILED CELLS
  Q4_distractor x frontier run 1: (a) rejects adding CHIL-005, (e) concludes the critical count remains 12 -- The candidate adds CHIL-005 despite its health of 52 being above the critical threshold of 50, and concludes the count b
  Q2_analytical x nano run 1: no_answer -- 
  Q2_analytical x nano run 3: (b) at least 2 of BOIL-001, COMP-002, GEN-004 are also named -- PUMP-003 and HVAC-007 are correctly ordered first and second, but only BOIL-001 is named as a prioritized asset; COMP-00
  Q3_synthesis x nano run 2: c -- The candidate states 'Across 60 analyzed assets' but the evidence says 50 assets were analyzed, which is a fabricated st
  Q4_distractor x nano run 1: (d) rejects REMOVING FAN-012, (e) concludes the critical count remains 12 -- The candidate wrongly recommends removing FAN-012 (health 48 is critical) and concludes the count is 11, violating crite
  Q4_distractor x nano run 2: no_answer -- 
  Q4_distractor x nano run 3: no_answer -- 

Mean judge COGS per cell: $0.016852
Cells re-adjudicated (fail-confirmation protocol, v1.1): 5 of 30
Full answers and per-cell data: phase0_raw.json
Author: Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026