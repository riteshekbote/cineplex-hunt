## 2026-09-03 15:49:11 UTC [target] (model nemotron3)
[NEW] 132 hosts in inventory from passive DNS/CT (seed 2026-09-02)
[NEW] 6 live HTTP hosts confirmed: `cloud.systems.cineplex.de`, `data-9fc27eb430.cineplex.de`, `profil.cineplex.de`, `support.systems.cineplex.de`, `mailing.cineplex.de`, `vpn-portal.systems.cineplex.de`
[NEW] 8 CNAME signals to third-party: `your-storageshare.de`, `cineplex-relay.iocnt.net`, `azurecontainerapps.io`, `showtimeanalytics.com`, `zammad.com`, `mailjet.com`, `ntxzone.de` (2x)
[NEW] High-value API targets identified: `api.cineplex.de`, `graphql-api.app.cineplex.de`, `graphql-api.app.staging.cineplex.de`, `graphql-api.app.couat.cineplex.de`, `booking.cineplex.de`, `buchung.cineplex.de`
[NEW] Auth/identity surface: `auth.cineplex.de`, `login.cineplex.de`, `sso.cineplex.de`, `account.cineplex.de`, `my.cineplex.de`, `profil.cineplex.de`
[NEW] Staging/dev surface: `app.staging.cineplex.de`, `staging.cineplex.de`, `dev.cineplex.de`, `web-dev.cineplex.de`, `booking-dev.cineplex.de`, `buchung-dev.cineplex.de`, `bms-dev.cineplex.de`, `prelive.cineplex.de`, `uat.cineplex.de`, `test.cineplex.de`
[NEW] Customer-facing portals: `shop.cineplex.de`, `webshop.cineplex.de`, `tickets.cineplex.de`, `booking.cineplex.de`, `portal.cineplex.de`, `mobile.cineplex.de`, `app.cineplex.de`
[NEW] Admin/internal: `admin.cineplex.de`, `dashboard.cineplex.de`, `cms.cineplex.de`, `ci.cineplex.de`, `jenkins.cineplex.de`, `jira.systems.cineplex.de`
[NEW] VPN/remote access: `vpn-portal.systems.cineplex.de`, `vpn-openvpn-cpz.systems.cineplex.de`
[NEW] Regional cinema sites (potential multi-tenant): 20+ location subdomains (aichach, bayreuth, eisenach, frankfurt, etc.)
[HYP] GraphQL Introspection & Unauthorized Mutations on Production API
class: OTHER
asset: graphql-api.app.cineplex.de
confidence: 75
reasoning: GraphQL endpoints frequently expose introspection in production; staging counterpart (graphql-api.app.staging.cineplex.de) exists suggesting shared schema; no auth required for introspection query; mutations for booking/payment may lack proper authorization checks
evidence_needed: Introspection query returns full schema; mutation (e.g., createBooking, modifyPayment) succeeds without auth or with weak auth
verify_steps: GET https://graphql-api.app.cineplex.de/ with query `{__schema{types{name fields{name}}}}`; POST mutation `mutation{createBooking(input:{...}){id}}` with minimal headers
impact: Full API schema enumeration → discover hidden mutations → unauthorized booking creation/modification/cancellation → financial loss + PII access (Critical)
testability: PASSIVE
[HYP] IDOR/BOLA on Booking API — Cross-User Booking Access
class: IDOR
asset: booking.cineplex.de
confidence: 70
reasoning: Booking systems commonly use numeric/sequential booking IDs; `booking.cineplex.de` and `buchung.cineplex.de` (German) suggest multi-language deployment with shared backend; regional subdomains (e.g., `www.booking.cineplex.de`) indicate multi-tenant architecture; auth.cineplex.de/sso.cineplex.de centralize auth but booking endpoints may not validate ownership
evidence_needed: Booking reference/ID parameter (booking_id, order_id, reservation_id) accessible without ownership validation; changing ID returns other user's booking details (PII, seats, payment info)
verify_steps: GET https://booking.cineplex.de/api/booking/{id} (or /booking/{id}, /reservation/{id}) with valid session; iterate numeric IDs; check for 200 vs 403/404; test cross-user access with two test accounts
impact: Access to all customers' booking data (names, emails, phone, seats, payment partials) → PII dump + booking manipulation (High/Critical)
testability: AUTH_HELPED
[HYP] JWT Algorithm/Key Confusion on Central Auth (auth.cineplex.de / sso.cineplex.de)
class: AUTH
asset: auth.cineplex.de
confidence: 65
reasoning: Central auth endpoints (auth.cineplex.de, sso.cineplex.de, login.cineplex.de) likely issue JWTs for SSO across cineplex.de subdomains; multiple subdomains (app, booking, portal, my, profil) suggest shared token validation; algorithm confusion (RS256→HS256) or key confusion (public key as HMAC secret) possible if asymmetric signing used but validation accepts symmetric; `profil.cineplex.de` redirects to `/preference` (Showtime Analytics) indicating third-party integration with token sharing
evidence_needed: JWT from login shows `alg: RS256`; validation accepts HS256-signed token with public key; or JWKS endpoint exposes keys usable for forgery
verify_steps: GET https://auth.cineplex.de/.well-known/jwks.json (or /jwks, /keys); capture JWT from login flow; test alg:none, RS256→HS256, key confusion via crafted tokens against protected endpoint (e.g., profil.cineplex.de/preference)
impact: Forge valid tokens for any user → full ATO across all Cineplex properties (Critical)
testability: PASSIVE (JWKS fetch) + AUTH_HELPED (token capture)
[PARKED] GraphQL Introspection & Unauthorized Mutations on Production API: Confidence 75 but introspection alone is often disabled in production; need to confirm endpoint exists and responds — will probe first
[PARKED] IDOR/BOLA on Booking API — Cross-User Booking Access: Confidence 70 but requires valid session (AUTH_HELPED); booking endpoint path unknown — need discovery first
[PARKED] JWT Algorithm/Key Confusion on Central Auth: Confidence 65 but JWKS endpoint may not exist; token capture requires auth flow — lower priority for initial passive probe
[FINAL] Ranked survivors (all retained for now, ordered by testability × impact):
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ — Accept: application/json — body: `{"query":"{__schema{types{name fields{name}}}"}` — expect 200 with schema if introspection enabled, 400/403 if disabled
[LEARN] REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot password pages" as out of scope
[LEARN] REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
[LEARN] REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
[LEARN] REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized in directives
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized
[RISK] cineplex: 78 — Large attack surface (132 hosts, 6 live, 4 GraphQL endpoints, central auth, booking/payment flows, staging/dev exposure, third-party CNAMEs); high business value (ticketing, payments, PII, loyalty); multiple high-priority classes applicable (GraphQL, IDOR, JWT, SSRF-to-cloud via Azure Container Apps); wildcard-dominated DNS limits subdomain takeover but increases shared-infra risk
## 2026-09-03 19:05:33 UTC [target] (model nemotron3)
[PRIO] graphql-api.app.cineplex.de,8.8,attack_surface=9,business_value=9,tech_exposure=10,gate_ease=8,cloud_surface=6,freshness=9
[PRIO] booking.cineplex.de,8.3,attack_surface=9,business_value=9,tech_exposure=7,gate_ease=6,cloud_surface=7,freshness=8
[PRIO] auth.cineplex.de,8.0,attack_surface=8,business_value=10,tech_exposure=9,gate_ease=5,cloud_surface=5,freshness=8
[PRIO] api.cineplex.de,7.5,attack_surface=8,business_value=8,tech_exposure=8,gate_ease=7,cloud_surface=6,freshness=7
[PRIO] graphql-api.app.staging.cineplex.de,7.2,attack_surface=7,business_value=7,tech_exposure=10,gate_ease=8,cloud_surface=5,freshness=6
[PRIO] buchung.cineplex.de,7.0,attack_surface=7,business_value=8,tech_exposure=6,gate_ease=6,cloud_surface=6,freshness=7
[PRIO] sso.cineplex.de,6.8,attack_surface=7,business_value=9,tech_exposure=8,gate_ease=4,cloud_surface=4,freshness=7
[PRIO] profil.cineplex.de,6.5,attack_surface=6,business_value=7,tech_exposure=7,gate_ease=8,cloud_surface=8,freshness=6
[HYP] GraphQL Introspection Enabled on Production API
class: OTHER
asset: graphql-api.app.cineplex.de
confidence: 75
reasoning: GraphQL endpoint in inventory; staging counterpart exists suggesting shared schema; introspection commonly enabled in production misconfigurations; no prior probe confirmed status
evidence_needed: Introspection query returns full schema with types/fields; mutations visible in schema (createBooking, modifyPayment, cancelBooking)
verify_steps: GET https://graphql-api.app.cineplex.de/ — Accept: application/json — body: {"query":"{__schema{types{name fields{name}}}"}} — expect 200 with schema if enabled, 400/403 if disabled
impact: Full API schema enumeration → discover hidden mutations → unauthorized booking creation/modification/cancellation → financial loss + PII access (Critical)
testability: PASSIVE
[HYP] IDOR/BOLA on Booking API — Cross-User Booking Access via Numeric IDs
class: IDOR
asset: booking.cineplex.de
confidence: 70
reasoning: Booking systems use numeric/sequential IDs; booking.cineplex.de and buchung.cineplex.de share backend; regional subdomains indicate multi-tenant; central auth (auth.cineplex.de/sso.cineplex.de) but booking endpoints may not validate ownership
evidence_needed: Booking reference parameter (booking_id, order_id, reservation_id) returns other user's data without ownership check; 200 for unauthorized IDs vs 403/404
verify_steps: GET https://booking.cineplex.de/api/booking/{id} (test /booking/{id}, /reservation/{id}, /api/v1/booking/{id}) with valid session; iterate numeric IDs 1000-1010; check for 200 vs 403/404; compare responses across two test accounts
impact: Access to all customers' booking data (names, emails, phone, seats, payment partials) → PII dump + booking manipulation (High/Critical)
testability: AUTH_HELPED
[HYP] JWT Algorithm Confusion (RS256→HS256) on Central Auth
class: AUTH
asset: auth.cineplex.de
confidence: 65
reasoning: Central auth issues JWTs for SSO across subdomains (app, booking, portal, my, profil); multiple subdomains suggest shared token validation; profil.cineplex.de redirects to Showtime Analytics indicating third-party token sharing; asymmetric signing with public JWKS enables RS256→HS256 confusion if validation accepts symmetric
evidence_needed: JWKS endpoint exposes public keys; JWT from login shows alg:RS256; validation accepts HS256-signed token using public key as HMAC secret
verify_steps: GET https://auth.cineplex.de/.well-known/jwks.json (also /jwks, /keys); capture JWT from login flow; test alg:none, RS256→HS256 via crafted tokens against protected endpoint (e.g., profil.cineplex.de/preference)
impact: Forge valid tokens for any user → full ATO across all Cineplex properties (Critical)
testability: PASSIVE (JWKS fetch) + AUTH_HELPED (token capture)
[PARKED] GraphQL Introspection Enabled on Production API: Confidence 75 but introspection often disabled in production; need passive probe first to confirm endpoint responds
[PARKED] IDOR/BOLA on Booking API — Cross-User Booking Access via Numeric IDs: Confidence 70 but requires valid session (AUTH_HELPED); booking endpoint path unknown — need discovery first
[PARKED] JWT Algorithm Confusion (RS256→HS256) on Central Auth: Confidence 65 but JWKS endpoint may not exist; token capture requires auth flow — lower priority for initial passive probe
[FINAL] Ranked survivors (all retained, ordered by testability × impact):
[NEXT] PROBE: GET https://graphql-api.app.cineplex.de/ — Accept: application/json — Content-Type: application/json — body: {"query":"{__schema{types{name fields{name}}}"}} — expect 200 with schema if introspection enabled, 400/403 if disabled
[LEARN] REJECTED username_enumeration @ auth.cineplex.de/login.cineplex.de/sso.cineplex.de: Program explicitly lists "Username enumeration based on login or forgot password pages" as out of scope
[LEARN] REJECTED ssl_tls_best_practices @ all HTTPS endpoints: "SSL/TLS best practices" and "SSL attacks" are out of scope
[LEARN] REJECTED csrf_logout @ all endpoints: "CSRF on logout" is out of scope
[LEARN] REJECTED descriptive_errors @ all endpoints: "Descriptive error messages or headers" is out of scope
[LEARN] REJECTED known_vuln_library @ all: "Use of known-vulnerable library without exploit specific to implementation" is out of scope
[LEARN] ACCEPTED graphql_introspection @ graphql-api.app.cineplex.de: Not in rejected classes; high-value if enabled
[LEARN] ACCEPTED idor_booking @ booking.cineplex.de: IDOR/BOLA explicitly prioritized in directives
[LEARN] ACCEPTED jwt_alg_confusion @ auth.cineplex.de: JWT alg/key confusion explicitly prioritized
[RISK] cineplex: 78 — Large attack surface (132 hosts, 6 live, 4 GraphQL endpoints, central auth, booking/payment flows, staging/dev exposure, third-party CNAMEs); high business value (ticketing, payments, PII, loyalty); multiple high-priority classes applicable (GraphQL, IDOR, JWT, SSRF-to-cloud via Azure Container Apps); wildcard-dominated DNS limits subdomain takeover but increases shared-infra risk
