# Re-adjudication note, 2026-07-30

Two nano Q1_retrieval cells in phase0_report.md carry failed_criteria = judge_parse_failure. Their stored answers were re-adjudicated on 2026-07-30 with the same judge (claude-opus-4-8), same rubric, same reference answer, per the v1.1 fail-confirmation protocol. Raw verdicts in readjudication_raw.json.

- Run 2: the judge's output failed to parse a second time, with the same free-form checkmark formatting. Deterministic judge-formatting artifact. The cell remains excluded from substantive counts and is reported as an artifact.
- Run 3: parsed cleanly on re-read. Substantive FAIL on criterion (c): the candidate answer asserts "6 critical assets are not identified," contradicting the evidence. The cell's FAIL stands as a real failure.

Corrected nano Q1 reading: 1 pass, 1 substantive fail, 1 artifact. The discrimination gate (nano fails >= 2 of 15 post fail-confirmation) held before this note and holds after it. No local-SUT cell is affected; local cells involve no metered API on the SUT side.

One additional artifact stands as reported: nano Q4_distractor run 1 returned zero output tokens (transient API error, no answer produced, no judge involvement). It cannot be re-adjudicated because there is no answer to judge; it is excluded from substantive counts.

Latency context for this run: local-SUT latencies (mean 335.0 s qwen3.5-ctx8k, 279.5 s gemma4-ctx8k) were measured under shared host load (a second agent system resident on the same 16 GB host for part of the run, plus one host reboot mid-run, auto-recovered by the watchdog). Pass/fail results are temperature-0 and unaffected; treat latencies as an upper bound, not a clean benchmark.
