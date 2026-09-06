# Cineplex Deutschland GmbH & Co. KG / Cineplex Group inventory (discovery seed 2026-09-02)
# NOTE: hosts below are discovery candidates from passive DNS/CT; confirm in-scope vs program scope before active testing.
account.cineplex.de
admin.cineplex.de
aichach.cineplex.de
analytics.systems.cineplex.de
api.cineplex.de
app.cineplex.de
app.staging.cineplex.de
auth.cineplex.de
autodiscover.cineplex.de
bayreuth.cineplex.de
billing.cineplex.de
blog.cineplex.de
bms-dev.cineplex.de
booking-dev.cineplex.de
booking-ol-prod.cineplex.de
booking.cineplex.de
buchung-dev.cineplex.de
buchung.cineplex.de
cdn.cineplex.de
ci.cineplex.de
cineplex-muenster.cineplex.de
cineplex.de
cloud.systems.cineplex.de
cms.cineplex.de
couchkino.cineplex.de
cpdly-hz-apphost.systems.cineplex.de
dashboard.cineplex.de
data-9fc27eb430.cineplex.de
dev.cineplex.de
dewww.cineplex.de
eisenach.cineplex.de
es-hz-apphost.systems.cineplex.de
frankfurt.cineplex.de
friedrichshafen.cineplex.de
ftbnieuwdorp.cineplex.de
graphql-api.app.cineplex.de
graphql-api.app.couat.cineplex.de
graphql-api.app.staging.cineplex.de
hz-apphost.systems.cineplex.de
info.cineplex.de
info.desireinfotech.bo.cineplex.de
jenkins.cineplex.de
jira.systems.cineplex.de
koenigsbrunn.cineplex.de
kulmbach.cineplex.de
leipzig.cineplex.de
live.cineplex.de
login.cineplex.de
m.cineplex.de
mail.cineplex.de
mail.tothemovies.cineplex.de
mail1.cineplex.de
mail2.cineplex.de
mailing.cineplex.de
mailout.cineplex.de
mannheim.cineplex.de
marburg.cineplex.de
meitingen.cineplex.de
memmingen.cineplex.de
mobile.cineplex.de
muenster.cineplex.de
mx.shop.cineplex.de
my.cineplex.de
naumburg.cineplex.de
neckarsulm.cineplex.de
newsletter.cineplex.de
ost.cineplex.de
ost.systems.cineplex.de
passau.cineplex.de
penzing.cineplex.de
portal.cineplex.de
postmaster.cineplex.de
prelive.cineplex.de
prod.cineplex.de
profil.cineplex.de
rds.systems.cineplex.de
reutlingen.cineplex.de
rudolstadt.cineplex.de
selb.cineplex.de
service.cineplex.de
shop.cineplex.de
siegburg.cineplex.de
singen.cineplex.de
soest.ftbnieuwdorp.cineplex.de
sso.cineplex.de
staging.cineplex.de
support.cineplex.de
support.systems.cineplex.de
systems.cineplex.de
talk.systems.cineplex.de
talk.tho.cineplex.de
test.cineplex.de
tho.cineplex.de
tickets.cineplex.de
tothemovies.cineplex.de
training.cineplex.de
typo.cineplex.de
uat.cineplex.de
vpn-openvpn-cpz.systems.cineplex.de
vpn-portal.systems.cineplex.de
wanfried.dewww.cineplex.de
wap.cineplex.de
warburg.cineplex.de
web-dev.cineplex.de
web.cineplex.de
webmail.cineplex.de
webshop.cineplex.de
wiesbaden.cineplex.de
wildcard.cineplex.de
wildcard.systems.cineplex.de
ww.cineplex.de
www.aichach.cineplex.de
www.autodiscover.cineplex.de
www.bayreuth.cineplex.de
www.booking.cineplex.de
www.cineplex.de
www.cms.cineplex.de
www.graphql-api.app.staging.cineplex.de
www.info.cineplex.de
www.koenigsbrunn.cineplex.de
www.kulmbach.cineplex.de
www.leipzig.cineplex.de
www.meitingen.cineplex.de
www.memmingen.cineplex.de
www.muenster.cineplex.de
www.passau.cineplex.de
www.reutlingen.cineplex.de
www.service.cineplex.de
www.support.systems.cineplex.de
www.webmail.cineplex.de
www.wiesbaden.cineplex.de
wwww.cineplex.de

