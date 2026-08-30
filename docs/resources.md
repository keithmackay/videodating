# Video, Audio & Transcript Analysis — Library and Vendor Survey

Research date: **2026-08-30**. Target stack: Next.js / Node (Vercel-style hosting) with a Python
sidecar for ML work. Use case: scheduled 1:1 speed-dating video calls, recorded and transcribed,
with post-call analysis to extract compatibility signals.

> **Three findings that change the obvious answer.** Read these before anything else.
>
> 1. **Twilio Programmable Video is NOT shutting down.** The widely-cited December 5, 2026 EOL was
>    *reversed* — Twilio now says Video remains a standalone product. Most blog comparisons still
>    repeat the dead EOL. It is still not our pick, but not for the reason you'd expect.
> 2. **Hume AI's Expression Measurement API — the default recommendation for vocal emotion — was
>    sunset in June 2026.** Last job creation May 14, 2026; API access ended June 14, 2026; it has
>    been stripped from the TypeScript SDK. Any plan built around it is dead on arrival.
> 3. **Emotion recognition is now a regulated category, not just a sensitive one.** The EU AI Act's
>    prohibition took effect February 2025, and Microsoft retired Azure's emotion inference back in
>    2023. Category 4 below is a legal question before it is a technical one.

---

## 1. Video / Web Conferencing Infrastructure

All options here are WebRTC SFUs with a hosted control plane. The differentiator for us is not
latency (all are fine for 2-party calls) but **recording ergonomics** — specifically whether we can
get *per-participant audio tracks*, which roughly doubles downstream diarization quality.

| Platform | Model | Recording | Built-in transcription | Maintenance | Fit |
|---|---|---|---|---|---|
| **Daily.co** | Usage-based, ~$0.004/min scaling to ~$0.0015/min at volume; 10k free min/month | Composite **and `raw-tracks`** (per-track, to your own S3) | Yes | Active | **Best fit** |
| **LiveKit** | Cloud per-track-min (~$0.004 audio, $0.006–0.024 video); **self-host = infra only** | Egress: room-composite, track, track-composite → S3/GCS/Azure | Via agents/plugins | Very active, large OSS community | Strong runner-up |
| **Whereby Embedded** | Subscription from ~$6.99/mo + usage | Yes, higher tiers | Limited | Active | Fastest to ship, least control |
| **100ms** | Usage-based | Yes | Yes | Active | Credible, smaller ecosystem |
| **Agora** | Usage-based, aggressive volume pricing | Yes (cloud recording) | Add-on | Active | Global scale; heavier SDK |
| **Vonage Video API** | Usage-based | Yes (archiving, incl. individual streams) | Add-on | Active (OpenTok successor) | Fine, no standout advantage |
| **Twilio Video** | Usage-based | Yes | No | **Active — EOL reversed** | Roadmap uncertainty after a public EOL-then-reversal is itself a risk |
| **Zoom Video SDK** | Usage-based, generous free tier | Yes | Yes | Active | Good quality; heaviest embed |

**Why raw per-track recording matters.** Speaker diarization is the single biggest accuracy risk in
this pipeline — a mixed-down stereo file forces the STT model to *guess* who spoke, and diarization
error compounds into every downstream signal. If each participant's audio arrives as its own file,
speaker attribution becomes exact and free, and diarization stops being an error source at all.
Daily's `raw-tracks` and LiveKit's track egress both give this; most others give you a composite
mix. This one capability should drive the choice.

**Vercel caveat.** Recording processing is CPU-heavy and long-running (LiveKit's own guidance is
2–6 CPUs per composite job). This does not belong in a Vercel serverless function. Expect a
queue plus a worker (Inngest/Trigger.dev, or a container on Fly/Railway/ECS) regardless of vendor.

---

## 2. Speech-to-Text / Transcription

