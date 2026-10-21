# Open Registration Policy

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-013  
**Title:** Open Registration Policy  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft - for owner approval  
**Normative References:** [Registered-Meta-Models](Registered-Meta-Models.md), [Registry-Federation-Interface](Registry-Federation-Interface.md), [Discovery](../03-federation/Discovery.md), [Data-Mastership](../02-architecture/Data-Mastership.md)  
**Informative References:** [Decentralized-Registry](Decentralized-Registry.md), [Certification](Certification.md), [Validation](../02-architecture/Validation.md)  
**Copyright:** Vercy contributors  
**License:** Apache-2.0

---

# 1. Purpose

The catalogue of a single steward cannot keep up with the number of data
structures in the world. This policy opens the Vercy register so that **anyone
may register a Meta-Model, or a whole registry of Meta-Models**, and so that
every other Universe can discover, read and understand those structures and
learn how to work with them.

Registration is an act of **discovery, not of storage**: Vercy records where a
structure lives, who answers for it, what it claims and how much of that claim
has been checked. It never becomes the master of a registered structure.

---

# 2. Scope

This policy applies to:

- **model registrations**: one Meta-Model with its own source;
- **registry registrations**: a publisher's registry of many Meta-Models, read by
  Vercy through the [Registry Federation Interface](Registry-Federation-Interface.md);
- every card, badge and catalogue listing derived from either.

It does not govern the content of Vercy's own models, which follow their own
publication gates, and it grants no rights to the data a registered structure
describes.

---

# 3. Who May Register

3.1 Any person or organisation MAY register, including commercial publishers.

3.2 A registrant SHALL prove control of the source it registers before an entry
is published (Section 6).

3.3 Registration SHALL be free of charge.

3.4 A registrant's name appears **only as attribution** (publisher, owner,
steward). Descriptions SHALL NOT contain advertising, pricing or calls to buy.
The Vercy standard and Vercy's own models remain vendor-neutral regardless of
who registers.

---

# 4. What May Be Registered

4.1 A registrable structure is a **data model with a declared structure**: a
Meta-Model, schema, ontology, vocabulary or catalogue of such, published in a
machine-readable form at a stable location.

4.2 Every entry SHALL state: identifier, name, publisher, owner, version, kind,
status, license, access and purpose, as defined by the
[entry schema](registry/entry.schema.json).

4.3 Any license is admissible, including proprietary ones, provided it is
stated. A structure with `access: restricted` MAY be registered: its public
metadata is listed, its content is not.

4.4 The following SHALL NOT be registered:

- personal data, secrets or credentials inside a model or its examples;
- malicious payloads or content designed to compromise readers or agents;
- models whose purpose is to cause harm to people (for example operational
  instructions for weapons or for attacking systems);
- content that infringes another party's rights;
- registrations that impersonate another publisher.

---

# 5. Trust Levels

Every listing carries exactly one trust level. Vercy states how much of a claim
it has checked; it does not vouch for the truth of a third-party structure.

| Level | Meaning | Set by |
|---|---|---|
| **Registered** | Ownership proven; the entry passed the automatic check (Section 7). Claims are self-declared. | automatic |
| **Verified** | Declared conformance confirmed by a conformance run ([Validation](../02-architecture/Validation.md) V0-V5) and a reproducible Semantic Fingerprint. | automatic or certifier |
| **Reviewed** | The model's card passed a publication gate: completeness, settled subject, live sources and an independent review of exactly this version. | review process |
| **Canonical** | Reviewed by at least two independent reviewers with no open hold. | review process |

5.1 Publication at the **Registered** level SHALL be automatic once Sections 6
and 7 are satisfied. There is no pre-moderation.

5.2 Every card, API answer and search result SHALL show the trust level, the
registrant and the date of the last successful check.

5.3 A trust level SHALL drop automatically when its evidence no longer holds
(for example a changed fingerprint without a new conformance run).

---

