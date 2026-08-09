# Packaging Profiles

**Meta-Universe Specification - Entity Core Exploration**

**Document ID:** ECORE-003 (candidate MU-V3-ECORE-003)  
**Title:** Entity Core - Packaging Profiles: One Graph, Many Packagings  
**Document Class:** Normative draft (pre-normative until accepted)  
**Version:** 0.1  
**Status:** Working Draft (standard-evolution exploration, entity-core branch)  
**Normative References:** Entity-Core-Direction (ECORE-001), Entity-Graph-Model (ECORE-002), Semantic Fingerprint (ARCH-009), MMAS-Interchange (MUIF), Model-Traversal-and-Layout (ARCH-017), Data-Mastership (ARCH-018), Versioning (ARCH-002), Naming-Conventions (ARCH-003), Validation (V0-V5)  
**Informative References:** Interface-Bindings (ECORE-004), Projection (CORE-009), Virtual Projection (CORE-012), MMAS-Composition (ARCH-016)  
**License:** Apache-2.0

---

# 1. Purpose

The entity core direction (ECORE-001) refocuses the standard on three things: defining entity properties and methods, a set of physical packaging formats, and a set of access interfaces with one uniform security description. This document specifies the second of the three: the **packaging profile**.

A Meta-Model in the entity core view is a single **semantic graph**: entities with properties and methods, arranged in bundles and layers, carrying questions, findings and records (ECORE-002). That graph can be physically packaged in many ways: as a tree of Markdown files, as a MUIF JSON document, as rendered HTML, as tables in a relational database. Each packaging serves a different consumer; none of them is the model. The model is the graph; a packaging is a carrier.

This document defines what makes a packaging lawful: the profile concept, the four initial profiles (MD, JSON, HTML, DB), the description protocol every packaging must carry, the round-trip rules that keep all packagings equivalent, and the extension rule for future profiles.

---

# 2. Scope

This specification governs:

- the definition and registration of packaging profiles;
- the four initial profiles: MD, JSON, HTML, DB;
- the description protocol (discoverable manifests) for every packaging;
- profile-to-profile conversion and its equivalence guarantee.

It does not govern how a consumer reaches a packaging over a wire or a protocol: that is [Interface-Bindings](Interface-Bindings.md) (ECORE-004). It does not redefine the entity model: properties, methods, questions, findings and records are defined in ECORE-002 and are only carried here.

---

# 3. The Packaging Profile Concept

## 3.1 One graph, many packagings

A **packaging profile** is a named, versioned specification of how the semantic graph of ECORE-002 is laid out in a particular carrier technology. A **packaging** is a concrete instance: this repository, this JSON file, this database.

The governing rule:

> All packagings of the same model version SHALL be **fingerprint-equivalent**: the Semantic Fingerprint (ARCH-009) computed over the semantic core recovered from any conformant packaging SHALL be identical.

The fingerprint is computed per the canonicalization algorithm of ARCH-009 over the profile-independent semantic core (the MUIF semantic core), never over the carrier bytes. A byte hash of a packaging identifies a file; only the Semantic Fingerprint identifies the model. Two packagings may differ in every byte and still be the same model; two packagings with different fingerprints are different models regardless of how similar they look.

## 3.2 What a profile must specify

Every profile specification SHALL define:

1. **Carrier mapping**: how each primitive of the entity model (entity, property, method, bundle, layer, question, finding, record) maps to carrier units (files, JSON nodes, HTML elements, table rows);
2. **Manifest discovery**: the profile-specific well-known mechanism by which a reader finds the manifest (Section 4) without out-of-band knowledge;
3. **Findings enumeration**: the mechanical procedure that lists every Finding in the packaging, with a coverage proof (Section 4.3);
4. **Semantic core extraction**: the procedure that recovers the MUIF semantic core from the carrier, so the Semantic Fingerprint (ARCH-009) can be computed;
5. **Normative and informative split**: which carrier content is semantic and which is presentation (Section 10);
6. **Origin discipline**: how the profile marks authored, harvested and generated content, per ARCH-017 Â§9 and ARCH-018.

