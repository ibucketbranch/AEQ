# AEQ GRID-2Q EXPERIMENT -- PRE-REGISTRATION v1.4.2 (HARNESS-CLIENT NOTE)

**Amended:** 2026-07-29 (UTC), before any counted local-SUT cells executed.
**Author:** Michael Valderrama | AI Agent Architect | Independent R&D (c) 2026. Drafted and registered by his coding agent at his direction.
**Supersedes:** v1.4.1 for the harness HTTP client timeout only. Roster, prior, serving config, and all measurement rules carry forward UNCHANGED.

The harness's per-request client timeout for system-under-test calls was raised from 300 s to 900 s. Server logs from the aborted v1.4.1 attempt show local-SUT requests completing successfully in 3 to 5 minutes under host load; one request was clipped by the client at exactly 300 s mid-generation and would have been miscounted as a zero-output failure. The timeout is an operational client setting, not a rubric, gate, or scoring rule. Latency remains reported as measured (v1.4 prior, item 4). Judge-call timeout is unchanged at 300 s.

---
*Terminology compliance: this document uses "AI agent(s)" exclusively.*
