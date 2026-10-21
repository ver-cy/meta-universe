# The live register

This directory is the **live, machine-readable register of Meta-Models** described in [Registered-Meta-Models](../Registered-Meta-Models.md). Registration is an act of discovery, not of storage: every entry is a reference to an authoritative source, never a copy of it.

| File | Meaning |
|---|---|
| [`registered-models.csv`](registered-models.csv) | The flat, searchable index: one row per registered model |
| [`entries/`](entries/) | One YAML file per model: the full entry (schema below) |
| [`entry.schema.json`](entry.schema.json) | JSON Schema every entry must validate against |

For the catalogue of ~1180 **external** standards a Meta-Model may import (Schema.org, FHIR, ISO 20022, ...), see [External-Models-Registry](../External-Models-Registry.md) and [`external-models.csv`](../external-models.csv); this register lists **Meta-Models built on the Vercy standard**.

## How to find a model

Search [`registered-models.csv`](registered-models.csv) by kind, domain or keyword (it is small enough to read whole), then open the model's file under [`entries/`](entries/) for conformance, dependencies and the authoritative source.

## How to use a registered model in your Dimension

1. Open the entry; check `license`, `conformance` and `status`.
2. Clone or vendor the `source.repository` at the pinned `source.ref` (vendor into your model's `imports/` per MMAS-Package).
3. Read the model's own `BOOTSTRAP.md` and walk it in its declared order (ARCH-017).
4. Bind it: reference its namespaces from your model, or adapt it and record your changes as deltas in your Dimension; keep the original IDs for federation compatibility.
5. Respect mastership (ARCH-018): the registered source stays the master of the model; your copy is a mirror or a fork, never a second master.

## How to register a model

Anyone may register, including commercial publishers, under the [Open Registration Policy](../Open-Registration-Policy.md) (ECO-013); the interfaces are in the [Registry Federation Interface](../Registry-Federation-Interface.md) (ECO-014).

1. Copy an existing file in `entries/` as a template; fill every required field of [`entry.schema.json`](entry.schema.json) and add a `proof` block (domain, repository or DID).
2. Publish the proof token printed by `vercy register token {your-id}`: `https://{domain}/.well-known/vercy-verification.txt`, a token file in your repository, or a DID signature.
3. Check the entry locally: `vercy register check entries/{your-id}.yaml` (install with `pip install "vercy[yaml]"`). It reports every failure and exits non-zero, so it also runs in CI.
4. Add the matching row to [`registered-models.csv`](registered-models.csv) and open a pull request. An entry that passes the check and the proof is published at the **Registered** trust level without pre-moderation.
5. Registration does not transfer ownership and can be withdrawn by the Owner at any time (status `retired`; entries are never deleted, so identifiers stay resolvable).

To register a whole registry, use `kind: registry` with a `harvest` block pointing to your `/.well-known/meta-universe.json`; your registry stays the master and the register keeps a mirror.

## Entry statuses

`draft` (registered, evolving) · `stable` (versioned releases, change-controlled) · `suspended` (set by the register: source unreachable or proof failed) · `deprecated` (superseded, pointer to successor) · `retired` (withdrawn by Owner; tombstone entry remains).
