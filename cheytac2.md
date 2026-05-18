# .375-class Heavy ELR Build Guide — No Legacy Constraints

> **Status:** v2 build-guide draft, 2026-05-18. This is the no-compromise rebuild of `cheytac.md` with **zero Victrix-compatibility constraints**. It is written to support RFQs and component ordering for a single-shot, no-weight-cap, KO2M-class rifle. Decision gates are in §11.
>
> **Companion doc:** `cheytac.md` is the v1 build that constrains projectile, twist, and chamber to keep loaded-ammo compatibility with the existing Victrix Tormento. Read that one if dual-rifle portability matters. Read this one if it doesn't.

---

## 0. How to use this guide

This is a build guide, not load data. Use it to brief builders, compare quotes, and prevent expensive ordering mistakes. Do not treat any velocity, pressure, twist/stability, or barrel-life estimate as a substitute for the builder's chamber print, current component data, and a safe load workup.

**Before ordering the action or barrel, get these in writing:**

| Gate | Required answer |
|---|---|
| Cartridge | .375 EnABELR or .375 CT, with exact bolt-face requirement confirmed by the builder/action maker. |
| Bullet | Exact bullet model and weight that controls throat/freebore. |
| Brass | Confirmed source, current availability, expected lot quantity, and compatible shellholder/dies. |
| Reamer | Actual reamer print or print family; do not rely on generic cartridge names. |
| Elevation | Solver estimate for 2 miles using the chosen bullet, plausible MV, atmospherics, rail/mount cant, and TARAC configuration. |
| Builder | Written quote covering parts, labor, test-fire scope, accuracy expectation, and substitutions. |
| Legal/NFA | Suppressor legality, transfer route, current ATF processing time, and match/range suppressor rules. |

**Non-negotiables:** single-shot action, heavy steel barrel, .375 400gr-class bullet path, premium mount, optical elevation assist for 2 miles unless final solver data proves otherwise, and a builder with documented .375-class experience.

---

## 1. Scope

Build a dedicated **Heavy ELR** rifle: single-shot, no weight cap, optimized for **maximum hit probability at 2 miles** from bench/prone. No portability, no shared-load, no dual-rifle constraints. Every decision is "what's best for this rifle on this target," nothing else.

**Working spec (re-justified without Victrix constraints):**

| Decision | Choice | Reason |
|---|---|---|
| **Cartridge** | **.375 EnABELR** (primary) / .375 CheyTac (strong alternate) | EnABELR is a modern Applied Ballistics-origin Heavy ELR cartridge designed around efficient use of very high-BC .375 solids in a shorter package than .375 CT. Component ecosystem is narrower than .375 CT but usable. .375 CT is the close second if component breadth and proven match history matter more than the EnABELR efficiency path. |
| **Bullet** | **Warner Tool 400gr Flatline** (primary) / Berger 407gr ELR Solid (alt) / CE 400gr MTH-class (alt) | Very high G7 BC in this caliber class — Warner Flatline publishes **G7 0.552**, Berger 407gr publishes **G7 0.523**, Hornady 390gr A-Tip **G7 0.497**. Wind drift at 2 miles is the dominant error term; max BC is the single biggest hit-probability lever. |
| **Twist** | **Gain twist 8→7** (or straight 1:7.5) | Stabilizes 400gr Flatline at altitude with SG ~1.8–2.0. Gain twist reduces engraving stress at the chamber end. |
| **Barrel length** | **38"** (40" considered) | Sweet spot for 400gr velocity vs harmonics in a 1.450"/MTU heavy contour. 40" adds ~50 fps but starts losing stiffness; only worth it on a known 2-mile range where 50 fps matters. |
| **Feed** | Single-shot | Standard for KO2M-class builds. |
| **Action class** | BAT EX | Largest practical custom action; handles both .375 EnABELR and .375 CT bolt-head families. |
| **Build path** | Turnkey custom build | Most predictable for both cartridges. |
| **Budget tier** | $20k+ — best-of-everything | Drives every choice below. |

Treat the cartridge, bullet, bolt face, and reamer as a single package. Changing one late can force changes to all of the others.

**Explicitly out of scope for v2:** Repeater builds. Light ELR / NRL ELR weight-capped rifles. Hunting rifles. Dual-rifle ammo portability. Inventory carryover from the Victrix (assume nothing carries; spec the rifle for itself).

---

## 2. Cartridge selection — .375 EnABELR vs .375 CheyTac

The two viable no-compromise picks. Decide between them before ordering anything else; almost every other decision flows from this.

### 2.1 .375 EnABELR (recommended primary)

