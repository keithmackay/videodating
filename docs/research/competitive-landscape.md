# Competitive Landscape: Video Speed Dating & Timed-Video Matchmaking

Research compiled 2026-08-30 for the `videodating` project (signup + preferences → Stripe payment → scheduled event → time-bounded, recorded, transcribed video pairing).

---

## 1. Executive summary

- **Video speed dating is a ~6-year-old category with one recurring pattern**: it spikes during forced isolation (COVID 2020–21), then collapses when in-person events return. Almost every pure-play that launched 2020–21 is dead, acquired, or pivoted.
- **The only durable pure-play** is **Filteroff**, which survived by behaving like an *events company* (scheduled, ticketed, curated) rather than a swipe app — and was ultimately acquired by Spark Networks.
- **Big platforms treat video as a feature, not a product.** Hinge shipped in-app video calling in 2020 and quietly killed it in 2023. Meta built and shut down a dedicated video speed-dating product (Sparked) in under a year.
- **The category is re-opening right now.** Tinder announced Video Speed Dating at its March 2026 "Sparks" keynote (LA pilot, 3-minute verified video chats). That validates the model but also signals a well-funded incumbent entering.
- **The hardest problem is not video — it's liquidity.** Every source on speed dating economics converges on the same failure mode: gender ratio imbalance and no-shows. Ticketing, deposits, and gender-quota pricing are the operational levers, and they matter more than any algorithm.
- **The closest solved analogue for "structured timed video session + recording + analysis"** is asynchronous/structured video interviewing (HireVue et al.), which also supplies a strong cautionary tale on ML-from-video: HireVue's own data scientist found visual signals added ~0.25% predictive power, and the company killed facial analysis in 2021 under regulatory pressure.

---

## 2. Pure-play video speed dating platforms

### Filteroff / Filter Off — *the reference implementation*
- Founded by Zach Schleien and Brian Weinreich; launched publicly Feb 2020 (NYC), immediately before lockdown.
- **Model:** location- and interest-segmented **scheduled virtual speed-dating events**. Users join an event; the platform auto-schedules and auto-rotates through a series of short video dates (~3 minutes), with mutual-like gating afterward. Also runs a curated matchmaker service placing users on individual video dates.
- **Monetization:** freemium app + paid/ticketed events + premium matchmaking. Notably raised **$2.4M including ~$2M from AB InBev** (a beer maker sponsoring virtual singles events — an early signal that *sponsorship of events* is a viable second revenue line alongside subscriptions).
- **Traction/press:** #1 on Product Hunt, NYT and BBC coverage.
- **Outcome:** acquired by **Spark Networks SE** (owner of Zoosk, EliteSingles, Jdate, Christian Mingle); Crunchbase records announcement Nov 2022 and completion Oct 2024. Founder moved to VP Marketing at Spark. App still live on iOS/Android as of 2026.
- **Why it matters to us:** closest 1:1 competitor. Its survival argument is that events create *scarcity and a scheduled commitment*, which fixes the "nobody shows up" problem swipe apps have.
- Sources: https://www.getfilteroff.com/about-us · https://www.crunchbase.com/acquisition/spark-networks-acquires-filter-off--4b0f1bbc · https://westchestermagazine.com/archive/filteroff-video-dating/ · https://techround.co.uk/interviews/meet-zach-schleien-brian-weinreich-filteroff/

### Meta "Sparked" — *the well-funded failure*
- Built by Meta's NPE (New Product Experimentation) team; tested 2021 in select markets incl. Chicago, plus themed "global date nights" and dedicated LGBTQ / age-bracket events.
- **Model:** pre-planned local events; **4-minute video dates**, extendable to a **10-minute** second round if both parties opted in. No swiping, no profiles-first — serendipity-first.
- **Monetization:** none (experiment).
- **Outcome:** shut down **January 20, 2022** for lack of traction — despite Facebook's distribution advantage.
- **Lesson:** distribution alone doesn't solve it. Meta had unlimited users and still couldn't get enough *simultaneous, local, correctly-gendered* people into one time slot. Density per (city × time slot × preference bucket) is the binding constraint.
- Sources: https://techcrunch.com/2022/01/13/meta-shuts-down-its-experimental-video-speed-dating-service-sparked/ · https://www.engadget.com/meta-facebook-video-speed-dating-sparked-shutting-down-collab-154126226.html

