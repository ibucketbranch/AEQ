# AEQ GRID-2Q PHASE 0 -- CALIBRATION RESULTS
Run completed: 2026-07-24T05:32:26Z | Runs per cell: 3
Frontier: gpt-5.2 | Nano: gpt-5-nano | Judge: claude-opus-4-8
Pricing verified against official pages: False  << VERIFY BEFORE PUBLICATION

## PASS MATRIX (query class x tier)
  Q1_retrieval     | frontier: 3/3 | nano: 3/3 | qwen7b: 3/3 | llama3b: 0/3 | anthropic:claude-haiku-4-5: 1/3
  Q2_analytical    | frontier: 3/3 | nano: 1/3 | qwen7b: 0/3 | llama3b: 0/3 | anthropic:claude-haiku-4-5: 2/3
  Q3_synthesis     | frontier: 3/3 | nano: 3/3 | qwen7b: 3/3 | llama3b: 0/3 | anthropic:claude-haiku-4-5: 1/3
  Q4_distractor    | frontier: 2/3 | nano: 0/0 | qwen7b: 0/3 | llama3b: 0/3 | anthropic:claude-haiku-4-5: 0/3
  Q5_quantitative  | frontier: 3/3 | nano: 3/3 | qwen7b: 0/3 | llama3b: 3/3 | anthropic:claude-haiku-4-5: 3/3
  (tiers beyond frontier/nano are exploratory; the gate ignores them)

## CALIBRATION GATE (locked -- pre-registration section 3)
  Achievability : frontier passed 14/15 (needs >= 13)  -> OK
  Discrimination: nano failed 2/15 (needs >= 2)  -> OK
  >>> CALIBRATION PASS <<<

## NANO FAILURE DISTRIBUTION (Phase 0 prior: failures concentrate in Q4/Q5)
  Q1_retrieval    : 0 failed run(s)
  Q2_analytical   : 2 failed run(s)
  Q3_synthesis    : 0 failed run(s)
  Q4_distractor   : 0 failed run(s)
  Q5_quantitative : 0 failed run(s)

