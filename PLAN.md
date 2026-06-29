# PLAN — multilingual-museum-labels

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: J. Carter (acting maintainer) · Lane: donated

## Executive summary

`multilingual-museum-labels` is an Elyos good-deed project that produces **plain-language,
multilingual object descriptions** ("labels," "wall text," "gallery cards") for **small,
under-resourced museums, historical societies, and community/teaching collections** — and the
visitors who read them. For each object the project produces a short, accurate, jargon-free
description in a **source language** plus **reviewed translations** into one or more target
languages, every one carrying a **per-object license + attribution + provenance** record.

The defining constraint — the project's identity — is **"never invent an object."** A museum label
is a statement of record about a real artefact; a hallucinated date, maker, material, or provenance
is not a cosmetic error but a corruption of the public record and a breach of the museum's trust.
Every factual claim in a description must trace to a **sourced, attributed catalogue fact** supplied
or verified by the holding institution. We write *from* curatorial fact; we do not generate it.

The work runs in the **donated lane**: a human runs their own coding agent interactively to draft
descriptions and translations and supporting artefacts, then opens PRs; the Elyos CLI only prepares
workspaces and opens PRs. The project is **medium risk tier**: descriptions need **factual/domain
accuracy** and translations need a **qualified bilingual reviewer**, so a domain-competent human
sign-off gates every deliverable. Two narrow content classes escalate the gate above medium and are
handled by exception (see §8): **culturally sensitive heritage** (human remains, sacred/ceremonial
objects, Indigenous/community-affiliated material) routes to a **source-community / cultural
authority review**, and any text touching **contested legal ownership, restitution, or repatriation**
is **HIGH risk**, requires **licensed cultural-property-law counsel sign-off**, carries an
explicit **"informational, not legal advice"** framing, and is **jurisdiction-sourced** — or is
omitted.

Honest status note: the program is real but **no specific partner museum is yet secured.** Until a
museum confirms in writing that it wants the work, owns/can license the catalogue facts we build on,
and will publish the result, `verifiedNeed` is recorded as `false` on tasks whose value depends on a
named beneficiary, and Definition of Shipped cannot be met. Securing a first partner museum is the
top open dependency (see Open questions and Roadmap M2).

## Problem & beneficiaries

**Who is helped.**

- **Primary beneficiaries — visitors who cannot read the existing labels.** Non-native speakers,
  tourists, immigrant and refugee community members, low-literacy adults, children, and people with
  cognitive or reading disabilities who arrive at a small museum and find labels only in one
  language, written in specialist curatorial prose. They leave without understanding what they are
  looking at.
- **Direct beneficiaries — small/under-resourced museums.** Volunteer-run local history museums,
  community and heritage collections, historical societies, small university teaching collections,
  and library special collections that **want** multilingual, plain-language labels but have **no
  translation budget, no in-house plain-language writer, and no localisation pipeline.** Large,
  well-funded national museums are *not* the target (they have these resources, and serving them
  would risk primarily benefiting a comparatively resourced institution rather than the public).

**The need.** Good interpretive labelling is a known driver of museum access and learning, and
multilingual labelling is a recognised equity gap for small institutions. Today a small museum's
choices are: (a) no translation at all; (b) unreviewed machine translation, which mangles proper
nouns, period terminology, materials, and cultural nuance, and silently introduces factual errors;
or (c) expensive professional localisation they cannot afford. The gap is **accurate, plain,
reviewed, correctly-licensed** descriptions that a small museum can actually print and display.

**Verified need: TO BE SECURED.** The *category* need is well-evidenced (museum-access and
plain-language literature; the visible scarcity of multilingual labels in small institutions). But a
**specific requesting museum, its object list, its target languages, and — critically — its right to
license the underlying catalogue facts and images** are **not yet secured.** Tasks are written so the
project can build reusable foundations (schemas, glossaries, plain-language and cultural-sensitivity
guidelines, the license model, a worked exemplar from openly-licensed objects) **without** a partner,
while clearly flagging that **delivery/adoption tasks are blocked** until a partner museum and its
rights are confirmed.

**Partner org: TO BE SECURED.** Candidate partner types: local historical societies and community
museums; regional/national museum-development and small-museum networks (e.g., AAM's small-museum
community, UK Museum Development networks, state/provincial museum associations, ICOM, Collections
Trust); university teaching collections and library special collections; GLAM-Wikimedia
"museums-on-Wikimedia" partners (a natural fit because their object metadata/images are already
openly licensed). None is committed as of this draft.

## Goals and non-goals

**Goals**

- Stand up a **repeatable pipeline** that turns sourced catalogue facts about an object into a
  **plain-language source-language description** and **reviewed translations**, with full provenance
  and per-object licensing.
- Make **plain language a measured property**, not an aspiration: defined reading-level / plain-language
  targets, checked per description.
- Maintain **per-object license + attribution + provenance** as structured, machine-checkable data so
  every published label is correctly credited and traceable.
- Maintain per-language-pair **glossaries** (art/heritage terminology, proper nouns, transliteration,
  do-not-translate lists) so terminology is consistent and reviewable.
- Guarantee **qualified human review** of every description and translation before delivery, with
  escalation paths for culturally sensitive and legally contested material.
- Deliver label sets that a partner museum **actually adopts and displays/publishes.**

**Non-goals**

- **Not** a general machine-translation service, public website, or self-serve label generator.
- **Not** a source of new scholarship — we **do not author original provenance, attributions, dates,
  or art-historical claims.** We rephrase and translate **already-established, sourced** curatorial
  facts. Generating new factual claims about an artefact is out of scope.
- **Not** a venue for contested legal/ownership/restitution determinations — we do not adjudicate
  ownership, and we do not give legal advice (see §8 for the narrow, gated way contestation may be
  *neutrally noted*).
