# TASKS — multilingual-museum-labels

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: J. Carter (acting maintainer) · Lane: donated

The backlog for the `multilingual-museum-labels` good-deed project. Read alongside
[PLAN.md](./PLAN.md). Milestones (M0–M3) match the roadmap there.

## How these tasks map to Elyos

Each task below becomes an **Elyos Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- **id** — stable slug id, e.g. `multilingual-museum-labels-schema-001` (table column `ID`).
- **title** — the task title.
- **project** — always `multilingual-museum-labels`.
- **type** — one of `code | research | writing | data | design-spec | maintenance` (table `Type`).
- **lane** — `donated` for all current tasks (no funded/API execution). Funded tasks would need
  `fundedBudgetUsd`; none here.
- **priority** — `high | medium | low`.
- **domain** — array, e.g. `["museums","translation","heritage","licensing"]`.
- **riskTier** — `low | medium | high`. Description/translation/sensitivity tasks are **medium**
  (need a domain-aware/bilingual reviewer); pure tooling/schema/process tasks are **low**; any task
  that could touch **contested legal ownership/restitution** is **high** (licensed-attorney gate). (table `Risk`)
- **urgent** — boolean (default false; no live emergency).
- **deliverable** — `pr | dataset | document | translation` (table `Deliverable`).
- **tokenEstimate** — `small | medium | large` (table `Size`).
- **status** — `open | in-progress | review | delivered | done` (all start `open`).
- **context / objective** — why + what.
- **acceptanceCriteria[]** — checkable bullets (listed below tables for key tasks).
- **resources[]** — links/paths (schemas, guides, glossary, source URLs/grants, standards).
- **output** — path/description of the produced artefact.
- **requestor** — partner/requestor; `TO BE SECURED` until a partner museum is confirmed.
- **verifiedNeed** — boolean; **`false`** wherever value depends on an unsecured partner.
- **outputLicense** — **MIT** for code/tooling and project-metadata datasets; **CC BY 4.0** for
  descriptions built on PD/open facts with no share-alike; **CC BY-SA 4.0** where a source is
  share-alike; **per the partner grant** for partner-supplied facts. Never more permissive than the source.

---

## Milestone M0 — Foundation & cold-start (no partner required)

Goal: build the reusable machinery and prove the full pipeline on **openly-licensed exemplar
objects**, end-to-end except partner adoption.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| multilingual-museum-labels-schema-001 | Content schemas (object/description/provenance/review/glossary) + CI structural check | code | medium | low | pr | — | Maintainer |
| multilingual-museum-labels-rights-001 | Per-object two-layer rights model (facts vs. image) + source allow-list policy | data | small | low | dataset | — | License reviewer / Maintainer |
| multilingual-museum-labels-guide-001 | Plain-language writing guide + reading-level targets (+ attestation fallback) | writing | small | low | document | — | Maintainer |
| multilingual-museum-labels-guide-002 | Cultural-sensitivity + contestation triage guide (CARE; sensitive-heritage; legal-escalation) | writing | medium | medium | document | — | Cultural-authority advisor / Maintainer |
| multilingual-museum-labels-review-001 | Reviewer checklist (fidelity, plain-language, terminology, neutrality, cultural, privacy) | writing | small | low | document | guide-001, guide-002 | Maintainer |
| multilingual-museum-labels-review-002 | Reviewer-handoff template + COI/independence + sign-off recording | writing | small | low | document | review-001 | Maintainer |
| multilingual-museum-labels-glossary-001 | Glossary for 1 language pair (terms, proper nouns, transliteration, do-not-translate) | data | small | medium | dataset | schema-001 | Qualified bilingual reviewer |
| multilingual-museum-labels-license-000 | **BLOCKING:** confirm facts licensable + credit line + image decision for each exemplar object | research | small | low | document | rights-001 | License reviewer / Maintainer |
| multilingual-museum-labels-exemplar-001 | Plain-language source descriptions for ≥3 openly-licensed exemplar objects | writing | medium | medium | document | schema-001, rights-001, guide-001, guide-002, license-000 | Domain-aware reviewer |
| multilingual-museum-labels-exemplar-002 | Translate the ≥3 exemplar descriptions into 1 target language | translation | medium | medium | translation | exemplar-001, glossary-001 | Qualified bilingual reviewer |
| multilingual-museum-labels-tooling-001 | Readability check + claim-to-source grounding self-check script | code | small | low | pr | schema-001, guide-001 | Maintainer |