A packaging that satisfies its profile on all six points is **conformant**; a reader facing a conformant packaging never guesses.

---

# 4. The Description Protocol

## 4.1 The manifest

Every packaging SHALL carry a discoverable **manifest**. The manifest is the generalization of the ARCH-017 entry point (`manifest.yaml`) to carriers that are not file trees. It SHALL declare, at minimum:

| Field | Meaning |
|-------|---------|
| `profile` | The packaging profile name (registry id, ARCH-003) |
| `profile_version` | The profile version (ARCH-002) |
| `spec_version` | The entity core specification version this packaging conforms to |
| `entity_roots` | The root entities of the graph: for each, registry id plus CSN, Namespace, version, and Semantic Fingerprint (ARCH-009) |
| `findings_enumeration` | The name of the profile-defined procedure, view or index that enumerates all Findings |
| `semantic_fingerprint` | The fingerprint of the whole packaged graph |
| `mastership` | Pointer to the Mastership Register content (ARCH-018 `sources.yaml`), inline or by reference |
| `generated_at` / `observed_at` | When this packaging was produced, and, for mirrors, when the master was last observed |

Registry id plus CSN is the only normative identity of the packaged entities; acronyms appearing in a packaging are display aliases.

## 4.2 Discovery per carrier

The manifest is only useful if a reader can find it. Each profile fixes the location:

- **MD**: `manifest.yaml` at the repository root, exactly as ARCH-017 Â§4;
- **JSON**: the top-level MUIF manifest object;
- **HTML**: a machine-readable manifest element in every rendered page and a well-known document at the packaging root (Section 7);
- **DB**: the description protocol table `_vercy_manifest` (Section 8).

## 4.3 The completeness rule, generalized

ARCH-017 Â§7 proves, for file trees, that no file is left behind. The entity core generalizes the rule to every carrier:

> A conformant reader SHALL be able to enumerate **all Findings** in a packaging and prove that none was missed. Every carrier unit falls into exactly one of three classes: **enumerated** (carries semantic content and is reachable from the manifest), **well-known** (a reserved location or table with predefined meaning), or **excluded** (declared as carrying no model meaning). Orphans and ambiguous units are validation failures.

For the MD profile this is literally the ARCH-017 coverage check. For the JSON profile it is schema validation plus the closed-world property of a single document. For the HTML and DB profiles it is defined in Sections 7 and 8. The coverage check is part of structural validation (V1) in every profile.

---

# 5. The MD Profile

**Ancestor:** ARCH-017 (Model-Traversal-and-Layout) plus MMAS-Package. The MD profile is the authoring profile: the layout in which humans and agents write.

Rules:

- The packaging is a file tree conforming to ARCH-017: entry point `BOOTSTRAP.md` plus `manifest.yaml`, bundles and layers in declared order, well-known locations (`canon/`, `raw/`, `artifacts/`, `sources.yaml`) with their ARCH-017 meanings.
- Every semantic file is a `.md` file with **YAML front matter**. The front matter carries the machine-readable semantic core of the unit: identity (ARCH-003), kind, the entity, property, method, question, finding or record payload fields defined by ECORE-002. The Markdown body carries the human narrative.
- Classification uses ARCH-017 `kind_rules`: file names carry the kind by convention (`{kind}-{id}-{memo}.md`), declared once in the repository manifest as ordered match rules; the first matching rule wins; a file matched by no rule is an orphan.
- Findings enumeration = the canonical walk (ARCH-017 Â§10) restricted to files whose kind resolves to `finding` (or a declared sub-kind of it), plus the coverage check.
- Semantic core extraction = collect the front matter of all enumerated files, assemble per ECORE-002, canonicalize per ARCH-009. The Markdown body is non-semantic unless a front matter field explicitly promotes a named body section into the core.
- Origin discipline is inherited whole from ARCH-017 Â§9: authored, harvested, generated, with the well-known locations implying origin.