### SpeedDate.com — *the original (2007-era)*
- Founded by Stanford GSB students Simon Tisminezky and Dan Abelon out of an entrepreneurship class.
- **Model:** round-robin live speed dating in-browser — up to ~15 people in an hour, ~3 minutes each, via live video and IM. Essentially the same product we're building, 18 years earlier.
- **Monetization:** freemium, revenue from premium subscriptions.
- **Outcome:** grew large, later folded into the broader online-dating consolidation; the brand is no longer an operating consumer product.
- Source: https://en.wikipedia.org/wiki/SpeedDate.com

### Ditto (formerly Iso Date)
- Launched Feb 2023, NYC-first, with expansion plans to Toronto/LA.
- **Model:** **3-minute live video speed-dating sessions on a fixed weekly slot (Tuesdays, 8–9pm ET)**. Users set preferences and are matched into rotations.
- **Monetization:** "Ditto Deluxe" at **$19.99/month**, whose headline perk is **"Stop the Clock"** — paying to extend a date past the timer. This is the single most directly copyable monetization idea in the space: it sells the moment of highest emotional intensity.
- **Safety tech:** AI detection of inappropriate content + in-session reporting.
- **Status:** minimal public activity since 2023; treat as likely dormant.
- Source: https://techcrunch.com/2023/02/14/video-dating-apps/

### IRLY ("I Really Like You")
- Launched Feb 2023, Gen Z-targeted.
- **Model:** video chat with **in-app games and conversation prompts** (Truth or Dare, Would You Rather) to defuse awkwardness; "Live Mode" (instant call) vs "Classic Mode" (scheduled). Video and audio messaging.
- **Takeaway:** structured prompts/games are the standard mitigation for dead-air in a 3-minute stranger video call. Worth building as a first-class feature, not a gimmick.
- Source: https://techcrunch.com/2023/02/14/video-dating-apps/

### Candid
- Launched Feb 2023, Bay Area college students. **Asynchronous** video-first, not live speed dating: 45-second in-app videos answering prompts, voted on by others ("creative," "funny," "stunning," "candid"), matched via hashtag/interest categories.
- Relevant as the *other* branch of video dating — async video profiles — which has consistently underperformed live video.
- Source: https://techcrunch.com/2023/02/14/video-dating-apps/

### Glimpse (YC W20) → acquired by twine
- Founded 2019 by Helena Merk and Brian Li; the live product was born the first weekend of SF lockdown: **2-minute conversations with auto-rotation** to the next person. Originally student-focused.
- **Pivoted from dating to professional/event networking**, launched a Zoom Breakout Rooms app, and was **acquired by twine (Feb 2022)**. twine now sells "speed matching" as an enterprise Zoom-native product: automatic timed back-to-back conversations driven by matchmaking rules, tags, and interests.
- **Lesson:** the *rotation engine* is more monetizable B2B (events, conferences, onboarding) than B2C dating. A meaningful adjacent revenue line for our pairing engine.
- Sources: https://medium.com/joinglimpse/glimpse-launches-beta-for-zoom-breakout-room-app-and-is-acquired-by-twine-53fa75ff94f4 · https://partner.zoom.com/solutions/twine/ · https://www.inc.com/kevin-j-ryan/zoom-breakout-rooms-twine-glimpse-acquisition.html

### Sparkze
- Positions video dating as an **online game show** format rather than a 1:1 rotation — group-format entertainment with elimination mechanics. Niche but shows the "format-as-differentiator" path.
- Source: https://www.datingadvice.com/online-dating/online-speed-dating

---

## 3. Incumbent dating apps and their video features

