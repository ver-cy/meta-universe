# Overview: The Whole Standard, Connected

**Meta-Universe Specification**

**Document ID:** MU-V2-FOUND-006  
**Title:** Overview: The Complete, Connected Description of the Vercy Meta-Universe  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** Vision, Principles, Terminology, MUC, MMAS-Core, MUFP, Model-Traversal-and-Layout, Data-Mastership, AI-Agent-Guide, Agent-Operations  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0

---

# 1. What this document is

The specification is 90 documents. Each one is self-contained; none of them, alone, shows the whole. This document is the whole: one connected narrative of what the Vercy Meta-Universe is, how its parts fit, in what order to read them, and where the standard currently stands. Nothing here is normative; every section links to the documents that are.

If you read only one document, read this one. If you are an AI agent, read [AGENTS.md](../AGENTS.md) first instead: it is this map, compressed for machines.

---

# 2. The idea in one paragraph

Organizations, products, devices and AI agents each maintain their own world of meaning: their entities, their vocabulary, their truth. Today those worlds interoperate by copying data and hoping the meaning survives. Vercy takes the opposite stance: **meaning stays home, and understanding travels.** Every world is a sovereign **Universe** with its own constitution; knowledge is modelled once, at the source, as meta-models; other worlds receive **Projections** (views, not copies) under explicit **Contracts**; history is an append-only stream of **Events** that lets any past state of knowledge be reconstructed. Federation replaces integration: no central schema, no apex authority, no silent loss.

---

# 3. The four layers of reality

Everything in the standard sits on one ladder of abstraction:

| Layer | What lives there | Who defines it |
|-------|------------------|----------------|
| M4 | The constitution of meaning itself: what a Universe, Object, Event *is* | [MUC](../01-constitution/Meta-Universe-Constitution.md) |
| M3 | How meta-models are built, packaged, versioned, validated | [MMAS](../02-architecture/MMAS-Core.md) |
| M2 | Domain meta-models: "software product", "employee", "polity" | Model authors (e.g. AISMM) |
| M1 | Instances: *this* product, *this* person, *this* law | Universes, at runtime |

The chain of governed concepts runs: **Universe → Dimension → Namespace → Object → Projection / Event**, with Relationship, Contract, Context, Identity and Lifecycle as first-class citizens beside them. Each concept has one defining document in [04-core-concepts](../04-core-concepts/Universe.md).

---

# 4. The standards family: eight rooms, one house

The repository is organized so that each folder answers exactly one question.

| Room | Question it answers | Documents |
|------|---------------------|-----------|
| [00-foundation](Vision.md) | Why does this exist, and what do words mean? | 6 |
| [01-constitution](../01-constitution/Meta-Universe-Constitution.md) | What laws can never be broken? | 5 |
| [02-architecture](../02-architecture/MMAS-Core.md) | How is a meta-model built, laid out, walked, mastered, versioned, validated? | 18 |
| [03-federation](../03-federation/MUFP.md) | How do sovereign universes interoperate? | 14 |
| [04-core-concepts](../04-core-concepts/Universe.md) | What are the primitives? | 12 |
| [05-reference-architecture](../05-reference-architecture/Architecture.md) | How does one apply it (patterns and anti-patterns)? | 10 |
| [06-ecosystem](../06-ecosystem/Registered-Meta-Models.md) | How does it live in the world (registries, 1180 external standards, case studies)? | 11 |
| [07-guides](../07-guides/Getting-Started.md) | How do I start, as a human or an agent? | 10 |

Around the rooms: `schemas/` (10 JSON Schemas: the validatable face), `tools/` (fingerprint, validate, spec-index, requirements), `tests/` (the semantic test kit), `examples/` (minimal-person, the golden federation example, MUFP transcripts), and three machine indexes: [spec-index.yaml](../spec-index.yaml), [REQUIREMENTS-INDEX.md](../REQUIREMENTS-INDEX.md) (1284 addressable requirements), [llms.txt](../llms.txt).

---

# 5. The life of a meta-model

The documents are many; the lifecycle they describe is one.