**Acceptance criteria — key M0 tasks**

`schema-001` (content schemas + CI)
- `objectSchema`, `descriptionSchema`, `provenanceSchema`, `reviewSchema`, `glossarySchema` exported
  from `packages/schema/src/schemas.ts` and compiled/exposed via `validate.ts` (AJV + `ajv-formats`),
  matching the existing `taskSchema`/`registrySchema` pattern — **no vendor/agent-specific logic.**
- `objectSchema` captures separate `factsRights` and `imageRights` blocks, `sourcedFacts[]` (each with
  a `sourceRef`), `sensitivity`, `contestation`, and `eligibility`.
- A structural-check script parses each YAML/Markdown-front-matter artefact to JSON and validates it;
  wired into `pnpm test` so **CI fails on any malformed or non-conformant content file.**
- `pnpm build && pnpm test && pnpm lint` pass.

`rights-001` (two-layer rights model)
- Documents the **facts-vs-image** rights distinction and an allow-list policy of permitted source
  families (PD, CC0/CC BY/CC BY-SA open collections, partner-supplied-under-grant); excludes
  all-rights-reserved/unverified sources with a reason.
- Defines the **output-license decision** (CC BY 4.0 default for open facts; CC BY-SA 4.0 for
  share-alike sources; per-grant for partner facts) and the rule "never more permissive than source."
- Each future object record must carry a **snapshot** (committed copy + **SHA-256 hash** + web-archive
  URL where available) of the governing license/grant.

`license-000` (BLOCKING prerequisite of `exemplar-001`)
- For **each exemplar object**, confirm and record on its object record: (a) facts are **licensable**
  for a derivative plain-language description (open license or written grant); (b) the **required
  attribution/credit line** (verbatim); (c) **image rights** decision (include/exclude).
- If any is unconfirmed, the object is **rejected** and another openly-licensed object selected.
  `exemplar-001` **must not start** until this passes for the chosen objects.

`exemplar-001` (plain-language source descriptions)
- ≥ 3 openly-licensed objects each get a label-sized (≈40–120-word) plain-language description written
  **strictly from sourced facts** (every claim maps to a `sourceRef`).
- Each meets the configured **readability target** (or carries reviewer plain-language attestation),
  preserves proper nouns/dates/materials, and is **neutral** on any contested point.
- Agent **uncertainty flags** (`UNCERTAIN: …`) captured into `review.yaml` as `agentFlags`; **no
  sign-off while any flag is unresolved**; unresolved **grounding** flags force claim removal.
- Sensitivity/contestation triage run; any `sensitive-heritage`/`contested-legal` object is **escalated
  or excluded** per `guide-002` (not silently written).
- **Domain-aware reviewer sign-off recorded in the PR**, reviewer independent of drafting (COI declared);
  per-object license/attribution/provenance present and verified (manual check in M0).

`guide-002` (cultural-sensitivity + contestation triage)
- Defines the triage classes (`none | sensitive-heritage | restricted`; `none | noted | contested-legal`),
  the **CARE-aligned source-community/cultural-authority review** requirement (with binding community
  veto incl. "do not describe/image/display"), and the **HIGH-risk legal escalation** (default omit;
  else licensed cultural-property-attorney sign-off + jurisdiction-sourcing + "not legal advice" framing
  + non-partisan).

