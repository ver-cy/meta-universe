# Case Study: The Orkestron Ecosystem

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-010  
**Title:** Case Study: The Orkestron Ecosystem as a Working Meta-Universe  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [Known-Implementations](Known-Implementations.md), [Registered-Meta-Models](Registered-Meta-Models.md), [Meta-Model-Composition](../02-architecture/Meta-Model-Composition.md), [Extension-Model](../02-architecture/Extension-Model.md), [AI-Agent-Guide](../07-guides/AI-Agent-Guide.md), [Case-Study-Axiacracy-MOS](Case-Study-Axiacracy-MOS.md)  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0

---

# 1. Purpose

This case study documents a real, running ecosystem of meta-models and products, the **Orkestron ecosystem**, as a worked illustration of Meta-Universe concepts in production use.

It exists for two reasons:

1. **Evidence.** The standard should be able to point at at least one place where its concepts (Universe, Dimension, Namespace, Object, Projection, Event, Semantic Package, Federation) are not hypothetical but carry live products.
2. **Feedback.** Several parts of this specification (the composition layer, the external-model registry, the AI-agent guidance) were shaped by problems first hit inside this ecosystem. Recording the mapping keeps that lineage honest.

This document is informative. Nothing in it is required for conformance, and listing the ecosystem here does not imply certification (see [Known-Implementations](Known-Implementations.md)).

For a second, larger-scale case study (a whole polity modelled as one Meta-Universe Dimension), see [Case Study: Axiacracy and the Meta-Orchestrator State](Case-Study-Axiacracy-MOS.md).

---

# 2. The ecosystem at a glance

Orkestron is an ecosystem for **AI agents doing professional work**, organized as four surfaces:

| Surface | Role | Meta-Universe reading |
|---------|------|-----------------------|
| **orkestron.ai** | The facade: explains the service | The Universe's public self-description |
| **orkestron.dev** | Supplier side: standards, norms, supplier cabinet, agent runtimes | The Universe's constitution and architecture layer |
| **orkestro.net** | Marketplace: deal mechanics, customer cabinet | Federation surface: where independent parties transact over shared semantics |
| **Agent runtime** (Agent Hub, PA-service) | Where agents actually execute | Object instantiation and event generation |

Around these surfaces lives a family of open meta-model specifications, and around those a fleet of concrete products (an event platform, realm storefronts, landing sites, an AI-guide). Every product carries its own structured product model; the specifications define what such a model is.

---

# 3. The meta-model family

Four specifications form the semantic backbone. Each one occupies a distinct level, and together they illustrate the Meta-Universe layering (M1 to M4) in practice.

## 3.1 AISMM: one product as a full-context model

