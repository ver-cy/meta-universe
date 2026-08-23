# Relationship

**Meta-Universe Specification**

**Document ID:** MU-V2-CORE-006  
**Title:** Relationship — A First-Class Semantic Entity  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MUFP  
**Informative References:** [Object](../04-core-concepts/Object.md), [Event](../04-core-concepts/Event.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the concept of a **Relationship** within the Meta-Universe.

A Relationship is a first-class semantic entity that expresses a meaningful connection between two or more Meta-Objects. Relationships are governed, versioned and traceable independently from the objects they connect.

---

# 2. Definition

A Relationship represents a semantic assertion describing how Meta-Objects are connected.

A Relationship is a **first-class semantic entity, not a technical link.** In real organizations, relationships frequently carry more meaning than the objects they join: the bond *employee ↔ manager*, the bond *person ↔ family*, the bond *company ↔ contract* — these are where obligation, authority and consequence actually live. The Meta-Universe therefore governs Relationships in their own right, with their own identity, lifecycle, ownership and provenance.

A Relationship SHALL describe meaning rather than implementation.

Implementation-specific references, foreign keys or graph edges SHALL NOT be considered semantic relationships unless they explicitly represent semantic meaning.

---

# 3. Relationship Principles

Every Relationship SHALL:

- have a well-defined semantic meaning;
- reference one or more Meta-Objects;
- preserve traceability;
- have an identifiable lifecycle;
- belong to an authoritative Universe;
- remain independent from storage technology.

Relationships are semantic objects in their own right.

---

# 4. Core Components

Every Relationship SHOULD define:

- canonical identifier;
- relationship type;
- source object(s);
- target object(s);
- semantic meaning;
- cardinality;
- lifecycle state;
- owner;
- provenance;
- version.

Additional metadata MAY be defined by domain Meta-Models.

---

# 5. Relationship Types

Typical relationship categories include:

- Association
- Composition
- Aggregation
- Dependency
- Ownership
- Membership
- Assignment
- Reference
- Derivation
- Equivalence

Domain Meta-Models MAY introduce additional relationship types.

---

# 5a. Relationship Profile

A **Relationship Profile** is a standardized, reusable class of relation that MAY be shared across meta-models so that the same connection means the same thing everywhere it appears.

Recommended baseline Relationship Profiles include:

- `reportsTo` — an actor is accountable to another within an authority structure;
- `owns` — an actor holds ownership of an object;
- `memberOf` — an object participates in a group or collective;
- `dependsOn` — an object requires another to function or to hold meaning;
- `implements` — an object realizes a specification, capability or contract.

A Relationship Profile SHOULD define its semantic meaning, expected source and target categories, default cardinality and typical temporal behavior. Meta-Models SHOULD reuse published Relationship Profiles rather than redefining equivalent relations, so that connections remain comparable and federatable across Universes. Local extensions to a Relationship Profile SHALL remain additive and SHALL NOT redefine its established meaning.

---

# 6. Cardinality

Relationship cardinality SHALL be explicit whenever applicable.

Typical forms include:

- One-to-One
- One-to-Many
- Many-to-One
- Many-to-Many

Cardinality SHALL describe semantics rather than database implementation.

---

# 7. Identity

Every significant Relationship SHALL possess a canonical Identity.

Identity SHALL remain stable throughout the lifecycle of the Relationship.

Changing relationship attributes SHALL NOT create a new identity.

Replacing the semantic meaning SHALL create a new Relationship.

---

# 8. Ownership

Every Relationship SHALL have an authoritative owner.

Ownership determines responsibility for establishing, maintaining and retiring the relationship.

Ownership SHALL remain traceable.

---

# 9. Lifecycle

A Relationship SHOULD progress through explicit lifecycle states such as:

- Proposed
- Active
- Suspended
- Deprecated
- Retired

Lifecycle transitions SHALL be represented through Events.

---

# 10. Temporal Validity

A Relationship MAY include temporal validity.

Typical attributes include:

- validFrom;
- validUntil;
- observedAt;
- terminatedAt.

The temporal validity and lifecycle of a Relationship SHALL be expressed through the [Event](../04-core-concepts/Event.md) primitive and recorded on the Semantic Timeline, so that *when* a connection held — and when it ceased to hold — is reconstructable independently of the current state of the objects it joins.

Temporal validity SHALL NOT affect canonical identity.

---

# 11. Events

Creation, modification and retirement of Relationships SHOULD be represented by immutable Events.

Historical states SHALL remain reconstructable.

---

# 12. Federation

Relationships MAY span Objects originating from different Universes.

Cross-Universe Relationships SHALL:

- preserve the canonical identities of all participating Objects;
- identify the authoritative owner;
- reference the governing federation agreement when applicable.

Federation SHALL NOT transfer ownership of participating Objects.

---

# 13. Imported Relationships

Imported Relationships SHALL preserve:

- originating namespace;
- provenance;
- version;
- semantic meaning.

Local extensions SHALL remain additive.

---

# 14. Traceability

Every Relationship SHALL preserve:

- provenance;
- ownership history;
- lifecycle history;
- event history;
- semantic lineage.

Relationship history SHALL remain auditable.

---

# 15. Validation

A conforming implementation SHOULD validate:

- referenced object identities;
- relationship type;
- cardinality;
- semantic consistency;
- lifecycle state;
- federation constraints.

---

# 16. Architectural Invariants

Every Relationship SHALL preserve:

- semantic meaning;
- canonical identity;
- traceability;
- ownership;
- constitutional compliance.

Relationships SHALL NEVER be reduced to implementation-only links.

---

# Future Directions

The Meta-Universe advances a guiding principle: **meaning emerges from Relationships, not only from Objects.** As this principle matures, a future **Relationship Profile catalog** is anticipated — a published, federatable library of standardized relation classes (extending the `reportsTo` / `owns` / `memberOf` / `dependsOn` / `implements` baseline) that meta-models can import the way they import Namespaces, so that the *structure* of knowledge becomes as reusable and as discoverable as the entities within it. This direction is anticipated but not yet normative.

---

# Final Statement

A Relationship is a first-class semantic construct of the Meta-Universe.

It represents meaningful connections between Meta-Objects, enabling knowledge to be modeled as an evolving semantic network whose structure is as important as the objects themselves. By treating Relationships as independently governed artifacts, Meta-Universe preserves meaning, traceability and interoperability across federated semantic universes.
