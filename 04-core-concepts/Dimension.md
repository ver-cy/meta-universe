# Dimension

**Meta-Universe Specification**

**Document ID:** MU-V2-CORE-002  
**Title:** Dimension — The Semantic Management Context  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MUFP  
**Informative References:** [Universe](../04-core-concepts/Universe.md), [Namespace](../04-core-concepts/Namespace.md), [Projection](../04-core-concepts/Projection.md), [Contract](../04-core-concepts/Contract.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the concept of a **Dimension** within the Meta-Universe architecture.

A Dimension is the **semantic management context** of a Universe. It provides an independent management space within which shared objects are interpreted, disclosed and trusted according to context-specific rules, while remaining under the sovereignty of its parent Universe.

---

# 2. Definition

A Dimension is the **semantic management context** within a Universe.

The three governance axes of the Meta-Universe are distinct:

- the **Universe** is the *jurisdiction* — it holds semantic sovereignty;
- the **Dimension** is the *management context* — it determines how concepts are interpreted, disclosed and trusted within a given management space;
- the **Namespace** is the *organization* — it determines how concepts are named, organized and published.

A Dimension is **not** a folder of objects. Two Dimensions within the same Universe MAY share the very same base objects — for example a single `Person` object — while interpreting them under different rules. The Product Dimension, the HR Dimension, the Security Dimension and the Finance Dimension of one company all reference the same underlying Meta-Objects, yet each applies:

- its own interpretation rules;
- its own disclosure contracts;
- its own trust policies;
- its own projections.

A Dimension is a logical management context within a Universe.

Each Dimension:

- belongs to exactly one Universe;
- has its own management purpose;
- may interpret shared objects under its own rules;
- may contain multiple Namespaces;
- may define local semantic policies, disclosure contracts and trust policies;
- participates in federation through its parent Universe.

Dimensions do not possess independent sovereignty.

---

# 3. Relationship to Universe

A Universe MAY contain one or more Dimensions.

Every Dimension SHALL belong to exactly one Universe.

Dimensions inherit the constitutional principles and governance of their parent Universe.

A Dimension SHALL NOT exist outside a Universe.

---

# 4. Purpose of Dimensions

Dimensions exist to separate independent semantic domains while avoiding unnecessary fragmentation into multiple Universes.

Typical motivations include:

- organizational separation;
- business domains;
- legal boundaries;
- security boundaries;
- lifecycle separation;
- experimental environments.

---

# 5. Internal Structure

A Dimension SHALL contain one or more Namespaces.

Recommended hierarchy:

Universe
    └── Dimension
            └── Namespace
                    └── Objects

Namespaces organize concepts.

Dimensions organize semantic spaces.

---

# 6. Semantic Autonomy

A Dimension MAY define:

- local semantic models;
- local naming conventions;
- local validation rules;
- local extension policies;
- local federation profiles.

Such rules SHALL remain compatible with the parent Universe and SHALL NOT violate MUC.

---

# 7. Identity

Every Dimension SHALL possess:

- a globally unique identifier;
- a stable canonical name;
- a parent Universe reference;
- version metadata.

Identifiers SHALL remain stable throughout the Dimension lifecycle.

---

# 8. Ownership

Every Dimension SHALL declare a responsible owner or steward.

The owner MAY differ from the owner of the parent Universe.

Responsibility for governance MAY be delegated while constitutional authority remains with the Universe.

---

# 9. Namespace Management

Namespaces SHALL be managed within a Dimension.

Namespace uniqueness SHALL be guaranteed within the scope of the Dimension.

Multiple Dimensions MAY contain namespaces with identical local names provided their fully-qualified semantic identities remain unique.

---

# 10. Federation

Dimensions do not federate independently.

Federation SHALL be established between Universes.

A Universe MAY selectively expose one or more Dimensions through federation.

The decision to expose a Dimension SHALL be governed by the parent Universe.

---

# 11. Visibility

Dimensions MAY be classified as:

- public;
- partner;
- internal;
- restricted;
- private.

Visibility affects discoverability but SHALL NOT affect semantic identity.

---

# 12. Evolution

Dimensions MAY evolve independently.

Evolution MAY include:

- new namespaces;
- namespace retirement;
- local extensions;
- semantic refinements.

Evolution SHALL preserve identifier stability and constitutional compliance.

---

# 13. Typical Examples

Examples of Dimensions include:

Enterprise Universe

- Business
- Technology
- Finance
- Human Resources

Personal Universe

- Professional Identity
- Education
- Health
- Family

Government Universe

- Taxation
- Healthcare
- Justice
- Transportation

These examples are illustrative and not normative.

---

# 14. Architectural Invariants

Every Dimension SHALL preserve:

- reference to its parent Universe;
- constitutional compliance;
- semantic consistency;
- traceability;
- ownership;
- version integrity.

A Dimension SHALL NEVER claim sovereignty independent of its parent Universe.

---

# Future Directions

The framing of the Dimension as a management context rather than a storage partition anticipates a future **Semantic Management Context profile** describing how interpretation rules, disclosure contracts and trust policies are declared per Dimension and evaluated together when the same base object is observed from different management contexts. Such a profile would formalize how a single shared object (for example `Person`) yields different governed projections in the Product, HR, Security and Finance Dimensions without duplication of truth. This direction is anticipated but not yet normative.

---

# Final Statement

A Dimension is an autonomous semantic space within a Universe.

It provides a scalable mechanism for organizing large semantic ecosystems into coherent domains while preserving a single constitutional authority, consistent governance and interoperable federation across the entire Universe.
