# MMAS Package

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-007  
**Title:** Meta-Model Architecture Standard — Repository and Package Structure  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** Meta-Universe Constitution (MUC), MMAS-Core, Versioning  
**Informative References:** Extension-Model, MMAS-Conformance, Meta-Universe Federation Protocol (MUFP), Model-Traversal-and-Layout, Data-Mastership  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the canonical repository and package structure for Meta-Models conforming to the Meta-Model Architecture Standard (MMAS).

The objective is to ensure that every Meta-Model has a predictable organization that is understandable by both humans and AI agents.

---

# 2. Scope

This specification applies to:

- Meta-Model repositories;
- distributable Meta-Model packages;
- repository manifests;
- bundles;
- layers;
- supporting assets;
- examples and documentation.

Implementations MAY use additional files provided they do not violate this specification.

---

# 3. Design Principles

A conforming package SHALL be:

- modular;
- self-describing;
- versioned;
- traceable;
- machine-readable;
- human-readable;
- suitable for federation.

Repository structure SHALL reflect semantic architecture rather than implementation technology.

---

# 4. Canonical Repository Structure

Every Meta-Model SHOULD follow the canonical structure below.

```text
meta-model/
│
├── README.md
├── BOOTSTRAP.md            # operating instructions: how to read this model (read first)
├── LICENSE
├── CHANGELOG.md
├── manifest.yaml
├── sources.yaml            # Data Mastership Register: System of Record per dataset
│
├── bundles/
│   ├── <bundle-name>/
│   │   ├── bundle.yaml
│   │   ├── README.md
│   │   ├── <layer-name>/
│   │   │   ├── layer.yaml
│   │   │   ├── objects/
│   │   │   ├── relationships/
│   │   │   ├── events/
│   │   │   ├── contracts/
│   │   │   └── projections/
│   │   └── ...
│   └── ...
│
├── canon/                  # canonical source texts the model treats as ground truth
├── raw/                    # unprocessed harvested captures from external systems (never hand-edited)
├── artifacts/              # generated, regenerable outputs (never authored)
├── imports/
├── mappings/
├── schemas/
├── examples/
├── diagrams/
├── docs/
└── tools/
```

Equivalent layouts MAY be used if semantic organization is preserved.

The traversal contract over this structure (deterministic bundle/layer walk order, total file classification, the completeness check) and the reserved meanings of `BOOTSTRAP.md`, `canon/`, `raw/` and `artifacts/` are defined normatively in [Model-Traversal-and-Layout](Model-Traversal-and-Layout.md). The `sources.yaml` register and the rules for deciding whether the model or an external system (a wiki, a tracker, a database) is the master of a dataset are defined in [Data-Mastership](Data-Mastership.md).

---

# 5. Repository Manifest

Every repository SHALL contain a manifest.

The manifest SHOULD declare:

- identifier;
- name;
- version;
- owner;
- namespace;
- supported MMAS version;
- supported MUC version;
- supported MUFP version;
- imported standards;
- compatibility statement.

The manifest is the primary entry point for automated discovery.

---

# 6. Bundle Structure

Every Bundle SHOULD contain:

- bundle manifest;
- documentation;
- layers;
- optional examples.

Bundles SHALL have a single semantic responsibility.

---

# 7. Layer Structure

Each Layer SHOULD contain:

- layer manifest;
- object definitions;
- relationships;
- events (if applicable);
- contracts (if applicable);
- projection profiles (if applicable).

Layers SHOULD remain independently understandable.

---

# 8. Documentation

Every public repository SHOULD include:

- README;
- architecture overview;
- change history;
- licensing information;
- contribution guidance (optional).

Documentation SHALL remain synchronized with the published version.

---

# 9. Examples

Reference examples SHOULD be stored separately from normative specifications.

Examples SHALL NOT redefine normative semantics.

Example artifacts SHOULD identify the specification version they target.

---

# 10. Imported Standards

Imported semantic models SHOULD be isolated under the imports/ directory.

Mappings between imported and local concepts SHOULD be stored under mappings/.

Imported artifacts SHALL preserve references to their original source and version.

---

# 11. Repository Metadata

