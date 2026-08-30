# Compatibility Science: What Actually Predicts Romantic Connection

Research survey for the videodating speed-dating platform. Compiled 2026-08-30.

Downloaded PDFs live in [`papers/`](papers/) (39 files, all verified). Sources marked
**cited-only** were paywalled with no retrievable open-access version.

---

## Executive summary — the five findings that should drive product decisions

1. **Pre-interaction questionnaires cannot predict dyad-specific attraction.** Joel,
   Eastwick & Finkel (2017) threw 100+ self-report measures and random forests at two
   speed-dating studies. They could predict *actor* variance (how choosy you are) and
   *partner* variance (how desirable you are in consensus), but predicted
   **relationship variance — the "chemistry" term — at essentially zero out of sample**,
   despite it being the largest variance component. This is the load-bearing constraint
   on the whole category.

2. **The interaction itself carries real, measurable signal.** McFarland, Jurafsky &
   Rawlings (2013) found that traits explain ~15% of variance in "clicking" while speech
   features add **another 7.5% net of traits** — roughly a third of the explainable
   signal — and that this grows with each additional minute of conversation. This is
   precisely the data a video product has and a profile-matching site does not.

3. **Stated preferences are near-worthless; revealed behavior is everything.** Four
   independent literatures converge (Eastwick & Finkel 2008; Fisman et al. 2006/2008;
   Kurzban & Weeden 2005/2007; Hitsch, Hortaçsu & Ariely 2010). Onboarding preference
   sliders should be treated as a cold-start crutch, never as the matching substrate.

4. **Optimize for mutual acceptance, not one-sided relevance.** The reciprocal
   recommender literature (Pizzato et al. 2010 onward) shows one-sided ranking
   systematically fails in two-sided markets, producing congestion on a few popular
   users. Harmonic-mean or min-like aggregation of the two directional scores is the
   established fix.

5. **Report held-out, base-rate-adjusted metrics or you are repeating Gottman's error.**
   Heyman & Smith Slep (2001) showed Gottman-style divorce prediction collapsed from 90%
   accuracy / 65% PPV in-sample to 69% / **29%** on a holdout, and **21%** after base-rate
   adjustment. Ranganath et al. (2013) drop from 78% to 53% accuracy on unseen speakers.
   Speaker-disjoint validation is mandatory.

**Net thesis:** *who* two people are, measured before they meet, predicts compatibility
barely at all; *how the conversation actually goes* predicts a meaningful amount. That is
a strong argument for video-first — and a hard ceiling on any marketing claim about
predicting matches from profiles. Even the best in-conversation models top out around
r ≈ 0.2–0.5 or 70–75% balanced accuracy.

---

## 1. Classic Psychological Compatibility Literature

### 1.1 Similarity–attraction

**Byrne, D. (1971). *The Attraction Paradigm*. Academic Press.** *(book, cited-only)*
The founding "law of attraction": attraction is a linear function of the *proportion* of
attitudes shared, not the raw count. Practical consequence: any similarity score must be
normalized by items answered, not summed.

