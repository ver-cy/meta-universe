# Registry Federation Interface

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-014  
**Title:** Registry Federation Interface  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft - for owner approval  
**Normative References:** [Open-Registration-Policy](Open-Registration-Policy.md), [Discovery](../03-federation/Discovery.md), [Registered-Meta-Models](Registered-Meta-Models.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md)  
**Informative References:** [Decentralized-Registry](Decentralized-Registry.md), [Data-Mastership](../02-architecture/Data-Mastership.md), RFC 8615  
**Copyright:** Vercy contributors  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the interfaces through which a publisher registers a
Meta-Model or a whole registry with a Vercy register, and through which other
Universes read what is registered. It makes the
[Open Registration Policy](Open-Registration-Policy.md) executable.

---

# 2. Interfaces at a Glance

| # | Interface | Direction | Form |
|---|---|---|---|
| I1 | Model submission | publisher to register | pull request, or `POST /api/v1/registry/submissions` |
| I2 | Registry submission | publisher to register | a domain whose Discovery Document lists the registry |
| I3 | Proof of control | publisher to register | token file, repository token, or DID signature |
| I4 | Check report | register to publisher | `GET /api/v1/registry/submissions/{id}` |
| I5 | Harvest | register from publisher | periodic read of the Discovery Document and catalogue |
| I6 | Read and resolve | any Universe from register | `/api/v1/models/{search,resolve,catalog}`, cards, `AGENTS.md` |
| I7 | Report | anyone to register | `POST /api/v1/registry/reports` |

---

# 3. I1 Model Submission

3.1 **By pull request.** A publisher adds one entry file to
[`registry/entries/`](registry/entries/) and one row to
[`registry/registered-models.csv`](registry/registered-models.csv), as described
in the register [README](registry/README.md).

3.2 **By API.** A publisher sends the same entry as JSON:

```http
POST /api/v1/registry/submissions
Content-Type: application/json

{
  "kind": "model",
  "entry": { ...fields of registry/entry.schema.json... },
  "proof": { "method": "domain", "domain": "example.org" },
  "card_supplement": { ...optional, card-supplement schema... }
}
```

The register answers `202 Accepted` with a submission id and the proof token to
publish (I3). The entry is published at the **Registered** level as soon as the
proof is found and the automatic check passes.

3.3 A publisher MAY attach a **card supplement** (the same schema Vercy uses for
its own cards) to supply sections its model does not carry: what agents may and
must not do, moral aspects, owners, recognition cues. A supplement never edits
the registered source.

---

# 4. I2 Registry Submission

4.1 A publisher that keeps its own registry submits only its domain:

```http
POST /api/v1/registry/submissions
{ "kind": "registry", "domain": "models.example.org", "proof": { "method": "domain" } }
```

4.2 The domain SHALL serve a [Discovery Document](../03-federation/Discovery.md)
at `/.well-known/meta-universe.json`. Its `publicSchemas` list the registry's
models; each item SHALL carry an `id`, a `version`, a Semantic Fingerprint and a
retrieval `href`. Its `registries` member MAY point to a catalogue file in the
entry format when the registry is large:

```json
"registries": [
  { "role": "catalogue", "format": "vercy-entry/1", "href": "https://models.example.org/catalogue.jsonl",
    "harvest": { "cadence": "P1D" } }
]
```

4.3 The publisher's registry stays the master. The register keeps a **mirror**
of the entries it harvests and labels each one with its origin registry.

---

# 5. I3 Proof of Control

| Method | What the publisher does | What the register checks |
|---|---|---|
| `domain` | serves the issued token at `https://{domain}/.well-known/vercy-verification.txt` | the file contains the token |
| `repository` | commits the token at the path named in the submission | the file exists at the registered `source.ref` |
| `did` | signs the submission with the key of `universe.did` | the signature verifies against the DID document |

The token is public and derived from the entry id: `vercy-register-` followed by the first 32 hex
characters of SHA-256 of `vercy-register:{id}` (the reference command `vercy register token {id}`
prints it). It does not need to be secret: what it proves is control of the place it is published in.

Proof is re-checked on every harvest (Policy Section 6).

---

# 6. I4 Check Report

`GET /api/v1/registry/submissions/{id}` returns the status and a report:

```json
{
  "id": "sub-2026-10-21-0001",
  "status": "published | pending-proof | failed | suspended",
  "trust_level": "registered",
  "fingerprint": "sha256:...",
  "card": "https://ver.cy/models/{publisher}.{model}/",
  "completeness": 0.82,
  "failures": [ { "check": "source-reachable", "detail": "HTTP 404 at source.repository" } ],
  "checked_at": "2026-10-21T12:00:00Z"
}
```

The same check runs offline with the reference command `vercy register check
{entry-file}`, so that publishers can validate before submitting and in CI.

---

# 7. I5 Harvest

7.1 The register reads each registered registry at the cadence it declares,
bounded between one hour and thirty days, and re-checks every model registration
at least weekly.

7.2 A harvest compares fingerprints. A changed fingerprint creates a new version
record; trust levels earned for an earlier version do not carry over to it.

7.3 A source that stays unreachable for 30 days moves the entry to `suspended`
(Policy Section 9).

7.4 Harvested content is fetched in isolation and treated as untrusted data.

---

# 8. I6 Read and Resolve

8.1 Every registered model is readable through the existing catalogue
interfaces, extended with two fields:

| Field | Meaning |
|---|---|
| `publisher` | The registrant namespace, for example `example` in `example.orders`. |
| `trust_level` | `registered`, `verified`, `reviewed` or `canonical`. |

8.2 `GET /api/v1/models/search?q=...&trust_level=verified&publisher=...` filters
by level and publisher. `resolve` accepts any registered identifier and returns
the entry, the card URL, the source and the fingerprint.

8.3 Each registered model has a card page and a machine card
(`/models/cards/{id}.json`, vercy.card/1) with the trust level shown, plus an
`AGENTS.md` that tells an agent how to read the structure and where its master
lives.

8.4 The register publishes its own Discovery Document listing every published
entry, so that one register can federate with another without manual exchange.

---

# 9. I7 Report

`POST /api/v1/registry/reports` with the entry id, the reason (one of
`prohibited-content`, `impersonation`, `rights`, `wrong-trust-level`, `other`)
and a description. Handling follows Policy Section 11.

---

# 10. Conformance

A register conforms to this interface when it implements I1 to I7, applies the
[Open Registration Policy](Open-Registration-Policy.md), and passes the
interface fixtures in `tests/registry-federation/`.

---

# Final Statement

A publisher needs one domain or one pull request to make its structures part of
the shared map. A reader needs one search to find them and one label to know how
far to trust them.
