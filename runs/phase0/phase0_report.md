# AEQ GRID-2Q PHASE 0 -- CALIBRATION RESULTS
Run completed: 2026-07-24T01:38:33Z | Runs per cell: 3
Frontier: gpt-5.2 | Nano: gpt-5-nano | Judge: claude-opus-4-8
Pricing verified against official pages: False  << VERIFY BEFORE PUBLICATION

## PASS MATRIX (query class x tier)
  Q1_retrieval     | frontier: 3/3 | nano: 2/3
  Q2_analytical    | frontier: 3/3 | nano: 2/3
  Q3_synthesis     | frontier: 3/3 | nano: 3/3
  Q4_distractor    | frontier: 3/3 | nano: 3/3
  Q5_quantitative  | frontier: 3/3 | nano: 3/3

## CALIBRATION GATE (locked -- pre-registration section 3)
  Achievability : frontier passed 15/15 (needs >= 13)  -> OK
  Discrimination: nano failed 2/15 (needs >= 2)  -> OK
  >>> CALIBRATION PASS <<<

## NANO FAILURE DISTRIBUTION (Phase 0 prior: failures concentrate in Q4/Q5)
  Q1_retrieval    : 1 failed run(s)
  Q2_analytical   : 1 failed run(s)
  Q3_synthesis    : 0 failed run(s)
  Q4_distractor   : 0 failed run(s)
  Q5_quantitative : 0 failed run(s)

## FAILED CELLS
  Q1_retrieval x nano run 2: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradicting data, but never explicitly states the critical ass
  Q2_analytical x nano run 2: (b) at least 2 of BOIL-001, COMP-002, GEN-004 are also named -- Candidate names BOIL-001 and COMP-002 as priorities, satisfying (b) with two of the three; PUMP-003 and HVAC-007 are ran

Mean judge COGS per cell: $0.013276
Full answers and per-cell data: phase0_raw.json
Author: Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026