# .375 CheyTac Build Plan — Heavy ELR, No-Compromise

> **Status:** v1 draft, 2026-05-15. Build path is turnkey custom, single-shot, no-compromise budget. Open questions called out inline and consolidated in §11.

## 1. Scope

Build a dedicated **Heavy ELR** competition rifle in .375 CheyTac. Targets: King of 2 Miles class — single-shot, no weight cap, maximum BC bullets, 2-mile-and-out from bench/prone. Not a hunting rifle, not a light-class match gun, not portable.

**Locked decisions (from scoping conversation):**
| Decision | Choice | Reason |
|---|---|---|
| Cartridge | .375 CheyTac (classic) | Owner already shoots .375 CT — brass, dies, load data carry over. |
| Feed | Single-shot | Rigid platform, accommodates any OAL, standard for KO2M-class builds. |
| Action class | BAT EX / EXS-tier | Largest practical custom action; chambers both .375 CT and .50 BMG bolt heads if you ever want a second barrel. |
| Build path | Turnkey custom build (one shop sources, fits, chambers, test-fires) | Most predictable for a cartridge that requires real lathe work. |
| Budget tier | $18k+ — best-of-everything | Drives action, barrel, glass, mount, and bipod choices. |
| **Twist rate** | **Gain twist 10→9 (or straight 1:9)** | Optimal SG (~2.1 at sea level, ~1.9 at altitude) for 350gr at 3,000 fps. Clears transonic with margin, no overspin drag penalty. Victrix's 1:10 is conservative; 1:7 is overkill. |
| **Bullet weight** | **350gr** | Owner's existing load. 1:9 stabilizes 350gr with ~SG 2.0 — Applied Ballistics sweet spot. Headroom for up to 380gr if owner ever wants to chase a higher-BC option. |

**Explicitly out of scope for v1:** .375 EnABELR alternative path (skipped per owner). Repeater builds. Light ELR / NRL ELR weight-capped rifles. Hunting builds.

---

## 2. What carries over from the existing Victrix .375 CT

Owner's existing rifle is a **Victrix Armaments Tormento** in .375 CheyTac (30" barrel, 1:10 twist, button-rifled 416R, 3-port brake — [Victrix product page](https://victrixarmaments.com/en/tormento/)). The build goal is a *sibling* rifle that shares loaded-ammo compatibility, not a totally divergent platform.

The following do NOT need to be re-sourced for this build (confirm inventory before final order):

- **Brass** — Peterson .375 CT and/or ADG, already fire-formed to the Victrix chamber. **Caveat:** new chamber will fire-form once — brass works but won't be as concentric on first fire as it will after 1–2 firings in the new chamber. Headstamp-segregate the new-chamber lot.
- **Dies** — full-length, neck, seater. Reuse if from Warner Tool, Whidden, Shoot-Long, or similar. **Caveat:** chamber-specific neck-sizing dies tuned to the Victrix may need a fresh bushing or re-tuning for the new chamber's neck dimensions.
- **Load data** — owner's existing 350gr recipe is the starting point. Every barrel has its own pressure/velocity curve, so expect a small ladder to confirm node — but powder, primer, COAL, and bullet are all carried over.
- **Bullets** — owner's existing supply of **Cutting Edge .375 350gr Lazer LRT-SF** (G1 0.807 / G7 0.414, OAL 2.078", projection 1.479", CE-spec twist requirement 1:10 or faster — see §7). Directly reusable — same bore, same SG regime in 1:9 as in the Victrix's 1:10. CE's bullets are a confirmed match for this build.

**What this means for the doc:** the reloading-bench section is skipped. We only spec the rifle.

### What we're really matching the Victrix for — and what we're not

**Important framing correction:** the goal of "matching the Victrix" is *not* identical dope cards. Every rifle has to be trued on its own — even two rifles with identical components will print different dope because each barrel has its own velocity (chamber length, bore finish, throat geometry differ), and the new 36" barrel will run ~150 fps faster than the Victrix's 30" regardless of anything else we match. A ballistic solver regenerates a dope card in 30 seconds from a chronograph reading, so dope-card portability isn't a meaningful labor savings.

What we *actually* need from Victrix compatibility:

1. **Loaded rounds chamber safely in both rifles.** This is the safety concern. If the new chamber's freebore is shorter than the Victrix's, a Victrix-loaded round seats the bullet into the lands → pressure spike → dangerous. If longer, the bullet jumps farther → less accurate but safe. The fix: chamber cast or reamer print from Victrix.
2. **The load recipe transfers.** Same brass, same powder, same charge, same primer, same COAL all work in the new chamber within safe pressure limits.
3. **Same stability regime (SG).** Bullet flies similarly — wind drift behavior, transonic behavior, drag model holds.