**M0 Definition of Done:** content schemas + structural CI check merged; plain-language guide,
cultural-sensitivity/triage guide, reviewer checklist, and handoff template merged; one language-pair
glossary started (≥ 40 entries); two-layer rights model + BLOCKING per-object license prerequisite
demonstrated; **≥ 3 openly-licensed exemplar objects taken end-to-end to a plain-language source
description + 1 reviewed translation each**, each passing readability, grounding, and a manual
license/attribution check; readability + grounding tooling green in CI. The 100% / ≥ 90% / ≥ 95%
metrics are **effective from M1** (M0 verifies exemplars manually plus the structural check). Partner
adoption deferred to M2 (so M0 deliverables carry `verifiedNeed: false`).

---

## Milestone M1 — Repeatability & reviewer network

Goal: make the pipeline repeatable and recruit/qualify reviewers.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| multilingual-museum-labels-reviewers-001 | Reviewer qualification criteria + onboarding (domain + bilingual + sensitivity) | writing | small | low | document | review-001 | Maintainer |
| multilingual-museum-labels-reviewers-002 | Recruit ≥2 qualified reviewers or engage a museum/GLAM-Wikimedia community | research | medium | low | document | reviewers-001 | Maintainer / Steward |
| multilingual-museum-labels-glossary-002 | Extend glossary + guides to a 2nd language pair | data | small | medium | dataset | glossary-001 | Qualified bilingual reviewer |
| multilingual-museum-labels-license-002 | License-check tooling (object record ↔ deliverable metadata) enforced in CI | code | medium | low | pr | schema-001, rights-001 | Maintainer |
| multilingual-museum-labels-watcher-001 | Automated source/grant-change watcher (hash-diff vs. snapshots) | code | small | low | pr | rights-001, schema-001 | Maintainer |
| multilingual-museum-labels-escalation-001 | Sensitivity + legal-escalation procedure finalised + dry-run on a contrived example | writing | small | medium | document | guide-002 | Cultural-authority advisor / Maintainer |
| multilingual-museum-labels-exemplar-003 | Second exemplar batch in a 2nd target language, reviewed | translation | medium | medium | translation | exemplar-001, glossary-002 | Qualified bilingual reviewer |

**Acceptance criteria — key M1 tasks**

`reviewers-001`
- Objective criteria for a **domain-aware reviewer** (heritage/museum literacy; can verify factual
  fidelity + plain language) and a **qualified bilingual reviewer** (native/near-native target +
  heritage-translation competence), plus **sensitivity awareness**.
- Defines **reviewer independence** (drafter ≠ sole reviewer), **COI declaration**, the
  community/cultural-authority requirement for sensitive items, and a **disagreement/conflict-resolution
  rule** (reconcile against sources/glossary → escalate to third reviewer/maintainer → conservative
  reading wins; recorded in `review.yaml`).

`license-002`
- Tooling validates each deliverable's metadata against its object record and **fails CI** if the
  credit line, required disclaimer, or provenance is missing, or if the output license is incompatible
  with (or more permissive than) the source rights. This is the **full source-compatibility
  enforcement** automated from M1 (M0 was structural-check + manual).

`watcher-001`
- Re-fetches allow-listed sources/grants, recomputes `snapshotHash`, and **flags drift** against
  stored snapshots for re-verification before further work or delivery; runs on a schedule/CI.

`escalation-001`
- The end-to-end sensitivity + legal procedure is documented and **dry-run** on a contrived
  `sensitive-heritage` and a contrived `contested-legal` example, demonstrating the correct routes
  (community review / attorney gate / omission) and that ungated material **cannot** reach sign-off.

**M1 Definition of Done:** qualification criteria published (independence, COI, sensitivity,
conflict resolution) and ≥ 2 qualified reviewers (or a museum/GLAM-Wikimedia community) engaged;
glossary + guides cover ≥ 2 language pairs; license check **enforced in CI** and **source/grant-change
watcher operating**; sensitivity/legal escalation procedure finalised and dry-run; a second exemplar
batch reviewed. **Steward named** (governance prerequisite for M2).

---

## Milestone M2 — First partner museum delivery (needs partner)

