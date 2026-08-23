# Consent and Disclosure

**Meta-Universe Specification**

**Document ID:** MU-V2-FED-005  
**Title:** Consent and Disclosure — Knowledge Disclosure Principles  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MMAS, MUFP, Federation-Contracts.md  
**Informative References:** Trust-Model.md, Semantic-Mapping.md  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the constitutional principles governing semantic knowledge disclosure within the Meta-Universe.

Its objective is to ensure that semantic knowledge is shared intentionally, proportionally and under explicit authority while preserving sovereignty, ownership and trust.

Disclosure governs access to semantic knowledge, not ownership of that knowledge.

The Meta-Universe replaces the classical model of *"access to data"* with a model of the **negotiation of knowledge**. Under the classical model, a requester authenticates and is then granted access to records in a store. Under the Meta-Universe model, a requester and a holder *negotiate* what knowledge is appropriate, for what purpose, under which contract — and the holder then *generates* a purpose-specific Projection rather than opening a window onto a database. Schema may be public; specific data is the subject of negotiation; the result is a Projection, not database access.

---

# 2. Scope

This specification applies to:

- Projection exchange;
- Semantic Contracts;
- federation requests;
- schema discovery;
- instance data;
- AI agent interactions;
- delegated access.

---

# 3. Disclosure Principles

Knowledge disclosure SHALL be:

- explicit;
- purpose-driven;
- contract-governed;
- traceable;
- least-knowledge;
- revocable where applicable;
- technology independent.

Knowledge SHALL NEVER be disclosed implicitly.

---

# 3a. The Negotiation of Knowledge

Disclosure within the Meta-Universe SHALL proceed as a *negotiation of knowledge*, not as a grant of *access to data*. The canonical sequence is:

1. **Discover semantic schema** — the requester reads the holder's public semantic structure.
2. **Declare purpose** — the requester states explicitly why the knowledge is sought.
3. **Establish trust** — the parties establish the trust required for the declared purpose.
4. **Negotiate Semantic Contract** — the parties agree the rules under which knowledge may be used.
5. **Evaluate disclosure policy** — the holder evaluates its policy against purpose, trust, contract and classification.
6. **Generate appropriate Projection** — the holder *constructs* a Projection shaped to the agreed purpose.
7. **Exchange only required knowledge** — only the Projection, carrying the minimum necessary knowledge, is exchanged.
8. **Record disclosure event** — the disclosure is recorded as a traceable Event.

The contrast with the classical model is structural, not cosmetic:

| Classical "Access to Data" | Meta-Universe "Negotiation of Knowledge" |
| --- | --- |
| Authenticate, then access records | Discover schema, declare purpose, negotiate contract |
| Schema and data exposed together | Schema public; specific data negotiated |
| Result is a database view or query window | Result is a purpose-specific Projection |
| Purpose is implicit or unrecorded | Purpose is declared, evaluated and recorded |

The schema is public; the specific data is the subject of negotiation; the outcome is a Projection generated for one purpose, never an open channel into a store. A holder SHALL NOT satisfy a disclosure request by granting database access in lieu of generating a Projection.

A participating Universe SHOULD expose public semantic structure before exposing instance data.

Schema discovery MAY include:

- namespaces;
- object types;
- relationships;
- projection profiles;
- supported contracts.

Knowledge structure MAY be public even when no instance data is disclosed.

---

# 5. Purpose

Every disclosure request SHALL declare its purpose.

Purpose SHALL participate in authorization.

A disclosure approved for one purpose SHALL NOT automatically authorize another purpose.

---

# 6. Consent

Where applicable, disclosure SHALL require explicit consent from the governing authority.

Consent MAY originate from:

- the owning Universe;
- an authorized steward;
- an applicable Semantic Contract;
- legal or regulatory authority.

Consent SHALL be identifiable and traceable.

---

# 7. Disclosure Levels

Implementations MAY classify disclosure, for example:

- Public
- Partner
- Restricted
- Confidential
- Private

Classification SHALL be explicit.

---

# 8. Projection-Based Disclosure

Knowledge SHOULD be disclosed through Projections.

A Projection MAY:

- omit attributes;
- transform values;
- aggregate information;
- anonymize identities;
- redact sensitive knowledge.

The canonical Meta-Object SHALL remain unchanged.

---

# 9. Least Knowledge Principle

Only the minimum semantic knowledge necessary for the declared purpose SHOULD be disclosed.

Access SHALL be evaluated per request rather than assumed globally.

---

# 10. Authorization

Authorization SHOULD consider:

- purpose;
- context;
- trust level;
- governing Contracts;
- disclosure classification;
- lifecycle state.

Successful authentication alone SHALL NOT imply authorization.

---

# 11. Revocation

Disclosure rights MAY be revoked.

Revocation SHALL:

- be traceable;
- identify authority;
- preserve historical audit records.

Previously disclosed historical knowledge SHALL remain governed by applicable Contracts.

---

# 12. Auditability

Every disclosure SHOULD preserve:

- requester;
- responding Universe;
- purpose;
- disclosed Projection(s);
- governing Contract;
- timestamp;
- decision outcome.

Audit records SHALL remain reconstructable.

---

# 13. Federation

Federated disclosure SHALL preserve:

- sovereignty;
- ownership;
- provenance;
- canonical identities;
- semantic authority.

Receiving Universes SHALL respect contractual disclosure obligations.

---

# 14. Validation

Implementations SHOULD validate:

- declared purpose;
- applicable consent;
- contract scope;
- authorization;
- projection consistency;
- disclosure classification.

Validation SHALL precede disclosure.

---

# 15. Architectural Invariants

Knowledge disclosure SHALL preserve:

- constitutional compliance;
- semantic sovereignty;
- ownership;
- provenance;
- traceability.

Disclosure SHALL NEVER redefine semantic truth.

---

# 16. Future Directions

The negotiation of knowledge anticipates a machine-driven form in which steps 2 through 6 are conducted between agents through an **Executable Semantic Contract**, so that purpose declaration, trust evaluation and Projection generation are performed and recorded automatically. A future companion specification would define the disclosure-policy language by which a holder declares, once, how it will respond to whole classes of negotiated requests — enabling proportional disclosure at machine speed without weakening the requirement that every disclosure remain purpose-bound, contract-governed and traceable.

---

# Final Statement

Knowledge disclosure within the Meta-Universe is governed by explicit purpose, consent and Semantic Contracts rather than unrestricted access.

By separating public semantic structure from protected instance knowledge and exchanging context-aware Projections instead of raw objects, the Meta-Universe enables secure, explainable and interoperable federation while preserving the autonomy and authority of every sovereign Universe.
