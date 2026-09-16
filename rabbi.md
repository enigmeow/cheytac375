# The Tactical Rabbi — takeover research notes

> **Status:** research in progress. Started 2026-09-16. Purpose: prep for meeting to take over
> website + app development for thetacticalrabbi.com (Rabbi Raziel Cohen — firearms training,
> security assessments, preparedness education).
>
> Everything below came from passive, public observation (DNS, whois, HTTP headers, served JS,
> cert-transparency logs). Nothing was logged into or probed beyond public URLs.
> **Confirmed** = observed directly. **Inferred** = my read of the evidence; verify at the meeting.

---

## 1. Summary (read this first)

- **Site:** https://thetacticalrabbi.com — bespoke, hand-coded React site on an experimental
  Vite-based Next-compatible stack ("vinext" + Rolldown + React Server Components).
- **Hosting:** self-managed **Hetzner Cloud VPS** in Helsinki, nginx in front of a Node process.
  No CDN. Origin IP is publicly exposed.
- **DNS/registrar:** GoDaddy, WHOIS-privacy-shielded. Domain registered 2019.
- **Recent activity:** DNS record + TLS cert both changed **2026-09-11**; all static assets built
  **2026-09-15 17:09 UTC** (the day before I looked). This looks like a **relaunch/migration
  within the last week** — possibly the old developer's final push, or an in-flight migration
  we are inheriting mid-stream. **Ask about this.**
- **Staging env exists:** `staging.thetacticalrabbi.com` → same box. Cert for it has lapsed
  (current cert covers apex only), so staging may be half-decommissioned.
- **Backend is a real registration system, not just a brochure** (corrected 2026-09-16 pm — see
  §12): `/api/applications`, `/api/participants/verification/{start,confirm}`, `/api/uploads/selfie`,
  `/api/course-interest`. Applications are *reviewed and approved manually*; **no online payment**
  anywhere. No email (no MX), no commerce integration, no analytics observed.
- **Nothing SaaS-managed:** no WordPress/Wix/Squarespace/Vercel/Netlify. Whoever built this is a
  strong developer who likes very new tooling — which is also the main handoff risk (see §7).

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
| Provider | **Hetzner Online GmbH**, netname `CLOUD-HEL1` (Hetzner Cloud, Helsinki, Finland) | confirmed (RIPE whois) |
| rDNS | `static.234.40.29.2.clients.your-server.de` | confirmed |
| Web server | `nginx/1.28.3`, HTTP/2, ALPN h2 | confirmed |
| CDN / WAF | **none** — no Cloudflare/Fastly/Akamai headers, DNS points straight at origin | confirmed |
| TLS | Let's Encrypt, issuer `YE1`, subject `CN=thetacticalrabbi.com`, valid 2026-09-11 → 2026-12-10 | confirmed |
| TLS automation | ~60-day renewal cadence visible in CT logs since 2025-01 ⇒ certbot (or similar) on a timer | inferred |
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

Chunks (build ID hash suffixes stripped): `framework`, `index`, `rolldown-runtime`,
`navigation-errors`, `layout-segment-context`, `FutureDateSignup`, `NewsletterSignup`,
`PressMarquee`. All stamped `Last-Modified: Tue, 15 Sep 2026 17:09:19 GMT`. No source maps served
(`.js.map` → 404).

Routes observed (from nav links):
`/`, `/about`, `/contact`, `/courses`, `/courses/active-shooter-response`,
`/courses/private-lesson`, `/courses/tactical-pistol`, `/courses/tactical-rifle`, `/merch`.

Preloaded images: `/images/tactical-rabbi-logo.png`, `/images/hero.jpg`.

Missing basics (worth flagging as quick wins):
- `/robots.txt` → 404
- `/sitemap.xml` → 404
- `/.well-known/security.txt` → 404
- no `<meta name="generator">`, no analytics tag observed on homepage or `/merch`
- no CSP header

---

## 5. Backend / integrations

