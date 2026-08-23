# Naming Conventions

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-003  
**Title:** Meta-Model Architecture Standard — Naming Conventions  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** Meta-Universe Constitution (MUC), MMAS-Core  
**Informative References:** Versioning, Meta-Universe Federation Protocol (MUFP)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the naming rules used throughout the Meta-Universe ecosystem.

Consistent naming improves discoverability, semantic interoperability, federation, automation and long-term maintainability.

---

# 2. Scope

These rules apply to:

- Meta-Universe standards
- Meta-Models
- Bundles
- Layers
- Objects
- Properties
- Relationships
- Events
- Contracts
- Projection Profiles
- Namespaces

Implementations MAY define additional local conventions provided they remain compatible with this specification.

---

# 3. Naming Principles

Names SHALL be:

- unambiguous;
- stable;
- human-readable;
- machine-readable;
- technology independent;
- semantically meaningful.

Names SHALL describe concepts rather than implementation details.

---

# 4. Canonical Language

English SHALL be the canonical language for all normative names.

Localized labels MAY be provided as metadata.

Canonical identifiers SHALL remain language-independent.

---

# 5. Identifier vs Display Name

Every significant artifact SHOULD distinguish between:

- Identifier (stable)
- Display Name (human-friendly)

Example:

Identifier:
employee.performance-review

Display Name:
Employee Performance Review

Display names MAY change.

Identifiers SHOULD remain stable.

---

# 6. Canonical Semantic Name (CSN)

The distinction between Identifier and Display Name is generalized, for every public concept, into a **Canonical Semantic Name (CSN)**. Each public concept SHALL have both:

- a **Human / Display Name** — localized, human-friendly, and free to change (for example "Salary Agreement");
- an immutable **Canonical Semantic Name (CSN)** — a stable, technology-independent identifier of meaning (for example `employee.compensation.salaryAgreement`).

Example:

```text
Display Name : Salary Agreement
CSN          : employee.compensation.salaryAgreement
```

The CSN is analogous to a fully-qualified class name or an RDF URI, but it is deliberately **technology-independent**: it commits to no programming language, serialization or transport. It expresses the position of a concept within its semantic hierarchy and nothing more.

Rules:

- Every public concept SHALL have exactly one CSN.
- A CSN SHALL be immutable once published; renaming a concept SHALL be treated as a semantic change under [Versioning](Versioning.md) and SHALL produce a new CSN, never a silent rewrite of the existing one.
- All **federation interactions SHALL exchange CSNs**. The Meta-Universe Federation Protocol (MUFP) transmits CSNs; it SHALL NOT rely on Display Names for identity.
- User interfaces SHOULD present the localized Display Name while resolving it to the underlying CSN.
- Display Names MAY differ across languages, contexts and presentations; the CSN SHALL remain the same.

To prevent name collisions across a federation, a CSN SHOULD be paired with the [Semantic Fingerprint](Versioning.md) of the concept's defining version. Together, the CSN identifies *which concept* and the fingerprint identifies *which meaning*, so that two universes using the same CSN can detect whether they actually agree on its semantics before relying on it.

---

# 6a. CSN Grammar and Identifier Scheme

To make CSNs and identifiers machine-checkable, this section gives their formal grammar.

A **Canonical Semantic Name** SHALL conform to the following ABNF (RFC 5234):

```abnf
CSN       = segment *("." segment)
segment   = lower *(ALPHA / DIGIT)
lower     = %x61-7A            ; a-z  (a segment SHALL start lowercase)
ALPHA     = %x41-5A / %x61-7A
DIGIT     = %x30-39
```

The first `segment` is the **namespace**; the remaining segments name the concept within it (for example `employee.compensation.salaryAgreement` — namespace `employee`). This grammar is the normative source for the `csn` pattern in [`schemas/common.schema.json`](../schemas/common.schema.json) and is enforced by check `V2-03` in [Validation](Validation.md).

An **Identifier** (the `id` of an Object, Relationship, Event, Contract or Projection, and the value of a Local Identity) is opaque and SHALL be stable for the lifetime of the thing it names. An implementation SHALL adopt one of the following identifier schemes, declared so that consumers can resolve it:

