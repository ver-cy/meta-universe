# MUIF Schemas

Machine-readable **JSON Schema (Draft 2020-12)** definitions for the
**Meta-Universe Interchange Format (MUIF) v1.0**. These are the concrete,
validatable face of the abstract model defined in
[../02-architecture/MMAS-Interchange.md](../02-architecture/MMAS-Interchange.md).

| Schema | Defines |
|--------|---------|
| `common.schema.json` | Shared `$defs`: CSN, identifier, canonicalIdentity, semver, fingerprint, provenance, lifecycleState, cardinality, conformance |
| `object.schema.json` | A Meta-Object (Semantic Point of Truth) |
| `relationship.schema.json` | A first-class Relationship |
| `event.schema.json` | An immutable Event |
| `contract.schema.json` | A Semantic Contract |
| `projection.schema.json` | A context-specific Projection |
| `manifest.schema.json` | The meta-model package entry point (Composition Hierarchy) |
| `dataset-binding.schema.json` | MMAS 2.1 portable DatasetBinding: logical structure, representation, carrier, access and traversal |
| `coverage-proof.schema.json` | Deterministic traversal inventory and completeness proof |

The two MMAS 2.1 binding schemas are packaging metadata and are deliberately
outside the MUIF semantic fingerprint. See
[Data-Portability-and-Access](../02-architecture/Data-Portability-and-Access.md).

## Validating a model

Use any standard JSON Schema 2020-12 validator. Examples:

```bash
# Node (ajv-cli)
npx ajv-cli validate -s schemas/manifest.schema.json \
  -r "schemas/*.schema.json" \
  -d examples/minimal-person/person.muif.json --spec=draft2020

# Python (check-jsonschema)
check-jsonschema --schemafile schemas/manifest.schema.json \
  examples/minimal-person/person.muif.json
```

## Non-semantic fields

Properties marked **NON-SEMANTIC** in the schema descriptions
(`displayName`, `description`, `assertedAt`, `metaModel.fingerprint`, …) are
excluded from the **Semantic Fingerprint** computation. See the canonicalization
algorithm in [MMAS-Interchange](../02-architecture/MMAS-Interchange.md) and the
reference tool `mu-fingerprint` (see [../tools/](../tools/)).
