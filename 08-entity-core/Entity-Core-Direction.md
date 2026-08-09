# Entity Core Direction

**Meta-Universe Specification (Exploration Branch)**

**Document ID:** ECORE-001 (candidate MU-V3-ECORE-001)
**Title:** Entity Core: the Refocused Value Proposition of the Standard
**Document Class:** Direction (pre-normative)
**Version:** 0.1 (Exploration)
**Status:** Working Draft, branch only; `main` is unchanged
**Normative References (by binding, not restatement):** MMAS-Core, Meta-Model-Composition (ARCH-016), Model-Traversal-and-Layout (ARCH-017), Data-Mastership (ARCH-018), Policy Consistency (ARCH-014), Versioning (ARCH-002), Naming (ARCH-003), Semantic Fingerprint (ARCH-009), MMAS-Interchange (MUIF), MUFP, Projection (CORE-009), Virtual-Projection (CORE-012), Validation (V0-V5), Federation Synchronization (FED-011..FED-014)
**License:** Apache-2.0

---

# 1. Purpose

This document states, crisply, what the standard is for, and directs the Entity
Core exploration accordingly.

The Meta-Universe family has grown a constitution, an architecture standard, a
federation protocol and a large body of core concepts. Each is sound. What has
been implicit until now is the single sentence that all of them serve:

> **The primary value of the standard is to define the properties and the methods
> of entities; to provide the formats in which that knowledge is structured and
> packaged (a set of format profiles: database, file as `.md`, `.html`, `.json`,
> ...); and to define the interfaces through which it is reached (`.git`, MCP,
> SQL), including how security works in each interface.**

Given only a conformant description, any reader, human or agent, with no
out-of-band knowledge, can: parse the format (the description protocols), find
all Findings about an entity, know which operations the entity exposes, know how
to communicate with the interface that serves it, and know how access is
governed there (access groups, an authorization center, policy). The data is
continuously synchronized, and all federation logic of meta-universes remains in
force, refined and elaborated, never replaced.

Everything else in the family, composition, traversal, mastership, projections,
federation, exists to make that sentence true at ecosystem scale.

---

# 2. The Refocus in One Diagram

```text
            what is described          how it is packaged         how it is reached
  +---------------------------+   +------------------------+   +--------------------+
  |  ENTITY                   |   |  FORMAT PROFILES       |   |  INTERFACES        |
  |   properties (data)       |   |   database (rows)      |   |   .git  (pull/PR)  |
  |   methods (behavior)      |   |   files: .md .html     |   |   MCP   (tools)    |
  |                           |   |          .json ...     |   |   SQL   (queries,  |
  |  described as a graph:    |   |   interchange (MUIF)   |   |         procedures)|
  |  Entity -> Bundle         |   +------------------------+   +--------------------+
  |        -> Layer           |     one graph, many                each interface
  |        -> Finding         |     packagings                     carries its own
  +---------------------------+                                    security description
```

The description graph is invariant. Formats and interfaces are pluggable
projections of the same graph. Security is part of the description, not an
afterthought of the deployment.

---

# 3. Why Properties AND Methods

The v2 family describes entities almost entirely through data: Properties,
Relationships, Events. Entity Core makes **behavior first-class**: an entity
exposes **operations**, not only data.

- A Product entity does not only *have* a price; it exposes `reprice`,
  `discontinue`, `forecast_demand`.
- A Repository entity does not only *have* branches; it exposes `open_proposal`,
  `run_validation`, `cut_release`.
- An Employee entity does not only *have* competencies; it exposes
  `request_review`, `book_capacity`.

The reason methods matter is the interface principle: **methods are what
interfaces execute**. A property is what an interface *reads*; a method is what
an interface *does*. When the description omits methods, every interface invents
its own verbs, and the promise that "a conformant reader knows how to
communicate with the interface" collapses into per-system documentation. When
methods are declared on the entity:

- an MCP server exposes each method as a **tool** with the declared signature;
- a SQL interface exposes read methods as views or table functions and mutating
  methods as **procedures**;
- a git interface executes a mutating method as a **proposal** (a branch plus a
  change request against the model repository).

One declaration, three executions. The method, not the interface, is the unit of
semantics. Mutating methods default to **propose-only** (the write path adopted
for the family): execution produces a proposal routed to the entity's System of
Record per ARCH-018, never a silent direct write.

---

# 4. The Universal Description Graph

Every described entity takes the same shape, regardless of domain, storage or
interface:

```text
  Entity  ->  Bundle of layers  ->  Layer  ->  Finding
```

- An **Entity** is a thing with identity: CSN plus Namespace plus version, pinned
  by a Semantic Fingerprint per ARCH-009.