Normative content: front matter, manifests, `sources.yaml`, promoted body sections. Informative content: all other body prose, diagrams, `docs/`.

---

# 6. The JSON Profile

**Ancestor:** MUIF (MMAS-Interchange). The JSON profile is the interchange profile: the packaging that travels between tools and universes.

Rules:

- The packaging is a MUIF document: a manifest object referencing the primitives, serialized as canonical JSON (RFC 8259, UTF-8); YAML 1.2 authoring is permitted and SHALL be losslessly convertible, per MUIF Â§4.
- The entity core primitives extend the MUIF document model: alongside the `muifType` discriminators of MUIF, this exploration adds `Entity`, `Method`, `Question`, `Finding`, `Record` types, defined by JSON Schemas (draft 2020-12) in the entity core schema set. The extension SHALL follow the MUIF extension conventions so that a v1 MUIF reader degrades gracefully (unknown types are preserved, not dropped).
- Manifest discovery is trivial: the document root is the manifest.
- Findings enumeration = all nodes with `muifType: Finding`; the closed-world property of a single document makes the coverage proof a schema validation (V1).
- Semantic core extraction follows MUIF: project the document to the semantic core, excluding the non-semantic keys of MUIF Â§5 (`displayName`, `description`, keys beginning with `_` or `x-ui`, and the rest of the MUIF Â§5 list). Fingerprinting is then ARCH-009: normalize, serialize canonically, hash.

Normative content: the entire MUIF semantic core. Informative content: the non-semantic keys of MUIF Â§5.

The JSON profile is the **reference profile** for equivalence: when two packagings disagree about the semantic core, the dispute is settled by converting both to the JSON profile and comparing canonical forms.

---

# 7. The HTML Profile

**Ancestor:** the rendered artifacts of ARCH-017 (`artifacts/`), promoted from disposable view to conformant packaging. The HTML profile is the reading profile: what a browser, a search engine, or a person sees.

The problem it solves: a rendered page is normally a dead end, a projection with no way back. The HTML profile requires the rendering to carry its own semantics, so that a reader with nothing but the pages can recover every Finding.

Rules:

- Every page SHALL embed a machine-readable annotation block: a `<script type="application/vercy+json">` element containing the MUIF JSON (Section 6) of every primitive the page renders. Rendered prose is a projection of the annotation, never the other way around.
- Element-level annotation MAY additionally mark rendered fragments with `data-vercy-id` and `data-vercy-kind` attributes, linking visible text to the primitive it renders; this is informative navigation aid, not the semantic carrier.
- The packaging root SHALL serve a well-known manifest document (`/.well-known/vercy-manifest.json` or, for file-system packagings, `vercy-manifest.json` at the root) carrying the Section 4 manifest plus the complete page inventory: every page URL, and for each page, the ids of the primitives it carries.
- Findings enumeration = the page inventory joined with the per-page annotation blocks. The coverage proof: every Finding id listed in the manifest inventory SHALL be present in exactly one page's annotation block; a Finding rendered without annotation, or annotated on no inventoried page, is an orphan (V1 failure).
- Semantic core extraction = concatenate the annotation blocks per the inventory, assemble the MUIF document, then canonicalize and fingerprint per ARCH-009. The rendered HTML markup, styling and scripts are non-semantic in their entirety.
- HTML packagings are **generated**, never authored (ARCH-017 Â§9): they declare their generator and input fingerprint, and deleting and rebuilding them SHALL be lossless.

Normative content: annotation blocks and the well-known manifest. Informative content: everything the eye sees.

---

# 8. The DB Profile

**Ancestor:** none in v2; this is the new carrier the entity core adds. The DB profile is the operating profile: the packaging that serves queries, joins and row-level access control.

## 8.1 Relational mapping

A conformant DB packaging SHALL provide the following base tables (names are normative; a deployment MAY prefix them with a schema name declared in the manifest table):

