# Meta-Model Composition

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-016  
**Title:** Meta-Model Architecture Standard — Composition, Nesting and Connectors  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** Meta-Universe Constitution (MUC), MMAS-Core, [Extension-Model](Extension-Model.md), [Semantic-Mapping](../03-federation/Semantic-Mapping.md)  
**Informative References:** [Relationship](../04-core-concepts/Relationship.md), [Object](../04-core-concepts/Object.md), [Projection](../04-core-concepts/Projection.md), [Connector-Catalogue](../06-ecosystem/Connector-Catalogue.md), [External-Models-Registry](../06-ecosystem/External-Models-Registry.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

[Extension-Model](Extension-Model.md) defines how a Meta-Model **imports and extends**
an external standard. [Semantic-Mapping](../03-federation/Semantic-Mapping.md) defines
how two sovereign Meta-Models **align meaning** without merging. This document fills
the layer between them: **structural composition** — how the *Properties* of one
Meta-Model relate to *other Meta-Models*, and the rule for deciding, for any given
concept, whether it should be:

- a **literal Property** (a field) held by the Meta-Model itself; or
- an **embedded** nested Meta-Model (the Property's type *is* another model); or
- a **reference** to a separately governed entity or code list.

Without this layer the registered models are semantic islands: the same concept —
an address, a country, a money amount, a provenance record — is re-modelled
independently in dozens of Meta-Models with diverging shapes, so they duplicate
fields and cannot be composed, joined or validated together. This document defines
the principles, mechanisms and connectors that turn the catalogue of
[External Models](../06-ecosystem/External-Models-Registry.md) into a connected
fabric.

---

# 2. The Composition Problem

A Meta-Model author repeatedly meets a concept that *could* be a simple field but
is in fact a thing the wider ecosystem already models. Three failures follow from
treating every such concept as a local field:

- **Forking** — `street`, `city`, `postcode`, `country` modelled ad-hoc in one
  Meta-Model and differently in the next: the Address concept is forked and the two
  cannot interoperate.
- **Drift** — a country or currency list copied into a local enumeration silently
  diverges from the authority that maintains it.
- **Staleness** — an employer's attributes inlined into a Person rather than
  referenced: every Person carries a private, ageing copy of the same Organization.

Meta-Universe SHALL prefer **composition over duplication** — the structural
counterpart of the **extension over duplication** principle of
[Extension-Model](Extension-Model.md) §3. The remainder of this document makes that
preference operational.

---

# 3. Kinds of Concept

Every concept appearing in a Meta-Model SHALL be classified, for the purpose of
representation, as exactly one of the following kinds. The kind determines the
permitted composition mechanism (§4) via the decision rubric (§5).

| Kind | Definition | Test | Default representation |
|------|------------|------|------------------------|
| **Attribute** | A literal value with no independent identity, no internal structure, and no external authority over its values. | "Is it just a value the host owns?" | Property (field) |
| **Value Object** | A structured bundle of sub-values that travel together and are equal when their parts are equal; it has no identity of its own. | "Does it have ≥2 parts that only make sense as a unit?" | EMBED |
| **Entity** | A thing with its own identity and lifecycle, referenceable and shareable independently of any host. | "Can other Objects point at it; can it be created, versioned, owned on its own?" | REFERENCE |
| **Code / Classifier** | A member of a value set, classification or identifier scheme governed by an external authority. | "Is the set of allowed values maintained by someone else?" | REFERENCE (to the scheme) |
| **Facet** | A cross-cutting concern attached to many Objects regardless of domain — provenance, valid-time, policy, security marking, multilingual labels. | "Is this *about* the data rather than *part of* the domain payload?" | MIX-IN |

A concept's kind is a modelling decision, not an intrinsic truth: the same word
("address", "organization") may be an Entity in one Meta-Model and a Value Object
snapshot in another. The author SHALL record the chosen kind so that validators and
consumers can reason about it.

---

# 4. Composition Mechanisms

Six mechanisms connect Meta-Models. Each has a distinct coupling and sovereignty
profile. Two of them — **EXTEND** and **MAP** — are specified elsewhere and are
listed here only for completeness; this document specifies **EMBED**, **REFERENCE**
and **MIX-IN**.

| # | Mechanism | What it does | Coupling | Sovereignty | Specified in |
|---|-----------|--------------|----------|-------------|--------------|
| 1 | **EMBED** (composition) | A Property's type *is* another Meta-Model; the value travels inside the host as a nested Object with no independent identity. | Tight — host owns the composite | Nested model's *shape* is reused; its authority is preserved | **this document** |
| 2 | **REFERENCE** (association) | A Property holds an identifier resolved against an external entity or code scheme; the referent lives and is governed elsewhere. | Loose | Fully preserved — referent stays sovereign | **this document** |
| 3 | **MIX-IN** (facet / trait) | A cross-cutting Package's Properties are applied uniformly to many host Objects under their own namespace. | Orthogonal | Facet model stays authoritative | **this document** |
| 4 | **EXTEND** (specialization) | The host Meta-Model is-a / refines an imported model, adding constraints or Properties. | Tight (subtype) | Per import rules | [Extension-Model](Extension-Model.md) §8 |
| 5 | **MAP** (alignment) | Two sovereign models declare field equivalences without structural change. | None (structural) | Maximum | [Semantic-Mapping](../03-federation/Semantic-Mapping.md) |
| 6 | **ANNOTATE** (tagging) | A controlled-vocabulary concept is attached to a Property for meaning, not structure. | None | Maximum | this document (§4.3) |

## 4.1 EMBED

EMBED is used for **Value Objects**. The host Property is typed by another
Meta-Model (preferably one imported as a [Semantic Package](Extension-Model.md §4)),
and the embedded value:

- SHALL preserve the embedded model's namespace, version and
  [Semantic Fingerprint](Versioning.md);
- SHALL NOT be flattened into ad-hoc host Properties;
- has **no independent identity** in the host — it is a value, equal to any other
  embedded value with the same parts;
- contributes its shape to the host's own Semantic Fingerprint, so that two hosts
  that "have an address" can be shown to agree on what an address is.

EMBED is the correct mechanism precisely when a concept has internal structure that
recurs across the ecosystem (Address, Money, Quantity, Geographic Point, Personal
Name, Temporal Interval).

## 4.2 REFERENCE

REFERENCE is used for **Entities** and **Codes**. The host Property holds an
identifier, not a copy of the referent's contents.

- **Entity reference** — modelled as a [Relationship](../04-core-concepts/Relationship.md)
  to a Meta-Object identified by its canonical identifier, or as an identifier
  Property typed by an identifier scheme. The referent's attributes SHALL NOT be
  inlined; they are obtained by resolving the reference (subject to
  [Contract](../04-core-concepts/Contract.md) and
  [Projection](../04-core-concepts/Projection.md) when the referent is in another
  Universe).
- **Code reference** — modelled as a Property whose value is "a term drawn from
  scheme *S*", carrying the scheme's URI and version. The members of *S* SHALL NOT
  be copied into a local enumeration; carrying the scheme + version makes drift
  detectable.

A reference MAY be **snapshotted** — embedded as an immutable value copy — when
audit or immutability requires a frozen view (for example a Projection capturing an
address as it stood at a point in time). A snapshot SHALL be marked as such and
SHALL record the source identifier and the capture Event, so it is never mistaken
for the live referent. This is the legitimate face of "duplication" (§6).

## 4.3 MIX-IN and ANNOTATE

A **Facet** SHALL be applied as a MIX-IN: a declared facet Package whose Properties
merge into the host under their own namespace and are applied uniformly across many
Objects (for example `prov:*` provenance on every Object, valid-time on every
versioned Object, `odrl:*` policy on a Contract). A Facet SHALL NOT be re-invented
as bespoke domain fields, and SHALL NOT be buried in the domain payload — it is
*about* the data.

ANNOTATE attaches a controlled-vocabulary concept (a SKOS concept, a schema.org
type) to a Property to fix its meaning without changing its structure. It is the
lightest mechanism and preserves full sovereignty.

---

# 5. The Decision Rubric

For any concept *C* appearing in Meta-Model *M*, apply the following tests **in
order**; the first that matches fixes the representation.

1. **Facet test (orthogonal, applied first).** Is *C* a cross-cutting concern
   (provenance, valid-time, access policy, security marking, multilingual label)
   rather than domain payload? → **MIX-IN** the relevant facet model. Stop.

2. **Identity test.** Does *C* denote a thing with its own identity and lifecycle,
   that can be referred to, created, versioned or owned independently of *M*? →
   *C* is an **Entity**: **REFERENCE** it by identifier. Embed only as a marked
   **snapshot** when immutability/audit demands it. Stop.

3. **Authority test.** Is *C*'s set of permitted values, or its internal structure,
   already governed by an external standard?
   - A **code list / classification / identifier scheme** → **REFERENCE** that
     scheme (term + scheme URI + version). Never copy its members. Stop.
   - A **structured value-object standard** (Address, Money, …) → prefer that
     canonical model and continue to the Structure test.

4. **Structure test.** Does *C* have internal structure — two or more sub-values
   that travel together and would be meaningless split across the host? → *C* is a
   **Value Object**: **EMBED** it as a nested Meta-Model (preferably an imported
   canonical one). Do not flatten its parts. Stop.

5. **Reuse test.** Even if *C* is currently atomic, do two or more Meta-Models in
   scope need it in the same shape (now or foreseeably)? → factor *C* out as a
   shared Value Object and EMBED/REFERENCE it, so the shape is defined once. Stop.

6. **Default.** *C* is an **Attribute**: a literal with no independent identity, no
   external authority, no internal structure and no cross-model reuse. Represent it
   as a **Property (field)**. Duplicating such a field across Meta-Models is
   acceptable (§6).

```text
            ┌───────────────────────────────────────────────┐
  concept C │ 1. cross-cutting concern?  ── yes ─▶ MIX-IN    │
            │ 2. own identity/lifecycle? ── yes ─▶ REFERENCE │
            │ 3. governed value set?     ── yes ─▶ REFERENCE │
            │ 4. internal structure?     ── yes ─▶ EMBED     │
            │ 5. reused across models?   ── yes ─▶ EMBED     │
            │ 6. otherwise              ─────────▶ FIELD     │
            └───────────────────────────────────────────────┘
```

A conforming Meta-Model SHOULD be able to justify each Property by naming the test
that produced its representation.

---

# 6. When Duplication Is Acceptable

Composition over duplication is a default, not an absolute. Duplicating a value, or
holding the "same" concept as a plain field in several Meta-Models, is **correct**
in these cases:

- **Atomic attributes.** A `title`, a `quantity`, a free-text `note` — a literal
  with no shared authority. Two Meta-Models each holding such a field are not
  forking a concept; they hold two independent properties that happen to share a
  name.
- **Immutable snapshots.** A Projection, audit record or
  [Conflict Preservation](../03-federation/Conflict-Resolution.md) entry that
  deliberately freezes a value copy for immutability or locality. Here the *copy is
  the point*; it SHALL be marked as a snapshot with its source identifier and
  capture Event (§4.2).
- **Sovereignty by mapping.** When two models are independently governed and a
  crosswalk ([Semantic-Mapping](../03-federation/Semantic-Mapping.md)) is preferable
  to structural coupling, each keeps its own fields and the link is a MAP, not an
  EMBED.
- **Avoiding over-normalization.** When extracting a shared model would add more
  coupling than the concept is worth (a one-off, genuinely local atomic value),
  keeping a field is the proportionate choice.

Duplication is a **defect** only when it forks a *structured* Value Object,
*copies* a governed code list, *inlines* an Entity, or *re-invents* a Facet — the
four cases the rubric is designed to catch.

---

# 7. Compositional Roles of External Models

To make composition predictable at ecosystem scale, every external model in the
[Registry](../06-ecosystem/External-Models-Registry.md) can be assigned a
**compositional role** that predicts how other models should link to it. The
[Connector-Catalogue](../06-ecosystem/Connector-Catalogue.md) applies these roles to
the foundational connectors, and all 1180 catalogued standards carry a role and a
default link type in
[`external-models.csv`](../06-ecosystem/external-models.csv) (distribution in
[External-Models-Registry §3a](../06-ecosystem/External-Models-Registry.md)).

| Role | Description | Default link | Examples |
|------|-------------|--------------|----------|
| **R1 Foundational Value-Object** | Structured, identity-free, recurs everywhere | EMBED | Address (CIQ xAL), Money, Quantity (QUDT), GeoPoint, Personal Name, Temporal Interval |
| **R2 Reference Data / Code List** | Curated value set or classification | REFERENCE | ISO 3166, ISO 4217, ISO 639, UCUM, GPC, NACE, ESCO, SNOMED CT |
| **R3 Identifier Scheme** | Keys for entities | REFERENCE | LEI, ISIN, GTIN, GLN, DOI, ORCID/ISNI, IBAN/BIC, DID |
| **R4 Entity Model** | Things with identity and lifecycle | REFERENCE; snapshot-EMBED | schema:Organization, FHIR Patient, W3C ORG, schema:Place |
| **R5 Cross-cutting Facet** | Concerns applied across many Objects | MIX-IN | PROV-O, OWL-Time, ODRL, SKOS-XL labels |
| **R6 Aggregate / Document** | Composes R1–R5 into a document | composes (rarely embedded) | UBL Invoice, C-CDA, EPCIS Event, Order |
| **R7 Upper Ontology / Foundation** | Ontological grounding | ALIGN / ANNOTATE | BFO, DOLCE, ISO 15926 upper, Common Logic |
| **R8 Mapping / Lifting Tooling** | Implements MAP / transformation | n/a (tooling) | R2RML, RML, SAWSDL |

Roles are guidance, not law: a model MAY be embedded in one context and referenced
in another. The role names the *typical* and *recommended* link.

---

# 8. Expressing Composition in MMAS

Each mechanism has a concrete MMAS expression. Every link, regardless of mechanism,
SHALL preserve the linked model's **namespace, version, provenance and Semantic
Fingerprint**, and SHALL NOT violate the import invariants of
[Extension-Model](Extension-Model.md) §18.

- **EMBED** — a Property typed by a Meta-Object type from another Namespace; the
  embedded model is declared as a Semantic Package dependency; the host fingerprint
  incorporates the embedded shape.
- **REFERENCE (entity)** — a [Relationship](../04-core-concepts/Relationship.md) to a
  Meta-Object, or an identifier-typed Property; cross-Universe references are
  governed by Contract and exchanged as Projections.
- **REFERENCE (code)** — a Property typed `term ∈ scheme`, carrying scheme URI +
  version; validators MAY check membership and detect drift.
- **MIX-IN** — a facet Package merged under its own namespace; applied uniformly;
  declared in the Meta-Model's facet list.
- **EXTEND** / **MAP** / **ANNOTATE** — as specified in their owning documents.

A Meta-Model SHOULD declare, for each Property, its **composition kind**
(attribute / embed / reference / mixin) and, for embed and reference, the connector
identifier and version. This declaration is what makes a model's composition
machine-checkable.

---

# 9. Worked Example — `employee.person`

A single Person concept exercises every mechanism:

| Concept | Kind | Mechanism | Connector |
|---------|------|-----------|-----------|
| name | Value Object | EMBED | Personal Name (CIQ xNL / schema name parts) |
| address | Value Object | EMBED | Postal Address (CIQ xAL / vCard ADR) |
| nationality | Code | REFERENCE | ISO 3166-1 |
| primaryLanguage | Code | REFERENCE | ISO 639 (+ ISO 15924 script) |
| salary | Value Object | EMBED | Monetary Amount (amount + ISO 4217 currency) |
| height | Attribute (+unit) | FIELD + REFERENCE | literal value; unit ∈ UCUM |
| employer | Entity | REFERENCE | Organization by ISO 17442 LEI |
| orcid | Identifier | REFERENCE | ORCID / ISO 27729 ISNI |
| provenance | Facet | MIX-IN | PROV-O |
| validFrom/validTo | Facet | MIX-IN | OWL-Time / Lifecycle valid-time |
| accessPolicy | Facet | MIX-IN | ODRL |

For federation, the same `person` then **MAPs** to `fhir:Patient` and `foaf:Person`
via [Semantic-Mapping](../03-federation/Semantic-Mapping.md) — no field of the
Person is duplicated to achieve interoperability; only correspondences are declared.

---

# 10. Anti-Patterns

- **Flattened Value Object** — `addr_line1`, `addr_city`, `addr_zip` as host fields
  instead of an embedded Address. Forks the concept; blocks join and validation.
- **Copied code list** — a local `country` enum instead of a reference to ISO 3166.
  Drifts from the authority.
- **Inlined entity** — an employer's name/address/registration copied into every
  Person instead of a reference. Produces stale duplicates; violates the referent's
  sovereignty.
- **Re-invented facet** — bespoke `created_by` / `created_at` / `source` fields
  instead of a PROV mix-in. Fragments provenance across the ecosystem.
- **Over-embedding** — wrapping a genuinely atomic attribute in a nested model.
  Needless coupling; the inverse mistake.
- **Embedding an entity by value** — copying a thing that has identity, losing its
  identity, lifecycle and sovereignty.

These map one-to-one onto the failures the rubric (§5) is designed to prevent and
extend [Common Design Mistakes](../05-reference-architecture/Anti-Patterns.md).

---

# 11. Validation and Conformance

A conforming implementation SHOULD validate that:

- every Property declares a composition kind;
- embed and reference Properties name a connector and a version;
- code-typed Properties carry a scheme URI and version (drift-detectable);
- no Property cluster reproduces the shape of a known Value Object connector as
  flat fields (a forking check);
- snapshots are marked and carry source identifier and capture Event.

These checks are recommended additions to the
[Validation](Validation.md) levels and the
[Semantic Test Kit](../tests/). Composition declarations are themselves part of the
Meta-Model and therefore covered by its Semantic Fingerprint.

---

# 12. Architectural Invariants

Composition SHALL NEVER violate:

- the **Meta-Universe Constitution** and semantic sovereignty — referenced and
  embedded models retain their own authority, identity and governance;
- **provenance and traceability** — every link records origin, namespace and
  version;
- **version integrity** — links are version-aware; a change in a connector triggers
  compatibility assessment, not silent migration;
- **the import invariants** of [Extension-Model](Extension-Model.md) §18.

---

# Final Statement

A field is the right answer more often than not — but not when the "field" is
secretly an address, a country, an organization or a provenance record that the
rest of the world already models. Meta-Model Composition gives authors a single
rule for telling these apart, three mechanisms (embed, reference, mix-in) for
wiring them together, and a catalogue of connectors to wire them to. It is the
layer that turns a registry of a thousand isolated standards into a composable
fabric — where a concept is modelled once and reused everywhere, without any model
surrendering its sovereignty.
