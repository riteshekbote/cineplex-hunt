# Validated findings (running count 0)

- 2 lead(s) marked VALID at 2026-09-03 19:07:25 UTC
  - | Q4 Provable | **NO** | Probe `booking.cineplex.de/api/booking/{id}` returned HTTP 403 — endpoint blocked without valid session; AUTH_HELPED required |
  - **Verdict: HOLD** — Endpoint exists but 403 blocks unauthenticated testing. Needs valid test-account session to verify ownership validation. Reopen only with AUTH_HELPED and two-account proof showing 

- 3 lead(s) marked VALID at 2026-09-04 19:08:54 UTC
  - **Verdict: VALID**
  - | Q7 Reasonable triager? | Borderline — staging sometimes deprioritized, but env confusion is a valid finding class |
  - | 1 | GraphQL Introspection (prod POST) | **VALID** | 5.3 |
