# Decentralized Registry

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-007  
**Title:** Decentralized Registry Profile (DID + VC)  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [Registered-Meta-Models](../06-ecosystem/Registered-Meta-Models.md), [Certification](../06-ecosystem/Certification.md), W3C Decentralized Identifiers (DID), W3C Verifiable Credentials (VC)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document describes a **Decentralized Registry profile** — one concrete way to
realize the **Federation of Registries** of
[Registered-Meta-Models](../06-ecosystem/Registered-Meta-Models.md) on open
identity primitives: **Decentralized Identifiers (DID)** and **Verifiable
Credentials (VC)**.

The profile gives each Universe a self-controlled identity, expresses registry
entries, Conformance Statements and Certifications as independently verifiable
credentials, and keeps **Discovery separate from storage** so that semantic
sovereignty stays with each publisher even as the ecosystem scales.

This is a **profile, not a mandate.** The Federation of Registries does not
require DIDs or VCs; this document shows how it maps cleanly onto them for
deployments that want decentralized trust.

---

# 2. Scope

This document covers:

- assigning a DID to each Universe;
- issuing registry entries, Conformance Statements and Certifications as VCs;
- the resolution and verification flow for a consumer;
- how the profile preserves the Reference-Not-Copy and sovereignty invariants of
  the Registry.

It does not replace [Registered-Meta-Models](../06-ecosystem/Registered-Meta-Models.md)
or [Certification](../06-ecosystem/Certification.md); it is a binding of those
documents to DID/VC.

---

# 3. Each Universe Has a DID

In this profile, every Universe controls a **Decentralized Identifier (DID)**.

- The DID is the Universe's self-sovereign identity: it is created and controlled
  by the Universe, not assigned by a central registry.
- The DID resolves to a **DID Document** holding the public keys and service
  endpoints used to verify the Universe's assertions and to locate its
  authoritative Meta-Models.
- Because identity is self-controlled, no registry can revoke a Universe's
  existence; a registry can only choose whether to *list* it.

The DID is what lets a registry entry *point at* an authoritative source whose
identity can be verified independently of the registry doing the pointing.

---

# 4. Registry Entries, Conformance and Certification as Verifiable Credentials

The profile expresses the Registry's records as **Verifiable Credentials (VC)** —
tamper-evident, cryptographically signed statements with an issuer, a subject and
a verifiable proof:

- a **Registry Entry VC** carries the metadata of
  [Registered-Meta-Models §4–5](../06-ecosystem/Registered-Meta-Models.md)
  (identifier, publisher, versions, namespace, repository location), issued by the
  publishing Universe about its own model;
- a **Conformance Statement VC** asserts that a model conforms to declared
  standards and validation levels, with the
  [Validation](../02-architecture/Validation.md) evidence referenced as proof;
- a **Certification VC** is issued by a certifying body following
  [Certification](../06-ecosystem/Certification.md), carrying the certification
  level, supported versions and issue date.

Each credential names its **issuer** (a DID), its **subject** (the model or
participant), and a **proof**. A consumer can therefore tell apart *who claims
what*: a publisher's self-declaration, a validator's conformance statement and a
certifier's certification are distinct, independently verifiable credentials —
mirroring the artifact-versus-participant distinction of
[Certification §4a](../06-ecosystem/Certification.md).

---

# 5. Resolution and Verification Flow

A consumer discovering and trusting a model proceeds, conceptually:

```text
1. Discover    — find a Registry Entry VC (via a Local, Community or Global
                 registry index).
2. Resolve     — resolve the issuer DID to its DID Document and public keys.
3. Verify      — check the credential's proof against those keys; confirm the
                 issuer is the subject's publisher (or an accepted certifier).
4. Locate      — follow the entry to the authoritative repository / endpoint.
5. Cross-check — verify the model's Semantic Fingerprint matches the value the
                 credential attests, and inspect any Conformance / Certification
                 VCs the same way.
6. Decide      — weigh the verified claims (and their issuers' trust) before
                 adopting or federating.
```

Every step is independently checkable: the consumer trusts cryptographic proof
and verifiable issuers, not the good faith of whichever registry surfaced the
entry.

---

# 6. Discovery Stays Separate From Storage

The profile reinforces the Registry's central invariant: a registry entry is a
*reference*, not a copy.

- A registry holds **credentials and indexes** — discovery metadata — never the
  authoritative model.
- The model itself stays at the publisher's endpoint, identified by the
  publisher's DID.
- Verification depends on the issuer's keys, not on the registry's custody, so a
  registry that goes offline does not invalidate a credential a consumer already
  holds.

Registries can still federate as in
[Registered-Meta-Models §15](../06-ecosystem/Registered-Meta-Models.md) — a Global
registry indexing Community registries indexing Local ones — but now each indexed
claim is a verifiable credential rather than an unverifiable copy.

---

# 7. Preserving Sovereignty

Because identity (DID) and authority (VC issuance) remain with each participant:

- semantic sovereignty stays with the publisher — listing a model never transfers
  control of it;
- certification is decentralized — any qualified body can issue a Certification VC
  under the published criteria, and any consumer can re-verify it without the
  certifier's cooperation;
- trust is the consumer's decision — the profile supplies verifiable facts; it does
  not impose a central authority that decides who may participate.

This is the same sovereignty model MUC and MUFP apply to Meta-Models, expressed in
the vocabulary of decentralized identity.

---

# 8. Architectural Position

The Decentralized Registry profile preserves every Registry invariant —
sovereignty, publisher ownership, provenance, traceability and Reference-Not-Copy
— while adding cryptographic verifiability. It is optional: a deployment may run
the Federation of Registries with simpler trust mechanisms and adopt this profile
only where decentralized, independently verifiable trust is required.

---

# 9. Future Directions

A dedicated **Federation of Registries** specification (named in
[Registered-Meta-Models §16](../06-ecosystem/Registered-Meta-Models.md)) could
standardize the credential schemas for Registry Entries, Conformance Statements
and Certifications; define registry-to-registry federation as exchange of
verifiable credentials; specify revocation and freshness for VCs; and bind the
[Semantic Coherence Score](../06-ecosystem/Semantic-Coherence-Score.md) and
[Trust Vector](../02-architecture/Traceability.md) into discovery as verifiable
trust signals. Such a specification would let DID/VC be one interoperable profile
among others rather than a hard dependency.

---

# Final Statement

A Decentralized Registry profile shows that global discoverability and local
sovereignty are not in tension. Give each Universe a self-controlled identity,
make every registry record a verifiable credential, and keep the authoritative
model with its publisher — and the ecosystem can scale its discovery worldwide
while every participant still holds, and can prove, the truth it owns.