### Tinder — Video Speed Dating (2026, active threat)
- Announced at **Tinder Sparks 2026** (March 12, 2026), the company's first product keynote and its largest overhaul in years (10+ features).
- **Video Speed Dating:** **3-minute live video chats for photo-verified users only**, scheduled sessions framed as a "vibe check," **with the option to extend** promising sessions (same mechanic Ditto charged for). Piloting in **Los Angeles**, broader testing later in 2026.
- Shipping alongside: **Chemistry** (AI recommendation layer using personality signals and optional image analysis), an **Events tab** (browse local trivia nights, pottery classes, see which singles are attending), and **Face Check** mandatory liveness verification rolling out globally.
- **Implication for us:** identity/liveness verification gating entry to video is becoming table stakes, not a differentiator. Tinder is validating both the format and the price of admission (verification friction).
- Sources: https://techcrunch.com/2026/03/12/tinder-tries-to-lure-people-back-to-online-dating-with-irl-events-virtual-speed-dating/ · https://www.tinderpressroom.com/2026-03-12-Tinder-Debuts-Inaugural-Product-Keynote-Tinder-Sparks-2026-Start-Something-New · https://www.globaldatinginsights.com/featured/tinder-sparks-2026-ai-upgrades-event-system-video-speed-dating/

### Hinge — built video calling, then killed it
- Rolled out in-app audio/video "Date From Home" during 2020. **Quietly sunset the audio and video calling feature in 2023** once in-person dating resumed; users preferred to move straight to IRL dates.
- **The single most important negative datapoint in this research.** 1:1 video calling *between existing matches* is a feature users abandon. What Hinge shut down is not what we're building — the durable thing is video as the *discovery/screening* mechanism (you meet strangers you'd never have matched with), not video as a step between matching and meeting.
- Source: https://www.fastcompany.com/90955293/hinge-quietly-shuts-down-its-pandemic-era-audio-and-video-calling-feature

### Bumble
- Shipped video chat + audio calls in 2019/2020 and a **"Virtual Date Badge"** letting users signal willingness to video chat — a lightweight consent/intent signal worth copying. Bumble still offers audio and video calls as of the most recent reporting, making it the main incumbent that *didn't* retreat.
- Source: https://www.cnbc.com/2021/08/28/the-future-of-dating-apps-match-bumble-is-much-more-social.html

### Match, Plenty of Fish, Zoosk, Jack'd
- All shipped free video during 2020. POF and Zoosk went further with **livestreaming to the whole community**, not just matches — a one-to-many format that converts better for engagement metrics than 1:1 but is a different product.

### Coffee Meets Bagel, OkCupid, HER
- Notably **did not build native video** — they pointed users at Zoom/FaceTime instead. CMB's own survey of 1,140 users found only **28% planned to video chat more** post-outbreak vs 39% who'd text more. Weak intrinsic demand for video among their (relationship-oriented) users.
- Sources: https://www.forbes.com/sites/dawnstaceyennis/2021/12/25/how-dating-apps-are-countering-foda-this-covid-19-christmas/ · https://fortune.com/2020/04/13/online-dating-apps-coronavirus-bumble-tinder-hinge-quarantine-covid-19/

### Adoption baseline
Tinder reported that a large share of users video chatted with a match during the pandemic and **~40% said they'd continue using video post-pandemic** — the stated intent was strong; the revealed behavior (Hinge's shutdown) was much weaker. Discount stated intent heavily.

---

## 4. Adjacent video-first dating apps (context, mostly cautionary)

| App | Model | Status / outcome |
|---|---|---|
| **Snack** | "Video-first dating," TikTok-style vertical video profiles, Gen Z | Raised $3.5M pre-seed + $2M SAFE incl. a "Gen Z Syndicate" of young investors; hyped 2021, little visible traction since |
| **Lolly** | Match while browsing short-form video content | Wound down |
| **Feels** | Video/multimedia-heavy profiles, anti-swipe | Still operating (France-origin), niche |
| **Loveflutter** | Text/personality-first, "Promoted Places" ad model to stay free | Defunct |
| **The Right Stuff** (Date Right Stuff) | Thiel-backed conservative dating app, invite-only | **Shut down Nov 21, 2025** with ~24 hours' notice; had been reported as floundering within 3 months of launch, plagued by bugs and bots |
| **Taimi** | LGBTQ+ platform with 1:1 video chat | Operating |
| **LivU / Chatroulette-likes** | Random video matching with filters | Operating but a different (and reputationally risky) category |
| **Blush** | AI dating *simulator*, not human matching | Operating; adjacent, not competitive |

