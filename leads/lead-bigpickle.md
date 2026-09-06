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
## 2026-09-04 16:26:54 UTC [target] (model bigpickle)
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` returned 200 `len=115` (updated from 114 in prior cycle)
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/status` confirmed 404
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/debug` confirmed 404
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/routes` confirmed 404
[CHANGED] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` body length changed from 114 to 115 bytes (new content or timestamp update)
[CHANGED] probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.cineplex.de/` GET still returns 403 (WAF-gated)
[CHANGED] probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.staging.cineplex.de/` GET still returns 403 (WAF-gated)
[PRIO] data-9fc27eb430.cineplex.de,8.2,0.25(8,200 live relay)+0.25(8,internal relay CNAME)+0.15(9,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted CDN)+0.10(9,fresh active deploy)
[PRIO] graphql-api.app.cineplex.de,7.6,0.25(7,POST 200 introspect)+0.25(9,core API)+0.15(10,GraphQL)+0.15(6,gated GET but POST open)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] graphql-api.app.staging.cineplex.de,6.8,0.25(6,staging untested POST)+0.25(7,shared schema)+0.15(10,GraphQL)+0.15(7,likely same WAF)+0.10(6,cloud)+0.10(6,fresh)
[PRIO] booking.cineplex.de,5.2,0.25(4,403 all paths)+0.25(8,booking core)+0.15(5,REST)+0.15(3,gated)+0.10(7,cloud)+0.10(6,stale probes)
[HYP] Relay /metrics endpoint discloses internal service topology or Prometheus stats
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 72
reasoning: Probe-results confirms `GET /metrics` returns 200 with 115 bytes (updated from 114 in prior cycle). This is the second authless 200 surface on the franchise relay beyond `/health` (len=15) and root (len=?). Metrics endpoints on Node/relay infra commonly expose process info, uptime, route tables, or internal hostnames. The 115-byte response likely contains structured JSON or Prometheus text with service names, route counts, or upstream targets. This is distinct from the REJECTED grafana/metrics-only class because it is a relay-specific endpoint on active CI/CD infra (build header cST-...-prd), not a Grafana dashboard.
evidence_needed: (1) Content of `/metrics` response body — any internal hostname, route, port, or upstream target; (2) whether `Content-Type` is `text/plain` (Prometheus) or `application/json` (custom); (3) any other paths returning 200 (e.g. `/config`, `/info`, `/env`)
verify_steps: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cineplex.de/config — check for config disclosure; (3) GET https://data-9fc27eb430.cineplex.de/info — check for info endpoint; (4) GET https://data-9fc27eb430.cineplex.de/env — check for environment variables
impact: Internal relay topology / upstream targets / route table disclosure → footprint for SSRF targeting; medium if only stats, medium-high if upstream hostnames or auth tokens leaked
testability: PASSIVE
[HYP] GraphQL introspection POST bypasses WAF to expose full schema with IDOR-capable mutations
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 70
reasoning: KB marks introspection CONFIRMED (POST 200, full schema, 100+ mutations, PII-exposing queries) from prior sessions. Probe-results only logs GET requests (403). The WAF is method-gated — GET/HEAD blocked, POST with `Content-Type: application/json` passes. Full schema enumeration enables targeted IDOR/BOLA on the 100+ mutations exposed. However, actual mutation/IDOR tests require live customer data which the program forbids, limiting testability to schema-only enumeration.
evidence_needed: (1) POST https://graphql-api.app.cineplex.de/ with `{"query":"{__schema{queryType{name}}}"}` returning 200 + JSON; (2) schema containing `userById`, `searchUsers`, `adminUsers`, `login` mutation fields confirmed via introspection
verify_steps: (1) POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only introspection, ≤1 rps; (2) if 200, POST with `{"query":"{__schema{mutationType{name}}}"}` to confirm mutation surface; (3) do NOT call userById/order/ticket queries — those expose customer PII per program restrictions
impact: Full schema enumeration → targeted IDOR/BOLA probes on user/ticket/order mutations → critical if auth bypass confirmed; medium if schema-only disclosure
testability: PASSIVE
[HYP] Staging GraphQL endpoint accepts introspection POST with relaxed WAF rules
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging environment mirrors production schema but commonly has weaker WAF/auth rules. Probe-results shows GET returning 403 (same WAF rule as prod) but POST may pass. `graphql-api.app.couat.cineplex.de` also exists as UAT sibling — env confusion likely. If staging introspection succeeds, schema comparison with prod reveals auth-gate differences and potentially exposed test resolvers.
evidence_needed: POST https://graphql-api.app.staging.cineplex.de/ with introspection query returns 200 with same or different schema as prod
verify_steps: (1) POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only; (2) compare response to prod introspection; (3) if different schema or no auth, report as env confusion
impact: Staging schema + mutation access without production WAF → easier exploitation path to booking/voucher/user mutations; medium-high
testability: PASSIVE
[FINAL] Relay /metrics endpoint topology disclosure @ data-9fc27eb430.cineplex.de — conf 72, PASSIVE, second authless 200 surface, 115 bytes unexamined, highest immediate value
[FINAL] GraphQL introspection via POST @ graphql-api.app.cineplex.de — conf 70, PASSIVE, KB-CONFIRMED, schema-only read-only
[FINAL] Staging GraphQL introspection @ graphql-api.app.staging.cineplex.de — conf 55, PASSIVE, cheaper than prod, env confusion value
[NEXT] PROBE: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cineplex.de/config — check for config disclosure; (3) GET https://data-9fc27eb430.cineplex.de/info — check for info endpoint; (4) GET https://data-9fc27eb430.cineplex.de/env — check for environment variables
[LEARN] ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 115 bytes — second authless 200 surface; content unexamined; not in REJECTED class
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 100+ sensitive mutations and PII-exposing queries
[LEARN] ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passive verification
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot password pages" as out of scope
[LEARN] REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
[LEARN] REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
[LEARN] REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
[RISK] cineplex: 8/100 — target "api" fully 403-gated at root; the only active attack surface is the franchise relay (`data-9fc27eb430.cineplex.de`, CNAME `cineplex-relay.iocnt.net`) which serves unauthenticated 200 JSON on `/health`, `/`, and now confirmed `/metrics` (115 bytes). The GraphQL production endpoint accepts introspection POST but root GET is WAF-blocked — schema enumeration is confirmed but the actual mutation/IDOR tests require live customer data which the program forbids. JWKS endpoint is 404 so passive JWT analysis is blocked. Remaining live hosts (`profil`, `support`, `mailing`, `vpn-portal`) are third-party managed (Zammad, Mailjet, ntxzone) and carry low inherent risk. Program explicitly forbids exposing customer/employee/financial/auth data during testing, which eliminates the highest-value IDOR/mutation probes without a test/sandbox account or explicit consent. The relay `/metrics` endpoint is the highest-priority immediate probe — 115 bytes of unexamined content on an authless surface may contain internal topology useful for relay SSRF chaining.
## 2026-09-04 19:07:49 UTC [target] (model bigpickle)
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` returned 200 `len=115` (updated from 114 in prior cycle)
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/status` confirmed 404
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/debug` confirmed 404
[NEW] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/routes` confirmed 404
[CHANGED] probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` body length changed from 114 to 115 bytes (new content or timestamp update)
[CHANGED] probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.cineplex.de/` GET still returns 403 (WAF-gated)
[CHANGED] probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.staging.cineplex.de/` GET still returns 403 (WAF-gated)
[PRIO] data-9fc27eb430.cineplex.de,8.2,0.25(8,200 live relay)+0.25(8,internal relay CNAME)+0.15(9,JSON health/wire)+0.15(10,no-auth gate)+0.10(7,google-fronted CDN)+0.10(9,fresh active deploy)
[PRIO] graphql-api.app.cineplex.de,7.6,0.25(7,POST 200 introspect)+0.25(9,core API)+0.15(10,GraphQL)+0.15(6,gated GET but POST open)+0.10(8,cloud)+0.10(8,fresh)
[PRIO] graphql-api.app.staging.cineplex.de,6.8,0.25(6,staging untested POST)+0.25(7,shared schema)+0.15(10,GraphQL)+0.15(7,likely same WAF)+0.10(6,cloud)+0.10(6,fresh)
[PRIO] booking.cineplex.de,5.2,0.25(4,403 all paths)+0.25(8,booking core)+0.15(5,REST)+0.15(3,gated)+0.10(7,cloud)+0.10(6,stale probes)
[HYP] Relay /metrics endpoint discloses internal service topology or Prometheus stats
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 72
reasoning: Probe-results confirms `GET /metrics` returns 200 with 115 bytes (updated from 114 in prior cycle). This is the second authless 200 surface on the franchise relay beyond `/health` (len=15) and root (len=?). Metrics endpoints on Node/relay infra commonly expose process info, uptime, route tables, or internal hostnames. The 115-byte response likely contains structured JSON or Prometheus text with service names, route counts, or upstream targets. This is distinct from the REJECTED grafana/metrics-only class because it is a relay-specific endpoint on active CI/CD infra (build header cST-...-prd), not a Grafana dashboard.
evidence_needed: (1) Content of `/metrics` response body — any internal hostname, route, port, or upstream target; (2) whether `Content-Type` is `text/plain` (Prometheus) or `application/json` (custom); (3) any other paths returning 200 (e.g. `/config`, `/info`, `/env`)
verify_steps: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cineplex.de/config — check for config disclosure; (3) GET https://data-9fc27eb430.cineplex.de/info — check for info endpoint; (4) GET https://data-9fc27eb430.cineplex.de/env — check for environment variables
impact: Internal relay topology / upstream targets / route table disclosure → footprint for SSRF targeting; medium if only stats, medium-high if upstream hostnames or auth tokens leaked
testability: PASSIVE
[HYP] GraphQL introspection POST bypasses WAF to expose full schema with IDOR-capable mutations
class: MISCONFIG
asset: graphql-api.app.cineplex.de
confidence: 70
reasoning: KB marks introspection CONFIRMED (POST 200, full schema, 100+ mutations, PII-exposing queries) from prior sessions. Probe-results only logs GET requests (403). The WAF is method-gated — GET/HEAD blocked, POST with `Content-Type: application/json` passes. Full schema enumeration enables targeted IDOR/BOLA on the 100+ mutations exposed. However, actual mutation/IDOR tests require live customer data which the program forbids, limiting testability to schema-only enumeration.
evidence_needed: (1) POST https://graphql-api.app.cineplex.de/ with `{"query":"{__schema{queryType{name}}}"}` returning 200 + JSON; (2) schema containing `userById`, `searchUsers`, `adminUsers`, `login` mutation fields confirmed via introspection
verify_steps: (1) POST https://graphql-api.app.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only introspection, ≤1 rps; (2) if 200, POST with `{"query":"{__schema{mutationType{name}}}"}` to confirm mutation surface; (3) do NOT call userById/order/ticket queries — those expose customer PII per program restrictions
impact: Full schema enumeration → targeted IDOR/BOLA probes on user/ticket/order mutations → critical if auth bypass confirmed; medium if schema-only disclosure
testability: PASSIVE
[HYP] Staging GraphQL endpoint accepts introspection POST with relaxed WAF rules
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Staging environment mirrors production schema but commonly has weaker WAF/auth rules. Probe-results shows GET returning 403 (same WAF rule as prod) but POST may pass. `graphql-api.app.couat.cineplex.de` also exists as UAT sibling — env confusion likely. If staging introspection succeeds, schema comparison with prod reveals auth-gate differences and potentially exposed test resolvers.
evidence_needed: POST https://graphql-api.app.staging.cineplex.de/ with introspection query returns 200 with same or different schema as prod
verify_steps: (1) POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — body: `{"query":"{__schema{queryType{name}}}"}` — read-only; (2) compare response to prod introspection; (3) if different schema or no auth, report as env confusion
impact: Staging schema + mutation access without production WAF → easier exploitation path to booking/voucher/user mutations; medium-high
testability: PASSIVE
[FINAL] Relay /metrics topology disclosure @ data-9fc27eb430.cineplex.de — conf 72, PASSIVE, second authless 200 surface, 115 bytes unexamined, highest immediate value
[FINAL] GraphQL introspection via POST @ graphql-api.app.cineplex.de — conf 70, PASSIVE, KB-CONFIRMED, schema-only read-only
[FINAL] Staging GraphQL introspection @ graphql-api.app.staging.cineplex.de — conf 55, PASSIVE, cheaper than prod, env confusion value
[NEXT] PROBE: (1) GET https://data-9fc27eb430.cineplex.de/metrics — capture full body + Content-Type header (read-only, ≤1 rps); (2) GET https://data-9fc27eb430.cineplex.de/config — check for config disclosure; (3) GET https://data-9fc27eb430.cineplex.de/info — check for info endpoint; (4) GET https://data-9fc27eb430.cineplex.de/env — check for environment variables
[LEARN] ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 115 bytes — second authless 200 surface; content unexamined; not in REJECTED class
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 100+ sensitive mutations and PII-exposing queries
[LEARN] ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; now extended to GraphQL API via userById/searchUsers/adminUsers
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passive verification
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot password pages" as out of scope
[LEARN] REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
[LEARN] REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
[LEARN] REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
[RISK] cineplex: 8/100 — target "api" fully 403-gated at root; the only active attack surface is the franchise relay (`data-9fc27eb430.cineplex.de`, CNAME `cineplex-relay.iocnt.net`) which serves unauthenticated 200 JSON on `/health`, `/`, and now confirmed `/metrics` (115 bytes). The GraphQL production endpoint accepts introspection POST but root GET is WAF-blocked — schema enumeration is confirmed but the actual mutation/IDOR tests require live customer data which the program forbids. JWKS endpoint is 404 so passive JWT analysis is blocked. Remaining live hosts (`profil`, `support`, `mailing`, `vpn-portal`) are third-party managed (Zammad, Mailjet, ntxzone) and carry low inherent risk. Program explicitly forbids exposing customer/employee/financial/auth data during testing, which eliminates the highest-value IDOR/mutation probes without a test/sandbox account or explicit consent. The relay `/metrics` endpoint is the highest-priority immediate probe — 115 bytes of unexamined content on an authless surface may contain internal topology useful for relay SSRF chaining.
## 2026-09-04 21:34:17 UTC [target] (model bigpickle)
[HYP] GraphQL IDOR via userById/searchUsers/adminUsers with valid JWT
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 85
reasoning: KB CONFIRMED full introspection via POST (200, 200+ types, 100+ Query fields incl. userById/searchUsers/adminUsers/currentUser). User type exposes email, fullName, telephone, birthDate, street, city, zipCode, orders, invoices, vouchers. IDOR/BOLA is explicitly prioritized in directives. No active mutation/query against live data was performed; per program rule exposing customer PII during testing is out of scope.
evidence_needed: (1) Valid session JWT obtainable (login mutation returns jwt/refreshToken/csrf); (2) userById(id) returns data for an account not belonging to the token's principal; (3) no authorization check between queried id and authenticated user.
verify_steps: (1) POST / with `{"query":"{__schema{queryType{name}}}"}` → 200 (already confirmed); (2) obtain test/sandbox account or explicit consent — HUMAN step; (3) WITH that account only, POST userById(otherUserId) and check cross-account response; (4) do NOT touch live customer records without consent.
impact: Cross-tenant PII dump (name, contact, birthDate, bookings, invoices, vouchers) → critical account/data compromise
testability: HUMAN_ONLY
[HYP] Staging GraphQL accepts introspection POST with relaxed WAF
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 55
reasoning: Prod root GET 403 but GraphQL POST 200 — WAF is method-gated. staging.cineplex.de and couat.cineplex.de exist as UAT siblings; staging env commonly mirrors schema with weaker auth. Same WAF rule likely (GET 403 confirmed) but POST untested on staging.
evidence_needed: POST with introspection query returns 200 and a schema; compare vs prod schema for auth-gate differences and test resolvers; presence of additional mutation fields not in prod.
verify_steps: (1) POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — `{"query":"{__schema{queryType{name}}}"}` — read-only ≤1 rps; (2) repeat for graphql-api.app.couat.cineplex.de; (3) diff mutation/query field lists vs prod; (4) read-only only — no mutating queries.
impact: Schema/env confusion → test-scope exposure aiding targeted exploits in prod; medium if schema-only
testability: PASSIVE
[HYP] IOMB relay exposes realtime publish/subscribe channel without auth
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 35
reasoning: /metrics reveals mode IOMB (IO Message Broker), 164M messages queued, active producer. A broker used to stream realtime data (seat/booking/pricing/signage feeds) may expose a WebSocket/stream gateway. HTTP analogues /publish /subscribe /stream /events all 404; server is Google-fronted (via: 1.1 google, alt-svc h3) which typically blocks arbitrary Upgrade/socket routing.
evidence_needed: WSS handshake success returning non-404 upstream frames; discovery of a stream path via error/redirect message in response body.
verify_steps: (1) GET / with headers Connection: Upgrade + Upgrade: websocket + Sec-WebSocket-Key → observe response (read-only, no data written); (2) HEAD the same paths already probed; (3) do NOT attempt to publish or subscribe to any channel.
impact: Unauthenticated subscription to realtime franchise feed (potential PII/booking events) → medium-high if channel exists; none if behind auth
testability: PASSIVE
[NEXT] PROBE: POST https://graphql-api.app.staging.cineplex.de/ — Header `Content-Type: application/json` — Body `{"query":"{__schema{queryType{name}}}"}` — read-only introspection, ≤1 rps — then repeat for graphql-api.app.couat.cineplex.de
[RISK] cineplex: 6/100 — relay HTTP surface is now fully enumerated and low-value (broker queue stats only; all routes 404), so the only confirmed high-value finding (production GraphQL introspection + schema) is LIVE but its exploitation (IDOR via userById/searchUsers) requires a sanctioned account due to program PII restrictions → HUMAN_ONLY. Remaining actionable passive lead is staging/couat env-confusion introspection. No authless SSRF surface found; JWT passive analysis blocked by JWKS 404.
## 2026-09-04 23:18:46 UTC [target] (model bigpickle)
[HYP] Testing-only confirmation-code oracle / forced-delete shipped to production GraphQL
class: AUTH
asset: graphql-api.app.cineplex.de
confidence: 72
reasoning: PROD schema (my live introspection: POST 200, GET?query= 200) exposes `testing_getConfirmationCode(email, ConfirmationCodeType)` where type ∈ LOGIN_CREATION|EMAIL_CHANGE|PASSWORD_RESET, and `testing_forceDeleteUser(email)` — email-arg only, no token arg. If the resolver is wired in the prod Lambda (same `/var/task/graphql.js` monolith, schema identical to staging), an unauthenticated attacker obtains PASSWORD_RESET/EMAIL_CHANGE confirmation codes for any email without mailbox access = silent ATO, and/or deletes arbitrary accounts. Execution was NOT attempted (mutates/looks up auth data → program out-of-scope).
evidence_needed: anonymous call to `{testing_getConfirmationCode(email:"<sandbox>",type:"PASSWORD_RESET")}` returns a code without session → schema-to-resolver wiring confirmed on prod
verify_steps: (1) obtain program consent or test/sandbox account — HUMAN step; (2) ONLY with sanctioned test email, POST `{"query":"query{testing_getConfirmationCode(email:\"<sandbox>\",type:\"PASSWORD_RESET\")}"}` to prod and staging; (3) do NOT use any real customer email; (4) compare response presence vs gate error
impact: silent ATO via password-reset/email-change code oracle, bulk account destruction; critical if wired, config/disclosure if schema-only
testability: HUMAN_ONLY
[HYP] Publicly reachable staging GraphQL with identical schema + test resolvers (env confusion)
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 60
reasoning: Staging POST introspection 200 with full Query(83)/Mutation(140) surface identical to prod, served on Cloudflare with no IP allow-listing; `testing_*` resolvers present here too. Staging is a sanctioned proving ground — the cheapest place to prove or disprove the testing_* resolver wiring without touching prod customer data (mutations on live customer data still forbidden).
evidence_needed: same sandbox-email test on staging returns a code → resolver actively resolves in a test env with same codebase as prod
verify_steps: (1) program consent for staging-only test; (2) POST `testing_getConfirmationCode` with a disposable/sandbox email on staging; (3) if 200+code, report as staging-live + prod-present schema evidence; (4) if gate error, schema-vs-resolver drift is itself the finding
impact: proves prod backdoor plausibility; staging is externally reachable test tooling with destructive ops; medium-high
testability: HUMAN_ONLY
[HYP] IOMB relay metrics queue-depth disclosure
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 35
reasoning: /metrics body (captured) = `{"mode":"IOMB","writer":{"queue_length":0,"queue_capacity":30000,"messages_queued":167863188,"messages_dropped":0}}` — 167.8M backlog signals broker saturation but leaks no hostname/route/upstream; single-metric, low sensitivity, borderline descriptive class
evidence_needed: metrics gaining sensitive fields or authless sub-endpoint (everything else already 404)
verify_steps: (1) volume vs latency drift on /metrics over cycles; (2) no further value expected — keep parked
impact: negligible alone; only relevant as a breadcrumb if broker auth is later probed
testability: PASSIVE
## 2026-09-05 01:04:57 UTC [target] (model bigpickle)
[HYP] Staging GraphQL mirrors prod destructive mutation surface with no network gate
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 62
reasoning: POST introspection → 200 (verified again this cycle); query fields 83 and mutation fields 140 are set-equal to prod. Staging surface includes login, requestPasswordReset, changePassword, updateUserAdminStatus, deleteUser, deleteCineplexUser, deleteCompanies, increaseUserTestingStatus, sendTestEmail. Root GET 403 is WAF-only. No client-cert/IP allow-list (introspection answered from this vantage). Same /var/task monolith codebase pattern as prod Lambda.
evidence_needed: resolver parity proof — a sandbox-email call returning 200 vs a role-gate error on the same mutation on staging
verify_steps: (1) [DONE] POST `{"query":"{__schema{queryType{fields{name}}}}"}` → 200 83Q set-equal prod; (2) obtain program consent + disposable sandbox email — HUMAN; (3) staging-only: call increaseUserTestingStatus/sendTestEmail/requestPasswordReset with that email; compare gate vs arg error; (4) never on live customer data.
impact: externally reachable test tooling with destructive/admin mutations sharing prod codebase → env-confusion stepping stone to mass user manipulation if any resolver skips role-gating; medium-high
testability: HUMAN_ONLY (schema parity PASSIVE-confirmed)
[NEXT] HUMAN: request program consent + two disposable sandbox accounts from bugs.olivermaicher.eu — then (a) staging-only validation of increaseUserTestingStatus/sendTestEmail/requestPasswordReset / deleteUser on the sandbox email to prove resolver wiring vs role gates, and (b) prod two-account IDOR check of userById/searchUsers with the sanctioned accounts. Passive surface is exhausted; no further high-value read-only probe exists.
[RISK] cineplex: 35/100 — current confirmed findings are real but schema-level: GraphQL introspection enabled on PROD and STAGING, exposing PII-bearing queries (userById, adminUsers, searchUsers, userByQr, voucherInstanceByQR, invoice) and destructive mutations (deleteUser, updateUserAdminStatus), with build-identical test envs publicly reachable. Exploitation (IDOR/BOLA, test-mutation/resolver abuse) is blocked to HUMAN_ONLY by the program's customer-data/consent rule and requires sanctioned credentials; relay fully enumerated at low value; JWT analysis blocked by JWKS absence. Bulk of reportable impact hinges on obtaining a test/sandbox account.
## 2026-09-05 05:50:23 UTC [target] (model bigpickle)
[HYP] couat GraphQL accepts introspection POST and exposes schema differing from prod/staging
class: MISCONFIG
asset: graphql-api.app.couat.cineplex.de
confidence: 55
reasoning: couat is a sibling UAT env of staging (both in inventory); prod and staging both return root GET 403 (WAF) but GraphQL POST 200 with identical 83Q/140M schemas. couat shares the same WAF pattern expectation but POST was never tested and no schema was ever captured. If couat runs an older/newer build, the field diff pinpoints schema→env drift (e.g., `testing_*` fields present/absent).
evidence_needed: POST introspection returns 200 with a field list; diff vs the 83Q/140M baseline yields adding/removing mutations (notably testing_getConfirmationCode / testing_forceDeleteUser / deleteUser / updateUserAdminStatus density)
verify_steps: (1) POST https://graphql-api.app.couat.cineplex.de/ — Content-Type: application/json — `{"query":"{__schema{queryType{name}}}"}` — read-only ≤1 rps; (2) if 200, POST `{"query":"{__schema{queryType{fields{name}} mutationType{fields{name}}}}"}` and diff Q/M names vs stored prod/staging list; (3) no mutating calls
impact: schema/env drift adds evidence of non-prod code in prod (or backdoored fields present in UAT), strengthening the testing_* backdoor report; medium as schema-only, none if 403
testability: PASSIVE
[HYP] api.cineplex.de root GET 403 is WAF-gated while POST / subpaths reach a live gateway
class: MISCONFIG
asset: api.cineplex.de
confidence: 42
reasoning: the same edge WAF produced root GET 403 + GraphQL POST 200 on `graphql-api.app.*`; `api.cineplex.de` was only ever logged at root GET 403. As the canonical REST gateway, undirected subpaths (`/v1`, `/v2`, `/graphql`, `/api`, `/swagger`, `/openapi.json`) and POST method could present an authless 200 surface analogous to the sibling bypass. Not yet tested.
evidence_needed: any non-403 status on POST or a subpath; an OpenAPI/GraphQL schema object; an unauthenticated 200 JSON response
verify_steps: (1) GET https://api.cineplex.de/robots.txt and GET /v1/ and GET /graphql (read-only, ≤1 rps); (2) POST https://api.cineplex.de/graphql — Content-Type application/json — `{"query":"{__schema{queryType{name}}}"}`; (3) if any 200, enumerate schema exactly as on graphql-api.app; (4) no authentication-required or mutating requests
impact: if a GraphQL/REST discovery surface exists, broadens IDOR/BOLA reach (same directives); likely none if purely 403
testability: PASSIVE
[HYP] Production `testing_*` backdoor resolvers remain the top reportable finding, pending sandbox consent
class: AUTH
asset: graphql-api.app.cineplex.de
confidence: 72
reasoning: prod schema carries testing_getConfirmationCode(email, ConfirmationCodeType) and testing_forceDeleteUser(email) with 83Q/140M surface identical to staging; root GET 403 never blocked POST introspection, so the resolvers are plausibly wired in the same `/var/task/graphql.js` monolith. Execution is blocked to HUMAN_ONLY by program PII/consent rule — a structural gating constraint, not a technical one.
evidence_needed: sanctioned sandbox email call returning a code (resolver parity) — cannot be gathered passively
verify_steps: (1) obtain program consent + disposable sandbox email — HUMAN; (2) staging-only first: POST `{"query":"query{testing_getConfirmationCode(email:\"<sandbox>\",type:\"PASSWORD_RESET\")}"}`; (3) only on proof, prod with consent; never real customer data
impact: silent ATO via confirmation-code oracle (PASSWORD_RESET/EMAIL_CHANGE) and arbitrary account deletion; critical if wired, config/disclosure if schema-only
testability: HUMAN_ONLY
## 2026-09-05 09:52:31 UTC [target] (model bigpickle)
## 2026-09-05 13:14:21 UTC [target] (model bigpickle)
[NEW] `graphql-api.app.couat.cineplex.de/` — SSL handshake failure (SSLv3 alert) — new GraphQL host in inventory, previously unprobed
[NEW] `api.cineplex.de/graphql` — HTTP 403 — GraphQL endpoint exists on api.cineplex.de but WAF-gated (same pattern as graphql-api.app.cineplex.de)
[NEW] `api.cineplex.de/robots.txt` — request timeout — new endpoint tested
[CHANGED] `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31 — second authless 200 surface confirmed stable
[CHANGED] `graphql-api.app.cineplex.de/` — persistent 403 at root, GraphQL POST introspection CONFIRMED 200 with full schema (WAF bypass stable)
[CHANGED] `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
[CHANGED] `auth.cineplex.de/.well-known/jwks.json` — persistent 404 — passive JWKS fetch blocked for JWT alg confusion
[CHANGED] `booking.cineplex.de/api/booking/{id}` — persistent 403 — session-gated, AUTH_HELPED required
[PRIO] graphql-api.app.cineplex.de,9.2,attack_surface=10,business_value=10,tech_exposure=10,gate_ease=6,cloud_surface=8,freshness=10
[PRIO] graphql-api.app.staging.cineplex.de,8.45,attack_surface=9,business_value=8,tech_exposure=10,gate_ease=6,cloud_surface=8,freshness=10
[PRIO] data-9fc27eb430.cineplex.de,4.95,attack_surface=4,business_value=3,tech_exposure=2,gate_ease=10,cloud_surface=6,freshness=8
[PRIO] api.cineplex.de,4.9,attack_surface=3,business_value=7,tech_exposure=6,gate_ease=2,cloud_surface=5,freshness=7
[PRIO] graphql-api.app.couat.cineplex.de,0,attack_surface=0,business_value=0,tech_exposure=0,gate_ease=0,cloud_surface=0,freshness=0
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 85
reasoning: Prod schema includes userById, searchUsers, adminUsers queries that return PII (email, fullName, telephone, etc.). With a valid JWT, an attacker could query other users' data. IDOR/BOLA explicitly prioritized in directives.
evidence_needed: A valid JWT from a test account to query userById with a different user's ID.
verify_steps: (1) Obtain a test JWT via login mutation with test credentials; (2) POST GraphQL query `userById(id: "test-user-id")` with the JWT; (3) If returns PII of another user, IDOR confirmed.
impact: Mass PII exposure of customers; high severity.
testability: HUMAN_ONLY
[HYP] Staging GraphQL testing_* resolvers active with no role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 60
reasoning: Staging schema identical to prod, includes testing_getConfirmationCode, testing_forceDeleteUser resolvers. Staging may have weaker access controls, allowing unauthorized execution.
evidence_needed: Execution of testing_getConfirmationCode with a sandbox email returning a code.
verify_steps: (1) POST GraphQL mutation `testing_getConfirmationCode(email: "sandbox@test.com", type: "PASSWORD_RESET")` without auth; (2) If 200 and returns code, resolver is active.
impact: Account takeover via confirmation code oracle; high severity.
testability: HUMAN_ONLY
[HYP] Relay metrics queue-depth disclosure reveals internal architecture
class: MISCONFIG
asset: data-9fc27eb430.cineplex.de
confidence: 35
reasoning: /metrics returns JSON with queue_length, queue_capacity, messages_queued, messages_dropped. 167.8M messages queued suggests broker saturation, but no sensitive data.
evidence_needed: Metrics gaining sensitive fields (hostnames, routes, upstreams).
verify_steps: (1) Monitor /metrics over time for field changes; (2) No further value expected.
impact: Low; only relevant as breadcrumb if broker auth is probed.
testability: PASSIVE
[PARKED] Relay metrics queue-depth disclosure: confidence 35 < 40, impact negligible, no sensitive data exposed.
[FINAL] Production GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT (confidence 85, HUMAN_ONLY)
[FINAL] Staging GraphQL testing_* resolvers active with no role gating (confidence 60, HUMAN_ONLY)
[NEXT] HUMAN: Request program consent + two disposable sandbox accounts from bugs.olivermaicher.eu for staging-only testing of testing_* resolvers and prod two-account IDOR check.
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: CONFIRMED — full introspection enabled on production, returns 200 with complete schema including 100+ sensitive mutations and PII-exposing queries
[LEARN] ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized; extended to GraphQL API via userById/searchUsers/adminUsers — but testability HUMAN_ONLY per program PII rule
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized; login mutation returns jwt/refreshToken — but JWKS 404 limits passive verification
[LEARN] ACCEPTED relay_internal_disclosure @ data-9fc27eb430.cineplex.de: Live 200 JSON health/build surface on relay; not rejected; active infra; high discovery value
[LEARN] ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: GET /metrics returns 200 with 114-115 bytes — second authless 200 surface; content unexamined; not in REJECTED class
[LEARN] REJECTED grafana/metrics-only @ data-9fc27eb430.cineplex.de: confidence drops if only /health + build header confirmed with no other 200 surface (metrics-only leaks are borderline descriptive-header class)
[LEARN] ACCEPTED idor_relay @ data-9fc27eb430.cineplex.de: if undocumented relay API routes surface, IDOR/BOLA applies per directives
[LEARN] REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot password pages" as out of scope
[LEARN] REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
[LEARN] REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope
[LEARN] REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
[RISK] cineplex: 35/100 — current confirmed findings are real but schema-level: GraphQL introspection enabled on PROD and STAGING, exposing PII-bearing queries (userById, adminUsers, searchUsers, userByQr, voucherInstanceByQR, invoice) and destructive mutations (deleteUser, updateUserAdminStatus), with build-identical test envs publicly reachable. Exploitation (IDOR/BOLA, test-mutation/resolver abuse) is blocked to HUMAN_ONLY by the program's customer-data/consent rule and requires sanctioned credentials; relay fully enumerated at low value; JWT analysis blocked by JWKS absence. Bulk of reportable impact hinges on obtaining a test/sandbox account.
## 2026-09-05 16:08:19 UTC [target] (model bigpickle)
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 85
reasoning: Prod schema includes userById, searchUsers, adminUsers queries returning PII (email, fullName, telephone). IDOR/BOLA explicitly prioritized. Requires valid JWT (HUMAN_ONLY per PII/consent rule).
evidence_needed: A valid JWT from a test account to query userById with another user's ID.
verify_steps: (1) Obtain test JWT via login mutation with sanctioned test credentials; (2) POST GraphQL `userById(id:"test-id")` with JWT; (3) If returns other user's PII, IDOR confirmed.
impact: Mass customer PII exposure; high severity.
testability: HUMAN_ONLY
[HYP] Staging GraphQL testing_* resolvers active with no role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 60
reasoning: Staging schema identical to prod, includes testing_getConfirmationCode, testing_forceDeleteUser. Staging may lack access controls.
evidence_needed: Execution of testing_getConfirmationCode with sandbox email returning a code.
verify_steps: (1) POST GraphQL `testing_getConfirmationCode(email:"sandbox@test.com", type:"PASSWORD_RESET")` without auth; (2) If 200 with code, resolver active.
impact: Account takeover via confirmation-code oracle; high severity.
testability: HUMAN_ONLY
[HYP] Relay broker saturation indicates write-path DoS / message-tampering surface
class: OTHER
asset: data-9fc27eb430.cineplex.de
confidence: 20
reasoning: /metrics reveals IOMB writer with 273.9M messages queued against 30k capacity — massive overflow suggests broker saturation, but no authless route to inject/drain messages found; /routes /status /debug all 404. No sensitive data exposed.
evidence_needed: An authless route to read/inject queued message content.
verify_steps: Passive monitoring only; no active manipulation surface identified.
impact: None demonstrated; low.
testability: PASSIVE
[NEXT] HUMAN: Request program consent + two disposable sandbox accounts (or staging admin/test creds) from bugs.olivermaicher.eu to enable staged verification of the two HUMAN_ONLY finals: staging `testing_*` resolvers and prod two-account GraphQL IDOR.
[LEARN] ACCEPTED relay_metrics @ data-9fc27eb430.cineplex.de: /metrics body now examined and fully understood — internal IOMB broker architecture (mode IOMB, writer queue 30k capacity, 273.9M messages queued, 0 dropped), no PII/sensitive data; descriptive-infra info only, not reportable alone.
[LEARN] REJECTED relay_broker_saturation @ data-9fc27eb430.cineplex.de: 273.9M queued messages over 30k capacity is infra saturation with no exploitable authless manipulation surface; DoS class not applicable absent injection route; no sensitive data.
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" are out of scope — reaffirmed for /metrics infra disclosure.
[RISK] cineplex: 35/100 — Metrics surface now fully closed out (IOMB infra disclosure, descriptive-header class, no PII). Confirmed findings remain GraphQL introspection on PROD+STAGING exposing PII-bearing queries (userById, searchUsers, adminUsers, userByQr, voucherInstanceByQR, invoice) and destructive mutations (deleteUser, updateUserAdminStatus) with build-identical test envs reachable. Exploitation (IDOR/BOLA, test resolver/mutation abuse) blocked to HUMAN_ONLY by the program's customer-data/consent rule and requires sanctioned credentials; relay fully enumerated at low value; JWT analysis blocked by JWKS absence. Bulk of reportable impact still hinges on obtaining a test/sandbox account from the program.
## 2026-09-05 18:22:46 UTC [target] (model bigpickle)
[HYP] Staging GraphQL WAF method-gate bypass mirrors confirmed prod POST introspection
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 60
reasoning: Prod introspection confirmed via POST (200, full schema) while GET returns 403 — WAF is method-gated; staging shares the same graphql-api.app.*.cineplex.de build and the identical 403-on-GET posture across all probe cycles, but its POST path has never been tested (gap in probe-results)
evidence_needed: POST {"query":"{__schema{queryType{name}}}"} to staging returns 200 with parseable JSON schema (not 403)
verify_steps: (1) POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — body {"query":"{__schema{queryType{name}}}"} — read-only schema query, ≤1 rps, identical method/body class to the already-confirmed prod introspection; (2) on 200, request {"query":"{__schema{mutationType{fields{name}}}}"} and diff vs prod for testing_* / env-specific resolvers; (3) do NOT execute mutations or fetch any user/order/ticket records
impact: schema + testing_* resolver disclosure on a build-identical env; env-confusion breadcrumbs if staging shares secrets/DB endpoints with prod; medium
testability: PASSIVE
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers with Valid JWT
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 85
reasoning: Introspected schema exposes userById/searchUsers/adminUsers/userByQr/voucherInstanceByQR returning User PII (email, fullName, telephone, street); IDOR/BOLA explicitly prioritized by program; no ownership gate visible at schema level
evidence_needed: two-account proof — own JWT reading a second sandbox account's record via userById(otherId) returns PII
verify_steps: (1) obtain program consent + two disposable sandbox accounts; (2) login mutation → JWT; (3) userById(ownId) vs userById(otherId) compare; never touch live customer IDs
impact: mass cross-tenant PII dump, GDPR breach, account/data-theft primitive; critical
testability: HUMAN_ONLY
[HYP] JWT alg/key confusion on login-issued tokens (auth / GraphQL)
class: AUTH
asset: auth.cineplex.de
confidence: 45
reasoning: login mutation returns jwt+refreshToken+csrf; JWT alg confusion explicitly prioritized; auth.cineplex.de/.well-known/jwks.json 404 blocks passive key acquisition
evidence_needed: decode an issued JWT's alg header; a forged HS256/none token accepted by currentUser
verify_steps: (1) sanctioned test-login → capture token; (2) decode header (alg/kid); (3) if RS256, forge HS256-with-public-key and replay to currentUser — sandbox/consent only
impact: token forgery → full ATO across app/booking/profil/portal; critical
testability: AUTH_HELPED
[NEXT] PROBE: POST https://graphql-api.app.staging.cineplex.de/ — Content-Type: application/json — body {"query":"{__schema{queryType{name}}}"} — read-only schema introspection, ≤1 rps, same method/body class as the prod-confirmed introspection (triage run-2026-09-05-16-30 LEAD 2 HOLD); record status + body bytes + Content-Type; if 200, follow with mutationType fields diff vs prod and check for testing_* resolvers
[RISK] cineplex: 35/100 — Confirmed reportable finding stands (prod GraphQL introspection, schema-wide PII/mutation disclosure; 5.3 CVSS). Everything higher-severity (IDOR via userById/searchUsers/adminUsers conf 85, staging testing_* resolver abuse conf ~55, JWT forgery conf 45) is gated by the program's customer-data exclusion and requires consent+tests data that have not yet been requested; relay/JWKS/metrics paths fully closed at low value. Risk jumps materially only if (a) human obtains staging admin/test creds or two sandbox accounts, or (b) staging POST introspection now reveals env-confusion/testing_* mutation reachability.
## 2026-09-05 20:42:33 UTC [target] (model bigpickle)
## 2026-09-05 22:37:58 UTC [target] (model bigpickle)
[HYP] Staging testing_* confirmation-code oracle without role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 70
reasoning: schema now reachable (POST 200, conf 100%); queryType contains `testing_getConfirmationCode` and `testing_forceDeleteUser`; staging builds are routinely deployed without RBAC; no auth directive evident at schema level
evidence_needed: running `testing_getConfirmationCode` against a fabricated email returns a code (not auth/PERMISSION_DENIED error)
verify_steps: (1) POST `{"query":"query{testing_getConfirmationCode(email:\"probe-<nonce>@example.com\", type:\"PASSWORD_RESET\")}"}` to `https://graphql-api.app.staging.cineplex.de/` ≤1 rps; (2) response containing a code → RESOLVER UNGATED → escalate to HUMAN for consent before any real-email use; (3) auth error / null → role-gated or inert
impact: account-takeover primitive via reset-code oracle for any email (staging; prod if parity confirmed); high severity
testability: HUMAN_ONLY (execution needs consent; fabricated email only)
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers with valid JWT
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 85
reasoning: prod schema confirmed exposes `userById`/`searchUsers`/`adminUsers`→User PII (email, fullName, telephone, street, birthDate); no ownership gate at schema level; IDOR/BOLA explicitly prioritized
evidence_needed: two-account proof — own JWT reading a second sandbox account via `userById(otherId)`
verify_steps: (1) program consent + two disposable sandbox accounts; (2) `login` mutation → JWT; (3) `userById(ownId)` vs `userById(otherId)` PII comparison; never live customer IDs
impact: cross-tenant mass PII dump, GDPR breach; critical
testability: HUMAN_ONLY
[HYP] Staging admin/destructive mutations role-gated weaker than prod
class: MISCONFIG
asset: graphql-api.app.staging.cineplex.de
confidence: 50
reasoning: staging exposes `updateUserAdminStatus`, `deleteUser`, `deleteCineplexUser`, `sendTestNotification`, `saveImagePath` with no auth directive in schema; build-identical envs often share service accounts with laxer RBAC
evidence_needed: an unauthenticated or low-privilege call to a non-destructive sentinel (`increaseUserTestingStatus` with own id) differing from prod authorization behavior
verify_steps: (1) obtain staging test JWT (HUMAN consent); (2) call `increaseUserTestingStatus` sentinel, compare status vs prod; (3) only if sentinel passes, ENTITY review of delete/admin surface — no live-data mutation
impact: admin/user data manipulation, mass deletion on staging that shares backends; high
testability: HUMAN_ONLY
[NEXT] PROBE: POST `https://graphql-api.app.staging.cineplex.de/` — `Content-Type: application/json` — body `{"query":"query{testing_getConfirmationCode(email:\"probe-<urandom-nonce>@example.com\", type:\"PASSWORD_RESET\")}"}` — read-only schema-level check of role gating, fabricated non-existent email only, ≤1 rps; 200-with-code → confirm oracle and escalate to HUMAN for consent; auth/PERMISSION_DENIED/null → role-gated or inert, downgrade hypothesis
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.staging.cineplex.de: POST introspection returns 200 with full schema (140 mutations, 83 queries) — WAF method-gate bypass (GET 403/POST 200) mirrors prod exactly; no env-specific WAF strength.
[LEARN] ACCEPTED staging_sensitive_parity @ graphql-api.app.staging.cineplex.de: staging queryType contains userById/searchUsers/adminUsers/userByQr/voucherInstanceByQR/invoice + testing_getConfirmationCode/testing_forceDeleteUser; PII surface identical to prod at schema level.
[LEARN] REJECTED app.staging.cineplex.de @ TLS-dead: SSLv3 handshake failure — no web surface reachable; not pursuable.
[RISK] cineplex: **45/100** — Staging GraphQL surface now confirmed reachable with full PII-bearing queries and `testing_*` account-oracle resolvers on a build-identical env, adding a genuinely new exploitable-pipeline candidate. Reportable finding unchanged (prod introspection, 5.3 CVSS). Automation ceiling reached: the two highest-impact paths (conf 85 prod IDOR, conf 70 staging testing_* oracle) both terminate at HUMAN consent + sandbox/test data, which has not yet been requested from bugs.olivermaicher.eu. Risk jumps to 60+ only if consent unlocks either oracle confirmation or two-account IDOR proof.
## 2026-09-06 00:13:32 UTC [target] (model bigpickle)
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers — resolver auth gate absent
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 88
reasoning: `currentUser` (no token) → UNAUTHENTICATED, but `userById` with fabricated ID reaches `decodePublicId` (INVALID_ID) — ID decode runs BEFORE any auth check on prod AND staging (probe 2026-09-06, HTTP 200 both). Schema exposes userById→User(email, fullName, telephone, street, birthDate). No directive/app-level gate visible pre-decode.
evidence_needed: two-account proof — own JWT reading second sandbox account via `userById(otherId)` returns PII
verify_steps: (1) program consent + two disposable sandbox accounts; (2) `login` mutation → JWT; (3) `userById(ownId)` vs `userById(otherId)`; never real customer IDs; (4) treat any PII response as report-only
impact: mass cross-tenant PII dump, GDPR breach; critical
testability: HUMAN_ONLY
[HYP] Staging testing_* confirmation-code oracle without role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 70
reasoning: staging introspection (POST 200) exposes `testing_getConfirmationCode`/`testing_forceDeleteUser`; build-identical to prod per userById gate-parity probe; no auth directive at schema level
evidence_needed: `testing_getConfirmationCode` on fabricated email returns code (not auth/PERMISSION_DENIED)
verify_steps: (1) consent; (2) POST `{"query":"query{testing_getConfirmationCode(email:\"probe-<nonce>@example.com\",type:\"PASSWORD_RESET\")}"}` ≤1 rps; (3) code → oracle confirmed; auth error → gated
impact: reset-code oracle → ATO primitive if prod parity; high
testability: HUMAN_ONLY
[HYP] JWT alg/key confusion on login-issued tokens
class: AUTH
asset: auth.cineplex.de
confidence: 45
reasoning: login mutation returns jwt+refreshToken+csrf; alg confusion prioritized; JWKS 404 blocks passive key fetch
evidence_needed: issued token's alg header; forged HS256-with-public-key accepted by currentUser
verify_steps: consent + test login → decode header → forge if RS256; sandbox only
impact: token forgery → ATO; critical
testability: AUTH_HELPED
[NEXT] HUMAN: Request bugs.olivermaicher.eu consent for (a) two disposable sandbox accounts to prove `userById`/`searchUsers`/`adminUsers` IDOR and (b) one fabricated-email execution of `testing_getConfirmationCode` on staging — cite prod+staging `userById` resolving past the auth gate (INVALID_ID at `decodePublicId`, never UNAUTHENTICATED, HTTP 200 both).
[RISK] cineplex: 52/100 — Reportable finding unchanged (prod introspection, 5.3 CVSS). New signal this cycle materially strengthens the top hypothesis: `userById` demonstrably bypasses the auth gate (vs gated `currentUser`) on both prod and staging, raising IDOR conf to 88. Absolute ceiling reached short of consent: every remaining confirm (prod two-account IDOR, staging oracle) is HUMAN_ONLY; automation adds no further lift without exceeding program customer-data rules. Jumps to 65+ only if consent unlocks oracle/IDOR proof.
## 2026-09-06 04:48:37 UTC [target] (model bigpickle)
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers — resolver auth gate absent
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 88
reasoning: Re-confirmed 2026-09-06 04:47 UTC over GET — `userById` fabricated ID returns `INVALID_ID` from `decodePublicId`, resolves past auth while `currentUser` (no token) returns UNAUTHENTICATED; schema maps `userById`→User(email, fullName, telephone, street, birthDate); no directive in schema; IDOR/BOLA prioritized.
evidence_needed: two-account proof — own JWT reading second sandbox account via `userById(otherId)` returns PII.
verify_steps: (1) consent + two disposable sandbox accounts; (2) `login` mutation → JWT; (3) GET `?query={userById(id:"<otherId>"){email,fullName}}` vs own-id response; never live IDs.
impact: cross-tenant mass PII dump / GDPR breach; critical
testability: HUMAN_ONLY
[HYP] Staging testing_* confirmation-code oracle without role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 72
reasoning: Staging introspection exposes `testing_getConfirmationCode`/`testing_forceDeleteUser`; gate-skip parity with prod now shown on two methods (POST prior, GET now: INVALID_ID, not UNAUTHENTICATED); no auth directive at schema level; build-identical envs routinely ship laxer RBAC.
evidence_needed: `testing_getConfirmationCode` on fabricated email returns a code (not auth/PERMISSION_DENIED).
verify_steps: (1) consent; (2) GET `?query={testing_getConfirmationCode(email:"probe-<nonce>@example.com",type:"PASSWORD_RESET")}` ≤1 rps; (3) code → oracle; auth error → gated.
impact: reset-code oracle → ATO primitive if backend parity holds; high
testability: HUMAN_ONLY
[HYP] JWT alg/key confusion on login-issued tokens
class: AUTH
asset: auth.cineplex.de
confidence: 45
reasoning: `login` mutation returns jwt+refreshToken+csrf; alg confusion prioritized; JWKS 404 blocks passive key fetch.
evidence_needed: issued token `alg` header; forged HS256-with-public-key accepted by `currentUser`.
verify_steps: consent + test login → decode header → forge if RS256; sandbox only.
impact: token forgery → ATO; critical
testability: AUTH_HELPED
[NEXT] HUMAN: submit `bugs.olivermaicher.eu` consent request for (a) two disposable sandbox accounts to prove `userById`/`searchUsers`/`adminUsers` IDOR and (b) one fabricated-email `testing_getConfirmationCode` execution on staging — cite re-confirmed gate-skip on prod AND staging over GET+POST (INVALID_ID at `decodePublicId`, never UNAUTHENTICATED, HTTP 200 both, 2026-09-06) plus active WAF method-gate attenuation as fresh evidence.
[RISK] cineplex: 55 — WAF method-gate attenuation broadens an already-open GraphQL surface but adds no new reportable class; reportable unchanged (prod introspection, 5.3). Fresh gate-skip re-confirmation raises IDOR confidence basis but both decisive paths (prod two-account IDOR 88, staging oracle 72) remain consent-gated; jumps to 65+ only if consent unlocks oracle/IDOR proof.
## 2026-09-06 09:08:17 UTC [target] (model bigpickle)
class: AUTH
asset: auth.cineplex.de
confidence: 45
reasoning: login mutation returns jwt+refreshToken+csrf; alg confusion prioritized; JWKS 404 blocks passive key fetch
evidence_needed: issued token's alg header; forged HS256-with-public-key accepted by currentUser
verify_steps: consent + test login → decode header → forge if RS256; sandbox only
impact: token forgery → ATO; critical
testability: AUTH_HELPED
[NEXT] HUMAN: Request bugs.olivermaicher.eu consent for (a) two disposable sandbox accounts to prove `userById`/`searchUsers`/`adminUsers` IDOR and (b) one fabricated-email execution of `testing_getConfirmationCode` on staging — cite prod+staging `userById` resolving past the auth gate (INVALID_ID at `decodePublicId`, never UNAUTHENTICATED, HTTP 200 both).
[RISK] cineplex: 52/100 — Reportable finding unchanged (prod introspection, 5.3 CVSS). New signal this cycle materially strengthens the top hypothesis: `userById` demonstrably bypasses the auth gate (vs gated `currentUser`) on both prod and staging, raising IDOR conf to 88. Absolute ceiling reached short of consent: every remaining confirm (prod two-account IDOR, staging oracle) is HUMAN_ONLY; automation adds no further lift without exceeding program customer-data rules. Jumps to 65+ only if consent unlocks oracle/IDOR proof.
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers — resolver auth gate absent
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 88
reasoning: Re-confirmed 2026-09-06 04:47 UTC over GET — `userById` fabricated ID returns `INVALID_ID` from `decodePublicId`, resolves past auth while `currentUser` (no token) returns UNAUTHENTICATED; schema maps `userById`→User(email, fullName, telephone, street, birthDate); no directive in schema; IDOR/BOLA prioritized.
evidence_needed: two-account proof — own JWT reading second sandbox account via `userById(otherId)` returns PII.
verify_steps: (1) consent + two disposable sandbox accounts; (2) `login` mutation → JWT; (3) GET `?query={userById(id:"<otherId>"){email,fullName}}` vs own-id response; never live IDs.
impact: cross-tenant mass PII dump / GDPR breach; critical
testability: HUMAN_ONLY
[HYP] Staging testing_* confirmation-code oracle without role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 72
reasoning: Staging introspection exposes `testing_getConfirmationCode`/`testing_forceDeleteUser`; gate-skip parity with prod now shown on two methods (POST prior, GET now: INVALID_ID, not UNAUTHENTICATED); no auth directive at schema level; build-identical envs routinely ship laxer RBAC.
evidence_needed: `testing_getConfirmationCode` on fabricated email returns a code (not auth/PERMISSION_DENIED).
verify_steps: (1) consent; (2) GET `?query={testing_getConfirmationCode(email:"probe-<nonce>@example.com",type:"PASSWORD_RESET")}` ≤1 rps; (3) code → oracle; auth error → gated.
impact: reset-code oracle → ATO primitive if backend parity holds; high
testability: HUMAN_ONLY
[HYP] JWT alg/key confusion on login-issued tokens
class: AUTH
asset: auth.cineplex.de
confidence: 45
reasoning: `login` mutation returns jwt+refreshToken+csrf; alg confusion prioritized; JWKS 404 blocks passive key fetch.
evidence_needed: issued token `alg` header; forged HS256-with-public-key accepted by `currentUser`.
verify_steps: consent + test login → decode header → forge if RS256; sandbox only.
impact: token forgery → ATO; critical
testability: AUTH_HELPED
[NEXT] HUMAN: submit `bugs.olivermaicher.eu` consent request for (a) two disposable sandbox accounts to prove `userById`/`searchUsers`/`adminUsers` IDOR and (b) one fabricated-email `testing_getConfirmationCode` execution on staging — cite re-confirmed gate-skip on prod AND staging over GET+POST (INVALID_ID at `decodePublicId`, never UNAUTHENTICATED, HTTP 200 both, 2026-09-06) plus active WAF method-gate attenuation as fresh evidence.
[RISK] cineplex: 55 — WAF method-gate attenuation broadens an already-open GraphQL surface but adds no new reportable class; reportable unchanged (prod introspection, 5.3). Fresh gate-skip re-confirmation raises IDOR confidence basis but both decisive paths (prod two-account IDOR 88, staging oracle 72) remain consent-gated; jumps to 65+ only if consent unlocks oracle/IDOR proof.
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers — resolver auth gate absent
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 88
reasoning: Re-confirmed 2026-09-06 04:47 UTC over GET — `userById` fabricated ID returns `INVALID_ID` from `decodePublicId`, resolves past auth while `currentUser` (no token) returns UNAUTHENTICATED; schema maps `userById`→User(email, fullName, telephone, street, birthDate); no directive in schema; IDOR/BOLA prioritized.
evidence_needed: two-account proof — own JWT reading second sandbox account via `userById(otherId)` returns PII.
verify_steps: (1) consent + two disposable sandbox accounts; (2) `login` mutation → JWT; (3) GET `?query={userById(id:"<otherId>"){email,fullName}}` vs own-id response; never live IDs.
impact: cross-tenant mass PII dump / GDPR breach; critical
testability: HUMAN_ONLY
[HYP] Staging testing_* confirmation-code oracle without role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 72
reasoning: Staging introspection exposes `testing_getConfirmationCode`/`testing_forceDeleteUser`; gate-skip parity with prod now shown on two methods (POST prior, GET now: INVALID_ID, not UNAUTHENTICATED); no auth directive at schema level; build-identical envs routinely ship laxer RBAC.
evidence_needed: `testing_getConfirmationCode` on fabricated email returns a code (not auth/PERMISSION_DENIED).
verify_steps: (1) consent; (2) GET `?query={testing_getConfirmationCode(email:"probe-<nonce>@example.com",type:"PASSWORD_RESET")}` ≤1 rps; (3) code → oracle; auth error → gated.
impact: reset-code oracle → ATO primitive if backend parity holds; high
testability: HUMAN_ONLY
[HYP] JWT alg/key confusion on login-issued tokens
class: AUTH
asset: auth.cineplex.de
confidence: 45
reasoning: `login` mutation returns jwt+refreshToken+csrf; alg confusion prioritized; JWKS 404 blocks passive key fetch.
evidence_needed: issued token `alg` header; forged HS256-with-public-key accepted by `currentUser`.
verify_steps: consent + test login → decode header → forge if RS256; sandbox only.
impact: token forgery → ATO; critical
testability: AUTH_HELPED
[NEXT] HUMAN: submit `bugs.olivermaicher.eu` consent request for (a) two disposable sandbox accounts to prove `userById`/`searchUsers`/`adminUsers` IDOR and (b) one fabricated-email `testing_getConfirmationCode` execution on staging — cite re-confirmed gate-skip on prod AND staging over GET+POST (INVALID_ID at `decodePublicId`, never UNAUTHENTICATED, HTTP 200 both, 2026-09-06) plus active WAF method-gate attenuation as fresh evidence.
[RISK] cineplex: 55 — WAF method-gate attenuation broadens an already-open GraphQL surface but adds no new reportable class; reportable unchanged (prod introspection, 5.3). Fresh gate-skip re-confirmation raises IDOR confidence basis but both decisive paths (prod two-account IDOR 88, staging oracle 72) remain consent-gated; jumps to 65+ only if consent unlocks oracle/IDOR proof.
verify_steps: consent + test login → decode header → forge if RS256; sandbox only.
impact: token forgery → ATO; critical
testability: AUTH_HELPED
[NEXT] HUMAN: submit `bugs.olivermaicher.eu` consent request for (a) two disposable sandbox accounts to prove `userById`/`searchUsers`/`adminUsers` IDOR and (b) one fabricated-email `testing_getConfirmationCode` execution on staging — cite re-confirmed gate-skip on prod AND staging over GET+POST (INVALID_ID at `decodePublicId`, never UNAUTHENTICATED, HTTP 200 both, 2026-09-06) plus active WAF method-gate attenuation as fresh evidence.
[RISK] cineplex: 55 — WAF method-gate attenuation broadens an already-open GraphQL surface but adds no new reportable class; reportable unchanged (prod introspection, 5.3). Fresh gate-skip re-confirmation raises IDOR confidence basis but both decisive paths (prod two-account IDOR 88, staging oracle 72) remain consent-gated; jumps to 65+ only if consent unlocks oracle/IDOR proof.
[HYP] Production GraphQL IDOR via userById/searchUsers/adminUsers — resolver auth gate absent
class: IDOR
asset: graphql-api.app.cineplex.de
confidence: 91
reasoning: Fresh delta 2026-09-06 09:07 UTC — root GET status changed 403→400 on BOTH prod and staging, now returning native Express/API-Gateway body ("GET query missing.", x-powered-by: Express, x-amzn-apigw-id) instead of Cloudflare 403. This lifts the WAF method-gate: GET with `?query=` now reaches the backend authlessly. Verified GET probes: `currentUser` (no token)→UNAUTHENTICATED on prod; `userById(id:"fake")`→INVALID_ID at decodePublicId (past auth, no UNAUTHENTICATED) on prod AND staging. Prepends direct GET (not just POST-introspection) as the reachable gate-skip; IDOR/BOLA prioritized.
evidence_needed: two-account proof — own JWT reading second sandbox account via `userById(otherId)` returns PII.
verify_steps: (1) consent + two disposable sandbox accounts; (2) `login` mutation → JWT; (3) GET `?query={userById(id:"<otherId>"){email,fullName}}` vs own-id; never live IDs.
impact: cross-tenant mass PII dump / GDPR breach; critical
testability: HUMAN_ONLY
[HYP] Staging testing_* confirmation-code oracle without role gating
class: AUTH
asset: graphql-api.app.staging.cineplex.de
confidence: 74
reasoning: Same gate-skip 403→400 attenuation now confirmed on staging root (native Express response 2026-09-06 09:07); `userById(fake)`→INVALID_ID over plain GET, not UNAUTHENTICATED. Staging introspection exposes `testing_getConfirmationCode`/`testing_forceDeleteUser`; no auth directive at schema level.
evidence_needed: `testing_getConfirmationCode` on fabricated email returns a code (not auth/PERMISSION_DENIED).
verify_steps: (1) consent; (2) GET `?query={testing_getConfirmationCode(email:"probe-<nonce>@example.com",type:"PASSWORD_RESET")}` ≤1 rps; (3) code → oracle; auth error → gated.
impact: reset-code oracle → ATO primitive if backend parity holds; high
testability: HUMAN_ONLY
[HYP] JWT alg/key confusion on login-issued tokens
class: AUTH
asset: auth.cineplex.de
confidence: 45
reasoning: `login` mutation returns jwt+refreshToken+csrf; alg confusion prioritized; JWKS 404 blocks passive key fetch.
evidence_needed: issued token `alg` header; forged HS256-with-public-key accepted by `currentUser`.
verify_steps: consent + test login → decode header → forge if RS256; sandbox only.
impact: token forgery → ATO; critical
testability: AUTH_HELPED
[NEXT] HUMAN: submit `bugs.olivermaicher.eu` consent request for (a) two disposable sandbox accounts to prove `userById`/`searchUsers`/`adminUsers` IDOR and (b) one fabricated-email `testing_getConfirmationCode` execution on staging — NEW evidence 2026-09-06 09:07: root GraphQL GET 403→400 on prod AND staging (native Express "GET query missing." body, x-powered-by: Express, x-amzn-apigw-id), direct authless GET reach; `userById(fake)`→INVALID_ID past auth gate; `currentUser`(no token)→UNAUTHENTICATED. Single GET with valid JWT now suffices to prove IDOR.
[RISK] cineplex: 60 — Reportable unchanged (prod introspection 5.3), but the 403→400 WAF attenuation materially strengthens the POC case for the top IDOR hypothesis (conf 88→91): the GraphQL backend is now directly reachable over plain GET with no WAF method-gate, and the auth-gate gap (userById vs currentUser) is demonstrably present on both prod and staging. Decisive proof (two-account IDOR, staging oracle) still HUMAN_ONLY consent-gated; automation ceiling reached without exceeding customer-PII rules.
