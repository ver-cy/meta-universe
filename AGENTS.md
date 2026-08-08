# AGENTS.md — Reading Meta-Universe as an AI agent

This file is the entry point for an AI agent (or any automated tool) ingesting
this repository. It tells you what to read first and which artifacts are
machine-readable.

## What this is

Meta-Universe is a **family of open standards** for federated semantic systems:
how independent "universes" of meaning describe reality, build meta-models, and
federate knowledge while preserving identity, context, ownership, trust and
traceability. It is a specification, not a runtime.

## Read in this order

1. **`spec-index.yaml`** — the machine-readable index of every document (id,
   class, status, path). Start here to enumerate the spec.
2. **`00-foundation/Terminology.md`** — the normative vocabulary. Resolve terms
   here, not from prose.
3. **`01-constitution/Meta-Universe-Constitution.md`** — the fundamental laws
   (21 articles). Each normative statement has an ID (`MUC-Rnn`).
4. **`REQUIREMENTS-INDEX.md`** — every RFC 2119 requirement across all normative
   documents, with stable IDs. Cite these IDs.
5. **`02-architecture/MMAS-Interchange.md`** + **`schemas/`** — the MUIF
   serialization and JSON Schemas: the concrete, validatable face of the model.
6. **`03-federation/MUFP-Messages.md`** — the wire protocol (envelopes, state
   machine, errors) for federating.

## Machine-readable artifacts

| Artifact | Use |
|----------|-----|
| `spec-index.yaml` | Enumerate documents and their status. |
| `schemas/*.schema.json` | Validate MUIF models, MUFP envelopes, discovery and validation reports (JSON Schema 2020-12). |
| `schemas/dataset-binding.schema.json` | Validate MMAS 2.1 logical structure, representation, carrier, access and traversal bindings. |
| `schemas/coverage-proof.schema.json` | Validate deterministic traversal inventories and completeness proofs. |
| `REQUIREMENTS-INDEX.md` | Address individual normative requirements by ID. |
| `mu-fingerprint` (see `tools/`) | Compute the reproducible Semantic Fingerprint of a model. |
| `mu-validate` (see `tools/`) | Validate a MUIF model against the V0–V2 checks. |
| `/.well-known/meta-universe.json` | A Universe's discovery document (see `examples/well-known/`). |

## Worked examples

- `examples/minimal-person/` — smallest model + fingerprint reproducibility.
- `examples/federation-acme-govtax/` — two universes federate end-to-end.
- `examples/federation-handshake/` — a MUFP message transcript.
- `examples/interop/` — mapping to RDF/OWL, Schema.org, FHIR, FOAF.
- `examples/data-bindings/` — portable Git/Markdown, SQL and MCP/HTML bindings.

## Working ON a conformant model (not this spec repo)

If you were pointed at a *model repository* (it has `BOOTSTRAP.md`,
`manifest.yaml`, `sources.yaml`), your operating instructions are
**`07-guides/Agent-Operations.md`**: read BOOTSTRAP → manifest → sources before
content; walk bundles in declared order; write **only** to the dataset's
declared master; never hand-edit `raw/`, mirrors or `artifacts/`; re-run the
coverage walker after structural changes; refuse writes when mastership is
undeclared. The connected human-readable map of the whole standard is
**`00-foundation/Overview.md`**.

## Building an agent on Meta-Universe

See **`07-guides/AI-Integration-Patterns.md`** and **`07-guides/AI-Agent-Guide.md`**:
load meta-models as tool schemas, retrieve meaning via Projections + Events
(not raw rows), enforce an Executable Semantic Contract in the loop, and produce
traceable results.

## Rules of engagement

- Treat **Terminology** and the **Constitution** as authoritative; do not infer
  normative meaning from informative prose.
- A model "means the same thing" iff its **Semantic Fingerprint** matches.
- Never treat schema discoverability as data access.
