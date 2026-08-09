# Entity Graph Model

**Meta-Universe Specification (Exploration Branch)**

**Document ID:** ECORE-002 (candidate MU-V3-ECORE-002)
**Title:** Entity Core: the Entity Description Graph (Entity, Property, Method, Bundle, Layer, Finding, Record)
**Document Class:** Normative draft (pre-normative until accepted)
**Version:** 0.1 (Exploration)
**Status:** Working Draft, branch only; `main` is unchanged
**Normative References (by binding, not restatement):** MMAS-Core, Meta-Model-Composition (ARCH-016), Model-Traversal-and-Layout (ARCH-017), Data-Mastership (ARCH-018), Policy Consistency (ARCH-014), Versioning (ARCH-002), Naming (ARCH-003), Semantic Fingerprint (ARCH-009), MMAS-Interchange (MUIF), Projection (CORE-009), Virtual-Projection (CORE-012), Validation (V0-V5), Federation Synchronization (FED-011..FED-014)
**Informative References:** ECORE-001 (Entity-Core-Direction), the ELMM profile (MMDG edge vocabulary, context machinery, decision log R1-R6)
**License:** Apache-2.0

---

# 1. Purpose and Scope

This document defines the entity description graph introduced in ECORE-001: the
seven node types (Entity, Property, Method, Bundle, Layer, Finding, Record),
the edges between them, the traversal semantics that extend ARCH-017, the
question catalog as the layer's contract, and the invariants ECORE-I1..ECORE-I8.

It governs **how an entity is described**. It does not govern how descriptions
are packaged into concrete formats (ECORE-003) or served through concrete
interfaces with their security descriptions (ECORE-004), except where a rule
must be stated here so those documents can bind to it.

Normative language (SHALL, SHOULD, MAY) is used in the RFC 2119 sense, with the
standing caveat that the whole document is a Working Draft on a branch.

---

# 2. The Graph at a Glance

```text
                         +----------------------------------+
                         |             ENTITY               |
                         |  identity: CSN + Namespace       |
                         |            + version             |
                         |  pin: Semantic Fingerprint       |
                         +----+--------------+---------+----+
            declares          |              |         |   declares
        +---------------------+              |         +--------------------+
        v                                    v                              v
  +-----------+                    +------------------+             +-------------+
  | PROPERTY  |                    |  BUNDLE (1..n)   |             |   METHOD    |
  | typed,    |                    |  coherent group  |             | name, sig,  |
  | mastered  |                    |  of layers       |             | semantics,  |
  +-----------+                    +--------+---------+             | pre, effects|
                                            | contains               +-------------+
                                            v
                                   +------------------+
                                   |   LAYER (1..n)   |
                                   |  question set =  |
                                   |  its contract    |
                                   +--------+---------+
                                            | asks
                                            v
                                   +------------------+
                                   |    QUESTION      |
                                   +--------+---------+
                                            | answered-by (0..n)
                                            v
                                   +------------------+   carried-by   +----------+
                                   |     FINDING      | -------------> |  RECORD  |
                                   | one answer, with |    (1..n)      | concrete |
                                   | provenance,      |                | packaging|
                                   | observed_at,     |                +----------+
                                   | confidence,      |
                                   | mastership       |
                                   +------------------+
```

One graph, many packagings, many interfaces. Sections 3 to 9 define the nodes;
section 10 defines the edges and traversal; section 11 the question catalog;
section 12 the invariants; section 13 validation.

---

# 3. Entity

An **Entity** is a described thing with independent identity and lifecycle: a
product, a repository, a person-role, an organization, a contract, a server. In
MMAS terms an Entity corresponds to a Meta-Object whose kind is Entity per the
ARCH-016 classification (own identity, referenceable, owned).

**Identity.** An Entity SHALL be identified by the triple:

- **CSN** (canonical semantic name) per ARCH-003;
- **Namespace** per ARCH-003;
- **version** per ARCH-002.

