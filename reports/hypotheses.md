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

## RANKED HYPOTHESES 2026-09-03 23:48:00 UTC
- [95] graphql-api.app.cineplex.de: GraphQL Introspection Enabled on Production — Full Schema + Dangerous Mutations Exposed (from art/lead_nemotron3.txt)
- [45] api.cineplex.de: JWT alg confusion / weak signing on auth API (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fie
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://graphql-api.app.cineplex.de/ — Accept: application/json — Content-Type: application/json — Authorization: Bearer <valid_jwt_from_login> — bo
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives

## RANKED HYPOTHESES 2026-09-04 02:43:23 UTC
- [95] graphql-api.app.cineplex.de: GraphQL Introspection Enabled on Production — Full Schema + Dangerous Mutations Exposed (from art/lead_nemotron3.txt)
- [62] data-9fc27eb430.cineplex.de: Undocumented API surface / relay-forwarding SSRF primitive on franchise relay (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only introspectio
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://graphql-api.app.cineplex.de/ — Accept: application/json — Content-Type: application/json — Authorization: Bearer <valid_jwt_from_login> — bo
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but auth.cineplex.de/.wel
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-04 07:26:39 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: {"query":"mutation{login(email:\"test@test.de\",password:\"test\"){jwt
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-04 12:20:37 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- [68] data-9fc27eb430.cineplex.de: Relay metrics endpoint discloses internal service topology / Prometheus stats (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cinepl
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: {"query":"mutation{login(email:\"test@test.de\",password:\"test\"){jwt
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but auth.cineplex.de/.wel
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114 bytes — second authless 200 surface; content unexamined; not in REJECTED
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-04 16:31:26 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- [72] data-9fc27eb430.cineplex.de: Relay /metrics endpoint discloses internal service topology or Prometheus stats (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cinepl
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 115 bytes — second authless 200 surface; content unexamined; not in REJECTED
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but auth.cineplex.de/.wel
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114 bytes — second authless 200 surface; content unexamined; not in REJECTED
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-04 19:10:50 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- [72] data-9fc27eb430.cineplex.de: Relay /metrics endpoint discloses internal service topology or Prometheus stats (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cinepl
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 115 bytes — second authless 200 surface; content unexamined; not in REJECTED
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114 bytes — second authless 200 surface; content unexamined; not in REJECTED
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-04 21:34:53 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with valid JWT (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: POST https://graphql-api.app.staging.cineplex.de/ — Header `Content-Type: application/json` — Body `{"query":"{__schema{queryType{name}}}"}` — read-only 
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-04 23:18:56 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- [72] graphql-api.app.cineplex.de: Testing-only confirmation-code oracle / forced-delete shipped to production GraphQL (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-05 01:05:23 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- [62] graphql-api.app.staging.cineplex.de: Staging GraphQL mirrors prod destructive mutation surface with no network gate (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: request program consent + two disposable sandbox accounts from bugs.olivermaicher.eu — then (a) staging-only validation of increaseUserTestingStatus/send
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-05 05:51:12 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- [55] graphql-api.app.couat.cineplex.de: couat GraphQL accepts introspection POST and exposes schema differing from prod/staging (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-05 09:56:26 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-05 13:18:34 UTC
- [85] graphql-api.app.cineplex.de: Production GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_bigpickle.txt)
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Request program consent + two disposable sandbox accounts from bugs.olivermaicher.eu for staging-only testing of testing_* resolvers and prod two-account
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-05 16:13:27 UTC
- [85] graphql-api.app.cineplex.de: Production GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_bigpickle.txt)
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Request program consent + two disposable sandbox accounts (or staging admin/test creds) from bugs.olivermaicher.eu to enable staged verification of the t
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps)
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: /metrics body now examined and fully understood — internal IOMB broker architecture (mode IOMB, writer que
- LEARN: REJECTED relay_broker_saturation @ data-9fc27eb430.cineplex.de: 273.9M queued messages over 30k capacity is infra saturation with no exploitable authless manipu
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope — reaffirmed for /metrics infra disclosure.
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJE
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope

## RANKED HYPOTHESES 2026-09-05 18:29:20 UTC
- [85] graphql-api.app.cineplex.de: GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (from art/lead_nemotron3.txt)
- [60] graphql-api.app.staging.cineplex.de: Staging GraphQL WAF method-gate bypass mirrors confirmed prod POST introspection (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — body {"query":"{__schema{queryType{name}}}"} — read-only schema intr
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://api.cineplex.de/graphql — Content-Type: application/json — body: {"query":"{__schema{mutationType{fields{name}}}"}} — read-only introspectio
- LEARN: `/metrics` body fully understood — descriptive infra only (IOMB broker stats), not reportable alone
- LEARN: `relay_broker_saturation` REJECTED — 273.9M queued over 30k capacity is infra saturation with no exploitable authless manipulation surface
- LEARN: ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 1
- LEARN: ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUM
- LEARN: ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passi
- LEARN: ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
- LEARN: ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 115 bytes — second authless 200 surface; content examined: internal IOMB bro
- LEARN: REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only l
- LEARN: ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
- LEARN: REJECTED relay_broker_saturation @ data-9fc27eb430.cineplex.de: 273.9M queued messages over 30k capacity is infra saturation with no exploitable authless manipu
- LEARN: REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot pass
- LEARN: REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
- LEARN: REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
- LEARN: REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
- LEARN: REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