- **Not** relicensing or "freeing" copyrighted source material, object images, or a museum's
  proprietary catalogue text; we honour each rights-holder's terms.
- **Not** partisan or editorialising on contested histories (colonial acquisition, war, religion,
  identity, politics): we present **sourced, attributed, neutral** facts; we do not take sides.
- **Not** audio guides, AR/VR, OCR of handwritten ledgers, print typesetting/DTP, signage hardware,
  or hosting — beyond the plain delivery formats a partner needs.
- **Not** handling controlled, embargoed, or restricted collections data, donor PII, or
  not-for-public-display sensitive records.

## Success metrics (outcomes)

Outcome-based and beneficiary-centric. Baselines are ~0 (new project). **Outcome** targets are for
the first ~6 months after a partner museum is secured; **interim foundation metrics** are tracked
from M0/M1 so progress is visible *before* a partner exists. We explicitly **do not** count "PRs
merged," "objects drafted," or "words translated" as success — only **reviewed, correctly-licensed
descriptions a museum actually displays for visitors.**

**Outcome metrics (post-partner)**

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| Object descriptions **adopted and displayed/published** by a partner museum | 0 | ≥ 25 objects | Partner written confirmation in PR/receipt + display/publication evidence |
| **Languages** delivered end-to-end per adopted object (source + reviewed translations) | 0 | ≥ 2 target languages across the set | Project registry |
| Descriptions passing **qualified reviewer sign-off on first or second pass** | n/a | ≥ 90% (**effective from M1**) | Reviewer checklist outcomes |
| Descriptions meeting the **plain-language reading-level target** before sign-off | n/a | ≥ 95% | Readability check artifact per description |
| **License/attribution/provenance compliance** of delivered artefacts | n/a | 100% (hard gate; **automated from M1**, manual in M0) | License-check task / CI per deliverable |
| **Factual defects** found *after* delivery (wrong date/maker/material/provenance) | n/a | 0 | Post-delivery defect log + museum feedback |
| **Sensitive-content / contested-claim handling escapes** (sensitive item shipped without required escalated review) | n/a | 0 | Audit of `review.yaml` escalation flags |
| Partner-reported / visitor-reported **usefulness** (qualitative) | n/a | Positive from ≥ 1 partner | Partner feedback; optional visitor feedback if partner collects it |

**Interim foundation metrics (M0/M1, partner-independent)**

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| Reusable **schemas + guidelines** merged (object/description/provenance/review/glossary; plain-language guide; cultural-sensitivity guide) | 0 | complete by end of M1 | Files merged + CI green |
| Glossary **terms** captured per language pair | 0 | ≥ 40 per pair | Glossary entry count |
| Reviewers **qualified** (criteria met + onboarded; bilingual + heritage-aware) | 0 | ≥ 2 by end of M1 | Reviewer roster |
| Worked **exemplar** objects fully pipelined from openly-licensed sources | 0 | ≥ 3 objects × 1 target language | Exemplar deliverables in repo |

