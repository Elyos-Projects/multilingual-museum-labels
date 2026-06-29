# Competitive + Improvement Analysis — `multilingual-museum-labels`

> Analyst review of PLAN.md v0.1.0 (2026-06-28) and TASKS.md. Lane: donated. Risk tier: medium (with sensitive-heritage and contested-legal escalation classes). Web-researched competitor grounding with cited URLs.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually rigorous for a v0.1 draft. It correctly identifies its hardest problems (rights, hallucination, cultural sensitivity) and gates them. Findings below are ordered by importance.

**Strong / correct:**

- **"Never invent an object" as identity constraint** is the right spine for museum interpretation. Machine translation and generative drafting both silently corrupt proper nouns, dates, materials, and provenance; museum professionals broadly hold that MT is "not yet good enough" without human review, and major museums pay for professional human translation (Field Museum/Multilingual Connections, Met/Eriksen) precisely for this reason ([AMT Lab](https://amt-lab.org/blog/2022/7/museums-use-of-natural-language-processing)). The claim-to-source grounding pass + blocking grounding flags directly answer this.
- **Two-layer rights model (facts vs. image), tracked per object**, is correct and frequently missed: the artwork copyright and the photograph copyright differ, and modern/contemporary works remain in copyright even when a photo is openly licensed. The BLOCKING per-object `license-000` prerequisite is the right enforcement.
- **Plain language as a measured gate** (CEFR A2–B1 / readability threshold, reviewer attestation fallback) aligns with museum-field guidance: ~8th-grade reading level, ≤ ~50 words of body text, defined jargon, active voice ([MuseumNext](https://www.museumnext.com/article/10-tips-for-writing-effective-museum-exhibit-labels/), [accessible-labels guidance](https://stepblogblog.wordpress.com/2020/05/12/6-golden-rules-for-writing-accessible-museum-labels/)).
- **Non-partisan-by-construction** for contested histories and the **HIGH-risk legal gate** (default omit; else licensed cultural-property counsel + jurisdiction-sourcing + "not legal advice") are appropriately conservative and consistent across Exec/§6/§8/governance/risks.
- **Honest status**: `verifiedNeed=false`, partner/reviewers/counsel all "TO BE SECURED," success = displayed not merged. This is the correct posture and is consistently applied.

**Most important correctness gaps:**

1. **Source-community authority is gated but framed too passively (consultation, not authority/co-authorship).** The plan treats source communities as a *review/veto* step layered on top of a curator-fact pipeline ("route to community review," "community wishes override"). Current decolonial-museum and repatriation-era practice is stronger: source communities hold **interpretive authority and co-authorship** over their heritage, not just a veto at the end — co-curation, community advisory boards with real decision-making power, and the community's *own narrative* alongside (or instead of) the institutional one ([PoLAR/decolonization](https://polarjournal.org/2024/09/21/decolonization-at-the-museum-exploring-power-dynamics-and-changing-ethical-norms-repatriation-policy-in-us-museums/), [decolonizing practices](https://esg.sustainability-directory.com/term/decolonizing-museum-practices/)). The plan's "never invent an object — write only from sourced curatorial fact" rule, while correct for factual claims, **can collide with this**: the curatorial record is often *itself* the colonial artifact (mis-attributions, missing community context). The plan needs an explicit data-model affordance for **community-authored interpretation/perspective as a first-class content type** (not just a sensitivity flag), and a rule that for affiliated heritage the community can supply facts/context that *correct or supplement* the institutional catalogue. This is the single most important plan-correctness finding.

2. **TK Labels / Local Contexts and Traditional Knowledge labeling are absent from the data model.** The plan references CARE principles (governance) but never mentions **TK Labels** or **Biocultural (BC) Labels** from Local Contexts — the field-standard, machine-attachable digital markers for exactly this use case (access/use/attribution protocols for Indigenous heritage in public-domain or third-party-held collections) ([Local Contexts TK Labels](https://localcontexts.org/labels/traditional-knowledge-labels/), [Mukurtu TK Labels FAQ](https://mukurtu.org/support/traditional-knowledge-labels-faq/)). A label project that produces *public-facing object labels* for affiliated heritage and does **not** carry TK Labels through to delivery is leaving the most relevant interoperable standard on the table. This belongs in `objectSchema` (a `tkLabels[]`/`careNotice` block) and in the delivery package.

**Lesser gaps / omissions:**

- **Accessibility is under-scoped relative to its own beneficiary list.** §3 names low-vision, low-literacy, cognitive-disability, and child visitors, but Scope explicitly excludes audio and treats only *reading level* as accessibility. Field practice for accessible labels is broader: **large-print/alt-format text, minimum type size (18–24pt), high contrast, sans-serif, line length, plus alt-text/audio-description and Braille** ([accessible-labels guidance](https://stepblogblog.wordpress.com/2020/05/12/6-golden-rules-for-writing-accessible-museum-labels/), [Tulane label guide](https://libguides.tulane.edu/c.php?g=1311227&p=9637555)). The plan can stay out of hardware/DTP yet still **emit accessibility-ready outputs**: structured alt-text per object, a large-print plain-text variant, and contrast/type guidance in the delivery spec. Right now "audio guides… out of scope" reads as excluding the very visitors named.
- **Plain-language metric for non-English source languages.** The plan honestly flags this (reviewer attestation fallback) but Flesch-Kincaid-family metrics are English-centric; the plan should name at least candidate cross-lingual approaches (e.g., LIX, sentence-length/word-frequency proxies, CEFR-vocabulary lists) so attestation isn't the only path for major target languages.
- **"Translation preserves plain-ness" is asserted but not measured** the way source readability is — translations get reviewer attestation only. Consider a back-translation or readability spot-check on target text where a metric exists.
- **No explicit handling of bilingual/parallel label layout conventions** (which language first, script direction RTL, transliteration display). The glossary covers transliteration conventions but delivery formatting of bidirectional/parallel labels isn't specified.
- **Scope correctly excludes hosting/portal**, but with no partner CMS named, "delivery format" risk is real — see §3 interoperability gap.

Overall: completeness is high; the two structural gaps (community authority as co-authorship; TK Labels in the model) and the accessibility under-scope are the substantive ones.

---

## 2. Competitive landscape

| Competitor | What it is | Strengths | Weaknesses (vs. this project's niche) |
|---|---|---|---|
| **Bloomberg Connects** | Free philanthropy-funded mobile guide app; 1,500+ institutions | Free to museum *and* visitor; built-in accessibility (VoiceOver, captions, transcripts, zoom, font size); multilingual via Google Translate; explicitly courts small orgs ([site](https://www.bloombergconnects.org/), [Bloomberg Philanthropies](https://www.bloomberg.org/arts/connecting-audiences-to-culture-online-or-onsite/)) | Multilingual = **unreviewed Google Translate** (the exact failure mode this project targets); app/phone-mediated, not physical wall labels; content not openly licensed/portable; centralized platform | 
| **Smartify** | Image-recognition + audio-guide app; 700+ orgs, AI personalized tours | Scan-to-identify; offline; AI-personalized tours; some free guides ([MuseumNext](https://www.museumnext.com/article/smartify-and-the-future-of-bring-your-own-device-byod/), [trendwatching](https://www.trendwatching.com/innovation-of-the-day/smartify-uses-ai-to-generate-a-personalized-audio-tour-for-every-museum-visitor)) | Language coverage **varies per museum**, often English-only; in-app purchases; vendor lock-in; not designed for tiny volunteer museums or open content |
| **Google Arts & Culture** | Free platform; digitized collections + on-device translation | Huge reach; free; Lens/translate features | MT accuracy criticism (no idiom/context handling); skews to large institutions; not a label-production workflow; content governance is Google's, not the community's ([AMT Lab](https://amt-lab.org/blog/2022/7/museums-use-of-natural-language-processing)) |
| **Museum CMS — TMS (Gallery Systems), PastPerfect, etc.** | Collections management systems of record | Authoritative catalogue data; many small museums already on PastPerfect | CMS, not an interpretation/translation pipeline; no plain-language or multilingual review workflow; data often siloed/proprietary |
| **Cuseum** | Museum mobile-engagement platform with AI translation + TTS | Real-world community-language work (Heard Museum → Navajo; Vizcaya → Spanish/Portuguese/Haitian Creole); built-in AI translation, TTS, accessibility ([Cuseum AI](https://cuseum.com/blog/2025/2/6/ai-for-interactive-storytelling-at-museums), [mobile engagement](https://cuseum.com/mobile-engagement)) | Aimed at mid-to-large budgets; paid SaaS; AI translation without the rigorous human/community review gate; proprietary |
| **Local Contexts / TK + BC Labels** | Standards for Indigenous attribution/protocol markers | The field standard for community authority/attribution over heritage; interoperable digital labels; public-domain-aware ([Local Contexts](https://localcontexts.org/labels/traditional-knowledge-labels/)) | Not a translation or plain-language label producer — **complementary, not competitive**; the project should *adopt* it |
| **Mukurtu CMS** | Free, open-source Indigenous-built CMS w/ cultural protocols + TK Labels | Granular cultural-access protocols; community records w/ multiple narratives; TK Labels native; Roundtrip metadata export ([Mukurtu](https://mukurtu.org/)) | A platform/CMS (heavier adoption); access-control oriented; not a multilingual plain-language label pipeline — again **complementary** as a delivery/integration target |
| **Wikidata / Wikimedia Commons GLAM (Sum of All Paintings, SDC)** | Open structured collections data, multilingual labels in up to ~300 languages | Truly multilingual structured data; CC0/open; "Sum of All Paintings" already synced many museum catalogues; free reviewer/volunteer community ([Wikidata GLAM](https://wikimediafoundation.org/news/2016/08/23/wikidata-glam/), [SDC GLAM](https://commons.wikimedia.org/wiki/Commons:Structured_data/GLAM)) | Structured *labels* ≠ interpretive plain-language *visitor* labels; quality uneven; not curated for accessibility/plain-language; community governance not source-community-specific |
| **Smithsonian Open Access** | 5.1M+ CC0 items + metadata, API, GitHub | Best-in-class open object data for the cold-start exemplar set; commercial-reuse-clear CC0 ([CC](https://creativecommons.org/2020/02/27/smithsonian-releases-2-8-million-images-data-into-the-public-domain-using-cc0/), [SI Open Access](https://www.si.edu/openaccess)) | It's a *source*, not a competitor; large-institution content (watch the "small museum benefit" guardrail — use it for exemplars, not as the beneficiary) |
| **Audio-guide vendors (SmartGuide, Guide ID, amuseapp)** | Paid digital audio-guide / BYOD solutions, 30+ languages | Turnkey multilingual audio; mature ([SmartGuide](https://www.smartguide.app/)) | Paid; audio not text labels; translation quality and community authority not the selling point |

**Landscape summary:** the commercial field (Bloomberg Connects, Smartify, Cuseum, Google) competes on **app reach and convenience** but mostly delivers **unreviewed machine translation** and **proprietary, non-portable** content for **phone-mediated** experiences. The open/ethical field (Local Contexts/TK Labels, Mukurtu, Wikidata/Smithsonian) provides **standards, protocols, and open data** but **not a plain-language, reviewed, multilingual visitor-label production workflow for tiny museums**. Nobody occupies the project's exact intersection.

---

## 3. Gaps we can fill

1. **Reviewed (not raw-MT) multilingual visitor labels for museums with zero translation budget.** Every app competitor leans on Google Translate; the project's qualified-bilingual + grounding gate is the differentiator the field implicitly admits is needed.
2. **Open, portable, attribution-clean label content** (CC BY / CC BY-SA / per-grant) that the museum *owns* and can print, host, or push to Wikidata/Bloomberg/its CMS — versus vendor-locked app content.
3. **Plain-language + accessibility-ready outputs** (reading-level-checked, large-print/alt-text variants) tuned for low-literacy, low-vision, immigrant, and child visitors — a combination no competitor packages together.
4. **Source-community authority built into the content model** via TK/BC Labels + community-authored interpretation — bridging the gap between the standards bodies (Local Contexts/Mukurtu) and the production workflow none of them run.
5. **A cold-start path with no partner** using Smithsonian/Wikidata/PD open data — proving the pipeline before a museum commits, which SaaS vendors cannot offer a volunteer museum.
6. **Provenance + rights-as-data** (per-object, facts vs. image, hash/archive snapshots) — auditable correctness the app platforms don't expose.
7. **Interoperability/delivery gap to fill:** export to the formats small museums actually use (print CSV/PDF, **Wikidata/Commons SDC upload**, Mukurtu/PastPerfect-friendly metadata) so labels live beyond a single vendor.

---

## 4. Differentiators to win

- **Reviewed accuracy over convenience** — "never invent an object" + claim-to-source grounding + qualified bilingual review is a categorical quality claim no MT-based app makes.
- **Single strongest differentiator: community-authored, TK-Labeled, openly-licensed labels that the museum owns.** Combining (a) source-community interpretive authority/co-authorship, (b) Local Contexts TK/BC Labels carried through to delivery, and (c) an open license + full provenance produces an artifact that is simultaneously *ethical*, *portable*, and *correct* — a position the commercial apps (proprietary, MT, veto-less) and the standards bodies (no production workflow) each only half-occupy.
- **Built for the under-resourced** — explicit small-museum eligibility guardrail; free; donated lane; no SaaS fee or lock-in.
- **Accessibility + plain language as measured gates**, not marketing.
- **Auditable rights & provenance** as structured, CI-checked data.
- **Standards-aligned and interoperable** (Getty AAT/ULAN/TGN, Dublin Core, schema.org, CARE, TK Labels, Wikidata) rather than a walled garden.

---

## 5. Claude API leverage (and hard limits)

**Where Claude (with review) adds the most value:**

1. **Plain-language drafting from sourced facts.** Claude rewrites verified catalogue facts into label-sized (40–120-word), CEFR-A2/B1, jargon-defined visitor text — then a readability metric + reviewer gate. This is the highest-volume, best-fit use, and pairs with the emit-`UNCERTAIN:`-flags discipline already in the plan.
2. **Translation drafts seeded by the glossary.** Claude produces first-pass translations honoring do-not-translate lists, proper nouns, transliteration, and preserved plain-ness — strictly as a *draft* for the qualified bilingual reviewer. Strong multilingual coverage helps under-served languages where professional translators are scarce.
3. **Label templates, glossary scaffolding, and reviewer-checklist assists** — generating per-language-pair glossary candidates (terms/proper nouns to confirm), house-style templates, accessibility alt-text drafts, and pre-filling `review.yaml`/grounding-check structure to lower reviewer load.
4. (Secondary) **Triage assist** — flag candidate sensitive-heritage/contested-legal items and uncertain claims for human routing (never auto-decide).
5. (Secondary, MCP) **Grounding/claim-to-source checking** — Claude maps each drafted sentence back to a `sourceRef` and surfaces ungrounded claims for removal.

**Where Claude must NOT decide (hard gates):**

- **Translation final approval and cultural framing** — a qualified bilingual reviewer and, for affiliated heritage, the **source community** decide; Claude output is never delivered unreviewed.
- **TK/Indigenous heritage authority** — community consent, interpretation, and TK-Label assignment are the community's, not the model's. "Do not describe/image/display" overrides any draft.
- **Factual claims about real objects** — no AI-authored dates/makers/materials/provenance/attributions; every claim traces to a verified source or is removed (blocking grounding flag).
- **No AI-authored cultural/historical claims** without human + community review; no adjudication of contested ownership/restitution (HIGH-risk legal gate, licensed counsel).
- **License/rights determinations** — Claude may *surface* candidate license/credit info but a human license reviewer verifies; "if unclear, don't produce."

This split keeps the project inside CLAUDE.md guardrails and the donated lane (the human runs their own agent; no headless invocation; if metered drafting is ever wanted it moves to the funded lane with a hard budget cap).

---

## 6. Ten concrete optimizations

1. **Add a `communityInterpretation` content type + `tkLabels[]`/`careNotice` block to `objectSchema`** so source-community authorship and Local Contexts TK/BC Labels are first-class, carried through to delivery — not just a sensitivity flag. (Addresses §1 findings 1–2.)
2. **Promote source communities from "reviewer/veto" to "co-author/authority"** in §6/§8/governance: communities may supply facts/context that *correct or supplement* the institutional catalogue, with a documented co-curation/consent workflow (CARE + repatriation-era practice).
3. **Add accessibility outputs to the delivery package**: structured alt-text per object, a large-print plain-text variant, and a one-page contrast/type/line-length spec (18–24pt, sans-serif, dark-on-light) — staying out of hardware/DTP but serving the named low-vision/low-literacy beneficiaries.
4. **Name a Wikidata/Wikimedia Commons (SDC) export path** as a first delivery target — it gives partner-less museums an immediate, free, multilingual, openly-licensed home for labels and a built-in reviewer/volunteer community.
5. **Use Smithsonian Open Access (CC0) + Wikidata for the M0 exemplar set** explicitly, and record that exemplar use does not make a large institution the *beneficiary* (guardrail hygiene).
6. **Specify cross-lingual readability proxies** (LIX, sentence-length/word-frequency, CEFR vocab lists) per target language so reviewer-attestation isn't the only fallback for major languages; add a translation plain-ness spot-check (e.g., target-side readability or back-translation sample).
7. **Add a Mukurtu/PastPerfect/TMS-friendly metadata export** (Dublin Core + Roundtrip-style round-trippable fields) so labels integrate with the CMS a small museum already runs.
8. **Define bilingual/parallel-label layout conventions** in the delivery spec (language order, RTL handling, transliteration display) — currently unspecified.
9. **Add a lightweight "community sign-off" record type to `review.yaml`** distinct from expert sign-off, with consent scope and revocation, so a later community removal request is auditable end-to-end (ties to the decommissioning path).
10. **Build a glossary/translation-memory seed from Wikidata multilingual labels** (300-language structured data) to bootstrap proper-noun and term coverage cheaply, with human confirmation.

---

## 7. Parallel & perpendicular spin-offs

- **`multilingual-signage-templates`** (parallel): the plain-language + accessibility + parallel-layout work generalizes directly from museum object labels to wayfinding/signage; share the readability gate and bilingual-layout conventions.
- **`historical-markers-index` / `historical-markers`** (perpendicular): same "never invent — source-grounded, neutral, contested-history-aware" discipline applied to roadside/heritage markers; shared neutrality-by-construction and HIGH-risk legal gate.
- **`public-domain-translations`** (parallel): reviewed translation pipeline + glossary/TM tooling is reusable; museum glossaries feed a broader PD-translation corpus.
- **`local-history-stubs`** (perpendicular): plain-language, sourced micro-articles for small localities; same grounding + provenance model, different output venue (Wikidata/Wikipedia stubs).
- **`loc-public-domain-engine`** (parallel): a shared **PD/open-source ingestion + rights-snapshot + hash/archive engine** that this project, public-domain-translations, and local-history-stubs all consume — factor the allow-list + watcher out as a common library.
- **Museum-interpretation toolkit** (product spin-off): bundle the plain-language guide, cultural-sensitivity/CARE/TK-Label triage, reviewer checklist, glossary format, and accessibility spec as a reusable, openly-licensed **toolkit** any small museum can adopt without the full pipeline.
- **MCP server** (tooling spin-off): an agent-neutral MCP server exposing tools for *grounding-check* (claim→`sourceRef`), *readability-check* (multi-metric), *glossary lookup/do-not-translate*, *rights/license validation*, and *TK-Label lookup* — usable across all the spin-offs and by any partner's own agent, keeping vendor-neutrality per CLAUDE.md.

---

## 8. Open questions

1. **Community authority vs. "never invent an object":** when the institutional catalogue is itself a colonial artifact (mis-attribution, missing context), what is the precedence rule between sourced curatorial fact and community-supplied correction — and how is community-authored content provenance-recorded without a traditional `sourceRef`?
2. **TK/BC Labels operationalization:** does the project formally register with **Local Contexts** and carry TK/BC Labels into delivery, or only reference CARE? Who assigns labels — the community via Local Contexts, or the project on their behalf (it must be the former)?
3. **Delivery interoperability:** is Wikidata/Commons SDC a primary delivery target (partner-independent value), and which CMS exports (Mukurtu, PastPerfect, TMS) are worth supporting first?
4. **Accessibility scope line:** how far into alt-text/large-print/audio-description does the project go before it hits its "no audio/DTP/hardware" non-goal — and is excluding audio defensible given the named low-vision beneficiaries?
5. **Non-English readability metrics:** which concrete metric/proxy per priority target language, and the exact attestation wording where none exists?
6. **Reviewer + community sourcing at scale:** can a GLAM-Wikimedia or museum-network partnership supply *both* bilingual reviewers *and* a route to source communities, or are these separate recruitment tracks?
7. **Small-museum beneficiary integrity:** using Smithsonian/large-institution open data for exemplars is fine, but does any pathway risk the *beneficiary* drifting to a resourced institution? (Keep the eligibility call recorded.)
8. **Funded lane trigger:** at what object-set size does metered drafting under escrow become worth it, and what hard per-task cap keeps it inside CLAUDE.md budget discipline?

---

## Summary

**Top 3 competitors.** (1) **Bloomberg Connects** — free, accessible, 1,500+ orgs, but multilingual = unreviewed Google Translate and proprietary, phone-mediated content. (2) **Smartify** — scan-to-identify + AI audio tours, but per-museum/English-skewed languages and vendor lock-in. (3) **Cuseum** — real community-language work (Heard Museum/Navajo, Vizcaya) with built-in AI translation/TTS, but paid SaaS aimed at mid-to-large budgets and lacking a rigorous community-review gate. (Local Contexts/TK Labels, Mukurtu, Wikidata/Smithsonian are complementary standards/data sources, not competitors.)

**Single strongest differentiator.** Community-authored, TK-Labeled, openly-licensed plain-language labels that the museum *owns* — combining source-community interpretive authority, Local Contexts TK/BC Labels carried to delivery, an open license, and full provenance. Commercial apps are proprietary/MT/veto-less; standards bodies have no production workflow; this project uniquely occupies the intersection of ethical, portable, and correct.

**Top 3 Claude-API ideas.** (1) Plain-language drafting from verified facts into label-sized CEFR-A2/B1 text with `UNCERTAIN:` flags + readability gate. (2) Glossary-seeded translation *drafts* for qualified bilingual review, strong for under-served languages. (3) Label templates, glossary/TM scaffolding (seeded from Wikidata's ~300-language labels), accessibility alt-text drafts, and grounding/claim-to-source checking — all human-reviewed.

**Two most important plan-correctness findings.** (1) **Source-community authority is under-modeled:** the plan treats communities as a late-stage review/veto, but repatriation-era decolonial practice gives them interpretive authority and co-authorship — and "never invent an object" can collide with the fact that the curatorial record is often itself the colonial artifact. The data model needs community-authored interpretation as a first-class type with a precedence rule for community corrections. (2) **TK Labels / Local Contexts are absent from the schema and delivery** despite being the field-standard interoperable marker for exactly this heritage; add a `tkLabels[]`/`careNotice` block and carry it through. (Lesser but real: accessibility is under-scoped — large-print/alt-text/contrast outputs should be delivered for the low-vision/low-literacy visitors the plan itself names.)