The **EnABELR** ("Engineered by Applied Ballistics for Extreme Long Range") family was developed by Applied Ballistics Weapons Division, with Bryan Litz describing the design and Peterson Cartridge assisting with case/tooling development for production brass (released 2019). Same .375 bore as .375 CT, but a shorter, wider case engineered to keep .375 CT-class capacity while fitting a shorter overall package that mag-feeds in CheyTac-class actions where loaded .375 CT will not. ([Applied Ballistics — .375 / .338 EnABELR](https://appliedballisticsllc.com/the-375-338-enabelr-cartridges/) · [Peterson Cartridge — EnABELR background](https://www.petersoncartridge.com/technical-articles/posts/2019/july/the-next-big-thing-in-extreme-long-range-shooting-enabelrs/) · [Peterson — .375 EnABELR drawing](https://petersoncartridge.com/drawings-and-prints))

**Performance target (400gr-class .375 solid, 38" barrel):**
- MV: ~3,000–3,250 fps depending on chamber, barrel, pressure, bullet, and powder
- G7 BC: published values run roughly **0.50–0.55** for the best 400gr-class solids — Warner Flatline 400gr at **0.552**, Berger 407gr ELR Solid at **0.523**, Hornady 390gr A-Tip at **0.497**. Verify against current manufacturer data and AB CDM at order time.
- Drop to 2 miles vs .375 CT/350gr: expected to be meaningfully lower; run the exact bullet/MV in Applied Ballistics or 4DOF before treating any mil value as real
- Wind drift in 5 mph at 2 miles: expected to be materially lower than a 350gr .375 CT load if the selected bullet/MV combination carries a higher BC
- Time of flight at 2 miles: expected to be shorter than a slower/lower-BC .375 CT load; verify with the final drag model

**Component ecosystem:**
- **Brass:** Peterson was the production-brass partner for the EnABELR launch and remains the best-documented factory brass source. Resellers that have stocked .375 EnABELR include **Mile High Shooting, Solid Solution Designs, Science of Accuracy, and Cadex** — verify current stock at order time, all of them sell intermittently. Availability is narrower than .375 CT; confirm current stock, lot quantity, and reseller channel before ordering the action/barrel.
- **Dies:** Warner Tool, Whidden, Shoot-Long, and other custom die makers cut EnABELR; confirm current availability and lead time before committing.
- **Bullets:** **Warner Tool Flatline 400gr (G7 0.552)**, **Berger 407gr ELR Match Solid (G7 0.523)**, **Hornady 390gr A-Tip (G7 0.497)**, and Cutting Edge .375 400gr-class bullets are all plausible. Final throat/freebore should be cut around the chosen bullet.
- **Reamers:** PT&G, JGS, Manson all cut EnABELR reamers. ~$300, 4–8 wk.

**Trade-offs:**
- Newer cartridge, narrower vendor base. Confirm brass, dies, and reamer before money leaves the account.
- Cost-per-shot may be similar to or slightly above .375 CT depending on brass and bullet choice.
- Case head/bolt face and reamer details must be confirmed with the builder before action order.
- Smaller used-component market.

**ELR validation:** EnABELR-family cartridges have serious Applied Ballistics / ELR pedigree, but .375 CT has the clearer public KO2M win history. The 2017 KO2M winner was Derek Rodgers with .375 CheyTac; Paul Phillips was part of the winning Applied Ballistics team context and is a major ELR figure. ([PrecisionRifleBlog — KO2M equipment history](https://precisionrifleblog.com/2018/07/05/what-the-pros-use-king-2-miles-edition/) · [LongRangeHunting — KO2M 2017](https://www.longrangehunting.com/articles/king-of-2-miles-2017.1149/))

### 2.2 .375 CheyTac classic (strong alternate)

The classic CheyTac-family ELR cartridge: .408 CheyTac necked to .375. It has the clearer public KO2M track record, including the 2024 winners with a Victrix Crown in .375 CT, and many top finishes. ([Peterson Cartridge — .375 CheyTac](https://petersoncartridge.com/peterson-cartridge-makes-cheytac-caliber-casings) · [AccurateShooter — Heavy Artillery: .375 CheyTac for 2 Miles](https://www.accurateshooter.com/guns-of-week/heavy-artillery-375-cheytac-for-2-miles/))

**Performance (400gr CE MTH-MAX, 38" barrel):**
- MV: ~3,100–3,150 fps
- G7 BC: not currently published on CE's product page for the 400gr MTH; Berger 407gr Solid (G7 0.523) and Hornady 390gr A-Tip (G7 0.497) are the better-documented .375 CT options with published BCs.
- Drop to 2 miles: baseline (this is the reference)
- Wind drift at 2 miles: baseline

**Component ecosystem (broader than EnABELR):**
- **Brass:** Peterson, ADG, Bertram, and other CheyTac-specialty suppliers offer .375 CT brass. Pricing varies by maker and availability.
- **Dies:** Warner Tool, Whidden, Shoot-Long, Redding all stock.
- **Bullets:** Cutting Edge (350gr Lazer LRT-SF, 375gr MTH-MAX, 400gr Lazer/MTH-class options), Warner Flatline, Hornady A-Tip 390gr, Berger 407gr solid.
- **Reamers:** Not SAAMI. Use CIP/Peterson/PT&G/JGS/Manson print language and confirm the actual reamer print with the smith.

**KO2M validation:** 2024 winners and many historical top-10 finishers. It is one of the best-proven Heavy ELR cartridges.

**Trade-offs:**
- May give up some ballistic efficiency depending on the exact EnABELR and .375 CT loads being compared.
- Common CE .375 CT bullet choices often run slightly lower G7 BC than the highest-BC 400gr-class solids.
- Same bore and broadly similar rifle class; recoil, barrel life, and pressure behavior depend on the specific load and chamber.

### 2.3 Decision rubric

| If you value… | Pick |
|---|---|
| Maximum hit probability at 2 miles, willing to live with a narrower EnABELR supply chain | **.375 EnABELR** |
| Broader brass/bullet/die sourcing, willing to give up some ballistic efficiency | **.375 CheyTac** |
| Already have meaningful .375 CT inventory (Peterson brass, dies, load data) | **.375 CheyTac** — the inventory is real money even if the Victrix itself is irrelevant |

**Recommendation:** **.375 EnABELR.** This doc is "no compromise" by definition, and the EnABELR concept is compelling if the builder can source brass/dies/reamer and cut the rifle around the selected high-BC solid. The rest of §3 below assumes EnABELR. Where .375 CT changes the answer, it's flagged.

---

## 3. Parts list — subsystem by subsystem

### 3.0 Orderable baseline spec

Use this as the default quote spec. Builders can push back, but substitutions should be intentional and written down.

| Subsystem | Baseline | Builder must confirm |
|---|---|---|
| Cartridge | .375 EnABELR primary / .375 CT alternate | Exact chamber print, brass source, bolt face. |
| Bullet | 400gr-class .375 ELR solid | Final bullet model controls throat/freebore and twist. |
| Action | BAT EX single-shot, RB/RE, 40 MOA rail | Bolt face, firing pin, rail, inlet compatibility. |
| Barrel | Bartlein/Brux/Krieger steel, gain 8->7 or straight 1:7.5, 38" target | Contour, shank, finished length, expected MV window. |
| Chassis/stock | ARC ELR / MPA Heavy / Cadex / McMillan | Inlet, bedding, rail space for TARAC, final balance. |
| Trigger | Bix'n Andy TacSport Pro / TriggerTech Diamond Pro | Action compatibility and safe pull-weight range. |
| Brake | Terminator T5 / Area 419 Hellfire (verify .375 availability) / builder's preferred .375-class brake | Thread pitch, timing, blast management. APA Fat Bastard Gen 3 is **not currently catalog in .375** — don't assume it. |
| Optic | Kahles K540i DLR, SKMR4+ | Ring height, zero range, elevation reserve. |
| Mount/elevation | Spuhr SP-6602 + Charlie TARAC variable | Actual TARAC model/range and rail fit. |

---

### 3.1 Action — BAT EX, single-shot

The BAT Machine **EX** is the standard for Heavy ELR. The smaller **EXS** is for weight-capped builds; for no-cap, run the full EX for max rigidity and thermal mass.

- **Primary:** BAT Machine **EX** single-shot, .750" firing pin, integral 40 MOA rail, **EnABELR bolt face** (or .375 CT, see §2). ([batmachine.com — action lineup](https://www.batmachine.com/bat-actions/) · [Bullet Central — BAT inventory](https://bulletcentral.com/actions/))
- **Alternate 1:** Stiller **TAC 408** single-feed — proven, slightly cheaper, broader chassis inlets.
- **Alternate 2:** Defiance **Deviant XM** — Defiance's reputation matches BAT.
- **Spec to order:** right-bolt right-eject, cartridge-specific bolt face, integral 40 MOA rail, fluted bolt, large knob.

**Source:** BAT direct (6–12 mo lead) or Bullet Central if they have stock. Order **day 1 only after** the builder confirms cartridge, bolt face, and chassis/stock inlet.

---

### 3.2 Barrel — Bartlein gain twist 8→7, 38"

**Working twist: gain twist 8→7.** The Warner 400gr Flatline needs SG ≥ 1.5 at the transonic boundary; 1:7 gain delivers SG ~2.0 at sea level and ~1.8 at altitude. Straight 1:7.5 is the simpler alternate with ~95% of the same performance. 1:8 gain is the floor — works at sea level, marginal at altitude.

**Length: 38".** Two more inches than the v1 36" may buy modest velocity with slow powders, while staying more manageable than a 40" tube. 38" is a defensible Heavy ELR target length for an MTU/1.450" contour, but defer the final length to the builder's stiffness/balance experience.

- **Primary:** **Bartlein** 5R cut-rifled, **gain twist 8→7**, 1.450" → 0.95" MTU contour finished at **38"**, threaded to brake spec. ([bartleinbarrels.com](https://bartleinbarrels.com/))
- **Alternate 1:** **Bartlein straight 1:7.5**, same contour. Simpler.
- **Alternate 2:** **Brux** cut-rifled, 1:7 gain, same contour. Often shorter lead. ([bruxbarrels.com](https://bruxbarrels.com/))
- **Alternate 3:** **Krieger** 5R, 1:7. Historically the ELR gold standard. 12+ mo lead.
- **NOT recommended:** 1:9 or 1:10 — under-stabilizes 400gr at altitude.
- **NOT recommended:** Proof CF — carbon-wrapped is for weight-capped builds. Heavy steel for no-cap.

**Spec to order:** "Chosen .375 400gr-class solid, .375 EnABELR chamber, freebore/throat cut for that bullet and seating length, gain twist 8->7, 38" finished, MTU/1.450-class contour, threaded for [brake]." If going .375 CT: same idea, but specify the exact .375 CT/CIP/Peterson reamer print and the chosen CE/Berger/Hornady/Warner bullet.

**Builder questions:** What reamer print will you use? What freebore for the chosen bullet? What finished length do you recommend for stiffness and balance? What MV range do you expect without running abusive pressure?

**Velocity expectations:**
| Length | MV target (400gr-class / EnABELR) | MV target (400gr-class / .375 CT) |
|---|---|---|
| 34" | ~2,950–3,100 fps | ~3,000–3,100 fps |
| 36" | ~3,000–3,175 fps | ~3,050–3,125 fps |
| **38" (rec.)** | **~3,050–3,250 fps** | **~3,075–3,150 fps** |
| 40" | ~3,100–3,275 fps | ~3,100–3,180 fps |

---

### 3.3 Chassis — ARC ELR or MPA BA Comp Heavy

- **Primary:** **ARC ELR Chassis** with BAT EX inlet. Modular, adjustable cheek/LOP/buttplate, integrated arca/M-LOK. ([accuracysolutionsinc.com](https://www.accuracysolutionsinc.com/))
- **Alternate 1:** **MPA BA Competition Heavy** with BAT EX inlet. ([masterpiecearms.com](https://masterpiecearms.com/))
- **Alternate 2:** **Cadex CDX-40 Shadow** chassis. ([cadexdefence.com](https://www.cadexdefence.com/))
- **Alternate 3:** **McMillan A5 SuperMag** — bedded stock, old-school, beautifully made.

**Decision factor:** defer to the builder's preference; their bedding jigs matter.

---

### 3.4 Trigger — Bix'n Andy TacSport Pro or TriggerTech Diamond Pro

- **Primary:** **Bix'n Andy TacSport Pro** two-stage, BAT-compatible. ([bixnandy.com](https://bixnandy.com/))
- **Alternate 1:** **TriggerTech Diamond Pro** single-stage. ([triggertech.com](https://triggertech.com/))
- **Alternate 2:** **Jewell HVR**.

**Pull weight:** 8–12 oz typical for ELR. Owner preference (single vs two-stage) decides.

---

### 3.5 Muzzle brake — Terminator T5 (or builder's .375-class brake)

Recoil from a 400gr-class .375 ELR load is substantial even in a heavy rifle. A high-efficiency brake is mandatory for spotting impacts and preserving position.

- **Primary:** **Terminator T5**. Standard on many .375 CT / EnABELR-class builds; what the Sniper's Hide kit gun runs and what several Bartlein-recommended builds use.
- **Alternate 1:** **Area 419 Hellfire** — verify current .375-caliber availability and thread options. ([area419.com](https://www.area419.com/))
- **Alternate 2:** **MPA** muzzle brake (verify .375 availability with builder).
- **NOTE:** APA Fat Bastard Gen 3 is **not currently offered in .375** (APA's Gen 3 catalog is 6mm / 6.5mm / .30 / .338 / .22). If you see it spec'd in older build write-ups, that's either a custom one-off or an outdated reference. ([americanprecisionarms.com — Gen 3 Fat Bastard](https://www.americanprecisionarms.com/products/gen-3-fat-bastard-self-timing-muzzle-brake))

**Spec:** thread to Bartlein-specified shank (typically 1.000"-20 or 1.125"-20 for this contour). Timed brake. Confirm thread pitch with the builder before barrel order.

---

### 3.6 Optic — Kahles K540i DLR, 5–40×56

**Kahles K540i DLR**, 5–40×56, 36mm tube, 29 mils internal, FFP, illuminated, **SKMR4+** reticle. DLR variant for ELR-competition turret feel. ([kahles.at](https://www.kahles.at/) · [Area 419 — K540i DLR product page](https://www.area419.com/product/kahles-k540i/) · [Precision Rifle Australia — K540i review](https://precision-rifle.com.au/2025/01/17/kahles-k540i/) · [PrecisionRifleBlog — Wyoming ELR Scopes & Mounts](https://precisionrifleblog.com/2020/09/05/best-elr-scope-and-scope-mount-and-rings/))

Same choice as v1 — no Victrix dependency. The Kahles is alpha-class glass with the best ELR-competition turret on the market.

- **Approximate price:** $4,500.
- **Sources:** [EuroOptic](https://www.eurooptic.com/), [Area 419](https://www.area419.com/), [LRI / Liberty Optics](https://www.libertyoptics.com/), [B&H Photo](https://www.bhphotovideo.com/).

**Elevation planning for 2-mile capability:**

| Item | Published / nominal value |
|---|---|
| K540i total internal elevation travel | 29 mils |
| Action rail (40 MOA) | 11.6 mils cant |
| Spuhr SP-6602 (~20.6 MOA / 6 MIL) | 6 |
| Total base cant | ~17.6 mils |

Do **not** treat total internal travel plus base cant as guaranteed usable dial-up. The usable elevation after zero depends on where the rifle actually zeroes inside the scope's travel, ring/mount geometry, and how much travel remains above the zero stop. A 400gr-class .375 solid at realistic ELR velocities will need more elevation than this conventional scope/mount stack can reliably provide at 2 miles. **Charlie TARAC remains mandatory** unless final solver and zeroing data prove another elevation solution works — see §3.7.

(The earlier draft cited the SP-6602 at 60 MOA / 17.5 mil; Spuhr's actual published spec for the SP-6602 is **6 MIL / ~20.6 MOA**. The corrected math is reflected above. If you want more base cant without the TARAC, the alternative is a different one-piece mount with higher built-in cant — see §3.7 alternates.)

**Why Kahles K540i over alternatives:**
- Alpha-class glass (Schott HT tier).
- DLR turret designed for ELR-competition dial speed.
- 5–40x range wider than ZCO ZC527 (5–27).
- Lighter than ZCO (~1,110g vs ~1,250g).

**Trade-off vs March Genesis 4–40×52:** Genesis-style ELR scopes can offer much more internal elevation than conventional optics, potentially reducing or eliminating the TARAC requirement depending on the final dope. Kahles glass + turret feel is the preferred trade for this build, but verify current March specs before making the elevation comparison.

---

### 3.7 Scope mount + Charlie TARAC (mandatory)

**Mount:** **Spuhr SP-6602** (36mm rings, **~20.6 MOA / 6 MIL** built-in cant). Stacked on action's 40 MOA rail = **~60.6 MOA total base cant** (~17.6 mils). ([spuhr.biz](https://spuhr.biz/) · [EuroOptic — SP-6602 product page with verified cant spec](https://www.eurooptic.com/Spuhr-Unimount-36mm-6-MIL-206-MOA-15-Picatinny-Scope-Mount-SP-6602.aspx))

**Charlie TARAC: MANDATORY.** Kahles' 29 mils total internal elevation travel plus ~17.6 mils of base cant is not enough to count on for 2 miles after the rifle is actually zeroed. For 2 miles you need the TARAC's optical boost (or a deliberately engineered higher-elevation optic/mount solution — see alternates below).

- **Primary:** **Charlie TARAC variable**. Exact model, adjustment range, and price must be confirmed with TACOM HQ before ordering. ([tacomhq.com/charlie-tarac](https://tacomhq.com/charlie-tarac/))
- **Alternate:** Charlie TARAC fixed prism (~60 mils class). Confirm current model/price with TACOM HQ.
- **Higher-cant mount alternates** (if you'd rather buy more base cant than rely on the TARAC for 2 miles): **ERA-TAC adjustable 36mm** (0–70 MOA variable cant — heavier, but lets you tune without re-buying), or **ARC M-Brace** in 36mm (purpose-built ELR mount). With these you can lift base cant well above the SP-6602's 20.6 MOA.

**Total system elevation:** actual usable dial after zero plus the selected TARAC optical shift. This is more than enough for 2-mile work if the TARAC configuration is chosen correctly and verified in the solver.

---

### 3.8 Bipod — LRA Lite-Tactical

- **Primary:** **LRA Lite-Tactical Bipod** (carbon-leg; LRA's product is named "Lite-Tactical"). ([lraccuracy.com — Lite-Tactical bipod series](https://lraccuracy.com/collections/lite-tactical-bipod-series))
- **Alternate 1:** **Phoenix Precision Bipod**.
- **Alternate 2:** **MDT Ckye-Pod** (overkill for static ELR).
- **Avoid:** Atlas / Harris.

---

### 3.9 Rear support

- **Primary:** **Armageddon Gear Game Changer** filled heavy (steel shot or Lyman media).
- **Alternate:** dedicated rear sandbag (Edgewood, Protektor) for pure bench/prone work.

---

### 3.10 Suppressor (optional, recommended)

A .375 EnABELR or .375 CT with a high-efficiency brake is *brutally* loud. ELR matches generally allow suppressors — verify the specific match rule book before ordering.

- **Primary:** **Thunder Beast Arms Ultra 50** — a serious .50-class TBAC option to ask TBAC and the builder about for .375 CT / EnABELR. Confirm cartridge, barrel length, mount, and pressure limits with TBAC before ordering. ([thunderbeastarms.com](https://thunderbeastarms.com/))
- **Alternate:** Any quality **.50 BMG-rated** suppressor — Liberty Suppressors Sovereign 50, Bowers VERS-50, or comparable. .375 CT / EnABELR sits well inside a .50 BMG-rated envelope; confirm with the maker and your dealer.

**ATF Form 4 wait:** check [ATF's current processing times page](https://www.atf.gov/resource-center/current-processing-times) before buying. 2025–2026 ranges seen: eForm 4 individual ~10–11 days, eForm 4 trust ~11–25 days, paper Form 4 ~57–85 days. File parallel with build.

---

## 4. Builder shortlist (turnkey)

### 4.1 KO2M validation by cartridge

- **.375 EnABELR:** Applied Ballistics / ELR pedigree and credible modern ELR use, but less public KO2M win-history documentation than .375 CT. Treat builder-provided match history as an RFQ question.
- **.375 CheyTac:** 2024 KO2M winners (Polish team, Victrix Crown), most current top-10 placings. ([Ultimate Reloader — 2-mile .375 CT build](https://ultimatereloader.com/2024/06/02/building-a-2-mile-rifle-375-cheytac-build/))

### 4.2 Tier-1 builders

| Builder | Location | Strengths | Best fit for |
|---|---|---|---|
| **Warner Tool Company** | NH | Makes Flatline bullets, dies, and ELR hardware; confirm current rifle-build and EnABELR support directly. ([warnertoolcompany.com](https://www.warnertoolcompany.com/)) | **.375 EnABELR support / bullet ecosystem** |
| **Global Precision Group (GPG)** | Paul Phillips' shop | Paul Phillips is one of the most visible serious ELR names and has Applied Ballistics / KO2M winning-team history. Likely longest lead. | **.375 EnABELR or .375 CT** |
| **Vestal's Custom Rifles** | Bristol, VA | Robert Vestal personally builds. Bartlein-based. ELR-instructor reputation. Highest-touch shop. ([vestalscustomrifles.com](https://vestalscustomrifles.com/) · [Sniper's Hide — Vestal's CDX-40 .375 CT build](https://www.snipershide.com/shooting/threads/sold-elr-ready-vestals-custom-rifles-cadex-cdx-40-shadow-32-1-7-375-cheytac.7021368/)) | **.375 CT** (most experience here) |
| **Alamo Precision Rifles (APR)** | Hurst, TX | Catalog .375 CT, production-grade repeatability, fast turnaround. ([aprifles.com — APR Custom .375 CheyTac](https://aprifles.com/products/apr-custom-375-cheytac)) | **.375 CT** |

### 4.3 Tier-2 builders (excellent, less famous)

| Builder | Location | Notes |
|---|---|---|
| **Lethal Precision Arms (Mitchell Fitzpatrick)** | — | KO2M winner with self-built rifle; sells builds. |
| **K&P Gunsmithing** | TX | Makes APR's barrels. Will build full rifles. |
| **Long Rifles Inc (LRI)** | SD | Ship-them-parts model. Shorter lead. |
| **Dzuro's Guns** | Lake Havasu City, AZ | Custom ELR builds, BAT-experienced. ([dzurosguns.com](https://dzurosguns.com/custom_rifles.php)) |
| **Great Southern Gunworks (Extreme Rifles)** | GA | ELR specialist; 2-mile builds. ([extremerifles.com](https://www.extremerifles.com/tac)) |

### 4.4 NOT recommended

- **Surgeon Rifles** — actions don't chamber to .375 class.
- Any production shop without .375-class portfolio.

### 4.5 RFQ set: Warner Tool, GPG, Vestal's

**If going .375 EnABELR (recommended):** Warner Tool is a logical call because of the Flatline/die/ELR ecosystem, but confirm whether they want to own the full rifle build. GPG is the natural competitor because of Paul Phillips' ELR credentials and Applied Ballistics-adjacent experience. Vestal's quotes both cartridges and provides a price benchmark.

**If going .375 CT:** Vestal's primary, APR + GPG as competitors (same recommendation as `cheytac.md` §4).

Send the §12 RFQ to all three on the same day. Quote comparison rubric:

1. **Lead time** — action order to test-fire (6–14 mo).
2. **Total price delivered** (excluding owner-supplied optic, mount, TARAC, suppressor).
3. **Component substitutions** — what does the shop want to swap? Listen on chassis (their bedding jigs matter) and brake (their crowning matters). Push back on barrel-maker, twist, and bullet unless the builder has a strong reason.
4. **Accuracy guarantee + test-fire scope** — expected group size, rounds fired, distance.

**Disqualifiers:** vague chamber language, no named reamer print, no .375-class references, unwillingness to discuss brass/die supply, no test-fire plan, or a quote that treats the build like an ordinary magnum rebarrel.

---

## 5. Build sequence

Long-lead items determine the schedule. The key is to avoid ordering anything that locks the wrong bolt face, chamber, or inlet.

1. **RFQ phase.** Send §12 to the builder set. Ask for cartridge recommendation, reamer print, brass source, expected MV window, and test-fire plan.
2. **Decision lock.** Choose cartridge, builder, bullet, action, reamer print, barrel length, and chassis/stock.
3. **Action order.** Builder confirms bolt face and inlet first; action ships directly to builder.
4. **Barrel order.** Builder confirms twist, contour, finished length, shank, brake thread, and chamber print.
5. **Optic/elevation order.** Order Kahles K540i DLR, Spuhr SP-6602, and the builder-confirmed TARAC configuration early enough to test rail fit.
6. **Suppressor order, if buying.** File Form 4 early. Current ATF eForm waits are often measured in days/weeks, but filing early keeps it off the critical path.
7. **Chassis/stock order.** Order when builder confirms inlet and bedding plan for the action serial.
8. **Trigger/brake/support gear.** Order once builder confirms compatibility and thread pitch.
9. **Reloading tooling/components.** Buy brass, dies, shellholder, annealing pilot, trimmer insert, and bullets only after the cartridge/chamber path is final.
10. **Acceptance.** Builder test-fires, provides target/data, confirms headspace, and documents the starting load or ammo used for test-fire.

**Total project timeline: 9–14 months** from first order to first round downrange.

**Acceptance package to request from builder:** final chamber/reamer print, barrel maker/lot/twist/length, action serial, torque values, brake thread, tested ammo/load, test target, chrono data if available, recommended break-in/cleaning approach, and any parts that should be re-torqued after initial firing.

---

## 6. Rough budget (no-compromise tier)

| Item | Estimate | Notes |
|---|---|---|
| BAT EX action | $3,000 | EnABELR or .375 CT bolt face. |
| Bartlein gain-twist barrel | $900 | Cut-rifled, 1:7 gain, MTU 38". |
| ARC ELR chassis (or MPA Comp Heavy) | $3,500 | Inletted for BAT EX. |
| Bix'n Andy TacSport Pro trigger | $650 | |
| Terminator T5 brake (or builder's pick) | ~$400 | Plus ~$100 install/timing. (APA Fat Bastard Gen 3 is **not** offered in .375 — don't budget it.) |
| Kahles K540i DLR 5-40×56 (SKMR4+) | $4,500 | |
| Spuhr SP-6602 mount (36mm, 6 MIL cant) | $750 | |
| Charlie TARAC variable | ~$2,000+ | Confirm exact model/range/current price with TACOM HQ. |
| LRA Lite-Tactical bipod | $700 | |
| Armageddon Gear Game Changer | $120 | |
| Builder labor (chamber, fit, test-fire) | $2,500 | Often bundled into action+barrel quote. |
| EnABELR reamer (one-time, builder buys) | $300 | Or included in labor. |
| **Subtotal (rifle + glass + mount + TARAC + bipod)** | **~$19,300** | |
| Brass + dies + bullets — initial 100-rd inventory | ~$1,400–$2,000 | EnABELR: verify current brass/die availability and pricing before budget lock. |
| Thunder Beast Ultra 50 (optional) | $1,800–$2,400 | Confirm current price and current NFA tax treatment with TBAC/dealer/ATF. |
| **Total with suppressor + starting components** | **~$23,000–$24,000** | Wide-band so the quote isn't a surprise. |

Plus shipping, NFA transfer/admin fees, any applicable NFA tax, FFL transfer, sales tax, extra bullets/brass for load development, and builder-specific tooling. Keep a 15–25% contingency; ELR builds punish optimistic budgets.

**Budget rule:** the builder quote is the source of truth. This table is a planning range so the quote does not arrive as a surprise.

---

## 7. Bullet / load

This section defines the bullet path for chambering and solver work. It is not a loading manual. Use manufacturer data, builder guidance, pressure signs, chronograph data, and conservative ladder workups.

### 7.1 Primary: Warner Tool Flatline 400gr (.375 EnABELR)

| Parameter | Value |
|---|---|
| Bullet | Warner Tool Flatline 400gr |
| Caliber | .375 |
| Weight | 400 gr |
| **G1 BC** | **1.103** (Warner-published) |
| **G7 BC** | **0.552** (Warner-published; verify against current lot data and AB CDM) |
| Construction | Solid copper, lathe-turned |
| Source | [warner-tool.com — .375 400gr Flat Line product page](https://www.warner-tool.com/product/375-400gr-flat-line/) · [Applied Ballistics — solver & BC database](https://appliedballisticsllc.com/) |

**Stability check for 1:7 gain twist:**
| Condition | MV (38") | SG | Verdict |
|---|---|---|---|
| Sea level, 59 °F | final MV | ~2.0 target | Sweet spot |
| 6,000 ft, 20 °F | final MV | ~1.85 target | Solid margin |
| 10,000 ft transonic | ~1,200 fps | ~1.7 | Above 1.5 threshold |

**Powder:** Retumbo, RL-50, or H50BMG. Charge weight must come from builder/manufacturer data and safe ladder workup.
**Primer:** CCI 250 Magnum or Federal 215M.
**Brass:** confirm current Peterson and Applied Ballistics Weapons Division (ABWD) reseller-channel .375 EnABELR brass availability before chambering.

**Load-development requirement:** do not load bulk ammo until the finished chamber is known, the builder has confirmed safe starting data, and the first velocity node is proven in this barrel.

### 7.2 Alternate: Berger 407gr ELR Match Solid

| Parameter | Value |
|---|---|
| Bullet | Berger .375 407gr ELR Match Solid (P/N 37407) |
| **G1 BC** | **1.022** (Berger-published) |
| **G7 BC** | **0.523** (Berger-published) |
| Min twist | 1:8 or faster |
| Construction | Solid copper, lathe-turned |
| Source | [bergerbullets.com — .375 Cal 407 Grain ELR Match Solid](https://bergerbullets.com/product/375-caliber-407-grain-elr-match-solid-bullets/) |

Sits between the Warner Flatline (0.552 G7) and the Hornady A-Tip (0.497 G7). Useful as a hedge if Warner Tool supply tightens or if a builder has stronger Berger-load experience.

### 7.3 Alternate: Hornady 390gr A-Tip Match

| Parameter | Value |
|---|---|
| Bullet | Hornady .375 390gr A-Tip Match (#3729) |
| **G1 BC** | **0.987** (Hornady-published) |
| **G7 BC** | **0.497** (Hornady-published) |
| Recommended twist | 1:11 (Hornady) — runs comfortably in 1:7 or 1:8 |
| Construction | Aluminum-tipped match bullet (not a solid) |
| Source | [hornady.com — .375 390gr A-Tip Match](https://www.hornady.com/bullets/rifle/375-cal-.375-390-gr-a-tip-match) |

Mainstream-distribution alternate. Lower BC than the Flatline or Berger Solid, but easiest to source.

### 7.4 Alternate: Cutting Edge 400gr-class (.375 CT path)

| Parameter | Value |
|---|---|
| Bullet | CE .375 400gr MTH single-feed (or 402gr MTAC for pure target use) |
| **G7 BC** | Not currently published on CE's product page; verify with CE before relying on a specific number |
| Construction | Solid copper, lathe-turned |
| Source | [cuttingedgebullets.com — .375 400gr MTH single-feed](https://cuttingedgebullets.com/products/375-400gr-single-feed-mth-match-tactical-hunting) · [CE 400gr Lazer LRT-SF reference](https://cuttingedgebullets.com/products/375-400gr-single-feed-lazer-tipped-hollow-point3) |

Use if going .375 CT and you want CE's specific bullet construction. Confirm published BC at order time — CE bullets work but require asking for current G7 data per bullet.

### 7.5 Headroom

1:7 gain twist also handles:
- Anything heavier in the 400–425gr range if Warner or others release it
- Lighter bullets (350gr-class Lazer LRT-SF) — over-stabilized but functional; leave them for the Victrix

400gr-class is the current top of the practical curve for both cartridges. Heavier custom bullets exist but aren't standard.

---

## 8. What we're NOT building

- A repeater — single-shot is correct for KO2M.
- A weight-capped Light ELR build — different rifle entirely.
- A .408 CheyTac — .375-class is generally the more efficient ELR competition path today unless a builder makes a specific .408 case.
- A .50 BMG — too much recoil for accuracy work.
- A hunting rifle.
- **Anything constrained by an existing rifle's chamber, twist, or load.** That's `cheytac.md`'s scope.

---

## 9. Things that can ruin this build

1. **Picking a builder without .375-class portfolio.** Reamer print, throat tolerance, headspace — these matter and aren't generic-magnum work.
2. **Cheap rings/mount.** A $4,500 scope on $200 rings *will* shift under .375 EnABELR recoil. Spuhr-class or better.
3. **Wrong twist for 400gr.** 1:9 or 1:10 won't stabilize 400gr at altitude. 1:7 or 1:8 gain only.
4. **Skipping the suppressor.** .375 EnABELR with a brake is genuinely dangerous to the shooter and anyone left of the gun.
5. **Cheap rear bag.** Sub-MOA at 2 miles needs repeatable rear support.
6. **Buying the optic last.** Second-longest lead. Day-1 order.
7. **Cartridge indecision after action ordered.** Bolt face is cartridge-family-specific. Lock cartridge before the action goes in.
8. **Buying components before the chamber path is real.** Brass, dies, shellholder, reamer, bullet, and throat are coupled.
9. **Skipping solver validation.** The elevation stack must be checked with the exact bullet, MV, zero, atmospherics, and TARAC setting before the first 2-mile trip.

---

## 10. Sources

**Cartridge & projectile research**
- [Warner Tool Company — Flatline bullets, dies, ELR hardware](https://www.warnertoolcompany.com/)
- [AccurateShooter — .375 EnABELR cartridge background](https://www.accurateshooter.com/cartridges/the-375-enabelr-cartridge/)
- [Peterson Cartridge — .375 EnABELR and CheyTac drawings](https://petersoncartridge.com/drawings-and-prints)
- [AccurateShooter — Heavy Artillery: .375 CheyTac for 2 Miles](https://www.accurateshooter.com/guns-of-week/heavy-artillery-375-cheytac-for-2-miles/)
- [Peterson Cartridge — .375 CheyTac brass](https://petersoncartridge.com/peterson-cartridge-makes-cheytac-caliber-casings)
- [Cutting Edge Bullets — .375 400gr MTH single-feed](https://cuttingedgebullets.com/products/375-400gr-single-feed-mth-match-tactical-hunting)
- [Cutting Edge — 400gr LRT-SF reference spec](https://cuttingedgebullets.com/products/375-400gr-single-feed-lazer-tipped-hollow-point3)
- [Berger Bullets — .375 407gr ELR Match Solid](https://bergerbullets.com/product/375-caliber-407-grain-elr-match-solid-bullets/)
- [Hornady — .375 390gr A-Tip Match (#3729)](https://www.hornady.com/bullets/rifle/375-cal-.375-390-gr-a-tip-match)
- [Warner Tool — .375 400gr Flat Line](https://www.warner-tool.com/product/375-400gr-flat-line/)
- [Applied Ballistics — .375/.338 EnABELR cartridge background](https://appliedballisticsllc.com/the-375-338-enabelr-cartridges/)
- [Applied Ballistics — solver & bullet BC database](https://appliedballisticsllc.com/)
- [Peterson Cartridge — EnABELR background article](https://www.petersoncartridge.com/technical-articles/posts/2019/july/the-next-big-thing-in-extreme-long-range-shooting-enabelrs/)
- [Hornady 4DOF — drag-curve solver](https://www.hornady.com/4dof)

**KO2M validation & ELR competition**
- [King of 2 Miles — official results & history](https://kingof2miles.com/)
- [LongRangeHunting — KO2M 2017 report](https://www.longrangehunting.com/articles/king-of-2-miles-2017.1149/)
- [Ultimate Reloader — 2-mile .375 CheyTac ARC chassis + BAT EX build](https://ultimatereloader.com/2024/06/02/building-a-2-mile-rifle-375-cheytac-build/)
- [Sniper's Hide — Vestal's Cadex CDX-40 .375 CT build](https://www.snipershide.com/shooting/threads/sold-elr-ready-vestals-custom-rifles-cadex-cdx-40-shadow-32-1-7-375-cheytac.7021368/)
- [Sniper's Hide — Best bipod for heavy ELR guns](https://www.snipershide.com/shooting/threads/best-bipod-for-heavy-elr-guns.7073192/)
- [PrecisionRifleBlog — Wyoming ELR Scopes & Mounts (what the pros use)](https://precisionrifleblog.com/2020/09/05/best-elr-scope-and-scope-mount-and-rings/)

**Actions, barrels, chassis, triggers**
- [BAT Machine Co — action lineup](https://www.batmachine.com/bat-actions/)
- [Bullet Central — BAT action inventory](https://bulletcentral.com/actions/)
- [Bartlein Barrels — cut-rifled, gain-twist](https://bartleinbarrels.com/)
- [Brux Barrels](https://bruxbarrels.com/)
- [Accuracy Rifle Systems — ARC ELR chassis](https://www.accuracysolutionsinc.com/)
- [Masterpiece Arms — MPA BA Comp Heavy chassis](https://masterpiecearms.com/)
- [Cadex Defence — CDX-40 Shadow chassis](https://www.cadexdefence.com/)
- [Bix'n Andy — TacSport Pro trigger](https://bixnandy.com/)
- [TriggerTech — Diamond Pro](https://triggertech.com/)

**Brakes, optics, mounts, suppressors**
- [American Precision Arms — Gen 3 Fat Bastard brake (not currently catalog in .375)](https://www.americanprecisionarms.com/products/gen-3-fat-bastard-self-timing-muzzle-brake)
- [Area 419 — Hellfire Maverick & K540i DLR retailer](https://www.area419.com/)
- [Area 419 — Kahles K540i DLR product page](https://www.area419.com/product/kahles-k540i/)
- [Kahles — K540i DLR official](https://www.kahles.at/)
- [Precision Rifle Australia — K540i DLR field review](https://precision-rifle.com.au/2025/01/17/kahles-k540i/)
- [Spuhr — SP-6602 mount](https://spuhr.biz/)
- [TACOM HQ — Charlie TARAC optical periscope](https://tacomhq.com/charlie-tarac/)
- [Thunder Beast Arms — Ultra 50 (.375-class) and Ultra-line suppressors](https://thunderbeastarms.com/)
- [EuroOptic — Kahles retailer](https://www.eurooptic.com/)
- [Liberty Optics (LRI)](https://www.libertyoptics.com/)
- [B&H Photo — Kahles retailer](https://www.bhphotovideo.com/)

**Bipods, support gear**
- [Long Range Accuracy — LRA Lite-Tactical bipod](https://lraccuracy.com/collections/lite-tactical-bipod-series)
- [Kestrel — 5700 Elite w/ Applied Ballistics](https://kestrelinstruments.com/)
- [Safran Vectronix — Terrapin-X LRF](https://www.safran-vectronix.com/)

**Reloading bench**
- [Mighty Armory — Big Boy press, Magnum decap dies](https://www.mightyarmory.com/)
- [AMP Annealing — Mark II](https://www.ampannealing.com/)
- [Brownells — Cerrosafe (only relevant if you change your mind on the chamber-match question)](https://www.brownells.com/)
- [ATF — current processing times (Form 4 and Form 1)](https://www.atf.gov/resource-center/current-processing-times)

**Builders**
- [Warner Tool Company — full rifle builds](https://www.warnertoolcompany.com/)
- [Vestal's Custom Rifles](https://vestalscustomrifles.com/)
- [Alamo Precision Rifles — APR Custom .375 CheyTac](https://aprifles.com/products/apr-custom-375-cheytac)
- [Dzuro's Guns — custom rifles](https://dzurosguns.com/custom_rifles.php)
- [Great Southern Gunworks (Extreme Rifles) — TAC line](https://www.extremerifles.com/tac)

---

## 11. Decision gates before ordering

This section is the actual build checklist. Do not move to the next gate until the current one is answered in writing.

| Gate | Decision | Default | Exit criteria |
|---|---|---|---|
| 1 | Cartridge | .375 EnABELR | Builder confirms brass/die/reamer availability and bolt face. If not, switch to .375 CT. |
| 2 | Bullet | 400gr-class high-BC solid | Exact bullet model selected; builder confirms throat/freebore and twist. |
| 3 | Builder | Warner/GPG/Vestal's RFQ set | Quote accepted with reamer print, test-fire plan, and substitutions documented. |
| 4 | Action | BAT EX | Action maker/builder confirms bolt face, rail, inlet, and lead time. |
| 5 | Barrel | 38" gain 8->7 steel | Builder confirms final length/contour/twist and expected MV window. |
| 6 | Chassis/stock | Builder preference | Inlet, bedding workflow, rail length, and TARAC clearance confirmed. |
| 7 | Elevation system | Kahles + Spuhr + TARAC | Solver estimate confirms the system reaches 2 miles with usable zero and optical shift. |
| 8 | Suppressor | Optional | Legal path and match/range rules checked; Form 4 filed if buying. |
| 9 | Loading setup | Buy after chamber path is final | Brass, dies, shellholder, trimmer, annealing pilot, bullets, powder, primers confirmed. |

**Current recommendation:** start RFQs around .375 EnABELR, but allow a builder to talk the project into .375 CT if they can show stronger sourcing, test-fire, or match-history reasons. The winning answer is the rifle system that can be built, fed, tested, and maintained.

---

## 12. RFQ email template

Send the same email to all three shortlisted builders on the same day. Keep the spec identical so quotes are comparable.

**Contacts:**
- **Warner Tool Company** — via [warnertoolcompany.com](https://www.warnertoolcompany.com/) or phone the shop (NH).
- **Global Precision Group** — Paul Phillips. Reachable via Ultimate Reloader / KO2M circles; phone is reliable.
- **Vestal's Custom Rifles** — via [vestalscustomrifles.com](https://vestalscustomrifles.com/). Bristol, VA.

```
Subject: .375 EnABELR (or .375 CheyTac) Heavy ELR build — RFQ

Hi [shop],

I'm planning a Heavy ELR build and would like a quote and lead-time
estimate. Single-shot, no weight cap, dedicated to KO2M-class shooting.
No existing rifle to match — this is a clean-sheet build optimized for
2-mile hit probability.

I'm running an active decision between .375 EnABELR (preferred, for max
BC + velocity with the Flatline 400gr) and .375 CheyTac classic. I'd
like quotes for both paths if you build both; if you only build one,
please quote that one and tell me why you'd push there.

Working spec (in order of priority):

  1. Use case:        Heavy ELR (no weight cap), single-shot, KO2M-class.
                      First-round-hit at 2 miles is the design target.
  2. Cartridge:       .375 EnABELR (preferred) or .375 CheyTac (alternate).
  3. Bullet / load:   400gr-class .375 ELR solid. Warner Flatline 400gr
                      is the current EnABELR preference; CE/Berger/Hornady
                      alternatives are open if you recommend them.
  4. Barrel:          Bartlein cut-rifled, gain twist 8→7 (or straight
                      1:7.5), 38" finished, MTU contour, threaded for
                      the brake you recommend. Brux or Krieger acceptable
                      as alternates if Bartlein lead is prohibitive.
  5. Action:          BAT EX single-shot, cartridge-appropriate bolt face,
                      integral 40 MOA rail, right-bolt right-eject.
                      Stiller TAC 408 single-feed or Defiance Deviant XM
                      acceptable as alternates.
  6. Trigger:         Bix'n Andy TacSport Pro (preferred) or TriggerTech
                      Diamond Pro. Open to your preference.
  7. Brake:           Terminator T5 (preferred), Area 419 Hellfire (verify
                      .375 thread availability), or your recommended
                      .375-class brake. (APA Fat Bastard Gen 3 is not
                      currently offered in .375 — don't quote that.)
  8. Chassis:         Open to your preference — Cadex CDX-40, McMillan
                      A5 SuperMag, ARC ELR, or MPA BA Comp Heavy all
                      acceptable. Pick what you have the best bedding
                      workflow for.
  9. Optic / mount:   I'll supply — Kahles K540i DLR 5-40x56 (36mm tube,
                      SKMR4+ reticle) on Spuhr SP-6602 (6 MIL / ~20.6 MOA) plus a
                      TACOM HQ Charlie TARAC variable model. I'll source
                      these unless you recommend a different elevation plan.
 10. Finish:          Cerakote, color to discuss. Match brake.

Please quote:
  - Total turnkey price (action, barrel, chassis, trigger, brake,
    fitting, chambering, bedding, threading, finish, test-fire) —
    excluding owner-supplied optic + mount + TARAC + suppressor.
  - Lead time from deposit to test-fire.
  - Accuracy guarantee (group size, distance, rounds).
  - Test-fire scope (rounds fired, ammo source, target medium, data
    provided).
  - Any component substitutions you'd recommend and why.
  - Deposit terms and progress-billing schedule.

Please also answer:
  - Which cartridge would you recommend for this exact use case, and why?
  - What exact chamber/reamer print would you use?
  - What bullet would you cut the throat/freebore around?
  - What bolt face should I order for the BAT EX?
  - What brass, dies, shellholder, and trimming/annealing tooling should I buy?
  - What finished barrel length and contour would you choose for stiffness and balance?
  - What realistic MV window do you expect without running abusive pressure?
  - Can you confirm rail length/clearance for the Spuhr + Charlie TARAC setup?
  - What data will you provide at delivery: target, chrono, starting load/ammo, torque values?
  - What would make you refuse or modify this spec?

If you have a strong preference between EnABELR and CT for the use case,
I want to hear it. I'm open to being talked into either.

Thanks,
[name]
[phone]
[email]
```

**After quotes come back:** score on price, lead time, accuracy guarantee, cartridge-experience depth, who pushed back on what. The right answer is the shop that ships rifles that hit at 2 miles — not cheapest, not fastest.

---

## 13. Support gear (same as v1 — not rifle-dependent)

Rifle is half the system. For 2-mile shooting the LRF, weather meter, chronograph, and spotting setup are co-equal.

### 13.1 Rangefinder

- **Primary:** **Vectronix Terrapin-X** — ~3,000 yd on reflective. ~$3,000.
- **Alternate:** Sig Sauer Kilo 10K-ABS HD (~$2,200).
- **Alternate:** Leica Geovid Pro 32 (binos + LRF, ~$3,500).

### 13.2 Weather meter

- **Primary:** **Kestrel 5700 Elite with Applied Ballistics** — ~$700.

### 13.3 Chronograph (mandatory for new-barrel velocity)

- **Primary:** **Garmin Xero C1 Pro** — radar-based. ~$600.
- **Alternate:** LabRadar (~$560).

### 13.4 Spotting scope + tripod

- **Vortex Razor HD 27-60×85** — ~$1,800.
- **Swarovski STX 25-60×85** — alpha tier, ~$3,500.
- **RRS TVC-34** tripod.

### 13.5 Mat / bags

- **MidwayUSA Pro Series shooting mat** or **Crosstac Tactical**.
- **Edgewood "minigater"** front bag.
- **Protektor Mfg #13** rear bag.

### 13.6 Support gear budget

| Item | Est. cost |
|---|---|
| Vectronix Terrapin-X LRF | $3,000 |
| Kestrel 5700 Elite (AB) | $700 |
| Garmin Xero C1 Pro chrono | $600 |
| Vortex Razor HD spotting scope | $1,800 |
| RRS tripod | $1,200 |
| Edgewood + Protektor bags | $400 |
| **Support gear subtotal** | **~$7,700** |

**Full system budget:** ~$23–24k rifle + components + ~$7.7k support gear = **~$31–32k fully equipped 2-mile shooter** (planning range — quote is source of truth).

---

## 14. Reloading bench notes for .375 EnABELR

.375 EnABELR and .375 CT both stress a bench far harder than normal magnum cartridges. Standard magnum presses may flex meaningfully with these large cases.

### 14.1 Press

- **Mighty Armory Big Boy** — purpose-built for .375 CT / EnABELR / .50 BMG. ([mightyarmory.com](https://www.mightyarmory.com/))
- **Whidden 18" press** — long-stroke alt.
- **Forster Co-Ax** — at capacity limit; works but flexes.

### 14.2 Decapping

- **Mighty Armory Big Boy Magnum Decapping Die** — standard pins flex on big-magnum primer pockets.

### 14.3 Annealing

EnABELR brass is expensive and less widely stocked than .375 CT. Annealing every 2–3 firings can materially extend case life. Treat it as effectively required for this budget tier.

- **AMP Mark II with .375 EnABELR pilot** — ~$1,400.

### 14.4 Powder dispensing

Charges are 155–165 gr. RCBS ChargeMaster handles but slowly.

- **AutoTrickler V4** for precision and volume.

### 14.5 Case prep

- **Giraud Tri-Way trimmer with .375 EnABELR cutter** — trim every firing.
- **K&M chamfer/deburr**.

### 14.6 Components

- **Brass:** Peterson is the best-documented factory source for .375 EnABELR brass and was the production-brass partner for Applied Ballistics. Resellers that have carried it: Mile High Shooting, Solid Solution Designs, Science of Accuracy, Cadex (verify current stock — all of them sell intermittently). Confirm stock and lot availability before chambering; do not assume .375 CT-level supply.
- **Dies:** Warner Tool, Whidden, Shoot-Long, or other custom die makers; confirm current lead time.
- **Powders:** Retumbo, RL-50, H50BMG.
- **Primers:** CCI 250 Magnum or Federal 215M.

---

## 15. Ballistic solver + dope workflow

For .375-class at 2 miles, solver accuracy is the difference between a 6-foot hit and a 6-foot miss.

### 15.1 Recommended solver

- **Applied Ballistics Mobile** (paired with Kestrel 5700 Elite AB) — Custom Drag Model library. **Primary.**
- **Hornady 4DOF** — free, bullet-specific drag. Good second-opinion solver.
- **Strelok Pro** — fine under 1,500 yd; not recommended past that.

### 15.2 Workflow once the rifle is built

1. **Chronograph** — 20 shots in the new barrel, log avg MV.
2. **Truing range** — 600 → 1,500 yd in 200-yd increments. Compare predicted vs actual; adjust MV or G7 BC by ~1% until matched.
3. **Stretch to 2,000 yd.** Re-true if drift > 0.2 mil.
4. **Verify transonic** — plot velocity vs range; no yaw flyers.
5. **Beyond 2,000 yd** — drag curve dominates. Use AB CDM or 4DOF only.

### 15.3 Log every session

Date, location, MV (if chrono'd), atmospherics, wind, range, dial, hold, impact. Cold Bore app or notebook. ~3 sessions and you know the gun.

---

## 16. Range setup + 2-mile target plan

### 16.1 Ranges that support 2 miles

- **NRA Whittington Center** — Raton, NM. Long-standing KO2M Global Finals host. ([nrawc.org — KO2M Global Finals 2026](https://www.nrawc.org/events/items/king-of-2-miles-global-finals-2026/))
- **Spearpoint Ranch** — WY. Private, dedicated ELR.
- **Boomershoot** — ID. Annual ELR event with 1,400-yd targets.
- **Sacramento Valley Shooting Center** — CA. Has hosted KO2M.
- **Camp de Canjuers** — France. Hosted the 2024 KO2M (European venue when KO2M travels off Raton).

**Not a 2-mile venue, but useful for practice/truing:** **K&M Shooting Complex** (Finger, TN) is the premier PRS facility in the southeast, but max distance is roughly 1,200–1,400 yd — not 2-mile work. Use it to true dope before traveling to Raton/Spearpoint for the actual 2-mile session. ([kmprecisionrifletraining.com](https://kmprecisionrifletraining.com/km-shooting-complex/))

### 16.2 Target sizes

| Range | Steel |
|---|---|
| 1,000 yd | 24" (~1 MOA) |
| 1,500 yd | 36" |
| 2,000 yd | 48" |
| 3,000 yd | 60" |
| 3,500 yd (2 mi) | 72" (KO2M plate ~40"×40") |

**AR550 minimum recommended** for durable targets. Confirm target thickness, distance, and impact-energy limits with the range; .375-class ELR rounds can damage light steel.

### 16.3 Spotting

Spotter on tripod, every shot. Bullet trace visible at 2,000+ yd in right light. Time of flight at 2 mi will be several seconds with any .375-class load, so splash/trace timing and wind-call discipline matter.

---

## 17. NFA Form 4 timeline (if running suppressor)

1. File Form 4 when buying.
2. Fingerprints, photos, dealer transfer/admin steps, and any applicable NFA tax. As of 2026, suppressor transfer-tax treatment has changed; verify the current Form 4 instructions and ATF guidance before budgeting a stamp.
3. **Processing time, 2026:** check [ATF's current processing times page](https://www.atf.gov/resource-center/current-processing-times) before relying on a specific number. Recent ranges seen across 2025–2026: **eForm 4 individual ~10–11 days median**, **eForm 4 trust ~11–25 days**, **paper Form 4 ~57–85 days** (paper has been much slower than eForms throughout the post-2024 eForms era). The system has been improving but the spread is large and the snapshot moves week to week.
4. Pick up from dealer when approved.

**Order suppressor early, parallel with rifle build.** Even if the approval is fast, this keeps transfer timing off the rifle-build critical path.

---

## 18. Realistic 2-mile expectations

### 18.1 First-round hit %

Treat hit-probability estimates as anecdotal until you have solver data and range time on this exact rifle. Public ranges quoted by serious ELR shooters under match conditions vary widely with target size, atmospherics, wind, range confidence, and shooter experience. Build a private estimate from your own solver runs and truing data rather than copying numbers out of any build guide (including this one).

### 18.2 Expected groups

| Range | Group (this build, good conditions) |
|---|---|
| 1,000 yd | 0.4–0.6 MOA |
| 1,500 yd | 0.6–0.9 MOA |
| 2,000 yd | 0.8–1.3 MOA |
| 3,500 yd (2 mi) | 1.2–2.5 MOA (~42–87" groups) |

A 72" KO2M plate at 2 mi is *expected*; a 40" plate is genuinely gettable.

### 18.3 Wind dominates past 1,500 yd

A small wind-read error at 2 miles puts the bullet *feet* off target — the exact displacement depends on the bullet/MV/atmospherics combination and should be computed in your solver before treating any number as real. The qualitative point holds regardless of specific values: **wind call matters more than rifle, dope, or optic past 1,500 yd.** Practice wind reading more than anything else.

### 18.4 Barrel life

**~700–1,000 rounds** before accuracy degrades is a reasonable planning placeholder. Actual life depends on pressure, powder, firing cadence, cleaning, and what accuracy standard you require.

### 18.5 Cost-per-shot (.375 EnABELR)

Order-of-magnitude planning numbers; verify current component prices before relying on these.

- Brass amortized over 15 firings: ~$0.65 (assumes ~$10/case)
- Bullet (Warner Flatline 400gr): ~$3.50–$4.50
- Powder (large ELR charge × ~$50/lb): ~$1.20–$1.80
- Primer: ~$0.15
- **Loaded round: ~$6.00–$7.00**

.375 CT shooting comparable 400gr-class bullets runs in roughly the same range; specific delta depends on which bullet/brass you pick and current pricing. A 30-round range trip is on the order of **$180–$210 in components**, not counting travel, fuel, range fees, or rebuilds.

---

## 19. Glossary

| Term | Meaning |
|---|---|
| ELR | Extreme Long Range — 1,500–3,500+ yd |
| KO2M | King of 2 Miles |
| BC | Ballistic Coefficient. G1 = older model, G7 = boattail VLDs |
| SG | Gyroscopic Stability Factor. >1.5 adequate, >2.0 sweet spot |
| MV | Muzzle Velocity |
| MOA | Minute of Angle. ~1.047" at 100 yd |
| Mil | Milliradian. 3.6" at 100 yd. 3.4377 MOA/mil |
| FFP | First Focal Plane |
| COAL / OAL | Cartridge / Overall Length |
| Freebore | Chamber length forward of case mouth |
| Throat | Chamber-to-lands transition |
| Truing | Validating predicted vs actual drop |
| Transonic | ~1.0–1.2 Mach — destabilization zone |
| Form 4 | NFA suppressor transfer form |
| RFQ | Request for Quote |
| EnABELR | Engineered by Applied Ballistics for Extreme Long Range |
| ABWD | Applied Ballistics Weapons Division — Applied Ballistics' rifle/cartridge arm; the channel that fronts EnABELR-class hardware and brass |

### .375 EnABELR at a glance

- Bullet diameter: .375"
- Parent: Applied Ballistics-origin short/wide ELR case family (2019, developed with Peterson)
- Case capacity: Applied Ballistics describes it as "similar to .375 CheyTac" — neither AB nor Peterson publish a specific gr-H₂O number. Confirm with the actual brass lot.
- Typical MV (400gr-class from 38"): ~3,000–3,250 fps depending on load and pressure
- Brass life with annealing: ~15 firings
- Barrel life: ~700–1,000 rounds

### .375 CheyTac classic at a glance

- Bullet diameter: .375"
- Parent: .408 CheyTac necked down
- Case capacity: ~160 gr H₂O (commonly cited; varies by brass lot and case prep)
- Typical MV (400gr from 38"): 3,100–3,180 fps
- Brass life with annealing: ~15 firings
- Barrel life: ~800–1,200 rounds

---

## 20. Future-Claude session brief

### 20.1 Build summary

| Subsystem | Working choice |
|---|---|
| Cartridge | **.375 EnABELR (primary)** / .375 CT (strong alternate) — owner decides before action order |
| Action | BAT EX, cartridge-appropriate bolt face, 40 MOA rail |
| Barrel | Bartlein gain twist 8→7, 38" cut-rifled, MTU contour |
| Bullet | Warner Flatline 400gr (EnABELR) / CE 400gr MTH-MAX (CT) |
| Trigger | Bix'n Andy TacSport Pro |
| Brake | Terminator T5 (or builder's preferred .375-class brake) |
| Optic | Kahles K540i DLR 5-40×56, SKMR4+ |
| Mount | Spuhr SP-6602 (36mm, 6 MIL / ~20.6 MOA cant) |
| Extra elevation | Charlie TARAC variable model — mandatory |
| Bipod | LRA Lite-Tactical |
| Chassis | Defer to builder |
| Builder | Warner Tool/GPG/Vestal's RFQ set for EnABELR; Vestal's/APR/GPG for CT |

### 20.2 Critical context

- This is the **zero-Victrix-compat** build. No projectile, twist, chamber, brass, or load constraints from any other rifle.
- **Cartridge decision (EnABELR vs CT) is the load-bearing call.** Bolt face is cartridge-specific; lock before action order.
- Companion doc `cheytac.md` is the Victrix-compatible v1 — read that if dual-rifle ammo portability matters.

### 20.3 Where the project is

- Doc is v2 build-guide draft; use §11 decision gates before ordering anything.
- No RFQs sent.
- No components ordered.

### 20.4 Next concrete steps

1. **Lock cartridge: EnABELR or CT.** Single biggest decision.
2. Send §12 RFQ to Warner Tool + GPG + Vestal's same day.
3. Pick builder and get cartridge/bolt-face/reamer/bullet answers in writing.
4. Order action and barrel through/with the builder.
5. Order Kahles K540i DLR + Spuhr SP-6602 + builder-confirmed Charlie TARAC configuration.
6. Decide suppressor — if yes, file Form 4 in parallel (§17).
7. Order Vectronix Terrapin-X + Kestrel 5700 Elite + Garmin Xero in parallel.
8. Order LRA bipod + Edgewood/Protektor bags last.

### 20.5 Useful prompts to restart

- "Pick up the .375 EnABELR build from `cheytac2.md`. Status check."
- "Got quotes from Warner + GPG + Vestal's: [paste]. Help me compare."
- "Walk me through the EnABELR vs CT decision one more time."
- "Compare cheytac2.md (no-compromise) vs cheytac.md (Victrix-compat) line by line."

### 20.6 What this doc deliberately does NOT cover

- Any Victrix compatibility — that's `cheytac.md`'s entire scope.
- Hunting use cases.
- .408 CheyTac, .416 Barrett, .50 BMG.
- Repeater actions.
- Light ELR weight-capped builds.
