# The Tactical Rabbi — takeover research notes

> **Status:** research pass complete for what's observable from outside (2026-09-16). Purpose:
> prep for meeting to take over website + app development for thetacticalrabbi.com
> (Rabbi Raziel Cohen — firearms training, security assessments, preparedness education).
> Next update should come from the meeting itself (§8 checklist, §9 questions).
>
> Everything below came from passive, public observation (DNS, whois, RIPE/ASN, HTTP headers,
> served JS, cert-transparency logs, page content). Nothing was logged into or probed beyond
> public URLs. **Confirmed** = observed directly. **Inferred** = my read of the evidence; verify
> at the meeting.

---

## 1. Summary (read this first)

- **What they sell:** in-person, live-fire range classes in Henryville PA / Randolph NJ,
  $175–$350 (§12). **Not video courses.** All video is public YouTube (§11).
- **Site:** https://thetacticalrabbi.com — bespoke, hand-coded React site on an experimental
  Vite-based Next-compatible stack ("vinext" + Rolldown + React Server Components) (§4).
- **Backend is a real registration system:** application form with legal name + **required
  selfie** + returning-participant verification, reviewed **manually** by an admin. Routes:
  `/api/applications`, `/api/participants/verification/{start,confirm}`, `/api/uploads/selfie`,
  `/api/course-interest`. **No online payment anywhere** — collected off-site after approval (§12).
  ⇒ participant PII + selfies live in a database on the server.
- **Hosting:** **Hetzner Online GmbH, directly** — Hetzner Cloud VPS, Helsinki (HEL1), AS24940.
  Hand-managed VM, nginx 1.28.3 → Node. No CDN/WAF, no PaaS, origin IP exposed (§3, §13).
- **DNS/registrar:** GoDaddy, WHOIS-privacy-shielded. Domain registered 2019, expires 2027-05-10.
  No MX, no SPF/DMARC (§2).
- **Recent activity:** new Hetzner IP block **2026-09-09**, DNS + TLS cutover **2026-09-11**,
  production build **2026-09-15 17:09 UTC** (the day before I looked). A migration/relaunch
  happened *this week*; we may be inheriting it mid-stream. **Ask about this** (§6).
- **Staging env exists:** `staging.thetacticalrabbi.com` → same box; its cert has lapsed.
- **Only one bookable session** right now (Advanced Tactical Pistol, Sun 2026-09-20). Every other
  course is a "Notify me" waitlist.
- **Nothing SaaS-managed:** no WordPress/Wix/Squarespace/Vercel/Netlify/Stripe/Mailchimp. Whoever
  built this is a strong developer who likes very new tooling — which is also the main handoff
  risk (§7).

---

## 2. DNS + domain

| Item | Value | Status |
|---|---|---|
| Apex `A` | `2.29.40.234` | confirmed |
| `AAAA` | none | confirmed |
| `www` | `A` → `2.29.40.234` (no CNAME) | confirmed |
| `staging` | `A` → `2.29.40.234` | confirmed |
| `NS` | `ns65.domaincontrol.com`, `ns66.domaincontrol.com` (**GoDaddy DNS**) | confirmed |
| `MX` | **none** — domain sends/receives no email | confirmed |
| `TXT` | none (no SPF/DKIM/DMARC, no verification records) | confirmed |
| Registrar | GoDaddy.com, LLC | confirmed |
| Registrant | Domains By Proxy, LLC (Arizona) — privacy shield | confirmed |
| Created | 2019-05-10 | confirmed |
| Expires | **2027-05-10** | confirmed |
| Registrar "Updated" | 2026-05-11 | confirmed |
| Registry "Updated" | **2026-09-11 20:40 UTC** | confirmed |

Notes:
- Registry update on 2026-09-11 + LE cert issued 2026-09-11 20:18 UTC ⇒ the A record was
  repointed to the Hetzner box that day. (inferred)
- No SPF/DMARC means anyone can spoof `@thetacticalrabbi.com`. Cheap fix once we own DNS.
- Need GoDaddy account access (or a DNS transfer) to do anything with DNS. See §8.