A repository SHOULD expose machine-readable metadata sufficient for discovery.

Recommended metadata includes:

- semantic fingerprint;
- supported profiles;
- package checksum;
- publication date;
- repository URL;
- digital signature (optional).

---

# 12. Packaging

A distributable MMAS package SHALL preserve:

- directory structure;
- manifests;
- identifiers;
- semantic references;
- version metadata.

Packaging format is implementation-specific.

Examples include Git repositories, archives or registries.

---

# 13. Semantic Distribution Package (SDP)

While Section 4 defines the canonical *repository* layout, federation requires a portable, publishable *distribution* unit. A **Semantic Distribution Package (SDP)** is that unit: a single, signed, self-contained artifact that carries a Meta-Model (or a bounded part of it) together with everything needed to verify, place and use it in another universe — analogous to a Maven, npm or OCI artifact, but for semantic models rather than code or images.

A conforming SDP SHALL contain:

- a **manifest** (`manifest.yaml`) — identity, version, owner, namespace and supported standard versions, as in Section 5;
- the **bundles and layers** that constitute the packaged Meta-Model;
- the package **[Semantic Fingerprint](Versioning.md)** computed over the normalized semantic structure;
- a **digital signature** binding the contents to a publisher;
- a **conformance declaration** stating MUC, MMAS and MUFP conformance (see [MMAS-Conformance](MMAS-Conformance.md));
- the list of **imported standards** and the corresponding [Semantic Packages](Extension-Model.md);
- the **semantic mappings** between imported and local concepts;
- optional **projections** and **examples** that aid interpretation without redefining semantics.

A representative SDP, expanded, has the following shape:

```text
employee-mm-2.3.1.sdp
│
├── manifest.yaml          # identity, version, conformance declaration
├── bundles/               # bundles & layers (objects, relationships, events, contracts, projections)
├── mappings/              # semantic mappings to imported standards
├── imports/               # imported Semantic Packages (Schema.org, O*NET, FHIR, …)
├── examples/              # optional reference examples
├── fingerprint.sha256     # Semantic Fingerprint of the normalized structure
└── signature.sig          # digital signature of the package
```

An SDP SHALL be self-verifying: a consumer SHALL be able to recompute the Semantic Fingerprint from the contained structure, check it against `fingerprint.sha256`, and validate the signature before trusting the package. The SDP is the on-the-wire and on-the-shelf form of the same composition the repository holds; it SHALL NOT redefine semantics, only package them.

---

# 14. Repository Evolution

Repository structure SHOULD evolve compatibly.

Structural changes that affect discovery or interoperability SHALL be versioned and documented.

Migration guidance SHOULD accompany structural changes.

---

# 15. AI-Native Requirements

A conforming repository SHOULD allow AI agents to:

- discover the manifest;
- enumerate bundles and layers;
- resolve imports;
- identify dependencies;
- locate examples;
- determine conformance;
- navigate the model without implementation-specific knowledge.

Repository layout SHOULD minimize ambiguity for automated reasoning.

---

# 16. Architectural Invariants

Repository organization SHALL preserve:

- semantic identity;
- traceability;
- ownership;
- version integrity;
- constitutional compliance.

Repository structure SHALL NEVER redefine semantic meaning.

---

# 17. Future Directions

The Semantic Distribution Package makes Meta-Models portable; the natural next step is to make them **discoverable and resolvable at scale**. A future direction is for the ecosystem layer (`06-ecosystem`) to operate as a **Semantic Package Registry**: a federation-aware service that indexes published SDPs and [Semantic Packages](Extension-Model.md) by identity, [Semantic Fingerprint](Versioning.md), conformance level and compatible version range, and that resolves dependencies and migrations on request — the semantic-knowledge counterpart of Maven Central, npm or an OCI registry. Such a registry would standardize publication, signature trust, search and retrieval so that any universe can locate, verify and adopt a Meta-Model without out-of-band coordination.

---

# Final Statement

The MMAS package structure is the canonical physical organization of a Meta-Model.

Its purpose is to make semantic models discoverable, reusable, extensible and interoperable across repositories, organizations and AI agents while remaining independent of implementation technologies.