**Montoya, R. M., Horton, R. S., & Kirchner, J. (2008). Is actual similarity necessary for
attraction? A meta-analysis of actual and perceived similarity. *Journal of Social and
Personal Relationships*, 25(6), 889–922.**
[DOI](https://doi.org/10.1177/0265407508096700) ·
[PDF](http://persweb.wabash.edu/facstaff/hortonr/pubs/Montoya,%20Horton,%20&%20Kirchner,%202008,%20JSPR%20similarity%20effect%20meta%20analysis.pdf)
→ `montoya2008_actual_perceived_similarity_meta.pdf`

460 effect sizes from 313 studies. Actual similarity r ≈ .47, perceived similarity r ≈ .39
overall — but the moderator pattern is what matters: actual similarity predicts attraction
in *no-interaction* and *short-interaction* paradigms and is **non-significant in existing
relationships**, while perceived similarity predicts at every stage. Computed profile
similarity is a decent predictor of "would swipe" and a poor predictor of what happens
after people talk.

**Montoya, R. M., & Horton, R. S. (2013). A meta-analytic investigation of the processes
underlying the similarity-attraction effect. *JSPR*, 30(1), 64–94.** *(cited-only)*
[DOI](https://doi.org/10.1177/0265407512452989) — 240 lab studies. Key moderators are
proportion of similarity, **centrality/importance of the attitude**, and salience. Weight
similarity items by self-rated importance; an unweighted Jaccard over trivia underperforms.

**Bahns, A. J., Crandall, C. S., Gillath, O., & Preacher, K. J. (2017). Similarity in
relationships as niche construction. *JPSP*, 112(2), 329–355.**
[DOI](https://doi.org/10.1037/pspp0000088) ·
[PDF](https://quantpsy.org/pubs/bahns_crandall_gillath_preacher_2017.pdf)
→ `bahns2017_similarity_niche_construction.pdf`

11 field samples, 1,523 interacting dyads. Within-dyad similarity was significant on 86% of
measured variables and was present **at the outset**, not increasing with duration — pairs
are selected-in similar rather than converging. Similarity also predicted dyad stability.
Do not expect a "they'll grow alike" effect to rescue a mismatched pair.

**Tidwell, N. D., Eastwick, P. W., & Finkel, E. J. (2013). Perceived, not actual,
similarity predicts initial attraction in a live romantic context. *Personal
Relationships*, 20(2), 199–215.**
[PDF](https://faculty.wcas.northwestern.edu/eli-finkel/documents/InPress_TidwellEastwickFinkel_PersonalRelationships_000.pdf)
→ `tidwell2013_perceived_similarity_speeddating.pdf`

The live-context confirmation of Montoya's moderator: in real speed dates **perceived**
similarity predicted liking; **actual** similarity across personality, attitudes and values
did not. Unusually direct design consequence — the system's job may be less to maximize
measured similarity than to *surface and make salient* the overlap that already exists.

### 1.2 Complementarity — weak support

**Winch, R. F. (1958). *Mate-Selection: A Study of Complementary Needs*.** *(book,
cited-only)* Origin of the complementary-needs hypothesis. Support has been scattered;
"complementary" is rarely operationalized independently of outcome.

**Dijkstra, P., & Barelds, D. P. H. (2008). Do people know what they want: A similar or
complementary partner? *Evolutionary Psychology*, 6(4), 595–602.** *(cited-only)*
[DOI](https://doi.org/10.1177/147470490800600406) — Correlations between own personality
and *ideal partner* personality strongly support similarity, yet asked in the abstract most
people say they want a complementary partner. Another stated-vs-actual dissociation.

Complementarity survives only in narrow interlocking pairs (dominance–submissiveness on the
interpersonal circumplex; nurturance–dependence) and mainly for long-term rather than
initial attraction. Not a viable general matching principle.

### 1.3 Attachment theory

**Hazan, C., & Shaver, P. (1987). Romantic love conceptualized as an attachment process.
*JPSP*, 52(3), 511–524.** *(cited-only)*
[DOI](https://doi.org/10.1037/0022-3514.52.3.511) ·
[PubMed](https://pubmed.ncbi.nlm.nih.gov/3572722/)
Introduced the three-category adult attachment measure (secure/anxious-ambivalent/avoidant),
showing the infant distribution roughly replicates in adults (~56/19/25%). Styles predicted
love experiences, mental models, and relationship duration. Note it is a *three-item
forced-choice* instrument, since superseded by dimensional anxiety/avoidance scales (ECR).

**Li, T., & Chan, D. K.-S. (2012). How anxious and avoidant attachment affect romantic
relationship quality differently: A meta-analytic review. *EJSP*, 42(4), 406–419.**
*(cited-only)* [DOI](https://doi.org/10.1002/ejsp.1842) — 73 studies, N = 21,602. Both
dimensions are detrimental; **avoidance** is the stronger negative predictor. The predictive
value is largely an **actor** effect, making attachment a per-user risk/expectation feature
rather than a dyadic matching key.

**Candel, O.-S., & Turliuc, M. N. (2019). Insecure attachment and relationship satisfaction:
A meta-analysis of actor and partner associations. *PAID*, 147, 190–199.** *(cited-only)*
[DOI](https://doi.org/10.1016/j.paid.2019.04.037) — Actor effects substantially exceed
partner effects. Same warning against "complementary attachment pairs."

### 1.4 Big Five and relationship satisfaction

**Malouff, J. M., et al. (2010). The Five-Factor Model of personality and relationship
satisfaction of intimate partners: A meta-analysis. *JRP*, 44(1), 124–127.** *(cited-only)*
[DOI](https://doi.org/10.1016/j.jrp.2009.09.004) — 19 samples, N = 3,848. Four traits
predict *the partner's* satisfaction: low neuroticism (strongest), high agreeableness,
conscientiousness, extraversion; openness does not. Note the shape — this is a **main effect
of one person's trait level**, not an interaction. Some people are better partners on
average. That is a *ranking* signal, not a matching signal.

**Neyer, F. J., & Asendorpf, J. B. (2001). Personality–relationship transaction in young
adulthood. *JPSP*, 81(6), 1190–1204.**
[DOI](https://doi.org/10.1037/0022-3514.81.6.1190) ·
[PDF](https://www.ffri.hr/~ibrdar/komunikacija/seminari/Asendorph,%202001%20-%20Personality%20-%20relationship%20transaction.pdf)
→ `neyer2001_personality_relationship_transaction.pdf`
Personality effects on relationship outcomes strongly dominated the reverse, except at the
transition into a first partnership. Personality is largely a *stable exogenous* predictor —
good news for using it as a persistent user feature.

**Mund, M., & Neyer, F. J. (2014). Treating personality–relationship transactions with
respect. *European Journal of Personality*.** *(cited-only)*
[DOI](https://doi.org/10.1002/per.1966) — Narrow **facets** outpredict broad domains.
Facet- or item-level personality features will likely beat five aggregated scores.

**Weidmann, R., Schönbrodt, F. D., Ledermann, T., & Grob, A. (2017/2018). Actor, partner,
and similarity effects of personality on global and experienced well-being. *JRP*.**
*(cited-only)* [DOI](https://doi.org/10.1016/j.jrp.2018.06.003) — The decisive negative
result for similarity matching on personality: **actor and partner effects are robust;
similarity effects are negligible and mostly vanish once main effects are controlled.** A
model scoring couples on Big Five profile distance is unlikely to beat one that just scores
each person's own trait levels.

### 1.5 Gottman — and the critiques

**Gottman, J. M., & Levenson, R. W. (1992). Marital processes predictive of later
dissolution. *JPSP*, 63(2), 221–233.**
[DOI](https://doi.org/10.1037/0022-3514.63.2.221) ·
[PDF](https://bpl.studentorg.berkeley.edu/docs/41-Marital%20Processes92.pdf)
→ `gottman1992_marital_processes_dissolution.pdf`
Established the *regulated / non-regulated* typology from observational coding of a
15-minute conflict discussion. Methodologically this is the origin of thin-slice couple
prediction — short structured video-recorded interaction, machine-codable affect, downstream
outcome — the exact template a video product can reproduce.

**Gottman, J. M., & Levenson, R. W. (2000). The timing of divorce: Predicting when a couple
will divorce over a 14-year period. *JMF*, 62(3), 737–745.** *(cited-only)*
[DOI](https://doi.org/10.1111/j.1741-3737.2000.00737.x) — Different predictors for different
timings: **negative affect during conflict predicted *early* divorce; absence of positive
affect predicted *late* divorce.** Reported ~93% accuracy. The timing-dependence result is
the substantive gem — "negativity" and "no positivity" are distinct failure modes on
distinct clocks. The 93% figure is what the critiques below dismantle.

**Gottman, J. M. (1993/1999). A theory of marital dissolution and stability.**
[PDF](https://www.johngottman.net/wp-content/uploads/2011/05/A-theory-of-marital-dissolution-and-stability.pdf)
→ `gottman1999_theory_marital_dissolution.pdf`
The theory behind the Four Horsemen (criticism, contempt, defensiveness, stonewalling) and
the ~5:1 positive-to-negative ratio in stable couples. Contempt is repeatedly the strongest
single negative marker.

**Heyman, R. E., & Smith Slep, A. M. (2001). The hazards of predicting divorce without
crossvalidation. *JMF*, 63(2), 473–479.** *(cited-only; open full text at
[PMC1622921](https://pmc.ncbi.nlm.nih.gov/articles/PMC1622921/))*
**The most important methodological citation in this document.** Splitting 528 respondents
into build/holdout halves: 90% accuracy and 65% PPV on the development sample collapsed to
69% accuracy and **29% PPV** on holdout; adjusting for the true 16% base rate dropped PPV to
**21%**. Gottman's headline figures were post-hoc fitted equations reported without
cross-validation.

**Stanley, S. M., Bradbury, T. N., & Markman, H. J. (2000). Structural flaws in the bridge
from basic research on marriage to interventions for couples. *JMF*, 62(1), 256–264.**
*(cited-only)* [DOI](https://doi.org/10.1111/j.1741-3737.2000.00256.x) — Objects to
inferring causal, intervention-ready mechanisms from correlational observational data, to
deriving variables after outcomes were known, and to overreach from small samples into
prescriptive advice.

**Kim, H. K., Capaldi, D. M., & Crosby, L. (2007). Generalizability of Gottman and
colleagues' affective process models. *JMF*, 69(1), 55–72.** *(cited-only; open at
[PMC1828692](https://pmc.ncbi.nlm.nih.gov/articles/PMC1828692/))*
Independent replication on 85 couples: **"the major findings of Gottman et al. failed to
replicate."** Only 2 of 22 affective processes predicted separation. Affect *clusters* still
related to satisfaction; affect *sequences* predicted nothing. For the product: the coarse
"how much positive vs negative affect is in this interaction" signal has some support; the
elaborate sequential-microcoding machinery does not generalize.

### 1.6 Aron — manufactured closeness

**Aron, A., Melinat, E., Aron, E. N., Vallone, R. D., & Bator, R. J. (1997). The
experimental generation of interpersonal closeness. *PSPB*, 23(4), 363–377.** *(cited-only —
every candidate PDF resolved to a course deck or paywall)*
[DOI](https://doi.org/10.1177/0146167297234003)
The "36 questions." 45 minutes of reciprocal escalating self-disclosure produced
significantly greater closeness than matched small talk. Studies 2–3 found **no** effect of
matching pairs on attitude agreement, of expecting mutual liking, or of making closeness an
explicit goal. Two actionable consequences: (a) closeness in a first conversation is a
manipulable property of the **prompt structure**, so the product can raise baseline
connection for everyone by scripting escalating reciprocal disclosure; (b) the null on
attitude matching is another blow to similarity-based pairing.

### 1.7 Fisher temperament typing

**Brown, L. L., Acevedo, B., & Fisher, H. E. (2013). Neural correlates of four broad
temperament dimensions. *PLOS ONE*, 8(11), e78734.**
[DOI](https://doi.org/10.1371/journal.pone.0078734) → `brown2013_neural_correlates_fti.pdf`
fMRI validation of the FTI's four dimensions against hypothesized neurochemical systems
(dopamine / serotonin / testosterone / estrogen-oxytocin). Small-N imaging; suggestive
convergent evidence, not construct validation.

**Fisher, H. E., Island, H. D., Rich, J., Marchalik, D., & Brown, L. L. (2015). Four broad
temperament dimensions. *Frontiers in Psychology*, 6:1098.**
[DOI](https://doi.org/10.3389/fpsyg.2015.01098) → `fisher2015_four_temperament_dimensions.pdf`
The FTI validation paper: 56 items, four scales, correlated against the NEO. The dimensions
map substantially onto Big Five space (Curious/Energetic ≈ extraversion+openness, Cautious ≈
conscientiousness, Prosocial ≈ agreeableness), so incremental validity is limited. **Stated
plainly:** the FTI was developed *for* Chemistry.com/Match, its dyadic matching rules derive
largely from proprietary site data, and no independent peer-reviewed evidence shows
FTI-based matching predicts relationship outcomes. Useful as consumer-facing typology and
cold-start signal; not defensible as a predictive engine.

### 1.8 Joel, Eastwick & Finkel — the central result

**Joel, S., Eastwick, P. W., & Finkel, E. J. (2017). Is romantic desire predictable? Machine
learning applied to initial romantic attraction. *Psychological Science*, 28(10), 1478–1489.**
*(note: Psychological Science, not PNAS)*
[DOI](https://doi.org/10.1177/0956797617714580) ·
[PDF](http://pauleastwick.com/s/JoelEastwickFinkel2017PSci.pdf)
→ `joel2017_romantic_desire_predictable.pdf`

Two speed-dating studies, ~350 participants, >100 self-report trait and preference measures
each, fully crossed 4-minute dates. Random forests with proper out-of-sample validation plus
a Social Relations Model decomposition predicted **actor** variance and **partner** variance
at meaningful levels, but predicted **relationship variance — A's specific desire for B
above and beyond both main effects — at essentially zero out of sample**, even though it is
the *largest* variance component. The authors: romantic desire "may well be more like an
earthquake, involving a dynamic and chaos-like process, than a chemical reaction involving
the right combination of traits and preferences."

**Joel, S., Eastwick, P. W., Allison, C. J., et al. (2020). Machine learning uncovers the
most robust self-report predictors of relationship quality across 43 longitudinal couples
studies. *PNAS*, 117(32), 19061–19071.**
[DOI](https://doi.org/10.1073/pnas.1917036117) ·
[open preprint](https://research.gold.ac.uk/id/eprint/29101/1/preprint%20Joel%20et%20al%20Prediction%20Project%20PNAS%202020.pdf)
→ `joel2020_relationship_quality_ml.pdf`

43 longitudinal datasets, 11,196 couples, cross-validated random forests.
**Relationship-specific variables** (perceived partner commitment, appreciation, sexual
satisfaction, conflict) explain ~45% of current and ~18% of future satisfaction;
**individual-difference variables** (personality, attachment, life satisfaction) only ~21% /
~12%; and a partner's own traits add almost nothing once the actor's relationship
perceptions are known. Machine learning **did not beat simple main-effects regression** — no
interaction or "matching" effects were recovered.

### 1.9 Stated vs revealed preferences

**Eastwick, P. W., & Finkel, E. J. (2008). Sex differences in mate preferences revisited: Do
people know what they initially desire in a romantic partner? *JPSP*, 94(2), 245–264.**
[DOI](https://doi.org/10.1037/0022-3514.94.2.245) ·
[PDF](https://faculty.wcas.northwestern.edu/eli-finkel/documents/EastwickFinkel2008_JPSP.pdf)
→ `eastwick2008_stated_vs_revealed_preferences.pdf`
Classic sex differences appear reliably in *stated* ideals (men rate attractiveness higher,
women earning prospects), but **there were no sex differences in the associations between
stated ideals and actual romantic interest in live partners**, and stated ideals for an
attribute failed to predict interest as a function of that attribute in partners actually
met. Onboarding preference sliders are near-worthless as predictors of in-app choice.

**Finkel, E. J., & Eastwick, P. W. (2008). Speed-dating. *Current Directions in Psychological
Science*, 17(3), 193–197.**
[PDF](https://faculty.wcas.northwestern.edu/eli-finkel/documents/CDir_FinkelEastwick_FINAL.pdf)
→ `finkel2008_speeddating_methodology.pdf`
The methodological primer: why speed-dating yields real-time, fully-crossed dyadic data with
actual outcome stakes, and how the **Social Relations Model** decomposes ratings into
actor/partner/relationship components. This decomposition is the analytic frame the product
should adopt for its own metrics.

---

## 2. Dating-Industry and Speed-Dating Research

### 2.1 The definitive critical review

**Finkel, E. J., Eastwick, P. W., Karney, B. R., Reis, H. T., & Sprecher, S. (2012). Online
Dating: A Critical Analysis From the Perspective of Psychological Science. *Psychological
Science in the Public Interest*, 13(1), 3–66.**
[DOI](https://doi.org/10.1177/1529100612436522) ·
[PDF](https://faculty.wcas.northwestern.edu/eli-finkel/documents/2012_FinkelEastwickKarneyReisSprecher_PSPI.pdf)
→ `finkel2012_online_dating_pspi.pdf`

The single most important source for the product thesis. Three findings:

- **The access / communication / matching framework.** Online dating differs from
  conventional dating on exactly three dimensions. Access (exposure to a larger pool) is a
  genuine large benefit; communication (CMC before meeting) is a mixed benefit that becomes
  *harmful* past a modest threshold; matching is essentially unsupported.
- **Verdict on matching algorithms.** eHarmony's, Chemistry.com's and PerfectMatch's systems
  are judged "unlikely to work" as advertised. Claims rest on proprietary, unpublished,
  non-peer-reviewed analyses. Critically, the algorithms operate on *individual-difference*
  data gathered before any interaction, while the strongest predictors of relationship
  success (conflict-resolution patterns, sexual compatibility, stress and social support,
  life events) are **emergent properties of the dyad**, unmeasurable before the two people
  interact.
- **Why pre-meeting data fails.** Relationship variance is the consequential component and
  profile data does not predict it. The review also notes that a **modest** amount of
  pre-meeting CMC increases attraction while *extended* CMC decreases it (idealization
  collapses on first meeting) — an argument for getting people into live interaction fast,
  which is exactly the video speed-dating premise.

### 2.2 eHarmony's claims and rebuttals

**Carter, S. R., & Buckwalter, J. G. (2009). Enhancing mate selection through the Internet.
*Interpersona*, 3(Suppl. 2), 105–125.** *(cited-only — OA landing pages served HTML)*
[Journal](https://interpersona.psychopen.eu/index.php/interpersona/article/view/3297)
The core eHarmony-affiliated defense: eHarmony-matched couples reported higher
marital-adjustment scores than "unfettered" couples. Both authors were eHarmony-affiliated;
the design is cross-sectional and self-selected, so it cannot separate algorithm effect from
selection effect.

**Houran, J., Lange, R., Rentfrow, P. J., & Bruckner, K. H. (2004). Do online matchmaking
tests work? *North American Journal of Psychology*, 6(3), 507–526.** *(cited-only,
ProQuest paywall)*
The earliest independent critique: matchmakers' scientific claims are not referenced in
detail, full analyses are neither posted for customers nor offered publicly, and the
reanalysis suggested eHarmony couples were in some respects *more* dissimilar than controls
— the opposite of the similarity-matching claim. See also
[Houran & Lange on compatibility matching](https://www.scielo.org.mx/scielo.php?script=sci_arttext&pid=S2007-48322011000200002).

### 2.3 The Columbia speed-dating experiments

**Fisman, R., Iyengar, S. S., Kamenica, E., & Simonson, I. (2006). Gender Differences in Mate
Selection: Evidence From a Speed Dating Experiment. *Quarterly Journal of Economics*, 121(2),
673–697.**
[DOI](https://doi.org/10.1162/qjec.2006.121.2.673) ·
[PDF](https://business.columbia.edu/sites/default/files-efs/pubfiles/867/fisman%20iyengar.pdf)
→ `fisman2006_gender_differences_speeddating.pdf`
The experiment that produced the widely reused Columbia dataset (~21 waves, random partner
assignment, randomized variation in the *number* of partners). Because they observe each
individual yes/no rather than only realized matches, preferences are identified directly.
Men respond mainly to physical attractiveness; women weight intelligence and race more
heavily; men *discount* women whose intelligence or ambition exceeds their own. Female
selectivity rises with pool size — **choice set size itself changes revealed preference.**

**Fisman, R., Iyengar, S. S., Kamenica, E., & Simonson, I. (2008). Racial Preferences in
Dating. *Review of Economic Studies*, 75(1), 117–132.**
[DOI](https://doi.org/10.1111/j.1467-937X.2007.00465.x) ·
[PDF](https://sites.bu.edu/fisman/files/2015/11/RES08-racial_preferences.pdf)
→ `fisman2008_racial_preferences_dating.pdf`
Women exhibit strong same-race preference; men do not. Same-race preference increases with
own-race share in the subject's home ZIP code and is stronger among older and more
conservative subjects, but is **unrelated to the subject's stated importance of race**. See
also §5 — this racial preference is baked into the labels of the benchmark dataset most ML
papers train on.

### 2.4 Stated preferences do not predict actual choices

**Todd, P. M., Penke, L., Fasolo, B., & Lenton, A. P. (2007). Different cognitive processes
underlie human mate choices and mate preferences. *PNAS*, 104(38), 15011–15016.**
*(cited-only — PNAS, PMC and LSE endpoints all returned HTML)*
[PNAS](https://www.pnas.org/doi/10.1073/pnas.0705290104) ·
[LSE Research Online](https://eprints.lse.ac.uk/14711/)
In a real speed-dating event, stated ideal-partner criteria bore little relation to whom
participants actually chose. Choices were instead predicted by the chooser's *own* mate
value — people pursued partners of roughly matched desirability, consistent with an
aspiration-adjusting heuristic rather than a preference-satisfaction rule.

**Lenton, A. P., Penke, L., Todd, P. M., & Fasolo, B. The heart has its reasons: Social
rationality in mate choice.**
[PDF](http://www.larspenke.eu/pdfs/Lenton_Penke_Todd_Fasolo_in_press_-_Social_rationality_in_mate_choice.pdf)
→ `lenton2009_social_rationality_mate_choice.pdf` *(substitute for the Todd et al. PNAS
paper, restating the finding)*

**Kurzban, R., & Weeden, J. (2005). HurryDate: Mate preferences in action. *Evolution and
Human Behavior*, 26(3), 227–244.** *(cited-only, Elsevier paywall)*
[DOI](https://doi.org/10.1016/j.evolhumbehav.2004.08.012)
10,526 HurryDate participants, sessions of ~25 men and ~25 women in 3-minute rounds. Choices
were driven overwhelmingly by observable physical attributes assessable within seconds —
attractiveness, age, height, BMI — with almost no contribution from the interests, values
and background variables that questionnaire matching relies on.

**Kurzban, R., & Weeden, J. (2007). Do advertised preferences predict the behavior of speed
daters? *Personal Relationships*, 14(4), 623–632.**
[PDF](https://gwern.net/doc/sociology/2007-kurzban.pdf)
→ `kurzban2007_advertised_preferences_speeddaters.pdf`
The follow-up: daters' *advertised* preferences had essentially no predictive power over
their actual date-night choices.

**Lenton, A. P., & Francesconi, M. (2010). How humans cognitively manage an abundance of mate
options. *Psychological Science*, 21(4), 528–533.** *(cited-only, SAGE paywall)*
[DOI](https://doi.org/10.1177/0956797610364958)
Across 84 speed-dating events (1,868 women, 1,870 men), as options grew, choosers shifted
weight **away** from attributes that take time to elicit (occupation, education) and
**toward** attributes assessable at a glance (height, weight). Choice overload does not
merely reduce satisfaction — it *degrades the criteria people use*. Direct implication: a
small curated round of live dates should produce deeper-criteria selection than an infinite
swipe feed.

### 2.5 Revealed preferences at scale

**Hitsch, G. J., Hortaçsu, A., & Ariely, D. (2010). What makes you click? Mate preferences in
online dating. *Quantitative Marketing and Economics*, 8(4), 393–427.** (working paper: NBER
WP 11255)
[DOI](https://doi.org/10.1007/s11129-010-9088-6) ·
[NBER PDF](https://www.nber.org/system/files/working_papers/w11255/w11255.pdf)
→ `hitsch2005_what_makes_you_click_nber.pdf`
Estimates mate preferences from browsing and first-contact decisions on a major US site. No
evidence of strategic self-handicapping; strong similarity preferences on many attributes;
powerful same-race preferences users would not admit in surveys; steep gradients on physical
attractiveness and (for men's income) earnings. Profile-stage behavior is heavily driven by a
handful of coarse screenable attributes — the speed-dating conclusion at internet scale.

### 2.6 Consensus vs uniqueness of taste

**Eastwick, P. W., & Hunt, L. L. (2014). Relational mate value: Consensus and uniqueness in
romantic evaluations. *JPSP*, 106(5), 728–751.**
[PDF](https://pauleastwick.squarespace.com/s/EastwickHunt2014JPSP.pdf) ·
[PubMed](https://pubmed.ncbi.nlm.nih.gov/24611897/)
→ `eastwick2014_relational_mate_value.pdf`
Reconceives mate value as both *target variance* (consensus — everyone agrees this person is
desirable) and *relationship variance* (uniqueness). Among strangers consensus dominates;
as acquaintance lengthens **consensus shrinks and uniqueness grows**. A matching system
trained on aggregate desirability is really predicting the consensus component — exactly the
component that decays into irrelevance as a real relationship forms.

### 2.7 Industry sources — use with caution

**Rudder, C. — OkTrends blog (OkCupid, 2009–2014) and *Dataclysm* (Crown, 2014).**
*(cited-only; blog and trade book, no paper exists)*
[Archived OkTrends post](https://gwern.net/doc/psychology/okcupid/yourlooksandyourinbox.html)
Reported message-level regularities: men initiate at roughly 4:1; reply rate tracks the
sender's attractiveness rating nearly linearly, with top-rated men receiving ~11× the
messages of the lowest-rated; copy-pasted openers underperform bespoke ones by only ~25%
(and so are far more *efficient* per unit effort — an unflattering explanation of spam
dynamics); Black users, particularly Black women, receive systematically fewer messages and
lower ratings. Rudder also reported a handful of idiosyncratic questions (horror movies,
travel) predicting long-term-match agreement better than obvious ones. **Non-peer-reviewed,
internally analyzed, non-reproducible, single-platform with its own selection and UI
effects.** Useful as hypotheses about engagement mechanics; establishes nothing about
compatibility.

**Match Group / The Kinsey Institute — "Singles in America" (annual since 2011; Helen Fisher,
Justin R. Garcia; fielded by Dynata).** *(cited-only; press releases only)*
[2025 release](https://match.mediaroom.com/2025-06-10-Match-and-The-Kinsey-Institute-Unveil-14th-Annual-Singles-in-America-Study)
A large annual cross-sectional survey of US singles 18–98, sampled to represent the single
population and explicitly *not* Match's users. **Establishes:** descriptive prevalence and
year-over-year trends in attitudes and behavior — useful for market sizing and for naming
emergent behaviors (app fatigue, "slow dating," video-date adoption). **Does not establish:**
anything predictive. It is sponsor-funded marketing research released by press release; the
instrument, weighting and microdata are unpublished; it is cross-sectional; and it measures
*stated* attitudes, which §2.4 shows diverge sharply from choice. Cite for market context
only.

---

## 3. Thin Slices, Nonverbal Synchrony, Prosody, and Linguistic Style Matching

### 3.1 Thin slices — how much signal is in a few minutes?

**Ambady, N., & Rosenthal, R. (1992). Thin slices of expressive behavior as predictors of
interpersonal consequences: A meta-analysis. *Psychological Bulletin*, 111(2), 256–274.**
*(cited-only, APA paywall)* [DOI](https://doi.org/10.1037/0033-2909.111.2.256)
The foundational result for this whole product category: across 38 effect sizes where naive
raters judged clips under 300 seconds, mean predictive accuracy against objective criteria
was **r = .39**. Slices under 30 seconds performed no worse than 4–5 minute slices, and clips
containing face **plus body** outperformed face-only. Implication for a 3–5 minute video
date: the observable window is already at or past diminishing returns for thin-slice signal —
more minutes buys less than better features.

**Murphy, N. A., & Hall, J. A. (2021). Capturing behavior in small doses: A review of
comparative research in evaluating thin slices for behavioral measurement. *Frontiers in
Psychology*.** *(cited-only; readable at
[PMC8116694](https://pmc.ncbi.nlm.nih.gov/articles/PMC8116694/))*
The limits paper. Thin-slice reliability varies sharply by construct — affect and
expressivity slice well; stable traits, intentions and future behavior slice poorly — and
"accuracy" claims are often tested against chance rather than a meaningful absolute standard,
so a significant coefficient can still be small. Moderators: culture, rater expertise,
in-group membership, slice location within the interaction. Treat r = .39 as an upper-bound
average over favorable constructs.

### 3.2 Prosody and interactional stance in actual speed dates — highest-value cluster

**Ranganath, R., Jurafsky, D., & McFarland, D. A. (2013). Detecting friendly, flirtatious,
awkward, and assertive speech in speed-dates. *Computer Speech & Language*, 27(1), 89–115.**
[DOI](https://doi.org/10.1016/j.csl.2012.01.005) ·
[PDF](https://web.stanford.edu/~jurafsky/pubs/ranganath2013.pdf)
→ `ranganath2013_flirtatious_speech_speeddates.pdf`

The closest existing analogue to this product. 1,000+ four-minute speed dates, each side self-
and partner-rated on four stances; SVM over lexical + prosodic + dialog-act features reaches
**up to 78% vs a 50% baseline on prototype deciles for seen speakers, but 53% vs a 37%
baseline for unseen speakers** — the generalization cliff is the number to plan around.
Signals:

- **Flirtation in women:** negation (teasing/self-deprecation), *like*, *I*, collaborative
  style (appreciations, medial laughter).
- **Flirtation in men:** *you*, *you know*, *um*, sex-related words, less work talk.
- **Friendliness:** other-directed laughter, appreciations, higher/later F0, faster speech,
  more backchannels.
- **Awkwardness:** reduced speaker involvement — fewer turns, less laughter.
- *um* marks flirting for both sexes; *uh* does the opposite.
- Accommodation effects were partner-side, not self-side: men accommodated more to
  flirtatious/friendly women.

**Ranganath, R., Jurafsky, D., & McFarland, D. (2009). It's not you, it's me: Detecting
flirting and its misperception in speed-dates. *EMNLP 2009*, 334–342.**
[ACL Anthology](https://aclanthology.org/D09-1035/) → `ranganath2009_detecting_flirting.pdf`
Exploits the fact that both speaker and listener rated the speaker's flirtatiousness,
separating *intent* from *perception*. An **autoencoder compressing sparse lexical vectors to
30 dense features** helps against small-data sparsity; reaches **71.5% accuracy on detecting
intended flirtation — above the human interlocutor's own judgment.** Headline for product
design: humans are poor perceivers of intended flirtation and largely **project their own
intent** onto the partner, so self-report "did they like me" labels are systematically noisy.

**Jurafsky, D., Ranganath, R., & McFarland, D. (2009). Extracting social meaning: Identifying
interactional style in spoken conversation. *NAACL-HLT 2009*, 638–646.**
[ACL Anthology](https://aclanthology.org/N09-1072/) →
`ranganath2009_extracting_social_meaning.pdf`
The concrete feature spec to copy: prosodic (F0 min/max/mean/SD, within- and across-turn
pitch variance, RMS energy, turn duration, speaking rate), dialog-act (backchannel rate,
questions — especially *appreciations* and "sympathetic negatives" — laughter counts, filled
pauses, overlap, turn-taking latency), and LIWC-grouped lexical unigrams. ~75% accuracy vs a
50% balanced baseline. The real contribution is interpretive: **the same behavior means
different things by gender.**

**McFarland, D. A., Jurafsky, D., & Rawlings, C. (2013). Making the connection: Social bonding
in courtship situations. *American Journal of Sociology*, 118(6), 1596–1649.**
[DOI](https://doi.org/10.1086/670240) ·
[PDF](https://nlp.stanford.edu/pubs/mcfarlandjurafskyrawlings.pdf)
→ `mcfarland2013_making_the_connection.pdf`

Over 2,000 reports of "clicking," modeled dyadically (APIM). **Traits explain ~15% of
variance in clicking; speech features add another 7.5% net of traits**, and the effect
**grows with each additional minute** — first-minute-only models are much weaker. Gendered
signals: men feel connection when they **laugh, vary loudness, and reduce pitch variance**;
women when they **raise and vary pitch, speak softer with variable loudness, and take shorter
turns**. Women feel connection when they are the **topical focus** (*I*, self-markers) and
the man shows alignment (appreciations, sympathy, *you*); **hedges signal misalignment** and
predict *not* clicking. Net: successful dates show a reciprocal *asymmetric* pattern —
female-focused topic, male-demonstrated understanding.

### 3.3 Linguistic style matching

**Ireland, M. E., Slatcher, R. B., Eastwick, P. W., Scissors, L. E., Finkel, E. J., &
Pennebaker, J. W. (2011). Language style matching predicts relationship initiation and
stability. *Psychological Science*, 22(1), 39–44.**
[DOI](https://doi.org/10.1177/0956797610392928) ·
[PDF](https://sites.socsci.uci.edu/~lpearl/courses/readings/IrelandEtAl2011_RelationshipPrediction.pdf)
→ `ireland2011_language_style_matching.pdf`

Directly implementable and speed-dating-based. LSM = similarity of **function-word usage**
(pronouns, articles, prepositions, conjunctions, auxiliary verbs, negations, quantifiers,
adverbs) across nine LIWC categories, computed per category as `1 − |a−b|/(a+b+ε)` and
averaged. **Study 1:** in transcripts of 40 speed dates, higher LSM predicted mutual romantic
interest, **OR = 3.05** — 33.3% of above-median-LSM pairs mutually wanted contact vs 9.1%
below median. **Study 2:** LSM in 86 couples' IMs predicted still dating at 3 months,
**OR = 1.95** (76.7% vs 53.5%). Cheap to compute from a transcript, no acoustics needed, and
it is a **dyadic** metric — which fits a matching product better than per-person scores.

### 3.4 Nonverbal synchrony, mimicry, and posture

**Chartrand, T. L., & Bargh, J. A. (1999). The chameleon effect: The perception–behavior link
and social interaction. *JPSP*, 76(6), 893–910.** *(cited-only, APA paywall)*
[DOI](https://doi.org/10.1037/0022-3514.76.6.893)
The mechanism paper behind synchrony-as-rapport. Experiment 2 is load-bearing: confederates
who **mimicked** participants' mannerisms produced significantly higher liking and
smoother-interaction ratings — mimicry *causes* rapport rather than merely accompanying it.
Mimicry is nonconscious and automatic, which is why it survives as a signal even when people
are performing for a camera. (1999-era social psych with small cells; direction solid,
magnitude uncertain.)

**Ramseyer, F., & Tschacher, W. (2011). Nonverbal synchrony in psychotherapy: Coordinated body
movement reflects relationship quality and outcome. *JCCP*, 79(3), 284–295.** *(cited-only,
APA paywall)* [DOI](https://doi.org/10.1037/a0023419)
**The method to copy for video: Motion Energy Analysis (MEA).** Frame-differencing within
fixed regions of interest on a stationary two-person video yields per-person motion time
series; windowed cross-correlation with time lags (±5s), aggregated and compared against
pseudo-synchrony surrogate controls, gives a synchrony score. Synchrony above chance
predicted self-reported relationship quality and outcome. Directly transferable to a two-tile
video call layout, and it needs **no pose estimation**.

**Ramseyer, F., & Tschacher, W. (2014). Nonverbal synchrony of head- and body-movement in
psychotherapy: Different signals have different associations with outcome. *Frontiers in
Psychology*, 5:979.**
[DOI](https://doi.org/10.3389/fpsyg.2014.00979) →
`ramseyer2014_nonverbal_synchrony_head_body.pdf`
Important refinement: head and body synchrony are **not interchangeable** — head-movement
synchrony tracked relationship/bond ratings while body synchrony tracked symptom outcome. For
a webcam product where the head is the only reliably visible region, this is the encouraging
result: **head-region MEA is the rapport-relevant channel.**

**Grammer, K., Honda, M., Jüette, A., & Schmitt, A. (1999). Fuzziness of nonverbal courtship
communication unblurred by motion energy detection. *JPSP*, 77(3), 487–508.** *(cited-only,
APA paywall)* [DOI](https://doi.org/10.1037/0022-3514.77.3.487)
Pioneered motion-energy quantification of opposite-sex first encounters. Individual courtship
cues are ambiguous one at a time, but **aggregate movement quantity and its temporal
patterning** disambiguate interest: female movement/signaling *rate* correlated strongly with
the male partner's reported interest. Supports a continuous synchrony/energy feature over a
discrete gesture-detector taxonomy.

**Vacharkulksemsuk, T., Reit, E., Khambatta, P., Eastwick, P. W., Finkel, E. J., & Carney,
D. R. (2016). Dominant, open nonverbal displays are attractive at zero-acquaintance. *PNAS*,
113(15), 4009–4014.** *(cited-only, Cloudflare-blocked)*
[DOI](https://doi.org/10.1073/pnas.1508932113)
Postural **expansiveness** is the strongest coded nonverbal predictor of a "yes" — in 144 live
speed-dates each 1 SD increase in coded expansiveness raised the odds of a yes by **76%
(OR ≈ 1.76)**, outperforming smiling and nodding. A dating-app field experiment (2,983
potential yeses, 6 confederates × expansive/contracted photos) replicated causally at
**OR ≈ 1.27**. Caveat: the seated, torso-cropped webcam frame compresses exactly the postural
range this effect lives in, and the study is small-n from the power-posing lineage — treat as
a hypothesis to validate on your own data.

### 3.5 Turn-taking, questions, and laughter

**Huang, K., Yeomans, M., Brooks, A. W., Minson, J., & Gino, F. (2017). It doesn't hurt to
ask: Question-asking increases liking. *JPSP*, 113(3), 430–452.**
[DOI](https://doi.org/10.1037/pspi0000097) ·
[PDF](https://www.hbs.edu/ris/Publication%20Files/Huang%20et%20al%202017_6945bc5e-3b3e-4c0a-addd-254c9e603c60.pdf)
→ `huang2017_question_asking_liking.pdf`

The single most actionable coachable signal. Across three studies of live dyads,
question-asking — specifically **follow-up questions**, which signal responsiveness —
causally increases partner liking, with responsiveness as the statistical mediator. Study 3
is a **face-to-face speed-dating field study** where the authors trained an NLP
**follow-up-question detector** and showed higher follow-up-question rates significantly
predicted second-date offers. Bonus: people **do not anticipate** that asking questions makes
them more liked, so surfacing this is genuinely novel feedback rather than something users
already know.

Laughter and backchannels are best sourced from the Stanford cluster above: other-directed
and medial laughter are among the strongest friendliness/flirtation markers (Ranganath et al.
2013), laughter counts are a core excitement feature predicting clicking for men (McFarland
et al. 2013), and backchannel frequency correlates with wanting to be friends with a partner.

### 3.6 Vocal pitch and vocal accommodation

**Puts, D. A., Barndt, J. L., Welling, L. L. M., Dawood, K., & Burriss, R. P. (2011).
Intrasexual competition among women: Vocal femininity and flirtatiousness. *Personality and
Individual Differences*, 50(1), 111–115** (and Puts et al. 2007, *Evolution and Human
Behavior*). *(cited-only, Elsevier paywall)*
[DOI](https://doi.org/10.1016/j.paid.2010.09.011)
Lowered male F0 drives perceived physical **dominance** more than attractiveness, with
negative curvilinear as well as linear relationships between male F0 and female attractiveness
ratings; raised and more variable female F0 tracks perceived femininity and flirtatiousness.
Worth flagging that Ranganath et al. 2013 did **not** reproduce the predicted F0-max increase
for *self-reported* female flirtation — they found it only for *partner-perceived*
flirtation. Pitch is a perception signal more than an intention signal.

**Hughes, S. M., Farley, G., & Rhodes, B. C. (2010). Vocal and physiological changes in
response to the physical attractiveness of conversational partners. *Journal of Nonverbal
Behavior*, 34(3), 155–167.** *(cited-only, Springer paywall)*
[DOI](https://doi.org/10.1007/s10919-010-0087-9)
The most directly useful vocal-*change* result: both men and women shifted to a
**lower-pitched voice** and showed **elevated physiological arousal** when speaking to a more
attractive opposite-sex partner. This is a within-person, within-call delta — measurable
without cross-person normalization, making it unusually robust to microphone and
individual-baseline variation. Related: interpersonal physiological synchrony is a real signal
but requires wearables and is not extractable from video; vocal-arousal proxies are the
accessible substitute.

---

## 4. AI / NLP / ML Prediction of Attraction and Compatibility

### 4.1 Multimodal and nonverbal prediction of speed-dating outcomes

**Veenstra, A., & Hung, H. (2011). Do they like me? Using video cues to predict desires during
speed-dates. *ICCV Workshops*, 838–845.** *(cited-only, IEEE paywall)*
[IEEE](https://ieeexplore.ieee.org/document/6130340)
Purely visual, appearance-free cues — body position, interpersonal proximity/lean, motion
energy — aggregated into statistical descriptors and fed to SVMs to predict self-reported
attraction and contact-exchange decisions. Accuracies are modest (~60s%) but well above
chance. The standard demonstration that **movement alone carries attraction signal**.

**Bilakhia, S., Petridis, S., & Pantic, M. (2013). Audiovisual detection of behavioural
mimicry. *ACII 2013*.**
[PDF](https://ibug.doc.ic.ac.uk/media/uploads/documents/bilakhiapetridispantic_acii2013.pdf)
→ `bilakhia2013_audiovisual_mimicry_detection.pdf`
Detects mimicry episodes from facial-point tracking plus prosody using time-lagged cross-modal
models. Establishes the windowed-cross-correlation-at-candidate-lags methodology most later
synchrony work reuses.

**Bilakhia, S., Petridis, S., Nijholt, A., & Pantic, M. (2015). The MAHNOB Mimicry Database.
*Pattern Recognition Letters*, 66, 52–61.** *(cited-only, Elsevier paywall)*
[Database](https://mahnob-db.eu/mimicry/) — 11 hours / 54 sessions of synchronized
multi-sensor dyadic audio-video annotated for mimicry episodes. Not romantic, but the
reference corpus for behavioral mimicry/synchrony detection. Free for research under EULA.

**Kikuchi, Hayashi, Kimura, Inoue, Ishii & Okada (2026). Speech signals complement LLMs for
predicting interpersonal attraction in speed dating. *ICMI 2026*.**
[arXiv:2607.23037](https://arxiv.org/abs/2607.23037) →
`arxiv2026_speech_llm_speeddating_attraction.pdf`
The most directly on-point recent paper. On Japanese speed-dating conversations they compare a
**transcript-only LLM predictor**, a **supervised speech (paralinguistic) predictor**, and
their fusion. Fusion improves pairwise *ranking* accuracy across all conditions, but
per-participant correlation gains were **not statistically significant after
multiple-comparison correction** — speech complements text *conditionally*, mainly for the
subset of participants where the acoustic model is already stronger. Sobering evidence that
audio is not a free lift over transcripts.

**Hayashi, Okada et al. Multimodal Speed Dating Dataset (MMSD). *HCII 2025 Late Breaking
Papers* (Springer, 2026).** *(cited-only, Springer paywall)*
[Springer](https://link.springer.com/chapter/10.1007/978-3-032-12801-0_3)
1,250 dyadic speed-date interactions, 147 Japanese participants, synchronized audio/video/
transcripts, profile data, **33 psychometric scales**, and impression ratings ("love" and
"like") at **four time points during each date** plus final mutual-contact decisions. The
modern successor to the Stanford SDC and the richest multimodal romantic-outcome corpus in
existence.

**Kimura et al. (2025). What timing and behavior patterns determine speed dating success in
Japan? *CHI 2025 Extended Abstracts*.** *(cited-only, ACM paywall)*
[ACM DL](https://dl.acm.org/doi/10.1145/3706599.3720028)
Uses the four-timepoint MMSD ratings to show **when** during a date impressions crystallize —
practically important for deciding how long a call must run before a prediction is
trustworthy.

### 4.2 Rapport and engagement modeling — the transferable stack

**ACII 2026 Dyadic Conversations (DaiKon) Workshop & Challenge.**
[arXiv:2605.02672](https://arxiv.org/abs/2605.02672) →
`daikon2026_dyadic_conversations_challenge.pdf`
Defines a shared task for **continuous rapport estimation** from dyadic audio-video.
Baselines encode windowed multimodal descriptors (768-D audio, 1024-D video, 1792-D fused)
through shared MLP encoders to a scalar rapport score; test performance is **0.40 CCC / 0.50
Pearson for audio and multimodal, versus only 0.19 CCC for video-only**. Two takeaways:
**audio dominates video for rapport**, and even the best systems explain well under half the
variance. The current benchmark to build against.

**Li et al. (2024). DAT: Dialogue-aware transformer with modality-group fusion for human
engagement estimation. *MultiMediate'24 / ACM MM 2024*.**
[arXiv:2410.08470](https://arxiv.org/abs/2410.08470) → `li2024_dat_engagement_estimation.pdf`
Transformer fusing per-modality groups (audio, visual, pose) and explicitly conditioning on
*the partner's* behavior stream; won the MultiMediate engagement challenge. The
"modality-group fusion + dialogue-awareness" architecture is the sensible default for a
two-person video pipeline.

**Lee, Yun et al. (2023). HIINT: Historical, intra- and inter-personal dynamics modeling with
cross-person memory transformer.**
[arXiv:2305.12369](https://arxiv.org/abs/2305.12369) → `lee2023_hiint_cross_person_memory.pdf`
Cross-person memory tokens let a transformer model how each speaker's state is driven by the
other's history — the architectural answer to attraction being a **dyadic**, not individual,
property.

### 4.3 LLMs applied directly to romantic attraction

**Matz, S., Peters, H., Cerf, M., Grunenberg, E., Eastwick, P. W., Back, M., & Finkel, E. J.
(2024/2026). Large language models can detect verbal indicators of romantic attraction.**
[arXiv:2407.10989](https://arxiv.org/abs/2407.10989) · *Scientific Reports* (2026),
[doi:10.1038/s41598-026-52308-x](https://www.nature.com/articles/s41598-026-52308-x)
→ `matz2025_llm_verbal_romantic_attraction.pdf`

**964 speed dates.** ChatGPT and Claude 3 are prompted on raw transcripts to predict both
subjective attraction ratings and objective match outcomes, with a Brunswik-lens analysis of
which linguistic cues drive the model. Predictive correlations are **r = 0.12–0.23** — low in
absolute terms, but **on par with human judges**, **incremental to the speed daters' own
predictions**, with LLM-vs-human judgment overlap at r = 0.21–0.35. The right framing: an LLM
adds signal a person doesn't have, while remaining a weak predictor in absolute terms.

**Love first, know later: Persona-based romantic compatibility through LLM text world engines
(2025).** [arXiv:2512.11844](https://arxiv.org/abs/2512.11844) →
`2025_love_first_know_later_llm_compatibility.pdf`
Inverts the standard pipeline: instead of scoring static profiles it instantiates LLM persona
agents, **simulates the conversation first**, then scores compatibility on the simulated
interaction. Validated on speed-dating data (initial chemistry) and divorce-prediction data
(long-term stability). Relevant if you ever want to pre-screen pairings before spending real
user minutes, though simulated-conversation validity is the obvious open question.

### 4.4 Reciprocal recommendation for online dating

**Pizzato, L., Rej, T., Chung, T., Koprinska, I., & Kay, J. (2010). RECON: A reciprocal
recommender for online dating. *RecSys 2010*, 207–214.** *(cited-only, ACM paywall)*
[ACM DL](https://dl.acm.org/doi/10.1145/1864708.1864747)
The founding paper. Builds explicit *and* implicit preference profiles per user from message
history, scores candidate pairs **in both directions**, and harmonically combines them.
Evaluated on a large commercial Australian site: reciprocal scoring materially raises the
**success rate** (positive reply to a first contact) over one-sided content-based
recommendation. The core lesson — optimize for mutual acceptance, not one-sided click
probability — is non-negotiable.

**Xia, P., Liu, B., Sun, Y., & Chen, C. (2015). Reciprocal recommendation system for online
dating.** [arXiv:1501.06247](https://arxiv.org/abs/1501.06247) →
`xia2015_reciprocal_recommendation_dating.pdf`
Learns preferences from interaction (message/reply) **graphs** rather than stated profile
filters, using similarity-based collaborative filtering with a reciprocal fusion step.
Establishes that behavioral preference beats stated preference — the same gap Eastwick &
Finkel found psychologically.

**Neve, J., & Palomares, I. (2019). Latent factor models and aggregation operators for
collaborative filtering in reciprocal recommender systems. *RecSys 2019*, 219–227.**
*(cited-only, ACM paywall)* [ACM DL](https://dl.acm.org/doi/10.1145/3298689.3347026)
Replaces heuristic reciprocal scoring with matrix-factorization latent factors and compares
**aggregation operators** (harmonic mean, arithmetic mean, min, OWA) for combining the two
directional scores. **Harmonic mean and min-like operators dominate because they punish
asymmetry.** The practical recipe for implementing reciprocity on top of any embedding model.

**Palomares, I., Porcel, C., Pizzato, L., Guy, I., & Herrera-Viedma, E. (2021). Reciprocal
recommender systems: Analysis of state-of-art literature, challenges and opportunities.
*Information Fusion*, 69, 298–333.**
[arXiv:2007.16120](https://arxiv.org/abs/2007.16120) →
`palomares2021_reciprocal_recsys_survey.pdf`
The definitive survey: taxonomy across dating, recruitment and mentoring; a unified processing
pipeline; and a catalogue of open problems (two-sided cold start, congestion/popularity
concentration, evaluation metrics that reward one-sided relevance, ethics).

**Tomita, Y., Togashi, R., & Moriwaki, D. (2022). Matching theory-based recommender systems in
online dating. *RecSys 2022* industry track.**
[arXiv:2208.11384](https://arxiv.org/abs/2208.11384) →
`tomita2022_matching_theory_dating_recsys.pdf`
Frames matching as a **two-sided market / deferred-acceptance** problem rather than a ranking
problem, to combat **congestion** (everyone recommended to the same few popular users).
Deployed at a Japanese dating service; reports improved match rates and better distribution of
attention.

**Narita et al. (2025). Counterfactual reciprocal recommender systems for user-to-user
matching.** [arXiv:2508.01867](https://arxiv.org/abs/2508.01867) →
`narita2025_counterfactual_reciprocal_recsys.pdf`
Off-policy/counterfactual estimation correcting the exposure bias that makes offline
evaluation of dating recommenders systematically misleading. Important before A/B or offline
evaluation of a matching policy.

**Kleinerman, A., Rosenfeld, A., Ricci, F., et al. CCR: A content-collaborative reciprocal
recommender. *IJCAI*.** [PDF](https://www.ijcai.org/Proceedings/11/Papers/367.pdf) →
`kleinerman2018_ccr_reciprocal.pdf` — hybrid content + CF reciprocal baseline; useful
comparison point.

### 4.5 Ethics, fairness, and critique of algorithmic matchmaking

**Zheng et al. (2024). Leveraging opposite gender interaction ratio as a path towards fairness
in online dating recommendations based on user sexual orientation. *AAAI 2024*.**
[arXiv:2402.12541](https://arxiv.org/abs/2402.12541) →
`zheng2024_fairness_dating_recommendations.pdf`
Shows dating recommenders systematically underserve users whose interaction patterns deviate
from the majority sexual-orientation pattern, and proposes interaction-ratio re-weighting that
improves fairness at small utility cost.

**Hutson, J. A., Taft, J. G., Barocas, S., & Levy, K. (2018). Debiasing desire: Addressing
bias & discrimination on intimate platforms. *Proc. ACM CSCW*, 2:73.** *(cited-only, ACM)*
[ACM DL](https://dl.acm.org/doi/10.1145/3274342)
The canonical ethics paper: intimate platforms are not neutral, "preference" is not a defense
when design amplifies it, and it catalogues concrete interventions (removing race filters,
changing what is shown first, altering ranking).

**Zhao et al. (2022). Not just a preference: Reducing biased decision-making on dating
websites. *CHI 2022*.** *(cited-only, ACM)*
[ACM DL](https://dl.acm.org/doi/fullHtml/10.1145/3491102.3517587)
Experimental evidence that **presentation order matters**: showing self-identified important
attributes *before* race-related information measurably reduces anti-Black bias in choices.

**Paraschakis, D., & Nilsson, B. J. (2020). Matchmaking under fairness constraints: A speed
dating case study. *BIAS@ECIR 2020*.** *(cited-only, Springer)*
[Springer](https://link.springer.com/chapter/10.1007/978-3-030-52485-2_5)
Applies fairness constraints directly to the Fisman/Iyengar speed-dating data and quantifies
the fairness/accuracy trade-off.

> **Label-contamination warning.** Fisman et al. (2008) documents strong same-race preference
> in the Columbia corpus itself — i.e. **the benchmark dataset most ML papers train on has
> racial preference baked into its labels.** Any model trained to predict `match` on it will
> learn and reproduce that.

---

## 5. Available datasets

| Dataset | Contents | Modalities | Access |
|---|---|---|---|
| **Fisman & Iyengar Speed Dating Experiment** (Columbia, 2002–04) | 8,378 dyad-rows, 121 features, 551 participants; six-attribute ratings, stated preferences, decisions, `match` label | Tabular self-report only | **Fully public** — [Kaggle](https://www.kaggle.com/datasets/annavictoria/speed-dating-experiment), [OpenML 40536](https://www.openml.org/d/40536) |
| **Stanford Speed Dating Corpus (SDC)** — McFarland/Jurafsky | 991 four-minute dates, full transcripts + force-aligned audio, self & other ratings of friendly/awkward/assertive/flirtatious, pre/post surveys | Audio + transcript | **Restricted** — request from authors; [project page](https://nlp.stanford.edu/projects/social.shtml) |
| **MMSD — Multimodal Speed Dating Dataset** (JAIST, 2025/26) | 1,250 dyadic dates, 147 participants, impression ratings at 4 timepoints, 33 psychometric scales, mutual-contact outcomes | **Audio + video + transcript** | **By request** to authors |
| **MAHNOB Mimicry Database** | 11h / 54 sessions dyadic interaction, mimicry annotations | Audio + multi-view video + physiological | Free for research under EULA — [mahnob-db.eu/mimicry](https://mahnob-db.eu/mimicry/) |
| **DaiKon (ACII 2026) rapport challenge** | Dyadic conversations, continuous rapport annotations, published baselines (0.40 CCC) | Audio + video | Challenge registration — [arXiv:2605.02672](https://arxiv.org/abs/2605.02672) |
| **UDIVA** | 188 dyadic sessions, ~90h, self-reports + personality labels | Audio + video + HRV | Free for research — [arXiv:2012.14259](https://arxiv.org/abs/2012.14259) |
| **MultiMediate / NoXi** | Dyadic engagement/backchannel annotations | Audio + video | Free for research |
| **HurryDate** (Kurzban & Weeden) | ~10,500 speed-date decisions, physical/demographic attributes | Tabular | Via authors |

**Practical read:** only the Kaggle/Columbia set is truly drop-in public, and it has no speech
or video at all — plus severe post-date **leakage** columns (`attr_o`, `like_o`, `dec_o` are
recorded after the date and essentially encode the decision; honest pre-date-only models drop
far closer to chance) and the racial-preference contamination noted above. Every corpus with
real conversational audio-video *and* romantic outcome labels (SDC, MMSD) is access-controlled.
The realistic path: pretrain rapport/engagement/synchrony models on the freely available
non-romantic dyadic corpora (MAHNOB Mimicry, UDIVA, MultiMediate, DaiKon), then fine-tune on
consented in-product data — which will quickly become a better corpus than anything published.

---

## 6. Implications for the videodating product

### 6.1 What to measure — proposed v1 feature set

The cheapest high-value signals are all **transcript-side and dyadic**, requiring no audio
model, no pose estimation, and no per-user calibration:

| Feature | Source | Reported effect |
|---|---|---|
| **Language style matching** (9 LIWC function-word categories) | Ireland et al. 2011 | OR = 3.05 for mutual interest |
| **Follow-up question rate** | Huang et al. 2017 | Causal; predicts second-date offers |
| **Appreciations / sympathetic negatives** | Jurafsky et al. 2009 | Core friendliness marker |
| **Laughter counts** (other-directed, medial) | Ranganath 2013; McFarland 2013 | Friendliness + male clicking |
| **Pronoun targeting** (`I` / `you` asymmetry) | McFarland et al. 2013 | Female clicking via topical focus |
| **Hedge rate** (negative signal) | McFarland et al. 2013 | Predicts *not* clicking |
| **Turn balance, backchannel rate** | Jurafsky et al. 2009 | Involvement / awkwardness |

**v2 (audio):** F0 statistics and within-turn pitch variance, speaking rate, RMS energy,
filled-pause type (*um* vs *uh*), and the within-call **vocal pitch delta** (Hughes et al.
2010) — robust to microphone variation because it is a within-person change.

**v3 (video):** head-region **Motion Energy Analysis** synchrony (Ramseyer & Tschacher 2014),
windowed cross-correlation at ±5s lags against pseudo-synchrony surrogate controls. Head
region specifically, since that is both the rapport-relevant channel and the reliably visible
one on a webcam.

### 6.2 Modeling constraints, non-negotiable

1. **Decompose with the Social Relations Model** (Finkel & Eastwick 2008) into actor / partner
   / relationship variance from day one. Publishing an aggregate accuracy number without this
   decomposition hides whether the model has learned anything beyond "who is generally
   desirable."
2. **Speaker-disjoint validation.** Ranganath's 78% → 53% cliff is what happens otherwise.
3. **Report base-rate-adjusted PPV on a holdout.** Match base rates are ~16% in the Columbia
   data; accuracy against a majority-class baseline is meaningless.
4. **Gender-conditional models.** Every conversation-signal paper here found the same behavior
   means different things by gender. A single pooled model averages away the signal.
5. **Reciprocal scoring with an asymmetry-punishing aggregator** (harmonic mean or min), not
   one-sided ranking — and watch for congestion on popular users.
6. **Expect a ceiling.** In-conversation models top out around r ≈ 0.2–0.5 / 70–75% balanced
   accuracy. Design the UX around ranking and surfacing, not around confident prediction.

### 6.3 Design opportunities the literature directly supports

- **Script escalating reciprocal self-disclosure.** Aron et al. 1997 shows closeness is a
  manipulable property of the *prompt structure*. This raises baseline connection for
  everyone, independent of any matching model — likely the highest-leverage single feature.
- **Keep choice sets small.** Lenton & Francesconi: large option sets shift people *toward*
  glanceable attributes (height, weight) and away from ones that take time to elicit. A
  curated round of live dates should produce better-criteria selection than an infinite feed.
- **Get to live interaction fast.** Finkel et al. 2012: modest pre-meeting CMC helps, extended
  CMC hurts (idealization collapses on first meeting).
- **Surface perceived similarity, don't just compute actual similarity.** Tidwell et al. 2013:
  perceived similarity predicts liking; actual similarity does not. Making existing overlap
  salient during the call may matter more than optimizing the pairing.
- **Coach the follow-up question.** Huang et al. 2017 found people genuinely do not know this
  works — rare, actionable, novel feedback.
- **Feedback on misperception.** Ranganath et al. 2009: people project their own intent onto
  their partner and are poor at reading intended flirtation. "How you came across vs what you
  intended" is a defensible product surface — and a warning that self-report labels are noisy.

### 6.4 Claims to avoid making

Given Finkel et al. 2012, Joel et al. 2017/2020, and the eHarmony critique history, the
product should **not** claim to predict compatibility from profiles or questionnaires. That
claim is well-documented as unsupported, and the critical literature is prominent enough that
making it invites exactly the treatment eHarmony received. The defensible claim is narrower
and more interesting: *we measure what actually happened in the conversation.*

---

## Appendix: download status

**39 PDFs saved and verified** in [`papers/`](papers/):

`2025_love_first_know_later_llm_compatibility.pdf`, `arxiv2026_speech_llm_speeddating_attraction.pdf`,
`bahns2017_similarity_niche_construction.pdf`, `bilakhia2013_audiovisual_mimicry_detection.pdf`,
`brown2013_neural_correlates_fti.pdf`, `daikon2026_dyadic_conversations_challenge.pdf`,
`eastwick2008_stated_vs_revealed_preferences.pdf`, `eastwick2014_relational_mate_value.pdf`,
`finkel2008_speeddating_methodology.pdf`, `finkel2012_online_dating_pspi.pdf`,
`fisher2015_four_temperament_dimensions.pdf`, `fisman2006_gender_differences_speeddating.pdf`,
`fisman2008_racial_preferences_dating.pdf`, `gottman1992_marital_processes_dissolution.pdf`,
`gottman1999_theory_marital_dissolution.pdf`, `hitsch2005_what_makes_you_click_nber.pdf`,
`huang2017_question_asking_liking.pdf`, `ireland2011_language_style_matching.pdf`,
`joel2017_romantic_desire_predictable.pdf`, `joel2020_relationship_quality_ml.pdf`,
`kleinerman2018_ccr_reciprocal.pdf`, `kurzban2007_advertised_preferences_speeddaters.pdf`,
`lee2023_hiint_cross_person_memory.pdf`, `lenton2009_social_rationality_mate_choice.pdf`,
`li2024_dat_engagement_estimation.pdf`, `matz2025_llm_verbal_romantic_attraction.pdf`,
`mcfarland2013_making_the_connection.pdf`, `montoya2008_actual_perceived_similarity_meta.pdf`,
`narita2025_counterfactual_reciprocal_recsys.pdf`, `neyer2001_personality_relationship_transaction.pdf`,
`palomares2021_reciprocal_recsys_survey.pdf`, `ramseyer2014_nonverbal_synchrony_head_body.pdf`,
`ranganath2009_detecting_flirting.pdf`, `ranganath2009_extracting_social_meaning.pdf`,
`ranganath2013_flirtatious_speech_speeddates.pdf`, `tidwell2013_perceived_similarity_speeddating.pdf`,
`tomita2022_matching_theory_dating_recsys.pdf`, `xia2015_reciprocal_recommendation_dating.pdf`,
`zheng2024_fairness_dating_recommendations.pdf`

**Cited-only** (paywalled, access-controlled, or no PDF exists): Byrne 1971; Winch 1958;
Montoya & Horton 2013; Dijkstra & Barelds 2008; Hazan & Shaver 1987; Li & Chan 2012; Candel &
Turliuc 2019; Malouff et al. 2010; Mund & Neyer 2014; Weidmann et al. 2017/2018; Gottman &
Levenson 2000; Heyman & Smith Slep 2001; Stanley et al. 2000; Kim et al. 2007; Aron et al.
1997; Carter & Buckwalter 2009; Houran et al. 2004; Todd et al. 2007; Kurzban & Weeden 2005;
Lenton & Francesconi 2010; Ambady & Rosenthal 1992; Murphy & Hall 2021; Chartrand & Bargh
1999; Ramseyer & Tschacher 2011; Grammer et al. 1999; Vacharkulksemsuk et al. 2016; Puts et
al. 2007/2011; Hughes et al. 2010; Veenstra & Hung 2011; Bilakhia et al. 2015; Hayashi/Okada
MMSD 2025; Kimura et al. 2025; Pizzato et al. 2010; Neve & Palomares 2019; Hutson et al. 2018;
Zhao et al. 2022; Paraschakis & Nilsson 2020; OkCupid/OkTrends/Dataclysm; Match "Singles in
America".

Notes on retrieval: Stanford's `nlp.stanford.edu/pubs/` paths largely 404 — the working mirror
is `web.stanford.edu/~jurafsky/pubs/`. PNAS, PMC and several publisher "PDF" endpoints return
HTML or JSON rather than PDFs; every download was verified with `file` and non-PDFs were
deleted rather than left in place.
