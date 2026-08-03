# Registered Meta-Models

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-001  
**Title:** Registry of Compatible Meta-Models  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MMAS, MUFP  
**Informative References:** Compatibility-Matrix, Certification, Known-Implementations  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0  

---

# 1. Purpose

This document defines the concept of the Meta-Universe Registered Meta-Models Registry.

The registry provides a discoverable catalog of Meta-Models that conform to the Meta-Universe standards and can participate in semantic federation.

Registration promotes interoperability, reuse and consistent governance. It does not transfer ownership of a Meta-Model.

Registration is an act of *discovery*, not of storage: a registered entry is a reference to an authoritative source, never a copy of it.

For the broad catalogue of **external** standards, ontologies and vocabularies that a Meta-Model may import or map to (Schema.org, RDF/OWL, FHIR, ISO 20022, ESCO and ~1180 others across 37 domains), see the [External Models Registry](../06-ecosystem/External-Models-Registry.md).

---

# 2. Scope

The registry can contain:

- Domain Meta-Models;
- Foundation Meta-Models;
- Enterprise Meta-Models;
- Industry Meta-Models;
- Government Meta-Models;
- Community Meta-Models;
- Imported Standards;
- Federation Profiles.

---

# 3. Design Principles

Every registered entry is expected to be:

- discoverable;
- versioned;
- traceable;
- independently governed;
- semantically documented;
- technology independent.

Registration does not imply endorsement or certification unless explicitly stated.

---

# 4. Registry Entry

Each registry entry typically defines:

- Model Identifier;
- Model Name;
- Publisher;
- Owner;
- Current Version;
- Supported MUC Version;
- Supported MMAS Version;
- Supported MUFP Version;
- Conformance Level;
- License;
- Repository Location;
- Status.

---

# 5. Metadata

Recommended metadata includes:

- Purpose;
- Scope;
- Supported Domains;
- Primary Namespace;
- Dependencies;
- Imported Standards;
- Federation Profiles;
- Validation Assets;
- Documentation.

Metadata is preferably machine-readable.

---

# 6. Registration Status

Typical lifecycle states:

- Proposed
- Registered
- Certified (optional)
- Deprecated
- Archived

Historical entries remain discoverable.

---

# 7. Conformance

Registered Meta-Models typically declare:

- supported standards;
- conformance level;
- validation status;
- known limitations;
- compatibility notes.

Conformance remains explicit.

---

# 8. Compatibility

Compatibility can include:

- semantic compatibility;
- version compatibility;
- federation compatibility;
- mapping availability;
- profile compatibility.

Compatibility is version-specific.

---

# 9. Imported Standards

Registry entries can represent imported standards such as:

- Schema.org
- OData CSDL
- HL7 FHIR
- O*NET
- ESCO
- BPMN
- ArchiMate

Imported standards preserve provenance.

---

# 10. Governance

Each registered model identifies:

- governing authority;
- publication process;
- maintenance policy;
- issue tracking mechanism.

Ownership remains with the publisher.

---

# 11. Discovery

Consumers are able to discover:

- model metadata;
- supported versions;
- namespaces;
- repository location;
- documentation;
- federation capabilities.

Discovery precedes adoption.

---

# 12. Validation

Registry implementations typically validate:

- identifier uniqueness;
- metadata completeness;
- declared conformance;
- version consistency;
- repository availability.

Validation results are publishable.

---

# 13. Example Registry Entries

Illustrative examples:

- Employee Meta-Model
- Organization Meta-Model
- Product Meta-Model
- Software Meta-Model
- AI Agent Meta-Model
- Digital Twin Meta-Model
- Healthcare Meta-Model
- Government Meta-Model

These examples are informative.

---

# 14. Architectural Invariants

The registry preserves:

- semantic sovereignty;
- publisher ownership;
- provenance;
- traceability;
- constitutional compatibility.

Registration improves discoverability without centralizing semantic authority.

---

# 15. Federation of Registries

The Meta-Universe does not assume a single central catalog. Discovery is itself federated: registries form a *Federation of Registries*, mirroring the same sovereignty model that MUC and MUFP apply to Meta-Models. No registry owns the models it lists; each entry is a reference to an authoritative source held by its publisher.