Goal: deliver an adopted label set. **All tasks gated on a secured partner museum + rights grant**
(`verifiedNeed` flips to `true` only when the partner + grant are confirmed).

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| multilingual-museum-labels-partner-001 | Secure first partner museum; written facts/image grant; agree objects + languages | research | medium | low | document | reviewers-002 | Steward / Maintainer |
| multilingual-museum-labels-ingest-001 | Ingest partner object facts + rights + sensitivity triage into object records | data | medium | medium | dataset | partner-001, schema-001, guide-002 | Domain-aware reviewer / License reviewer |
| multilingual-museum-labels-produce-001 | Produce ≥25 plain-language source descriptions from partner facts | writing | large | medium | document | ingest-001, guide-001 | Domain-aware reviewer |
| multilingual-museum-labels-translate-001 | Translate the set into ≥1 agreed target language | translation | large | medium | translation | produce-001, glossary-002 | Qualified bilingual reviewer |
| multilingual-museum-labels-delivery-001 | Package + deliver set; confirm museum displays/publishes it | writing | small | medium | document | translate-001, license-002 | Steward |

**Acceptance criteria — key M2 tasks**

`partner-001`
- Outreach (acting maintainer → Steward) targets the named candidate types (local historical
  societies/community museums, museum-development/small-museum networks, university teaching
  collections, library special collections, GLAM-Wikimedia partners), aiming for **≥ 3 serious
  conversations by end of M1.**
- **Pause/decision point:** if **no partner is secured by end of M1**, the maintainer makes an explicit
  **go / pivot / hold** decision (e.g., pivot to labels for *openly-licensed* collections only).
- A named small/under-resourced museum confirmed in writing as requestor; a **written facts/image
  rights grant** (permitted use, derivatives, credit line, output license); agreed object list +
  target language(s); reviewer coverage confirmed. On completion, related tasks update `requestor`
  and `verifiedNeed: true`.

`ingest-001`
- Each partner object gets an `object.yaml` with sourced facts (`sourceRef` per claim), `factsRights`
  + `imageRights`, snapshot (hash/archive) of the grant, and a completed **sensitivity + contestation
  triage**; ineligible/sensitive/contested objects are **flagged and routed**, not produced by default.

`delivery-001`
- Delivered set includes descriptions, translations, provenance, attribution/credit line + any
  disclaimer, reviewer sign-offs (incl. bilingual; community/legal where escalated); license check
  green; **museum confirms it displays/publishes the set in writing** (recorded in the PR/receipt).
  This is the first true **Definition of Shipped** event.

**M2 Definition of Done:** partner museum secured with written grant (`verifiedNeed=true`); ≥ 25
objects produced with reviewed source + ≥ 1 target language, all gates passed; the set **delivered and
confirmed displayed/published** by the museum.

---

## Milestone M3 — Scale program

Goal: scale to more objects/languages with sustained quality and tracked outcomes.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| multilingual-museum-labels-scale-001 | Produce + translate additional objects across ≥2 target languages | translation | large | medium | translation | delivery-001 | Qualified bilingual reviewers |
| multilingual-museum-labels-rotation-001 | Reviewer rotation + load balancing | maintenance | small | low | document | reviewers-002 | Maintainer |
| multilingual-museum-labels-outcomes-001 | Outcome tracking: factual-defect log + sensitivity-escape audit + feedback | data | small | low | dataset | delivery-001 | Steward |
| multilingual-museum-labels-maint-001 | Source/grant re-verification + glossary/guide maintenance cadence | maintenance | small | low | document | rights-001 | Maintainer |

**Acceptance criteria — key M3 tasks**

`outcomes-001`
- A maintained log capturing, per delivered set: display/adoption status, post-delivery **factual
  defects** (target 0), **sensitivity-handling escapes** (target 0), and partner/visitor usefulness
  feedback; feeds PLAN.md success metrics.

`maint-001`
- A documented cadence to re-verify object rights/grants (detect upstream/license/grant change via the
  stored snapshot) and refresh glossaries/guides; defines the **withdrawal procedure** if a license
  changes to forbid reuse **or a community requests removal.**