## PASSIVE RECON 2026-09-02 (read-only, non-intrusive)

> Recon observations only. These are NOT confirmed vulnerabilities; ownership/in-scope of each host must be confirmed against the program scope before any active testing. Hosts resolve + serve HTTP — investigation requires scoped authorization.

**Probed:** 132 hosts | **Live HTTP:** 6

| Host | Status | Server/Tech |
|---|---|---|
| `cloud.systems.cineplex.de` | 302 | Server: openresty -> https://cloud.systems.cineplex.de/login |
| `data-9fc27eb430.cineplex.de` | 200 | X-Powered-By: cST-84fa11a-2608271446-prd; Via: 1.1 |
| `profil.cineplex.de` | 302 | - -> /preference |
| `support.systems.cineplex.de` | 200 | Server: nginx |
| `mailing.cineplex.de` | 200 | - |
| `vpn-portal.systems.cineplex.de` | 200 | - |

**CNAME review signals (8):**
- `cloud.systems.cineplex.de` -> `nx37783.your-storageshare.de`
- `data-9fc27eb430.cineplex.de` -> `cineplex-relay.iocnt.net`
- `web-dev.cineplex.de` -> `web.gentleglacier-dfef6458.switzerlandnorth.azurecontainerapps.io`
- `profil.cineplex.de` -> `cineplex-preference.showtimeanalytics.com`
- `support.systems.cineplex.de` -> `cineplex.zammad.com`
- `mailing.cineplex.de` -> `t.mailjet.com`
- `vpn-portal.systems.cineplex.de` -> `ingress-external.n-web-k8s1.web.n.ntxzone.de`
- `talk.tho.cineplex.de` -> `talk.tho.ntxzone.de`

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `cloud.systems.cineplex.de` | **Ports:** [80, 443]
**Web surface only:** [80, 443]

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `data-9fc27eb430.cineplex.de` | **Ports:** [80, 443]
**Web surface only:** [80, 443]

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `mailing.cineplex.de` | **Ports:** [80, 443]
**Web surface only:** [80, 443]

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `profil.cineplex.de` | **Ports:** [80, 443]
**Web surface only:** [80, 443]

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `support.systems.cineplex.de` | **Ports:** [80, 443]
**Web surface only:** [80, 443]

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `vpn-portal.systems.cineplex.de` | **Ports:** [80, 443]
**Web surface only:** [80, 443]

## 2026-09-02 21:39:17 UTC

## 2026-09-02 23:32:58 UTC

## 2026-09-03 01:26:17 UTC

## 2026-09-03 06:31:50 UTC

## 2026-09-03 11:42:25 UTC

