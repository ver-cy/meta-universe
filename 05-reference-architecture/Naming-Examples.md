# Naming Examples

**Meta-Universe Specification**

**Document ID:** MU-V2-REFARCH-008  
**Title:** Naming Examples  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MMAS (Naming Conventions)  
**Informative References:** Reference Repository, Anti-Patterns  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document provides illustrative naming examples for Meta-Universe compliant repositories, Meta-Models and semantic artifacts.

It complements the normative Naming Conventions specification by demonstrating recommended naming practices through concrete examples.

---

# 2. Design Principles

Names SHOULD be:

- clear;
- stable;
- human-readable;
- AI-readable;
- technology independent;
- semantically meaningful.

Names SHOULD describe concepts rather than implementations.

---

# 3. Repository Names

Recommended:

- employee-meta-model
- product-meta-model
- software-meta-model
- organization-meta-model
- healthcare-meta-model

Avoid:

- model-v2-final
- temp-repository
- test123
- new-model

---

# 4. Folder Names

Recommended:

- 00-foundation
- 01-constitution
- 02-architecture
- 03-federation
- 04-core-concepts
- 05-reference-architecture
- 06-domain-models
- 07-guides
- examples

Avoid:

- misc
- docs2
- stuff
- temp

---

# 5. Document Names

Recommended:

- Employee.md
- Organization.md
- Projection.md
- Semantic-Mapping.md
- Federation-Contracts.md

Avoid:

- employee_final_v3.md
- new_file.md
- draft2.md

Normative filenames SHOULD remain stable across releases.

---

# 6. Namespace Examples

Recommended:

- employee
- organization
- finance
- healthcare
- ai-agent
- software

Qualified examples:

- employee:Employee
- employee:Skill
- organization:Department
- product:Product
- software:Service

---

# 7. Object Examples

Recommended object names:

- Employee
- Department
- Product
- Customer
- Invoice
- Contract
- Service
- AIAgent

Object names SHOULD represent business concepts.

---

# 8. Relationship Examples

Recommended:

- reportsTo
- memberOf
- owns
- assignedTo
- dependsOn
- implements
- supervises
- belongsTo

Relationship names SHOULD express semantic meaning.

---

# 9. Event Examples

Recommended:

- EmployeeCreated
- ContractApproved
- ProjectionPublished
- IdentityBound
- FederationEstablished
- SynchronizationCompleted

Events SHOULD describe completed occurrences.

---

# 10. Projection Examples

Recommended Projection names:

- EmployeePublicProjection
- EmployeeHRProjection
- EmployeePayrollProjection
- ProductCatalogProjection
- IncidentSummaryProjection

Projection names SHOULD indicate context.

---

# 11. Contract Examples

Recommended:

- EmployeeDisclosureContract
- HRFederationContract
- ProductExchangeContract
- AIAgentCapabilityContract

Contract names SHOULD indicate purpose.

---

# 12. Identity Examples

Canonical Identity:

employee:550e8400-e29b-41d4-a716-446655440000

Local Identity:

HR-10245

Binding:

employee:550e8400... ↔ HR-10245

Canonical Identity SHOULD remain globally stable.

---

# 13. Version Examples

Recommended:

- 1.0.0
- 1.2.1
- 2.0.0

Avoid:

- final
- latest
- vNext

Semantic Versioning SHOULD be used.

---

# 14. Complete Naming Example

Repository:

employee-meta-model

Namespace:

employee

Object:

Employee

Relationship:

reportsTo

Projection:

EmployeeHRProjection

Contract:

EmployeeDisclosureContract

Event:

EmployeePromoted

This naming sequence demonstrates consistent semantic naming across architectural layers.

---

# 15. Architectural Checklist

Before publishing:

- Is the name stable?
- Is it technology independent?
- Is it semantically meaningful?
- Is it understandable without implementation knowledge?
- Is it consistent with MMAS Naming Conventions?

---

# 16. Toward a Semantic Style Guide

The examples in this document address *naming*, but naming is only one facet of stylistic consistency. The same way the *Google Java Style Guide* governs far more than identifier names — covering layout, comments, idioms and uniform phrasing so that thousands of engineers write code that reads as if one author produced it — the Meta-Universe benefits from a single **Semantic Style Guide** that governs how semantic models are *written*, not just named.

A Semantic Style Guide would standardize, in one place:

- **Naming rules** — the conventions illustrated throughout this document (repositories, namespaces, Objects, Relationships, Events, Projections, Contracts, identities, versions).
- **Entity-description rules** — how an Object, Relationship or Event is described, in what order, with what level of detail.
- **Uniform phrasing** — a consistent voice and sentence shape for definitions, so that descriptions read the same across thousands of independently authored models.
- **Relationship and Event conventions** — verb forms for Relationships (`reportsTo`, `dependsOn`) and past-tense completed forms for Events (`EmployeePromoted`, `ContractApproved`).
- **Final Statement style** — a consistent closing-statement form for every document.
- **Uniform Purpose / Scope / Principles** — a shared opening structure so each document presents its purpose, scope and design principles in the same recognizable way.
- **Domain-meta-model recommendations** — house style for assembling a complete domain model from these parts.

The goal is *machine-mergeable uniformity*: when thousands of organizations publish semantic models in one consistent style, AI agents can understand, analyze, compare and merge them far more reliably than if each publisher invented its own phrasing. Style consistency is not cosmetic — for an AI-native ecosystem it is a precondition for automated reasoning across models.

---

# Future Directions

The **Semantic Style Guide** described above is expected to grow into a standalone informative companion to the normative Naming Conventions — a Meta-Universe equivalent of a language style guide, covering naming, description, phrasing, Relationship/Event conventions, document structure and Final Statement form. Its measure of success is simple: any two organizations following it would produce models an AI agent could read, analyze and merge as though they came from a single author.

---

# Final Statement

Consistent naming is essential for long-term semantic interoperability.

By applying stable, meaningful and technology-independent names, Meta-Universe implementations become easier to understand, validate, federate and evolve for both humans and AI agents while preserving semantic clarity across repositories and domains.