**AISMM (AI-driven Software Meta-Model)**, now published at [ver-cy/software-meta-model](https://github.com/ver-cy/software-meta-model) (v3.2.0, Apache-2.0; complete Orkestron history preserved), models a **single software product** as a complete system: why it exists, what value it creates, how it is designed, specified, implemented, operated, controlled and changed. Models are human-readable and machine-readable, with UUID-stable identities, a registry file and portable bindings for Git, filesystems, databases, object stores, HTTP and MCP.

Meta-Universe reading:

- AISMM is a **domain meta-model** (M2) for the domain "software product".
- One AISMM product model is a **Namespace**: a governed set of Object definitions and their instances (features, decisions, components, releases).
- The registry file (`aismm.registry.json`) plays the role of the Namespace's machine-readable self-description, the pattern this standard generalizes as spec indexes and package manifests.

## 3.2 PLMM: the landscape as a federation above AISMM

**PLMM (Product Landscape Meta-Model)**, published at [orkestron-ai/product-landscape-meta-model](https://github.com/orkestron-ai/product-landscape-meta-model) (v0.1, Apache-2.0), models the **portfolio between products**: registry, dependency and integration graph, shared capabilities, ownership, governance, in eleven layers.

Meta-Universe reading:

- PLMM is a **federation-shaped meta-model**: it does not absorb product models, it **references** them. Each product keeps its sovereign AISMM model; PLMM holds the relations.
- This is exactly the Meta-Universe stance on federation: sovereignty of the parts, a connective layer for the whole. Where MUFP federates *between organizations*, PLMM applies the same discipline *inside* one organization.

## 3.3 BKM: knowledge as a distributable package

**BKM (Base Knowledge Model)** (v0.4, private at the time of writing) defines how a **profession's knowledge** is packaged so an AI agent can load it as its core competence. Packs exist for the Analyst and Event-Management professions (the latter with 179 entities).

Meta-Universe reading:

- A BKM pack is a **Semantic Package**: versioned, distributable, importable knowledge with declared conformance.
- The agent architecture that consumes it separates three contexts: **Agent Core** (the portable BKM pack), **Role Context** (per-employer identity and scope), **Task Context** (the concrete assignment). This is a live instance of the Context and Perspective concepts: one body of knowledge, projected differently per role and task, without copying it.

## 3.4 Contracts: executable semantics of a mission

The **software-agents-contracts** specification defines Contract, Protocol and Deliverable: the regulated execution of one atomic mission by an agent.

Meta-Universe reading:

- A Contract is an **Executable Semantic Contract** in the sense of this standard: an agreement whose meaning is precise enough to drive execution and verification, not just documentation.

---

# 4. Mapping table

| Meta-Universe concept | Orkestron realization |
|-----------------------|------------------------|
| Universe | The Orkestron ecosystem as a sovereign semantic jurisdiction |
| Dimension | A surface or major management context (marketplace, supplier side, a product family) |
| Namespace | One product's AISMM model; one BKM pack; one PLMM layer |
| Object | A feature, decision, component, agent, mission, deal |
| Projection | A realm storefront's read-only view; a supplier dashboard; a customer cabinet |
| Event | A mission executed, a deal closed, a release shipped, a track-record entry |
| Semantic Package | A BKM profession pack; an imported external standard |
| Federation Contract | A realm API token contract; a marketplace deal |
| Trust | Agent track record and rank (APM); control policies with autonomy ramps |

---

# 5. Federation in practice: realms

The clearest production illustration of Projection and Federation is the **realm** pattern of the ecosystem's event platform.

A realm is a scoped slice of platform data (events, organizers) exposed through a token-authenticated **realm API**. Independent storefront sites, each with its own brand, languages and editorial voice, consume a realm as a **read-only projection**:

- The platform stays **sovereign**: it owns the data, its schema and its lifecycle.
- Each storefront holds a **contract** (the token and the API surface), not a copy of the platform's internals.
- Data crosses the boundary **as projections**, on demand, in the consumer's presentation context.
- Several national storefronts run this way in production, each a separate consumer of the same sovereign source.

This is MUFP's core promise in miniature: *interoperability without absorption*. The pattern was running before this standard formalized it, and it survived replication across consumers precisely because the sovereignty boundary was never blurred.

---

# 6. Composition and external standards in practice

AISMM v3.2 includes an **external-binding layer** and the MMAS 2.1 portable data-surface contract: a product model does not restate public standards or confuse its semantics with one storage carrier. In ecosystem practice, models bind to identifiers and vocabularies such as ISO 3166, LEI, ESCO, schema.org types and W3C ORG.

Working through real bindings surfaced the questions this standard now answers normatively:

- *When is an external concept a field, a nested model, or a reference?* Answered by [Meta-Model-Composition](../02-architecture/Meta-Model-Composition.md) (ARCH-016).
- *Which standard should I bind to for a given concept?* Answered by the [External Models Registry](External-Models-Registry.md) (1180 catalogued standards with compositional roles) and the [Connector Catalogue](Connector-Catalogue.md).

---

# 7. Lessons the standard took from this ecosystem

1. **Registry files pay for themselves.** Every model that shipped with a machine-readable registry survived tooling changes; every model without one eventually needed reconstruction. Hence the emphasis on spec indexes, package manifests and fingerprints.
2. **Sovereignty is an operational property, not a slogan.** The realm pattern works because the boundary is enforced by contract and token, not by convention. Federation concepts in this standard are written to be enforceable the same way.
3. **Knowledge wants to be a package.** Separating portable knowledge (BKM) from role and task context turned single-purpose agents into reusable specialists. The Semantic Package concept generalizes this.
4. **Federation inside an organization is still federation.** PLMM showed that referencing sovereign models beats merging them even when one legal entity owns everything. Absorption creates staleness; reference creates accountability.
5. **A model that AI agents cannot traverse will not be maintained.** Every artifact in the family is designed to be read by agents first and humans equally; this drove the AI-facing guidance in [AI-Agent-Guide](../07-guides/AI-Agent-Guide.md).

---

# 8. Status and references

- Ecosystem origin: Orkestron.AI. AISMM stewardship moved to the Vercy project with its complete Git history and attribution preserved.
- Public repositories: [software-meta-model](https://github.com/ver-cy/software-meta-model), [product-landscape-meta-model](https://github.com/orkestron-ai/product-landscape-meta-model).
- The standard itself is published vendor-neutrally at [ver.cy](https://ver.cy) with sources at [ver-cy/meta-universe](https://github.com/ver-cy/meta-universe); Orkestron appears in this document strictly as one known implementation.

Maturity, in the vocabulary of [Known-Implementations](Known-Implementations.md) §7: **Production** (surfaces and realm federation), **Reference Implementation** (AISMM), **Experimental** (PLMM, BKM, contracts).
