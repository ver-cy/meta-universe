# Core Profile

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-013  
**Title:** Meta-Universe Core Profile (MVP Conformance)  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, [MMAS-Interchange](../02-architecture/MMAS-Interchange.md), [Validation](../02-architecture/Validation.md), [MUFP-Messages](../03-federation/MUFP-Messages.md), [Discovery](../03-federation/Discovery.md), RFC 2119  
**Informative References:** [MMAS-Conformance](../02-architecture/MMAS-Conformance.md), [Security-Model](../03-federation/Security-Model.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

The full specification is large. The **Core Profile** defines the **minimal
mandatory subset** an implementation SHALL support to call itself
"Meta-Universe Core conformant." It exists so that a first interoperable
implementation is achievable without reading all documents, and so that
"conformance" has a precise floor.

Everything outside this profile is **optional** at the Core level and adds
capability, not baseline conformance.

---

# 2. Scope

The Core Profile covers two roles. An implementation MAY claim either or both:

- **Core Model** — producing and consuming valid meta-models.
- **Core Federation** — federating with another universe over MUFP.

---

# 3. Core Model requirements

A Core Model implementation SHALL:

1. Read and write **MUIF** documents per [MMAS-Interchange](../02-architecture/MMAS-Interchange.md),
   including the five primitives (Object, Relationship, Event, Contract,
   Projection) and the manifest.
2. Compute the **Semantic Fingerprint** reproducibly (the canonicalization of
   MMAS-Interchange).
3. Validate to at least **V3** ([Validation](../02-architecture/Validation.md)):
   pass all Error-severity checks of V0, V1, V2 and V3.
4. Preserve the constitutional invariants it can express: unique persistent
   identity (`MUC-R03`), provenance (`MUC-R13`), and Object/Projection separation
   (`MUC-R11`).

A Core Model implementation MAY omit: external-standard import, Knowledge Quality
scoring, MUDL, and runtime (V5) validation.

---

# 4. Core Federation requirements

A Core Federation implementation SHALL:

1. Publish a valid **Discovery Document** ([Discovery](../03-federation/Discovery.md)).
2. Implement the **minimal MUFP endpoint** ([MUFP-Messages §12](../03-federation/MUFP-Messages.md)):
   the HTTP/JSON binding, the state machine, version negotiation, and the messages
   `Hello … ProjectionResponse`.
3. **Verify the Semantic Fingerprint** of every received MUIF payload (`MUIF-R12`).
4. Return no Projection without an accepted Contract and a declared purpose
   (`MUC-R21`, `MUC-R25`).
5. Run the binding over authenticated transport and honor revocation
   ([Security-Model](../03-federation/Security-Model.md)).

A Core Federation implementation MAY omit: Synchronization, Identity Binding,
Conflict handling and signed envelopes — these belong to higher MUFP levels.

---

# 5. Conformance statement

A Core Profile claim SHALL state which role(s) are supported and the validation
level reached, for example:

```text
Meta-Universe Core conformant
  Core Model: yes (Validation V3)
  Core Federation: yes (MUFP minimal endpoint)
```

Such a claim is verifiable with the reference tool `mu-validate` and the
[Semantic Test Kit](../tests/).

---

# 6. Architectural Invariants

- The Core Profile SHALL be a strict subset of the full specification; it SHALL
  NOT add requirements that contradict any document.
- A Core claim SHALL be independently verifiable.

---

# Future Directions

Additional named profiles (e.g. *Federation Level 2/3*, *AI-Native*, industry
Federation Profiles) will layer on top of the Core Profile, each adding a defined
set of optional capabilities.

---

# Final Statement

> The Core Profile is the smallest honest "yes": the least an implementation must
> do to interoperate — and a clear ladder for everything it may do next.