What we *don't* need and aren't trying to match:
- Identical velocity (longer barrel = faster, that's a feature — buys ~150 fps and ~1.5 mils less drop at 2 miles)
- Identical dope card (re-true the new rifle, takes one range session per shooter)
- Identical group size (every barrel is its own thing)

### Why 1:9 (gain twist 10→9), not Victrix's 1:10?

The Victrix's 1:10 stabilizes 350gr safely but conservatively — SG ≈ 1.7 at sea level, dropping to ~1.5 at altitude. Applied Ballistics' rule for ELR is "SG > 1.5 at the transonic boundary"; 1:10 is right on the edge.

**Gain twist 10→9 puts SG at ~2.1 at sea level and ~1.9 at altitude.** That's the sweet spot — comfortably above the transonic threshold, no overspin-induced drag penalty (which starts kicking in above SG ~2.5 for 350gr), and headroom for up to ~380gr bullets if you ever swap.

**Ammo portability:** the existing 350gr load is still fully safe and accurate in the new 1:9 — the bullet just stabilizes with more margin. Dope card won't be *identical* to the Victrix's (different SG → slightly different gyroscopic drift, plus 36" barrel = +150 fps), but it's a small velocity-correction in a ballistic solver, not a re-tune. **You can shoot the same loaded rounds in both rifles without modification.**

**What you give up vs sticking with 1:10:** essentially nothing for 350gr. The dope card translates with a velocity correction either way (because the longer barrel changes velocity regardless of twist).

---

## 3. Parts list — subsystem by subsystem

### 3.1 Action — BAT EX / EXS, single-shot

The BAT Machine **EX** (or the slightly smaller **EXS**) is the standard for Heavy ELR .375 CheyTac. The EXS is BAT's smallest CheyTac-and-BMG-capable action, designed specifically for ELR shooters working under match weight caps; the full EX is the no-compromise choice when weight is not a concern.

- **Primary:** BAT Machine **EX** single-shot, .750" firing pin, integral 30 MOA or 40 MOA rail. ([batmachine.com](https://www.batmachine.com/bat-actions/))
- **Alternate 1:** BAT **EXS** — same family, smaller footprint, more chassis options. Use this if a specific chassis won't inlet the full EX.
- **Alternate 2:** Stiller **TAC 408** (1.450" diameter) single-feed — well-proven, slightly cheaper, more chassis inlets available.
- **Alternate 3:** Defiance **Deviant XM** in CheyTac single-shot config — Defiance's reputation is excellent, fit-and-finish on par with BAT.
- **Spec to order:** right-bolt right-eject, .375 CT bolt face, integral 40 MOA rail, fluted bolt, large knob.

**Source:** BAT direct (long lead — 6–12 months) or [Bullet Central](https://bulletcentral.com/actions/) (sometimes carries stock). Order this **first** — everything else builds around it.

**Open Q (§11):** if owner's existing CheyTac is also BAT-based, consider standardizing on the same brand for parts/scope-base commonality.

---

### 3.2 Barrel — Bartlein gain twist 10→9, 36" (KO2M Heavy ELR sweet spot)

**Twist locked at gain twist 10→9** — the perfect twist for 350gr at 3,000 fps. Bartlein offers this explicitly. Same SG at the muzzle as straight 1:9 (~2.1 at sea level), with lower bullet engraving stress at the chamber end. Cut-rifled, single-point, premium-grade only.

**Length: 36"** — the KO2M Heavy ELR sweet spot. Six inches longer than the Victrix's 30" buys roughly **~150 fps of muzzle velocity** from the same 350gr load (~25–30 fps per inch). At 2 miles, that's about 1.5 mils less drop and noticeably less wind drift. 36" stays within the harmonics envelope of a heavy MTU/1.450" contour — past 38" you start losing stiffness per unit length, and 40" is where match shooters report real whip and POI walk.

- **Primary:** **Bartlein** 5R cut-rifled, **gain twist 10→9**, 1.450" → 0.95" Heavy Palma+ or MTU contour finished at **36"**, threaded to brake spec. Cerakote or bead-blast stainless. ([bartleinbarrels.com](https://bartleinbarrels.com/))
- **Alternate 1:** **Bartlein straight 1:9**, same contour and length. Mechanically simpler, easier to source, ~98% of the gain-twist benefit for 350gr.
- **Alternate 2:** **Brux** cut-rifled, gain twist 10→9 or straight 1:9, same contour. Often shorter lead times than Bartlein. ([bruxbarrels.com](https://bruxbarrels.com/))
- **Alternate 3:** **Krieger** 5R, 1:9. Historically the ELR gold standard, longest lead times (often 12+ months).
- **Outer-envelope option:** **38" finished length** — adds another ~50 fps but loses some stiffness; only worth it if you have a specific 2-mile range and want maximum velocity. Defer to the builder's recommendation given chassis fit and balance.
- **NOT recommended:** 1:7 or 1:8 gain twist — over-spins 350gr enough to measurably hurt accuracy via overspin-induced drag and dispersion. Reserve for a future 400gr-bullet build.
- **NOT recommended:** Proof CF for *Heavy* ELR — carbon-wrapped is for weight-limited builds. For no-cap Heavy, run a heavy steel contour for rigidity and thermal mass.

**Spec to order:** call Bartlein with the bullet: "Cutting Edge .375 350gr Lazer LRT-SF (single-feed, OAL 2.078", projection 1.479", G7 0.414), reamer print to match Victrix Tormento .375 CT chamber, **gain twist 10→9**, **36"** finished, MTU contour, threaded for [brake spec]." **Throat must match the owner's existing Victrix chamber** so loaded rounds chamber and engage the lands identically in both rifles — get a chamber cast from the Victrix and ship to the smith. (See §11 #2.)

**Length trade-off vs Victrix:**
| Length | MV (350gr est.) | vs Victrix 30" | Notes |
|---|---|---|---|
| 30" (Victrix) | ~2,950 fps | baseline | |
| 32" | ~3,000 fps | +50 fps | Modest gain |
| 34" | ~3,050 fps | +100 fps | Common KO2M length |
| **36"** | **~3,100 fps** | **+150 fps** | **Recommended — sweet spot** |
| 38" | ~3,150 fps | +200 fps | Diminishing returns + whip risk |
| 40" | ~3,180 fps | +230 fps | Not recommended |

Chronograph the new rifle, plug into ballistic solver (Hornady 4DOF / Applied Ballistics), re-print dope card. Same bullet, same load, same SG regime as Victrix — just faster.

---

### 3.3 Chassis — ARC ELR or MPA BA Comp Heavy

For no-cap Heavy ELR, the two dominant chassis are **Accurate Rifle Systems (ARC) ELR Chassis** and **MPA (Masterpiece Arms) BA Competition Heavy**. Both inlet for BAT EX, both have third-party-validated KO2M placements.

- **Primary:** **ARC ELR Chassis** with BAT EX inlet. Modular, adjustable cheek/LOP/buttplate, integrated arca/M-LOK. Used in *Ultimate Reloader*'s flagship .375 CT build. ([accuracysolutionsinc.com](https://www.accuracysolutionsinc.com/))
- **Alternate 1:** **MPA BA Competition Heavy** (or "Comp BA") with BAT EX inlet. ([masterpiecearms.com](https://masterpiecearms.com/))
- **Alternate 2:** **Cadex CDX-40 Shadow** chassis — Cadex builds full rifles in this platform; chassis-only is available. Already used for production .375 CT builds. ([cadexdefence.com](https://www.cadexdefence.com/))
- **Alternate 3 (stock, not chassis):** **McMillan A5** with full adjustability and three-way adjustable buttplate — old-school, beautifully made, what Vestal's typically pillar-beds onto. Heavier-feeling, less modular.

**Decision factor:** the builder you pick may have a strong preference / pre-existing inlet jigs. Defer final chassis choice to the builder unless you have a strong aesthetic preference.

---

### 3.4 Trigger — Bix'n Andy TacSport Pro or TriggerTech Diamond Pro

- **Primary:** **Bix'n Andy TacSport Pro** two-stage, BAT-compatible. Heavy-trigger camp's gold standard. ([bixnandy.com](https://bixnandy.com/))
- **Alternate 1:** **TriggerTech Diamond Pro** single-stage, frictionless release. PRS/ELR favorite. ([triggertech.com](https://triggertech.com/))
- **Alternate 2:** **Jewell HVR** — old school single-stage, still excellent.

**Pull weight:** 8–12 oz typical for ELR. Owner's preference (single vs two-stage) is the deciding factor.

---

### 3.5 Muzzle brake — APA Little/Fat Bastard or Terminator T5

.375 CheyTac generates significant recoil even from a 25+ lb rifle. A brake is mandatory both for spotting impacts and for repeatable position behind the gun.

- **Primary:** **American Precision Arms (APA) Fat Bastard Gen 3** in .375. Three-port, 100% gas redirection forward-and-rear, near-zero rearward thrust. ([americanprecisionarms.com](https://www.americanprecisionarms.com/))
- **Alternate 1:** **Terminator T5** — what's in the Sniper's Hide kit gun and many Bartlein-recommended builds.
- **Alternate 2:** **Area 419 Hellfire Maverick** — newer, gaining KO2M traction.

**Spec:** thread to barrel maker's specified shank diameter and pitch (Bartlein will spec this on order — typically 1.000"-20 or 1.125"-20 for this contour). Timed brake, not self-timing.

---

### 3.6 Optic — Kahles K540i DLR, 5–40×56 (locked)

**Kahles K540i DLR**, 5–40×56, **36mm tube, 29 mils internal elevation**, FFP, illuminated, integrated parallax, zero stop, twist guard. The **DLR variant** (100 clicks/revolution, "EasyRead" elevation turret) is the ELR competition spec — faster dialing, cleaner under-pressure readout than the standard 160-click turret. ([kahles.at](https://www.kahles.at/) · [Area 419 — K540i DLR](https://www.area419.com/product/kahles-k540i/) · [Precision Rifle Australia review](https://precision-rifle.com.au/2025/01/17/kahles-k540i/))

**Reticle:** **SKMR4+** — Kahles' best ELR reticle, full mil-grid Christmas tree, hold values to 14 mils. The MSR2/Ki is the alternative if you prefer slightly simpler wind references. The AMR (Applied Ballistics) is more PRS-oriented.

**Approximate price:** $4,500 (DLR variant, SKMR4+, right-hand windage).

**System elevation math for 2-mile capability:**

| Source | Mils |
|---|---|
| K540i internal travel | 29 |
| Action rail (40 MOA) | 11.6 |
| Spuhr SP-6602 mount cant (60 MOA) | 17.5 |
| **Total mechanical** | **~58 mils** |

A 350gr Lazer at 3,100 fps needs roughly **40–45 mils** of dial-up to reach 2,000 yards (depending on atmospherics) and **80–95 mils** to reach 2 miles (3,520 yards). So:
- **To 2,000 yards:** mechanical-only is fine. Skip the TARAC and just dial.
- **To 2 miles:** you need an optical assist. **Charlie TARAC is mandatory** for this build — see §3.7.

**Why Kahles K540i over the other "alpha tier" scopes:**
- Glass is alpha-class — same Schott HT tier as ZCO and S&B.
- Tracking and return-to-zero are bulletproof; Kahles' integrated parallax-in-turret has been refined over four generations.
- DLR turret was *designed* for competition dialing speed.
- 5–40x magnification range is wider than ZCO (5–27) and matches the heaviest March/S&B options.
- Lighter than ZCO ZC527 (~1,110g vs ~1,250g).
- Reliable shipping and warranty support in the US.

**Trade-off vs March Genesis 4–40×52:** Genesis has 44 mils internal elevation (vs Kahles' 29), which means with the same base hardware Genesis could reach 2 miles *without* a TARAC. Genesis advantage: one less optic to integrate. Kahles advantage: better glass, mature platform, faster turret feel. Net: this build accepts the TARAC trade and goes Kahles.

**Sources to order from:** [EuroOptic](https://www.eurooptic.com/), [Area 419](https://www.area419.com/) (carries the DLR variant), [LRI / Liberty Optics](https://www.libertyoptics.com/), [B&H Photo](https://www.bhphotovideo.com/).

---

### 3.7 Scope mount + cant + Charlie TARAC (mandatory for 2 miles)

**Mount:** **Spuhr SP-6602** for the Kahles K540i's **36mm tube**, with 60 MOA built-in cant. Stacked on the action's 40 MOA integral rail = **100 MOA total base cant** (~29 mils). ([spuhr.biz](https://spuhr.biz/))

- **Primary:** Spuhr **SP-6602** (36mm rings, 60 MOA cant). Confirm ring height for K540i's 56mm objective + heavy contour barrel — likely H38 or H44.
- **Alternate 1:** **ERA-TAC adjustable** in 36mm — variable 0–70 MOA cant, lets you tune without re-buying. Heavier; some prefer this for ELR.
- **Alternate 2:** **ARC M-Brace** in 36mm — purpose-built ELR mount, used in the *Ultimate Reloader* reference build.

**Charlie TARAC: MANDATORY for this build.** The Kahles K540i's 29 mils internal elevation + 100 MOA base cant gets you to ~2,000 yards. For 2 miles (3,520 yd) you need an optical assist. The **Charlie TARAC** is a periscope-prism device that optically shifts the target image up before it enters your scope, adding effective elevation without moving the scope's mechanical zero. ([tacomhq.com/charlie-tarac](https://tacomhq.com/charlie-tarac/))

- **Primary:** **Charlie TARAC Mk8 variable** — 0–250 mils (0–850 MOA), continuously adjustable. ~$2,000. Right answer for a no-compromise build because you can tune the boost rather than living with a fixed prism.
- **Alternate:** **Charlie TARAC Mk6 fixed prism** — 60 mils (200 MOA) fixed. ~$1,200. Cheaper but you commit to one elevation boost.
- **Mounting:** TARAC bolts to the same Picatinny rail as the scope mount; comes with rail-and-rings interface. Confirm rail length on chosen chassis is sufficient (most ELR chassis ship with 8–10" forward rail real estate).

**Total system elevation with Kahles K540i + Spuhr 60 MOA + 40 MOA rail + Charlie TARAC variable:** ~58 mils mechanical + 250 mils optical = **~308 mils**. Massive overshoot for 2 miles; gives flexibility to zero conservatively and run shorter optical boosts for typical ranges.

---

### 3.8 Rings (if Spuhr is not chosen)

Spuhr mounts are one-piece. If you use a separate base + rings:
- **Nightforce X-Treme Duty Ultralite** rings, 34mm or 36mm
- **Spuhr ISMS** rings
- **Hawkins Precision** heavy tactical rings

---

### 3.9 Bipod — LRA Light Tactical or Phoenix

For dedicated Heavy ELR (square range, prone, KO2M-style), the **LRA (Long Range Accuracy) Light Tactical** is the dominant choice — it puts the bipod apex *over* the bore axis, which keeps the rifle from torquing under recoil.

- **Primary:** **LRA Light Tactical Bipod** ([longrangeaccuracy.com](https://www.longrangeaccuracy.com/))
- **Alternate 1:** **Phoenix Precision Bipod** — common at KO2M, slightly slower for elevation adjustments per user reports.
- **Alternate 2:** **MDT Ckye-Pod** — 57% of top PRS shooters use it as their primary, but it's overkill for static ELR. Use if you also want a PRS-capable bipod.
- **Avoid:** Atlas / Harris — undersized for this rifle weight.

---

### 3.10 Rear support

- **Primary:** **Armageddon Gear Game Changer** (standard or "Pint Size") filled with heavy fill (steel shot or Lyman tumbling media).
- **Alternate:** **Wiebad Tac Pad** or **Fortune Cookie**.
- For pure bench/prone KO2M work, many shooters run a dedicated **rear sandbag** instead (Edgewood, Protektor) for max stability.

---

### 3.11 Suppressor (optional, recommended)

A .375 CheyTac with a Fat Bastard brake is *brutally* loud — well over 170 dB at the shooter's left ear. ELR matches allow suppressors. **Strongly recommend.**

- **Primary:** **Thunder Beast Arms Ultra 9** or **Ultra 12** in .375. (Match-class titanium.) ([thunderbeastarms.com](https://thunderbeastarms.com/))
- **Alternate:** **Q Full Auto** in .375, or **OCL Polonium 50** (rated for .50 BMG, so .375 CT is well within envelope).

**ATF Form 4 wait:** typically 30–90 days as of 2026. Order parallel with the build.

---

## 4. Builder shortlist (turnkey)

### KO2M validation: the rifle you already own is the right family

The **2024 King of 2 Miles winners** (Polish team Kuba Sidorowicz / Maciej Stasiak) shot a **Victrix Crown in .375 CheyTac** — the next-tier-up sibling of the owner's existing Victrix Tormento. That tells you two things: (1) the Victrix platform is genuinely KO2M-class hardware, and (2) the matched-sibling path (Victrix Crown alongside the Tormento) is a credible answer to "which builder."

Three credible paths from here:

**Path A — Buy the matched Victrix Crown.** Skip the custom-build process entirely. The Crown is purpose-built for Heavy ELR, ships with a longer/heavier barrel than the Tormento, and is guaranteed to have a chamber that's identical (or nearly so) to your existing rifle. Distributed in the US by [B&B Firearms](https://bnbfirearms.com/), [Solid Solution Designs](https://www.solidsolutiondesigns.com/), [American Precision Firearms](https://americanprecisionfirearms.com/), and others. Trade-off: less freedom to pick individual components (action, chassis, brake), and the barrel is button-rifled 416R rather than cut-rifled Bartlein. Cost: probably $15–18k including a Kahles K540i package.

**Path B — Tier-1 custom builder.** Build the spec'd parts list with one of the four shops below. These are the names that appear on KO2M podium finishers' rifles.

**Path C — Tier-2 custom builder.** Same parts list, less famous shop, often shorter lead times and tighter prices.

### Tier-1 custom builders (KO2M-podium-grade)

| Builder | Location | Strengths | KO2M / .375 CT track record |
|---|---|---|---|
| **Alamo Precision Rifles (APR)** | Hurst, TX | Catalog .375 CT in their store (Stiller TAC 408 + K&P barrel + McMillan A5); production-grade repeatability; reportedly 4-week quote-to-build turnaround on standard configs (verify for custom). Fast for this tier. | [APR Custom 375 CT in their catalog](https://aprifles.com/products/apr-custom-375-cheytac) — referenced by multiple KO2M shooters. |
| **Vestal's Custom Rifles** | Bristol, VA (was TX) | Robert Vestal personally builds; Bartlein-based; uses Cadex or McMillan stocks; Robert also teaches ELR clinics and wind-reading. Highest-touch shop on the list. | Multiple .375 CT ELR builds documented; [Vestal's CDX-40 Shadow .375 CT for sale](https://www.snipershide.com/shooting/threads/sold-elr-ready-vestals-custom-rifles-cadex-cdx-40-shadow-32-1-7-375-cheytac.7021368/). |
| **Global Precision Group (GPG)** | (Paul Phillips' shop) | **Paul Phillips won KO2M 2017** and is one of the most-named individuals in ELR. GPG builds for serious competitors. Likely longest lead times in tier 1 because of demand. | [Paul Phillips KO2M 2-mile-shot walkthrough](https://ultimatereloader.com/2025/06/08/the-2-mile-shot-getting-on-target-with-paul-phillips-gpg/) — 2017 King of 2 Miles champion. |
| **Warner Tool Company** | NH | Vertical integration: they make the .375 Flatline bullets, the dies, *and* the rifles. One vendor for projectile + chamber compatibility. | Built Marco Been's KO2M .375 CT. |

### Tier-2 custom builders (excellent, less-famous)

| Builder | Location | Strengths |
|---|---|---|
| **K&P Gunsmithing** | TX | Makes the barrel APR uses on their flagship .375 CT; will build full rifles around their own tubes. |
| **Lethal Precision Arms (Mitchell Fitzpatrick)** | (Fitzpatrick's shop) | Mitchell won a KO2M with a self-built rig; sells builds from his shop. |
| **Long Rifles Inc (LRI)** | SD | Ship-them-the-parts model; shorter wait than full-source builds. Good if you want to source components yourself. |
| **Dzuro's Guns** | Lake Havasu City, AZ | Custom ELR builds, BAT-action experience. ([dzurosguns.com](https://dzurosguns.com/custom_rifles.php)) |
| **Great Southern Gunworks (Extreme Rifles)** | GA | ELR specialist; 2-mile-capable builds. ([extremerifles.com](https://www.extremerifles.com/tac)) |
| **Ashbury Precision Ordnance** | VA | Chassis-and-action-integration specialist; APO ELR chassis is their own product. |

### NOT recommended

- **Surgeon Rifles** — their actions don't go to .375 CheyTac. Skip.
- **Production "custom" houses with no .375 CT in portfolio** — there's enough cartridge-specific knowledge (reamer print, throat dimensions, headspace, recoil mitigation, bedding) that you want a shop that's done it before. Don't be someone's first.

### Locked: Vestal's primary, quoting APR + GPG as competitive set

**Primary builder: Vestal's Custom Rifles** (Robert Vestal — Bristol, VA). Reasoning: highest-touch personal build, Robert's ELR-instructor reputation aligns with a no-compromise spec, Bartlein/Cadex aesthetic matches the parts list, KO2M-class .375 CT history.

**Quote competitors:**
- **Alamo Precision Rifles (APR)** — Hurst, TX. Closest production-grade analog; useful sanity check on price and lead time.
- **Global Precision Group (Paul Phillips)** — KO2M-champion-built; the "best possible smith" benchmark.

The RFQ email template in §12 covers all three shops. Send it to all three the same day so quote comparisons are apples-to-apples.

Compare quotes on:
1. **Lead time** — from action order to test-fire (expect 6–14 mo)
2. **Total price** — rifle delivered (without owner-supplied optic, mount, TARAC, suppressor)
3. **Component substitutions** — what does the shop want to substitute vs. the spec'd list? Listen to the smith on chassis (their fitting jigs matter) and brake (their crowning + timing process matters). Push back on bullet/twist/barrel-maker substitutions (those are locked).
4. **Victrix chamber-match willingness** — every shop should be able to chamber to a Cerrosafe cast you provide. If anyone refuses or wants "their reamer print" only, that's a deal-breaker for this build.
5. **Accuracy guarantee + test-fire scope** — expected group size, rounds fired, distance, target medium.

---

## 5. Build sequence

The long-lead items determine the schedule. Order in this sequence:

1. **Action — order day 1.** 6–12 month lead. Pick a builder before ordering so the action can ship directly to them.
2. **Optic — order day 1.** Some are 6+ months out (especially March Genesis and ZCO).
3. **Barrel — order once builder + reamer are confirmed.** Bartlein gain-twist is 6–9 months. Order before you have the action in hand; they'll ship to the smith.
4. **Suppressor (if buying) — file Form 4 day 1.** Even at 30–90 days, doesn't hurt to start.
5. **Chassis — order when builder confirms inlet availability for the action serial.** 2–4 months.
6. **Brake, trigger, rings/mount — order during build window.** Off-the-shelf, no lead.
7. **Bipod, rear bag — order last.** Same day delivery from most vendors.

**Total project timeline: 9–14 months from first order to first round downrange.**

---

## 6. Rough budget (no-compromise tier)

| Item | Estimate | Notes |
|---|---|---|
| BAT EX action | $3,000 | Direct from BAT or Bullet Central. |
| Bartlein gain-twist barrel | $850 | Cut-rifled, premium contour. |
| ARC ELR chassis (or MPA Comp Heavy) | $3,500 | Inletted for BAT EX. |
| Bix'n Andy TacSport Pro trigger | $650 | |
| APA Fat Bastard Gen 3 brake | $325 | Plus ~$100 timing/installation. |
| **Kahles K540i DLR 5-40×56** (SKMR4+ reticle) | $4,500 | Locked optic. Alpha-class glass + DLR turret + 36mm tube. |
| Spuhr SP-6602 mount w/ 60 MOA (36mm) | $750 | Stacks with 40 MOA rail for 100 MOA base. |
| Charlie TARAC Mk8 variable | $2,000 | Mandatory for 2-mile capability with K540i's 29 mil internal. |
| LRA Light Tactical bipod | $700 | |
| Armageddon Gear Game Changer | $120 | |
| Builder labor (chambering, fitting, test-fire) | $2,500 | Varies by shop; sometimes bundled into action+barrel quote. |
| **Subtotal (rifle, glass, mount, TARAC, bipod)** | **~$19,000** | |
| Thunder Beast Ultra 9 .375 (optional) | $1,800 | +$200 ATF stamp. |
| **Total with suppressor** | **~$21,000** | |

Add shipping, NFA tax stamp, FFL transfer fees (action goes through your dealer), and 8.5% sales tax (TX builders).

---

## 7. Bullet / load — Cutting Edge .375 350gr Lazer LRT-SF (locked)

Build is spec'd around the **Cutting Edge .375 350gr Lazer LRT-SF** — the projectile already running in the Victrix. Confirmed spec:

| Parameter | Value |
|---|---|
| Bullet | Cutting Edge .375 350gr Lazer LRT-SF (single-feed) |
| Caliber | .375 |
| Weight | 350 gr |
| **G1 BC** | **0.807** |
| **G7 BC** | **0.414** |
| OAL (overall length) | 2.078" |
| Projection length (out of case) | 1.479" |
| CE-stated minimum twist | 1:10 or faster |
| Source | [cuttingedgebullets.com](https://cuttingedgebullets.com/) |

**Stability check for our 1:9 gain-twist:**
| Condition | Estimated MV (36" barrel) | Estimated SG | Verdict |
|---|---|---|---|
| Sea level, 59 °F | ~3,100 fps | ~2.05 | Sweet spot |
| 6,000 ft, 20 °F | ~3,100 fps | ~1.85 | Comfortable margin |
| 10,000 ft transonic boundary | ~1,150 fps | ~1.7 | Above the 1.5 threshold — bullet stays asleep |

CE's "1:10 or faster" minimum is satisfied with ~30% margin. No over-stabilization concerns at this SG — solids don't have jacket-failure modes that justify worrying about overspin.

**Powder/primer/brass:** carry over from existing Victrix load. (Common starting points if working backward from CE's published loads: **Retumbo, RL-33, US869, or H50BMG**; primer **CCI 250 Magnum** or **Federal 215M**; brass **Peterson .375 CT** or **ADG**.)

**Throat/freebore implication for the new chamber:**
With 1.479" of bullet projecting from the case, the chamber freebore must accommodate seating the bullet to a sensible jump from the lands. The owner's Victrix already chambers this bullet at a known COAL — **the right move is to get a chamber cast (or reamer print) from Victrix and have Bartlein cut the new chamber to the same throat geometry.** Otherwise the same loaded round will land on the lands or jump differently in the two rifles, breaking dope-card portability. See §11 #2 (now elevated to highest priority).

**Headroom for future bullet swaps:**
1:9 gain twist will also stabilize:
- CE 377gr Lazer LRT-SF (G7 ~0.45)
- Warner Tool 364gr Flatline (G7 ~0.50)
- Hornady A-Tip 390gr (G7 ~0.50)

400gr Cutting Edge MTH-MAX and Warner Tool 400gr Flatline are the hard ceiling — *not* recommended in 1:9 (SG drops to ~1.4 at altitude). If you ever want those, plan for a separate barrel.

---

## 8. What we're NOT building

To prevent scope creep — explicitly excluded from this plan:

- A .408 CheyTac (covered in scoping conversation; .375 wins on BC, recoil, components)
- A .375 EnABELR (deliberately skipped per owner; revisit in v2 if interest changes)
- A repeater (single-shot is the right answer for this use case)
- A weight-capped (26 lb / 16 lb) "light ELR" build — different rifle, different chassis, different barrel
- A hunting rifle — totally different platform

---

## 9. Things that can ruin this build

Mistakes that show up in forum threads from people who built this and regretted it:

1. **Picking a builder who's never chambered .375 CT.** The reamer print and headspace tolerances are different from a typical magnum. Stick to the §4 list.
2. **Cheap rings/mount.** A $4,000 scope on $200 rings *will* shift under recoil. Spuhr-class or better, period.
3. **Wrong twist for 350gr.** 1:11.5 (CheyTac original spec) drops below SG 1.5 at altitude — transonic risk. 1:7+ over-spins 350gr and measurably hurts accuracy. Gain twist 10→9 or straight 1:9 is the right window.
4. **Skipping the suppressor.** Brake-only .375 CT is genuinely dangerous to the shooter and anyone left of the gun. Hearing protection alone is insufficient at extended sessions.
5. **Cheap rear bag.** Sub-MOA at 2 miles requires repeatable rear support. The Game Changer fill matters as much as the bag.
6. **Buying the optic last.** It's the second-longest lead item. Order it day 1.

---

## 10. Sources used (research backing the parts list)

- [Bullet Central — BAT action availability](https://bulletcentral.com/actions/)
- [BAT Machine Co — action lineup](https://www.batmachine.com/bat-actions/)
- [Ultimate Reloader — Building a 2-Mile .375 CheyTac (ARC chassis + BAT EX walkthrough)](https://ultimatereloader.com/2024/06/02/building-a-2-mile-rifle-375-cheytac-build/)
- [Alamo Precision Rifles — APR Custom .375 CheyTac](https://aprifles.com/products/apr-custom-375-cheytac)
- [Sniper's Hide — Vestal's Cadex CDX-40 .375 CT build](https://www.snipershide.com/shooting/threads/sold-elr-ready-vestals-custom-rifles-cadex-cdx-40-shadow-32-1-7-375-cheytac.7021368/)
- [AccurateShooter — Heavy Artillery: .375 CheyTac for 2 Miles](https://www.accurateshooter.com/guns-of-week/heavy-artillery-375-cheytac-for-2-miles/)
- [TACOM HQ — Charlie TARAC](https://tacomhq.com/charlie-tarac/)
- [Peterson Cartridge — .375 CheyTac brass](https://petersoncartridge.com/peterson-cartridge-makes-cheytac-caliber-casings)
- [PrecisionRifleBlog — Wyoming ELR Scopes & Mounts (what the pros use)](https://precisionrifleblog.com/2020/09/05/best-elr-scope-and-scope-mount-and-rings/)
- [Cutting Edge Bullets — 400gr Lazer LRT-SF](https://cuttingedgebullets.com/products/375-400gr-single-feed-lazer-tipped-hollow-point3)
- [Sniper's Hide — Best bipod for heavy ELR guns](https://www.snipershide.com/shooting/threads/best-bipod-for-heavy-elr-guns.7073192/)

---

## 11. Open questions for v2

**Resolved in v1.1–v1.4 (locked):**
- ~~Cartridge — .375 CheyTac classic.~~
- ~~Feed — single-shot.~~
- ~~Twist — gain twist 10→9, perfect for 350gr.~~
- ~~Barrel length — 36" (38" as outer envelope).~~
- ~~Bullet weight — 350gr (Victrix-portable load).~~
- ~~Bullet identity — Cutting Edge .375 350gr Lazer LRT-SF (G1 0.807 / G7 0.414, OAL 2.078", projection 1.479").~~
- ~~Optic — Kahles K540i DLR 5-40×56, SKMR4+ reticle.~~
- ~~Mount — Spuhr SP-6602 (36mm, 60 MOA), stacks with 40 MOA rail.~~
- ~~Charlie TARAC — Mk8 variable (0-250 mils) — mandatory for 2-mile capability with K540i.~~
- ~~Builder — Vestal's Custom Rifles (primary), with APR + GPG quote competitors. See §4 + §12 RFQ template.~~

**Still open (in priority order):**

1. **Victrix chamber cast / reamer print** — **highest priority, blocks barrel order.** Need a chamber cast from the Victrix (or call Victrix Armaments and ask for the .375 CT reamer print) so the new chamber's freebore matches. Without this, the same loaded round may chamber unsafely (bullet jammed into lands) in one of the two rifles. Cerrosafe cast is ~$30 of materials and 30 min of work.
2. **Verify existing Victrix load** — powder + charge weight + COAL + primer. Smith will want this to inform throat geometry. Velocity from the Victrix chrono will tell us what to expect from the new 36" barrel (rule of thumb: +25–30 fps/inch).
3. **Which chassis?** Defer to Vestal's preference (Cadex CDX-40 or McMillan A5 SuperMag typical), or pick now? Recommend deferring — bedding is chassis-specific.
4. **Suppressor: in this build or skip?** ATF Form 4 wait is 30–90 days but doesn't delay the rifle. See §18.
5. **Existing brass inventory:** how many fired cases on hand, firing count, neck-turned? Determines whether to order a fresh lot of Peterson at action-order time.
6. **Existing dies:** what set is owned (Warner Tool / Whidden / Shoot-Long)? FL + neck + seater complete? Confirm before new chamber dimensions are locked.
7. **Where does this rifle live?** Bench-only vs travel determines EX (heavier, stiffer) vs EXS (lighter, more portable).
8. **Doc location:** keep `cheytac.md` at the nearfield repo root, or move to a personal notes location? Not site code.
9. **Support gear inventory (from §13):** does any of the Vectronix LRF / Kestrel / Garmin chrono / spotting scope already exist from the Victrix kit? Affects the ~$7.7k support-gear budget add-on.
10. **Reloading bench inventory (from §14):** confirm press, decapping die, annealer, trimmer for .375 CT compatibility. Owner has the load working on the Victrix, so this should mostly be a verification pass.

---

## 12. RFQ email template (paste-and-tweak for all three shops)

Send the same email to Vestal's, APR, and GPG on the same day. Personalize the greeting + reference their work, but keep the spec identical so quotes are comparable.

**Contacts:**
- **Vestal's Custom Rifles** — Robert Vestal — via [vestalscustomrifles.com](https://vestalscustomrifles.com/) contact form, or phone the shop. Bristol, VA.
- **Alamo Precision Rifles** — via [aprifles.com](https://aprifles.com/) contact form. Hurst, TX.
- **Global Precision Group** — Paul Phillips' shop. Web presence is sparse; reachable via Ultimate Reloader / KO2M circles. Phone is reliable.

```
Subject: .375 CheyTac Heavy ELR build — RFQ for matched-sibling rifle to existing Victrix Tormento

Hi [Robert / APR team / Paul],

I'm planning a Heavy ELR .375 CheyTac build and would like a quote and lead-time
estimate. I already shoot a Victrix Tormento in .375 CT (1:10, 30") and want the
new rifle to be a "matched sibling" — same loaded ammunition (Cutting Edge 350gr
Lazer LRT-SF), longer barrel, faster twist for more transonic margin. Single-shot,
no weight cap, dedicated to KO2M-class use.

Locked spec (in order of priority):

  1. Cartridge / use:  .375 CheyTac, single-shot, Heavy ELR (no weight cap)
  2. Bullet / load:    Cutting Edge .375 350gr Lazer LRT-SF (G1 0.807 / G7 0.414,
                       OAL 2.078", projection 1.479"). Existing recipe carries over
                       from Victrix.
  3. Chamber:          Must accept rounds loaded for my Victrix Tormento. I can
                       provide a Cerrosafe chamber cast of the Victrix; please
                       chamber to match its freebore/throat. If you require your
                       own reamer print, please flag — this is a deal-breaker
                       requirement for the build.
  4. Barrel:           Bartlein cut-rifled, gain twist 10→9 (or straight 1:9 if
                       you strongly prefer), 36" finished, MTU or 1.450"→0.95"
                       Heavy Palma+ contour, threaded for the brake you recommend.
                       Brux or Krieger as alternates if Bartlein lead time is
                       prohibitive.
  5. Action:           BAT EX or EXS single-shot, .375 CT bolt face, integral
                       40 MOA rail, right-bolt right-eject. Stiller TAC 408
                       single-feed acceptable as alternate. Defiance Deviant XM
                       acceptable as alternate.
  6. Trigger:          Bix'n Andy TacSport Pro (preferred) or TriggerTech Diamond
                       Pro. Open to your preference.
  7. Brake:            APA Fat Bastard Gen 3 (preferred), Terminator T5, or Area
                       419 Hellfire Maverick — open to your recommendation given
                       crowning/timing process.
  8. Chassis:          Open to your preference — Cadex CDX-40, McMillan A5
                       SuperMag, ARC ELR, or MPA BA Comp Heavy all acceptable.
                       Pick what you have the best bedding workflow for. I'll
                       defer this to you.
  9. Optic / mount:    I'll supply — Kahles K540i DLR 5-40×56 (36mm tube, SKMR4+
                       reticle) on a Spuhr SP-6602 (60 MOA) plus a TACOM HQ Charlie
                       TARAC Mk8 variable. No need to source these.
 10. Finish:           Cerakote, color to discuss. Cerakote brake to match.

Please quote:
  - Total turnkey price (action, barrel, chassis, trigger, brake, fitting,
    chambering, bedding, threading, finish, test-fire). Excluding owner-supplied
    optic + mount + TARAC + suppressor.
  - Lead time from deposit to test-fire.
  - Accuracy guarantee (target group size, distance, rounds).
  - Test-fire scope (rounds fired, ammo source, target medium, data provided).
  - Willingness to chamber off my Victrix Cerrosafe cast — yes/no, and any
    process notes.
  - Any component substitutions you'd recommend and why.
  - Deposit terms and progress-billing schedule.

Happy to send the Victrix chamber cast as soon as I make it. Looking forward to
hearing from you.

Thanks,
[name]
[phone]
[email]
```

**After you have three quotes back:**

Score on a simple matrix — total price, lead time, willingness to chamber off your cast, accuracy guarantee, who pushed back on which components. Vestal's is the recommended pick going in, but be honest if a competing quote is meaningfully better. The right answer is the shop whose builder ships rifles that hit at 2 miles, not the cheapest or fastest.

---

## 13. Support gear (not in §3, but you need it for 2 miles)

The rifle itself is half the system. For 2-mile-capable shooting, the rangefinder, weather meter, chronograph, and spotting setup matter as much as the optic. None of this is in §3 because it's not rifle parts — it's the shooter's kit.

### 13.1 Rangefinder

LRF accuracy at 2 miles is non-negotiable. A 1% range error at 3,520 yd is ~35 yd of mismatch, which is several mils of mis-dial. Get something that ranges hard targets confidently past 3,500 yd.

- **Primary: Vectronix Terrapin-X** — Swiss military-grade, hand-held, ~3,000 yd on reflective targets. ~$3,000. Standard for KO2M-class. ([safran-vectronix.com](https://www.safran-vectronix.com/))
- **Alternate 1: Sig Sauer Kilo 10K-ABS HD** — bundled with Applied Ballistics solver. ~$2,200.
- **Alternate 2: Leica Geovid Pro 32** — binoculars + LRF combo, 4,000+ yd reflective. ~$3,500.
- **Avoid for ELR:** anything ranging only to ~1,500 yd. Backup-only.

### 13.2 Weather meter

Atmospherics drive dope at long range — a 10 °F temp change shifts POI ~0.5 mil at 1,500 yd. Without live atmospherics, you're guessing.

- **Primary: Kestrel 5700 Elite with Applied Ballistics** — wind, temp, RH, station pressure, density altitude; integrated AB solver pushes corrections directly to your dope. ~$700. ([kestrelinstruments.com](https://kestrelinstruments.com/))
- **Alternate: Kestrel 5700 Ballistics** (without AB) — pair with Hornady 4DOF or another solver.

### 13.3 Chronograph (mandatory for new-barrel velocity)

You need to chrono the new rifle on the first range trip. Without an actual MV, the solver is guessing.

- **Primary: Garmin Xero C1 Pro** — radar-based, no shoot-through, no muzzle blast issues. ~$600. Has displaced LabRadar as the new standard.
- **Alternate: LabRadar** — older but excellent. ~$560.
- **Avoid:** optical chronographs at this caliber — muzzle blast destroys them, and accuracy suffers near a brake.

### 13.4 Spotting scope + tripod

Self-spotting trace at 2,000+ yd requires good glass.

- **Vortex Razor HD 27-60×85** — best price-per-glass. ~$1,800.
- **Swarovski STX 25-60×85** — alpha tier. ~$3,500.
- **Tripod:** **RRS TVC-34** or **Two Vets No.2** carbon — ELR shooters' standard. The 35-lb rifle isn't on the tripod; the spotting scope is. But the tripod gets hammered by wind anyway.

### 13.5 Bench / mat / rear bag (already partially in §3.10)

- **MidwayUSA Pro Series shooting mat** or **Crosstac Tactical mat** — must support a 35+ lb rifle.
- **Edgewood "minigater" front bag** — bench-grade front rest.
- **Protektor Mfg #13 rear bag** — owl-ear, repeatable.

### 13.6 Support gear budget add-on

| Item | Est. cost |
|---|---|
| Vectronix Terrapin-X LRF | $3,000 |
| Kestrel 5700 Elite (AB) | $700 |
| Garmin Xero C1 Pro chrono | $600 |
| Vortex Razor HD spotting scope | $1,800 |
| RRS tripod | $1,200 |
| Edgewood front bag + Protektor rear | $400 |
| **Support gear subtotal** | **~$7,700** |

**Updated full-system budget:** ~$19k rifle + glass + bipod (§6) + ~$7.7k support gear + ~$1.8k suppressor (optional) = **~$28.5k to fully equipped 2-mile-capable shooter** (if all-new; less if any support gear carries over from the Victrix kit).

---

## 14. Reloading bench notes for .375 CheyTac

You already reload, so most of this is verification — but .375 CT may stress a bench set up for standard magnums.

### 14.1 Press

Standard short-action/long-action presses (RCBS Rock Chucker, Forster Co-Ax) *can* resize .375 CT but flex meaningfully. Recommended upgrades:

- **Forster Co-Ax** — works for .375 CT, at its capacity limit.
- **Mighty Armory Big Boy** — purpose-built for .375 CT / .408 CT / .50 BMG. ([mightyarmory.com](https://www.mightyarmory.com/))
- **Whidden 18" press** — long-stroke, big-magnum-oriented.

### 14.2 Decapping

Standard decapping pins flex on .375 CT primer pockets (large rifle magnum). Solution: **Mighty Armory Big Boy Magnum Decapping Die**.

### 14.3 Annealing

.375 CT brass is $4–6/round; annealing every 2–3 firings extends case life from ~5 firings to ~15+. Effectively required at this cost-per-shot.

- **AMP Mark II with .375 CT pilot** — industry standard, induction-based, repeatable. ~$1,400. ([ampannealing.com](https://www.ampannealing.com/))
- **Annealeez** — budget option, ~$300, less repeatable.

### 14.4 Powder dispensing

Charges are large (130–150 gr). Standard dispensers (RCBS ChargeMaster) handle this but slowly. For volume:

- **AutoTrickler V4** — precision-loader's standard.

### 14.5 Case prep

- **Giraud Tri-Way trimmer with .375 CT cutter** — trim every firing; big mags stretch.
- **K&M chamfer/deburr tool** — neck prep matters for these cases.

### 14.6 Components

Confirm what's on the bench:
- **Brass:** Peterson .375 CheyTac (confirm large or small primer pocket — Peterson makes both) or ADG.
- **Dies:** Warner Tool, Whidden, or Shoot-Long. Shoot-Long is purpose-cut for .375 CT.
- **Powders:** Retumbo, RL-33, RL-50, US869, H50BMG.
- **Primers:** CCI 250 Magnum or Federal 215M.

---

## 15. Ballistic solver + dope workflow

For .375 CheyTac at 2 miles, the difference between a good and bad solver is 1–2 mils at the target — meaning a hit vs. a 6-foot miss.

### 15.1 Recommended solver stack

- **Applied Ballistics Mobile** (paired with Kestrel 5700 Elite AB) — Custom Drag Model (CDM) library has bullet-specific drag curves measured on AB's range. **Primary recommendation for this build.**
- **Hornady 4DOF** — bullet-specific drag curves; free; well-supported. Great second-opinion solver.
- **GeoBallistics BallisticARC** — clean UI, less ELR-specific.
- **Strelok Pro** — fine for under 1,500 yd; not recommended past that.

### 15.2 Workflow once the rifle is built

1. **Chronograph in the new barrel** — 20 shots, log average MV. Plug into solver.
2. **Truing range** — shoot 600 → 1,500 yd in 200-yd increments. Compare predicted vs. actual drop. Adjust MV or G7 BC by ~1% increments until predicted matches actual.
3. **Stretch to 2,000 yd.** Re-true if drift > 0.2 mil.
4. **Verify transonic.** Plot velocity vs range; confirm bullet stays asleep (no yaw flyers).
5. **Beyond 2,000 yd** — your solver's drag curve dominates over BC. Use CDM or 4DOF only.

### 15.3 What to log every range session

Track in a notebook or Cold Bore app: date, location, MV (if chrono'd), atmospherics (temp, pressure, RH, density altitude), wind speed/direction, range, dial, hold, impact result. After ~3 sessions you'll know your gun.

---

## 16. Cerrosafe chamber-cast procedure

Cerrosafe is a low-melting-point alloy (~158 °F melt, ~190 °F pour) that you pour into a clean chamber, cool 30 seconds, and tap out as a perfect cast. Captures freebore, throat angle, neck dimensions — everything the new smith needs to match the Victrix.

### 16.1 Materials (~$50 total)

- 1 lb bar Cerrosafe — [Brownells](https://www.brownells.com/) or Roto Metals
- Cleaning rod + patches
- Q-tips
- Old pot for melting (not food cookware)
- Heat source — hot plate or propane torch
- Wooden dowel for tap-out

### 16.2 Procedure

1. **Clean the chamber thoroughly.** Solvent + brush + dry patches until patches come out white. Any oil/copper creates voids in the cast.
2. **Plug the bore.** Patch + cleaning rod jammed ~3" forward of the case mouth. Prevents Cerrosafe running down the bore.
3. **Melt Cerrosafe** to 190–200 °F. Below boiling water — easy in a small pot.
4. **Pour slowly into the chamber** from the bolt face end. Fill to the case mouth.
5. **Wait 30 seconds.** Cerrosafe expands slightly as it cools — fills every detail.
6. **Tap out** with the dowel from the muzzle end. Cast slides out as a perfect chamber mirror.
7. **Measure within 1 hour.** Cerrosafe shrinks ~0.002" after 24 hours; the first-hour reading is most accurate.

### 16.3 What to do with the cast

Ship to the chosen smith (Vestal's, etc.) with a note: "Match this freebore + throat geometry for the new .375 CT chamber." A good smith reads the cast directly with a caliper and optical comparator.

### 16.4 Alternative: ask Victrix for the reamer print

Call **Victrix Armaments** directly (Italy, but they have US contacts via B&B Firearms and Solid Solution Designs) and ask for the .375 CT reamer print. Some manufacturers share; others won't. If they share, the smith can order a matching reamer from **PT&G, JGS Precision Tool Service, or Manson Precision Reamers** — about $300 reamer cost, 4–8 wk lead.

---

## 17. Range setup + 2-mile target plan

Where to actually shoot this rifle.

### 17.1 Ranges that support 2 miles

- **NRA Whittington Center** — Raton, NM. Long-range ranges to ~1,700 yd routinely; private events push past 2 miles. Hosts KO2M historically.
- **Spearpoint Ranch** — WY. Private, dedicated ELR.
- **Boomershoot** — ID. Annual ELR event with 1,400-yd targets.
- **K&M Precision Shooting** — TN. ELR-specific.
- **Sacramento Valley Shooting Center** — CA. Has hosted KO2M.

### 17.2 Target sizes for known distances

- 1,000 yd → 24" steel (~1 MOA)
- 1,500 yd → 36" steel
- 2,000 yd → 48" steel
- 3,000 yd → 60" steel
- 3,500 yd (2 mi) → 72" steel (KO2M plate is ~40"×40" — small for the range)

Material: **AR500 minimum**, AR550 if budget allows. .375 CT pock-marks AR400 fast.

### 17.3 Spotting at extreme range

Every shot needs a spotter with a quality scope on a tripod. .375 CT bullets are visible in flight at 2,000+ yd via vapor trail (trace) with the right light. Time-of-flight at 2 miles ≈ 4–5 seconds — long enough to call wind correction mid-flight.

---

## 18. NFA Form 4 timeline (if running suppressor)

Open per §11 #4. If yes:

1. File Form 4 with the dealer when the suppressor is purchased.
2. Submit fingerprints, photos, $200 NFA tax stamp.
3. **eFile wait as of 2026:** ~30–90 days (down from 6–12 mo prior).
4. Pick up from dealer once approved.

**Key timing trick:** order the suppressor *first*, in parallel with the rifle build. The 30–90 day wait is then concurrent with the 9–14 month rifle build — not added.

**Tax stamp:** $200, paid at filing. Non-refundable if denied (rare for clean records).

---

## 19. Realistic 2-mile expectations

Honest baseline so you know what success looks like:

### 19.1 First-round hit %

- Solid Victrix-class rifle + Kestrel + Vectronix + experienced shooter: **20–40%** at 2 miles.
- Same setup, less experienced: 5–15%.
- KO2M champion-class shooter: 50%+.

A first-round hit at 2 miles is a real accomplishment regardless of equipment.

### 19.2 Expected group sizes by range

| Range | Group (this build, good conditions) |
|---|---|
| 1,000 yd | 0.5–0.75 MOA (5–7.5") |
| 1,500 yd | 0.75–1.0 MOA |
| 2,000 yd | 1.0–1.5 MOA |
| 3,500 yd (2 mi) | 1.5–3.0 MOA (~52–100" groups) |

A 72" KO2M plate is gettable; a 36" plate at 2 miles is luck.

### 19.3 Wind dominates past 1,500 yd

A 5 mph wind read error at 2 miles displaces the bullet **~8–12 feet**. Your wind call is more important than your dope, your rifle, or your optic past 1,500 yd. Practice wind reading more than anything else.

### 19.4 Barrel life

**~800–1,200 rounds** before accuracy degrades meaningfully. Plan for a re-barrel at ~1,000 rounds. The action and chassis last forever.

### 19.5 Cost-per-shot

- Brass amortized over 15 firings: ~$0.40
- Bullet (CE 350gr Lazer LRT-SF): ~$2.50–$3.50
- Powder (~140 gr/charge × $50/lb): ~$1.50
- Primer: ~$0.15
- **Total: ~$4.50–$5.50/round loaded**

Range trips of 30 rounds: ~$135–165 in components alone, not counting travel.

---

## 20. Glossary + quick-reference conversions

### 20.1 Terms used in this doc

| Term | Meaning |
|---|---|
| ELR | Extreme Long Range — typically 1,500–3,500+ yd |
| KO2M | King of 2 Miles — premier US ELR competition |
| BC | Ballistic Coefficient — drag efficiency. G1 = older model, G7 = better for boattail VLDs |
| SG | Gyroscopic Stability Factor. >1.5 adequate, >2.0 sweet spot |
| MV | Muzzle Velocity (fps) |
| MOA | Minute of Angle. ~1.047" at 100 yd |
| Mil | Milliradian. 3.6" at 100 yd. 3.4377 MOA per mil |
| FFP | First Focal Plane (reticle scales with magnification) |
| COAL / OAL | Cartridge / Overall Length |
| Freebore | Chamber length forward of case mouth where bullet sits before lands |
| Throat | Transition from chamber to rifling lands |
| Truing | Validating predicted vs. actual bullet drop at known ranges |
| Transonic | ~1.0–1.2 Mach (~1,125 fps at sea level) — bullets destabilize crossing this |
| Form 4 | NFA registration form for transferring a suppressor to an individual |
| Cerrosafe | Low-melt alloy used to take a chamber cast |
| RFQ | Request for Quote |

### 20.2 Conversion shortcuts

| From | To | Multiply by |
|---|---|---|
| Mils | MOA | 3.4377 |
| MOA | Mils | 0.2909 |
| Inches @ 100 yd | Mils | 0.2778 |

### 20.3 .375 CheyTac at a glance

- Bullet diameter: .375" (9.5 mm)
- Parent case: .408 CheyTac, necked down
- Case capacity: ~152 gr H₂O
- Typical MV (350gr from 30"): 2,900–2,950 fps
- Typical MV (350gr from 36"): 3,050–3,100 fps
- Bore: standard SAAMI .375
- Brass life with annealing: ~15 firings
- Barrel life: ~800–1,200 rounds

---

## 21. Future-Claude session brief (cold-start for a new session)

If you (Claude) are reading this in a fresh session, this section is your fast onboard.

### 21.1 Owner profile

- Already a .375 CheyTac shooter — owns a **Victrix Armaments Tormento** (.375 CT, 30" barrel, 1:10 twist, button-rifled 416R).
- Reloads ammo. Current load: **Cutting Edge .375 350gr Lazer LRT-SF** (G1 0.807 / G7 0.414, OAL 2.078", projection 1.479").
- Has brass + dies + load data working.
- Wants a *sibling* rifle (not a replacement) for Heavy ELR / KO2M-class shooting.

### 21.2 Build summary (all locked decisions — see §1 + §11 "Resolved")

| Subsystem | Locked choice |
|---|---|
| Cartridge | .375 CheyTac classic, single-shot |
| Action | BAT EX (or EXS), .375 CT bolt face, 40 MOA rail |
| Barrel | Bartlein gain twist 10→9, 36" cut-rifled, MTU contour |
| Trigger | Bix'n Andy TacSport Pro (primary) or TriggerTech Diamond Pro |
| Brake | APA Fat Bastard Gen 3 |
| Optic | Kahles K540i DLR 5-40×56, SKMR4+ reticle |
| Mount | Spuhr SP-6602 (36mm, 60 MOA) on 40 MOA action rail |
| Extra elevation | Charlie TARAC Mk8 variable (0-250 mils) — mandatory |
| Bipod | LRA Light Tactical |
| Chassis | Defer to builder — Cadex CDX-40 / McMillan A5 / ARC ELR / MPA Comp Heavy all OK |
| Builder | **Vestal's Custom Rifles** (primary) — APR + GPG as quote competitors |

### 21.3 Critical context you can't derive from the parts list

- **2024 KO2M winners shot a Victrix Crown in .375 CT** — owner's hardware family is KO2M-proven.
- **"Matched-sibling" goal is about safe ammo interchange + load recipe portability, NOT identical dope cards.** Dope is re-trued per rifle.
- **Chamber compatibility with the Victrix is the load-bearing constraint** — Cerrosafe cast required (procedure §16). Without it, the same loaded round may jam the bullet into the lands.
- **The user said the file lives at `/Users/joshsiegel/repos/nearfield/cheytac.md`** — but this is the nearfield (Sierra/Feral websites) repo. The file is a personal scratch doc, not project code. See §11 #8.

### 21.4 Where the project is right now (as of last edit)

- Doc is v1.4; design phase complete.
- Owner has not yet sent RFQ emails (template in §12).
- Cerrosafe cast not yet made (procedure §16).
- No components ordered yet.
- No quotes received.

### 21.5 Next concrete steps (in order)

1. Make Cerrosafe chamber cast of Victrix (§16).
2. Send §12 RFQ to Vestal's + APR + GPG simultaneously.
3. Order Kahles K540i DLR + Spuhr SP-6602 + Charlie TARAC Mk8 variable in parallel (long lead from EuroOptic / Area 419).
4. Decide suppressor yes/no (§11 #4) — if yes, file Form 4 in parallel (§18).
5. Order Vectronix Terrapin-X LRF + Kestrel 5700 Elite + Garmin Xero C1 Pro in parallel — these are shooter kit, not rifle kit.
6. Order LRA bipod, Edgewood/Protektor bags last (short lead).

### 21.6 Open questions still needing owner input (see §11)

- Chassis preference (or defer to Vestal's)
- Suppressor yes/no
- Brass/dies inventory verification
- Where the rifle lives (bench vs travel — affects EX vs EXS action sizing)
- Doc location preference

### 21.7 Useful one-line prompts to restart this work

- "Pick up the .375 CheyTac build from `cheytac.md`. Status check what's left."
- "Got quotes back from [shop A], [shop B], [shop C]: [paste]. Help me compare."
- "Made the Cerrosafe cast. Measurements: freebore = X.XXX, throat angle = X°, neck = X.XXX. What do they tell us?"
- "Walk me through the Kahles + Spuhr + TARAC ordering."
- "Compare what I'd give up by going Victrix Crown vs. finishing the Vestal's custom build."

### 21.8 What this doc deliberately does NOT cover

- Hunting use cases — out of scope (§8).
- .408 CheyTac builds — considered and rejected (§1).
- .375 EnABELR — considered and rejected (§1).
- Repeater actions — considered and rejected (§3.1).
- Light ELR / weight-capped builds — different rifle entirely.
- Sierra firearms-training-platform code in `app/sites/sierra/` — this doc is a personal scratch artifact and has zero relationship to the nearfield codebase.