## FAILED CELLS
  Q4_distractor x frontier run 1: (a) rejects adding CHIL-005 because health 52 is not below threshold, (e) concludes critical count remains 12 -- The candidate adds CHIL-005 (health 52 is above the critical threshold of 50, so it should be rejected) and concludes th
  Q2_analytical x nano run 1: judge_parse_failure -- Checking rubric (b): needs at least 2 of BOIL-001, COMP-002, GEN-004. Candidate names BOIL-001 as a priority, and mentio
  Q2_analytical x nano run 3: no_answer -- 
  Q4_distractor x nano run 1: no_answer -- 
  Q4_distractor x nano run 2: no_answer -- 
  Q4_distractor x nano run 3: no_answer -- 
  Q2_analytical x qwen7b run 1: (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- PUMP-003 first and HVAC-007 second in order (a met), justification cites quantitative signals (c met), no fabricated num
  Q2_analytical x qwen7b run 2: (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- PUMP-003 and HVAC-007 are correctly ranked first and second and BOIL-001 is named with valid quantitative justification,
  Q2_analytical x qwen7b run 3: (b) at least 2 of BOIL-001, COMP-002, GEN-004 named -- PUMP-003 first and HVAC-007 second are correct with quantitative justification and no fabricated numbers, but only BOIL-
  Q4_distractor x qwen7b run 1: a, d, e -- The candidate recommends adding CHIL-005 (should reject, health 52 not critical), recommends removing FAN-012 (should ke
  Q4_distractor x qwen7b run 2: a, d, e -- The candidate recommends adding CHIL-005 (rubric requires rejection), recommends removing FAN-012 (rubric requires keepi
  Q4_distractor x qwen7b run 3: (a) rejects adding CHIL-005, (d) rejects removing FAN-012, (e) concludes count remains 12, (f) no fabricated numbers -- The candidate recommends adding CHIL-005 and removing FAN-012 (stating its health 48 is 'above threshold of 50', which i
  Q5_quantitative x qwen7b run 1: a, b, c, e -- Candidate states $58,500 and $27,900 with a 2.10 ratio, none of which match the required $9,360, $5,657, and 1.65x figur
  Q5_quantitative x qwen7b run 2: a, b, c, e -- The candidate states $58,500 and $27,900 with a ratio of 2.10x, all of which are wrong; correct values are $9,360, ~$5,6
  Q5_quantitative x qwen7b run 3: a, b, c, e -- Candidate gives $58,500 and $27,900 averages with ratio 2.10, none matching the required $9,360, $5,657, and 1.65x figur
  Q1_retrieval x llama3b run 1: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradicting data, but never states that there are 12 critical 
  Q1_retrieval x llama3b run 2: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradicting data, but fails to state the critical asset count 
  Q1_retrieval x llama3b run 3: (a) states the critical asset count = 12 -- The candidate lists all five required asset IDs with no contradicting data, but never states the critical asset count of
  Q2_analytical x llama3b run 1: (a) top priority is PUMP-003 AND second priority is HVAC-007 -- The candidate omits PUMP-003 and HVAC-007 entirely, failing the required top-two ordering.
  Q2_analytical x llama3b run 2: (a) top priority is PUMP-003 AND second priority is HVAC-007, in that order -- The candidate omits PUMP-003 and HVAC-007 entirely, listing BOIL-001 as top priority, violating criterion (a).
  Q2_analytical x llama3b run 3: (a) top priority PUMP-003 then HVAC-007 -- The candidate omits PUMP-003 and HVAC-007 entirely, failing to name the required top two priorities in order.
  Q3_synthesis x llama3b run 1: c -- The claim that this action reduces annual maintenance cost from $86,400 to $0 is a fabricated statistic not supported by
  Q3_synthesis x llama3b run 2: c -- The claim that this action reduces annual maintenance cost from $86,400 to $0 is a fabricated statistic unsupported by t
  Q3_synthesis x llama3b run 3: c -- The claim that this action reduces annual maintenance cost from $86,400 to $0 is a fabricated/unsupported statistic, as 
  Q4_distractor x llama3b run 1: a, c, d, e, f -- The candidate contradicts itself on CHIL-005 (text rejects but list adds it), wrongly recommends adding PUMP-014 (health
  Q4_distractor x llama3b run 2: c, d, e, f -- The candidate wrongly adds PUMP-014 (health 58) to the critical list, wrongly agrees to remove FAN-012 (active, health 4
  Q4_distractor x llama3b run 3: c, d, e -- The candidate incorrectly adds PUMP-014 (health 58, not critical), wrongly agrees to remove FAN-012 (active health 48, w
  Q1_retrieval x anthropic:claude-haiku-4-5 run 1: (c) contains no asset IDs or counts contradicting the evidence -- While it correctly states there are 12 critical assets and includes all five required IDs, it incorrectly claims 8 criti
  Q1_retrieval x anthropic:claude-haiku-4-5 run 2: (b) cites ALL FIVE of these asset IDs: PUMP-003, HVAC-007, COMP-002, BOIL-001, PUMP-009 -- The answer correctly states there are 12 critical assets and does not contradict evidence, but it omits PUMP-009 from th
  Q2_analytical x anthropic:claude-haiku-4-5 run 1: (d) no fabricated numbers -- Meets ordering (PUMP-003 then HVAC-007), includes BOIL-001 and COMP-002, and cites quantitative signals, but fabricates 
  Q3_synthesis x anthropic:claude-haiku-4-5 run 1: (d) response is at most 250 words -- Meets (a), (b), (c), and (e) with evidence-backed risk/decline framing and focus on PUMP-003/overdue backlog, but the re
  Q3_synthesis x anthropic:claude-haiku-4-5 run 2: d -- Candidate meets (a), (b), (c), and (e) using only evidenced assets/stats and focusing on overdue high-risk items, but it
  Q4_distractor x anthropic:claude-haiku-4-5 run 1: a, e, f -- Candidate incorrectly adds CHIL-005 despite health 52 not meeting the <50 critical threshold, concludes the critical cou
  Q4_distractor x anthropic:claude-haiku-4-5 run 2: a, e -- Candidate incorrectly recommends adding CHIL-005 despite health 52 being above the critical threshold, and concludes the
  Q4_distractor x anthropic:claude-haiku-4-5 run 3: a, e -- Candidate incorrectly recommends adding CHIL-005 despite health 52 not meeting the critical (<50) threshold, and therefo

## PER-TIER ECONOMICS (local models have no per-token price; latency is the cost)
  frontier    : pass 14/15 | mean $0.005282/query | 4.3s latency | 276 out-tokens
  nano        : pass 10/12 | mean $0.000897/query | 12.7s latency | 2143 out-tokens
  qwen7b      : pass 6/15 | mean $0.000000/query | 11.5s latency | 206 out-tokens
  llama3b     : pass 3/15 | mean $0.000000/query | 6.0s latency | 202 out-tokens
  anthropic:claude-haiku-4-5: pass 7/15 | mean $0.002613/query | 3.8s latency | 333 out-tokens

Mean judge COGS per cell: $0.016856
Cells re-adjudicated (fail-confirmation protocol, v1.1): 31 of 75
Full answers and per-cell data: phase0_raw.json
Author: Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026