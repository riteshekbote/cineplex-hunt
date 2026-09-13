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

- 2 lead(s) marked VALID at 2026-09-10 11:49:47 UTC
  - **Verdict: HOLD** — JWKS 404 blocks passive verification. Requires valid credentials for login flow. Reopen when AUTH_HELPED session available.
  - | Q4 Provable non-invasively? | **NO** — requires valid JWT + querying other users' data = PII exposure, which program explicitly forbids |

- 5 lead(s) marked VALID at 2026-09-11 11:50:08 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | Q7 Reasonable triager | MAYBE — the proof is structural (typed error confirms resolver processed ID without auth) but no real user record was fetched. A strict triager may demand at least one valid-
  - | 1 | GraphQL introspection (prod) | **VALID** | 5.3 |
  - | 2 | Staging GraphQL env confusion | **VALID** | 6.5 |

- 2 lead(s) marked VALID at 2026-09-11 15:53:55 UTC
  - | 1 | GraphQL introspection (prod) | **VALID** | 5.3 | Ready to report |
  - | 2 | Staging GraphQL env confusion | **VALID** | 6.5 | Ready to report |

- 4 lead(s) marked VALID at 2026-09-12 01:34:53 UTC
  - | Q7 Reasonable triager? | **YES** — production GraphQL introspection with WAF bypass exposing booking/payment/admin mutations is a valid misconfiguration |
  - **Verdict: VALID**
  - | Q7 Reasonable triager? | **HOLD** — structural proof is strong (control-complete: 4 omissions vs 4 firing gates), but strict triager will demand at least one valid cross-user PII fetch before accept
  - | 1 | Production GraphQL Introspection (schema exposure + WAF bypass) | **VALID** | 5.3 | bugs.olivermaicher.eu |

- 11 lead(s) marked VALID at 2026-09-13 12:03:51 UTC
  - | Q5 Novel/unreported? | YES — prior triages at 2026-09-06/07/10/11/12 all marked VALID; not on any rejected list |
  - **Verdict: VALID**
  - | Q7 Reasonable triager? | YES — staging env exposed to public internet with identical prod schema is a valid finding |
  - **Verdict: VALID**
  - | Q3 Real impact? | YES — if confirmed with valid data, cross-user PII disclosure (email, phone, address, tickets, orders, subscriptions, invoices) |
  - | Q7 Reasonable triager? | HOLD — structural proof is strong (control-complete: 4 auth-omission resolvers vs 4 firing-gate resolvers), but strict triager will demand at least one valid cross-user PII 
  - | Q2 Reachable? | PARTIAL — GraphQL host is reachable; JWKS endpoint returns 404 (no passive key fetch); login mutation exists but requires valid credentials |
  - | Q4 Provable non-invasively? | NO — requires: (1) valid credentials to trigger login mutation and capture JWT, (2) decode JWT header to confirm RS256, (3) forge HS256 with public key, (4) replay to p
  - | 1 | Prod GraphQL Introspection | **VALID** | 5.3 | Report to bugs.olivermaicher.eu |
  - | 2 | Staging GraphQL Introspection + Env Confusion | **VALID** | 6.5 | Report (bundle with #1) |
  - **VALID leads ready for report: 2** (Leads 1+2). Recommend bundling into a single report covering production + staging GraphQL introspection with WAF bypass.

- 11 lead(s) marked VALID at 2026-09-13 23:14:16 UTC
  - | Q7 Reasonable triager? | **YES** — GraphQL introspection enabled in production with WAF method-gate bypass is a valid misconfiguration; prior triages at 09-04, 09-06, 09-07, 09-10, 09-11, 09-12, 09-
  - **Verdict: VALID**
  - | Q7 Reasonable triager? | **YES** — staging environment exposed to internet with same or expanded production schema is valid; prior triages at 09-04, 09-06, 09-07, 09-10, 09-11, 09-12, 09-13 all mark
  - **Verdict: VALID**
  - | Q4 Provable? | **NO** — JWKS 404 blocks passive verification; requires valid credentials to login via GraphQL mutation, capture JWT, decode header, forge HS256, replay. AUTH_HELPED required. Program
  - | Q2 Reachable? | **PARTIAL** — GraphQL endpoint reachable; resolvers confirmed in schema; but cross-user query requires valid JWT | ⚠️ |
  - | Q4 Provable? | **NO** — requires valid JWT + querying other users' data = PII exposure, which program explicitly forbids during testing | ❌ |
  - | Q7 Reasonable triager? | **HOLD** — structural proof from schema analysis is strong (4 auth-omission resolvers vs 4 firing-gate resolvers), but strict triager demands at least one valid cross-user P
  - | 1 | Prod GraphQL Introspection (WAF bypass) | **VALID** | 7.5 High | bugs.olivermaicher.eu |
  - | 2 | Staging GraphQL Introspection + Env Confusion | **VALID** | 6.5 Medium | bugs.olivermaicher.eu (bundle w/ #1) |
  - **Valid leads ready for report: 2** (Leads 1+2). Recommend bundling into a single report covering production + staging GraphQL introspection with WAF method-gate bypass (GET 403 / POST 200).