| Service | Pricing (async) | Diarization | Real-time | Notes |
|---|---|---|---|---|
| **AssemblyAI** | ~$0.15–0.21/hr; diarization +~$0.02/hr | Yes — widely benchmarked as best-in-class | Yes (~$0.45/hr) | Flat pricing, no concurrency surcharge |
| **Deepgram** | Nova-3 ~$0.46/hr PAYG; diarization +~$0.12/hr | Yes | Yes, very low latency | Fastest streaming; tiered/committed pricing |
| **OpenAI Whisper (self-host)** | GPU cost only | **No** — needs pyannote bolted on | No | Cheapest at volume, most ops burden |
| **Whisper API** | ~$0.36/hr | No | No | Simple, no diarization |
| **Google STT / AWS Transcribe / Azure Speech** | ~$0.60–1.44/hr | Yes | Yes | Pick if already in that cloud |
| **Rev AI** | ~$0.20+/hr | Yes | Yes | Human-transcription option for a golden eval set |

Published comparisons put AssemblyAI ahead of Deepgram on both cost and accuracy for async work
(cpWER ~30.2 vs ~37.9 in AssemblyAI's own benchmark — vendor-published, so treat directionally, but
the cost gap is independently verifiable). Deepgram's edge is streaming latency, which we don't
need for post-call batch analysis.

**Cost is a non-issue at our scale.** A 5-minute speed date is ~0.083 audio-hours; at $0.21/hr that
is under two cents per call. Optimize for accuracy and diarization quality, not price — and note
that if we take Daily's per-track recording, we can transcribe each speaker's file separately and
skip paid diarization entirely.

---

## 3. Sentiment / Emotion Analysis from Transcripts (NLP)

**Classical / open source**
- **NLTK VADER** — lexicon-based, rule-driven. Fast, zero cost, no GPU. Tuned for social-media-style
  text; weak on sarcasm, negation-at-distance, and conversational context. Useful as a cheap
  baseline, not as a product signal.
- **spaCy** — not a sentiment model itself; the right tool for tokenization, NER, and linguistic
  features (question rate, pronoun use, turn-taking metrics). Actively maintained.
- **Hugging Face transformers** — `cardiffnlp/twitter-roberta-base-sentiment-latest` (3-class
  sentiment), `j-hartmann/emotion-english-distilroberta-base` (7 Ekman emotions),
  `SamLowe/roberta-base-go_emotions` (28 GoEmotions labels). All permissively licensed and
  self-hostable. Cheap and deterministic once served.

**Commercial APIs**
- **Google Cloud Natural Language**, **Azure AI Language** (Text Analytics), **AWS Comprehend** —
  all actively maintained, all offer document- and sentence-level sentiment plus entity extraction,
  all priced per 1k characters. Solid, unremarkable, and none of them understand dialogue.

**LLM-as-judge** — the strongest fit for this specific problem. Off-the-shelf sentiment models
classify *sentences in isolation*. What actually predicts compatibility in a speed date is
conversational structure: who asked questions, whether topics were picked up or dropped, reciprocity
of self-disclosure, repair after an awkward beat, laughter alignment. A frontier model reading the
whole diarized transcript against a rubric captures that; a sentence classifier structurally cannot.

The 2026 literature is consistent on the tradeoff: frontier LLM judges score highest on broad
conversational benchmarks, while fine-tuned encoders (RoBERTa-class) run at 1–10% of the cost per
call and are competitive on *narrow, well-specified* labels. The standard production pattern is a
cascade — cheap classifier first, escalate ambiguous cases to the frontier model.

**Recommended path:** start with an LLM-as-judge over structured rubrics (Claude with a JSON schema
and explicit per-dimension scoring). Log every judgment. Once we have volume and a hand-labeled
golden set, distill the high-frequency dimensions into a fine-tuned encoder to cut cost. Do not
start with the classifier — we don't yet know which dimensions matter, and the LLM lets us change
the rubric with a prompt edit instead of a retraining run.

---

## 4. Facial Expression / Emotion Analysis from Video

**Read this section as a legal analysis with a tools appendix.**

The industry has retreated from this capability, and did so deliberately:

- **Azure Face API** — Microsoft retired inference of emotion, gender, age, smile, facial hair, hair
  and makeup. Closed to new customers June 21, 2022; existing customers cut off June 30, 2023.
  Microsoft's stated reasoning was the absence of scientific consensus linking facial configuration
  to internal emotional state, plus discriminatory-outcome risk.
- **EU AI Act** — bans emotion recognition in workplaces and education (effective Feb 2025), with
  narrow medical/safety exceptions. Consumer dating is not currently in the banned tier, but the
  Act's rationale is explicit about *limited reliability, lack of specificity, and poor
  generalizability*, with bias concentrated along age, ethnicity, race, sex and disability lines.
- **Affectiva** — acquired by Smart Eye; the commercially open emotion-AI offering has largely moved
  to automotive/research licensing rather than general developer API access.
- **AWS Rekognition** — still exposes an `Emotions` field on `DetectFaces`. AWS's own documentation
  frames it as detection of *apparent physical expression*, explicitly not a determination of a
  person's internal emotional state. That distinction is the entire legal defense, and it is fragile
  in a product that markets itself as reading compatibility.

**Open-source options (research-grade)**
- **py-feat** — actively maintained Python toolbox (Cosan Lab). Facial action units, landmarks, head
  pose, emotion classifiers. Best-documented option; built for research reproducibility.
- **OpenFace** (TadasBaltrusaitis) — the standard for facial action unit + gaze + head pose
  extraction. **Academic/research license — commercial use requires a separate CMU license.** This
  is a hard blocker for a commercial product without paid licensing.
- **DeepFace** — MIT licensed, actively maintained, includes an emotion head. License is clean;
  the emotion model is trained on posed-expression datasets (FER2013 lineage) and generalizes poorly
  to spontaneous conversational faces.
- **MediaPipe Face Mesh** — Google, actively maintained, Apache 2.0. Gives 468 landmarks and blend
  shapes, *not* emotion labels. Building our own classifier on top means we own the validity claim
  entirely — which is worse, not better, from a liability standpoint.

**Recommendation: defer this category entirely for v1.** The scientific basis is contested, the
regulatory trend is one-directional, the accuracy is worst exactly where the stakes are highest
(cross-ethnicity, neurodivergent expression), and the reputational downside of "the dating app
scored my face" is severe and not hypothetical. If we later want a non-verbal channel, **head-pose
and gaze-derived engagement signals** (from MediaPipe or py-feat) are far more defensible than
emotion labels: "both participants were oriented toward the camera and mutually attentive" is a
measurable behavioral claim; "the participant felt joy" is an inference the field cannot support.

---

## 5. Audio / Vocal Emotion & Prosody

- **Hume AI — Expression Measurement API: SUNSET.** New jobs ended May 14, 2026; API access and
  result download ended June 14, 2026; removed from the TypeScript SDK. Hume redirected the
  capability into EVI, their conversational voice product — which is a real-time voice *interface*,
  not a batch analysis tool for third-party recordings. **Do not design around this.** The sunset
  has visibly displaced users (audEERING and Imentiv both published migration pitches), which is
  worth remembering as a general lesson: single-vendor dependency on a novel-capability API is
  fragile.
- **openSMILE** — the long-standing standard for acoustic feature extraction (eGeMAPS, ComParE
  feature sets) from audEERING. Actively maintained, Python bindings available. Dual-licensed —
  **free for research, commercial use requires a license from audEERING.** Check this before
  committing.
- **librosa** — ISC licensed, actively maintained, fully permissive. MFCCs, pitch/F0, spectral
  features, tempo, RMS energy. Not an emotion model — a feature extractor you build on.
- **pyAudioAnalysis** — Apache 2.0, includes segmentation and classification helpers. Maintenance
  has been slow for some time; usable but not a foundation to build on.
- **Hugging Face SER models** — `speechbrain/emotion-recognition-wav2vec2-IEMOCAP`,
  `firdhokk/speech-emotion-recognition-with-facebook-wav2vec2-large-xlsr-53`, and several wav2vec2
  fine-tunes reporting ~80% validation accuracy. **That number is on acted-emotion corpora
  (IEMOCAP, RAVDESS) and does not survive contact with spontaneous conversational speech** — the
  gap between acted and natural affect is the well-documented central failure mode of this field.

