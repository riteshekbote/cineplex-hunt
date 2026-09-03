# Hypotheses (ranked)

## RANKED HYPOTHESES 2026-09-02 21:39:17 UTC

## RANKED HYPOTHESES 2026-09-02 23:32:58 UTC

## RANKED HYPOTHESES 2026-09-03 01:26:17 UTC

## RANKED HYPOTHESES 2026-09-03 06:31:50 UTC

## RANKED HYPOTHESES 2026-09-03 11:42:25 UTC

## RANKED HYPOTHESES 2026-09-03 15:49:19 UTC
- [75] graphql-api.app.cineplex.de: GraphQL Introspection & Unauthorized Mutations on Production API (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://graphql-api.app.cineplex.de/ — Accept: application/json — body: `{"query":"{__schema{types{name fields{name}}}"}` — expect 200 with schema if
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized in directives
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized

## RANKED HYPOTHESES 2026-09-03 19:05:42 UTC
- [75] graphql-api.app.cineplex.de: GraphQL Introspection Enabled on Production API (from art/lead_nemotron3.txt)
- [70] graphql-api.app.cineplex.de: Production GraphQL introspection leakage (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://graphql-api.app.cineplex.de/ — Accept: application/json — Content-Type: application/json — body: {"query":"{__schema{types{name fields{name}}
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fie
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized in directives
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives

## RANKED HYPOTHESES 2026-09-03 21:46:44 UTC
- [75] graphql-api.app.cineplex.de: GraphQL Introspection & Hidden Mutations on Production API (from art/lead_nemotron3.txt)
- [70] graphql-api.app.cineplex.de: Production GraphQL introspection leakage (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://graphql-api.app.cineplex.de/ — Accept: application/json — Content-Type: application/json — body: {"query":"{__schema{types{name fields{name}}
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fie
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized in directives
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