Three complementary registry scopes are recognized:

## 15.1 Local Registry

A Local Registry operates within a single organization or Universe. It indexes the Meta-Models, Projections and Federation Profiles that the organization owns or has adopted internally. It answers the question *what semantic assets do we hold and how do they fit together*, and it remains entirely under the organization's own governance.

## 15.2 Community Registry

A Community Registry serves an industry, profession or interest community (for example healthcare, public sector or robotics). It aggregates references published by its members, applies community conventions and curates compatibility and quality information relevant to that domain. Membership and curation rules belong to the community, not to a central authority.

## 15.3 Global Registry

A Global Registry is a public index that aggregates *published* models from Local and Community Registries without owning them. It indexes metadata, versions, compatibility, conformance and federation capabilities, and points back to the authoritative source for every entry. The Global Registry is a map of the ecosystem, not a warehouse of its contents.

## 15.4 Reference, Not Copy

Across all scopes the same invariant holds: a registry entry is a *reference* to an authoritative source, not a copy of the model. Registries replicate metadata for discovery; they never replicate semantic authority. This separates Discovery from storage, so that semantic sovereignty (who holds the truth) stays with the publisher even as discoverability scales globally. Registries can themselves federate — a Global Registry can index Community Registries, which in turn index Local Registries — forming a discovery fabric aligned with MUFP federation semantics.

---

# 16. Future Directions

A dedicated **Federation of Registries** specification could formalize this model: a common metadata and reference format, registry-to-registry federation contracts, propagation and freshness rules for indexed metadata, and trust signals that let consumers weigh entries from different registry scopes. It would also define how a [Compatibility Matrix](Compatibility-Matrix.md) and [Certification](Certification.md) records are surfaced consistently across federated registries.

---

# 17. The Live Register and Seed Entries

The registry defined above is live as machine-readable data in [`registry/`](registry/): one YAML entry per model under [`registry/entries/`](registry/entries/) validating against [`registry/entry.schema.json`](registry/entry.schema.json), a flat searchable index in [`registry/registered-models.csv`](registry/registered-models.csv), and the registration flow (pull request based) in [`registry/README.md`](registry/README.md). The register files are canonical; the table below is an informative snapshot. Each entry is a reference to an authoritative source, per §15.4.

| Model | Publisher | Version | Kind | Source | Status |
|-------|-----------|---------|------|--------|--------|
| Vercy world-model catalogue | Vercy project | 0.2.0 | Example library (the world of people and events on Earth: 112 vendor-neutral models in 15 clusters, MMAS cards with own bundles and layers) | [world-models](https://github.com/ver-cy/world-models) | Draft |
| AISMM (AI-driven Software Meta-Model) | Orkestron.AI | 3.1 | Domain Meta-Model (software product) | [software-meta-model](https://github.com/orkestron-ai/software-meta-model) | Stable |
| PLMM (Product Landscape Meta-Model) | Orkestron.AI | 0.1 | Enterprise Meta-Model (product landscape, federates AISMM) | [product-landscape-meta-model](https://github.com/orkestron-ai/product-landscape-meta-model) | Draft |
| BKM (Base Knowledge Model) | Orkestron.AI | 0.4 | Foundation Meta-Model (professional knowledge as Semantic Packages) | private at time of writing | Draft |
| MOS namespace family (Axiacracy / Meta-Orchestrator State) | Orkestron.AI | 0.1 | Government Meta-Models (38 namespaces: value substrate, polity, society, economy, civilization, runtime) | [meta-orchestrator-state](https://github.com/orkestron-ai/meta-orchestrator-state) | Draft |

Context for these entries: [Case Study: The Orkestron Ecosystem](Case-Study-Orkestron-Ecosystem.md) and [Case Study: Axiacracy and the Meta-Orchestrator State](Case-Study-Axiacracy-MOS.md).

---

# Final Statement

The Registered Meta-Models Registry provides a common discovery mechanism for interoperable semantic models across the Meta-Universe ecosystem.

By publishing standardized metadata, explicit conformance information and reusable federation capabilities, the registry enables humans and AI agents to discover, evaluate, reuse and federate Meta-Models while preserving ownership, governance and long-term semantic evolution.