Sources: https://thehustle.co/04192021-snack-app · https://melmagazine.com/en-us/story/snack-feels-lolly-gen-z-dating-apps · https://en.wikipedia.org/wiki/The_Right_Stuff_(app) · https://www.thedailybeast.com/peter-thiels-conservative-dating-app-floundering-after-3-months/

---

## 5. Event-operator businesses (offline + virtual)

These are the operators who understand the *unit economics* of a timed rotation, which is the part software teams usually get wrong.

- **SpeedDater (UK)**, **Slow Dating (UK)**, **Fastlife / FastLife (Canada, later linked with Plenty of Fish)** — traditional IRL speed dating operators. FastLife claims the world's largest range of speed dating events; its software exists only to sell tickets and reveal mutual matches afterward. Slow Dating experimented with virtual events during COVID and **no longer offers them** — a direct signal on virtual demand outside lockdown.
- **Lightning Speed Dating** — pivoted to virtual matchmaking alongside real-life events and won industry recognition for it.
- **Thursday** — event-based dating app; **pivoted entirely from app to event ticketing in January 2025** after hitting 2M users. Revenue is member-only tickets to curated mixers plus subscription tiers (early match access, higher swipe limits). Strongest recent evidence that *ticketed events* beat *swipe subscriptions* for this cohort.
- **Eventbrite data:** attendance at dating/singles events rose **42% from 2022 to 2023** — the IRL speed dating revival is real, and it's the demand pool a virtual product must either serve or steal from.

Sources: https://techcrunch.com/2024/08/08/thursday-dating-app-san-francisco-launch/ · https://slowdating.com/virtual-online-speed-dating-uk · https://www.datingnews.com/industry-trends/lightning-speed-dating-pioneers-virtual-matchmaking/ · https://speed-dating-websites.no1reviews.com/fastlife.html

### Rotation/event software vendors (B2B — potential competitors *and* potential model)
- **twine for Zoom** — Zoom-native automated timed rotation with matchmaking rules/tags. The most mature engine.
- **Fanciful** (fanciful.app) — dedicated virtual speed dating + speed-dating **event management software**, sold to organizers.
- **SpeedMatchApp** (speedmatchapp.com) — matchmaking events for speed dating, speed networking, business matchmaking, speed mentoring.
- **VEvents** (vevents.pro) — virtual speed dating and business networking events.
- **Remo**, **Kumospace** — general virtual event platforms with floor plans, AI matchmaking, and documented speed-dating playbooks.

If our pairing/rotation engine is good, selling it to independent speed-dating organizers is a lower-CAC revenue line than acquiring daters directly.

---

## 6. Why some succeed and most fail

Synthesized from the above; the patterns are consistent.

**Failure causes**
1. **Liquidity per time slot, not total users.** A speed dating event needs N men and N women *in the same city bucket, same age band, same 60 minutes*. Meta's Sparked died with Facebook-scale distribution because that intersection is brutally thin. This is the #1 killer.
2. **Gender ratio and no-shows.** Organizers universally report women's tickets selling out "in milliseconds" while men's take a week (in NYC hetero events the reported skew often runs the other way in some markets — either way, imbalance is the norm). One NYC event had 2 men against 20+ women and had to pay staff $20 each to sit in. Any imbalance beyond ~1–2 people forces attendees to sit out rounds and wrecks the experience.
3. **Video is a step users skip, not a step they want.** Hinge's shutdown; CMB's 28% figure. Users want to meet in person; video is tolerated only when it *replaces* an unavailable in-person option or *saves* them a bad date.
4. **Post-lockdown demand cliff.** Every 2020–21 launch faced a market that evaporated in 2022.
5. **Bots, safety, and Omegle-adjacency.** The Right Stuff died partly on bots. Any open video product inherits Chatroulette's reputational tail risk without hard verification.