The identity SHALL be pinned by a **Semantic Fingerprint** per ARCH-009. The
fingerprint is the semantic pin; a byte hash SHALL NOT be used as the semantic
pin (it may accompany it for transport integrity). Major versions are distinct
identities: `product@4` and `product@5` are two nodes, not one node with a
range; declared compatibility ranges act only as publish-time validation
predicates (adopted decision R1, recorded in the ELMM profile's decision log).

**Declaration.** An Entity declares its Properties (section 4), its Methods
(section 5), and its Bundles (section 6). The declaration is itself part of the
model and therefore covered by the fingerprint.

**Resolution.** Given the identity triple, a conformant resolver SHALL locate
exactly one entity description (or fail explicitly). Cross-entity references
use the identity triple, never a location.

---

# 4. Property

A **Property** is a declared, typed attribute of the Entity.

A Property SHALL declare:

- **name** (unique within the Entity, per ARCH-003 conventions);
- **type**: a literal type, an embedded value-object model, or a reference,
  classified by the ARCH-016 decision rubric; the composition kind (attribute /
  embed / reference / mixin) SHALL be recorded as ARCH-016 Â§8 requires;
- **cardinality**;
- **mastership**: the dataset (in the sense of ARCH-018) whose System of Record
  masters this Property's values. A Property whose values are externally
  mastered is readable through the description but SHALL be corrected only at
  its master.

A Property is what interfaces **read**. Interfaces SHALL NOT expose a write
operation on a Property directly; writes happen only through Methods
(section 5), which is how mastership stays enforceable.

---

# 5. Method

A **Method** is a declared operation the Entity exposes. Methods make behavior
first-class: an entity description without its operations is incomplete.

A Method SHALL declare:

- **name** (unique within the Entity);
- **signature**: typed parameters and a typed result, using the same type
  system as Properties (JSON Schema draft 2020-12 in the concrete schemas);
- **semantics**: a prose statement of what the operation means, precise enough
  that two interface bindings implement the same behavior;
- **preconditions**: what must hold before invocation (state predicates,
  required access);
- **effects**: what the operation changes, stated against Properties and
  mastered datasets ("sets `status` to `retired` in the model-mastered
  lifecycle dataset"), and what Events it emits;
- **mutation class**: `read` (no effects) or `mutating` (any effect).

**The binding rule.** A Method is **what an interface executes**. Each
interface binding (ECORE-004) maps the Method to its native executable form:

| Interface | A Method becomes |
|-----------|------------------|
| MCP | a tool, with the Method's signature as the tool schema |
| SQL | a view or table function (`read`) or a stored procedure (`mutating`) |
| .git | a read of the working tree (`read`) or a **git-mediated proposal**: a branch plus change request against the mastering repository (`mutating`) |

**Propose-only default.** A `mutating` Method SHALL default to **propose-only**
execution: invocation produces a proposal addressed to the System of Record of
each dataset the effects touch, routed through that dataset's change process
per ARCH-018 (model-mastered: the model's review flow; external-mastered: a
change request toward the external system or its steward). Direct-commit
execution is an opt-in per Method and per interface binding, permitted only
where the binding's security description (ECORE-004) explicitly grants it, and
never against a dataset the invoker's side does not master. A Method SHALL NOT
provide any path that bypasses mastership (invariant ECORE-I4).

---

# 6. Bundle

A **Bundle** is a coherent group of Layers with a single semantic
responsibility, exactly as in the MMAS composition hierarchy and ARCH-017 Â§5.
Entity Core adds no new bundle semantics; it binds them:

- a Bundle SHALL declare its single responsibility and its ordered list of
  Layers (dependency-first, per ARCH-017 Â§5);
- Bundles of one Entity SHALL be ordered dependency-first; cycles are
  non-conforming;
- a Bundle belongs to exactly one Entity description.

The bundle / layer layout proven by AISMM (the public software meta-model
specification) is the reference ancestor of this structure.

---

# 7. Layer

A **Layer** is the unit of descriptive focus inside a Bundle. What is new in
Entity Core: **a Layer carries its defining question set**.

A Layer SHALL declare:

- its one-line purpose (as ARCH-017 already requires for enumerated content);
- its **question catalog**: the ordered list of Questions this layer exists to
  answer about the Entity (section 11);
- its content enumeration per ARCH-017 Â§5 (files or, in database profiles, the
  Record sets that carry its Findings).

A Layer is complete when every Question in its catalog has at least one current
Finding or an explicit open-question marker; it is honest when it contains no
Finding answering a Question outside its catalog.

---

# 8. Finding

A **Finding** is the atomic unit of description: **the answer to exactly one
Question**.

A Finding SHALL carry:

- **question_ref**: the identifier of the one Question it answers (exactly one;
  invariant ECORE-I1);
- **answer**: the content, typed by the Question's declared answer type (a
  literal, a structured value, a reference to another Entity, prose);
- **provenance**: where this answer came from (authored by whom, harvested from
  which system, generated by which tool from which inputs), per the origin
  vocabulary of ARCH-017 Â§9; a restricted-access source specification may be
  recorded as provenance without disclosure of its content;
- **observed_at** and freshness metadata: when this answer was true of the
  world, and, for mirrored answers, the harvest time and staleness limit per
  ARCH-018 Â§8;
- **confidence**: the describer's stated confidence (an enumerated scale or a
  probability), so downstream trust weighting has something to weigh;
- **mastership**: the ARCH-018 dataset this Finding belongs to, which
  determines where a correction is written.

A Finding is small on purpose. "What is the production database engine?" is one
Question; its Finding is one answer with one provenance and one freshness. A
paragraph that answers four questions is four Findings, even if one Record
carries them all.