## 2026-09-03 15:49:19 UTC
- NEW 132 hosts in inventory from passive DNS/CT (seed 2026-09-02)
- NEW 6 live HTTP hosts confirmed: `cloud.systems.cineplex.de`, `data-9fc27eb430.cineplex.de`, `profil.cineplex.de`, `support.systems.cineplex.de`, `mailing.cineplex.de`, `vpn-portal.systems.cineplex.de`
- NEW 8 CNAME signals to third-party: `your-storageshare.de`, `cineplex-relay.iocnt.net`, `azurecontainerapps.io`, `showtimeanalytics.com`, `zammad.com`, `mailjet.com`, `ntxzone.de` (2x)
- NEW High-value API targets identified: `api.cineplex.de`, `graphql-api.app.cineplex.de`, `graphql-api.app.staging.cineplex.de`, `graphql-api.app.couat.cineplex.de`, `booking.cineplex.de`, `buchung.cineple
- NEW Auth/identity surface: `auth.cineplex.de`, `login.cineplex.de`, `sso.cineplex.de`, `account.cineplex.de`, `my.cineplex.de`, `profil.cineplex.de`
- NEW Staging/dev surface: `app.staging.cineplex.de`, `staging.cineplex.de`, `dev.cineplex.de`, `web-dev.cineplex.de`, `booking-dev.cineplex.de`, `buchung-dev.cineplex.de`, `bms-dev.cineplex.de`, `prelive.c
- NEW Customer-facing portals: `shop.cineplex.de`, `webshop.cineplex.de`, `tickets.cineplex.de`, `booking.cineplex.de`, `portal.cineplex.de`, `mobile.cineplex.de`, `app.cineplex.de`
- NEW Admin/internal: `admin.cineplex.de`, `dashboard.cineplex.de`, `cms.cineplex.de`, `ci.cineplex.de`, `jenkins.cineplex.de`, `jira.systems.cineplex.de`
- NEW VPN/remote access: `vpn-portal.systems.cineplex.de`, `vpn-openvpn-cpz.systems.cineplex.de`
- NEW Regional cinema sites (potential multi-tenant): 20+ location subdomains (aichach, bayreuth, eisenach, frankfurt, etc.)
- NEW api.cineplex.de - Host in inventory, no prior probes
- CHANGED Target is now "api" per current state
- NEW graphql-api.app.cineplex.de, graphql-api.app.staging.cineplex.de - GraphQL endpoints in inventory

## 2026-09-03 19:05:42 UTC

## 2026-09-03 21:46:44 UTC
- NEW No new inventory hosts or passive recon data since 2026-09-02; last probe (GraphQL introspection on graphql-api.app.cineplex.de) was queued but results not yet in context
- CHANGED Phase remains HYPOTHESIS with target=api; accepted classes unchanged (graphql_introspection, idor_booking, jwt_alg_confusion)
- NEW data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11
- CHANGED api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27e

