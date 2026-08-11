# AEQ GRID-2Q PHASE 0 -- CALIBRATION RESULTS
Run completed: 2026-07-24T20:30:34Z | Runs per cell: 3
Frontier: gpt-5.6-sol | Nano: gpt-5.6-luna | Judge: claude-opus-4-8
Pricing verified (official pages 2026-07-24) for: claude-haiku-4-5-20251001, claude-opus-4-8, gpt-5.6-luna, gpt-5.6-sol

## PASS MATRIX (query class x tier)
  Q1_retrieval     | frontier: 3/3 | nano: 3/3 | qwen7b: 3/3 | llama3b: 1/3 | anthropic:claude-haiku-4-5: 2/3
  Q2_analytical    | frontier: 3/3 | nano: 3/3 | qwen7b: 0/3 | llama3b: 0/3 | anthropic:claude-haiku-4-5: 0/3
  Q3_synthesis     | frontier: 3/3 | nano: 3/3 | qwen7b: 3/3 | llama3b: 0/3 | anthropic:claude-haiku-4-5: 0/3
  Q4_distractor    | frontier: 0/3 | nano: 1/3 | qwen7b: 0/3 | llama3b: 0/3 | anthropic:claude-haiku-4-5: 0/3
  Q5_quantitative  | frontier: 3/3 | nano: 3/3 | qwen7b: 0/3 | llama3b: 3/3 | anthropic:claude-haiku-4-5: 3/3
  (tiers beyond frontier/nano are exploratory; the gate ignores them)

## CALIBRATION GATE (locked -- pre-registration section 3)
  Achievability : frontier passed 12/12 non-trap cells (needs >= 11; v1.3 accounting, Q4 excluded)  -> OK
  Frontier on Q4 (reported as a finding, not gated): 0/3
  Discrimination: nano failed 2/15 (needs >= 2)  -> OK
  >>> CALIBRATION PASS <<<

## NANO FAILURE DISTRIBUTION (Phase 0 prior: failures concentrate in Q4/Q5)
  Q1_retrieval    : 0 failed run(s)
  Q2_analytical   : 0 failed run(s)
  Q3_synthesis    : 0 failed run(s)
  Q4_distractor   : 2 failed run(s)
  Q5_quantitative : 0 failed run(s)