A Finding SHALL NOT be edited in place when its origin is harvested or
generated (ARCH-017 Â§9); the correction goes to the master, and the Finding is
re-harvested or re-generated.

---

# 9. Record

A **Record** is the stored carrier of one or more Findings in a concrete
packaging: a markdown file (or a section of one), a JSON document, an HTML
fragment, a database row or row set, a MUIF document member.

Rules:

- a Record SHALL declare which Findings it carries (explicitly, or via a format
  profile's deterministic extraction rule defined in ECORE-003);
- a Record has exactly one **format profile** and exactly one origin (authored
  / harvested / generated, per ARCH-017 Â§9);
- the same Finding MAY be carried by multiple Records (a master Record and
  projected copies); in that case exactly one Record is the mastered carrier
  per ARCH-018, and every other carrier is a marked projection or mirror;
- Records are enumerable: in file packagings through the ARCH-017 walk, in
  database packagings through the profile's declared enumeration query
  (ECORE-003). A Record reachable by neither is an orphan and a validation
  failure.

The Record / Finding split is what makes the model storage-agnostic: Findings
are the invariant content, Records are the packaging, and re-packaging (say,
moving a layer from files to a database) changes Records only.

---

# 10. Edges and Traversal

## 10.1 Intra-entity edges

| Edge | From -> To | Cardinality |
|------|-----------|-------------|
| declares-property | Entity -> Property | 1 -> 0..n |
| declares-method | Entity -> Method | 1 -> 0..n |
| has-bundle | Entity -> Bundle | 1 -> 1..n, ordered |
| has-layer | Bundle -> Layer | 1 -> 1..n, ordered |
| asks | Layer -> Question | 1 -> 1..n, ordered |
| answered-by | Question -> Finding | 1 -> 0..n (0 = open question, marked) |
| carried-by | Finding -> Record | 1 -> 1..n (exactly one mastered carrier) |
| about | Finding -> Property or Method | 0..1 (when the Question concerns a declared Property or Method, the Finding SHOULD link it) |

## 10.2 Inter-entity edges

Between Entities (and between the meta-models that declare them), the edge
vocabulary is the MMDG edge set of the ELMM profile: **composes**,
**references**, **masters-link** and **deprecated-in-favor-of**. Their
semantics, validity rules, record shape and the binding of the edge field
`compositional_role` to the ARCH-016 roles R1-R8 are defined by the ELMM
profile and adopted here by reference, not restated.

What Entity Core states itself is only the identity rule: node identity on
these edges is always CSN plus Namespace plus version, pinned by the ARCH-009
Semantic Fingerprint, and a composed twin pins its member versions in a Twin
Composition Snapshot.

## 10.3 Traversal semantics (extending ARCH-017)

The ARCH-017 canonical walk is extended, not modified:

1. Entry point, manifests, mastership register, canon: exactly as ARCH-017 Â§4
   and Â§10.
2. Walk bundles in declared order; within each, layers in declared order.
3. **New:** on entering a Layer, read its question catalog before its content.
   The catalog tells the reader what it is about to learn.
4. Enumerate the Layer's Records (files per ARCH-017; database Records per the
   ECORE-003 profile), extract their Findings, and bind each Finding to its
   Question.
5. **Extended coverage check:** in addition to the file-level check of
   ARCH-017 Â§7, the walker SHALL verify: every Finding binds to exactly one
   Question, every Question is either answered or explicitly open, and every
   Record's Findings are extractable. Orphan Findings (no Question) and
   phantom Questions (undeclared but answered) are validation failures.
6. Entity-level closure: after all bundles, the walker can state, per Property
   and per Method, which Findings describe it, and per Question, what the
   current answer is, with provenance and freshness.

Two conformant walkers over the same entity description version SHALL produce
the same Finding set in the same order.

Consumers assembling context for a task SHOULD deliver Findings as context
packs; the pack shape and the seven context rules that govern assembly are
defined by the ELMM profile and adopted here by reference. Serving a consumer
never hands over raw Records when a projection of Findings suffices (CORE-009;
virtual projections per CORE-012 when the answer is computed on demand).

---

# 11. The Question Catalog: the Layer's Contract

A **Question** is a declared, identified, specific interrogative about the
Entity: "What is the deployment topology?", "Who masters the price?", "What
does `discontinue` require?".

Rules:

- a Question SHALL have a stable identifier, a precise phrasing, and a declared
  **answer type**;
- a Question SHALL belong to exactly one Layer (invariant ECORE-I2); if two
  layers need the same fact, one asks and the other references the Finding;
- the catalog is **the contract of the layer**: completeness is measured
  against it (answered / open per Question), change to it is a semantic change
  covered by the fingerprint and versioned per ARCH-002, and a reader can know
  what a layer will and will not tell them without reading its content;