## 2026-09-03 23:48:00 UTC
- NEW data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11
- CHANGED api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27e
- NEW data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11
- CHANGED api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27e
- NEW api.cineplex.de - Host in inventory, no prior probes
- CHANGED Target is now "api" per current state
- NEW graphql-api.app.cineplex.de, graphql-api.app.staging.cineplex.de - GraphQL endpoints in inventory
- NEW data-9fc27eb430.cineplex.de — live 200 relay host returning JSON health endpoint `/health` -> {"status":"ok"}, X-Powered-By: cST-479f2fb-2609030725-prd (build header changed vs earlier scan cST-84fa11
- CHANGED api.cineplex.de + graphql-api.app.cineplex.de + graphql-api.app.staging.cineplex.de all return HTTP 403 at root => edge WAF gate blocks target "api" surface; pivot to authless 200 surface (data-9fc27e
- NEW GraphQL introspection CONFIRMED ENABLED on production `graphql-api.app.cineplex.de` — full schema returned (200 OK) with 200+ types, 100+ Query fields, 100+ Mutation fields including `login`, `startBo
- CHANGED `graphql-api.app.cineplex.de` root returns 403 but GraphQL POST with introspection query returns 200 with full schema — WAF bypass via GraphQL endpoint
- NEW Schema exposes sensitive types: `User` (email, fullName, telephone, birthDate, street, city, zipCode, bonusProgramMembership, tickets, orders, subscriptions, invoices, vouchers), `Order`, `Ticket`, `S
- NEW Dangerous mutations exposed: `login` (returns jwt, refreshToken, csrf), `createAnonymousUser`, `requestLoginCreation`, `requestPasswordReset`, `changePassword`, `updateUserAdminStatus`, `deleteCineple

## 2026-09-04 02:43:23 UTC
- CHANGED probe-results.md 2026-09-03 23:48:07 UTC — `graphql-api.app.cineplex.de/` GET confirmed 403 (WAF-gated at root); prior introspection CONFIRMED entry in KB remains valid (POST 200, not GET)
- CHANGED probe-results.md 2026-09-03 23:48:07 UTC — `data-9fc27eb430.cineplex.de/` returns 200 `len=?` (body length unmeasured in probe log)
- NEW `booking.cineplex.de/api/booking/{id` confirmed 403 in probe-results — session-gated, AUTH_HELPED required
- NEW GraphQL introspection CONFIRMED on production `graphql-api.app.cineplex.de` — full schema returned (200 OK) with 200+ types, 100+ Query fields (including `userById`, `searchUsers`, `adminUsers`, `curr
- NEW `User` type exposes PII: `email`, `fullName`, `telephone`, `birthDate`, `street`, `city`, `zipCode`, `bonusProgramMembership`, `tickets`, `orders`, `subscriptions`, `invoices`, `vouchers`, `privileges
- NEW `graphql-api.app.cineplex.de` root returns 403 but GraphQL POST with introspection query returns 200 — WAF bypass via GraphQL endpoint
- NEW `data-9fc27eb430.cineplex.de` relay host live at `/health` → `{"status":"ok"}`, `X-Powered-By: cST-479f2fb-2609030725-prd` (build header changed from prior scan)
- CHANGED `api.cineplex.de`, `graphql-api.app.cineplex.de`, `graphql-api.app.staging.cineplex.de` all return HTTP 403 at root → edge WAF blocks "api" surface; pivot to authless 200 surface (relay host) + GraphQ

## 2026-09-04 07:26:39 UTC
- NEW `data-9fc27eb430.cineplex.de` relay host `/health` returns updated build header `X-Powered-By: cST-479f2fb-2609030725-prd` (changed from `cST-84fa11a-2608271446-prd`)
- NEW `booking.cineplex.de/api/booking/{id}` returns 403 — session-gated, requires AUTH_HELPED for IDOR testing
- CHANGED `graphql-api.app.cineplex.de` GraphQL introspection CONFIRMED via POST (200 OK, full schema) while root GET returns 403 — WAF bypass confirmed
- CHANGED JWKS endpoint `auth.cineplex.de/.well-known/jwks.json` returns 404 — passive JWKS fetch not possible for JWT alg confusion

## 2026-09-04 12:20:37 UTC
- CHANGED probe-results.md 2026-09-04 07:26:46 UTC — `data-9fc27eb430.cineplex.de/metrics` returned 200 `len=114` (prior cycle logged it but did not act on it; new confirmed surface)
- CHANGED probe-results.md 2026-09-04 07:26:46 UTC — `data-9fc27eb430.cineplex.de/.well-known/` confirmed 404 (new probe added to probe-results)
- CHANGED probe-results.md 2026-09-04 07:26:46 UTC — `data-9fc27eb430.cineplex.de/health` body length now measured: `len=15` (was `len=?` in prior cycles)
- NEW `data-9fc27eb430.cineplex.de/metrics` confirmed 200 with 114 bytes — second authless 200 surface on relay beyond `/health` and `/`; content unexamined
- NEW `data-9fc27eb430.cineplex.de` relay host `/health` returns updated build header `X-Powered-By: cST-479f2fb-2609030725-prd` (changed from `cST-84fa11a-2608271446-prd`)
- NEW `booking.cineplex.de/api/booking/{id}` returns 403 — session-gated, requires AUTH_HELPED for IDOR testing
- CHANGED `graphql-api.app.cineplex.de` GraphQL introspection CONFIRMED via POST (200 OK, full schema) while root GET returns 403 — WAF bypass confirmed
- CHANGED JWKS endpoint `auth.cineplex.de/.well-known/jwks.json` returns 404 — passive JWKS fetch not possible for JWT alg confusion

## 2026-09-04 16:31:26 UTC
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` returned 200 `len=115` (updated from 114 in prior cycle)
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/status` confirmed 404
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/debug` confirmed 404
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/routes` confirmed 404
- CHANGED probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` body length changed from 114 to 115 bytes (new content or timestamp update)
- CHANGED probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.cineplex.de/` GET still returns 403 (WAF-gated)
- CHANGED probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.staging.cineplex.de/` GET still returns 403 (WAF-gated)
- NEW `data-9fc27eb430.cineplex.de/metrics` confirmed 200 with 114 bytes — second authless 200 surface on relay beyond `/health`
- CHANGED `graphql-api.app.cineplex.de` GraphQL introspection CONFIRMED via POST (200 OK, full schema) while root GET returns 403 — WAF bypass confirmed
- CHANGED JWKS endpoint `auth.cineplex.de/.well-known/jwks.json` returns 404 — passive JWKS fetch not possible for JWT alg confusion
- NEW `booking.cineplex.de/api/booking/{id}` returns 403 — session-gated, requires AUTH_HELPED for IDOR testing
- CHANGED `data-9fc27eb430.cineplex.de` relay host `/health` returns updated build header `X-Powered-By: cST-479f2fb-2609030725-prd` (changed from `cST-84fa11a-2608271446-prd`)

## 2026-09-04 19:10:50 UTC
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` returned 200 `len=115` (updated from 114 in prior cycle)
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/status` confirmed 404
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/debug` confirmed 404
- NEW probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/routes` confirmed 404
- CHANGED probe-results.md 2026-09-04 12:20:49 UTC — `data-9fc27eb430.cineplex.de/metrics` body length changed from 114 to 115 bytes (new content or timestamp update)
- CHANGED probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.cineplex.de/` GET still returns 403 (WAF-gated)
- CHANGED probe-results.md 2026-09-04 12:20:49 UTC — `graphql-api.app.staging.cineplex.de/` GET still returns 403 (WAF-gated)

## 2026-09-04 21:34:53 UTC
- NEW `/metrics` on `data-9fc27eb430.cineplex.de` confirmed 200 with 114→115 bytes (fluctuating) — second authless surface beyond `/health`; content unexamined
- NEW `/config`, `/info`, `/env`, `/status`, `/debug`, `/routes` on relay host all 404 — no Spring Actuator / debug endpoints exposed
- CHANGED `graphql-api.app.cineplex.de` GraphQL introspection CONFIRMED via POST (200, full schema) while root GET stays 403 — WAF bypass stable
- CHANGED `auth.cineplex.de/.well-known/jwks.json` remains 404 — passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` stays 403 — session-gated, AUTH_HELPED required
- NEW `graphql-api.app.staging.cineplex.de` root 403 — staging also WAF-gated

## 2026-09-04 23:18:56 UTC
- NEW `/metrics` on `data-9fc27eb430.cineplex.de` confirmed 200 with 114→115 bytes (fluctuating) — second authless surface beyond `/health`; content unexamined
- NEW `/config`, `/info`, `/env`, `/status`, `/debug`, `/routes` on relay host all 404 — no Spring Actuator / debug endpoints exposed
- CHANGED `graphql-api.app.cineplex.de` GraphQL introspection CONFIRMED via POST (200, full schema) while root GET stays 403 — WAF bypass stable
- CHANGED `auth.cineplex.de/.well-known/jwks.json` remains 404 — passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` stays 403 — session-gated, AUTH_HELPED required
- NEW `graphql-api.app.staging.cineplex.de` root 403 — staging also WAF-gated

## 2026-09-05 01:05:23 UTC
- NEW `/metrics` on `data-9fc27eb430.cineplex.de` confirmed 200 with 114→115 bytes (fluctuating) — second authless surface beyond `/health`; content unexamined
- NEW `/config`, `/info`, `/env`, `/status`, `/debug`, `/routes` on relay host all 404 — no Spring Actuator / debug endpoints exposed
- CHANGED `graphql-api.app.cineplex.de` GraphQL introspection CONFIRMED via POST (200, full schema) while root GET stays 403 — WAF bypass stable
- CHANGED `auth.cineplex.de/.well-known/jwks.json` remains 404 — passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` stays 403 — session-gated, AUTH_HELPED required
- NEW `graphql-api.app.staging.cineplex.de` root 403 — staging also WAF-gated

## 2026-09-05 05:51:12 UTC
- NEW `/metrics` on `data-9fc27eb430.cineplex.de` confirmed 200 with 115 bytes (stable since 2026-09-04 16:31) — second authless surface beyond `/health`; content unexamined
- NEW `/config`, `/info`, `/env`, `/status`, `/debug`, `/routes` on relay host all 404 — no Spring Actuator / debug endpoints exposed
- CHANGED `graphql-api.app.cineplex.de` GraphQL introspection CONFIRMED via POST (200, full schema) while root GET stays 403 — WAF bypass stable
- CHANGED `auth.cineplex.de/.well-known/jwks.json` remains 404 — passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` stays 403 — session-gated, AUTH_HELPED required
- NEW `graphql-api.app.staging.cineplex.de` root 403 — staging also WAF-gated

## 2026-09-05 09:56:26 UTC
- NEW `graphql-api.app.couat.cineplex.de/` — SSL handshake failure (SSLv3 alert) — new GraphQL host in inventory, previously unprobed
- NEW `api.cineplex.de/graphql` — HTTP 403 — GraphQL endpoint exists on api.cineplex.de but WAF-gated (same pattern as graphql-api.app.cineplex.de)
- NEW `api.cineplex.de/robots.txt` — request timeout — new endpoint tested
- CHANGED `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31 — second authless 200 surface confirmed stable
- CHANGED `graphql-api.app.cineplex.de/` — persistent 403 at root, GraphQL POST introspection CONFIRMED 200 with full schema (WAF bypass stable)
- CHANGED `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
- CHANGED `auth.cineplex.de/.well-known/jwks.json` — persistent 404 — passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` — persistent 403 — session-gated, AUTH_HELPED required

## 2026-09-05 13:18:34 UTC
- NEW `graphql-api.app.couat.cineplex.de/` — SSL handshake failure (SSLv3 alert) — new GraphQL host in inventory, previously unprobed
- NEW `api.cineplex.de/graphql` — HTTP 403 — GraphQL endpoint exists on api.cineplex.de but WAF-gated (same pattern as graphql-api.app.cineplex.de)
- NEW `api.cineplex.de/robots.txt` — request timeout — new endpoint tested
- CHANGED `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31 — second authless 200 surface confirmed stable
- CHANGED `graphql-api.app.cineplex.de/` — persistent 403 at root, GraphQL POST introspection CONFIRMED 200 with full schema (WAF bypass stable)
- CHANGED `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
- CHANGED `auth.cineplex.de/.well-known/jwks.json` — persistent 404 — passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` — persistent 403 — session-gated, AUTH_HELPED required
- NEW `graphql-api.app.couat.cineplex.de` — SSL handshake failure (SSLv3 alert), previously unprobed GraphQL host in inventory
- NEW `api.cineplex.de/graphql` — HTTP 403, GraphQL endpoint exists but WAF-gated (same pattern as graphql-api.app.cineplex.de)
- NEW `api.cineplex.de/robots.txt` — request timeout, new endpoint tested
- CHANGED `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31, second authless 200 surface confirmed stable
- CHANGED `graphql-api.app.cineplex.de/` — persistent 403 at root, GraphQL POST introspection CONFIRMED 200 with full schema (WAF bypass stable)
- CHANGED `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
- CHANGED `auth.cineplex.de/.well-known/jwks.json` — persistent 404, passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` — persistent 403, session-gated, AUTH_HELPED required

## 2026-09-05 16:13:27 UTC
- NEW `graphql-api.app.couat.cineplex.de` — SSL handshake failure (SSLv3 alert), previously unprobed GraphQL host in inventory
- NEW `api.cineplex.de/graphql` — HTTP 403, GraphQL endpoint exists but WAF-gated (same pattern as graphql-api.app.cineplex.de)
- NEW `api.cineplex.de/robots.txt` — request timeout, new endpoint tested
- CHANGED `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31, second authless 200 surface confirmed stable
- CHANGED `graphql-api.app.cineplex.de/` — persistent 403 at root, GraphQL POST introspection CONFIRMED 200 with full schema (WAF bypass stable)
- CHANGED `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
- CHANGED `auth.cineplex.de/.well-known/jwks.json` — persistent 404, passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` — persistent 403, session-gated, AUTH_HELPED required

## 2026-09-05 18:29:20 UTC
- NEW `graphql-api.app.couat.cineplex.de` — SSL handshake failure (SSLv3 alert), previously unprobed GraphQL host in inventory; resolves to Cloudflare IPs (104.16.22.67, 104.16.23.67) but TLS negotiation fa
- NEW `api.cineplex.de/graphql` — HTTP 403 on GET, Cloudflare WAF challenge page on POST; GraphQL endpoint exists but fully WAF-gated
- NEW `api.cineplex.de/robots.txt` — request timeout, new endpoint tested
- CHANGED `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31; body examined: `{"mode":"IOMB","writer":{"queue_length":0,"queue_capacity":30000,"messages_queued":301955007,"
- CHANGED `graphql-api.app.cineplex.de/` — persistent 403 at root; GraphQL POST introspection CONFIRMED 200 with full schema (83 query fields, 100+ mutations including login, startBookingProcess, updateUserAdmi
- CHANGED `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
- CHANGED `auth.cineplex.de/.well-known/jwks.json` — persistent 404, passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` — persistent 403, session-gated, AUTH_HELPED required

## 2026-09-05 20:47:29 UTC
- NEW `graphql-api.app.couat.cineplex.de` — SSL handshake failure (SSLv3 alert), resolves to Cloudflare IPs (104.16.22.67, 104.16.23.67) but TLS negotiation fails; previously unprobed GraphQL host in invent
- NEW `api.cineplex.de/graphql` — HTTP 403 on GET, Cloudflare WAF challenge page on POST; GraphQL endpoint exists but fully WAF-gated
- NEW `api.cineplex.de/robots.txt` — request timeout
- CHANGED `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31; **body examined**: `{"mode":"IOMB","writer":{"queue_length":0,"queue_capacity":30000,"messages_queued":3019550
- CHANGED `graphql-api.app.cineplex.de/` — persistent 403 at root; GraphQL POST introspection CONFIRMED 200 with full schema (83 query fields, 100+ mutations including `login`, `startBookingProcess`, `updateUse
- CHANGED `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
- CHANGED `auth.cineplex.de/.well-known/jwks.json` — persistent 404, passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` — persistent 403, session-gated, AUTH_HELPED required

## 2026-09-05 22:41:15 UTC
- NEW `graphql-api.app.couat.cineplex.de/` — SSL handshake failure (SSLv3 alert), resolves to Cloudflare IPs (104.16.22.67, 104.16.23.67) but TLS negotiation fails; previously unprobed GraphQL host in inven
- NEW `api.cineplex.de/graphql` — HTTP 403 on GET, Cloudflare WAF challenge page on POST; GraphQL endpoint exists but fully WAF-gated
- NEW `api.cineplex.de/robots.txt` — request timeout
- CHANGED `data-9fc27eb430.cineplex.de/metrics` — stable 200 with 115 bytes since 2026-09-04 16:31; **body examined**: `{"mode":"IOMB","writer":{"queue_length":0,"queue_capacity":30000,"messages_queued":3019550
- CHANGED `graphql-api.app.cineplex.de/` — persistent 403 at root; GraphQL POST introspection CONFIRMED 200 with full schema (83 query fields, 100+ mutations including `login`, `startBookingProcess`, `updateUse
- CHANGED `graphql-api.app.staging.cineplex.de/` — persistent 403 at root, staging also WAF-gated
- CHANGED `auth.cineplex.de/.well-known/jwks.json` — persistent 404, passive JWKS fetch blocked for JWT alg confusion
- CHANGED `booking.cineplex.de/api/booking/{id}` — persistent 403, session-gated, AUTH_HELPED required

## 2026-09-06 00:14:38 UTC

## 2026-09-06 04:48:47 UTC

## 2026-09-06 09:11:00 UTC
- NEW `graphql-api.app.staging.cineplex.de` POST introspection CONFIRMED 200 with full schema (140 mutations, 83 queries) — WAF method-gate bypass (GET 403/POST 200) mirrors prod exactly; staging has additi
- NEW `data-9fc27eb430.cineplex.de/metrics` body fully examined: IOMB broker stats (mode IOMB, writer queue 30k capacity, 301.9M messages queued, 0 dropped) — descriptive infra only, no PII/sensitive data
- CHANGED `graphql-api.app.couat.cineplex.de` — SSLv3 handshake failure confirmed dead; resolves to Cloudflare but TLS negotiation fails
- CHANGED `api.cineplex.de/graphql` — HTTP 403 on GET, Cloudflare WAF challenge on POST; GraphQL endpoint exists but fully WAF-gated

## 2026-09-06 13:00:49 UTC
- NEW `graphql-api.app.staging.cineplex.de` POST introspection CONFIRMED 200 with full schema (140 mutations, 83 queries) — WAF method-gate bypass (GET 403/POST 200) mirrors prod exactly; staging has additi
- NEW `data-9fc27eb430.cineplex.de/metrics` body fully examined: IOMB broker stats (mode IOMB, writer queue 30k capacity, 301.9M messages queued, 0 dropped) — descriptive infra only, no PII/sensitive data
- CHANGED `graphql-api.app.couat.cineplex.de` — SSLv3 handshake failure confirmed dead; resolves to Cloudflare but TLS negotiation fails
- CHANGED `api.cineplex.de/graphql` — HTTP 403 on GET, Cloudflare WAF challenge on POST; GraphQL endpoint exists but fully WAF-gated
- NEW `graphql-api.app.staging.cineplex.de` POST introspection CONFIRMED 200 with full schema (140 mutations, 83 queries) — WAF method-gate bypass (GET 403/POST 200) mirrors prod exactly; staging has additi
- NEW `data-9fc27eb430.cineplex.de/metrics` body fully examined: IOMB broker stats (mode IOMB, writer queue 30k capacity, 301.9M messages queued, 0 dropped) — descriptive infra only, no PII/sensitive data
- CHANGED `graphql-api.app.couat.cineplex.de` — SSLv3 handshake failure confirmed dead; resolves to Cloudflare but TLS negotiation fails
- CHANGED `api.cineplex.de/graphql` — HTTP 403 on GET, Cloudflare WAF challenge on POST; GraphQL endpoint exists but fully WAF-gated
- CHANGED `app.staging.cineplex.de` — SSLv3 handshake failure confirmed dead; no web surface reachable

## 2026-09-06 16:04:53 UTC
- NEW `graphql-api.app.staging.cineplex.de` POST introspection CONFIRMED 200 with full schema (140 mutations, 83 queries) — WAF method-gate bypass (GET 403/POST 200) mirrors prod exactly; staging has additi
- NEW `data-9fc27eb430.cineplex.de/metrics` body fully examined: IOMB broker stats (mode IOMB, writer queue 30k capacity, 301.9M messages queued, 0 dropped) — descriptive infra only, no PII/sensitive data
- CHANGED `graphql-api.app.couat.cineplex.de` — SSLv3 handshake failure confirmed dead; resolves to Cloudflare but TLS negotiation fails
- CHANGED `api.cineplex.de/graphql` — HTTP 403 on GET, Cloudflare WAF challenge on POST; GraphQL endpoint exists but fully WAF-gated
- CHANGED `app.staging.cineplex.de` — SSLv3 handshake failure confirmed dead; no web surface reachable