- **`POST /api/course-interest`** — first API route found (see §12 for the full registration API). `OPTIONS` → `204`, `allow: OPTIONS, POST`;
  `GET` → `405`. Called by `NewsletterSignup` with JSON body
  `{ email, courseSlug: "all-courses", website }`. The `website` field is a **honeypot** (spam
  trap). Response JSON has `message` / `error`. `FutureDateSignup` forms (4 on homepage, class
  `future-date-signup is-compact`) presumably post the same route with a real `courseSlug`.
  **Unknown: where do submissions go?** No MX, no third-party email/CRM host referenced in the
  client. Could be a DB on the box, a file, a webhook, or a server-side mailer via a third-party
  API. **Ask.**
- **Merch:** `/merch` has no Stripe/Shopify/Snipcart/Gumroad/PayPal — no commerce wired. Static
  or placeholder. (confirmed absence of client-side signals; a server-side redirect is possible)
- **Newsletter provider:** none observed client-side.
- **Third-party hosts referenced:** youtube.com, instagram.com, facebook.com (socials/embeds);
  press links to latimes.com, dailywire.com, dailymail.co.uk, video.foxnews.com, archive.org.
- **No auth / login surface** observed.

---

## 6. Timeline (reconstructed)

| Date | Event | Source |
|---|---|---|
| 2019-05-10 | Domain registered (GoDaddy) | whois |
| 2023-11-05 | GoDaddy wildcard cert ⇒ on GoDaddy hosting | crt.sh |
| 2025-01 | First Let's Encrypt cert ⇒ moved to self-hosted, automated renewals every ~60d | crt.sh |
| 2026-05-11 | Registrar-side domain update (renewal?) | whois |
| 2026-08-26 | Last pre-migration LE cert (`YR2`) | crt.sh |
| **2026-09-11** | Registry-side DNS update **and** new LE cert (`YE1`) on the Hetzner box | whois + live cert |
| **2026-09-15 17:09 UTC** | Current production build deployed | asset `Last-Modified` |
| 2026-09-16 | This research | — |

Interpretation (inferred): the site was rebuilt on the new stack and cut over to a new/rebuilt
Hetzner server within the last ~5 days, with a further deploy the day before I looked. Either the
outgoing dev is still actively shipping, or the client did the cutover themselves. Either way,
**the deploy pipeline was exercised very recently, so the person who ran it knows exactly how it
works — get that walkthrough while it's fresh.**

---

## 7. Risks / things I'd want to fix early

1. **Framework bus-factor.** vinext + Rolldown + `@vitejs/plugin-rsc` are all young. Upgrades
   may break; docs and community help are thin. Decide early whether to (a) keep it, (b) migrate to
   stock Next.js (conventions are already Next-shaped, so this is plausible), or (c) rebuild on our
   own FastAPI + static pattern. Don't decide until we've seen the repo.
2. **Origin exposed, no WAF/CDN.** Firearms-training site with a visible Hetzner IP. Cloudflare in
   front is a cheap, familiar win (we already run two zones this way).
3. **No SPF/DMARC.** Trivial spoofing of their domain. Fix once we control DNS.
4. **Staging cert lapsed / staging on prod box.** Either restore properly (separate vhost + cert)
   or remove the DNS record. Staging on the same box as prod is fine for their scale, but it should
   be basic-auth'd.
5. **SEO basics missing** (robots, sitemap, no analytics). Cheap.
6. **Unknown data path for signups.** Until we know where `/api/course-interest` writes, we can't
   promise leads aren't being lost.
7. **Hetzner is EU-hosted (Helsinki).** Latency for a US audience is fine-ish but not ideal; a
   CDN mitigates. Also check whether any US-only data-residency expectations exist (probably not).

---

## 8. Access we need to take over (checklist for the meeting)

- [ ] **Source repo** — where is it (GitHub? their laptop?), and is there git history?
- [ ] **Hetzner Cloud** account/project access, or at least SSH key on the box + root/sudo
- [ ] **GoDaddy** account access for DNS + domain (or authorize a transfer to our registrar)
- [ ] **Server details**: OS, how the Node process is run (systemd? pm2? Docker? Coolify/Dokploy?),
      nginx config location, certbot config
- [ ] **Deploy procedure** — exactly what they ran on 2026-09-15. Script? CI? Manual `scp`?
- [ ] **Env vars / secrets** on the box (anything behind `/api/course-interest`)
- [ ] **Where signups go** — DB dump, mailbox, spreadsheet, webhook target
- [ ] **Staging** — is it meant to be alive? credentials?
- [ ] **Social accounts** linked from site (YouTube, Instagram, Facebook) — who owns them.
      YouTube especially: 679 videos / 77.3K subs is the main asset — Brand Account or personal? (see §11)