| Table | Carries |
|-------|---------|
| `entities` | One row per entity: registry id, CSN, Namespace, version, semantic fingerprint |
| `bundles` | One row per bundle: identity, owning entity, single responsibility, walk order |
| `layers` | One row per layer: identity, owning bundle, walk order, declared meaning |
| `questions` | One row per question: identity, owning layer, text, status |
| `findings` | One row per finding: identity, the question or layer it answers, payload (semantic fields per ECORE-002), provenance, origin, observed_at |
| `records` | One row per record: identity, owning entity, payload, origin, provenance, observed_at |

Properties and methods of entities MAY be carried as additional tables (`properties`, `methods`) or as structured columns on `entities`; the profile version pins the choice, the manifest table declares it.

The core | landscape | kernel role triad is a property of a registered meta-model as a registry node, never of the entities a model describes; it therefore has no column in `entities` (see Section 8.3 for the one place it may be surfaced).

## 8.2 Views

The packaging SHALL provide read views over the base tables; at minimum:

- `v_findings`: every Finding joined with its question, layer, bundle and entity, in canonical walk order. This view is the declared `findings_enumeration` of the manifest.
- `v_walk`: the canonical walk (ARCH-017 Â§5 ordering) as rows: one row per carrier unit, with kind and origin.
- `v_entities`: the entity graph with resolved edges.

Views are derived and informative; base tables are normative. An implementation MAY add projection views (CORE-009) and virtual projection views (CORE-012) freely; they never enter the fingerprint.

## 8.3 The description protocol table: `_vercy_manifest`

Discovery is the hard problem of a database: a connecting reader sees only a catalog of tables. The DB profile therefore reserves one table:

> `_vercy_manifest` (`key` text primary key, `value` text): the Section 4 manifest as key-value rows, with structured values as JSON text.

Required keys: `profile` (= `db`), `profile_version`, `spec_version`, `entity_roots` (JSON array), `findings_enumeration` (= the qualified name of `v_findings`), `semantic_fingerprint`, `mastership` (the ARCH-018 register as JSON), `schema_map` (JSON object naming every base table and view of this packaging, including any prefix), `generated_at`, `observed_at`, and for synchronized packagings `last_sync_at`, `sync_cadence`, `staleness_limit`.

Optional key: `model_role`. If the packaged model is itself a registered node of a composition graph, its node role (the core | landscape | kernel triad) MAY be surfaced here, once, as a property of the packaging manifest; it never appears per entity row.

A conformant reader connects, reads `_vercy_manifest`, learns the schema map, and proceeds mechanically. A database without `_vercy_manifest` is not a DB-profile packaging, whatever its tables look like.

## 8.4 Coverage

The coverage proof for the DB profile: every row of every table named in `schema_map` is enumerated content; tables present in the database but absent from `schema_map` SHALL be listed under an `excluded` key with the assertion that they carry no model meaning; a table in neither place is an orphan (V1 failure). The row count of `v_findings` SHALL equal the count of `findings` base rows.

---

# 9. Extension Rule for Future Profiles

The profile set is open: `.yaml` single-file packagings, `.csv` table exports, columnar stores, document databases and object stores are all plausible carriers. A future profile enters the standard only by **registration**, never by convention:

1. The profile author writes a profile specification covering all six points of Section 3.2;
2. The profile receives a registry id (ARCH-003) and a version (ARCH-002); the registration lands as a Model Registration Record in the ver-cy registry repository;
3. The profile demonstrates round-trip conformance (Section 10) against the JSON reference profile on at least one non-trivial model;
4. Until registered, a packaging in a new carrier is an artifact (ARCH-017 Â§6), not a packaging.

Profile enumerations in this document are the initial set, not a ceiling; the normative set of profiles is the registry.

---

# 10. Round-Trip Rules