- catalogs are per-entity-class and reusable: a meta-model SHOULD define its
  question catalogs once (per layer, per entity class) so that every entity of
  that class is described against the same questions. This is what makes
  descriptions comparable across entities and across universes.

Open questions are first-class: a Question with no Finding SHALL be marked
open, never silently absent. An open question is declared debt, exactly as a
`status: declared` mastership entry is per ARCH-018 Â§6.

---

# 12. Invariants

| ID | Invariant |
|----|-----------|
| **ECORE-I1** | Every Finding answers exactly one Question. A content unit answering several questions is several Findings. |
| **ECORE-I2** | Every Question belongs to exactly one Layer. Shared needs are met by reference, not duplicate questions. |
| **ECORE-I3** | Every Entity resolves identity: CSN plus Namespace plus version, pinned by a Semantic Fingerprint per ARCH-009; major versions are distinct identities. |
| **ECORE-I4** | Methods never bypass mastership: every effect of a mutating Method lands at the System of Record of the dataset it touches, per ARCH-018; propose-only is the default execution mode. |
| **ECORE-I5** | Findings are never orphaned from provenance: a Finding without provenance, or with provenance that names no origin, is non-conforming. |
| **ECORE-I6** | Every Finding is reachable by the canonical walk regardless of packaging: file or database, a Record no walker can enumerate is an orphan. |
| **ECORE-I7** | Exactly one Record is the mastered carrier of a Finding; every other carrier is a marked projection or mirror with its master and freshness declared. |
| **ECORE-I8** | An interface binding without its security description (access groups, authorization center, policy per ARCH-014) is non-conforming; a reader SHALL be able to learn how security works from the description alone. |

These invariants extend, and never relax, the architectural invariants of
ARCH-016 Â§12, ARCH-017 Â§12 and ARCH-018 Â§12.

---

# 13. Validation: How V0-V5 Applies

Entity Core adds checks inside the existing levels; it adds no new level.

| Level | Existing meaning | Entity Core additions (draft check IDs) |
|-------|------------------|------------------------------------------|
| **V0** Syntax | Artifacts parse | `EC-V0-01` entity description, question catalogs and Finding carriers parse against the ECORE schemas (JSON Schema 2020-12) |
| **V1** Structural | MMAS hierarchy present; ARCH-017 coverage | `EC-V1-01` every Layer declares a question catalog; `EC-V1-02` extended coverage: no orphan Findings, no phantom Questions, no unenumerable Records (ECORE-I1, I2, I6) |
| **V2** Semantic | Meaning-level checks | `EC-V2-01` every Finding carries provenance, observed_at and mastership (ECORE-I5); `EC-V2-02` one mastered carrier per Finding (ECORE-I7); `EC-V2-03` Method effects name only declared datasets and Properties; `EC-V2-04` propose-only not silently overridden (ECORE-I4) |
| **V3** Referential | References resolve | `EC-V3-01` question_refs, Property/Method links and inter-entity edges (composes, references, masters-link, deprecated-in-favor-of) resolve to identities pinned per ARCH-009 (ECORE-I3) |
| **V4** Federation | MUFP participation | `EC-V4-01` exchanged projections carry Findings with provenance and version pins, never bare answers; disclosure honors the interface security description (ECORE-I8) per FED-011..FED-014 |
| **V5** Runtime (optional) | Live drift | `EC-V5-01` interface bindings actually execute declared Methods and nothing else; `EC-V5-02` Finding freshness against declared cadence; stale mirrors flagged per ARCH-018 Â§8 |

Compatibility-range declarations between composed models are evaluated only as
publish-time validation predicates within these gates (adopted decision R1);
they never merge identities.

---

# 14. Open Questions for Review

1. Granularity guidance: a worked rule of thumb for when prose splits into
   multiple Findings, beyond the one-question test.
2. Whether the question catalog should support inheritance across entity
   classes (a base catalog refined per class) or stay flat in v0.1.
3. Whether `confidence` needs a normative scale or stays profile-defined.
4. The minimal database enumeration contract for ECORE-003 (a declared SQL
   query per layer versus a manifest table).
5. Whether Method preconditions warrant a machine-checkable predicate form or
   remain prose plus access requirements in v0.1.

---

# Final Statement

Seven node types, four inter-entity edges, eight invariants. An Entity declares
what it has (Properties) and what it does (Methods); Bundles and Layers give
the description its walkable shape; Questions state what a layer promises to
know; Findings keep every answer small, sourced, dated and mastered; Records
let the same knowledge live in a file today and a database tomorrow without a
single Finding changing. Everything above this graph, formats, interfaces,
security, federation, is a projection of it, and everything below it is already
standardized machinery this document deliberately declines to reinvent.