# 6. Proof of Control

A registrant SHALL prove control of the registered source by one of:

- **domain proof**: a token served at `https://{domain}/.well-known/vercy-verification.txt`;
- **repository proof**: a token committed to the registered repository at a
  path named in the submission;
- **identity proof**: a submission signed with the key of the Universe's DID
  ([Decentralized-Registry](Decentralized-Registry.md)).

Proof SHALL be re-checked on every harvest. A failed re-check suspends the entry
(Section 9) until proof is restored.

---

# 7. Automatic Check

Before publication, and on every harvest, an entry SHALL pass:

1. validation against the entry schema;
2. reachability of the declared source, or a declared `access: restricted`;
3. computation of the Semantic Fingerprint of the published version;
4. the content screens of Section 4.4 (secrets, personal data, payloads,
   prohibited purposes, impersonation of registered publisher names);
5. the build of a catalogue card, with its completeness score shown as is.

The check SHALL return a machine-readable report listing every failure, so that
a registrant can correct and resubmit without human help.

---

# 8. Namespaces and Identity

8.1 Identifiers take the form `{publisher}.{model}` in lower case.

8.2 A publisher namespace is reserved on the first successful proof of control
and belongs to that registrant while proof holds.

8.3 Identifiers are never reused. A withdrawn entry remains as a tombstone so
that references keep resolving.

8.4 Disputes over a namespace (trademark, impersonation) follow Section 11; the
contested namespace is frozen while the dispute is open.

---

# 9. Lifecycle

| Status | Meaning |
|---|---|
| `draft` | Registered and evolving. |
| `stable` | Versioned, change-controlled releases. |
| `suspended` | Source unreachable, proof failed or check failing beyond the grace period; hidden from default listings, still resolvable. |
| `deprecated` | Superseded; points to its successor. |
| `retired` | Withdrawn by the owner; tombstone only. |

9.1 Each released version SHALL carry its own fingerprint. A breaking change
SHALL be a new major version.

9.2 An entry whose source stays unreachable for 30 days becomes `suspended`; it
returns to its previous status on the next successful check.

---

# 10. Mastership, Withdrawal and Liability

10.1 The registrant remains the master of its structure
([Data-Mastership](../02-architecture/Data-Mastership.md)). Vercy keeps a
mirror of public metadata and of the card it builds, never a second master.

10.2 The owner MAY withdraw an entry at any time; it becomes `retired`.

10.3 Third-party structures SHALL NOT be merged automatically into Vercy's own
models or standards. Reuse inside Vercy happens only by an explicit, reviewed
reference, so that a poisoned or erroneous registration cannot propagate into
the core.

10.4 Registered content is the responsibility of its registrant. Vercy is
responsible for the accuracy of what it states about an entry: its trust level,
check results and dates.

---

# 11. Reports, Disputes and Appeals

11.1 Anyone MAY report an entry (prohibited content, impersonation, rights
infringement, wrong trust level) through the public report interface.

11.2 A report on prohibited content (Section 4.4) suspends the listing at once
pending review; other reports do not change visibility until decided.

11.3 Reports SHALL be decided within 14 days, with a written reason. The
registrant MAY appeal once; the appeal is decided by a different reviewer.

11.4 Decisions are recorded in a public log without personal data.

---

# 12. Security

- Submissions and harvests are rate-limited per publisher.
- Registered content is fetched and processed in isolation and treated as
  untrusted data, never as instructions to Vercy agents.
- Signed submissions and fingerprints make tampering detectable.

---

# 13. Governance of This Policy

Changes to this policy are proposed as public pull requests and take effect no
sooner than 14 days after publication of the accepted change. Until a steering
group is formed, the Vercy project owner decides.

---

# Final Statement

Vercy does not have to describe every structure itself. It has to make every
structure findable, readable and honestly labelled. Open registration turns the
register into common infrastructure while the standard stays neutral and the
core stays protected.
