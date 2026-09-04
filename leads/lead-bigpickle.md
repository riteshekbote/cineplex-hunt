## 2026-09-03 15:41:59 UTC [target] (model bigpickle)
[NEW] api.cineplex.de - Host in inventory, no prior probes
[CHANGED] Target is now "api" per current state
[NEW] graphql-api.app.cineplex.de, graphql-api.app.staging.cineplex.de - GraphQL endpoints in inventory
## 2026-09-03 19:03:44 UTC [target] (model bigpickle)
[PRIO] graphql-api.app.cineplex.de,8.5,0.25(9)+0.25(8)+0.15(10,GraphQL)+0.15(9,no-auth introspect)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] api.cineplex.de,7.5,0.25(7,untested)+0.25(9,core API)+0.15(9,REST/JWT)+0.15(8,likely open)+0.10(8,cloud)+0.10(6,fresh)
[PRIO] graphql-api.app.staging.cineplex.de,6.5,0.25(5,staging)+0.25(6)+0.15(10,GraphQL)+0.15(9)+0.10(7)+0.10(5)
[HYP] Production GraphQL introspection leakage
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 70
reasoning: Endpoint not in any REJECTED class; introspection is a known high-value passive check; staging/couat siblings exist suggesting shared GraphQL infra with potential env confusion
evidence_needed: 200 response returning __schema types/fields
verify_steps: (1) GET https://graphql-api.app.cineplex.de/ with Accept: application/json; (2) POST same with body {"query":"{__schema{types{name fields{name}}}}"}; (3) if blocked, POST query for a single known field to fingerprint resolver names
impact: Full API schema disclosure enabling targeted IDOR/BOLA and mutation attacks; medium
testability: PASSIVE
[HYP] JWT alg confusion / weak signing on auth API
class: AUTH
asset: api.cineplex.de
confidence: 45
reasoning: New, untested host; sibling auth.cineplex.de prioritizes JWT alg/key confusion per directives; api.cineplex.de likely issues/validates tokens for mobile/app clients
evidence_needed: token accepted with alg=none or HS256 with public key as HMAC secret
verify_steps: (1) OPTIONS/HEAD https://api.cineplex.de/ to fingerprint; (2) fetch a public endpoint returning any JWT and decode header; (3) if alg=RS256 observed, forge HS256 variant and replay to a validation endpoint — read-only only
impact: Token forgery -> ATO; high
testability: AUTH_HELPED
[HYP] Staging GraphQL env confusion / relaxed auth on sibling
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging/couat environments often mirror production GraphQL but with weaker auth; same resolver layer as prod endpoint
evidence_needed: different auth requirement or exposed schema vs production
verify_steps: (1) GET https://graphql-api.app.staging.cineplex.de/ Accept application/json; (2) introspection query as above; compare auth posture to prod
impact: Schema + mutation surface without auth; medium-high
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de: confidence 45, needs token acquisition — defer until endpoint fingerprinting returns token; keep as candidate
[FINAL] Production GraphQL introspection @ graphql-api.app.cineplex.de — confidence 70, passive-verifiable, high value, in scope
[FINAL] Staging GraphQL env confusion @ graphql-api.app.staging.cineplex.de — confidence 55, passive-verifiable, cheaper than prod first
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fields{name}}}}"} (read-only, 1 rps)
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
[RISK] cineplex: 8/100 — open-bug-bounty crowdsourced surface; active probes on customer-facing API carry PII-exposure risk which the program explicitly forbids; GraphQL introspection is read-only and low-risk; stay passive-first.
## 2026-09-03 21:46:33 UTC [target] (model bigpickle)
[PRIO] graphql-api.app.cineplex.de,8.5,0.25(9)+0.25(8)+0.15(10,GraphQL)+0.15(9,no-auth introspect)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] api.cineplex.de,7.5,0.25(7,untested)+0.25(9,core API)+0.15(9,REST/JWT)+0.15(8,likely open)+0.10(8,cloud)+0.10(6,fresh)
[PRIO] graphql-api.app.staging.cineplex.de,6.5,0.25(5,staging)+0.25(6)+0.15(10,GraphQL)+0.15(9)+0.10(7)+0.10(5)
[HYP] Production GraphQL introspection leakage
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 70
reasoning: Endpoint not in any REJECTED class; introspection is a known high-value passive check; staging/couat siblings exist suggesting shared GraphQL infra with potential env confusion
evidence_needed: 200 response returning __schema types/fields
verify_steps: (1) GET https://graphql-api.app.cineplex.de/ with Accept: application/json; (2) POST same with body {"query":"{__schema{types{name fields{name}}}}"}; (3) if blocked, POST query for a single known field to fingerprint resolver names
impact: Full API schema disclosure enabling targeted IDOR/BOLA and mutation attacks; medium
testability: PASSIVE
[HYP] JWT alg confusion / weak signing on auth API
class: AUTH
asset: api.cineplex.de
confidence: 45
reasoning: New, untested host; sibling auth.cineplex.de prioritizes JWT alg/key confusion per directives; api.cineplex.de likely issues/validates tokens for mobile/app clients
evidence_needed: token accepted with alg=none or HS256 with public key as HMAC secret
verify_steps: (1) OPTIONS/HEAD https://api.cineplex.de/ to fingerprint; (2) fetch a public endpoint returning any JWT and decode header; (3) if alg=RS256 observed, forge HS256 variant and replay to a validation endpoint — read-only only
impact: Token forgery -> ATO; high
testability: AUTH_HELPED
[HYP] Staging GraphQL env confusion / relaxed auth on sibling
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging/couat environments often mirror production GraphQL but with weaker auth; same resolver layer as prod endpoint
evidence_needed: different auth requirement or exposed schema vs production
verify_steps: (1) GET https://graphql-api.app.staging.cineplex.de/ Accept application/json; (2) introspection query as above; compare auth posture to prod
impact: Schema + mutation surface without auth; medium-high
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de: confidence 45, needs token acquisition — defer until endpoint fingerprinting returns token; keep as candidate
[FINAL] Production GraphQL introspection @ graphql-api.app.cineplex.de — confidence 70, passive-verifiable, high value, in scope
[FINAL] Staging GraphQL env confusion @ graphql-api.app.staging.cineplex.de — confidence 55, passive-verifiable, cheaper than prod first
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fields{name}}}}"} (read-only, 1 rps)
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
[RISK] cineplex: 8/100 — open-bug-bounty crowdsourced surface; active probes on customer-facing API carry PII-exposure risk which the program explicitly forbids; GraphQL introspection is read-only and low-risk; stay passive-first.
[NEW] data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11a-2608271446-prd => active deployment), CNAME cineplex-relay.iocnt.net, NOT behind the 403 WAF gate
[CHANGED] api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27eb430)
[PRIO] data-9fc27eb430.cineplex.de,8.0,0.25(8,200 live relay)+0.25(8,internal relay)+0.15(8,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted)+0.10(8,fresh active deploy)
[HYP] Relay/internal-service path disclosure via exposed health/build endpoint
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 60
reasoning: Only authless 200 JSON surface not behind the 403 gate; franchise relay (`cineplex-relay.iocnt.net`) with /health returning {"status":"ok"} and a mutable deployment header (cST-...-prd) indicating CI/CD-driven env; exposed internals often accompany an unauthenticated admin/proxy console or an SSRF-forwarding relay
evidence_needed: additional unauthenticated 200 endpoints (e.g. /metrics, /admin, /proxy, /api/, /internal) beyond /health; any path reflecting an upstream URL (relay-forwarding = SSRF primitive)
verify_steps: (1) GET /metrics, /debug, /admin, /proxy, /api/ on host (already /openapi,/swagger,/graphql,/healthz = 404); (2) if relay forwards, GET a path with a target param and confirm it returns an upstream response — read-only, do NOT point at cloud metadata; (3) compare /health header drift across scans to confirm live CI pipeline
impact: Internal relay/health/metrics disclosure -> footprint for SSRF/proxy abuse -> lateral movement toward cloud metadata; medium-high if relay reflects requests
testability: PASSIVE
[HYP] REST/JSON API shim reachable on relay (method-based gating bypass)
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 45
reasoning: Root and /health return distinct responses while /api* 404 — a routing shim exists serving JSON; root body empty on GET suggests POST/OPTIONS may expose controller routes that the 403 WAF on api.cineplex.de would not
evidence_needed: OPTIONS or HEAD on / returning Allow header list or a non-403 differing fallback; any path returning a distinct route/version identifier
verify_steps: (1) OPTIONS / and HEAD / on data-9fc27eb430.cineplex.de and compare Allow/status to root; (2) if Methods differ from Gate, enumerate /api/v1/* and /rpc/* on this relay instead of gated api.cineplex.de — read-only
impact: Undocumented API surface reachable without the edge auth-gate => potential IDOR/BOLA on relay-backed booking/service calls; medium
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de — root 403, no token/JWKS obtainable; gate blocks even fingerprinting; keep parked until an auth flow yields a token
[PARKED] GraphQL introspection @ graphql-api.app.cineplex.de / staging — 403 at root proves introspection visually disabled; triage INVALID; reopen only with valid session tokens
[PARKED] JWT alg confusion @ api.cineplex.de: conf 45, gate 403, no token; cannot verify passively now
[PARKED] GraphQL introspection (prod+staging): conf dropped to ~15 after 403; triage INVALID; no passive verification possible
[FINAL] Relay/internal-service disclosure @ data-9fc27eb430.cineplex.de — conf 60, live 200 JSON surface, unique in not being WAF-gated, high-value fresh active deploy
[FINAL] REST/JSON API shim @ data-9fc27eb430.cineplex.de — conf 45, method-based route gating on relay, worth one OPTIONS/HEAD probe to confirm routing exists
[NEXT] PROBE: OPTIONS and HEAD https://data-9fc27eb430.cineplex.de/ , then GET /metrics and /api/ on same host (read-only, ≤1 rps); if Allow differs from root or any new 200 JSON surface appears, enumerate /api/v1/* there instead of gated api.cineplex.de
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[RISK] cineplex: 7/100 — target "api" fully 403-gated at edge; remaining live 200 surface (data-9fc27eb430 relay, profil/preference, cloud, support, mailing, vpn-portal) is the only reachable perimeter; franchise relay carries moderate internal-exposure potential; program forbids touching customer/employee/financial/auth data, so stay strictly passive read-only on the health/build surface and never point a relay reflector at cloud metadata or customer endpoints.
## 2026-09-03 23:47:51 UTC [target] (model bigpickle)
verify_steps: (1) GET https://graphql-api.app.cineplex.de/ with Accept: application/json; (2) POST same with body {"query":"{__schema{types{name fields{name}}}}"}; (3) if blocked, POST query for a single known field to fingerprint resolver names
impact: Full API schema disclosure enabling targeted IDOR/BOLA and mutation attacks; medium
testability: PASSIVE
[HYP] JWT alg confusion / weak signing on auth API
class: AUTH
asset: api.cineplex.de
confidence: 45
reasoning: New, untested host; sibling auth.cineplex.de prioritizes JWT alg/key confusion per directives; api.cineplex.de likely issues/validates tokens for mobile/app clients
evidence_needed: token accepted with alg=none or HS256 with public key as HMAC secret
verify_steps: (1) OPTIONS/HEAD https://api.cineplex.de/ to fingerprint; (2) fetch a public endpoint returning any JWT and decode header; (3) if alg=RS256 observed, forge HS256 variant and replay to a validation endpoint — read-only only
impact: Token forgery -> ATO; high
testability: AUTH_HELPED
[HYP] Staging GraphQL env confusion / relaxed auth on sibling
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging/couat environments often mirror production GraphQL but with weaker auth; same resolver layer as prod endpoint
evidence_needed: different auth requirement or exposed schema vs production
verify_steps: (1) GET https://graphql-api.app.staging.cineplex.de/ Accept application/json; (2) introspection query as above; compare auth posture to prod
impact: Schema + mutation surface without auth; medium-high
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de: confidence 45, needs token acquisition — defer until endpoint fingerprinting returns token; keep as candidate
[FINAL] Production GraphQL introspection @ graphql-api.app.cineplex.de — confidence 70, passive-verifiable, high value, in scope
[FINAL] Staging GraphQL env confusion @ graphql-api.app.staging.cineplex.de — confidence 55, passive-verifiable, cheaper than prod first
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fields{name}}}}"} (read-only, 1 rps)
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
[RISK] cineplex: 8/100 — open-bug-bounty crowdsourced surface; active probes on customer-facing API carry PII-exposure risk which the program explicitly forbids; GraphQL introspection is read-only and low-risk; stay passive-first.
[NEW] data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11a-2608271446-prd => active deployment), CNAME cineplex-relay.iocnt.net, NOT behind the 403 WAF gate
[CHANGED] api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27eb430)
[PRIO] data-9fc27eb430.cineplex.de,8.0,0.25(8,200 live relay)+0.25(8,internal relay)+0.15(8,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted)+0.10(8,fresh active deploy)
[HYP] Relay/internal-service path disclosure via exposed health/build endpoint
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
verify_steps: (1) GET https://graphql-api.app.cineplex.de/ with Accept: application/json; (2) POST same with body {"query":"{__schema{types{name fields{name}}}}"}; (3) if blocked, POST query for a single known field to fingerprint resolver names
impact: Full API schema disclosure enabling targeted IDOR/BOLA and mutation attacks; medium
testability: PASSIVE
[HYP] JWT alg confusion / weak signing on auth API
class: AUTH
asset: api.cineplex.de
confidence: 45
reasoning: New, untested host; sibling auth.cineplex.de prioritizes JWT alg/key confusion per directives; api.cineplex.de likely issues/validates tokens for mobile/app clients
evidence_needed: token accepted with alg=none or HS256 with public key as HMAC secret
verify_steps: (1) OPTIONS/HEAD https://api.cineplex.de/ to fingerprint; (2) fetch a public endpoint returning any JWT and decode header; (3) if alg=RS256 observed, forge HS256 variant and replay to a validation endpoint — read-only only
impact: Token forgery -> ATO; high
testability: AUTH_HELPED
[HYP] Staging GraphQL env confusion / relaxed auth on sibling
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging/couat environments often mirror production GraphQL but with weaker auth; same resolver layer as prod endpoint
evidence_needed: different auth requirement or exposed schema vs production
verify_steps: (1) GET https://graphql-api.app.staging.cineplex.de/ Accept application/json; (2) introspection query as above; compare auth posture to prod
impact: Schema + mutation surface without auth; medium-high
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de: confidence 45, needs token acquisition — defer until endpoint fingerprinting returns token; keep as candidate
[FINAL] Production GraphQL introspection @ graphql-api.app.cineplex.de — confidence 70, passive-verifiable, high value, in scope
[FINAL] Staging GraphQL env confusion @ graphql-api.app.staging.cineplex.de — confidence 55, passive-verifiable, cheaper than prod first
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fields{name}}}}"} (read-only, 1 rps)
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
[RISK] cineplex: 8/100 — open-bug-bounty crowdsourced surface; active probes on customer-facing API carry PII-exposure risk which the program explicitly forbids; GraphQL introspection is read-only and low-risk; stay passive-first.
[NEW] data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11a-2608271446-prd => active deployment), CNAME cineplex-relay.iocnt.net, NOT behind the 403 WAF gate
[CHANGED] api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27eb430)
[PRIO] data-9fc27eb430.cineplex.de,8.0,0.25(8,200 live relay)+0.25(8,internal relay)+0.15(8,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted)+0.10(8,fresh active deploy)
[HYP] Relay/internal-service path disclosure via exposed health/build endpoint
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 60
reasoning: Only authless 200 JSON surface not behind the 403 gate; franchise relay (`cineplex-relay.iocnt.net`) with /health returning {"status":"ok"} and a mutable deployment header (cST-...-prd) indicating CI/CD-driven env; exposed internals often accompany an unauthenticated admin/proxy console or an SSRF-forwarding relay
evidence_needed: additional unauthenticated 200 endpoints (e.g. /metrics, /admin, /proxy, /api/, /internal) beyond /health; any path reflecting an upstream URL (relay-forwarding = SSRF primitive)
verify_steps: (1) GET /metrics, /debug, /admin, /proxy, /api/ on host (already /openapi,/swagger,/graphql,/healthz = 404); (2) if relay forwards, GET a path with a target param and confirm it returns an upstream response — read-only, do NOT point at cloud metadata; (3) compare /health header drift across scans to confirm live CI pipeline
impact: Internal relay/health/metrics disclosure -> footprint for SSRF/proxy abuse -> lateral movement toward cloud metadata; medium-high if relay reflects requests
testability: PASSIVE
[HYP] REST/JSON API shim reachable on relay (method-based gating bypass)
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 45
reasoning: Root and /health return distinct responses while /api* 404 — a routing shim exists serving JSON; root body empty on GET suggests POST/OPTIONS may expose controller routes that the 403 WAF on api.cineplex.de would not
evidence_needed: OPTIONS or HEAD on / returning Allow header list or a non-403 differing fallback; any path returning a distinct route/version identifier
verify_steps: (1) OPTIONS / and HEAD / on data-9fc27eb430.cineplex.de and compare Allow/status to root; (2) if Methods differ from Gate, enumerate /api/v1/* and /rpc/* on this relay instead of gated api.cineplex.de — read-only
impact: Undocumented API surface reachable without the edge auth-gate => potential IDOR/BOLA on relay-backed booking/service calls; medium
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de — root 403, no token/JWKS obtainable; gate blocks even fingerprinting; keep parked until an auth flow yields a token
[PARKED] GraphQL introspection @ graphql-api.app.cineplex.de / staging — 403 at root proves introspection visually disabled; triage INVALID; reopen only with valid session tokens
[PARKED] JWT alg confusion @ api.cineplex.de: conf 45, gate 403, no token; cannot verify passively now
[PARKED] GraphQL introspection (prod+staging): conf dropped to ~15 after 403; triage INVALID; no passive verification possible
[FINAL] Relay/internal-service disclosure @ data-9fc27eb430.cineplex.de — conf 60, live 200 JSON surface, unique in not being WAF-gated, high-value fresh active deploy
[FINAL] REST/JSON API shim @ data-9fc27eb430.cineplex.de — conf 45, method-based route gating on relay, worth one OPTIONS/HEAD probe to confirm routing exists
[NEXT] PROBE: OPTIONS and HEAD https://data-9fc27eb430.cineplex.de/ , then GET /metrics and /api/ on same host (read-only, ≤1 rps); if Allow differs from root or any new 200 JSON surface appears, enumerate /api/v1/* there instead of gated api.cineplex.de
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[RISK] cineplex: 7/100 — target "api" fully 403-gated at edge; remaining live 200 surface (data-9fc27eb430 relay, profil/preference, cloud, support, mailing, vpn-portal) is the only reachable perimeter; franchise relay carries moderate internal-exposure potential; program forbids touching customer/employee/financial/auth data, so stay strictly passive read-only on the health/build surface and never point a relay reflector at cloud metadata or customer endpoints.
[HYP] <title>
class: <IDOR|SSRF|AUTH|XSS|BUSLOGIC|MISCONFIG|OATH|OTHER>
asset: <host/endpoint>
confidence: <0-100>
reasoning: <facts only>
evidence_needed: <what proves it>
verify_steps: <passive-first concrete HTTP requests>
impact: <what attacker gets + severity>
testability: <PASSIVE|AUTH_HELPED|HUMAN_ONLY>
[NEW] api.cineplex.de - Host in inventory, no prior probes
[CHANGED] Target is now "api" per current state
[NEW] graphql-api.app.cineplex.de, graphql-api.app.staging.cineplex.de - GraphQL endpoints in inventory
[PRIO] graphql-api.app.cineplex.de,8.5,0.25(9)+0.25(8)+0.15(10,GraphQL)+0.15(9,no-auth introspect)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] api.cineplex.de,7.5,0.25(7,untested)+0.25(9,core API)+0.15(9,REST/JWT)+0.15(8,likely open)+0.10(8,cloud)+0.10(6,fresh)
[PRIO] graphql-api.app.staging.cineplex.de,6.5,0.25(5,staging)+0.25(6)+0.15(10,GraphQL)+0.15(9)+0.10(7)+0.10(5)
[HYP] Production GraphQL introspection leakage
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 70
reasoning: Endpoint not in any REJECTED class; introspection is a known high-value passive check; staging/couat siblings exist suggesting shared GraphQL infra with potential env confusion
evidence_needed: 200 response returning __schema types/fields
verify_steps: (1) GET https://graphql-api.app.cineplex.de/ with Accept: application/json; (2) POST same with body {"query":"{__schema{types{name fields{name}}}}"}; (3) if blocked, POST query for a single known field to fingerprint resolver names
impact: Full API schema disclosure enabling targeted IDOR/BOLA and mutation attacks; medium
testability: PASSIVE
[HYP] JWT alg confusion / weak signing on auth API
class: AUTH
asset: api.cineplex.de
confidence: 45
reasoning: New, untested host; sibling auth.cineplex.de prioritizes JWT alg/key confusion per directives; api.cineplex.de likely issues/validates tokens for mobile/app clients
evidence_needed: token accepted with alg=none or HS256 with public key as HMAC secret
verify_steps: (1) OPTIONS/HEAD https://api.cineplex.de/ to fingerprint; (2) fetch a public endpoint returning any JWT and decode header; (3) if alg=RS256 observed, forge HS256 variant and replay to a validation endpoint — read-only only
impact: Token forgery -> ATO; high
testability: AUTH_HELPED
[HYP] Staging GraphQL env confusion / relaxed auth on sibling
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging/couat environments often mirror production GraphQL but with weaker auth; same resolver layer as prod endpoint
evidence_needed: different auth requirement or exposed schema vs production
verify_steps: (1) GET https://graphql-api.app.staging.cineplex.de/ Accept application/json; (2) introspection query as above; compare auth posture to prod
impact: Schema + mutation surface without auth; medium-high
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de: confidence 45, needs token acquisition — defer until endpoint fingerprinting returns token; keep as candidate
[FINAL] Production GraphQL introspection @ graphql-api.app.cineplex.de — confidence 70, passive-verifiable, high value, in scope
[FINAL] Staging GraphQL env confusion @ graphql-api.app.staging.cineplex.de — confidence 55, passive-verifiable, cheaper than prod first
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fields{name}}}}"} (read-only, 1 rps)
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
[RISK] cineplex: 8/100 — open-bug-bounty crowdsourced surface; active probes on customer-facing API carry PII-exposure risk which the program explicitly forbids; GraphQL introspection is read-only and low-risk; stay passive-first.
[PRIO] graphql-api.app.cineplex.de,8.5,0.25(9)+0.25(8)+0.15(10,GraphQL)+0.15(9,no-auth introspect)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] api.cineplex.de,7.5,0.25(7,untested)+0.25(9,core API)+0.15(9,REST/JWT)+0.15(8,likely open)+0.10(8,cloud)+0.10(6,fresh)
[PRIO] graphql-api.app.staging.cineplex.de,6.5,0.25(5,staging)+0.25(6)+0.15(10,GraphQL)+0.15(9)+0.10(7)+0.10(5)
[HYP] Production GraphQL introspection leakage
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 70
reasoning: Endpoint not in any REJECTED class; introspection is a known high-value passive check; staging/couat siblings exist suggesting shared GraphQL infra with potential env confusion
evidence_needed: 200 response returning __schema types/fields
verify_steps: (1) GET https://graphql-api.app.cineplex.de/ with Accept: application/json; (2) POST same with body {"query":"{__schema{types{name fields{name}}}}"}; (3) if blocked, POST query for a single known field to fingerprint resolver names
impact: Full API schema disclosure enabling targeted IDOR/BOLA and mutation attacks; medium
testability: PASSIVE
[HYP] JWT alg confusion / weak signing on auth API
class: AUTH
asset: api.cineplex.de
confidence: 45
reasoning: New, untested host; sibling auth.cineplex.de prioritizes JWT alg/key confusion per directives; api.cineplex.de likely issues/validates tokens for mobile/app clients
evidence_needed: token accepted with alg=none or HS256 with public key as HMAC secret
verify_steps: (1) OPTIONS/HEAD https://api.cineplex.de/ to fingerprint; (2) fetch a public endpoint returning any JWT and decode header; (3) if alg=RS256 observed, forge HS256 variant and replay to a validation endpoint — read-only only
impact: Token forgery -> ATO; high
testability: AUTH_HELPED
[HYP] Staging GraphQL env confusion / relaxed auth on sibling
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging/couat environments often mirror production GraphQL but with weaker auth; same resolver layer as prod endpoint
evidence_needed: different auth requirement or exposed schema vs production
verify_steps: (1) GET https://graphql-api.app.staging.cineplex.de/ Accept application/json; (2) introspection query as above; compare auth posture to prod
impact: Schema + mutation surface without auth; medium-high
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de: confidence 45, needs token acquisition — defer until endpoint fingerprinting returns token; keep as candidate
[FINAL] Production GraphQL introspection @ graphql-api.app.cineplex.de — confidence 70, passive-verifiable, high value, in scope
[FINAL] Staging GraphQL env confusion @ graphql-api.app.staging.cineplex.de — confidence 55, passive-verifiable, cheaper than prod first
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ with Accept: application/json — if 200/400 GraphQL response, follow with POST {"query":"{__schema{types{name fields{name}}}}"} (read-only, 1 rps)
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized in directives
[RISK] cineplex: 8/100 — open-bug-bounty crowdsourced surface; active probes on customer-facing API carry PII-exposure risk which the program explicitly forbids; GraphQL introspection is read-only and low-risk; stay passive-first.
[NEW] data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11a-2608271446-prd => active deployment), CNAME cineplex-relay.iocnt.net, NOT behind the 403 WAF gate
[CHANGED] api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27eb430)
[PRIO] data-9fc27eb430.cineplex.de,8.0,0.25(8,200 live relay)+0.25(8,internal relay)+0.15(8,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted)+0.10(8,fresh active deploy)
[HYP] Relay/internal-service path disclosure via exposed health/build endpoint
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 60
reasoning: Only authless 200 JSON surface not behind the 403 gate; franchise relay (`cineplex-relay.iocnt.net`) with /health returning {"status":"ok"} and a mutable deployment header (cST-...-prd) indicating CI/CD-driven env; exposed internals often accompany an unauthenticated admin/proxy console or an SSRF-forwarding relay
evidence_needed: additional unauthenticated 200 endpoints (e.g. /metrics, /admin, /proxy, /api/, /internal) beyond /health; any path reflecting an upstream URL (relay-forwarding = SSRF primitive)
verify_steps: (1) GET /metrics, /debug, /admin, /proxy, /api/ on host (already /openapi,/swagger,/graphql,/healthz = 404); (2) if relay forwards, GET a path with a target param and confirm it returns an upstream response — read-only, do NOT point at cloud metadata; (3) compare /health header drift across scans to confirm live CI pipeline
impact: Internal relay/health/metrics disclosure -> footprint for SSRF/proxy abuse -> lateral movement toward cloud metadata; medium-high if relay reflects requests
testability: PASSIVE
[HYP] REST/JSON API shim reachable on relay (method-based gating bypass)
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 45
reasoning: Root and /health return distinct responses while /api* 404 — a routing shim exists serving JSON; root body empty on GET suggests POST/OPTIONS may expose controller routes that the 403 WAF on api.cineplex.de would not
evidence_needed: OPTIONS or HEAD on / returning Allow header list or a non-403 differing fallback; any path returning a distinct route/version identifier
verify_steps: (1) OPTIONS / and HEAD / on data-9fc27eb430.cineplex.de and compare Allow/status to root; (2) if Methods differ from Gate, enumerate /api/v1/* and /rpc/* on this relay instead of gated api.cineplex.de — read-only
impact: Undocumented API surface reachable without the edge auth-gate => potential IDOR/BOLA on relay-backed booking/service calls; medium
testability: PASSIVE
[PARKED] JWT alg confusion @ api.cineplex.de — root 403, no token/JWKS obtainable; gate blocks even fingerprinting; keep parked until an auth flow yields a token
[PARKED] GraphQL introspection @ graphql-api.app.cineplex.de / staging — 403 at root proves introspection visually disabled; triage INVALID; reopen only with valid session tokens
[PARKED] JWT alg confusion @ api.cineplex.de: conf 45, gate 403, no token; cannot verify passively now
[PARKED] GraphQL introspection (prod+staging): conf dropped to ~15 after 403; triage INVALID; no passive verification possible
[FINAL] Relay/internal-service disclosure @ data-9fc27eb430.cineplex.de — conf 60, live 200 JSON surface, unique in not being WAF-gated, high-value fresh active deploy
[FINAL] REST/JSON API shim @ data-9fc27eb430.cineplex.de — conf 45, method-based route gating on relay, worth one OPTIONS/HEAD probe to confirm routing exists
[NEXT] PROBE: OPTIONS and HEAD https://data-9fc27eb430.cineplex.de/ , then GET /metrics and /api/ on same host (read-only, ≤1 rps); if Allow differs from root or any new 200 JSON surface appears, enumerate /api/v1/* there instead of gated api.cineplex.de
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[RISK] cineplex: 7/100 — target "api" fully 403-gated at edge; remaining live 200 surface (data-9fc27eb430 relay, profil/preference, cloud, support, mailing, vpn-portal) is the only reachable perimeter; franchise relay carries moderate internal-exposure potential; program forbids touching customer/employee/financial/auth data, so stay strictly passive read-only on the health/build surface and never point a relay reflector at cloud metadata or customer endpoints.
[HYP] Unauthenticated IDOR/BOLA on user/order/ticket/voucher GraphQL queries
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 62
reasoning: Introspection confirmed (anonymous POST 200, sha256 9850f...); schema exposes `userById(id)`, `userByQr(qrCode)`, `voucherInstanceByQR(qrCode)`, `ticket(id)`, `order(id)`, `invoice(id)`, `getOnlineTicketingBooking(...securityKey)`; `currentUser` is gated (UNAUTHENTICATED) but these id/qr/securityKey-lookup queries have NO evident context-user dependency in their args, so their gate is unproven and likely missing
evidence_needed: an id/qr/booking fetch returns a record without valid session — but per program rule "exposure of customer data during testing" is OUT OF SCOPE, so this requires a test/sandbox account or explicit program consent
verify_steps: (1) already done: map which sensitive fields lack `@auth` in schema; (2) INVESTIGATE ONLY with non-customer test fixture/consent, never live PII; do NOT run `{userById(id:...)}` etc. against real users in this session
impact: cross-tenant PII/booking/voucher disclosure, account take-over via qr/securityKey data theft; critical if confirmed
testability: HUMAN_ONLY
[HYP] Mutation authorization gap / admin-mutation exposed via anonymous POST
class: BUSLOGIC
asset: graphql-api.app.cineplex.de
confidence: 55
reasoning: Anonymous POST reaches the full Mutation root; several mutations (`updateUser`, `updateUserAdminStatus`, `sendNotifications`, `createVoucherInstances`, `deleteCineplexUser`, `cancelTicket`, `updateTicket`) are admin-class and their resolvers sit in the same Lambda `/var/task/graphql.js`; arg lists show no explicit auth handle compared to gated `currentUser`
evidence_needed: calling an admin mutation without token returns non-UNAUTHENTICATED result or side effect — MUTATION = OUT OF SCOPE on live infra, requires consent/test env
verify_steps: (1) static: confirm mutation args vs `currentUser` gate asymmetry; (2) do NOT execute mutating queries on live data; request program consent or sandbox first
impact: mass PII/exposure, voucher minting, ticket cancellation, notification abuse; critical
testability: HUMAN_ONLY
[HYP] JWT issued by this GraphQL host with weak alg (alg confusion/none)
class: AUTH
asset: graphql-api.app.cineplex.de
confidence: 50
reasoning: `login`/`refreshLogin` return `jwt`+`refreshToken`+`csrf`, so this host authenticates; sibling `auth.cineplex.de` has JWT-alg confusion prioritized per directives; `/var/task/graphql.js` monolith suggests custom server-side JWT handling prone to alg confusion
evidence_needed: obtain any issued token, check `alg` header; forge HS256/none and replay — requires an account/session (AUTH_HELPED, cannot do passively)
verify_steps: (1) [NEXT passive] OPTIONS/HEAD to fingerprint JWT config nowhere available without token; (2) requires authenticated client => defer to AUTH_HELPED session with test account
impact: token forgery -> ATO, session hijack; high
testability: AUTH_HELPED
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ with `Accept: application/json; charset=utf-8` and `Content-Type: application/json` is already CONFIRMED live; immediate next probe: request specific introspection for input-arg types on `userById`, `getOnlineTicketingBooking`, and `updateUser` to confirm the exact non-PII gate behavior: POST `{"query":"{__type(name:\"Query\"){fields{name args{name type{name kind ofType{name kind}}}}}}"}` (schema-only, read-only, ≤1 rps) — do NOT fetch any user/ticket/order records.
[RISK] cineplex: 6/100 — the confirmed introspection is read-only and in-scope (low risk). Highest-value follow-ups (IDOR/mutation probes on user/ticket/order data and token forgery) directly touch customer/financial/auth data and the program EXPLICITLY forbids exposing that during testing; any such test requires a test/sandbox account or prior consent. Stay strictly read-only: schema/gate-behavior mapping only, never pull real PII or execute mutations against live infra.
## 2026-09-04 02:37:57 UTC [target] (model bigpickle)
[CHANGED] probe-results.md 2026-09-03 23:48:07 UTC — `graphql-api.app.cineplex.de/` GET confirmed 403 (WAF-gated at root); prior introspection CONFIRMED entry in KB remains valid (POST 200, not GET)
[CHANGED] probe-results.md 2026-09-03 23:48:07 UTC — `data-9fc27eb430.cineplex.de/` returns 200 `len=?` (body length unmeasured in probe log)
[NEW] `booking.cineplex.de/api/booking/{id` confirmed 403 in probe-results — session-gated, AUTH_HELPED required
[PRIO] data-9fc27eb430.cineplex.de,8.1,0.25(8,200 live relay)+0.25(8,internal relay CNAME)+0.15(8,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted CDN)+0.10(9,fresh active deploy)
[PRIO] graphql-api.app.cineplex.de,7.4,0.25(7,POST 200 introspect)+0.25(9,core API)+0.15(10,GraphQL)+0.15(6,gated GET but POST open)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] booking.cineplex.de,5.2,0.25(4,403 all paths)+0.25(8,booking core)+0.15(5,REST)+0.15(3,gated)+0.10(7,cloud)+0.10(6,stale probes)
[HYP] Undocumented API surface / relay-forwarding SSRF primitive on franchise relay
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 62
reasoning: Only confirmed authless 200 surface not behind the 403 WAF gate; `cineplex-relay.iocnt.net` CNAME is a relay/proxy by name; `/health` returns JSON; build header `cST-...-prd` changes across scans confirming live CI; relay hosts commonly proxy internal APIs — any path reflecting a caller-controlled upstream URL is an SSRF primitive
evidence_needed: (1) OPTIONS/HEAD on `/` returning `Allow` list differing from GET-only root; (2) GET `/metrics`, `/debug`, `/admin`, `/proxy`, `/api/` returning 200 JSON; (3) any query-param path (e.g. `?target=`) that returns upstream content
verify_steps: (1) HEAD https://data-9fc27eb430.cineplex.de/ — note `Allow` header and body length vs GET; (2) GET https://data-9fc27eb430.cineplex.de/metrics — check for Prometheus/stats JSON; (3) GET https://data-9fc27eb430.cineplex.de/api/ — check for REST routes; all read-only, ≤1 rps, no cloud-metadata targets
impact: Internal relay/health/metrics disclosure → footprint for SSRF/proxy abuse → lateral movement toward cloud metadata (169.254.169.254); medium-high if relay reflects requests
testability: PASSIVE
[HYP] GraphQL introspection via POST root on production — schema disclosure enabling targeted IDOR
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 65
reasoning: KB marks introspection CONFIRMED (POST 200, full schema, 100+ mutations, PII-exposing queries) from a prior session; probe-results only logged GET requests (403); the WAF is method-gated — GET is blocked, POST with `Content-Type: application/json` passes; this is a common WAF misconfiguration where the rule matches GET/HEAD but not POST
evidence_needed: (1) POST https://graphql-api.app.cineplex.de/ with `{"query":"{__schema{queryType{name}}}"}` returning 200 + JSON schema; (2) failure of same POST with `GET` method (confirms method-gating)
verify_steps: (1) POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only introspection, ≤1 rps; (2) if 200, POST with `{"query":"{__schema{mutationType{name}}}"}` to enumerate mutation surface; (3) do NOT call userById/order/ticket/voucher queries — those expose customer PII and the program forbids it
impact: Full schema enumeration → targeted IDOR/BOLA probes on user/ticket/order mutations → critical if auth bypass confirmed; medium if schema-only disclosure
testability: PASSIVE
[HYP] Staging GraphQL WAF bypass / relaxed auth on graphql-api.app.staging.cineplex.de
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 52
reasoning: Staging environments commonly mirror production schema but with weaker WAF/auth; probe-results shows GET returning 403 (same WAF rule as prod) but POST may pass; `graphql-api.app.couat.cineplex.de` also exists in inventory as a UAT sibling — env confusion likely
evidence_needed: POST https://graphql-api.app.staging.cineplex.de/ with introspection query returns 200 with same schema as prod
verify_steps: (1) POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only; (2) compare response to prod introspection; (3) if different schema or no auth, report as env confusion
impact: Staging schema + mutation access without production WAF → easier exploitation path to booking/voucher/user mutations; medium-high
testability: PASSIVE
[FINAL] Undocumented API surface / relay-forwarding SSRF primitive @ data-9fc27eb430.cineplex.de — conf 62, PASSIVE-verifiable, unique authless 200 surface, high relay-proxy potential
[FINAL] GraphQL introspection via POST root @ graphql-api.app.cineplex.de — conf 65, PASSIVE, schema-only read-only query, high-value per program directives
[FINAL] Staging GraphQL WAF bypass @ graphql-api.app.staging.cineplex.de — conf 52, PASSIVE, cheaper than prod first, env confusion = high value
[PARKED] JWT alg confusion @ api.cineplex.de — conf 45, root 403, no token obtainable; requires AUTH_HELPED session; gate blocks all fingerprinting
[PARKED] IDOR/BOLA via GraphQL userById @ graphql-api.app.cineplex.de — conf 62, HUMAN_ONLY (program forbids exposing customer PII during testing); needs test/sandbox account or explicit consent
[PARKED] Mutation authorization gap @ graphql-api.app.cineplex.de — conf 55, HUMAN_ONLY (mutations = live customer data modification); requires program consent or sandbox
[PARKED] JWT alg confusion on GraphQL host @ graphql-api.app.cineplex.de — conf 50, AUTH_HELPED; login mutation exists but no token obtainable passively
[NEXT] PROBE: (1) POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only introspection, ≤1 rps; (2) HEAD https://data-9fc27eb430.cineplex.de/ — note Allow header + body length; (3) GET https://data-9fc27eb430.cineplex.de/metrics — check for Prometheus/stats JSON; all read-only, no customer data, no mutations.
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 100+ sensitive mutations and PII-exposing queries
[LEARN] ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUMAN_ONLY per program PII rule
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but auth.cineplex.de/.well-known/jwks.json returns 404, no passive JWKS fetch possible
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[LEARN] REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot password pages" as out of scope
[LEARN] REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
[LEARN] REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
[LEARN] REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
[RISK] cineplex: 8/100 — target "api" fully 403-gated at root; the only active attack surface is the franchise relay (`data-9fc27eb430.cineplex.de`, CNAME `cineplex-relay.iocnt.net`) which serves unauthenticated 200 JSON on `/health` and `/` and may expose internal relay/proxy routes or SSRF-forwarding paths. The GraphQL production endpoint (`graphql-api.app.cineplex.de`) accepts introspection POST but root GET is WAF-blocked — schema enumeration is confirmed but the actual mutation/IDOR tests require live customer data which the program forbids. JWKS endpoint is 404 so passive JWT analysis is blocked. Remaining live hosts (`profil`, `support`, `mailing`, `vpn-portal`) are third-party managed (Zammad, Mailjet, ntxzone) and carry low inherent risk. Program explicitly forbids exposing customer/employee/financial/auth data during testing, which eliminates the highest-value IDOR/mutation probes without a test/sandbox account or explicit consent. Stay passive-first: relay surface enumeration + schema-only GraphQL introspection only.
## 2026-09-04 07:25:57 UTC [target] (model bigpickle)
## 2026-09-04 12:20:28 UTC [target] (model bigpickle)
[CHANGED] probe-results.md 2026-09-04 07:26:46 UTC — `data-9fc27eb430.cineplex.de/metrics` returned 200 `len=114` (prior cycle logged it but did not act on it; new confirmed surface)
[CHANGED] probe-results.md 2026-09-04 07:26:46 UTC — `data-9fc27eb430.cineplex.de/.well-known/` confirmed 404 (new probe added to probe-results)
[CHANGED] probe-results.md 2026-09-04 07:26:46 UTC — `data-9fc27eb430.cineplex.de/health` body length now measured: `len=15` (was `len=?` in prior cycles)
[NEW] `data-9fc27eb430.cineplex.de/metrics` confirmed 200 with 114 bytes — second authless 200 surface on relay beyond `/health` and `/`; content unexamined
[PRIO] data-9fc27eb430.cineplex.de,8.1,0.25(8,200 live relay)+0.25(8,internal relay CNAME)+0.15(8,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted CDN)+0.10(9,fresh active deploy)
[PRIO] graphql-api.app.cineplex.de,7.4,0.25(7,POST 200 introspect)+0.25(9,core API)+0.15(10,GraphQL)+0.15(6,gated GET but POST open)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] graphql-api.app.staging.cineplex.de,6.8,0.25(6,staging untested POST)+0.25(7,shared schema)+0.15(10,GraphQL)+0.15(7,likely same WAF)+0.10(6,cloud)+0.10(6,fresh)
[PRIO] booking.cineplex.de,5.2,0.25(4,403 all paths)+0.25(8,booking core)+0.15(5,REST)+0.15(3,gated)+0.10(7,cloud)+0.10(6,stale probes)
[HYP] Relay metrics endpoint discloses internal service topology / Prometheus stats
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 68
reasoning: Probe-results confirms `GET /metrics` returns 200 with 114 bytes — a second authless 200 surface on the franchise relay beyond `/health` (len=15) and root (len=?). Metrics endpoints on Node/relay infra commonly expose process info, uptime, route tables, or internal hostnames. This is distinct from the REJECTED grafana/metrics-only class because it is a relay-specific endpoint on active CI/CD infra (build header cST-...-prd), not a Grafana dashboard; and 114 bytes may contain structured JSON or Prometheus text with service names, route counts, or upstream targets — more than descriptive headers.
evidence_needed: (1) Content of `/metrics` response body — any internal hostname, route, port, or upstream target; (2) whether `Content-Type` is `text/plain` (Prometheus) or `application/json` (custom); (3) any other paths returning 200 (e.g. `/status`, `/config`, `/debug`, `/routes`)
verify_steps: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cineplex.de/status — check for additional JSON surface; (3) GET https://data-9fc27eb430.cineplex.de/debug — check for debug console; (4) GET https://data-9fc27eb430.cineplex.de/routes — check for route table disclosure
impact: Internal relay topology / upstream targets / route table disclosure → footprint for SSRF targeting; medium if only stats, medium-high if upstream hostnames or auth tokens leaked
testability: PASSIVE
[HYP] GraphQL introspection POST returns full schema despite GET being WAF-blocked
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 65
reasoning: KB marks introspection CONFIRMED (POST 200, full schema, 100+ mutations, PII-exposing queries) from a prior session. Probe-results only logs GET requests (403). The WAF is method-gated — GET/HEAD blocked, POST with `Content-Type: application/json` passes. This is a classic WAF rule misconfiguration matching on method rather than path+content. Full schema enumeration enables targeted IDOR/BOLA on the 100+ mutations exposed.
evidence_needed: (1) POST https://graphql-api.app.cineplex.de/ with `{"query":"{__schema{queryType{name}}}"}` returning 200 + JSON; (2) schema containing `userById`, `searchUsers`, `adminUsers`, `login` mutation fields confirmed via introspection
verify_steps: (1) POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only introspection, ≤1 rps; (2) if 200, POST with `{"query":"{__schema{mutationType{name}}}"}` to confirm mutation surface; (3) do NOT call userById/order/ticket queries — those expose customer PII per program restrictions
impact: Full schema enumeration → targeted IDOR/BOLA probes on user/ticket/order mutations → critical if auth bypass confirmed; medium if schema-only disclosure
testability: PASSIVE
[HYP] Staging GraphQL endpoint accepts introspection POST with relaxed WAF rules
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 52
reasoning: Staging environment mirrors production schema but commonly has weaker WAF/auth rules. Probe-results shows GET returning 403 (same WAF rule as prod) but POST may pass. `graphql-api.app.couat.cineplex.de` also exists as UAT sibling — env confusion likely. If staging introspection succeeds, schema comparison with prod reveals auth-gate differences and potentially exposed test resolvers.
evidence_needed: POST https://graphql-api.app.staging.cineplex.de/ with introspection query returns 200 with same or different schema as prod
verify_steps: (1) POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only; (2) compare response to prod introspection; (3) if different schema or no auth, report as env confusion
impact: Staging schema + mutation access without production WAF → easier exploitation path to booking/voucher/user mutations; medium-high
testability: PASSIVE
[FINAL] Relay metrics endpoint topology disclosure @ data-9fc27eb430.cineplex.de — conf 68, PASSIVE, second authless 200 surface, 114 bytes unexamined, highest immediate value
[FINAL] GraphQL introspection via POST @ graphql-api.app.cineplex.de — conf 65, PASSIVE, KB-CONFIRMED, schema-only read-only
[FINAL] Staging GraphQL introspection @ graphql-api.app.staging.cineplex.de — conf 52, PASSIVE, cheaper than prod, env confusion value
[NEXT] PROBE: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cineplex.de/status — check for additional JSON surface; (3) POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only introspection, ≤1 rps. All read-only, no customer data, no mutations.
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 100+ sensitive mutations and PII-exposing queries
[LEARN] ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUMAN_ONLY per program PII rule
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but auth.cineplex.de/.well-known/jwks.json returns 404, no passive JWKS fetch possible
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114 bytes — second authless 200 surface; content unexamined; not in REJECTED class
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[LEARN] REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot password pages" as out of scope
[LEARN] REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
[LEARN] REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
[LEARN] REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
[RISK] cineplex: 8/100 — target "api" fully 403-gated at root; the only active attack surface is the franchise relay (`data-9fc27eb430.cineplex.de`, CNAME `cineplex-relay.iocnt.net`) which serves unauthenticated 200 JSON on `/health`, `/`, and now confirmed `/metrics` (114 bytes). The GraphQL production endpoint accepts introspection POST but root GET is WAF-blocked — schema enumeration is confirmed but the actual mutation/IDOR tests require live customer data which the program forbids. JWKS endpoint is 404 so passive JWT analysis is blocked. Remaining live hosts (`profil`, `support`, `mailing`, `vpn-portal`) are third-party managed (Zammad, Mailjet, ntxzone) and carry low inherent risk. Program explicitly forbids exposing customer/employee/financial/auth data during testing, which eliminates the highest-value IDOR/mutation probes without a test/sandbox account or explicit consent. The relay `/metrics` endpoint is the highest-priority immediate probe — 114 bytes of unexamined content on an authless surface may contain internal topology useful for relay SSRF chaining.