**Practical recommendation.** Skip categorical vocal *emotion* labels — same validity problem as
faces, same regulatory heading. Instead extract **objective prosodic and conversational-dynamics
features** with librosa plus transcript timestamps: speaking-time balance, turn-taking latency,
interruption and overlap counts, pause distribution, pitch variance, laughter events, and
speech-rate convergence between speakers. These are *measurements*, not inferences about inner
states — they are cheap, explainable, permissively licensed, defensible to a regulator, and
(per the conversation-analysis literature) plausibly more predictive of rapport than any emotion
label would be. This is the highest value-per-risk work in the entire survey.

---

## 6. Cross-Platform Signal Extraction (Email, SMS, Social)

Technically feasible; commercially and legally the most hazardous item on the list. Access has
tightened sharply across every platform.

| Source | Access | Reality in 2026 |
|---|---|---|
| **Gmail API** | OAuth, Google verification + annual third-party security assessment for restricted scopes | Achievable but slow and expensive; Google scrutinizes mail-reading apps hard |
| **X / Twitter API** | Pay-per-use since Feb 2026, **no free tier**; ~$0.005/post read, 2M read/mo cap. Legacy Basic ($200/mo) and Pro ($5k/mo) closed to new signups; Enterprise ~$42k/mo | Costly, and terms restrict derived-data storage |
| **Instagram Graph API** | **Personal accounts categorically blocked.** Business/Creator only, and only with explicit app authorization | Effectively unusable for consumer dating users |
| **Meta / Facebook Graph** | App Review; friends/interests scopes largely closed post-Cambridge Analytica | Do not plan around this |
| **Twilio (SMS)** | Only messages sent through our own numbers | Cannot reach a user's existing texts |
| **Apply Magic Sauce** (Cambridge Psychometrics Centre) | Digital-footprint → Big Five, plus age/gender/politics/religion/**sexual orientation** predictions | Operating; academic pedigree. Inferring orientation and religion means generating GDPR Article 9 **special-category data** — a serious escalation |
| **IBM Watson Personality Insights** | **DISCONTINUED** — closed to new customers Dec 2020, fully withdrawn Dec 1, 2021 | Dead. Ignore any guide that recommends it |

**Legal considerations — these are load-bearing, not boilerplate.**

- **Call recording consent.** All-party (two-party) consent states include **California, Florida,
  Illinois, Pennsylvania, Washington, Maryland, Massachusetts, Montana, Nevada, New Hampshire,
  Connecticut**. California treats video conferences as confidential communications where
  participants expect privacy. Since we pair strangers across arbitrary states, **assume all-party
  consent is required universally** — explicit, logged, per-call, in-product consent from both
  participants before recording starts. This is simpler than geo-conditional logic and strictly
  safer.
- **Biometric privacy.** Illinois **BIPA** requires written consent before collecting biometric
  identifiers and carries a private right of action with statutory damages — it is the most
  litigated privacy statute in the US. Voiceprints and face geometry both fall in scope. Texas
  (CUBI) and Washington have analogous statutes. This risk attaches to categories 4 and 5 above and
  is a further reason to prefer behavioral measurements over biometric inference.
- **GDPR.** Consent must be freely given, specific, informed, unambiguous, and *as easy to withdraw
  as to give*. Bundling analysis consent into general ToS acceptance does not satisfy this. Special
  categories (Art. 9 — orientation, religion, health, politics) require explicit consent and a
  documented lawful basis; inferred data counts as personal data.
- **CCPA/CPRA.** Sensitive personal information triggers a right to limit use; California proposals
  would require explicit written consent for recordings involving biometric data.
- **Automated decision-making.** If analysis outputs materially affect matching, GDPR Art. 22 and
  emerging state AI rules imply transparency, explanation, and human-review obligations.

**Recommendation: cut category 6 from the roadmap entirely for now.** The access surface has
narrowed to near-nothing (Instagram blocks personal accounts outright, X charges enterprise rates,
Gmail demands an annual security audit), the data that remains reachable is weakly predictive, and
the legal exposure is concentrated in exactly the special categories that carry the heaviest
penalties. Every hour spent here buys less signal than an hour spent on conversational dynamics from
call audio we already have consent to record. Revisit only with dedicated privacy counsel and a
concrete, evidenced hypothesis about what signal we'd actually gain.

---

## Recommended Stack

| Layer | Pick | Rationale |
|---|---|---|
| **Video infra** | **Daily.co** | `raw-tracks` per-participant recording to our own S3 removes diarization as an error source — the highest-leverage decision in the pipeline. Prebuilt React components, transparent usage pricing, free tier covers all of development. **LiveKit** is the fallback if we need self-hosting for cost or data residency; its egress is equally capable but we operate it ourselves. |
| **Transcription** | **AssemblyAI** | Best-in-class diarization as a backstop, strong async accuracy, flat pricing with no concurrency surcharge. At ~2¢ per 5-minute date, cost is irrelevant — accuracy is the whole decision. |
| **Transcript analysis** | **LLM-as-judge (Claude) over a structured rubric** | Speed-date compatibility lives in conversational structure — reciprocity, question-asking, topic uptake — which sentence-level classifiers cannot see. Rubrics iterate with a prompt edit rather than a retraining cycle. Distill to a fine-tuned encoder later, once volume and a golden set tell us which dimensions matter. |
| **Prosody / audio** | **librosa + transcript timestamps → conversational dynamics** | Permissive license, no vendor risk, and it measures observable behavior (turn-taking latency, speaking balance, interruptions, pitch variance, convergence) rather than inferring inner states. Hume's sunset is the cautionary tale; openSMILE needs a commercial license; HF SER models are trained on acted corpora that don't transfer. |
| **Facial analysis** | **Defer** | Contested science, tightening regulation, worst accuracy on the most vulnerable users, severe reputational downside. If revisited: head-pose/gaze engagement via MediaPipe or py-feat, never emotion labels. |
| **Cross-platform signals** | **Defer** | Access surface has collapsed; remaining data is weakly predictive; exposure concentrates in GDPR special categories. Not a v1 problem. |
| **Processing** | **Queue + worker (Inngest / Trigger.dev), not Vercel functions** | Media processing is long-running and CPU-bound; serverless timeouts don't fit. |
| **Consent** | **Explicit, logged, per-call, both parties, all jurisdictions** | Simpler than geo-conditional logic and strictly safer given all-party-consent states and BIPA's private right of action. |

**The through-line.** The defensible product is built on *conversational behavior* — what was said,
who spoke when, how the two people traded turns and built on each other. The fragile product is
built on *inferred inner states* from faces and voices. The second is where the vendors are exiting
(Hume, Microsoft, Affectiva), where regulators are legislating, and where accuracy is weakest. It is
also, notably, where a competitor would most likely trip. Building on the first is both the lower-
risk path and, on the evidence, the more predictive one.

---

## Sources

- [Twilio: Video Will Remain a Standalone Product](https://www.twilio.com/en-us/changelog/-twilio-video-will-remain-a-standalone-product)
- [Twilio Programmable Video End of Life Notice](https://help.twilio.com/articles/20950630029595-Programmable-Video-End-of-Life-Notice)
- [Twilio Programmable Video is back from the dead — BlogGeek.me](https://bloggeek.me/twilio-programmable-video-back/)
- [Daily: Recording calls with the Daily API](https://docs.daily.co/guides/products/live-streaming-recording/recording-calls-with-the-daily-api)
- [Daily: recording.ready-to-download webhook](https://docs.daily.co/reference/rest-api/webhooks/events/recording-ready-to-download)
- [LiveKit Egress overview](https://docs.livekit.io/transport/media/ingress-egress/egress/)
- [livekit/egress on GitHub](https://github.com/livekit/egress)
- [WebRTC Platforms Compared: The 2026 Guide](https://www.rtcinsights.com/blog/webrtc-platforms-compared/)
- [AssemblyAI vs Deepgram: Accuracy & Speed Compared](https://www.assemblyai.com/blog/assemblyai-vs-deepgram)
- [Gladia: AssemblyAI vs Deepgram (2026)](https://www.gladia.io/blog/assemblyai-vs-deepgram)
- [Speaker Diarization API: AssemblyAI vs Deepgram vs Pyannote](https://www.forasoft.com/blog/article/speaker-diarization-api-comparison)
- [AssemblyAI vs Deepgram: API Pricing for High Volume](https://brasstranscripts.com/blog/assemblyai-vs-deepgram-pricing-high-volume-comparison)
- [Microsoft: Responsible AI investments and safeguards for facial recognition](https://azure.microsoft.com/en-us/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/)
- [EU AI Act Article 5: Prohibited AI practices](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-5)
- [FPF: Red Lines under the EU AI Act — emotion recognition prohibition](https://fpf.org/blog/red-lines-under-the-eu-ai-act-unpacking-the-prohibition-of-emotion-recognition-in-the-workplace-and-education-institutions/)
- [Wolters Kluwer: Prohibition of AI Emotion Recognition in the Workplace](https://legalblogs.wolterskluwer.com/global-workplace-law-and-policy/the-prohibition-of-ai-emotion-recognition-technologies-in-the-workplace-under-the-ai-act/)
- [Py-Feat](https://py-feat.org/) · [cosanlab/py-feat](https://github.com/cosanlab/py-feat)
- [OpenFace (TadasBaltrusaitis)](https://github.com/tadasbaltrusaitis/openface)
- [deepface on PyPI](https://pypi.org/project/deepface/)
- [audEERING: After Hume's Expression Measurement API](https://www.audeering.com/after-humes-expression-measurement-api-what-matters/)
- [Imentiv: Replacing Hume AI's Expression Measurement API](https://imentiv.ai/blog/replacing-hume-ais-expression-measurement-api-heres-what-imentiv-ai-offers/)
- [HumeAI TypeScript SDK releases](https://github.com/HumeAI/hume-typescript-sdk/releases)
- [speechbrain/emotion-recognition-wav2vec2-IEMOCAP](https://huggingface.co/speechbrain/emotion-recognition-wav2vec2-IEMOCAP)
- [firdhokk/speech-emotion-recognition-wav2vec2-large-xlsr-53](https://huggingface.co/firdhokk/speech-emotion-recognition-with-facebook-wav2vec2-large-xlsr-53)
- [Eugene Yan: Evaluating LLM-Evaluators (LLM-as-Judge)](https://eugeneyan.com/writing/llm-evaluators/)
- [JudgeBench: A Benchmark for Evaluating LLM-based Judges](https://arxiv.org/pdf/2410.12784)
- [Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/pdf/2306.05685)
- [Mindtickle: Call Recording Laws — 50-State & Global Consent Guide](https://www.mindtickle.com/legal/a-guide-to-call-recording-laws-and-regulations/)
- [Metaverse Law: Two-Party Consent Requirements for Recording Calls](https://www.metaverselaw.com/two-party-consent-requirements-for-recording-calls/)
- [Reed Smith: The legality of AI-powered recording and transcription](https://www.reedsmith.com/our-insights/blogs/employment-law-watch/102ls2n/the-legality-of-ai-powered-recording-and-transcription/)
- [Apply Magic Sauce — Prediction API documentation](https://applymagicsauce.com/documentation)
- [IBM Community: Watson Personality Insights deprecated](https://community.ibm.com/community/user/discussion/watson-pi-deprecated)
- [X (Twitter) API Pricing in 2026: All Tiers](https://postproxy.dev/blog/x-api-pricing-2026/)
- [Instagram Graph API: Complete Developer Guide for 2026](https://elfsight.com/blog/instagram-graph-api-complete-developer-guide-for-2026/)