## FAILED CELLS
  Q4_distractor x frontier run 1: (a) rejects adding CHIL-005, (e) concludes the critical count remains 12 -- The candidate adds CHIL-005 (health 52, not below the critical threshold of 50) and concludes a count of 13, violating r
  Q4_distractor x frontier run 2: a, e -- The candidate adds CHIL-005 rather than rejecting it (rubric requires rejection because health 52 is not below the criti
  Q4_distractor x frontier run 3: (a) rejects adding CHIL-005, (e) concludes critical count remains 12 -- The candidate adds CHIL-005 despite its health of 52 being above the critical threshold of 50, and concludes a count of 
  Q4_distractor x nano run 2: (a) rejects adding CHIL-005, (e) concludes the critical count remains 12 -- The candidate adds CHIL-005 (rubric requires rejecting it because health 52 is not below the critical threshold of 50) a
  Q4_distractor x nano run 3: a, e -- The candidate accepts adding CHIL-005 (health 52) despite the rubric requiring rejection because 52 is not below the cri
  Q2_analytical x qwen7b run 1: (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- PUMP-003 and HVAC-007 are correctly first and second, and BOIL-001 is named, but only one of the three required assets (
  Q2_analytical x qwen7b run 2: (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- PUMP-003 and HVAC-007 are correctly ordered first and second with quantitative justification and no fabricated numbers, 
  Q2_analytical x qwen7b run 3: (b) at least 2 of BOIL-001, COMP-002, GEN-004 are also named -- PUMP-003 is first and HVAC-007 second (a satisfied), justification cites quantitative signals with no fabricated numbers
  Q4_distractor x qwen7b run 1: a, d, e -- Candidate recommends adding CHIL-005 (should reject), recommends removing FAN-012 (should retain, and misstates FAN-012 
  Q4_distractor x qwen7b run 2: a, d, e, f -- Candidate recommends adding CHIL-005 (rubric requires rejecting since health 52 is not below 50), incorrectly states FAN
  Q4_distractor x qwen7b run 3: a, d, e, f -- Candidate recommends adding CHIL-005 (rubric requires rejection), recommends removing FAN-012 (rubric requires retaining
  Q5_quantitative x qwen7b run 1: a, b, c, e -- The candidate gives $58,500 and $27,900 with ratio 2.10, none matching the required figures; the numbers appear fabricat
  Q5_quantitative x qwen7b run 2: a, b, c, e -- The candidate states $58,500 and $27,900 with a ratio of 2.10, all of which are fabricated and incorrect; correct values
  Q5_quantitative x qwen7b run 3: a, b, c, e -- The candidate gives $58,500 and $27,900 with ratio 2.10, none of which match the required figures ($9,360, ~$5,657, ~1.6
  Q1_retrieval x llama3b run 2: (a) states the critical asset count = 12 -- Candidate lists all five required asset IDs with no contradicting data, but never states the critical asset count of 12.
  Q1_retrieval x llama3b run 3: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradicting data, but never states the critical asset count of
  Q2_analytical x llama3b run 1: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate omits PUMP-003 and HVAC-007 entirely, failing to name the top two required priorities.
  Q2_analytical x llama3b run 2: (a) top priority is PUMP-003 AND second priority is HVAC-007, (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- The candidate omits PUMP-003 and HVAC-007 entirely, failing the required top-two ordering; it names BOIL-001, COMP-002, 
  Q2_analytical x llama3b run 3: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate omits PUMP-003 and HVAC-007 entirely, starting instead with BOIL-001, so criterion (a) fails.
  Q3_synthesis x llama3b run 1: c -- The claim that the action reduces critical maintenance cost 'from $86,400 to $0' is a fabricated statistic unsupported b
  Q3_synthesis x llama3b run 2: c -- The claim that inspecting PUMP-003 would reduce critical asset maintenance cost 'from $86,400 to $0' is a fabricated sta
  Q3_synthesis x llama3b run 3: c -- The candidate fabricates a claim that maintenance cost would be reduced from $86,400 to $0, which is unsupported and fal
  Q4_distractor x llama3b run 1: (c) rejects adding PUMP-014, (d) rejects removing FAN-012, (e) critical count remains 12, (f) no fabricated numbers -- Candidate wrongly adds PUMP-014, wrongly removes FAN-012, ends with a fabricated 10-asset list, and misstates CHIL-005 r
  Q4_distractor x llama3b run 2: a, c, d, e -- Candidate contradicts itself on CHIL-005 (says don't add then lists it), wrongly adds PUMP-014 (health 58 not critical),
  Q4_distractor x llama3b run 3: (a) rejects adding CHIL-005, (c) rejects adding PUMP-014, (d) rejects removing FAN-012, (e) critical count remains 12 -- The candidate adds PUMP-014, recommends removing FAN-012, contradicts itself on CHIL-005, and produces an incorrect fina
  Q1_retrieval x anthropic:claude-haiku-4-5 run 3: Missing required critical asset ID PUMP-009. Incorrectly states that 8 critical assets have overdue maintenance; evidence specifies 8 assets portfolio-wide and 5 overdue critical assets. -- The answer gives the correct total of 12 but omits PUMP-009 and contradicts the overdue-maintenance count for critical a
  Q2_analytical x anthropic:claude-haiku-4-5 run 1: (d) no fabricated numbers -- Although the required ordering, additional assets, and quantitative justification are present, the answer falsely attrib
  Q2_analytical x anthropic:claude-haiku-4-5 run 2: (d) no fabricated numbers -- The $46,800 figure applies to the five overdue critical assets, not the candidate's listed five, which include warning-l
  Q2_analytical x anthropic:claude-haiku-4-5 run 3: (d) no fabricated numbers -- The answer incorrectly attributes the $46,800 figure to its five listed assets, including CHIL-005, whereas the evidence
  Q3_synthesis x anthropic:claude-haiku-4-5 run 1: (c) no fabricated statistics -- The claim that five high-risk assets are predicted to fail within 60–90 days overstates the evidence, which only identif
  Q3_synthesis x anthropic:claude-haiku-4-5 run 2: (c) no fabricated statistics -- The response inaccurately states that all eight overdue assets represent $46,800 and that five are predicted to fail, wh
  Q3_synthesis x anthropic:claude-haiku-4-5 run 3: (c) no fabricated statistics -- The response mislabels $86,400 as a maintenance budget and $46,800 as a maintenance backlog, and unsupportedly claims th
  Q4_distractor x anthropic:claude-haiku-4-5 run 1: (a) rejects adding CHIL-005 because health 52 is not below the critical threshold of 50, (e) concludes the critical count remains 12 -- The candidate incorrectly adds CHIL-005 despite its noncritical health score of 52 and consequently reports 13 critical 
  Q4_distractor x anthropic:claude-haiku-4-5 run 2: (a) rejects adding CHIL-005 because health 52 is not below the critical threshold of 50, despite the urgent field note, (e) concludes the critical count remains 12 -- The candidate incorrectly adds CHIL-005 and concludes there will be 13 critical assets rather than retaining the 12-asse
  Q4_distractor x anthropic:claude-haiku-4-5 run 3: (a) Candidate recommends adding CHIL-005, but it must reject adding it because health 52 is not below the critical threshold of 50 despite the urgent field note. (b) Candidate incorrectly frames GEN-009 as a removal from the critical list rather than rejecting its proposed addition because it is decommissioned and inactive. -- Although it correctly rejects PUMP-014, retains FAN-012, and states a count of 12, it wrongly adds CHIL-005 and reaches 

## PER-TIER ECONOMICS (local models have no per-token price; latency is the cost)
  frontier    : pass 12/15 | mean $0.015159/query | 6.9s latency | 371 out-tokens
  nano        : pass 13/15 | mean $0.002965/query | 5.6s latency | 360 out-tokens
  qwen7b      : pass 6/15 | mean $0.000000/query | 18.6s latency | 206 out-tokens
  llama3b     : pass 4/15 | mean $0.000000/query | 8.1s latency | 202 out-tokens
  anthropic:claude-haiku-4-5: pass 5/15 | mean $0.002573/query | 3.6s latency | 325 out-tokens

Mean judge COGS per cell: $0.020420
Cells re-adjudicated (fail-confirmation protocol, v1.1): 35 of 75
Full answers and per-cell data: phase0_raw.json
Author: Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026