---

## 3. Hosting / infrastructure

| Item | Value | Status |
|---|---|---|
| Provider | **Hetzner Online GmbH**, direct (see §13 for the full pin-down) | confirmed |
| Product | Hetzner **Cloud** VPS (netname `CLOUD-HEL1`), Helsinki, Finland | confirmed |
| ASN | AS24940 `HETZNER-AS`, prefix `2.29.0.0/16` | confirmed |
| rDNS | `static.234.40.29.2.clients.your-server.de` (Hetzner default) | confirmed |
| Web server | `nginx/1.28.3`, HTTP/2, ALPN h2; plain HTTP → 301 HTTPS | confirmed |
| CDN / WAF | **none** — no Cloudflare/Fastly/Akamai headers, DNS points straight at origin | confirmed |
| PaaS / control panel | **none visible** — nginx directly on the edge, no platform headers | inferred |
| TLS | Let's Encrypt, issuer `YE1`, subject `CN=thetacticalrabbi.com`, valid 2026-09-11 → 2026-12-10 | confirmed |
| TLS automation | ~60-day renewal cadence in CT logs since 2025-01 ⇒ certbot (or similar) on a timer | inferred |
| Security headers | HSTS `max-age=31536000`, `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin`. **No CSP.** | confirmed |
| Cache policy | HTML: `no-store, must-revalidate`. `/_next/static/*`: `public, max-age=31536000, immutable` (content-hashed filenames) | confirmed |
| Ports | 22/80/443/3000/8080 all appeared filtered from my sandbox — sandbox blocks raw sockets, so **inconclusive**, not evidence of a firewall | unknown |

Cert-transparency history (crt.sh, 34 certs):
- 2023-11-05: **GoDaddy-issued** wildcard `*.thetacticalrabbi.com` ⇒ site was on GoDaddy
  hosting (likely Managed WordPress or cPanel) at that time. (inferred)
- 2025-01 onward: Let's Encrypt every ~2 months ⇒ moved to self-hosted w/ automated renewal
  by early 2025. (inferred)
- Names seen: `thetacticalrabbi.com`, `*.thetacticalrabbi.com`, `staging.thetacticalrabbi.com`,
  `www.staging.thetacticalrabbi.com`.
- Latest pre-migration LE cert: 2026-08-26 (issuer `YR2`). Current: 2026-09-11 (`YE1`).

Comparison to our own stack (for planning): same shape as nearfield — single VPS, nginx TLS
terminator, app server behind it — but Hetzner not Linode, Node/React not FastAPI/static, GoDaddy
DNS with no CDN instead of Cloudflare-proxied.

---

## 4. Application stack

**Headline: React Server Components app using Next.js App-Router conventions, but built with
Vite + Rolldown via the experimental "vinext" framework — not real Next.js, not Vercel.**

Evidence:

| Fingerprint | Where seen | Interpretation |
|---|---|---|
| `data-precedence="vite-rsc/importer-resources"` on CSS `<link>` | HTML | `@vitejs/plugin-rsc` (Vite's RSC plugin) |
| `/_next/static/chunks/rolldown-runtime-C60lm6uB.js` | script tags | Bundled with **Rolldown** (Rust bundler from the Vite/VoidZero team) |
| `http://vinext.local`, `https://vinext.local` string literals | `index-C-O1LOUf.js` | vinext's internal placeholder origin |
| `vary: … X-Vinext-Interception-Context, X-Vinext-Mounted-Slots, X-Vinext-Rsc-Render-Mode` | every response | vinext runtime |
| `vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch, Next-Url` | every response | App-Router-style RSC streaming/nav |
| link to `nextjs.org/docs/app/api-reference/functions/use-search-params` | `index-*.js` | Next-compatible API surface |
| `/_next/static/…` paths, `Next-Router-*` headers | everywhere | Next.js conventions preserved for compatibility |

Chunks (build hash suffixes stripped): `framework`, `index`, `rolldown-runtime`,
`navigation-errors`, `layout-segment-context`, `FutureDateSignup`, `NewsletterSignup`,
`PressMarquee`, `RegistrationDateStep`. All stamped `Last-Modified: Tue, 15 Sep 2026 17:09:19 GMT`.
No source maps served (`.js.map` → 404).

Routes observed:
`/`, `/about`, `/contact` (+ `?interest=<slug>`), `/courses`, `/courses/tactical-pistol`,
`/courses/tactical-rifle`, `/courses/advanced-tactical-pistol` (+ `?session=<uuid>#registration`),
`/courses/advanced-tactical-rifle`, `/courses/active-shooter-response`, `/courses/stress-box`,
`/courses/private-lesson`, `/merch`. Nav "Affiliates" link → `/merch` (label/route mismatch);
`/affiliates` is a styled 404 ("404 · Off course").

Preloaded images: `/images/tactical-rabbi-logo.png`, `/images/hero.jpg`. Favicons versioned
`?v=20260902-exact-logo` ⇒ a deploy on/around 2026-09-02 too.

Missing basics (quick wins):
- `/robots.txt` → 404
- `/sitemap.xml` → 404
- `/.well-known/security.txt` → 404
- no `<meta name="generator">`, no analytics tag observed on any page
- no CSP header

---

## 5. Backend / integrations

Full registration API is documented in §12. Summary of the client-observed surface:

| Route | Method | Purpose |
|---|---|---|
| `/api/course-interest` | POST | waitlist / notify-me (`email`, `courseSlug`, honeypot `website`). `OPTIONS`→204, `GET`→405 |
| `/api/applications` | POST | class application (with selfie ref) |
| `/api/participants/verification/start` | POST | send verification code to a returning participant |
| `/api/participants/verification/confirm` | POST | confirm code |
| `/api/uploads/selfie` | POST/PUT | selfie upload (the `PUT` is probably a direct-to-storage step) |

- Backend has rate limiting and a payload-size cap (from client error strings).
- **Where data goes is invisible from outside.** No MX, no third-party email/CRM/SMS host referenced
  client-side ⇒ a DB on the box (or attached volume) plus some third-party API for verification
  codes. **Ask.**
- **Merch:** `/merch` has no Stripe/Shopify/Snipcart/Gumroad/PayPal — static or placeholder.
- **Newsletter provider:** none observed.
- **Third-party hosts referenced:** youtube.com, instagram.com, facebook.com (socials/embeds);
  press links to latimes, dailywire, dailymail, foxnews, nypost, yahoo, ynetnews, jewishlink.news,
  anash.org, archive.org.
- **No auth / login surface** observed — the admin review UI (if any) is not linked publicly.

---

## 6. Timeline (reconstructed)

| Date | Event | Source |
|---|---|---|
| 2019-05-10 | Domain registered (GoDaddy) | whois |
| 2023-11-05 | GoDaddy wildcard cert ⇒ on GoDaddy hosting | crt.sh |
| 2025-01 | First Let's Encrypt cert ⇒ moved to self-hosted, automated renewals every ~60d | crt.sh |
| 2026-05-11 | Registrar-side domain update (renewal?) | whois |
| 2026-08-26 | Last pre-migration LE cert (`YR2`) | crt.sh |
| ~2026-09-02 | Favicon asset version stamp ⇒ a deploy | `?v=20260902-exact-logo` |
| **2026-09-09** | Hetzner registers the `CLOUD-HEL1` inetnum containing this IP | RIPE |
| **2026-09-11** | Registry-side DNS update **and** new LE cert (`YE1`) on the Hetzner box | whois + live cert |
| **2026-09-15 17:09 UTC** | Current production build deployed | asset `Last-Modified` |
| 2026-09-16 | This research | — |

Interpretation (inferred): a new Hetzner Cloud server was created ~09-09, the site was cut over to
it on 09-11, and a further deploy landed 09-15. Either the outgoing dev is still actively shipping,
or the client did the cutover themselves. Either way, **the deploy pipeline was exercised days
ago, so the person who ran it knows exactly how it works — get that walkthrough while it's fresh.**

---

## 7. Risks / things I'd want to fix early

1. **Participant PII + selfies on a hand-managed box in Finland.** Legal names, phones, emails,
   photos of firearms-class applicants. Unknown backup, unknown access control, unknown retention
   (the form promises admin deletion). This is the first thing to audit once we have SSH.
2. **Framework bus-factor.** vinext + Rolldown + `@vitejs/plugin-rsc` are all young. Upgrades
   may break; docs and community help are thin. Decide early whether to (a) keep it, (b) migrate to
   stock Next.js (conventions are already Next-shaped, so this is plausible), or (c) rebuild on our
   own FastAPI + static pattern. Don't decide until we've seen the repo.
3. **No online payment.** "Only paid and confirmed registrations count" but payment is collected
   off-site by hand. Biggest product gap and the most obvious first build — with the same
   firearms-friendly-processor question Sierra has (`project_sierra_stripe_assumption` memory).
4. **Origin exposed, no WAF/CDN.** Firearms-training site with a visible Hetzner IP. Cloudflare in
   front is a cheap, familiar win (we already run two zones this way).
5. **No SPF/DMARC.** Trivial spoofing of their domain. Fix once we control DNS.
6. **Staging cert lapsed / staging on prod box.** Either restore properly (separate vhost + cert)
   or remove the DNS record. Staging on the same box as prod is fine for their scale, but it should
   be basic-auth'd.
7. **SEO basics missing** (robots, sitemap, no analytics). Cheap.
8. **Hetzner account ownership.** If the outgoing developer owns the account, the client doesn't
   control their own server or data (§13).

---

## 8. Access we need to take over (checklist for the meeting)

**Accounts**
- [ ] **Source repo** — where is it (GitHub? their laptop?), and is there git history?
- [ ] **Hetzner Cloud account** (console.hetzner.cloud) — who owns it, who pays. Project-member
      access at minimum; long-term the server should live under an account the client controls
      (Hetzner won't transfer servers between accounts — snapshot + rebuild).
- [ ] **SSH** key on the box + root/sudo
- [ ] **GoDaddy** account access for DNS + domain (or authorize a transfer to our registrar)
- [ ] **Social accounts** linked from site (YouTube, Instagram, Facebook) — who owns them.
      YouTube especially: 679 videos / 77.3K subs is the main asset — Brand Account or personal? (§11)
- [ ] **Old GoDaddy hosting** — is anything still there / still being billed?

**Server / deploy**
- [ ] OS, how the Node process is run (systemd? pm2? Docker?), nginx config location, certbot config
- [ ] **Deploy procedure** — exactly what they ran on 2026-09-15. Script? CI? Manual `scp`?
- [ ] **Env vars / secrets** on the box
- [ ] **Staging** — is it meant to be alive? credentials?
- [ ] **Backups** — do any exist? of what, where, how often?

**Data / registration system**
- [ ] Where do applications / selfies / participant profiles live (DB engine, storage path/bucket)?
- [ ] What sends verification codes — Twilio? SendGrid/Resend? A personal Gmail?
- [ ] Who reviews applications, and through what UI? Is there an admin panel we haven't seen?
- [ ] How is payment collected after approval today, and how is "confirmed" recorded?
- [ ] Where do `/api/course-interest` waitlist signups go, and does anyone act on them?
- [ ] Data retention / deletion process for selfies (they promise admin-removal on the form).

**Scope**
- [ ] **The "app"** — they mentioned app development. Is there an existing mobile app, a plan,
      or a store listing? (Nothing app-related is linked from the site.)

---

## 9. Questions to ask

1. Who built the current version, and are they available for a handoff call?
2. Why the rebuild/migration on Sept 9–15? Was it planned, or was something broken?
3. How many applications come in per session, and what does the manual review actually check?
4. How is payment collected today (invoice? Venmo/Zelle? in person?), and how often does an
   approved applicant fail to pay? (Sizes the value of online checkout.)
5. Every course but one shows "No upcoming dates." Is that seasonal, or is scheduling the bottleneck?
6. What does "app" mean to them — native iOS/Android, PWA, a booking/scheduling tool, an admin tool?
7. Merch: real store, or leave it as a link-out? (Nav says "Affiliates" and points at `/merch`.)
8. Budget/expectations for hosting — keep Hetzner, move to a US region, or consolidate onto infra
   we already run?
9. Any interest in gated/paid video given the 679-video YouTube catalog? (Not what they sell
   today; don't pitch it, just ask.)

---

## 10. Video hosting

**All video is on YouTube. The site hosts no video itself.** (confirmed — every page fetched)

- Across every route, exactly **one** embedded video: a homepage `<iframe>` of
  `https://www.youtube.com/embed/eea3Fitv-nU` ("Who is The Tactical Rabbi?"), with `i.ytimg.com`
  thumbnails. Two course pages (Active Shooter Response, Stress Box) each have a "Course videos"
  section that is a single outbound link to a public YouTube video (`watch?v=hYdeHeSfS48`,
  `watch?v=el8_ZB4WJzc`). No `<video>`, no `.mp4/.webm/.m3u8`, no Cloudflare Stream / Vimeo /
  Wistia / Mux / Bunny / JW Player anywhere.
- **YouTube channel:** `@TheTacticalRabbi`, channel ID `UCUj9deWle3pcj2BGofCvyhw` —
  **679 videos, 77.3K subscribers** (as of 2026-09-16). That's the audience; the website's job is
  converting some of it into class registrations.

Implications:
- YouTube = free hosting + the audience already lives there. Don't move public content off it.
- If they ever want **paid/gated video** (the Sierra model), our shared Cloudflare Stream account
  and the core `/api/videos` machinery are the fit. YouTube unlisted/private is not a real paywall.
  But that is *not* their business today (§12) — don't assume it.
- 679 videos with no index on the site: a searchable video library via the YouTube Data API is a
  cheap, high-value feature with zero hosting cost.

### What self-hosting his views would cost (Cloudflare Stream)

Cloudflare Stream bills **minutes delivered, not views**: **$1 per 1,000 minutes delivered** +
**$5/month per 1,000 minutes stored**, no free tier, and *client-side preloading/buffering counts
as billable delivery* (verified on developers.cloudflare.com/stream/pricing, 2026-09-16).

So 35M views (a plausible lifetime figure for a 679-video / 77K-sub channel) costs whatever
35M × average-minutes-watched works out to:

| Avg. watched per view | Minutes delivered | Delivery cost |
|---|---|---|
| 30 sec | 17.5M | $17,500 |
| 2 min | 70M | $70,000 |
| 4 min | 140M | $140,000 |
| 8 min | 280M | $280,000 |

Realistic band for ~10-minute training videos with 3–5 min retention: **$100K–$175K**, skewing
higher because of buffering. Storage is trivial: 679 × ~10 min ≈ 6,800 min ≈ **$35/month**.

Takeaway for the meeting: on YouTube those views cost **$0** and *earn* ad revenue. Stream (or
Mux, Bunny, etc.) only pays off for **gated** content where every delivered minute belongs to a
paying customer. Public library stays on YouTube; a paid course library is the only place a
Stream bill is worth paying.

---

## 11. What they actually sell — and how registration works

**In-person, live-fire range classes. Not video courses.** No videos are handed out, gated, or sold.

Catalog (from `/courses`, 2026-09-16):

| Course | Level | Length | Location | Price | Cap |
|---|---|---|---|---|---|
| Tactical Pistol | Beginner | 4 h | Henryville, PA | $275 | 8 |
| Tactical Rifle | Beginner | 4 h | Henryville, PA | $275 | 8 |
| Advanced Tactical Pistol | Advanced | 4 h | Henryville, PA | $275 | 8 |
| Advanced Tactical Rifle | Advanced | 4 h | Henryville, PA | $275 | 8 |
| Active Shooter Response | All | 4 h | Henryville, PA | $275 | 8 |
| Stress Box (shoot house) | Advanced | 4 h | Randolph, NJ | $350 | — |
| Private Lesson | All | flexible | by appointment | $175 | 1:1 |

Only **one** session open: Advanced Tactical Pistol, Sun 2026-09-20 10:00 EDT, session id
`035396ad-e282-4e6c-8a94-ebc64c3b1725`. Every other course shows "No upcoming dates" + a
"Notify me" form (→ `/api/course-interest` with the course slug). The catalog is mostly a
waitlist machine right now.

### Registration flow (observed on the live session page)

**Step 1 — pick a date.** Public details only. Copy: *"The exact training address is provided only
through the approved registration workflow."* and *"Applying does not reserve a seat. Only paid and
confirmed registrations count toward class capacity."*

**Step 2 — "Your application"** (an application, not a checkout):
- Legal first/last name ("as on government ID"), preferred name, email, phone
- "Have you registered or trained with The Tactical Rabbi before?" Yes/No
  - **Yes** ⇒ must verify identity first: `POST /api/participants/verification/start` →
    code sent → `POST /api/participants/verification/confirm` with `verificationCode`
- **Current selfie — required**, JPG/PNG/WebP ≤ 5 MB, uploaded via `/api/uploads/selfie`
  (multipart). Copy: *"used only for manual application review — not facial recognition — and
  retained with your participant profile until an administrator removes it. Verified returning
  participants may reuse the selfie already on file."*
- Firearms/training experience notes, free-text notes
- Required checkbox: cancellations non-refundable; transfers at administrator discretion
- Honeypot field `website`
- Submit ⇒ `POST /api/applications` (fields: `course`, `session`/`sessionId`, `legalFirstName`,
  `legalLastName`, `preferredName`, `email`, `phone`, `returningParticipant`, `selfie`,
  `experienceNotes`, `participantNotes`, `nonRefundableAcknowledged`, `verificationCode`, `website`)

**After submit is invisible from outside.** There is **no payment step on the site** (zero
Stripe/Square/PayPal/Venmo/Zelle references; the word "waiver" appears once, in prose). Given
"only paid and confirmed registrations count," payment is collected **off-site, manually, after
admin approval**. **Ask exactly how.**

Private Lesson has its own simpler request form (name/email/phone/training type/notes) —
"no course date or waiver is collected at this step."

### Why it's built this way (inferred)
Vetting applicants for live-fire firearms classes: legal name + selfie + returning-participant
verification + address released only after approval. A deliberate screening workflow, not
laziness. Any replacement we build must keep it — and it's exactly the kind of
pending → reviewed → approved/rejected → paid → confirmed lifecycle we run through BPMN on Sierra.
Sierra's classes product type maps almost 1:1 (course → session → application → payment).

---

## 12. Hosting provider — pinned down

**Hetzner Online GmbH, directly. Hetzner Cloud (VPS product), Helsinki datacenter (HEL1).
No reseller, no PaaS layer visible.**

| Evidence | Value |
|---|---|
| ASN | **AS24940 HETZNER-AS**, Hetzner Online GmbH, DE (Team Cymru + RIPE route object) |
| BGP prefix | `2.29.0.0/16`, route `descr: HETZNER-DC`, allocated 2010-09-21 |
| inetnum | `2.29.32.0 – 2.29.47.255`, netname **`CLOUD-HEL1`**, country FI, status ASSIGNED PA, org `ORG-HOA1-RIPE`, mnt-by `HOS-GUN` |
| inetnum created | **2026-09-09** — freshly registered Hetzner Cloud block, two days before the DNS cutover. Consistent with "spun up a new cloud server for the migration." |
| rDNS | `static.234.40.29.2.clients.your-server.de` — Hetzner's *default* rDNS; no custom PTR set |
| Product line | `CLOUD-*` netname ⇒ Hetzner **Cloud** (hourly-billed VPS via console.hetzner.cloud), not Hetzner **Robot** dedicated/auction hardware |
| Reseller / PaaS? | **No signs.** nginx directly on the edge (Coolify, Dokploy, CapRover, Kamal all put Traefik/Caddy/kamal-proxy there). No platform headers. Default rDNS. ⇒ hand-managed VM with a hand-written nginx config |
| Single-tenant? | Bogus `Host` header on 443 still serves the Tactical Rabbi page ⇒ it's the catch-all/default vhost. Reverse-IP lookup returned no other hostnames (block is only a week old, so indexes are thin — weak evidence, but nothing contradicts single-tenant). |

**Who to ask for:** the **Hetzner Cloud account** that owns the project containing this server —
that's the actual hosting relationship; whoever pays that invoice is the account holder. If the
outgoing developer owns it (very common), the clean move is: they add us as a project member, we
snapshot the server, then rebuild under an account the client controls.

Cost: a Hetzner Cloud VM in the class that runs nginx + one Node app is a few euros/month. There is
no hosting-cost reason to stay or leave — it's purely a control-and-location decision.

Residency: Helsinki, EU. Participant PII + selfies (§11) for US customers are stored in Finland.
Not illegal, but worth a sentence — a US region (Hetzner has Ashburn `ASH` and Hillsboro `HIL`) or
our own infra would be a more natural home.

---

## 13. Raw evidence snippets (for reference)

```
$ dig +short thetacticalrabbi.com A            → 2.29.40.234
$ dig +short thetacticalrabbi.com NS           → ns65/ns66.domaincontrol.com.
$ dig +short staging.thetacticalrabbi.com A    → 2.29.40.234
$ dig +short -x 2.29.40.234                    → static.234.40.29.2.clients.your-server.de.
$ whois -h whois.ripe.net 2.29.40.234          → inetnum 2.29.32.0-2.29.47.255, CLOUD-HEL1, FI,
                                                  ORG-HOA1-RIPE, created 2026-09-09
$ whois -h whois.cymru.com " -v 2.29.40.234"   → AS24940 | 2.29.0.0/16 | HETZNER-AS, DE
$ curl -I https://thetacticalrabbi.com
    HTTP/2 200
    server: nginx/1.28.3
    cache-control: no-store, must-revalidate
    vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch,
          Next-Url, X-Vinext-Interception-Context, X-Vinext-Mounted-Slots, X-Vinext-Rsc-Render-Mode
    strict-transport-security: max-age=31536000
    x-content-type-options: nosniff
    referrer-policy: strict-origin-when-cross-origin
$ curl -I .../_next/static/chunks/index-C-O1LOUf.js
    cache-control: public, max-age=31536000, immutable
    last-modified: Tue, 15 Sep 2026 17:09:19 GMT
$ curl -I -X OPTIONS https://thetacticalrabbi.com/api/course-interest
    HTTP/2 204, allow: OPTIONS, POST
$ curl --resolve bogus.example:443:2.29.40.234 https://bogus.example/   → 200, Tactical Rabbi page
$ curl -I http://2.29.40.234/                                             → 301 (nginx)
live cert: CN=thetacticalrabbi.com, Let's Encrypt YE1, Sep 11 2026 → Dec 10 2026
```

NewsletterSignup client code (deminified excerpt):
```js
fetch(`/api/course-interest`, {
  method: 'POST',
  headers: { 'content-type': 'application/json' },
  body: JSON.stringify({ email, courseSlug: 'all-courses', website })  // `website` = honeypot
})
```

RegistrationDateStep chunk — fetch targets and form fields:
```
fetch(`/api/applications`)                          POST
fetch(`/api/participants/verification/start`)       POST
fetch(`/api/participants/verification/confirm`)     POST
fetch(`/api/uploads/selfie`)                        POST (+ one PUT)
fields: course, session, sessionId, legalFirstName, legalLastName, preferredName, email, phone,
        returningParticipant, selfie, experienceNotes, participantNotes,
        nonRefundableAcknowledged, verificationCode, website
error strings: "Too many submission attempts were received…", "The application is too large…",
        "Verify your returning participant profile before submitting…"
```

Page meta: `<title>The Tactical Rabbi | Firearms Training & Security</title>` — "Professional
firearms training, security assessments, and preparedness education with Rabbi Raziel Cohen."