- [ ] **Old GoDaddy hosting** — is anything still there / still being billed?
- [ ] **Backups** — do any exist?
- [ ] **The "app"** — they mentioned app development. Is there an existing mobile app, a plan,
      or a store listing? (Nothing app-related is linked from the site.)

## 9. Questions to ask

1. Who built the current version, and are they available for a handoff call?
2. Why the rebuild/migration on Sept 11–15? Was it planned, or was something broken?
3. What's the goal for merch — real store, or leave it as a link-out?
4. Course signups: how many come in, and how are they currently followed up?
5. What does "app" mean to them — native iOS/Android, PWA, a booking/scheduling tool?
6. Any payment processing today (Venmo/Zelle/Square in person)? Firearms-friendly processor
   considerations apply here just like Sierra (see `project_sierra_stripe_assumption` memory).
7. Budget/expectations for hosting — keep Hetzner, or consolidate onto infra we already run?

---

## 10. Raw evidence snippets (for reference)

```
$ dig +short thetacticalrabbi.com A            → 2.29.40.234
$ dig +short thetacticalrabbi.com NS           → ns65/ns66.domaincontrol.com.
$ dig +short staging.thetacticalrabbi.com A    → 2.29.40.234
$ dig +short -x 2.29.40.234                    → static.234.40.29.2.clients.your-server.de.
$ whois 2.29.40.234                            → inetnum 2.29.32.0-2.29.47.255, netname CLOUD-HEL1, Hetzner Online GmbH
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

Page meta: `<title>The Tactical Rabbi | Firearms Training & Security</title>` — "Professional
firearms training, security assessments, and preparedness education with Rabbi Raziel Cohen."

## 11. Video hosting

**All video is on YouTube. The site hosts no video itself.** (confirmed — every page fetched)

- Fetched every route (`/`, `/about`, `/contact`, `/courses`, all four `/courses/*`, `/merch`):
  exactly **one** video element on the whole site — a homepage `<iframe>` embed of
  `https://www.youtube.com/embed/eea3Fitv-nU` ("Who is The Tactical Rabbi?"), with
  `i.ytimg.com` thumbnails. No `<video>`, no `.mp4/.webm/.m3u8`, no Cloudflare Stream / Vimeo /
  Wistia / Mux / Bunny / JW Player anywhere.
- **YouTube channel:** `@TheTacticalRabbi`, channel ID `UCUj9deWle3pcj2BGofCvyhw` —
  **679 videos, 77.3K subscribers** (as of 2026-09-16). That's the real content library and the
  real audience; the website is a thin front door to it.
- Additional press links on inner pages: nypost.com, yahoo.com, ynetnews.com, jewishlink.news,
  anash.org.

Implications for the takeover:
- YouTube = free hosting + the audience already lives there. Don't move public content off it.
- If they want **paid/gated course video** (the Sierra model), that's where a private host earns
  its keep — our shared Cloudflare Stream account is the obvious fit, and the `/api/videos`
  machinery already exists in core. YouTube unlisted/private is not a real paywall.
- 679 videos is a large back-catalog: a searchable/categorized video index on the site (pulling
  from the YouTube Data API) is a cheap, high-value feature that costs nothing in hosting.
- Ask who owns the YouTube channel login + whether it's a Brand Account (transferable) or a
  personal Google account. Add to §8 checklist.

---

## 12. What they actually sell — and how registration works (CORRECTS earlier assumptions)

**They are not selling video courses. The "courses" are in-person, live-fire range classes.**
No videos are handed out, gated, or sold; YouTube links on course pages are public promo clips.

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

Only **one** session was open: Advanced Tactical Pistol, Sun 2026-09-20 10:00 EDT, session id
`035396ad-e282-4e6c-8a94-ebc64c3b1725`. Every other course shows "No upcoming dates" + a
"Notify me" form (→ `/api/course-interest` with the course slug). So the catalog is mostly a
waitlist machine right now.

"Course videos" sections exist on Active Shooter Response and Stress Box only — each is a single
outbound link to a public YouTube video (`watch?v=hYdeHeSfS48`, `watch?v=el8_ZB4WJzc`). Nothing
gated.

### Registration flow (observed on the live session page)

**Step 1 — pick a date.** Public details only. Copy: *"The exact training address is provided only
through the approved registration workflow."* and *"Applying does not reserve a seat. Only paid and
confirmed registrations count toward class capacity."*

**Step 2 — "Your application"** (it's an application, not a checkout):
- Legal first/last name ("as on government ID"), preferred name, email, phone
- "Have you registered or trained with The Tactical Rabbi before?" Yes/No
  - **Yes** ⇒ must verify identity first: `POST /api/participants/verification/start` →
    code sent → `POST /api/participants/verification/confirm` with `verificationCode`
- **Current selfie — required**, JPG/PNG/WebP ≤ 5 MB, uploaded via `POST /api/uploads/selfie`
  (multipart). Copy: *"used only for manual application review — not facial recognition — and
  retained with your participant profile until an administrator removes it. Verified returning
  participants may reuse the selfie already on file."*
- Firearms/training experience notes, free-text notes
- Required checkbox: cancellations non-refundable; transfers at administrator discretion
- Honeypot field `website`
- Submit ⇒ `POST /api/applications` (fields: `course`, `session`/`sessionId`, `legalFirstName`,
  `legalLastName`, `preferredName`, `email`, `phone`, `returningParticipant`, `selfie`,
  `experienceNotes`, `participantNotes`, `nonRefundableAcknowledged`, `verificationCode`, `website`)
- Client error strings reveal rate limiting on the backend ("Too many submission attempts…") and a
  payload-size cap.

**What happens after submit is invisible from outside.** There is **no payment step on the site**
(zero Stripe/Square/PayPal/Venmo/Zelle references; only one "waiver" word, in prose). Given "only
paid and confirmed registrations count," payment must be collected **off-site, manually, after
admin approval** — invoice, Venmo/Zelle, phone. **Ask exactly how.** This is the single biggest
product gap and the most obvious thing we'd build.

Private Lesson has its own simpler request form (name/email/phone/training type/notes) —
presumably also `/api/applications` or `/api/course-interest`.

### Why it's built this way (inferred)
Vetting applicants for live-fire firearms classes: legal name + selfie + returning-participant
verification + address released only after approval. That's a deliberate screening workflow, not
laziness. Any replacement we build must keep it — it's also exactly the kind of
pending → reviewed → approved/rejected → paid → confirmed lifecycle we run through BPMN on Sierra.

### Backend surface (client-observed)
| Route | Method | Purpose |
|---|---|---|
| `/api/course-interest` | POST | waitlist / notify-me (email + courseSlug + honeypot) |
| `/api/applications` | POST | class application (multipart or JSON, with selfie ref) |
| `/api/participants/verification/start` | POST | send verification code to returning participant |
| `/api/participants/verification/confirm` | POST | confirm code |
| `/api/uploads/selfie` | POST/PUT | selfie upload (the one `PUT` in the chunk is probably a direct-to-storage step) |

⇒ There is a **database with participant profiles, sessions, applications, and stored selfies
(PII + biometric-adjacent images)** on that Hetzner box or attached storage, plus some way to send
verification codes (SMS or email — no MX on the domain, so a third-party API). **All of this is
in scope for the handoff: where is the data, who can see it, is it backed up, retention policy.**

### Other notes
- Nav "Affiliates" link points at `/merch` (label/route mismatch); `/affiliates` itself is a 404.
- Favicons versioned `?v=20260902-exact-logo` ⇒ another deploy on/around 2026-09-02.
- Course pages link to `/contact?interest=<slug>` — contact form is interest-aware.
- Sierra parallel: this catalog is close to Sierra's "classes" product type. If we ever fold
  them onto our platform, the model maps almost 1:1 (course → session → application → payment).

### Add to §8 checklist
- [ ] Where do applications/selfies/participant profiles live (DB engine, storage path/bucket)?
- [ ] What sends verification codes — Twilio? SendGrid/Resend? A personal Gmail?
- [ ] Who reviews applications, and through what UI? Is there an admin panel we haven't seen?
- [ ] How is payment collected after approval today, and how is "confirmed" recorded?
- [ ] Data retention / deletion process for selfies (they promise admin-removal on the form).