- A **Bundle** is a coherent group of layers with a single semantic
  responsibility, exactly as in the MMAS composition hierarchy.
- A **Layer** carries a **question set**: the specific questions this layer
  exists to answer about the entity. The question set is the layer's contract.
- A **Finding** is the atomic unit of information: **the answer to exactly one
  specific question** that describes the entity. Not a document, not a page, not
  a table: one question, one answer, with provenance, freshness and mastership.

This is deliberately the shape that AISMM (the public software meta-model
specification, github.com/orkestron-ai/software-meta-model) has proven in
production use: its bundle / layer / record layout is the direct ancestor of
this graph. Entity Core generalizes what AISMM demonstrated for software to any
entity in any domain, and names the atomic unit (the Finding) that AISMM's
records carry. The full model is specified in ECORE-002.

---

# 5. The Six Principles

**P1. Storage-agnostic.** A Finding may live in a database row, a `.md` section,
a `.json` document, an `.html` fragment or an interchange file. The graph is the
invariant; the packaging is a profile. No format is privileged; every format
profile must support lossless enumeration of the Findings it carries.

**P2. Interface-pluggable.** The same entity is reachable through `.git`
(clone, pull, propose), MCP (tools) and SQL (queries and procedures), and
through future interfaces, without changing the description. An interface
binding declares how properties are read and how methods are executed there.

**P3. Security-described.** Every interface binding carries its security
description: the access groups it recognizes, the authorization center it
defers to, and the policy that governs disclosure. A reader learns how security
works the same way it learns how parsing works: from the description, per
ARCH-014.

**P4. Continuous synchronization.** Descriptions are not snapshots that decay.
Every Finding carries `observed_at` and freshness metadata; mastership flows per
ARCH-018 keep copies honest; synchronization is the steady state. In v0.1 of
this exploration the synchronization transport is deliberately minimal: git
pull, no long-running services.

**P5. Federation-preserved.** Nothing in Entity Core replaces federation.
Sovereign universes still exchange projections, not ownership; contracts still
govern disclosure; FED-011..FED-014 still govern synchronization across
sovereignty boundaries. Entity Core refines what travels: projections carry
Findings with their provenance and pins.

**P6. Behavior first-class.** Properties and methods are peers in the
description. An entity description without its operations is as incomplete as
one without its attributes.

---

# 6. Mapping to Existing v2 Machinery

Each principle builds on named v2 machinery. The table states what is inherited
by reference and what is genuinely new in this exploration.