| Scheme | Form | Example |
|--------|------|---------|
| `uuid` | a UUID | `9d3f2c1a-...` |
| `uri` | an absolute URI | `https://acme.example/person/12345` |
| `urn` | a URN | `urn:mu:person:9d3f2c1a` |
| `qname` | `scheme:value` within a Universe | `employee:12345` |

Identifiers SHALL be compared as exact byte strings; they SHALL NOT be case-folded or normalized. A [Canonical Identity](../04-core-concepts/Identity.md) pairs a scheme with a value (`{ "scheme": "urn", "value": "urn:mu:person:9d3f2c1a" }`). New schemes MAY be registered without breaking existing identifiers.

---

# 7. Namespace Convention

Every public concept SHALL belong to a namespace.

Recommended format:

namespace:Concept

Examples:

employee:Skill

organization:Department

product:Capability

schema:Person

fhir:Patient

Namespaces SHALL be globally unique within their semantic scope.

---

# 8. Meta-Model Naming

Meta-Models SHOULD use descriptive names.

Recommended examples:

Employee Meta-Model

Product Landscape Meta-Model

Enterprise Landscape Meta-Model

Avoid implementation-specific names.

---

# 9. Bundle Naming

Bundle names SHOULD be nouns representing semantic domains.

Examples:

Identity

Knowledge

Governance

Runtime

History

Security

---

# 10. Layer Naming

Layers SHALL represent one coherent semantic concern.

Layer names SHOULD:

- use singular nouns;
- avoid abbreviations;
- avoid technology names.

Examples:

Employment History

Projects

Compensation

Competencies

---

# 11. Object Naming

Object names SHOULD:

- use singular nouns;
- represent real or conceptual entities;
- avoid implementation terminology.

Preferred:

Employee

Project

Skill

Avoid:

EmployeeTable

ProjectDTO

SkillRecord

---

# 12. Property Naming

Property names SHOULD:

- describe facts;
- use lowerCamelCase;
- avoid prefixes;
- avoid implementation suffixes.

Preferred:

firstName

createdAt

currentPosition

Avoid:

emp_name

fld1

col_employee

---

# 13. Relationship Naming

Relationship names SHOULD describe semantic meaning.

Examples:

worksFor

reportsTo

owns

dependsOn

assignedTo

Generic names such as "link" or "relation" SHOULD be avoided.

---

# 14. Event Naming

Events SHOULD describe completed facts.

Recommended pattern:

<Entity><PastTenseVerb>

Examples:

EmployeeCreated

ContractSigned

ProjectArchived

Avoid imperative names.

---

# 15. Contract Naming

Contracts SHOULD describe the business or semantic purpose.

Examples:

Employment Contract

Knowledge Disclosure Contract

Federation Agreement

Avoid implementation-oriented names.

---

# 16. File Naming

Specification documents SHOULD use:

Title-Case-With-Hyphens.md

Examples:

Meta-Universe-Constitution.md

Federation-Contracts.md

Identity-Binding.md

Example files SHOULD include the suffix:

.example.yaml

---

# 17. Reserved Terms

The following terms are reserved by the Meta-Universe standards family:

Universe

Dimension

Namespace

Meta-Model

Bundle

Layer

Object

Projection

Relationship

Event

Contract

Context

Identity

These terms SHALL NOT be redefined with incompatible meanings.

---

# 18. Imported Standards

Imported concepts SHALL preserve their original names whenever practical.

Local extensions SHOULD extend imported concepts instead of renaming them.

Example:

schema:Person

↓

employee:Employee

---

# 19. Naming Stability

Identifiers SHALL remain stable across compatible versions.

Renaming SHOULD be treated as a semantic change.

Migration guidance SHALL be provided whenever identifiers change.

---

# 20. Future Directions

The Canonical Semantic Name establishes a stable, technology-independent identity layer that future work may elaborate into a **Semantic Style Guide**: a companion standard defining the grammar of CSN segments, casing and pluralization rules, recommended hierarchy depth, and the resolution algorithm by which a localized Display Name maps to a CSN across languages. Such a guide would also specify a federation-wide CSN resolution service, so that any universe can dereference a CSN to its defining version and [Semantic Fingerprint](Versioning.md), closing the loop between naming and meaning.

---

# Final Statement

Consistent naming is a prerequisite for semantic interoperability.

The purpose of these conventions is not stylistic consistency alone, but the creation of stable, globally understandable semantic models that can evolve, federate and be interpreted reliably by both humans and AI systems.