1. **Author.** A model is written as a Git-native repository: bundles → layers → records, per [MMAS-Package](../02-architecture/MMAS-Package.md). Instructions live in `BOOTSTRAP.md`, canon texts in `canon/`, harvested evidence in `raw/`, generated output in `artifacts/`.
2. **Declare.** `manifest.yaml` declares the walk: bundle order, file classification, exclusions ([Model-Traversal-and-Layout](../02-architecture/Model-Traversal-and-Layout.md)). `sources.yaml` declares, for every dataset, who is the master: the model or an external system ([Data-Mastership](../02-architecture/Data-Mastership.md)).
3. **Verify.** A walker proves completeness (every file classified, zero orphans); [Validation](../02-architecture/Validation.md) levels V0-V5 verify syntax, structure, semantics, constitutionality, federation readiness and runtime behavior; the [Semantic Fingerprint](../02-architecture/Versioning.md) makes the model's identity reproducible.
4. **Package.** The model ships as a Semantic Distribution Package: signed, fingerprinted, self-verifying ([MMAS-Package §13](../02-architecture/MMAS-Package.md)).
5. **Federate.** Universes discover each other ([Discovery](../03-federation/Discovery.md)), bind identities, negotiate [Federation Contracts](../03-federation/Federation-Contracts.md), exchange Projections over [MUFP](../03-federation/MUFP-Messages.md), weigh each other with [Trust Vectors](../03-federation/Trust-Model.md), and preserve conflicts instead of overwriting them.
6. **Evolve.** Events accumulate on the Semantic Timeline ([Event](../04-core-concepts/Event.md)); versions follow [Versioning](../02-architecture/Versioning.md); migrations follow [Semantic-Migration](../02-architecture/Semantic-Migration.md); the [Provenance Graph](../02-architecture/Provenance-Graph.md) keeps every derivation queryable.

---

# 6. Reading paths by persona

- **Decision maker (30 min).** [Vision](Vision.md) → this document → [Case Study: Orkestron](../06-ecosystem/Case-Study-Orkestron-Ecosystem.md) and [Case Study: Axiacracy/MOS](../06-ecosystem/Case-Study-Axiacracy-MOS.md) (what it looks like in production and at civilization scale).
- **Architect.** [Principles](Principles.md) → [MUC](../01-constitution/Meta-Universe-Constitution.md) → [MMAS-Core](../02-architecture/MMAS-Core.md) → [MUFP](../03-federation/MUFP.md) → [Reference Architecture](../05-reference-architecture/Architecture.md) and [Anti-Patterns](../05-reference-architecture/Anti-Patterns.md).
- **Model builder.** [Getting-Started](../07-guides/Getting-Started.md) → [Create-a-New-Meta-Model](../07-guides/Create-a-New-Meta-Model.md) → [MMAS-Package](../02-architecture/MMAS-Package.md) → [Model-Traversal-and-Layout](../02-architecture/Model-Traversal-and-Layout.md) → [Data-Mastership](../02-architecture/Data-Mastership.md) → [Extension-Model](../02-architecture/Extension-Model.md) + [External-Models-Registry](../06-ecosystem/External-Models-Registry.md) (reuse before writing).
- **AI agent (or its author).** [AGENTS.md](../AGENTS.md) → [Agent-Operations](../07-guides/Agent-Operations.md) (operational rules on a live model) → [AI-Agent-Guide](../07-guides/AI-Agent-Guide.md) and [AI-Integration-Patterns](../07-guides/AI-Integration-Patterns.md) (building agents on the standard).
- **Human learner.** The course track at [ver.cy/learn](https://ver.cy/learn/): three structured courses from first principles to running a conformant model.

---

# 7. What exists today (honest status)

- **The specification**: 90 documents, Working Draft, 1284 indexed requirements, machine hub (spec-index, schemas, llms.txt), reference tools and a green test kit. Canonical home: [ver-cy/meta-universe](https://github.com/ver-cy/meta-universe); human portal: [ver.cy](https://ver.cy) (5 languages), spec browser at [ver.cy/spec](https://ver.cy/spec/).
- **Conformant models in production**: the Orkestron.AI product model and the DevTeam.Games platform model both carry the full ARCH-017/018 shape (entry bootstrap, walk manifest, mastership register, coverage walker at zero orphans, vendored canon, live mastership statuses including a retired system of record and an automated model→site drift watch).
- **Ecosystem**: AISMM v3 (stable) as the flagship domain meta-model; PLMM (draft) above it; 1180 external standards catalogued with compositional roles; two in-depth case studies.
- **Not yet**: a live registry service, certification, SDKs, and the candidate future standards (SVF, MMQS, SMS, MUDL, Semantic Package Registry) tracked in [Roadmap](../06-ecosystem/Roadmap.md).

---

# Final Statement

Vercy is one idea applied uniformly at every scale: meaning has a home, homes have laws, and understanding between homes is negotiated, versioned and traceable rather than copied and hoped for.

The rest of the specification is that idea, made precise.
