# Context

**Meta-Universe Specification**

**Document ID:** MU-V2-CORE-010  
**Title:** Context — Why Knowledge Must Be Interpreted This Way  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MUFP  
**Informative References:** [Object](../04-core-concepts/Object.md), [Relationship](../04-core-concepts/Relationship.md), [Event](../04-core-concepts/Event.md), [Projection](../04-core-concepts/Projection.md), [Contract](../04-core-concepts/Contract.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the concept of **Context** within the Meta-Universe.

Context provides the semantic conditions under which knowledge is interpreted. It ensures that the same Meta-Object, Relationship or Event may be understood differently without changing its canonical identity or semantic truth.

Context is fundamental to federation, projections and AI reasoning.

---

# 2. Definition

A Context is an explicit semantic frame that defines how information SHALL be interpreted.

Context SHALL describe the circumstances surrounding knowledge rather than the knowledge itself.

Without Context, semantic interpretation SHALL be considered incomplete.

---

# 3. Context Principles

Every Context SHALL be:

- explicit;
- identifiable;
- traceable;
- versioned;
- technology independent;
- composable.

Context SHALL influence interpretation without modifying canonical identity.

---

# 4. Scope

Context MAY apply to:

- Meta-Objects;
- Relationships;
- Events;
- Projections;
- Contracts;
- Queries;
- AI reasoning;
- Federation exchanges.

Different Contexts MAY coexist for the same semantic artifact.

---

# 5. Context Dimensions

A Context MAY include one or more of the following dimensions:

- business;
- organizational;
- temporal;
- geographical;
- legal;
- security;
- operational;
- analytical;
- cultural;
- linguistic.

Domain Meta-Models MAY define additional context dimensions.

---

# 6. Core Components

Every Context SHOULD define:

- canonical identifier;
- context type;
- purpose;
- scope;
- owner;
- originating Universe;
- validity period (optional);
- version.

---

# 7. Context and Identity

Context SHALL NEVER redefine canonical Identity.

The same Meta-Object MAY participate in multiple Contexts while preserving a single canonical Identity.

---

# 8. Context and Projection

Every Projection SHALL declare its Context.

Different Contexts MAY produce different Projections of the same Meta-Object.

These Projections SHALL remain semantically traceable to the same source object.

---

# 9. Context and Contracts

Semantic Contracts MAY restrict or authorize Contexts.

Knowledge disclosed under one Context SHALL NOT automatically be valid for another Context.

Purpose and Context SHOULD be evaluated together during authorization.

---

# 10. Context and Time

Context MAY vary over time.

Temporal Context SHOULD identify:

- effectiveFrom;
- effectiveUntil;
- observedAt.

Historical Context SHALL remain reconstructable.

---

# 11. Federation

Federated Universes SHALL preserve Context whenever semantic interpretation depends upon it.

If Context cannot be preserved, the receiving Universe SHALL be informed of the semantic limitation.

Implicit Context assumptions SHALL be avoided.

---

# 12. Traceability

Every Context SHALL preserve:

- provenance;
- owner;
- originating Universe;
- version;
- associated semantic artifacts.

Context evolution SHALL remain auditable.

---

# 13. Validation

A conforming implementation SHOULD validate:

- context completeness;
- identifier uniqueness;
- purpose consistency;
- compatibility with governing Contracts;
- temporal validity.

Validation SHALL evaluate Context without altering it.

---

# 13a. Completeness Summary — The Ten Core Concepts

Context is the final concept of the core foundation. With it, the ten core concepts of the Meta-Universe form a **minimal-yet-sufficient semantic foundation**: minimal because no concept can be removed without leaving a question unanswered, and sufficient because together they answer every question required to make meaning exist, persist, connect, change, be governed and be interpreted. Each concept answers exactly one question:

| # | Concept | The single question it answers |
| --- | --- | --- |
| 1 | [Universe](../04-core-concepts/Universe.md) | who holds sovereignty |
| 2 | [Dimension](../04-core-concepts/Dimension.md) | in which management space |
| 3 | [Namespace](../04-core-concepts/Namespace.md) | how concepts are organized |
| 4 | [Identity](../04-core-concepts/Identity.md) | what makes an entity the same over time |
| 5 | [Object](../04-core-concepts/Object.md) | what exists |
| 6 | [Relationship](../04-core-concepts/Relationship.md) | how objects connect |
| 7 | [Event](../04-core-concepts/Event.md) | what happened |
| 8 | [Contract](../04-core-concepts/Contract.md) | on what terms knowledge may be used |
| 9 | [Projection](../04-core-concepts/Projection.md) | how knowledge appears in a situation |
| 10 | **Context** | why it must be interpreted this way |

The first three concepts are the governance axes (sovereignty, management context, organization). The fourth establishes sameness over time. Concepts five through seven describe existence, structure and change. The eighth governs use; the ninth governs appearance; and the tenth — Context — explains why a given interpretation is the correct one. No further core concept is required, and none of these ten is redundant.

---

# 14. Architectural Invariants

Every Context SHALL preserve:

- canonical identities;
- semantic authority;
- provenance;
- traceability;
- constitutional compliance.

Context SHALL interpret meaning.

It SHALL NOT replace meaning.

---

# 15. Typical Examples

Examples include:

- HR performance review context;
- Financial reporting context;
- Public disclosure context;
- Security incident response context;
- AI planning context;
- Regulatory compliance context.

These examples are informative rather than normative.

---

# Future Directions

The completeness of the ten core concepts invites a future **Semantic Foundation Completeness profile** that formally demonstrates minimality and sufficiency — showing, for each concept, the question that becomes unanswerable if it is removed, and proving that the ten together close the space of questions a federated semantic system must answer. Such a profile would also describe how domain Meta-Models extend the foundation without disturbing its minimal core. This direction is anticipated but not yet normative.

---

# Final Statement

Context is the semantic lens through which knowledge is interpreted within the Meta-Universe.

By making Context explicit, Meta-Universe enables the same semantic reality to be understood, projected and federated across different purposes without duplicating truth or compromising semantic integrity. Context transforms isolated facts into meaningful knowledge while preserving a single authoritative source of truth.