1. For every ordered pair of registered profiles (A, B), a conversion A to B SHALL exist that preserves the semantic core. The conversion is total over conformant packagings: it consumes the manifest and the enumeration, never scrapes.
2. **Fingerprint preservation**: `fingerprint(A) = fingerprint(convert(A to B))`, computed per ARCH-009 in both cases. A conversion that changes the fingerprint is broken, whatever else it preserves.
3. **Round-trip closure**: converting A to B and back SHALL yield a packaging with the same fingerprint as A. Byte identity is NOT required and NOT expected: formatting, ordering of set-valued collections, and non-semantic decoration may differ.
4. Non-semantic content (descriptions, display names, rendered prose, styling) SHOULD be carried through conversions on a best-effort basis and MAY be lost; its loss is not a conformance failure.
5. Conversions SHALL be possible offline, from the packaging alone: a packaging that requires consulting a live system to be converted is not self-contained and is non-conforming.
6. Provenance of a conversion is a generation event: the output declares its generator, its input packaging and the input fingerprint (ARCH-017 Â§6, `artifacts/` discipline generalized).

---

# 11. Normative vs Informative, Per Profile

| Profile | Normative (semantic, fingerprinted) | Informative (never fingerprinted) |
|---------|-------------------------------------|-----------------------------------|
| MD | YAML front matter, manifests, `sources.yaml`, promoted body sections | Markdown prose, diagrams, `docs/`, `BOOTSTRAP.md` |
| JSON | The entire MUIF semantic core | Non-semantic keys per MUIF Â§5 |
| HTML | Annotation blocks, the well-known manifest | All rendered markup, styles, scripts |
| DB | Base tables, `_vercy_manifest` | Views, indexes, physical schema details |

Every profile carries this split in its specification; a reader determines what is binding without opening the content.

---

# 12. Validation

- **V0 (constitutional)**: the packaging claims no authority it does not have; mirrors are labeled as mirrors.
- **V1 (structural)**: the manifest exists, parses, and is discoverable at the profile's well-known location; the coverage check of Section 4.3 passes; the DB schema map is total.
- **V2 (semantic)**: the extracted semantic core validates against the ECORE-002 schemas; identities conform to ARCH-003; versions to ARCH-002.
- **V3 (compositional)**: entity edges resolve; compositional roles bind to ARCH-016.
- **V4 (interchange)**: the declared `semantic_fingerprint` equals the recomputed fingerprint (ARCH-009); round-trip closure against the JSON reference profile holds.
- **V5 (runtime)**: for synchronized packagings, `observed_at` and staleness limits are honored per ARCH-018.

---

# 13. Invariants

- **ECORE-I20**: One semantic graph, any number of packagings; the graph, not the packaging, is the unit of identity, and its identity is registry id plus CSN, Namespace, version, pinned by the Semantic Fingerprint (ARCH-009), never a byte hash.
- **ECORE-I21**: Every packaging carries a discoverable manifest per the description protocol; a packaging a reader must guess about is non-conforming.
- **ECORE-I22**: Every packaging supports total enumeration of Findings with a coverage proof; silent loss is impossible in every carrier, not only in file trees.
- **ECORE-I23**: Profile-to-profile conversion SHALL preserve the Semantic Fingerprint; round-trip closure holds for every registered profile pair.
- **ECORE-I24**: Non-semantic content never affects the fingerprint and may be lost in conversion without breaking conformance.
- **ECORE-I25**: Every profile declares its normative and informative split; bindingness is declared, never inferred from format.
- **ECORE-I26**: Packaging never redefines semantics; it only makes the graph reachable in a carrier (extends ARCH-017 Â§12).
- **ECORE-I27**: Mastership (ARCH-018) is packaging-independent: the Mastership Register travels with every packaging, and a mirror packaging is a mirror in every profile.
- **ECORE-I28**: New profiles enter only by registration in the ver-cy registry; convention is not conformance.

---

# Final Statement

A model that exists only as files is a model for people who like files. The entity core makes the graph primary and the carrier plural: write it as Markdown, ship it as JSON, read it as HTML, query it as tables, and let one fingerprint prove that all four are the same thing.
