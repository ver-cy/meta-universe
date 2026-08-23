# MUFP Messages — Protocol Mechanics and Bindings

**Meta-Universe Specification**

**Document ID:** MU-V2-FED-011  
**Title:** MUFP Messages, State Machine and Bindings  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** [MUFP](../03-federation/MUFP.md), [Federation-Lifecycle](../03-federation/Federation-Lifecycle.md), [Federation-Contracts](../03-federation/Federation-Contracts.md), [Trust-Model](../03-federation/Trust-Model.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md), RFC 2119, RFC 8259  
**Informative References:** [Identity-Binding](../03-federation/Identity-Binding.md), [Consent-and-Disclosure](../03-federation/Consent-and-Disclosure.md), [Synchronization](../03-federation/Synchronization.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

[MUFP](../03-federation/MUFP.md) defines *why* and *in what order* sovereign
universes federate. This document makes MUFP **implementable**: it defines the
concrete **messages**, the **state machine**, the **error taxonomy**, **version
negotiation**, **revocation**, and one concrete **HTTP/JSON binding**.

A developer SHOULD be able to implement a minimal, interoperable MUFP endpoint
from this document and the message schema alone.

---

# 2. Scope

This document specifies the on-the-wire protocol for the canonical federation
sequence. It does not redefine the *semantics* of trust, contracts, identity or
disclosure — those remain in their own documents; here they become messages.

Every message is an instance of the **MUFP Envelope** and validates against
[`schemas/mufp-envelope.schema.json`](../schemas/mufp-envelope.schema.json).

---

# 3. Protocol Overview

The protocol realizes the canonical federation sequence of [MUFP §6](../03-federation/MUFP.md):

```text
Discovery → Capability Negotiation → Trust Establishment → Semantic Contract
  → Schema Discovery → Projection Exchange → Synchronization → Continuous Federation
```

Knowledge (a Projection) is first exchanged only at **Projection Exchange** —
the sixth step. Everything before it negotiates *meaning, trust, rules and
purpose*.

---

# 4. The MUFP Envelope

Every message — request, response or error — is a single JSON **Envelope**:

```json
{
  "mufp": { "version": "1.0" },
  "messageId": "urn:mu:msg:9f1c...",
  "inReplyTo": "urn:mu:msg:7a02...",
  "type": "Hello",
  "from": "urn:mu:universe:acme",
  "to": "urn:mu:universe:gov-tax",
  "federationId": "urn:mu:fed:acme-govtax-001",
  "sentAt": "2026-06-27T10:00:00Z",
  "body": { },
  "signature": { "alg": "ed25519", "value": "base64..." }
}
```

- `messageId` SHALL be unique per sender; receivers SHALL treat re-delivery of
  the same `messageId` idempotently.
- `inReplyTo` SHALL be present on every response and SHALL reference the request.
- `federationId` SHALL be present once Establishment has occurred.
- `signature` is OPTIONAL in this version and is defined by the forthcoming
  Security-Model; when present it is a detached signature over the
  [canonical form](../02-architecture/MMAS-Interchange.md) of the envelope with
  `signature` removed.

---

# 5. State Machine

A federation between two parties progresses through the following states. The
table lists, for each state, the message that advances it and the resulting
state.

| State | Trigger (request / response) | Next state |
|-------|------------------------------|-----------|
| `INIT` | `Hello` → `HelloAck` | `DISCOVERED` |
| `DISCOVERED` | `CapabilityOffer` → `CapabilityAccept` | `NEGOTIATED` |
| `NEGOTIATED` | `TrustRequest` → `TrustResponse` (accepted) | `TRUSTED` |
| `TRUSTED` | `ContractProposal` → `ContractAccept` | `CONTRACTED` |
| `CONTRACTED` | `SchemaRequest` → `SchemaResponse` | `SCHEMA_SHARED` |
| `SCHEMA_SHARED` | `ProjectionRequest` → `ProjectionResponse` | `ACTIVE` |
| `ACTIVE` | `ProjectionRequest`, `SyncEvent`/`SyncAck`, `IdentityBindingProposal`/`Accept` | `ACTIVE` |
| `ACTIVE` | `Suspend` | `SUSPENDED` |
| `SUSPENDED` | `Resume` | `ACTIVE` |
| *(any)* | `Terminate` | `TERMINATED` |
| *(any)* | `Revoke` | downgrades to the state before the revoked element, or `TERMINATED` |
| *(any)* | `Error` | unchanged, unless the error is fatal (see §7) |

A responder SHALL reject any message that is not legal in the current state with
an `Error` of code `MUFP-E-STATE` (see §7). The protocol SHALL NOT skip stages:
for example, a `ProjectionRequest` received before `CONTRACTED` SHALL be refused.

---

# 6. Message Catalog

Each message `type` carries a `body`. Required body fields are listed; full
shapes are in the envelope schema's `$defs`.

| Stage | Message | Body (key fields) |
|-------|---------|-------------------|
| Discovery | `Hello` | `supportedVersions` (MUC/MMAS/MUFP ranges), `purpose` |
| | `HelloAck` | `supportedVersions`, `capabilities` |
| Capability | `CapabilityOffer` | `muc`, `mmas`, `mufp` (selected), `federationProfile?`, `projectionProfiles?` |
| | `CapabilityAccept` | `agreed` (resolved versions/profiles), `callbackUrl?` |
| Trust | `TrustRequest` | `evidence[]` (Trust Evidence), `requestedPurpose` |
| | `TrustResponse` | `decision` (`accept`/`deny`), `trustVector` (per-dimension), `reason?` |
| Contract | `ContractProposal` | `contract` (a [Federation Contract](../03-federation/Federation-Contracts.md) in MUIF) |
| | `ContractAccept` | `contractId`, `contractFingerprint` |
| | `ContractReject` | `contractId`, `reason`, `counter?` |
| Schema | `SchemaRequest` | `namespaces[]` / `csns[]`, `knownFingerprints?` |
| | `SchemaResponse` | `schemas[]` (MUIF), `fingerprints[]` |
| Projection | `ProjectionRequest` | `subject` (identity), `purpose`, `contractId`, `profile?` |
| | `ProjectionResponse` | `projection` (MUIF Projection), `contractId` |
| Sync | `SyncEvent` | `event` (MUIF [Event](../04-core-concepts/Event.md)), `streamId` |
| | `SyncAck` | `streamId`, `upTo` (event id) |
| Identity | `IdentityBindingProposal` | `binding` (canonical ↔ local), `evidence?` |
| | `IdentityBindingAccept` | `bindingId` |
| Lifecycle | `Suspend` / `Resume` / `Terminate` | `reason?`, `effectiveAt?` |
| Revocation | `Revoke` | `target` (`trust`/`contract`/`identityBinding`), `targetId`, `reason` |
| Error | `Error` | `code`, `requirement?`, `message`, `retriable` |

All MUIF payloads (`contract`, `schemas`, `projection`, `event`, `binding`)
SHALL be valid per [MMAS-Interchange](../02-architecture/MMAS-Interchange.md) and
SHALL carry the Semantic Fingerprint required for verification.

---

# 7. Error Taxonomy

Errors are protocol-level `Error` envelopes (the HTTP response is still `200`;
see §10). Each has a stable `code`:

| Code | Meaning | Retriable |
|------|---------|-----------|
| `MUFP-E-VERSION-UNSUPPORTED` | No common MUC/MMAS/MUFP version | no |
| `MUFP-E-CAPABILITY-MISMATCH` | Required profile/capability unavailable | no |
| `MUFP-E-TRUST-DENIED` | Trust not established for the requested purpose | maybe |
| `MUFP-E-CONTRACT-REJECTED` | Proposed contract not acceptable | maybe |
| `MUFP-E-SCHEMA-UNAVAILABLE` | Requested schema/namespace not exposed | no |
| `MUFP-E-DISCLOSURE-DENIED` | Projection refused (purpose/contract/least-knowledge) | no |
| `MUFP-E-FINGERPRINT-MISMATCH` | A payload's fingerprint does not verify | no |
| `MUFP-E-IDENTITY-UNRESOLVED` | Subject identity not bound/known | maybe |
| `MUFP-E-REVOKED` | Trust, contract or binding has been revoked | no |
| `MUFP-E-STATE` | Message illegal in the current state | no |
| `MUFP-E-RATE-LIMITED` | Too many requests | yes |
| `MUFP-E-INTERNAL` | Responder internal failure | yes |

`MUFP-E-DISCLOSURE-DENIED` enforces `MUC-R21`, `MUC-R22`, `MUC-R23`;
`MUFP-E-FINGERPRINT-MISMATCH` enforces `MUIF-R12`. An `Error` MAY cite the
`requirement` it enforces (a Requirements-Index ID).

---

# 8. Version Negotiation

`Hello` carries the initiator's supported version ranges for MUC, MMAS and MUFP.
The responder SHALL select, for each, the highest version it also supports, and
return the resolved set in `HelloAck`/`CapabilityAccept`. If any required axis
has no common version, the responder SHALL return `MUFP-E-VERSION-UNSUPPORTED`
and the federation SHALL NOT proceed.

---

# 9. Identity Agreement and Revocation

An [Identity Binding](../03-federation/Identity-Binding.md) is proposed with
`IdentityBindingProposal` and confirmed with `IdentityBindingAccept`, producing
a versioned, traceable Identity Agreement. Either party MAY later send `Revoke`
with `target: "identityBinding"`. After revocation, references to the bound
identity SHALL fail with `MUFP-E-REVOKED` until a new binding is established.
Trust and contracts are revoked the same way (`target: "trust"` / `"contract"`),
downgrading the state machine accordingly.

Revocation SHALL be recorded as an [Event](../04-core-concepts/Event.md);
history SHALL be preserved (the binding is not erased, it is ended).

---

# 10. HTTP/JSON Binding

This is one concrete, REQUIRED-to-interoperate binding. Other bindings (gRPC,
messaging) MAY be defined later.

- **Endpoint:** `POST {baseUrl}/mufp`
- **Content-Type:** `application/mufp+json`
- **Request body:** exactly one Envelope.
- **Response body:** exactly one Envelope. A *protocol-level* `Error` is returned
  with HTTP `200` (the error is semantic, not transport).
- **HTTP status codes** are reserved for transport/authn failures: `400`
  malformed envelope, `401`/`403` transport authentication, `429` transport rate
  limit, `5xx` server failure. Protocol outcomes always travel in the Envelope.
- **Synchronization:** if `CapabilityAccept` provided a `callbackUrl`, the
  producer SHALL deliver `SyncEvent` envelopes by `POST` to that URL; otherwise
  the consumer MAY poll by sending a `SyncEvent` request of its own with an empty
  `upTo`. Each `SyncEvent` SHALL be acknowledged with `SyncAck`.
- **Idempotency:** receivers SHALL deduplicate by `messageId`.

---

# 11. Worked Transcript (illustrative)

A minimal successful exchange (bodies elided). The full end-to-end federation of
two real meta-models is in [`examples/federation-handshake`](../examples/federation-handshake/).

```text
acme → gov-tax : Hello            (supportedVersions, purpose="tax-filing")
gov-tax → acme : HelloAck         (capabilities)
acme → gov-tax : CapabilityOffer  (muc=2.0, mmas=A4, mufp=1.0)
gov-tax → acme : CapabilityAccept (agreed, callbackUrl)
acme → gov-tax : TrustRequest     (evidence)
gov-tax → acme : TrustResponse    (accept, trustVector)
acme → gov-tax : ContractProposal (FederationContract MUIF)
gov-tax → acme : ContractAccept   (contractId, fingerprint)
acme → gov-tax : SchemaRequest    (namespaces=[person])
gov-tax → acme : SchemaResponse   (schemas, fingerprints)
acme → gov-tax : ProjectionRequest(subject=person:Person, purpose, contractId)
gov-tax → acme : ProjectionResponse(projection)        ← first data, step 6
acme → gov-tax : SyncAck          (streamId, upTo)
```

---

# 12. Conformance — Minimal Endpoint

A **minimal MUFP endpoint** (the basis for MUFP Level 1) SHALL:

- accept and emit valid Envelopes over the HTTP/JSON binding;
- implement the state machine of §5 and reject out-of-state messages with
  `MUFP-E-STATE`;
- perform version negotiation (§8);
- verify the Semantic Fingerprint of every MUIF payload (`MUIF-R12`), failing
  with `MUFP-E-FINGERPRINT-MISMATCH`;
- enforce that no Projection is returned without an accepted Contract and a
  declared purpose (`MUC-R21`, `MUC-R25`), failing with `MUFP-E-DISCLOSURE-DENIED`.

Higher MUFP levels add Synchronization, Identity Binding, Conflict handling and
signed envelopes.

---

# 13. Security Considerations

This version defines the protocol mechanics; the full threat model and the
required protections (envelope signing, replay defense, revocation propagation,
disclosure-leak prevention) are specified by the forthcoming **Security-Model**
(roadmap WS5) and constrained by [Trust-Model](../03-federation/Trust-Model.md).
Until then, implementations SHOULD run the binding over authenticated TLS and
SHOULD treat unsigned envelopes as unverified.

---

# 14. Architectural Invariants

- Knowledge (a Projection) SHALL NOT be exchanged before `CONTRACTED` and a
  declared purpose.
- The protocol SHALL NOT skip stages of the canonical sequence.
- Every MUIF payload SHALL be fingerprint-verified on receipt.
- Revocation SHALL be possible at any time and SHALL be recorded as history.
- Protocol outcomes SHALL travel in the Envelope, not in transport status codes.

---

# Future Directions

- **Signed envelopes** and replay protection (with Security-Model).
- Additional **bindings** (gRPC, message queues, libp2p).
- A **conformance test harness** that drives an endpoint through the state
  machine (feeds the Semantic Test Kit, roadmap WS6).
- **Capability/profile registry** so capabilities are discovered, not hard-coded.

---

# Final Statement

> A protocol is a promise made precise. MUFP Messages turn "semantic diplomacy"
> into envelopes, states and errors — so that two sovereign universes can be
> built by different teams, in different languages, and still understand each
> other on the wire.