**Success causes**
1. **Scheduled, ticketed commitment.** Payment is not just revenue — it's the anti-no-show mechanism and the gender-ratio lever. Filteroff and Thursday both monetize the commitment itself.
2. **Curation and segmentation** (city, age band, interest, identity group) to make thin liquidity feel dense.
3. **Verification as a product feature.** Tinder's Face Check gating video is the emerging standard.
4. **Selling the extension moment.** Ditto's paid "Stop the Clock" and Tinder's optional extend both monetize peak intent.
5. **Structure inside the call** — prompts, games, visible timer — so a 3-minute stranger call doesn't die in silence (IRLY).
6. **Sponsorship / brand partnership on events** (Filteroff × AB InBev, ~$2M) — an events business has advertisers a swipe app doesn't.

**Pricing benchmarks (IRL, useful for anchoring)**
- Speed dating tickets typically **$20–$40**, NYC **$25–$60** depending on operator, venue, age bracket.
- Organizers actively **price-discriminate by gender and live demand** to balance ratios (free tickets for the scarce side; up to ~$41 for the abundant side), and use "bring a friend of the opposite gender, half off" referrals.
- Subscription comp: Ditto Deluxe **$19.99/mo**.

Sources: https://www.zippymatch.com/How-much-should-I-charge-for-my-speed-dating-event/ · https://www.mysocialcalendar.com/news/speed-dating-nyc · https://dkras.substack.com/p/dating-experiments

---

## 7. Matching algorithms worth knowing

