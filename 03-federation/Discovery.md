# Discovery

**Meta-Universe Specification**

**Document ID:** MU-V2-FED-013  
**Title:** Universe Discovery Document  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** [MUFP](../03-federation/MUFP.md), [MUFP-Messages](../03-federation/MUFP-Messages.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md), RFC 8615 (Well-Known URIs), RFC 2119  
**Informative References:** [Registered-Meta-Models](../06-ecosystem/Registered-Meta-Models.md), [Decentralized-Registry](../06-ecosystem/Decentralized-Registry.md), [Compatibility-Matrix](../06-ecosystem/Compatibility-Matrix.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the **Universe Discovery Document** — the machine-readable
file a Universe publishes so that other universes and AI agents can discover, in
one fetch, *who it is, what it supports, and how to federate with it*.

It makes Discovery — the first stage of the [canonical federation sequence](../03-federation/MUFP.md) —
concrete and executable, rather than a description.

---

# 2. Location

A Universe SHALL publish its Discovery Document as JSON at the well-known URI
(RFC 8615):

```text
https://{authority}/.well-known/meta-universe.json
```

The document SHALL be served as `application/json` and SHOULD be cacheable. It
SHALL contain only **public** metadata: discoverability of a schema SHALL NOT
imply access to data ([MUC Article 10](../01-constitution/Meta-Universe-Constitution.md)).

---

# 3. Contents

The Discovery Document SHALL validate against
[`schemas/discovery.schema.json`](../schemas/discovery.schema.json) and SHALL
include:

| Field | Meaning |
|-------|---------|
| `metaUniverse.version` | The Meta-Universe version the document follows (`"2.0"`). |
| `universe.id` | The publishing Universe's identifier; `universe.did` MAY carry a Decentralized Identifier. |
| `conformance` | Declared MUC / MMAS / MUFP conformance. |
| `supportedVersions` | Version ranges accepted for MUC / MMAS / MUFP during negotiation. |
| `capabilities` | The MUFP capabilities offered (e.g. `projection-exchange`, `synchronization`). |
| `endpoints.mufp` | The URL of the Universe's MUFP endpoint (the [HTTP/JSON binding](../03-federation/MUFP-Messages.md)). |
| `publicSchemas` | The published namespaces, each with its [Semantic Fingerprint](../02-architecture/MMAS-Interchange.md) and a retrieval `href`. |
| `federationProfiles` | The [Federation Profiles](../03-federation/Federation-Profiles.md) the Universe supports. |
| `registries` | Optional pointers to registries the Universe participates in. |

The `publicSchemas[].fingerprint` lets a peer decide, *before any handshake*,
whether the two universes already agree on a concept's meaning.

---

# 4. Use in Federation

An initiator SHOULD fetch the Discovery Document before sending `Hello`. The
document supplies the `supportedVersions` for [version negotiation](../03-federation/MUFP-Messages.md)
and the `endpoints.mufp` to which the handshake is sent. An agent MAY compare
`publicSchemas` fingerprints against its own to skip schema discovery when the
fingerprints already match.

A Universe SHALL NOT rely on the Discovery Document for authentication or trust;
those are established by the [Trust Model](../03-federation/Trust-Model.md) and
[Security Model](../03-federation/Security-Model.md). Discovery answers *what is
possible*, not *what is permitted*.

---

# 5. Conformance

A Discovery Document conforms when it validates against the schema, exposes only
public metadata, and accurately reflects the Universe's supported versions,
capabilities and public-schema fingerprints.

---

# 6. Architectural Invariants

- The Discovery Document SHALL expose schema existence without exposing data.
- Published fingerprints SHALL match the corresponding published schemas.
- Discovery SHALL NOT be a substitute for trust or authorization.

---

# Future Directions

- A signed Discovery Document and DID-based resolution (with the
  [Decentralized Registry](../06-ecosystem/Decentralized-Registry.md)).
- A discovery aggregation format so a registry can index many universes' documents.

---

# Final Statement

> One fetch, and a stranger universe tells you who it is, what it speaks, and
> where to knock — without revealing a single fact it has not agreed to share.
