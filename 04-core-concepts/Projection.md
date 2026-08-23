# Projection

**Meta-Universe Specification**

**Document ID:** MU-V2-CORE-009  
**Title:** Projection — Federation Without Loss of Sovereignty  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MUFP  
**Informative References:** [Object](../04-core-concepts/Object.md), [Relationship](../04-core-concepts/Relationship.md), [Event](../04-core-concepts/Event.md), [Contract](../04-core-concepts/Contract.md), [Identity](../04-core-concepts/Identity.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the concept of a **Projection** within the Meta-Universe.

A Projection is a context-specific representation of a Meta-Object. It exposes only the semantic information required for a particular purpose, audience or interaction while preserving the identity, ownership and authority of the underlying Meta-Object.

---

# 1a. The Five Fundamental Primitives

A Projection is one of the five fundamental semantic primitives of the Meta-Universe. Each primitive answers exactly one question, and together they form a closed picture of how meaning exists and travels:

| Primitive | Question it answers |
| --- | --- |
| [Object](../04-core-concepts/Object.md) | *what exists* |
| [Relationship](../04-core-concepts/Relationship.md) | *how things are connected* |
| [Event](../04-core-concepts/Event.md) | *how it changes over time* |
| [Contract](../04-core-concepts/Contract.md) | *under which rules it may be used* |
| **Projection** | *how it looks in a context* |

The Object is the [Semantic Point of Truth](../04-core-concepts/Object.md); Relationships connect Objects; Events record how they change along the Semantic Timeline; Contracts license their use beyond the home Universe; and the Projection is how all of this *appears* in a given situation without ever becoming the truth itself.

---

# 1b. Federation Without Loss of Sovereignty

The Projection is the mechanism that enables **federation without loss of sovereignty.** Because only Projections — never the [Meta-Object](../04-core-concepts/Object.md) itself — cross a boundary, a Universe can collaborate widely while its source of truth never leaves home.

One Meta-Object MAY carry many Projections at once, for example:

- a **Public** projection (what anyone may see);
- an **HR** projection (what the HR management context may see);
- a **Finance** projection (what the Finance management context may see);
- a **Security** projection (what the security context may see);
- an **AI Agent** projection (what an autonomous agent is permitted to reason over);
- a **Partner** projection (what a federated partner Universe may consume).

All such Projections SHALL reference the **same Canonical [Identity](../04-core-concepts/Identity.md)**, SHALL be governed by **[Semantic Contracts](../04-core-concepts/Contract.md)**, and SHALL exist for **different declared Purposes**. No Projection SHALL ever become the source of truth for the entity it represents.

---

# 2. Definition

A Projection is a first-class semantic artifact derived from a Meta-Object.

A Projection SHALL:

- reference exactly one canonical Meta-Object;
- preserve the canonical Identity of its source;
- represent a specific context;
- exist for an explicit purpose;
- remain traceable to its origin.

A Projection is **not** a copy of an object.

It is an authorized semantic view of that object.

---

# 3. Projection Principles

Every Projection SHALL be:

- context-specific;
- purpose-driven;
- traceable;
- versioned;
- technology independent;
- governed by one or more Semantic Contracts.

Different Projections MAY legitimately expose different subsets or interpretations of the same Meta-Object.

---

# 4. Relationship to Meta-Object

Every Projection SHALL reference one canonical Meta-Object.

The Meta-Object remains the semantic source of truth.

A Projection SHALL NEVER redefine:

- identity;
- ownership;
- provenance;
- constitutional authority.

---

# 5. Projection Context

Every Projection SHALL declare its context.

Typical contexts include:

- business;
- operational;
- analytical;
- regulatory;
- public;
- internal;
- AI reasoning;
- visualization.

Context SHALL be explicit.

---

# 6. Purpose

Every Projection SHALL declare its intended purpose.

Typical purposes include:

- reporting;
- decision support;
- federation;
- integration;
- user interface;
- AI reasoning;
- compliance.

Purpose participates in authorization and disclosure decisions.

---

# 7. Projection Profiles

Projection behavior MAY be standardized through Projection Profiles.

A Projection Profile SHOULD define:

- included concepts;
- hidden concepts;
- transformation rules;
- disclosure policy;
- intended audience.

Profiles SHOULD be reusable.

---

# 8. Identity

Every Projection SHALL preserve the canonical Identity of its source Meta-Object.

Projection-specific identifiers MAY exist locally.

Local identifiers SHALL NOT replace the canonical Identity.

---

# 9. Ownership

Ownership of a Projection SHALL remain traceable.

Unless explicitly delegated, the authoritative owner of the Meta-Object remains the authoritative owner of the Projection.

Delegated stewardship MAY be recorded without changing semantic authority.

---

# 10. Lifecycle

A Projection SHOULD have an explicit lifecycle.

Typical states include:

- Draft
- Active
- Suspended
- Deprecated
- Archived

Lifecycle transitions SHOULD be represented through Events.

---

# 11. Federation

Projection is the preferred unit of knowledge exchange in Meta-Universe.

Federation SHOULD exchange Projections rather than Meta-Objects.

A receiving Universe SHALL treat the Projection as a context-specific representation rather than an authoritative replacement.

---

# 12. Disclosure

Projection disclosure SHALL be governed by Semantic Contracts.

Contracts MAY define:

- visible attributes;
- hidden attributes;
- transformation rules;
- retention period;
- redistribution rights.

Disclosure SHALL always be purpose-driven.

---

# 13. Traceability

Every Projection SHALL preserve:

- source Meta-Object;
- originating Universe;
- originating Namespace;
- governing Contract(s);
- provenance;
- creation time;
- version.

Traceability SHALL remain reconstructable.

---

# 14. Evolution

A Projection MAY evolve independently from other Projections of the same Meta-Object.

Evolution SHALL NOT invalidate the canonical Identity or semantic authority of the source Meta-Object.

Changes SHALL remain versioned and traceable.

---

# 15. Validation

A conforming implementation SHOULD validate:

- source object reference;
- canonical identity preservation;
- declared context;
- declared purpose;
- governing contracts;
- disclosure consistency;
- projection profile compatibility.

---

# 16. Architectural Invariants

Every Projection SHALL preserve:

- canonical identity;
- semantic traceability;
- ownership;
- provenance;
- constitutional compliance.

A Projection SHALL NEVER become the semantic authority over its source Meta-Object.

---

# Future Directions

The five-primitive framing anticipates a future **Projection Profile catalog** of reusable, federatable projection definitions (Public, HR, Finance, Security, AI Agent, Partner and others), each binding included and hidden concepts, transformation rules and a governing Semantic Contract template. Such a catalog would let Universes publish and import standardized projections the way they import Namespaces, making "federation without loss of sovereignty" a turnkey capability rather than a bespoke arrangement. This direction is anticipated but not yet normative.

For projections whose content is *computed live from a source* rather than stored — runtime metrics and other volatile facts — see [Virtual Projection](../04-core-concepts/Virtual-Projection.md), which defines hot/cold descriptive facts and Virtual Stream Views.

---

# Final Statement

A Projection is the constitutional mechanism through which knowledge is safely shared within the Meta-Universe.

It allows the same Meta-Object to appear differently in different contexts while preserving a single semantic truth. By exchanging Projections instead of ownership, sovereign Universes can collaborate, protect sensitive knowledge and maintain long-term semantic interoperability without compromising authority or identity.