### Gale–Shapley / stable marriage — used by Hinge ("Most Compatible")
- Devised 1962 by David Gale and Lloyd Shapley for the stable marriage problem; Shapley shared the 2012 Nobel in Economics (with Roth) for it.
- Produces a **stable matching**: no two people would both prefer each other over their assigned partners.
- **Hinge's adaptation:** learns preferences implicitly from like/pass behavior rather than stated criteria, and **removes the gender division** — everyone is in one pool proposing/receiving, rather than the classic men-propose/women-dispose formulation. Surfaces one "Most Compatible" person per day.
- **Reported result:** Most Compatible pairs exchange phone numbers **~8× more often** than ordinary matches.
- **Direct relevance:** this is exactly the right family of algorithms for our problem. Assigning K rotation partners per participant at a scheduled event is a *many-to-many stable assignment under time-slot constraints* — closer to hospital/residents matching (Roth's NRMP) than to a recommender system. Bipartite matching with capacity constraints + a round-scheduling layer (each participant occupies exactly one room per round, meets each partner at most once) is the core technical problem.
- Sources: https://techcrunch.com/2018/07/11/hinge-employs-new-algorithm-to-find-your-most-compatible-match-for-you/ · https://thehustle.co/hinge-machine-learning-algorithm

### OkCupid — weighted question matching
- Each question has three inputs: your answer, your desired answer from a partner, and **importance**.
- Importance is scored on a fixed scale: **Irrelevant = 0, A little = 1, Somewhat = 10, Very = 50, Mandatory = 250**.
- Compute satisfaction of A by B's answers, and of B by A's, then combine (geometric mean of the two percentages) to produce a symmetric match percentage.
- **Relevance:** cheap, explainable, cold-start-friendly. A small weighted-question set at signup gives us a compatibility prior *before* anyone has any behavioral history — exactly the cold-start problem a scheduled-event product has on day one. Also gives users a legible reason for a pairing, which matters when they've paid.
- Sources: https://www.ted.com/talks/christian_rudder_inside_okcupid_the_math_of_online_dating · https://blogs.ams.org/mathgradblog/2016/06/08/okcupid-math-online-dating/ · https://hdsr.mitpress.mit.edu/pub/i4eb4e8b

### eHarmony — 29 Dimensions of Compatibility
- Developed by clinical psychologist Neil Clark Warren with Galen Buckwalter (Chief Scientific Officer 1997–2008). Core patent: **US 6,735,568** (Buckwalter et al.).
- **~436-question psychometric intake**, grouped into sections including Emotional Temperament, Social Style, Cognitive Mode, Physicality. Matches were required to clear a threshold across a large majority of the 29 dimensions (reported as >25/29).
- The exact 29 dimensions were never disclosed; publicly named examples include humor, spirituality, sociability, ambition.
- **Relevance & caution:** heavy intake questionnaires produce great match quality *for the users who finish them* and catastrophic signup drop-off for everyone else. For a paid-event product, the questionnaire is better placed **after** payment (sunk-cost keeps completion high) than before.
- Sources: https://www.eharmony.com/tour/what-is-the-compatibility-quiz/ · https://courses.edx.org/asset-v1:MITx+15.071x_2a+2T2015+type@asset+block/Unit9_eHarmony_AllSlides.pdf · https://www.prnewswire.com/news-releases/eharmony-unveils-its-compatibility-scoring-for-the-first-time-300378763.html

### Prior art warning
**US 2022/0261927 A1 — "Speed Dating Platform with Dating Cycles and Artificial Intelligence."** A published US patent application covering, by title, essentially our product category (cyclic speed-dating rounds + AI). Worth a proper read by counsel before launch — it is the most direct IP risk surfaced in this research.
Source: https://patents.google.com/patent/US20220261927A1/en

---

## 8. Structured timed video sessions outside dating

### HireVue — the closest technical analogue
- Structured/asynchronous video interviewing: candidates answer a fixed set of job-analysis-derived questions on camera under a timer; responses are recorded, transcribed, and scored.
- Scale: **19M+ video interviews across 700+ customers**, so the ingest/recording/transcription pipeline at our target scale is a solved, commoditized problem.
- **The critical lesson:** HireVue **discontinued facial-expression analysis in January 2021** after pressure from researchers, regulators, and EPIC (which filed an FTC complaint). Their own data scientist stated that **visual data added roughly 0.25% of predictive power** — essentially nothing.
- Post-2021 the product scores **verbal content, response structure, language patterns**, and in some configurations vocal delivery (pace, filler words).
- **Direct implications for our recorded/transcribed calls:**
  1. Don't build facial/emotion analysis. It doesn't work, and it's a regulatory magnet (Illinois BIPA, NYC Local Law 144, EU AI Act high-risk classification).
  2. **The transcript is the asset, not the video.** Text carries nearly all the extractable signal, is cheap to store and process, and is far less sensitive than raw video.
  3. Recording a two-party conversation requires **two-party consent** in many US states (CA, IL, FL, PA, WA, MA…) — explicit in-flow consent from both participants before the session starts, plus retention limits and deletion, is non-negotiable.
- Sources: https://www.shrm.org/topics-tools/news/talent-acquisition/hirevue-discontinues-facial-analysis-screening · https://incidentdatabase.ai/cite/95/ · https://d3.harvard.edu/platform-peopleanalytics/submission/hirevue-a-face-scanning-algorithm-decides-whether-you-deserve-the-job

### Enterprise speed-networking
twine/Zoom, Remo, Kumospace (§5) solve the same rotation scheduling problem for conferences, onboarding, and mentoring. Their published patterns — pre-tagged interests, rule-based matching, automatic timed room moves, "don't repeat a partner" constraints — are the de facto spec for a rotation engine.

---

## 9. Implications for `videodating`

1. **Design the scheduler as the core IP.** Stable matching (Gale–Shapley family) with round/room constraints, no-repeat-partner, and graceful degradation when the ratio is off (e.g. auto-inserted "breather" rounds instead of visible sit-outs).
2. **Payment is a ratio lever, not just revenue.** Dynamic per-side pricing, refundable deposits against no-shows, and waitlists are the operational answer to the #1 category killer. Stripe should support variable pricing per cohort, refunds/holds, and bring-a-friend discounts from day one.
3. **Overbook and pre-confirm.** Speed-dating no-show rates are high; require a same-day confirm tap and a device/AV check before the event to prune ghosts.
4. **Verification before video.** Photo/liveness verification gating entry is now the industry norm (Tinder Face Check). Cheaper than moderating an incident.
5. **Structure inside the 3 minutes.** Visible timer, prompt cards, an optional icebreaker — this is what separates a good session from dead air.
6. **Monetize the extension.** "Stop the Clock" (Ditto, $19.99/mo) and Tinder's extend option both target the same peak-intent moment.
7. **Transcript-first analysis, no face analysis.** Two-party recording consent in the join flow; short default retention; per-user delete. Treat the transcript as the product surface (recap, "you both mentioned X," follow-up prompts).
8. **Niche and schedule tightly.** Thin liquidity is survivable only via segmentation plus concentration — few events, well-attended, per city/age/interest — never an always-on lobby.
9. **Consider the B2B rotation-engine line** (organizers, conferences) as a hedge; it's where Glimpse found its exit.
10. **Do the freedom-to-operate check** on US 2022/0261927 A1 before launch.

---

## Sources

- TechCrunch — Video dating app startups (2023): https://techcrunch.com/2023/02/14/video-dating-apps/
- TechCrunch — Meta shuts down Sparked: https://techcrunch.com/2022/01/13/meta-shuts-down-its-experimental-video-speed-dating-service-sparked/
- TechCrunch — Tinder IRL events + virtual speed dating (2026): https://techcrunch.com/2026/03/12/tinder-tries-to-lure-people-back-to-online-dating-with-irl-events-virtual-speed-dating/
- Tinder Press Room — Sparks 2026 keynote: https://www.tinderpressroom.com/2026-03-12-Tinder-Debuts-Inaugural-Product-Keynote-Tinder-Sparks-2026-Start-Something-New
- Global Dating Insights — Tinder Sparks 2026: https://www.globaldatinginsights.com/featured/tinder-sparks-2026-ai-upgrades-event-system-video-speed-dating/
- Fast Company — Hinge shuts down audio/video calling: https://www.fastcompany.com/90955293/hinge-quietly-shuts-down-its-pandemic-era-audio-and-video-calling-feature
- CNBC — Dating apps turn to video and audio: https://www.cnbc.com/2021/08/28/the-future-of-dating-apps-match-bumble-is-much-more-social.html
- Filteroff: https://www.getfilteroff.com/about-us · Crunchbase acquisition: https://www.crunchbase.com/acquisition/spark-networks-acquires-filter-off--4b0f1bbc
- Glimpse → twine: https://medium.com/joinglimpse/glimpse-launches-beta-for-zoom-breakout-room-app-and-is-acquired-by-twine-53fa75ff94f4 · https://partner.zoom.com/solutions/twine/
- TechCrunch — Hinge Most Compatible / Gale-Shapley: https://techcrunch.com/2018/07/11/hinge-employs-new-algorithm-to-find-your-most-compatible-match-for-you/
- The Hustle — Hinge's Nobel algorithm: https://thehustle.co/hinge-machine-learning-algorithm
- Christian Rudder TED — Inside OkCupid: https://www.ted.com/talks/christian_rudder_inside_okcupid_the_math_of_online_dating
- Harvard Data Science Review — Matching algorithms in online dating: https://hdsr.mitpress.mit.edu/pub/i4eb4e8b
- eHarmony Compatibility Quiz: https://www.eharmony.com/tour/what-is-the-compatibility-quiz/
- SHRM — HireVue discontinues facial analysis: https://www.shrm.org/topics-tools/news/talent-acquisition/hirevue-discontinues-facial-analysis-screening
- AI Incident Database #95: https://incidentdatabase.ai/cite/95/
- TechCrunch — Thursday dating app: https://techcrunch.com/2024/08/08/thursday-dating-app-san-francisco-launch/
- Wikipedia — SpeedDate.com: https://en.wikipedia.org/wiki/SpeedDate.com · The Right Stuff: https://en.wikipedia.org/wiki/The_Right_Stuff_(app)
- ZippyMatch — speed dating event pricing: https://www.zippymatch.com/How-much-should-I-charge-for-my-speed-dating-event/
- Google Patents US20220261927A1: https://patents.google.com/patent/US20220261927A1/en