**M3 Definition of Done:** ≥ 25 objects across ≥ 2 target languages adopted (or a second partner
onboarded); reviewer rotation operating; outcome tracking + sensitivity-escape audit live;
source/grant maintenance cadence in effect; named sustainability owner.

---

## Backlog / future

Sized but unscheduled:

- **(medium) Partner export/print formats** — bilingual CSV for a label printer, simple bilingual PDF,
  or a Wikimedia Commons/Wikidata upload path, driven by partner need.
- **(medium) Image-rights helper** — a checklist/lookup distinguishing artwork vs. photograph
  copyright and PD-by-jurisdiction status, to speed `imageRights` decisions.
- **(small) Visitor-feedback loop** — optional QR-linked plain-language-clarity micro-survey if a
  partner agrees to collect it (privacy-reviewed; no PII).
- **(medium) Additional readability metrics** — per-language readability integrations beyond the
  first-language metric; reviewer-attestation templates for languages without metrics.
- **(large, funded — needs escrow) Surge production under funded lane** — metered drafting against a
  hard per-task budget for large object sets; would require `fundedBudgetUsd` and remains out of scope
  for v0.1.
- **(medium) Contested-history neutral-note workflow** — only if a partner requests and funds the
  HIGH-risk legal gate (licensed cultural-property attorney + jurisdiction-sourcing + "not legal
  advice"); default remains **omit.**

---

## Example task JSON

Schema-valid Task JSON for the first M0 task. `verifiedNeed` is **false** (no partner secured);
`outputLicense` is **MIT** because the content schemas + CI check are project tooling, not described
object content.

```json
{
  "id": "multilingual-museum-labels-schema-001",
  "title": "Content schemas (object/description/provenance/review/glossary) + CI structural check",
  "project": "multilingual-museum-labels",
  "type": "code",
  "lane": "donated",
  "priority": "high",
  "domain": ["museums", "heritage", "translation", "licensing", "schema"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "pr",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "multilingual-museum-labels produces plain-language, multilingual object descriptions for small museums, each with per-object license + attribution + provenance. Before any description is written, the project needs agent-neutral content schemas and a CI structural check so every object record, description, provenance, review, and glossary file is well-formed and conformant. The defining constraint is 'never invent an object': every factual claim must trace to a sourced fact, and rights for facts and image are tracked separately.",
  "objective": "Add objectSchema, descriptionSchema, provenanceSchema, reviewSchema, and glossarySchema to packages/schema/src/schemas.ts (AJV / JSON Schema draft-07), expose them via validate.ts like taskSchema/registrySchema, and wire a structural-check script into pnpm test so CI fails on any malformed or non-conformant content artefact.",
  "acceptanceCriteria": [
    "objectSchema, descriptionSchema, provenanceSchema, reviewSchema, glossarySchema exported from packages/schema/src/schemas.ts and compiled/exposed via validate.ts (AJV with ajv-formats), matching the existing taskSchema/registrySchema pattern with no vendor or agent-specific logic",
    "objectSchema captures separate factsRights and imageRights blocks, sourcedFacts[] each with a sourceRef, plus sensitivity, contestation, and eligibility fields",
    "A structural-check script parses each YAML or Markdown-front-matter artefact to JSON, validates it against the right schema, and is wired into pnpm test so CI fails on any malformed or non-conformant file",
    "pnpm build && pnpm test && pnpm lint all pass",
    "A changeset is added for the user-facing schema additions and commits are signed off (DCO)"
  ],
  "resources": [
    "C:/code/elyos/packages/schema/src/schemas.ts",
    "C:/code/elyos/planning/projects/multilingual-museum-labels/PLAN.md",
    "C:/code/elyos/CLAUDE.md",
    "Getty AAT/ULAN/TGN, Dublin Core, schema.org/CreativeWork (terminology/metadata reference)"
  ],
  "output": "PR adding the five content schemas to packages/schema, validate.ts wiring, the structural-check script, and a README documenting the content-file schemas",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "MIT"
}
```
