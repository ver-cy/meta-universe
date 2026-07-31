# Changelog

All notable changes to the Meta-Universe specification are recorded here.
This project follows the evolution and versioning rules defined in
[Versioning](02-architecture/Versioning.md) and [Change-Process](01-constitution/Change-Process.md).

## [Unreleased]

### Added
- **Model-Traversal-and-Layout** (Normative, MU-V2-ARCH-017,
  `02-architecture/`): the lossless traversal contract for Meta-Model
  repositories: single entry point (`BOOTSTRAP.md` + `manifest.yaml`), declared
  bundle/layer walk order, total file classification (kind + origin), the
  completeness rule (every file enumerated, well-known or excluded; orphans fail
  V1), and reserved locations `canon/`, `raw/`, `artifacts/`, `bootstrap/`.
- **Data-Mastership** (Normative, MU-V2-ARCH-018, `02-architecture/`): Systems
  of Record for Meta-Models: one master per dataset; three lawful patterns
  (model-mastered with write-back projections, external-mastered with harvested
  mirrors, partitioned); the `sources.yaml` Mastership Register; flow, freshness,
  conflict and AI-agent write rules.
- [MMAS-Package](02-architecture/MMAS-Package.md) §4 canonical tree extended
  with `BOOTSTRAP.md`, `sources.yaml`, `canon/`, `raw/`, `artifacts/` and
  pointers to the two new standards.

### Added (description, agents, learning)
- **Overview** (Informative, MU-V2-FOUND-006, `00-foundation/`): the complete,
  connected description of the whole standard: the idea, the M1-M4 layers, the
  eight-room map, the life of a meta-model, reading paths per persona, honest
  status. The single entry point for humans.
- **Agent-Operations** (Informative, MU-V2-GUIDE-010, `07-guides/`): operating
  instructions for AI agents working on a conformant model: cold-start,
  authority-aware answering, write rules, harvest/publish recipes, refusal
  conditions, team etiquette. [AGENTS.md](AGENTS.md) now routes agents to it.
- **Vercy Learn** ([ver.cy/learn](https://ver.cy/learn/)): three structured
  courses for humans (Foundations · Building a meta-model · Vercy for AI
  agents; 15 lessons), maintained site-side, linked from the spec.

### Changed
- Pilot feedback (first ARCH-017/018 pilot on a production AISMM model):
  [Model-Traversal-and-Layout](02-architecture/Model-Traversal-and-Layout.md)
  now blesses **centralized classification rules** (`kind_rules` in the
  repository manifest with the `{prefix}` placeholder) as an equivalent
  alternative to per-layer enumeration for convention-named files;
  [Data-Mastership](02-architecture/Data-Mastership.md) register entries gained
  a **`status` lifecycle field** (`active` / `declared` / `suspended` /
  `retired`), making "mastership decided, flow not yet built" a lawful,
  visible, validated state instead of hidden debt.
- **Case studies** (Informative, `06-ecosystem/`): [The Orkestron Ecosystem](06-ecosystem/Case-Study-Orkestron-Ecosystem.md)
  (MU-V2-ECO-010): a production ecosystem of meta-models (AISMM, PLMM, BKM,
  agent contracts) and federated realm projections; and
  [Axiacracy / Meta-Orchestrator State](06-ecosystem/Case-Study-Axiacracy-MOS.md)
  (MU-V2-ECO-011): a whole polity modelled as one Dimension with 38 namespaces,
  the largest known application of the standard.
- **Seed entries** (Informative) in [Registered-Meta-Models](06-ecosystem/Registered-Meta-Models.md) §17:
  first concrete registry references (AISMM 3.1, PLMM 0.1, BKM 0.4, the MOS
  namespace family).
- Case-study cross-references from [Known-Implementations](06-ecosystem/Known-Implementations.md) §8
  and the README Ecosystem section.

## [2.0.0-draft] — Working Draft

The first full standards-family release. Meta-Universe is no longer a single
conceptual document but an ISO-like family of standards: **MUC + MMAS + MUFP +
Core Concepts + Reference Architecture + Ecosystem + Guides**.

### Added
- **Standard Header** across every document (Document Class, Normative /
  Informative References, Copyright, Apache-2.0 License).
- **The Meta-Universe Manifesto** (Vision) — fifteen quotable beliefs.
- **Event** (`04-core-concepts/Event.md`) — the missing semantic primitive, with
  the *Semantic Timeline* (reconstruct any past state of knowledge).
- **Validation** (`02-architecture/Validation.md`) — layered validation levels
  V0–V5 and the relationship to Conformance and Certification.
- Concept additions throughout the spec, including: Semantic Fingerprint,
  Canonical Semantic Name (CSN), Semantic Lineage, Semantic Package, Semantic
  Distribution Package (SDP), Trust Vector, Negotiation of Knowledge,
  Conflict Preservation, Semantic Coherence, Relationship Profile, Executable
  Semantic Contract, Federation of Registries, multidimensional Compatibility,
  and a consolidated *Candidate Future Standards* list (SVF, MMQS, SMS, MUDL,
  Semantic Package Registry).

### Changed
- **Principles** reorganized into four value families (Reality, Federation,
  Architecture, Longevity).
- **Constitution (MUC)** restructured into six chapters with continuously
  numbered articles; added **Article 10 — Semantic Discovery** and
  **Article 15 — Security and Confidentiality**.
- **README** rebuilt as a GitHub landing page (navigation, Mermaid diagrams,
  collapsible sections, status legend, ecosystem map).
- License changed to **Apache-2.0**.

### Migrating from v1.x
See [Migration-from-v1](07-guides/Migration-from-v1.md). The key concept rename
is **Galaxy → Namespace**; the architecture is now
*Universe → Dimension → Namespace → Object → Projection*.
