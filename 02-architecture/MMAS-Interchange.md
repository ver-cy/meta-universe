# MMAS-Interchange — Meta-Universe Interchange Format (MUIF)

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-009  
**Title:** Meta-Universe Interchange Format (MUIF) and Semantic Fingerprint  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** [MMAS-Core](../02-architecture/MMAS-Core.md), [Versioning](../02-architecture/Versioning.md), [Naming-Conventions](../02-architecture/Naming-Conventions.md), RFC 8785 (JSON Canonicalization Scheme), RFC 2119  
**Informative References:** [Validation](../02-architecture/Validation.md), [MMAS-Package](../02-architecture/MMAS-Package.md), [Extension-Model](../02-architecture/Extension-Model.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the **Meta-Universe Interchange Format (MUIF)** — the
canonical, machine-readable serialization of a meta-model — and the exact
**canonicalization algorithm** used to compute a reproducible **Semantic
Fingerprint**.

MUIF is the concrete face of the abstract model defined by [MMAS-Core](../02-architecture/MMAS-Core.md).
It is the foundational artifact on which validation, packaging, migration,
federation pre-checks and tooling depend: without a single canonical form, the
Semantic Fingerprint referenced throughout the specification would not be
reproducible across implementations, and "AI-native" / "machine-readable" would
remain claims rather than facts.

---

# 2. Scope

This document specifies:

- the MUIF document model and its serialization (JSON, with YAML permitted);
- the JSON Schema definitions for each primitive and for the manifest;
- the separation of **semantic** from **non-semantic** content;
- the canonicalization algorithm and the Semantic Fingerprint.

It does not define transport (see [MUFP](../03-federation/MUFP.md)) or packaging
and signing (see [MMAS-Package](../02-architecture/MMAS-Package.md)).

---

# 3. The MUIF Document Model

A MUIF document encodes the MMAS **Composition Hierarchy**:

```text
Meta-Model (manifest)
  ├── Bundles ── Layers
  ├── Objects ── Properties
  ├── Relationships
  ├── Events
  ├── Contracts
  └── Projections
```

The entry point is a **manifest**. Each primitive carries a `muifType`
discriminator (`Object`, `Relationship`, `Event`, `Contract`, `Projection`).

The normative JSON Schemas (Draft 2020-12) live in [`/schemas`](../schemas/):

| Schema | Primitive |
|--------|-----------|
| `manifest.schema.json` | Meta-Model package entry point |
| `object.schema.json` | Object |
| `relationship.schema.json` | Relationship |
| `event.schema.json` | Event |
| `contract.schema.json` | Contract |
| `projection.schema.json` | Projection |
| `common.schema.json` | Shared definitions (CSN, identifier, provenance, …) |

A MUIF document SHALL validate against `manifest.schema.json` (which references
the others).

---

# 4. Serialization

- The canonical serialization is **JSON** (RFC 8259), UTF-8.
- **YAML** 1.2 MAY be used for authoring; it SHALL be losslessly convertible to
  the JSON model. The Semantic Fingerprint is defined over the JSON model, so
  the choice of JSON or YAML SHALL NOT affect the fingerprint.
- Identifiers and Canonical Semantic Names follow [Naming-Conventions](../02-architecture/Naming-Conventions.md).

---

# 5. Semantic vs Non-Semantic Content

The Semantic Fingerprint is computed over the **semantic core** only. The
following are **non-semantic** and SHALL be excluded from canonicalization:

- object keys: `displayName`, `description`, `documentation`, `comment`,
  `label`, `labels`, `ui`, `assertedAt`, `assertionTime`, `generatedAt`,
  `lastModified`, `fingerprint`, `examples`, `$schema`, `$comment`;
- any key beginning with `_` or with `x-ui`.

Rationale: changing a human label, a description, a recording timestamp, or the
self-declared fingerprint MUST NOT change the meaning of a model and therefore
MUST NOT change its fingerprint. Each schema marks such fields **NON-SEMANTIC**
in its description.

---

# 6. Canonicalization Algorithm

Given a MUIF document, the canonical form is produced as follows.

1. **Parse** the document into an abstract value (object / array / string /
   number / boolean / null).
2. **Project to the semantic core.** Recursively remove every non-semantic key
   (Section 5). Remove keys whose value is `null`, an empty object, or an empty
   array — *absent* and *empty* are treated as equivalent.
3. **Normalize values.**
   - Strings SHALL be normalized to Unicode **NFC**.
   - **Object keys** SHALL be sorted by ascending Unicode code point (ordinal).
   - **Arrays SHALL be treated as sets**: each element is canonicalized, then
     the elements are sorted by the ordinal comparison of their canonical
     string. (Order-significant sequences are not used by the core model in
     v1.0; a future revision MAY introduce an explicit ordered-array tag — see
     Future Directions.)
   - Integers SHALL be emitted in shortest decimal form without leading zeros or
     a leading `+`. Other numbers follow the number formatting of RFC 8785
     (JSON Canonicalization Scheme).
4. **Serialize** the normalized tree to canonical JSON: UTF-8, sorted keys, no
   insignificant whitespace, JSON string escaping per RFC 8785.
5. **Hash.** Compute `SHA-256` over the UTF-8 bytes of the canonical JSON.

The **Semantic Fingerprint** is:

```text
sha256:<lowercase-hex-of-the-sha256-digest>
```

Two MUIF documents with the same semantic core SHALL yield the same fingerprint,
regardless of serialization format, key order, set-array order, whitespace, or
non-semantic fields.

---

# 7. Worked Example

The reference example [`/examples/minimal-person`](../examples/minimal-person/)
contains the same model in two very different serializations
(`person.muif.json` and a deliberately reordered `person.variant.json` with
extra non-semantic fields). Both produce the identical fingerprint:

```text
sha256:a628b2afb96dc673f7e2f9161569e573fc70892d10a6997fad7aaa14b04a639d
```

This is verified by the reference tool [`mu-fingerprint`](../tools/):

```text
mu-fingerprint examples/minimal-person/person.muif.json
mu-fingerprint examples/minimal-person/person.variant.json
# → identical sha256:a628b2af...b04a639d
```

---

# 8. Conformance

A document is **MUIF-conformant** when:

- it validates against `manifest.schema.json` and the referenced schemas;
- every primitive declares its `muifType`, `id` and required fields;
- its Semantic Fingerprint, when self-declared in `metaModel.fingerprint`,
  equals the value computed by the canonicalization algorithm of Section 6.

A meta-model SHALL be exchangeable as MUIF to claim MMAS conformance at level
**A4 Validated** or above (see [MMAS-Conformance](../02-architecture/MMAS-Conformance.md)).

---

# 9. Architectural Invariants

- The Semantic Fingerprint SHALL be computed over the semantic core only.
- The fingerprint SHALL be independent of serialization, key order, set order,
  whitespace and non-semantic fields.
- A change in meaning SHALL change the fingerprint; a change in formatting or
  labels SHALL NOT.
- `metaModel.fingerprint` SHALL be excluded from its own computation.

---

# Future Directions

- **Full RFC 8785 compliance** for all number forms, and a conformance test
  vector set for canonicalization (feeds the WS Semantic Test Kit).
- **Ordered-array tagging** for the rare cases where array order is semantically
  significant.
- **Signed MUIF / SDP**: detached signatures over the canonical bytes, enabling
  the Semantic Distribution Package (see [MMAS-Package](../02-architecture/MMAS-Package.md)).
- A formal **MMAS metamodel** (grammar) from which the schemas are generated.

---

# Final Statement

> A model means the same thing no matter how it is written down. MUIF makes that
> precise: one canonical form, one fingerprint — so that two systems can agree
> they are talking about exactly the same meaning before they exchange a single
> fact.