**Denominator & sample rule for the "≥ 90% pass" rate.** The denominator is **every description
deliverable that reaches qualified review** (counted once per deliverable, not per pass); a
deliverable "passes" if it earns reviewer sign-off on its **first or second** pass. The rate is
reported **only once the denominator is ≥ 10**; below that we report the raw count (e.g., "7/8
passed") to avoid small-sample noise.

## Scope

**What an "object description" is (bounded).** A short interpretive label: typically a **title/name,
date, maker/origin, materials/technique, and a plain-language 40–120-word description** of what the
object is, what it was for, and why it matters — written for a general visitor, plus optional
"accession/credit line" per the museum's convention. Length and fields are configurable per partner
house style; the default keeps to label-sized text, not catalogue essays.

**"Plain language" defined (measured).** Source-language text targets roughly **CEFR A2–B1 / a
plain-language reading level** (short sentences, common words, defined jargon, active voice,
concrete). Where automated readability metrics exist for a language (e.g., Flesch-Kincaid / similar
for English), the description must meet the configured threshold; **for languages without reliable
automated metrics, the qualified reviewer attests to plain-language conformance** against the
project's plain-language checklist. Translations must **preserve plain-ness**, not just meaning.

**"Small / under-resourced museum" defined.** A holding institution that is volunteer-run or has
minimal professional staff and **no dedicated translation/localisation budget**, and whose primary
purpose is public/community/educational benefit (not a for-profit attraction). Where ambiguous, the
maintainer + steward make an explicit call recorded in the partner record; serving a large,
well-resourced institution is out of scope (guardrail: no primary benefit to a resourced entity).

**Prioritisation rule (which objects/languages first).** (1) A **secured partner museum's** stated
priority objects and target languages; (2) objects whose **source facts and images are already
openly licensed** (PD / CC / partner-owned with clear grant) — lowest rights risk; (3) target
languages with **reviewer coverage already available**; (4) the **largest visitor-need gap** (e.g.,
the dominant non-native-speaker community for that museum's locale). Culturally sensitive and
legally contested objects are **de-prioritised** to later, escalation-gated batches, never the
cold-start exemplar set.

**In scope**

- A **per-object record** of sourced catalogue facts + rights, with provenance.
- **Plain-language source-language descriptions** rewritten from those sourced facts.
- **Reviewed translations** of those descriptions into named target languages (decomposed per
  *object × language*).
- Per-language-pair **glossaries** (terminology, proper nouns, transliteration, do-not-translate).
- **Plain-language guide**, **cultural-sensitivity guide**, **reviewer checklist**, and
  **reviewer-handoff template**; sign-off recorded in the PR.
- **Per-object + per-deliverable license/attribution/provenance verification.**
- Delivery packaging: source facts reference, description, translations, glossary refs, provenance,
  attribution/credit line, license, reviewer sign-off.

**Out of scope**

- Authoring **new** facts, attributions, dates, or scholarship about an object.
- Objects whose **underlying facts/images are not licensable** for the intended use (unverified or
  incompatible rights → not produced).
- **Adjudicating ownership/restitution**, or any **legal advice**; high-risk legal content beyond the
  narrow neutral-note exception in §8.
- Culturally sensitive material handled **without** the required source-community/cultural-authority
  review (we will not ship it ungated).
- Audio/video, AR, OCR of manuscripts, complex-script typesetting/DTP, signage hardware, hosting, or
  a public portal.
- Donor PII, restricted/embargoed collection records, or any not-for-public-display data.

## Solution approach & architecture

This is primarily a **content/data pipeline** project (deliverables are descriptions + translations +
data artefacts), with light agent-neutral tooling. It rides on existing Elyos donated-lane mechanics
(CLI prepares workspace, human runs agent, PR opened, human/expert review gates "done"). All
tooling/schemas live in the **agent-neutral core** (`packages/schema`), with no vendor-specific
logic, per CLAUDE.md.

**Pipeline (per object, then per object × language)**

1. **Ingest & verify object facts + rights.** Capture the museum's sourced catalogue facts into an
   `object.yaml`; record rights for **both** the *facts/text* and any *image* separately; confirm the
   object is eligible (rights clear; sensitivity/contestation classified). Record provenance (source,
   version/date, retrieval date, who supplied/verified).
2. **Classify sensitivity & contestation.** Run the cultural-sensitivity + legal-contestation
   triage (see §8). Route sensitive objects to community/cultural-authority review; route
   ownership/restitution-touching text to the HIGH-risk legal gate or omit it.
3. **Draft plain-language source description.** Agent writes a label-sized description **strictly from
   the sourced facts**, applying the plain-language guide and glossary, and **emits uncertainty
   flags** for anything not directly supported by a source.
4. **Readability + grounding self-check.** Agent runs the readability check and a
   **claim-to-source grounding pass** (every factual statement maps to a source line); flags
   unresolved items.
5. **Draft translations.** Agent translates the approved source description per the language-pair
   glossary, preserving proper nouns, dates, materials, and plain-ness.
6. **Qualified human review.** A domain-competent reviewer (and, for translations, a qualified
   bilingual reviewer) verifies factual fidelity, plain-language conformance, terminology, cultural
   appropriateness, and neutrality; completes the checklist; **records sign-off in the PR.**
7. **License & attribution check.** Confirm per-object license, required attribution/credit line, and
   any disclaimers are present and correct; confirm output license is compatible with source rights.
8. **Package & deliver.** Assemble the bundle, hand off to the partner museum, and record adoption /
   display.

**Artifacts / data model**

- `objects/<objectId>/object.yaml` — `{ objectId, title, alternativeNames, dateOrPeriod, maker,
  origin, materials, dimensions, accessionNumber, sourcedFacts[] (each {claim, sourceRef}),
  factsRights {licenseName, licenseUrl, holder, derivativesAllowed, grantEvidence},
  imageRights {present, licenseName, licenseUrl, holder} | null,
  sensitivity {class: none|sensitive-heritage|restricted, communityAffiliation, notes},
  contestation {class: none|noted|contested-legal, notes},
  eligibility {eligible: bool, reason}, provenance, suppliedBy, verifiedBy, verifiedDate }`.
- `objects/<objectId>/descriptions/<lang>.md` — the plain-language description (source or translation),
  with front-matter linking object + language + role (source|translation).
- `objects/<objectId>/provenance.yaml` — links the description to object record version, facts source,
  glossary version, drafter (agent + human), reviewer(s), and sign-off.
- `objects/<objectId>/attribution.txt` — credit line + license + any required disclaimer (verbatim).
- `objects/<objectId>/review.yaml` — checklist results, `agentFlags`, readability result, sensitivity/
  contestation escalation status, reviewer COI declarations, sign-off(s).
- `glossaries/<src>-<tgt>.yaml` — `{ term, translation|preserve, partOfSpeech, notes }` + proper-noun
  and transliteration conventions + do-not-translate list.
- `guides/plain-language.md`, `guides/cultural-sensitivity.md`,
  `templates/reviewer-checklist.md`, `templates/reviewer-handoff.md`.

**Standards alignment (use, don't reinvent).** Terminology and metadata align where practical to
**Getty vocabularies (AAT/ULAN/TGN)**, **Dublin Core**, and **schema.org/CreativeWork**; cultural-data
practice follows **CARE Principles for Indigenous Data Governance** and museum sensitivity guidance.
We **reference** these standards; we do not build heavy ontology tooling.

**Formats.** UTF-8 throughout; Markdown/plain text as the canonical description format; YAML for
metadata. Partner-specific export formats (e.g., CSV for a label printer, simple bilingual PDF) are
added only on request.

**Content schemas & CI validation.** The Task JSON schema lives in `packages/schema/src/schemas.ts`
(AJV / JSON Schema **draft-07**). This project adds **content schemas in the same package** —
`objectSchema`, `descriptionSchema`, `provenanceSchema`, `reviewSchema`, `glossarySchema` — compiled
and exposed via `validate.ts` exactly like `taskSchema`/`registrySchema` (AJV with `ajv-formats`).
YAML/Markdown-front-matter artefacts are parsed to JSON and validated by a structural-check script
wired into `pnpm test`, so **CI fails on any malformed or non-conformant content file.** The license
gate builds on this by cross-checking each deliverable's metadata against its object record. This
keeps validation **agent-neutral** and in the core schema package, not in adapters.

**Key decisions**

- **Source-grounded only ("never invent an object").** Every factual claim links to a `sourceRef`;
  the grounding self-check + reviewer enforce it. Ungrounded claims block sign-off.
- **Rights-as-data, per object, facts and image separately.** The label's text rights and the
  object's image rights are different and tracked independently; only the parts with clear,
  compatible grants are produced/published.
- **Plain language as a measured gate**, not a vibe (readability metric where available; reviewer
  attestation otherwise).
- **Sensitivity & contestation triage before drafting**, with explicit escalation routes (community
  review; HIGH legal gate).
- **Neutrality by construction** for contested histories: sourced + attributed + non-partisan, or not
  written.
- **No PII / no restricted data ingested** — public, licensable object facts only.

## Data, licensing & compliance

**This is the project's most important section. Be conservative; when rights or facts are unclear, do
not produce the description.**

**Two distinct rights layers, tracked per object.**

1. **The catalogue facts / source text** the description is built from. Facts themselves are
   generally not copyrightable, but **the museum's catalogue *expression* (its written description,
   research notes, selection/arrangement) can be.** We therefore require either (a) the partner
   museum's **written grant** to use its catalogue facts for derivative plain-language descriptions,
   or (b) facts drawn from **openly-licensed / public-domain** sources (PD object data, CC-licensed
   collections, Wikidata/Wikimedia GLAM data). We **rephrase**, we do not copy proprietary catalogue
   prose.
2. **The object image** (if any). Image rights are **separate and often more restrictive** —
   especially for **modern/contemporary works still in copyright** (the *artwork* may be in copyright
   even when a *photo* is freely licensed, and vice-versa). Images are included **only** with verified
   compatible rights; otherwise the description ships **without** the image.

**Allow-listed source families (each verified per object).**

- **Public-domain object data** (works whose copyright has expired; PD per the applicable
  jurisdiction — verify, as PD status is jurisdiction-specific). Most appropriate for the cold-start
  exemplar set.
- **Openly-licensed collections data** (CC0 / CC BY / CC BY-SA museum open-data and GLAM-Wikimedia
  datasets) — honour share-alike/attribution terms exactly.
- **Partner-museum-supplied facts** under a **written grant** specifying permitted use, derivatives,
  attribution/credit line, and output license. **No grant → no production.**
- **Excluded:** all-rights-reserved third-party catalogues, scraped data of unclear provenance,
  controlled/embargoed records, and any source whose terms are unverified or incompatible.

**Per-object license/provenance record (required before drafting).** For each object we record:
identifiers; the sourced facts each with a `sourceRef`; facts-rights and image-rights blocks
(license name + URL, holder, derivatives-allowed, grant evidence); a **snapshot** of the governing
license/grant (committed copy + **SHA-256 hash** + web-archive URL where available); the required
**attribution/credit line**; sensitivity and contestation classification; and `verifiedBy` /
`verifiedDate`. A **source/grant-change check** (minimal/manual in M0, automated in M1) re-checks
snapshots and flags drift before further work or delivery.

**BLOCKING prerequisite for any object's first description.** Before drafting, the maintainer/license
reviewer must have **confirmed in writing, recorded on the object record:** (a) the **facts/text are
licensable** for a derivative plain-language description (open license or written partner grant); (b)
the **required attribution/credit line** (verbatim); and (c) **image rights** status (include or
exclude). If any is unconfirmed, that object is **not** produced.

**Privacy / PII.** Object descriptions can incidentally name **living people** (artists, donors,
people depicted). We: collect **no** donor or visitor personal data; include personal information
about living individuals **only** where it is already public, sourced, and necessary to describe the
object, and **never** sensitive personal data; respect privacy and avoid defamatory or
unverified statements about living persons (reviewer check). Partner contacts and any non-public
collection data are handled out-of-band and **never committed.**

**Cultural rights & sensitivity (binding).** For Indigenous, sacred/ceremonial, ancestral-remains,
or community-affiliated material we follow **CARE principles** and museum sensitivity practice:
such objects are flagged at triage and **require source-community / cultural-authority review**
before any description is written or shipped; community wishes (including a request **not** to
describe, image, or display) **override** production. This is a hard gate (see §8).

**Non-partisan / contested histories.** Colonial acquisition, war, religion, politics, and identity
are presented with **sourced, attributed, neutral** language; we do not editorialise, advocate, or
adjudicate. Where a fact is genuinely contested in reliable sources, we may **neutrally note that it
is contested, with attribution to the sources** — never assert a winner.

**Output licensing.** Project **tooling/code is MIT.** **Description content** is released under a
license **compatible with the source rights** and the partner grant — defaulting to **CC BY 4.0** for
descriptions built on PD/open facts with no share-alike obligation, **CC BY-SA 4.0** where a source
is share-alike, and **whatever the partner grant specifies** for partner-supplied facts. We **never**
relicense more permissively than the source allows and **never** assert a license over an underlying
image we do not control.

## Quality, review & risk gates

**Risk tier: medium (with two escalation classes above it).** Per the good-deed definition, medium =
needs domain accuracy and a **reviewer with the relevant skill** — here, a **domain-aware reviewer**
for factual fidelity/plain-language and a **qualified bilingual reviewer** for each translation.

**Required review before a deed is "done"**

1. **Agent self-check** — readability check **and** claim-to-source grounding pass, emitting
   uncertainty flags (first pass; not sufficient alone).
2. **Qualified human reviewer** sign-off recorded in the PR — factual fidelity to sources,
   plain-language conformance, terminology/proper nouns, cultural appropriateness, neutrality;
   for translations, a **qualified bilingual reviewer.**
3. **License & attribution verification** — per-object license + credit line + any disclaimer +
   complete provenance + compatible output license.
4. **CI green** for code/tooling and structural checks on content files.
5. **Maintainer approval** of the PR.

**Reviewer independence.** Reviewers must be **independent of the drafting step**: the human who ran
the drafting agent may **not** be the sole sign-off reviewer for that deliverable, and each reviewer
records a **conflict-of-interest declaration.**

**Escalation class 1 — culturally sensitive heritage (above medium).** Any object classified
`sensitive-heritage` (human/ancestral remains, sacred/ceremonial objects, Indigenous or
community-affiliated material) requires **source-community or cultural-authority review** in addition
to the standard gate, follows **CARE principles**, and **honours a community request not to describe/
image/display.** No such object ships without that review recorded in `review.yaml`.

**Escalation class 2 — contested legal ownership/restitution (HIGH risk).** Any description text that
would touch **ownership, title, restitution, or repatriation claims** is **HIGH risk** and is handled
one of two ways: (a) **omit** the contested legal content (default — keep the label to uncontested
descriptive facts); or (b) if neutrally noting contestation is genuinely necessary and partner-
requested, it requires **sign-off by a licensed attorney competent in cultural-property/heritage law
for the relevant jurisdiction**, must be **jurisdiction-sourced** (cite the governing law/authority),
must be **strictly non-partisan** (note the claim and counter-claim with attribution, assert no
winner), and must carry a clear **"This is general information, not legal advice"** disclaimer. No
HIGH-risk text merges without the attorney sign-off recorded in the PR.

**Agent uncertainty self-check (operationalized).** The drafting agent must emit explicit flags in the
form `UNCERTAIN: <location> | <type: fact|grounding|term|proper-noun|cultural|legal|ambiguous-source>
| <note>` for anything not directly supported by a source or otherwise uncertain. Flags are copied
into `review.yaml` as `agentFlags`. **No sign-off may be recorded while any flag is unresolved**: each
must be `resolved` (with the reviewer's adjudication) or `accepted-as-is` (with reasoning).
**Grounding flags are blocking**: an unresolved "claim has no source" flag means the claim is removed.

**Definition of Shipped (project-specific).** A label set is *shipped* only when: acceptance criteria
met **and** plain-language target met **and** all factual claims source-grounded **and** qualified
reviewer (and bilingual reviewer per translation; community/legal reviewer where escalated) sign-off
recorded **and** per-object license/attribution/provenance verified **and** CI green **and** the set
is **delivered to and adopted (displayed/published) by the partner museum.** Merged-but-not-displayed
is **not** shipped.

## Roadmap & milestones

**M0 — Foundation & cold-start (no partner required).**
Goal: build the reusable machinery and prove the full pipeline on **openly-licensed exemplar
objects**, end-to-end except partner adoption.
Exit criteria: content schemas (`object/description/provenance/review/glossary`) merged with a
**structural CI check**; **plain-language guide** + **cultural-sensitivity/triage guide** +
**reviewer checklist** + **handoff template** merged; one language-pair glossary started (≥ 40
terms); the per-object **rights model + BLOCKING license prerequisite** demonstrated; **≥ 3
openly-licensed exemplar objects** taken end-to-end to a **plain-language source description + 1
reviewed target-language translation each**, each passing the readability check, grounding check, and
a manual license/attribution check; `verifiedNeed=false` recorded where no partner.
**License-gate note:** M0 ships a **minimal automated structural check** (required license/
attribution/provenance/sensitivity fields present and well-formed); **full source-compatibility
enforcement is automated in M1.** The 100% / ≥ 90% / ≥ 95% metrics are **effective from M1**, with M0
verifying exemplars manually plus the structural check.

**M1 — Repeatability & reviewer network.**
Goal: make the pipeline repeatable and recruit/qualify reviewers.
Exit criteria: written **reviewer-qualification criteria** (domain-aware + bilingual + sensitivity-
aware; independence + COI rules) and **≥ 2 qualified reviewers** (or a partner such as a museum
network / GLAM-Wikimedia community engaged); glossary + guides generalised to **≥ 2 language pairs**;
**license-check tooling enforced in CI**; **automated source/grant-change watcher** operating;
**sensitivity-triage + legal-escalation procedure** finalised and dry-run on a contrived sensitive/
contested example; a second batch of exemplars across a second language reviewed. **Steward named**
(prerequisite for M2).

**M2 — First partner museum delivery (needs partner).**
Goal: deliver an adopted label set.
Exit criteria: a **partner museum secured** with a **written facts/image grant** (`verifiedNeed=true`);
agreed object list + target languages; **≥ 25 objects** produced with reviewed source + ≥ 1 target
language, all gates passed; the set **delivered and confirmed displayed/published** by the museum.
First true "Definition of Shipped" event. Dependency: M0/M1 + partner + grant.

**M3 — Scale program.**
Goal: scale to more objects/languages with sustained quality and tracked outcomes.
Exit criteria: ≥ 25 objects across **≥ 2 target languages** adopted (or a second partner museum
onboarded); reviewer rotation established; outcome tracking (post-delivery factual-defect log,
sensitivity-escape audit, partner/visitor feedback) operating; named sustainability/maintenance
owner; source/grant re-verification cadence in effect.

## Work breakdown

The itemized, sized backlog lives in **[TASKS.md](./TASKS.md)**, organized by the milestones above
(M0–M3) plus a Backlog/future section. Each task maps to an Elyos Task JSON (schema in
`packages/schema/src/schemas.ts`) with id, type, lane, risk tier, deliverable, acceptance criteria,
and license fields. M0/M1 tasks are partner-independent foundations and exemplars; M2+ tasks are
gated on a secured partner museum and its rights grant, and are marked accordingly
(`verifiedNeed: false`, `requestor: TO BE SECURED` until then).

## Governance, roles & stakeholders

- **Maintainer (Owner): J. Carter (acting)** — accepts/sequences tasks, approves PRs, owns the
  object-record/rights-model integrity and the license gate. Acts as interim license/compliance
  reviewer until a dedicated reviewer is named.
- **Qualified reviewers (per need): TO BE SECURED** — a **domain-aware reviewer** (heritage/museum
  literacy) for factual fidelity + plain language, and a **qualified bilingual reviewer** per target
  language. Sign-off recorded in PRs; rotation defined in M1/M3.
- **License/compliance reviewer** — may be the maintainer initially; verifies per-object rights
  (facts + image) and per-deliverable attribution/disclaimer; escalates ambiguous rights.
- **Cultural-authority / source-community reviewers: ENGAGED PER OBJECT** — required for
  `sensitive-heritage` items; their decisions (including "do not describe/display") are binding.
- **Cultural-property-law counsel (HIGH-risk legal gate): TO BE SECURED** — a licensed attorney
  competent in heritage/cultural-property law for the relevant jurisdiction; sign-off required for any
  contested-ownership/restitution text (else such text is omitted).
- **Steward (last-mile owner): TBD — named by end of M1** (acting maintainer holds the duties in the
  interim). Owns the partner-museum relationship and the rights grant, and confirms **adoption /
  display.** Naming a steward is a **prerequisite for entering M2.**
- **Partner / requestor: TO BE SECURED** — the small museum defining objects + languages, granting
  rights, and confirming display/publication.

## Dependencies & integrations

- **Elyos donated lane:** `packages/cli` (workspace prep + PR), `packages/core`, `packages/schema`
  (Task JSON + the new content schemas). No funded-lane / API-key execution in this project.
- **Open source data:** public-domain object data; CC/CC0 collections; **Wikidata / Wikimedia
  Commons GLAM** datasets and tools (a natural low-rights-risk source for the exemplar set).
- **Standards/vocabularies:** Getty AAT/ULAN/TGN, Dublin Core, schema.org, CARE principles (reference
  use; subject to their own terms).
- **Readability tooling** per language where available (e.g., Flesch-Kincaid-family libraries for
  English); reviewer attestation where not.
- **Human reviewers / a museum network or GLAM-Wikimedia community** for qualified + bilingual review
  — external dependency, **not yet secured.**
- **Partner museum** for objects, **rights grant**, and adoption — **not yet secured.**
- **Cultural-property-law counsel** for the HIGH-risk legal gate — **not yet secured** (only needed if
  contested-ownership text is ever attempted; default is to omit).

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Hallucinated / unsourced object facts (wrong date, maker, material, provenance) enter a public label | Medium | Critical | "Never invent an object": claim-to-source grounding pass; ungrounded-claim flags are blocking; reviewer verifies fidelity; post-delivery defect log | Reviewers / Maintainer |
| Rights violation — using non-licensable catalogue prose, or an in-copyright image, or wrong attribution | Medium | High | Per-object two-layer rights record (facts + image); written partner grant or open-license only; BLOCKING license prerequisite; "if unclear, don't produce" | License reviewer / Maintainer |
| Culturally insensitive handling of sacred/ancestral/Indigenous material | Medium | Critical | Sensitivity triage before drafting; mandatory source-community/cultural-authority review; CARE principles; community wishes override (incl. "do not describe") | Cultural-authority reviewers / Steward |
| Partisan or one-sided framing of contested histories (colonial, war, politics, religion) | Medium | High | Non-partisan-by-construction rule; sourced + attributed neutral language; "note contestation, never adjudicate"; reviewer neutrality check | Reviewers / Maintainer |
| Contested legal ownership/restitution text without legal competence → harm/liability | Low | Critical | Default = omit; HIGH-risk gate requires licensed cultural-property attorney sign-off, jurisdiction-sourcing, "not legal advice" framing | Maintainer / Counsel |
| Translation error mangles proper nouns, period terms, materials, or plain-ness | Medium | High | Glossary-driven translation; qualified bilingual reviewer mandatory; plain-language preserved-and-checked | Bilingual reviewers |
| Defamatory / privacy-harming statements about living people | Low | High | PII rule (public+sourced+necessary only, no sensitive data); reviewer defamation/privacy check | Reviewers / Maintainer |
| No qualified/bilingual reviewer available for a target language | High | High | Don't ship unreviewed; partner with museum network / GLAM-Wikimedia; scope only languages with reviewer coverage | Steward / Maintainer |
| No partner museum secured → nothing reaches "shipped" | High | High | M0/M1 build partner-independent value + exemplars; concrete outreach plan; `verifiedNeed=false`; pause/decision point if no partner by end of M1 | Acting maintainer → Steward |
| Serving a large/resourced institution (no real need) | Low | Medium | "Small/under-resourced" eligibility definition; explicit maintainer+steward call recorded | Maintainer / Steward |
| Source facts/images/grant change or are withdrawn after delivery | Medium | Medium | Snapshot hash/archive; source/grant-change watcher; provenance enables impact assessment + withdrawal | Maintainer |

## Security & privacy

- **Threat surface** is small: public/open source ingestion + text artefacts in a public repo. Main
  risks are **integrity** (wrong/tampered facts, mistranslation), **rights/compliance**, and
  **cultural/legal sensitivity** — not data exfiltration.
- **No secrets** in the normal flow (donated lane uses the human's own agent; no API keys, tokens, or
  escrow). Per CLAUDE.md, never write secrets/tokens into logs, receipts, or committed files.
- **PII:** no donor/visitor data collected; information about living people limited to public, sourced,
  necessary, non-sensitive facts; partner contacts and any non-public collection data kept out-of-band
  and uncommitted.
- **Sensitive/restricted data:** controlled, embargoed, or not-for-public-display records are out of
  scope and must never be ingested or committed.
- **Abuse/misuse prevention:** refusal guardrails apply — refuse tasks that would inject
  misinformation, push a partisan narrative, deceive/target people, give unqualified high-stakes
  (legal) advice, primarily benefit a for-profit, or violate a license/privacy/cultural right. Source
  integrity verification (correct, current, authoritative source) is part of every task.
- **Supply-chain:** pin source/grant URLs + version/date; **hash/archive snapshots** and run a
  source/grant-change watcher (M0 minimal, M1 automated).

## Sustainability & maintenance

- **After delivery,** the maintainer + steward keep object records, glossaries, and guides current and
  re-verify rights/facts when upstream sources or grants change. Reviewer rotation (M1/M3) avoids
  single-person dependence.
- **Outcome tracking** continues post-delivery: a factual-defect/feedback log per delivered set, a
  periodic **sensitivity-escape audit**, and partner check-ins to confirm continued display and capture
  errors. Outcomes (adoption/display, defects, cultural handling, usefulness) — not merge counts — are
  the maintained metrics.
- **Decommissioning:** if a source's rights change to forbid reuse, or a community requests removal,
  affected deliverables are flagged and, if required, withdrawn; provenance makes impact assessment and
  museum notification possible.

## Open questions

1. **Partner museum:** which small museum is the first requestor; what are its priority objects,
   target languages, and house-style label conventions? (Blocks M2 and `verifiedNeed=true`.)
   **Partner-sourcing plan (concrete):**
   - **Outreach target types (named):** local historical societies/community museums; regional/national
     museum-development and small-museum networks (AAM small-museum community, UK Museum Development,
     state/provincial associations, ICOM, Collections Trust); university teaching collections; library
     special collections; GLAM-Wikimedia partner museums.
   - **Owner:** acting maintainer until a Steward is named (by end of M1), who then takes over.
   - **Timeline:** outreach in parallel with M0; aim for **≥ 3 serious conversations by end of M1** and
     a **signed grant + first partner during M2 sourcing.**
   - **Pause/decision point:** if **no partner is secured by end of M1**, pause new production and make
     an explicit **go / pivot / hold** decision (e.g., pivot to publishing labels for *openly-licensed*
     collections only, where no partner grant is needed).
2. **Reviewer sourcing:** recruit individual domain + bilingual reviewers, or partner with a museum
   network / GLAM-Wikimedia community? What exactly qualifies a "domain-aware" reviewer?
3. **Rights model per source family:** confirm the exact compatible **output license + credit line**
   for (a) PD object data (jurisdiction-dependent), (b) CC/CC-BY-SA open collections, and (c)
   partner-supplied facts under grant. Confirm the **image-rights** decision tree (artwork vs. photo
   copyright).
4. **Cultural-authority reviewers:** how are appropriate source-community/cultural authorities
   identified and engaged per object, and what is the binding-decision workflow under CARE?
5. **Legal counsel:** is contested-ownership text ever in scope, or do we hard-omit it for v0.1?
   (Default: omit; counsel only if a partner specifically requests and funds review.)
6. **Reading-level targets per language:** which automated readability metric (if any) per language,
   and the reviewer-attestation fallback wording for languages without one.
7. **Delivery formats:** what do partners actually need — plain Markdown, bilingual CSV for a label
   printer, simple bilingual PDF, or a Wikimedia upload?
8. **Funded lane?** Proposal implies donated; do we ever want metered drafting under escrow for a
   large object set? (Out of scope for v0.1.)

## References

- `C:\code\elyos\CLAUDE.md` — Elyos work rules, lanes, quality bar, refusal guardrails.
- `C:\code\elyos\docs\good-deed-definition.md` — good-deed criteria and risk tiers.
- `C:\code\elyos\packages\schema\src\schemas.ts` — Task JSON schema (and home of the new content schemas).
- `C:\code\elyos\planning\ROADMAP.md` — portfolio roadmap (this project listed under Track 4).
- Getty Vocabularies (AAT / ULAN / TGN); Dublin Core; schema.org/CreativeWork — terminology/metadata.
- CARE Principles for Indigenous Data Governance; museum sensitivity guidance — sensitive-heritage handling.
- Creative Commons license suite (CC0 / CC BY 4.0 / CC BY-SA 4.0) — output licensing.
- Wikidata / Wikimedia Commons GLAM datasets and tools — candidate open-source data + partner community.
- Plain-language / readability guidance (CEFR; Flesch-Kincaid-family metrics where applicable).

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified against the first draft and **have been
applied** in the body of this PLAN (and the companion TASKS.md). Each line states the change and where
it now lives.

1. **Two-layer rights model (facts vs. image) made explicit.** Split rights into `factsRights` and
   `imageRights` in the data model and §7, because artwork copyright and photo copyright differ and
   in-copyright modern works are a real trap. (§6, §7)
2. **"Never invent an object" elevated to the project's identity constraint**, with a concrete
   enforcement (claim-to-source grounding pass; blocking grounding flags). (Exec summary, §6, §8)
3. **Plain language redefined as a measured gate** (CEFR A2–B1 / readability threshold; reviewer
   attestation where no metric exists) rather than an aspiration. (§5, §8, metrics)
4. **Cultural-sensitivity escalation class added** (human remains/sacred/Indigenous → source-community/
   cultural-authority review; CARE; community veto). (§8, §6, governance, risks)
5. **HIGH-risk legal escalation class added** for contested ownership/restitution: default omit;
   else licensed cultural-property attorney sign-off + jurisdiction-sourcing + "not legal advice"
   framing + non-partisan. (Exec summary, §8, governance)
6. **Non-partisan-by-construction rule** for contested histories (colonial/war/religion/politics):
   sourced + attributed + neutral, "note contestation, never adjudicate." (§3, §6, §8, risks)
7. **"Small/under-resourced museum" given an objective definition** to prevent primarily benefiting a
   resourced institution (guardrail #3). (§5, risks)
8. **Sensitivity + contestation triage inserted as pipeline step 2**, *before* drafting, so escalation
   happens prior to writing. (§6)
9. **BLOCKING per-object license prerequisite** (facts licensable + credit line verbatim + image
   decision) modeled on vital-info-translations' `license-000`. (§6, TASKS M0)
10. **Snapshot integrity (SHA-256 hash + web-archive) + source/grant-change watcher** added for both
    facts and grants (M0 minimal, M1 automated). (§6, §14, roadmap)
11. **Content schemas placed in the agent-neutral core** (`objectSchema`/`descriptionSchema`/etc. in
    `packages/schema`) with CI structural check, matching the house pattern and CLAUDE.md's
    "no vendor logic in core." (§6)
12. **Standards alignment added** (Getty AAT/ULAN/TGN, Dublin Core, schema.org, CARE) as *reference*,
    avoiding heavy ontology build. (§6, references)
13. **PII / living-persons + defamation stance added** (public+sourced+necessary+non-sensitive only;
    reviewer defamation/privacy check). (§6, §14, risks)
14. **Reviewer independence + COI declaration** required; drafter cannot be sole reviewer. (§8,
    governance, TASKS)
15. **Operationalized agent uncertainty flags** with a typed `UNCERTAIN:` format incl. `grounding` and
    `legal` types; grounding flags are blocking. (§8)
16. **Outcome metrics made beneficiary-centric and anti-vanity** (displayed objects, defects=0,
    sensitivity-escapes=0, plain-language %, usefulness) with baselines/targets + a sample rule for
    the pass-rate denominator. (§4)
17. **Interim foundation metrics** added so progress is visible before a partner exists. (§4)
18. **Cold-start uses openly-licensed exemplar objects** (incl. GLAM-Wikimedia), so M0 needs no partner
    grant and carries the lowest rights risk. (§5, roadmap M0, TASKS)
19. **Prioritisation rule** added (partner priority → open-licensed facts → reviewer coverage →
    visitor-need gap; sensitive/contested de-prioritised). (§5)
20. **Steward as last-mile/adoption owner**, named-by-end-of-M1 as an M2 prerequisite, owning the
    partner relationship and the rights grant. (Governance, roadmap)
21. **Definition of Shipped tightened to "displayed/published," not merged**, with all gates
    enumerated. (§8)
22. **Partner-sourcing plan made concrete** (named target types, owner, timeline, pause/decision point
    with a pivot to open-collections-only). (§16, risks)
23. **Decommissioning/withdrawal path** added for rights change *and* community removal requests, using
    provenance for impact assessment. (§15)
24. **Glossary expanded to include proper-noun + transliteration + do-not-translate conventions**, the
    most error-prone parts of heritage translation. (§6, §7)
25. **Funded-lane explicitly deferred** (donated-only for v0.1; metered surge drafting noted as future,
    requiring `fundedBudgetUsd`), keeping budget-cap discipline from CLAUDE.md in view. (§16, TASKS
    backlog)

---

## Review sign-off

**Reviewer:** Senior staff engineer + TPM (self-review against PLAN_SPEC.md, CLAUDE.md, and the
good-deed definition). **Date:** 2026-06-28. **Verdict:** Ready for maintainer review as v0.1.0 Draft.

**Completeness check.**
- All **17 required H2 sections** present and in the spec's order. ✔
- Metadata header matches house convention (Status/Version/Date/Owner/Lane). ✔
- TASKS.md present with schema-field mapping, milestone tables (M0–M3) matching this roadmap,
  acceptance criteria + DoD per milestone, a backlog, and a **schema-valid example Task JSON**
  (`verifiedNeed:false`, honest `outputLicense`). ✔
- Appendix A lists **25 specific, applied** improvements with locations. ✔

**Correctness / guardrail check.**
- **License/provenance:** open/PD/CC-or-granted only; two-layer rights; BLOCKING per-object
  prerequisite; snapshot+watcher; output license never more permissive than source. ✔
- **Privacy/PII:** no donor/visitor data; living-persons limited to public/sourced/necessary;
  defamation/privacy reviewer check; restricted data out of scope. ✔
- **Non-partisan:** contested histories handled neutrally, sourced, attributed, never adjudicated. ✔
- **HIGH-risk legal content:** contested ownership/restitution defaults to omit; otherwise
  **mandatory licensed cultural-property-attorney sign-off + jurisdiction-sourcing + "not legal
  advice" framing + non-partisan.** ✔
- **Cultural sensitivity:** CARE-aligned source-community review gate with binding community veto. ✔
- **Risk tier:** medium, with two named escalation classes above it; expert/community/legal sign-off
  required before "done" where applicable, per the good-deed definition. ✔
- **Lanes/architecture:** donated-only; agent-neutral schemas in core; no headless agent invocation;
  funded lane explicitly deferred (and would require `fundedBudgetUsd`). ✔
- **Honesty:** partner, reviewers, and counsel all marked **TO BE SECURED**; `verifiedNeed=false`
  until a partner is confirmed; success = *displayed*, not merged. ✔

**Fixes applied during review.**
- Aligned the M0 exit-metric wording with the metrics table's "effective from M1" caveat (avoids
  over-claiming a 100%/≥90%/≥95% gate before tooling exists).
- Ensured the example Task JSON in TASKS.md uses only schema-enumerated values and includes all
  required fields (validated field-by-field against `schemas.ts`).
- Made the HIGH-risk legal gate consistent across Exec summary, §6, §8, governance, and risks.

**Residual items requiring a human decision** (tracked in Open questions): securing a first partner
museum + rights grant; whether contested-ownership text is ever in scope (default: omit); per-source
output-license confirmations; per-language readability-metric choices; reviewer/cultural-authority/
counsel sourcing.
