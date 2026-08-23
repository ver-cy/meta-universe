# Change Process

**Meta-Universe Specification**

**Document ID:** MU-V2-CONST-003  
**Title:** Change Process  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** Meta-Universe Constitution (MUC), MMAS, MUFP  
**Informative References:** Governance.md, Conformance.md  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the normative process for evolving the Meta-Universe family of standards.

The objective is to enable continuous improvement while preserving long-term stability, interoperability and traceability.

---

# 2. Scope

This process applies to all normative specifications within the Meta-Universe standards family, including:

- Meta-Universe Constitution (MUC)
- Meta-Model Architecture Standard (MMAS)
- Meta-Universe Federation Protocol (MUFP)
- Future normative extensions

---

# 3. Guiding Principles

Every change SHALL follow these principles:

- Constitution before implementation.
- Explicit over implicit.
- Traceability by design.
- Backward compatibility whenever practical.
- Transparency.
- Community review.
- Versioned evolution.
- No silent semantic changes.

---

# 4. Change Lifecycle

Every change SHALL pass through the following lifecycle:

1. Proposal
2. Discussion
3. Impact Analysis
4. Draft Specification
5. Review
6. Approval
7. Publication
8. Adoption
9. Deprecation (optional)
10. Retirement (optional)

No stage SHALL be skipped for normative changes.

---

# 5. Change Request (CR)

Every proposed modification SHALL be represented as a Change Request (CR).

A CR SHOULD contain:

- unique identifier;
- title;
- motivation;
- affected documents;
- rationale;
- expected benefits;
- compatibility assessment;
- migration considerations;
- implementation impact;
- author;
- date.

---

# 6. Change Categories

Changes SHOULD be classified as one of the following:

### Editorial

Formatting, wording and clarification without changing semantics.

### Corrective

Correction of defects or ambiguities.

### Evolutionary

New capabilities that preserve compatibility.

### Breaking

Semantic changes that intentionally break compatibility.

Breaking changes SHALL require explicit justification.

---

# 6a. Semantic Change Classification

The Editorial / Corrective / Evolutionary / Breaking axis in Section 6 describes the **impact** of a change. It SHOULD be complemented by a second axis describing the **semantic subject** of the change — *what kind of meaning is affected*. This second axis is the **Semantic Change Classification**.

A change to the normative rule base SHALL additionally pass the pre-merge [Policy Consistency Check](../02-architecture/Policy-Consistency.md): a change that would make the rule set logically unsatisfiable SHALL NOT be merged.

Every Change Request SHOULD declare one or more semantic change types:

- **Model-structure change** — alters the structure of the meta-model (Objects, Relationships, Events, the shape of definitions).
- **Meaning/semantics change** — alters the meaning of an existing concept without necessarily changing its structure.
- **Federation-rules change** — alters how sovereign Universes federate, the rules of federation profiles or protocol guarantees.
- **Contract change** — alters Semantic Contracts: purpose, permissions, responsibilities or disclosure conditions.
- **Projection-behaviour change** — alters how Objects are projected into a given context.
- **Conformance-requirement change** — alters what is required to conform to a standard at any level.

The two axes are orthogonal: a single change carries both an impact category and one or more semantic change types (for example, an *Evolutionary* / *model-structure change*, or a *Breaking* / *meaning/semantics change*).

Declaring the semantic type explicitly enables AI agents to reason about change. An agent SHOULD be able to read a Change Request, determine its semantic change types, assess the resulting compatibility impact against the affected documents, and propose migration steps where compatibility cannot be preserved. Machine-readable classification therefore turns change management into an analyzable, semi-automatable process rather than a purely manual review.

---

# 7. Compatibility Assessment

Every Change Request SHALL include a compatibility assessment.

Possible outcomes include:

- Fully compatible
- Backward compatible
- Forward compatible
- Requires migration
- Breaking

---

# 8. Freeze Rule

Approved documents enter the Frozen state.

Frozen documents:

- become normative references;
- SHALL NOT receive silent modifications;
- MAY only change through a published Change Request;
- SHALL preserve complete revision history.

---

# 9. Versioning

Every published specification SHALL declare its version.

New versions SHALL be published instead of replacing previous normative releases.

Historical versions SHOULD remain publicly available.

---

# 10. Deprecation

Features MAY be deprecated before removal.

A deprecation notice SHOULD specify:

- affected feature;
- replacement;
- deprecation version;
- planned removal version.

Deprecation SHOULD precede any breaking removal.

---

# 11. Migration

Whenever compatibility cannot be preserved, migration guidance SHALL accompany the new specification.

Migration guidance SHOULD include:

- affected concepts;
- required transformations;
- compatibility strategy;
- examples.

---

# 12. Publication

Every published version SHALL include:

- version number;
- publication date;
- status;
- change summary;
- compatibility statement;
- normative references.

---

# 13. Auditability

The evolution of every normative document SHALL remain auditable.

It SHALL be possible to determine:

- why a change occurred;
- who proposed it;
- when it was accepted;
- which version introduced it.

---

# Future Directions

This document fixes the *constitutional* shape of the Semantic Change Classification — the change types and the requirement to declare them. The **detailed model** belongs to the Meta-Model Architecture Standard (MMAS): the formal taxonomy of semantic change types, their precise compatibility rules, and the machine-readable schema that lets AI agents compute compatibility impact and generate migrations. A future Semantic Migration Standard (SMS) would build on that taxonomy to standardize how migrations are expressed and applied. The Constitution establishes the axis; MMAS makes it operational.

---

# Final Principle

Meta-Universe evolves through transparent, versioned and traceable change.

Stability is preserved not by preventing evolution, but by making every evolution explicit, reviewable and reproducible.
