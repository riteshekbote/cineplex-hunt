# Validated findings (running count 0)

- 2 lead(s) marked VALID at 2026-09-03 19:07:25 UTC
  - | Q4 Provable | **NO** | Probe `booking.cineplex.de/api/booking/{id}` returned HTTP 403 — endpoint blocked without valid session; AUTH_HELPED required |
  - **Verdict: HOLD** — Endpoint exists but 403 blocks unauthenticated testing. Needs valid test-account session to verify ownership validation. Reopen only with AUTH_HELPED and two-account proof showing 

- 3 lead(s) marked VALID at 2026-09-04 19:08:54 UTC
  - **Verdict: VALID**
  - | Q7 Reasonable triager? | Borderline — staging sometimes deprioritized, but env confusion is a valid finding class |
  - | 1 | GraphQL Introspection (prod POST) | **VALID** | 5.3 |

- 2 lead(s) marked VALID at 2026-09-05 01:09:18 UTC
  - | Q4 Provable | No — requires valid session (AUTH_HELPED); probe confirms 403 |
  - | Q4 Provable | No — requires valid JWT; program forbids exposing customer PII during testing |

- 1 lead(s) marked VALID at 2026-09-05 05:51:22 UTC
  - | Q4 Provable | No — requires valid session (AUTH_HELPED) |

- 7 lead(s) marked VALID at 2026-09-06 18:14:31 UTC
  - | Q7 Reasonable triager accept? | **YES** — GraphQL introspection on production with WAF bypass (GET 403/POST 200) is a valid misconfiguration |
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | Q4 Provable non-invasively? | **NO** — requires valid JWT from login mutation (AUTH_HELPED) |
  - | Q4 Provable non-invasively? | **NO** — requires valid session (AUTH_HELPED) |
  - | GraphQL Introspection (Production) | **VALID** | 7.5 (High) |
  - | Staging GraphQL WAF Bypass | **VALID** | 6.5 (Medium) |

- 6 lead(s) marked VALID at 2026-09-07 22:16:31 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | Q2 Reachable? | AUTH_HELPED — requires valid JWT from login mutation |
  - | Q4 Provable? | NO — requires valid session + querying other users' bookings = PII exposure |
  - | 1 | Prod GraphQL Introspection | **VALID** | 5.3→8.1 | Report to bugs.olivermaicher.eu |
  - | 2 | Staging GraphQL Introspection + Env Confusion | **VALID** | 5.3→7.5 | Report to bugs.olivermaicher.eu |
