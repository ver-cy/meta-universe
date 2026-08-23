# Security Model

**Meta-Universe Specification**

**Document ID:** MU-V2-FED-012  
**Title:** Federation Security Model and Threat Model  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, [MUFP](../03-federation/MUFP.md), [MUFP-Messages](../03-federation/MUFP-Messages.md), [Trust-Model](../03-federation/Trust-Model.md), [Consent-and-Disclosure](../03-federation/Consent-and-Disclosure.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md), RFC 2119  
**Informative References:** [Identity-Binding](../03-federation/Identity-Binding.md), [Conflict-Resolution](../03-federation/Conflict-Resolution.md), [Traceability](../02-architecture/Traceability.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the **security model** of Meta-Universe federation: the
threat model, the protections every implementation SHALL provide, the
computation of the [Trust Vector](../03-federation/Trust-Model.md), the mechanics
of revocation, and the handling of privacy and personal data.

It exists because **trust is not security** ([MUC Article 15](../01-constitution/Meta-Universe-Constitution.md)).
Establishing trust answers *"do I believe who you are and what you model?"*;
security answers *"can the integrity, authenticity and confidentiality of what
we exchange be guaranteed regardless of trust?"* Both are required.

---

# 2. Scope

This document applies to the federation channel and to every artifact exchanged
across it — Envelopes, Projections, Contracts, Identity Bindings, Semantic
Mappings and Events. It does not mandate a specific cryptographic suite; it
mandates the properties that suite SHALL provide.

---

# 3. Security Principles

- **Trust is not security.** Security SHALL hold even when trust is high.
- **Verify, then use.** Every received artifact SHALL be authenticated and
  integrity-checked before it influences any decision.
- **Least knowledge by construction.** The protocol SHALL make over-disclosure
  hard, not merely discouraged.
- **History is evidence.** Security-relevant events SHALL be recorded as
  immutable [Events](../04-core-concepts/Event.md).

---

# 4. Assets and Trust Boundaries

The assets a federation must protect:

| Asset | Why it matters |
|-------|----------------|
| Identity Bindings | A forged binding lets an attacker impersonate the link between two real entities. |
| Semantic Mappings | A poisoned mapping silently changes meaning across the boundary. |
| Projections | The actual disclosed knowledge; the confidentiality target. |
| Events & Semantic Lineage | The record of truth; poisoning it corrupts every derived conclusion. |
| Contracts | The authorization basis for all disclosure. |
| Trust state | Drives what is permitted; its corruption escalates privilege. |

The trust boundary is the edge of each sovereign Universe. Everything crossing
it is untrusted until verified.

---

# 5. Threat Model

For each principal threat, the REQUIRED mitigation:

| # | Threat | Mitigation (SHALL) |
|---|--------|--------------------|
| T1 | **Spoofed identity / forged Identity Binding** | Authenticate the `from` party of every Envelope; bind every Identity Agreement to verifiable evidence and a signature; reject unverifiable bindings. |
| T2 | **Tampered payload** (model, projection, mapping) | Verify the [Semantic Fingerprint](../02-architecture/MMAS-Interchange.md) of every MUIF payload on receipt; fail with `MUFP-E-FINGERPRINT-MISMATCH`. |
| T3 | **Poisoned Semantic Mapping** | Mappings SHALL declare an authority and be fingerprint-pinned to specific model versions; a mapping that does not match both fingerprints SHALL be rejected. |
| T4 | **Event / lineage poisoning** | Events SHALL be immutable and provenance-signed; derived facts SHALL be recomputable from signed source Events. |
| T5 | **Projection leakage / over-disclosure** | No Projection SHALL be returned without an accepted Contract and a declared purpose; fields outside the contract SHALL be omitted at generation time, not filtered after. |
| T6 | **Replay** of a captured Envelope | Envelopes SHALL carry a unique `messageId` and `sentAt`; receivers SHALL reject duplicates and stale timestamps outside an agreed window. |
| T7 | **Man-in-the-middle** on the channel | The transport binding SHALL provide authenticated encryption (e.g. TLS); Envelopes SHOULD additionally be signed end-to-end. |
| T8 | **Privilege escalation via stale trust/contract** | Revocation SHALL take effect immediately and propagate (Section 8); references to revoked elements SHALL fail with `MUFP-E-REVOKED`. |
| T9 | **Repudiation** | Security-relevant actions (binding, disclosure, revocation) SHALL be recorded as signed Events, preserving non-repudiation. |
| T10 | **Denial of service** | Endpoints SHOULD rate-limit (`MUFP-E-RATE-LIMITED`) and bound the cost of validation and fingerprinting. |

---

# 6. Envelope Authentication and Integrity

- Every [MUFP Envelope](../03-federation/MUFP-Messages.md) SHOULD carry a
  detached `signature` over the **canonical form** of the envelope (per
  [MMAS-Interchange](../02-architecture/MMAS-Interchange.md)) with the
  `signature` field removed. Canonicalization makes the signed bytes
  reproducible across implementations.
- A receiver SHALL verify the signature against a key bound to the `from`
  identity before acting on the message. An unsigned envelope SHALL be treated
  as **unverified** and SHALL NOT be used to disclose protected knowledge.
- Every MUIF payload inside a body SHALL independently pass fingerprint
  verification (T2), so that a valid envelope cannot smuggle a tampered model.

---

# 7. Trust Vector Computation

The [Trust Model](../03-federation/Trust-Model.md) defines six dimensions. This
section makes them computable so that a `TrustResponse` is reproducible and
explainable.

Each dimension is scored in `[0.0, 1.0]` from declared, verifiable inputs:

| Dimension | Scored from |
|-----------|-------------|
| `identity` | strength of authentication of the counterpart's identity (e.g. verified DID, certificate chain) |
| `semantic` | validation level of the counterpart's models (V0–V5) and mapping quality |
| `governance` | evidence of governance maturity (audits, certifications) |
| `contract` | history of honored vs. breached contracts |
| `operational` | uptime / responsiveness / conformance of the endpoint |
| `historical` | length and incident record of prior federation |

A federation decision is a **function of the vector and the purpose**, not a
single scalar. A policy SHALL define, per purpose, the minimum required score on
each dimension; a request is accepted only if every required dimension meets its
threshold. The decision SHALL record the vector and the policy applied, so it can
be explained, traced and revisited. Trust SHALL NOT be reduced to one averaged
number that hides a failing dimension.

---

# 8. Revocation and Propagation

Trust, Contracts and Identity Bindings are revocable at any time via a `Revoke`
message ([MUFP-Messages §9](../03-federation/MUFP-Messages.md)).

- Revocation SHALL take effect on receipt and SHALL be recorded as an immutable
  [Event](../04-core-concepts/Event.md); the revoked element is **ended, not
  erased** (history is preserved).
- After revocation, any reference to the revoked element SHALL fail with
  `MUFP-E-REVOKED`, and the federation state machine SHALL downgrade to the state
  prior to the revoked element.
- A party that has shared a revoked Projection downstream SHALL propagate the
  revocation to its own consumers, honoring the `no-onward-disclosure` and
  retention terms of the governing Contract.
- Revocation propagation SHOULD be timely; the maximum propagation delay SHOULD
  be stated in the Federation Contract.

---

# 9. Privacy and Personal Data

Meta-Universe is frequently used to federate information about people, so
privacy is a first-class concern, not an afterthought.

- **Purpose binding.** Personal data SHALL be disclosed only for the explicit
  purpose of an accepted Contract ([MUC Articles 11–13](../01-constitution/Meta-Universe-Constitution.md)).
- **Data-subject alignment.** Where a Projection concerns a person, the model
  SHOULD identify the data-subject role so that data-subject rights (access,
  rectification, erasure-of-onward-copies, restriction) can be exercised through
  Contract amendment and revocation. This aligns with GDPR-style regimes without
  binding the standard to any single jurisdiction.
- **Minimization.** Least-knowledge (T5) is the technical expression of data
  minimization: the Projection carries only the contracted fields.
- **Erasure vs. history.** The immutable Event history records *that* a
  disclosure happened and *that* it was later revoked; it SHALL NOT be used to
  retain the personal payload beyond the Contract's retention term. Erasure
  applies to disclosed personal data; it does not rewrite the audit of the
  disclosure decision.

---

# 10. Security Considerations for Federation Documents

Every document in `03-federation/` SHOULD carry a brief **Security
Considerations** note identifying the threats it bears on and pointing here. The
mechanism documents map to this model as follows:

| Document | Primary threats |
|----------|-----------------|
| [Identity-Binding](../03-federation/Identity-Binding.md) | T1, T9 |
| [Semantic-Mapping](../03-federation/Semantic-Mapping.md) | T3 |
| [Consent-and-Disclosure](../03-federation/Consent-and-Disclosure.md) | T5, privacy |
| [Synchronization](../03-federation/Synchronization.md) | T4, T6 |
| [Trust-Model](../03-federation/Trust-Model.md) | T7, T8 |
| [MUFP-Messages](../03-federation/MUFP-Messages.md) | T2, T6, T7, T10 |

---

# 11. Conformance

A federation implementation conforms to this model when it:

- authenticates the `from` party and verifies envelope integrity before use;
- verifies the Semantic Fingerprint of every MUIF payload;
- rejects mappings not pinned to both models' fingerprints;
- returns no Projection without an accepted Contract and declared purpose;
- rejects replays and stale messages;
- applies revocation immediately, records it as an Event, and propagates it;
- computes and records the Trust Vector and the purpose policy for each decision.

---

# 12. Architectural Invariants

- Security SHALL NOT depend on trust being high.
- Every crossing artifact SHALL be authenticated and integrity-verified.
- Revocation SHALL be immediate, recorded and propagated.
- Personal data SHALL be purpose-bound and minimized.
- The audit of a decision SHALL survive erasure of the data the decision concerned.

---

# Future Directions

- A **cryptographic profile** (signature suites, key formats, DID methods) — to
  be co-developed with the [Decentralized Registry](../06-ecosystem/Decentralized-Registry.md).
- **Confidential computation** patterns so a Projection can be computed over data
  that is never disclosed in clear, and [Zero-Knowledge Policy Attestation](../03-federation/Zero-Knowledge-Attestation.md)
  so a Universe can prove policy conformance without revealing its model.
- A **security conformance test suite** within the Semantic Test Kit (roadmap WS6).

---

# Final Statement

> Trust decides whether two universes *want* to share meaning. Security guarantees
> that what crosses between them is exactly what was agreed — no more, unaltered,
> attributable, and revocable. Meta-Universe requires both.
