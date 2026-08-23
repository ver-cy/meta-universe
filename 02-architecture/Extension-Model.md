# Extension Model

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-005  
**Title:** Meta-Model Architecture Standard — Importing & Extending External Models  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** Meta-Universe Constitution (MUC), MMAS-Core, MMAS-Package  
**Informative References:** Versioning, Naming-Conventions, [Meta-Model-Composition](Meta-Model-Composition.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines how Meta-Universe Meta-Models SHALL import, reference and extend external semantic models while preserving interoperability, semantic integrity and long-term maintainability.

The objective is to encourage reuse of existing standards rather than redefining concepts that already exist.

---

# 2. Scope

This specification applies to:

- imported semantic models;
- imported namespaces;
- imported objects;
- imported relationships;
- imported vocabularies;
- local extensions;
- semantic mappings.

---

# 3. Architectural Principle

Meta-Universe SHALL prefer **extension over duplication**.

Existing semantic standards SHOULD be imported whenever they already describe the required concept with sufficient precision.

Whereas this document governs *importing and extending* an external model, the structural question of whether a concept should be a literal field, a nested (embedded) Meta-Model, or a reference to a separately governed model is specified in [Meta-Model-Composition](Meta-Model-Composition.md).

---

# 4. Semantic Package

An external standard SHALL NOT be imported as a loose collection of objects. It SHALL be imported as a **Semantic Package**: a single, versioned, self-describing unit that captures the import in full and can be reasoned about as a whole. This is the semantic-knowledge analogue of a software package manager, where a dependency is acquired as a named, versioned artifact rather than copied piecemeal.

A Semantic Package SHALL declare at minimum:

- **Source declaration** — the originating standard and its authority (for example Schema.org, O\*NET, HL7 FHIR);
- **Imported namespaces** — the namespaces brought in from the source;
- **Selected objects** — the specific concepts imported, rather than the entire source;
- **Local extensions** — extensions added on top of the imported concepts, kept separately identifiable;
- **Semantic mappings** — the explicit mappings between imported and local concepts (see Section 10);
- **Compatibility constraints** — the conditions under which the package remains valid;
- **Compatible version range** — the range of source versions the package is known to work with;
- **Semantic Fingerprint** — the package's own [Semantic Fingerprint](Versioning.md), so that consumers can detect whether two imports of the "same" standard actually agree in meaning.

Treating an import as a Semantic Package gives every dependency a stable identity, a version range and a fingerprint, exactly as a software package manager does for code, but applied to semantic knowledge. The Semantic Package is the import-time view; its distributable, publishable form is the **Semantic Distribution Package (SDP)** defined in [MMAS-Package](MMAS-Package.md), which carries the same declarations plus packaging, signature and conformance metadata.

---

# 5. Import Model

An imported model SHALL remain an independent semantic authority.

Importing a model SHALL NOT transfer ownership of:

- semantics;
- identifiers;
- versions;
- governance.

The originating standard remains authoritative.

---

# 6. Imported Metadata

Every imported model SHALL declare at least:

- source standard;
- namespace;
- imported version;
- import date;
- local owner;
- compatibility statement.

---

# 7. Imported Namespaces

Imported concepts SHALL preserve their original namespace whenever practical.

Examples:

schema:Person

fhir:Patient

odata:Entity

bpmn:Process

Local aliases MAY exist but SHALL NOT replace canonical references.

---

# 8. Extension Model

Local models MAY extend imported concepts.

Extensions SHALL:

- preserve original meaning;
- avoid modification of imported semantics;
- remain separately identifiable;
- declare ownership.

Preferred approach:

Imported Concept
        +
Local Extension
        =
Extended Concept

---

# 9. Prohibited Modifications

An implementation SHALL NOT:

- redefine imported semantics;
- silently rename imported concepts;
- change imported identifiers;
- claim ownership of imported standards.

If incompatible behavior is required, a new local concept SHALL be created.

---

# 10. Semantic Mapping

Mappings SHALL explicitly describe the relationship between imported and local concepts.

Supported mapping types MAY include:

- Equivalent
- Extension
- Specialization
- Generalization
- Derived From
- Partial Mapping
- Transformation Required

Mappings SHALL be version-aware.

---

# 11. Version Management

Imported models SHALL preserve references to their original versions.

Local extensions SHALL declare compatibility with the imported version.

Changes in imported standards SHOULD trigger compatibility assessment rather than automatic migration.

---

# 12. Multi-Source Models

A Meta-Model MAY import multiple external standards simultaneously.

Example:

- schema.org
- OData
- FHIR
- O*NET
- BPMN

Conflicts SHALL be resolved explicitly through semantic mappings.

---

# 13. Ownership

Ownership of imported concepts remains with the originating standard.

Ownership of local extensions belongs to the extending Meta-Model.

Ownership boundaries SHALL remain explicit.

---

# 14. Traceability

Every imported concept SHALL remain traceable to its origin.

Traceability SHOULD identify:

- originating standard;
- namespace;
- original identifier;
- imported version;
- extension history.

---

# 15. Federation

Federated universes SHOULD exchange canonical semantic references whenever both parties support the same imported standard.

When different standards are used, federation SHOULD rely on explicit semantic mappings rather than implicit assumptions.

---

# 16. Recommended Import Workflow

1. Discover an existing semantic standard.
2. Evaluate semantic suitability.
3. Import the canonical concept.
4. Preserve namespace and version.
5. Add local extensions only where necessary.
6. Publish semantic mappings.
7. Maintain compatibility during evolution.

---

# 17. Typical Examples

Examples of standards suitable for import include:

- Schema.org
- OData CSDL
- RDF / OWL vocabularies
- OpenAPI schemas
- BPMN
- DMN
- HL7 FHIR
- O*NET
- ESCO
- ArchiMate
- IFC
- OPC UA

The list is informative rather than exhaustive.

---

# 18. Architectural Invariants

Importing external models SHALL NEVER violate:

- Meta-Universe Constitution;
- semantic identity;
- provenance;
- ownership;
- traceability;
- version integrity.

---

# 19. Future Directions

The Semantic Package establishes the import-time unit of dependency. A future direction is to standardize the management of these packages across a federation: dependency resolution, transitive imports, version-range solving and conflict arbitration between overlapping standards, in the manner of an established package ecosystem. This converges with the **Semantic Package Registry** anticipated by [MMAS-Package](MMAS-Package.md), in which Semantic Packages are published, discovered and resolved by their [Semantic Fingerprint](Versioning.md) and compatible version range rather than by ad-hoc copying.

---

# Final Statement

Meta-Universe is designed to become a federation of semantic standards rather than a replacement for them.

The preferred architectural approach is to discover, import, reference and extend existing semantic models while preserving their identity, governance and meaning. This enables a global ecosystem of interoperable Meta-Models that evolve collaboratively instead of fragmenting into isolated semantic islands.
