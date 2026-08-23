# Semantic Mapping

**Meta-Universe Specification**

**Document ID:** MU-V2-FED-006  
**Title:** Semantic Mapping — Mapping Different Vocabularies  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MMAS, MUFP  
**Informative References:** Identity-Binding.md, Synchronization.md, [Meta-Model-Composition](../02-architecture/Meta-Model-Composition.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the Semantic Mapping model used by the Meta-Universe Federation Protocol (MUFP).

Semantic Mapping enables independent Universes to exchange knowledge even when they use different vocabularies, Meta-Models or external standards.

Mappings establish semantic correspondence without requiring either participant to modify its own authoritative model.

Crucially, Semantic Mapping in the Meta-Universe maps each local semantics to a **shared canonical meaning**, not to every other participant in turn. This replaces the quadratic burden of pairwise integration with a linear one against a common reference.

---

# 2. Scope

This specification applies to:

- Universes;
- Dimensions;
- Namespaces;
- Meta-Models;
- Objects;
- Relationships;
- Properties;
- Events;
- Projection Profiles;
- imported standards.

---

# 3. Mapping Principles

Every Semantic Mapping SHALL be:

- explicit;
- traceable;
- version-aware;
- technology independent;
- non-destructive;
- explainable.

Mappings SHALL describe semantic correspondence.

They SHALL NOT redefine canonical meaning.

---

# 4. Definition

A Semantic Mapping is a first-class semantic artifact describing the relationship between concepts originating from different semantic authorities.

Mappings enable interoperability while preserving sovereignty.

---

# 4a. The Canonical-Meaning Hub Model

Naive interoperability maps every model directly to every other model. For *N* participants this requires up to *N × (N − 1)* directed mappings — a quadratic, bespoke and unmaintainable burden in which each new participant must integrate separately with all the others.

```text
Pairwise (quadratic)            Canonical hub (linear)

A ── B                                A
│ ╲ ╱ │                               │
│  ╳  │                          B ── Canonical ── D
│ ╱ ╲ │                               │
C ── D                                C
```

The Meta-Universe SHOULD instead map each local semantics to a **canonical meaning** recognized by the federation parties. Each participant maintains mappings only between its own model and the canonical meaning; correspondence between any two participants is then composed through the hub. The integration cost becomes linear: a new participant publishes one set of mappings to the canonical meaning and immediately interoperates with all others.

A canonical meaning MAY be an agreed neutral concept, or an external standard adopted as the reference (for example O*NET, ESCO, HR-XML or Schema.org). The hub model SHALL NOT require any participant to adopt the canonical meaning as its own authoritative model; participants map *to* it, they do not surrender *to* it.

---

# 4b. The Semantic Mapping Registry

To make canonical-meaning mappings reusable rather than re-authored per federation, MUFP introduces the **Semantic Mapping Registry**: a curated, versioned library of mappings between commonly used standards and canonical meanings.

A Semantic Mapping Registry SHOULD hold reusable mappings such as those between O*NET, ESCO, HR-XML and Schema.org, each carrying its authority, version and provenance. With such a registry, an Employee Meta-Model can interoperate with partners across HR, recruitment and labour-market systems by referencing published mappings to those standards, instead of negotiating a bespoke per-pair integration each time. A registry entry is consulted, not copied; the authoritative models on either side remain unchanged.

Registry mappings SHALL remain subject to every requirement of this document — they are ordinary Semantic Mappings that happen to be published for reuse.

---

# 5. Mapping Types

Typical mapping types include:

- Equivalent
- Extension
- Specialization
- Generalization
- Derived From
- Alias
- Transformation Required
- Partial Mapping
- No Known Mapping

Domain standards MAY introduce additional mapping types.

---

# 6. Mapping Components

Every Semantic Mapping SHOULD define:

- canonical identifier;
- source concept;
- target concept;
- mapping type;
- mapping rationale;
- confidence (when applicable);
- governing authority;
- version;
- provenance.

---

# 7. Mapping Authority

Every Mapping SHALL identify the authority responsible for publishing it.

Mappings MAY be authored by:

- the authoritative Universe;
- a federation authority;
- a standards organization;
- an agreed neutral steward.

Authority SHALL remain explicit.

---

# 8. Version Compatibility

Mappings SHALL identify the versions of both participating semantic models.

Mappings SHALL be reviewed whenever either side evolves.

Historical mappings SHALL remain reconstructable.

---

# 9. Imported Standards

Mappings SHOULD be used when integrating external standards such as:

- Schema.org
- OData CSDL
- HL7 FHIR
- O*NET
- ESCO
- BPMN
- ArchiMate

Imported concepts SHALL retain their original identities.

---

# 10. Transformation

Some mappings MAY require semantic transformation.

Transformation rules SHALL be:

- deterministic whenever practical;
- documented;
- traceable;
- version-aware.

Transformation SHALL NOT silently alter semantic meaning.

---

# 11. Federation

Semantic Mapping is the preferred interoperability mechanism between heterogeneous Universes.

Federation participants SHOULD exchange canonical mappings before exchanging semantic knowledge.

Mappings SHALL support Projection exchange without requiring schema duplication.

---

# 12. Validation

A conforming implementation SHOULD validate:

- source and target identities;
- mapping type;
- authority;
- version compatibility;
- semantic consistency;
- traceability.

Mappings failing validation SHOULD NOT be used automatically.

---

# 13. Traceability

Every Mapping SHALL preserve:

- provenance;
- publishing authority;
- publication Event;
- version history;
- related Contracts (when applicable).

Traceability SHALL survive federation.

---

# 14. Architectural Invariants

Every Semantic Mapping SHALL preserve:

- canonical identities;
- semantic sovereignty;
- ownership;
- provenance;
- constitutional compliance.

Mappings SHALL connect meanings.

They SHALL NOT replace meanings.

---

# 15. Typical Examples

Examples include:

- employee:Employee ↔ schema:Person (Extension)
- employee:Skill ↔ O*NET Skill (Equivalent)
- healthcare:Patient ↔ fhir:Patient (Equivalent)
- organization:Department ↔ ArchiMate Business Actor (Partial Mapping)

These examples are informative rather than normative.

A worked interop appendix is in [examples/interop/](../examples/interop/) — it imports Schema.org as a Semantic Package, maps a local `employee.person` to Schema.org, FHIR and FOAF, and projects the Object to RDF/OWL.

---

# 16. Future Directions

The **Semantic Mapping Registry** introduced in this document anticipates a full companion specification. That specification would define how registries are published, discovered and federated; how registry entries declare their canonical meaning, authority, version and confidence; how mappings are deprecated and superseded as standards evolve; and how a **Federation of Registries** lets participants cross-verify mappings without any single registry becoming a global semantic authority. The intent is a growing public commons of reusable mappings — O*NET, ESCO, HR-XML, Schema.org and beyond — so that interoperability is increasingly a matter of *reference* rather than *negotiation*.

---

# Final Statement

Semantic Mapping is the interoperability bridge of the Meta-Universe.

Rather than forcing all participants to adopt a single vocabulary, Meta-Universe enables sovereign Universes to preserve their own semantic models while establishing explicit, traceable and version-aware correspondences between concepts. This allows knowledge to flow across heterogeneous ecosystems without sacrificing identity, meaning or constitutional autonomy.
