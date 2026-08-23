# Versioning

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-002  
**Title:** Meta-Model Architecture Standard — Versioning Strategy  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** Meta-Universe Constitution (MUC), MMAS-Core  
**Informative References:** Naming-Conventions, MMAS-Package  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the versioning strategy for all Meta-Universe specifications, Meta-Models and related semantic artifacts.

The objective is to enable continuous evolution while preserving semantic stability, interoperability and traceability.

---

# 2. Scope

This specification applies to:

- Meta-Universe standards
- Meta-Models
- Bundles
- Layers
- Schemas
- Objects
- Projections
- Contracts
- Federation Profiles

Every version SHALL be explicitly declared.

---

# 3. Versioning Principles

Versioning SHALL:

- be explicit;
- be immutable after publication;
- preserve traceability;
- support coexistence of multiple versions;
- distinguish semantic changes from editorial changes.

No published version SHALL be silently modified.

---

# 4. Independent Versioning

Each architectural element SHALL have its own lifecycle and version.

Examples include:

- Meta-Universe Specification
- MUC
- MMAS
- MUFP
- Meta-Model
- Bundle
- Layer
- Schema
- Projection Profile
- Contract

Updating one element SHALL NOT require changing unrelated versions.

---

# 5. Semantic Versioning

Specifications SHOULD follow Semantic Versioning.

MAJOR
: Breaking semantic changes.

MINOR
: New compatible capabilities.

PATCH
: Editorial corrections, clarifications and non-semantic improvements.

Implementations MAY adopt compatible internal schemes provided semantic meaning is preserved.

---

# 6. Version Identity

Every versioned artifact SHALL declare:

- identifier;
- version;
- publication date;
- status;
- owner;
- compatibility statement.

---

# 7. Semantic Fingerprint

A version number declares *intent*; a **Semantic Fingerprint** declares *identity of meaning*. Each published meta-model version SHALL carry a Semantic Fingerprint computed over the **normalized semantic structure** of the model — its Objects, Properties, Relationships, Events, Contracts and Projections as defined by [MMAS-Core](MMAS-Core.md) — and NOT over the Markdown, file ordering, whitespace or other presentation.

The fingerprint SHOULD be a cryptographic digest (for example `sha256`) of a canonical, deterministically serialized form of the semantic structure. Two artifacts whose meaning is identical SHALL produce the same fingerprint even if their formatting differs; any change in meaning SHALL produce a different fingerprint.

A versioned artifact SHOULD declare its fingerprint alongside its version identity:

```text
Version 2.1.0
Semantic Fingerprint sha256: 8D4A...F27C
```

The Semantic Fingerprint serves several purposes:

- **Semantic equivalence detection** — confirm that two artifacts mean the same thing regardless of formatting or editorial differences;
- **Hidden incompatibility detection** — reveal meaning changes that a version number failed to reflect (for example a PATCH release whose fingerprint changed);
- **Pre-federation compatibility check** — compare fingerprints before federation to decide whether negotiation or mapping is required;
- **Dependency and migration graphs** — use fingerprints as stable nodes when constructing version dependency and migration graphs across a federation.

The fingerprint SHALL be reproducible: any conforming implementation given the same semantic structure SHALL compute the same value. The exact canonical serialization, the semantic/non-semantic field separation, and the hashing procedure are defined normatively in [MMAS-Interchange (MUIF)](MMAS-Interchange.md), with a verified worked example and a reference implementation.

The Semantic Fingerprint pairs with the [Canonical Semantic Name](Naming-Conventions.md) to identify a concept both by stable name and by stable meaning, and it is one of the metadata fields carried by a [Semantic Distribution Package](MMAS-Package.md).

---

# 8. Compatibility

Every published version SHALL state its compatibility with previous versions.

Compatibility SHOULD be classified as:

- Fully Compatible
- Backward Compatible
- Forward Compatible
- Requires Migration
- Breaking

---

# 9. Coexistence

Multiple versions MAY coexist simultaneously.

Implementations SHOULD support explicit version negotiation whenever federation involves different versions.

---

# 10. Deprecation

Artifacts SHOULD be deprecated before removal.

A deprecation notice SHALL identify:

- deprecated artifact;
- replacement;
- deprecation version;
- planned removal version.

---

# 11. Migration

Breaking changes SHALL include migration guidance.

Migration documentation SHOULD describe:

- affected concepts;
- semantic differences;
- required transformations;
- compatibility strategy;
- examples.

---

# 12. Imported Standards

Imported semantic standards SHALL preserve their original version identifiers.

Local extensions SHALL maintain an explicit mapping between imported versions and local extensions.

---

# 13. Historical Preservation

Historical versions SHALL remain identifiable and reproducible.

Previous versions SHOULD remain publicly available whenever possible.

Historical versions SHALL NOT be rewritten.

---

# 14. Version Negotiation

Federated universes SHOULD declare supported versions during capability discovery.

If incompatible versions are detected, implementations SHOULD:

- negotiate a compatible version;
- apply semantic mappings;
- request migration;
- or reject federation.

---

# 15. Architectural Invariants

Version changes SHALL NEVER invalidate:

- global identity;
- ownership;
- provenance;
- traceability;
- constitutional compliance.

These invariants are governed by MUC.

---

# 16. Future Directions

The Semantic Fingerprint enables a fingerprint-driven view of evolution that future work may standardize as a **Semantic Migration Standard (SMS)**. Such a standard would treat fingerprints as the canonical nodes of a federation-wide version dependency and migration graph, define how migration transformations are attached to fingerprint pairs, and specify how negotiating universes select a migration path automatically. The fingerprint computation itself may also warrant a small companion profile that fixes the normalization and serialization procedure so that every implementation produces byte-identical digests.

---

# Final Statement

Versioning in Meta-Universe exists to preserve semantic continuity.

Evolution is encouraged, but every change must remain explicit, traceable, compatible whenever practical and understandable by both humans and AI systems.
