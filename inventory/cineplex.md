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