| Principle | Builds on (v2, by reference) | Genuinely new in Entity Core |
|-----------|------------------------------|------------------------------|
| P1 Storage-agnostic | ARCH-017 (lossless traversal, well-known locations, file kinds), MUIF (interchange serialization) | The **Record** as a packaging-neutral carrier of Findings; database rows and files as equal, enumerable citizens under one coverage rule |
| P2 Interface-pluggable | MUIF (file-level exchange), MUFP (federation exchange), CORE-009 / CORE-012 (projection as the served view) | **Interface bindings** as declared parts of the description: .git, MCP, SQL descriptors bound to properties and methods; the rule that a Method is what an interface executes |
| P3 Security-described | ARCH-014 (policy consistency), Contract (core concept), MUFP disclosure | Access groups, authorization center and policy declared **per interface binding**, discoverable by a reader without out-of-band knowledge |
| P4 Continuous synchronization | ARCH-018 (mastership patterns, flows, freshness, `sources.yaml`), FED-011..FED-014 (cross-universe synchronization) | Freshness (`observed_at`) and confidence carried at **Finding granularity**, not dataset granularity; sync as steady state of the description itself |
| P5 Federation-preserved | MUFP entire, CORE-009, CORE-012, FED-011..FED-014 | Nothing replaced; refinement only: the unit that projections carry is now named and typed (the Finding), so federation exchanges become auditable at question level |
| P6 Behavior first-class | MMAS-Core Property and Event primitives, ARCH-016 (composition kinds for properties) | The **Method** as a new described primitive: name, signature, semantics, preconditions, effects, propose-only default; composition-aware like Properties |
| Graph shape (all) | MMAS composition hierarchy (Meta-Model -> Bundle -> Layer -> ...), ARCH-017 canonical walk, ARCH-016 decision rubric | The **question catalog** as the layer's contract, and the **Finding** as the atom that answers exactly one question |
| Identity (all) | ARCH-003 (naming, CSN), ARCH-002 (versioning), ARCH-009 (Semantic Fingerprint, never a byte hash as the semantic pin) | Nothing new: adopted as-is; major versions are distinct identities and declared compatibility ranges act only as publish-time validation predicates (adopted decision R1, recorded in the ELMM profile's decision log) |

The honest summary: Entity Core adds **three genuinely new things**, the Method,
the Finding with its one-question rule, and the per-interface security
description. Everything else is v2 machinery, bound by reference and refocused.

---

# 7. Relationship to AISMM and ELMM

**AISMM is the proven ancestor.** The bundle / layer / record layout of AISMM
(public specification: github.com/orkestron-ai/software-meta-model) is the
field-tested origin of the Entity -> Bundle -> Layer -> Finding shape. AISMM
models one entity class (a software product) this way at production scale;
Entity Core states the shape domain-independently so that any Core meta-model
can describe its entities identically. AISMM itself requires no change to
conform: its records are Records, its record content decomposes into Findings,
its layer purposes become question catalogs.

**ELMM governs the composition of entities described this way.** ELMM,
subtitled "the semantic composition kernel of the enterprise landscape"
(adopted decision R2), does not describe entities itself, and the kernel holds
no composes edges of its own: it registers, governs and resolves the
composition graph of Core and Landscape meta-models whose entities are
described per Entity Core. The Meta-Model Dependency Graph that ELMM maintains
(edge types composes, references, masters-link and deprecated-in-favor-of, as
defined by the ELMM profile; node identity per CSN plus Namespace plus version
with Semantic Fingerprint per ARCH-009) presumes exactly what Entity Core
guarantees: that every composed model's entities are uniformly enumerable,
uniformly identified, and uniformly reachable through declared interfaces. The
Twin Composition Snapshot (the lockfile of a composed twin) pins the versions
and fingerprints of the entity descriptions it composes. Context packs built
for agents are assembled from Findings; the pack shape and the seven context
rules that govern assembly are defined by the ELMM profile and adopted here by
reference, not restated.

Any Core or Landscape enumeration appearing in these documents is illustrative
and non-normative; the normative set is the registry, and registry id plus CSN
is the only normative identity (adopted decision R2).

---

# 8. Non-Goals

Entity Core does **not**:

1. Replace MUC, MMAS, MUFP or any core concept. It is an additive profile
   candidate for v3, bound to v2 by reference.
2. Define a new ontology language. RDF/OWL, Schema.org and their peers remain
   imported standards per the Extension Model.
3. Define a query language. SQL is an interface binding, not a new dialect.
4. Mandate a storage engine or a runtime service. Sync v0.1 is git pull; a
   database is one format profile among several.
5. Reopen the adopted decisions R1-R6 recorded in the ELMM profile's decision
   log. They are encoded here as constraints.
6. Enumerate the normative set of formats or interfaces. The lists (.md, .html,
   .json, database; .git, MCP, SQL) are the initial profiles; the normative set
   is whatever the registry carries.
7. Model access control enforcement. Entity Core describes how security works
   at an interface; enforcement belongs to the interface implementation and its
   authorization center.
8. Change AISMM. Conformance of AISMM is by interpretation, not by revision.

---

# 9. Workplan for the Branch

Walking-skeleton-first (adopted decision R5): each step produces something a
reader or tool can actually walk.

1. **ECORE-001 Entity-Core-Direction, ECORE-002 Entity-Graph-Model** (this
   drop): direction and the entity graph model, Working Drafts on this branch.
2. **ECORE-003 Packaging-Profiles.md** (this drop): the `.md`, `.json`, `.html`
   and database profiles; for each, how Records are laid out, how Findings are
   enumerated, how the coverage check of ARCH-017 Â§7 extends to database rows.
3. **ECORE-004 Interface-Bindings.md** (this drop): descriptor shapes for .git,
   MCP and SQL; the method-to-execution binding; access groups, authorization
   center and policy declaration; propose-only mechanics per interface.
4. **Schemas**: JSON Schema draft 2020-12 for the entity description, the
   question catalog, the Finding, the Record manifest and the interface
   descriptor; wired into V0-V1 validation.
5. **Walking skeleton**: one small entity (a single product or repository)
   described once and served three ways (git checkout, an MCP tool list, a SQL
   schema), with the same Findings enumerable in all three.
6. **Upstream change requests**: file the small set of change requests against
   v2 documents that the profile needs (candidate targets: ARCH-017 kind
   vocabulary, Validation check additions), keeping the profile standalone
   until accepted, per the standalone-shipping pattern of adopted decision R4.
7. **Review gate**: present the branch for review; only after acceptance does
   any of this text move toward `main` as a v3 profile candidate.

---

# Final Statement

The standard's machinery was never the point. The point is that an entity,
any entity, can be described so completely that a stranger's tool can find
every answer, invoke every operation, respect every boundary, and stay current,
without a single conversation with the authors. Entity Core is the family
saying that sentence out loud and organizing itself around it.
