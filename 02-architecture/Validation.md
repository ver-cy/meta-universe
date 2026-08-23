# Validation

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-006  
**Title:** Validation — Levels of Semantic Verification  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, [MMAS-Core](../02-architecture/MMAS-Core.md), [MMAS-Conformance](../02-architecture/MMAS-Conformance.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md)  
**Informative References:** [Certification](../06-ecosystem/Certification.md), [Compatibility-Matrix](../06-ecosystem/Compatibility-Matrix.md), [Requirements Index](../REQUIREMENTS-INDEX.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines **Validation** within the Meta-Model Architecture Standard (MMAS).

Validation is the process of verifying that a meta-model is well-formed, internally consistent, constitutionally compliant and ready to participate in federation. It is the bridge between an architectural specification and a trustworthy semantic model.

---

# 2. Scope

This document applies to:

- the validation of a single meta-model and its artifacts;
- the validation of imported external standards;
- the role of validation across the meta-model lifecycle;
- the relationship between validation and [Conformance](../02-architecture/MMAS-Conformance.md) and [Certification](../06-ecosystem/Certification.md).

It does not mandate a specific validation tool or implementation.

---

# 3. Principles

- **Validation is layered.** Different concerns are verified at different levels.
- **Validation is continuous.** A model is validated throughout its lifecycle, not once.
- **Validation is explainable.** Every result identifies what was checked and why it passed or failed.
- **Validation is technology-independent.** It verifies semantics, not storage or transport.

---

# 4. Dimensions of Validation

Validation answers four progressively deeper questions:

1. Is the model **well-formed**? (syntax and structure)
2. Is the model **internally consistent**? (semantics)
3. Does the model **obey the Constitution**? (constitutional compliance)
4. Can the model **participate in federation**? (interoperability)

These questions map onto the validation levels below.

---

# 5. Validation Levels

The Meta-Universe defines a layered validation model. Each level assumes the levels below it have passed.

| Level | Name | Verifies |
|-------|------|----------|
| **V0** | Syntax | The artifacts are syntactically valid and parseable. |
| **V1** | Structural | The model conforms to the MMAS composition hierarchy (Meta-Model → Bundles → Layers → Objects → Properties / Relationships / Events / Contracts / Projections → Manifest). |
| **V2** | Semantic | The model is internally consistent: identities are unique, references resolve, relationships are well-typed, naming is canonical. |
| **V3** | Constitutional | The model preserves every applicable [Constitutional](../01-constitution/Meta-Universe-Constitution.md) article (identity, provenance, traceability, projection separation, context). |
| **V4** | Federation | The model can participate in federation: it exposes public schemas, declares Semantic Contracts, supports Projection exchange and version negotiation. |
| **V5** | Runtime *(optional)* | The model's live instances remain consistent with the model, and observed reality does not contradict declared semantics. |

V0–V3 are **mandatory** for any MMAS-conformant model. V4 is required for any model that participates in [federation](../03-federation/MUFP.md). V5 is OPTIONAL and applies to running implementations.

---

# 5a. Abstract Test Procedures

Each validation level is defined by a set of **Abstract Test Procedures (ATPs)** — checks that a conforming validator SHALL perform. Each check has a stable identifier (`V<level>-<nn>`), a severity on failure, and the normative requirement(s) it enforces (by ID, from the [Requirements Index](../REQUIREMENTS-INDEX.md)). ATPs make conformance reproducible: two validators applying these checks to the same model SHALL reach the same verdict.

## V0 — Syntax

| Check | Verifies | On fail | Enforces |
|-------|----------|---------|----------|
| `V0-01` | The document parses as well-formed JSON (or YAML losslessly convertible to it) in UTF-8. | Error | `MUIF-R02`, `MUIF-R03` |
| `V0-02` | `muif.version` is present and equals `"1.0"`. | Error | `MUIF-R01` |

## V1 — Structural

| Check | Verifies | On fail | Enforces |
|-------|----------|---------|----------|
| `V1-01` | The document validates against `manifest.schema.json` and the referenced primitive schemas. | Error | `MUIF-R01` |
| `V1-02` | Every primitive declares its `muifType` and all required fields. | Error | `MUIF-R01` |
| `V1-03` | The Composition Hierarchy is present (a `metaModel` plus at least one bundle or object). | Warning | `MMAS-CORE` composition |

## V2 — Semantic

| Check | Verifies | On fail | Enforces |
|-------|----------|---------|----------|
| `V2-01` | All `id` values are unique within the document. | Error | `MUC-R03` |
| `V2-02` | Every internal reference (`relationship.source`/`target`, `event.subject`, `projection.subject`/`contract`) resolves to a declared `id` or an explicitly declared federated identity. | Error | `MUC-R15` |
| `V2-03` | Every CSN matches the canonical pattern and each namespace used is declared. | Error | `NAME` (CSN) |
| `V2-04` | Every `relationship.kind` is a declared or known Relationship Profile class. | Warning | `REL` (profile) |
| `V2-05` | A self-declared `metaModel.fingerprint`, if present, equals the fingerprint computed per [MMAS-Interchange](../02-architecture/MMAS-Interchange.md). | Error | `MUIF-R12`, `MUIF-R18` |

## V3 — Constitutional

| Check | Verifies | On fail | Enforces |
|-------|----------|---------|----------|
| `V3-01` | Every Object has a unique, persistent identity. | Error | `MUC-R03`, `MUC-R04` |
| `V3-02` | Every significant fact declares an owner and provenance. | Error | `MUC-R12`, `MUC-R13`, `MUC-R14` |
| `V3-03` | No Projection redefines the identity of its subject. | Error | `MUC-R11` |
| `V3-04` | Every externally exposed Projection is governed by a Contract and declares a purpose. | Error | `MUC-R21`, `MUC-R22`, `MUC-R25` |
| `V3-05` | Every semantic fact exists within an explicit context. | Warning | `MUC-R08`, `MUC-R10` |
| `V3-06` | Origin, ownership, evolution and dependencies are determinable. | Warning | `MUC-R15`, `MUC-R16` |

## V4 — Federation

| Check | Verifies | On fail | Enforces |
|-------|----------|---------|----------|
| `V4-01` | The public schema is discoverable without exposing underlying data. | Error | `MUC-R17`, `MUC-R18`, `MUC-R19`, `MUC-R20` |
| `V4-02` | A Semantic Contract is declared for every externally exchanged Projection. | Error | `MUC-R21` |
| `V4-03` | A version and a Semantic Fingerprint are published for negotiation. | Error | `MUIF-R12` |
| `V4-04` | Semantic Mappings are present for every imported external standard. | Warning | `EXT` (Semantic Package) |

## V5 — Runtime *(optional)*

| Check | Verifies | On fail | Enforces |
|-------|----------|---------|----------|
| `V5-01` | Live instances conform to the declared model. | Info | — |
| `V5-02` | No semantic drift between the declared model and observed reality. | Info | — |

A validator MAY add checks, but SHALL implement at least the Error-severity checks of every level it claims to verify.

---

# 6. Severity Classification

A validation result SHALL classify each finding by severity:

- **Error** — a violation that prevents conformance at the relevant level.
- **Warning** — a concern that does not block conformance but SHOULD be addressed.
- **Info** — an observation or recommendation.

A model passes a level only when no **Error** remains unresolved at that level.

---

# 7. Validation Report

A validation run SHALL produce a **Validation Report** that includes:

- the model identity and version (with its [Semantic Fingerprint](../02-architecture/Versioning.md));
- the highest validation level achieved;
- every finding, with severity, location and explanation;
- the validator identity and the validation timestamp.

For each level attempted, the report SHALL record the status of every ATP check (Section 5a) by check ID. The machine-readable structure is defined by [`schemas/validation-report.schema.json`](../schemas/validation-report.schema.json); a worked example is [`examples/minimal-person/validation-report.json`](../examples/minimal-person/validation-report.json), which reports the minimal-person model passing V0–V4 and records its verified Semantic Fingerprint.

The report is itself a traceable artifact and MAY be referenced by a [Conformance Statement](../02-architecture/MMAS-Conformance.md) or a [Certificate](../06-ecosystem/Certification.md).

---

# 8. Validation of Imported Standards

When a meta-model imports an external standard as a [Semantic Package](../02-architecture/Extension-Model.md), the imported package SHALL be validated:

- its declared namespaces and selected objects resolve;
- local extensions do not modify the imported model in prohibited ways;
- semantic mappings are well-formed;
- the imported version falls within the declared compatible range.

---

# 9. Continuous Validation

Validation SHALL be applied across the meta-model lifecycle:

- on creation, before publication;
- on every change, as part of the [Change Process](../01-constitution/Change-Process.md);
- on import of an external standard or another model;
- before establishing or amending a [federation](../03-federation/Federation-Lifecycle.md).

A change that lowers a model's achieved validation level SHALL be treated as a significant change under the Change Process.

---

# 9a. Outcome Drift Detection

Levels V0–V4 verify that a model is *correct*. They do not verify that it is still
*achieving its purpose*. A model can be perfectly valid — every check green — while
the reality it describes drifts away from the intent it was built for.

**Outcome Drift** is the divergence between a declared purpose or hypothesis (held
in the model, e.g. an Object's stated intent or a business hypothesis) and the
observed outcome (a [hot descriptive fact](../04-core-concepts/Virtual-Projection.md)
read through a Virtual Projection). It is detected by a background audit — a
"ghost" auditor — that continuously compares the two:

> *The code is valid, the tests are green, but the metric the change was made to
> improve is falling.* → raise an Outcome Drift signal: technically conformant,
> purpose unmet; the model's hypothesis SHOULD be revisited.

Outcome Drift detection is part of optional **V5 (Runtime)** validation. It SHALL
NOT block structural conformance (a drifting model is still valid), but a detected
drift SHOULD be recorded as an [Event](../04-core-concepts/Event.md) and surfaced
to the owner. It connects the [Provenance Graph](../02-architecture/Provenance-Graph.md)
(*which intent does this serve?*) to live outcomes (*is that intent being met?*).

---

# 10. Relationship to Conformance and Certification

Validation, Conformance and Certification are distinct:

- **Validation** verifies the model against the levels defined here.
- **[Conformance](../02-architecture/MMAS-Conformance.md)** declares which standards and maturity levels the model claims (in particular, MMAS level **A4 Validated** requires passing V0–V3, and V4 where federation applies).
- **[Certification](../06-ecosystem/Certification.md)** is independent confirmation of those claims.

---

# 11. Architectural Invariants

- Validation SHALL be layered (V0 through V5).
- A higher level SHALL assume the lower levels have passed.
- A model SHALL NOT claim a validation level it has not achieved.
- Every validation result SHALL be explainable and traceable.

---

# Future Directions

The validation model defined here verifies a single meta-model. Several broader forms of verification are anticipated and would form a dedicated **Semantic Validation Framework (SVF)**:

- **Cross-Model Validation** — consistency across several meta-models (e.g. Employee MM ↔ Department MM ↔ Project MM).
- **Cross-Universe Validation** — consistency of a federation between independent Universes.
- **Runtime Drift Detection** — divergence between a declared model and the real state of the world.
- **AI Reasoning Validation** — verification that an AI agent's conclusions do not contradict the constraints and semantics of the model.

These extend beyond base MMAS validation and are recorded here as candidate future standards (see [Roadmap](../06-ecosystem/Roadmap.md)).

---

# Final Statement

> Validation is how a meta-model earns trust: not by assertion, but by passing, level after level, the checks that prove it is well-formed, consistent, lawful and ready to federate.
