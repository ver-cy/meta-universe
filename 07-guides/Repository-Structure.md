# Repository Structure

**Meta-Universe Specification**

**Document ID:** MU-V2-GUIDE-002  
**Title:** Semantic Repository Architecture  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MMAS  
**Informative References:** Getting-Started, Create-a-New-Meta-Model  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0  

---

# 1. Purpose

This guide explains the recommended Meta-Universe repository structure and the role of every major folder.

The repository layout is designed to be understandable by both humans and AI agents while supporting long-term evolution, traceability and semantic federation.

The normative counterparts of this guide are [MMAS-Package](../02-architecture/MMAS-Package.md) (the canonical layout), [Model-Traversal-and-Layout](../02-architecture/Model-Traversal-and-Layout.md) (the lossless walk contract and reserved locations for bootstraps, canon, raw data and artifacts) and [Data-Mastership](../02-architecture/Data-Mastership.md) (which system is the master of each dataset).

---

# 2. Design Goals

A Meta-Universe repository is expected to be:

- Git-native;
- modular;
- semantically organized;
- versioned;
- traceable;
- easy to navigate.

Repository organization reflects semantic architecture rather than implementation technology.

---

# 2a. Semantic Repository Architecture

The defining idea of a Meta-Universe repository is that it is organized **by semantics, not by file type or technology**. Conventional software repositories group files by what they *are* — `src/`, `docs/`, `tests/`, `lib/`, `config/`. A Meta-Universe repository instead groups documents by the *question they answer*. Each top-level folder is a question; its contents are the answer.

- `00-foundation` — **why** the standard exists;
- `01-constitution` — **which laws** it obeys;
- `02-architecture` — **how** it is built;
- `03-federation` — **how** it interacts with others;
- `04-core-concepts` — **which fundamental concepts** it uses;
- `05-reference-architecture` — **how** to apply it;
- `06-ecosystem` — **how** it lives in the wider ecosystem;
- `07-guides` — **how** to start;
- `examples` — **how** it looks in practice.

Because each folder corresponds to a question rather than a technology, the repository becomes a **semantic space** rather than a file tree. A newcomer can navigate by intent ("I need to know how this model federates" → `03-federation`), and so can an AI agent, which can map folders to questions and locate relevant knowledge without parsing file extensions. Reorganizing by technology would scatter the answer to a single question across many folders; organizing by semantics keeps each answer whole. This is the same principle the standards apply to Meta-Models — model meaning first — applied to the repository itself.

---

# 3. Recommended Structure

```
Repository/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── archive/
├── 00-foundation/
├── 01-constitution/
├── 02-architecture/
├── 03-federation/
├── 04-core-concepts/
├── 05-reference-architecture/
├── 06-ecosystem/
├── 07-guides/
├── examples/
└── schemas/ (optional)
```

---

# 4. Root Files

**README.md**

Entry point to the repository.

**LICENSE**

Publishing and reuse terms.

**CHANGELOG.md**

History of released versions.

---

# 5. archive/

Stores previous releases that remain available for historical reference.

Contents are not modified after archival.

---

# 6. 00-foundation/

Contains the conceptual foundation:

- Vision
- Principles
- Terminology
- Glossary

Read these documents first.

---

# 7. 01-constitution/

Defines the constitutional rules of the ecosystem:

- Constitution
- Governance
- Change Process
- Conformance

These documents answer *what must always remain true*.

---

# 8. 02-architecture/

Contains MMAS specifications describing how Meta-Models are built.

Typical topics include:

- versioning;
- naming;
- traceability;
- validation;
- package structure.

---

# 9. 03-federation/

Contains MUFP specifications describing semantic collaboration between independent Universes.

Typical topics include:

- trust;
- identity binding;
- synchronization;
- semantic mapping;
- federation lifecycle.

---

# 10. 04-core-concepts/

Defines the common semantic vocabulary shared across every Meta-Model.

Includes concepts such as:

- Universe;
- Object;
- Relationship;
- Projection;
- Context;
- Event;
- Lifecycle.

---

# 11. 05-reference-architecture/

Provides reusable architectural guidance.

Typical documents include:

- architecture;
- stack;
- interaction patterns;
- federation patterns;
- lifecycle patterns;
- reference diagrams.

---

# 12. 06-ecosystem/

Describes ecosystem-level capabilities.

Typical topics include:

- registries;
- compatibility;
- certification;
- implementations;
- roadmap.

---

# 13. 07-guides/

Contains practical guidance.

Examples:

- Getting Started;
- Repository Structure;
- Migration Guides;
- Publishing Guides.

Guides complement normative specifications.

---

# 14. examples/

Contains illustrative examples demonstrating correct application of the standards.

Examples are kept synchronized with current specifications.

---

# 15. schemas/ (Optional)

May contain machine-readable assets:

- JSON Schema;
- YAML;
- OpenAPI;
- OData;
- validation artifacts.

Schemas reference normative documents.

---

# 16. Navigation Strategy

Recommended reading order:

1. README
2. Foundation
3. Constitution
4. Architecture
5. Federation
6. Core Concepts
7. Reference Architecture
8. Ecosystem
9. Guides
10. Examples

---

# 17. Best Practices

Repository maintainers are encouraged to:

- keep documents focused;
- separate normative and informative content;
- preserve historical versions;
- maintain stable filenames;
- publish version metadata;
- automate validation where practical.

---

# 18. Final Statement

A well-structured repository is essential for discoverability, interoperability and long-term maintainability.

By following the recommended Meta-Universe repository organization, publishers create repositories that are easy to understand, validate, extend and federate, enabling both humans and AI agents to navigate semantic knowledge consistently across the ecosystem.
