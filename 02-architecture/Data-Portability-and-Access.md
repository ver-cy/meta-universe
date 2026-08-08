# Data Portability and Access

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-019
**Title:** Meta-Model Architecture Standard — Data Structure, Representation, Carrier and Traversal
**Document Class:** Normative
**Version:** 2.1 (Draft)
**Status:** Working Draft
**Normative References:** MMAS-Core, MMAS-Package, MMAS-Interchange, Model-Traversal-and-Layout, Data-Mastership, Validation
**Informative References:** Traceability, Provenance-Graph, Security-Model
**Copyright:** © Orkestron.AI
**License:** Apache-2.0

---

# 1. Purpose

Semantic data must remain intelligible when it moves between a directory, a Git tree, a database, an object store, an HTTP service or an MCP server. This standard makes the dimensions that were previously hidden behind “files in a repository” explicit and independent.

A conforming description answers six different questions:

1. **Dataset and logical structure** — what governed information exists and how it is shaped;
2. **Representation** — how that structure is encoded or rendered;
3. **Carrier and locator** — where durable state is held;
4. **Access** — by which protocol and capabilities it is reached;
5. **Traversal or query** — how its complete scope is enumerated deterministically;
6. **Package and proof** — how a transferable copy is verified.

The machine contract is [dataset-binding.schema.json](../schemas/dataset-binding.schema.json).

# 2. Scope and non-goals

This document governs portable descriptions of datasets and their physical bindings. It does not replace the MMAS semantic hierarchy, transfer mastership, prescribe one database technology, or redefine semantic **Projection**. A Projection selects meaning for a context; a Representation encodes data. HTML is a Representation, not a Projection.

# 3. Normative model

## 3.1 Dataset

A **Dataset** is the mastership unit defined by ARCH-018. It SHALL have a stable logical identifier that is independent of every locator. Moving a dataset SHALL NOT change its dataset or semantic object identities.

## 3.2 Logical structure

A **LogicalStructure** declares the technology-independent shape of the dataset: `record`, `table`, `tree`, `graph`, `document`, `stream`, `binary` or `hybrid`. It SHOULD declare identity keys, ordering semantics, partitions and a schema reference. A SQL schema, directory tree or Git tree is not by itself the logical structure; each is a possible physical realization.

## 3.3 Representation

A **RepresentationDescriptor** declares `mediaType`, optional profile URI, character encoding, compression, container, document model, parser/extractor identifiers and canonicalization policy. A filename extension MAY be a discovery hint but SHALL NOT substitute for a media type and profile.

Multiple compatible representations MAY exist for one logical structure. Their roles SHALL be explicit: `semantic-primary`, `alternate`, `evidence`, `projection-output` or `package-manifest`. Lossy representations SHALL declare what is lost and SHALL NOT be used to recompute a semantic fingerprint.

### Markdown profile

Markdown SHALL use `text/markdown` and SHOULD name a dialect (`commonmark`, `gfm` or an extension URI). A profile MAY declare YAML, TOML or JSON front matter; fenced-block languages; HTML handling; link/base-URI resolution; and selectors based on headings, block markers, fenced blocks or line ranges. Ingestion SHALL declare whether orphan narrative is semantic, evidence or ignored. Embedded HTML and executable content use the same security policy as HTML.

### HTML profile

HTML SHALL use `text/html` and SHALL distinguish a complete document from a fragment. A profile MAY use CSS selectors, XPath, element IDs, Microdata, RDFa or JSON-LD extractors. It SHALL declare base-URI handling, external-resource handling and script/embed policy. For untrusted or externally mastered HTML the default is: do not execute scripts, do not fetch active external content, and reject or strip dangerous elements according to the declared parser profile.

## 3.4 Carrier, locator and snapshot

A **Carrier** is the kind of system holding durable bytes or records. Core kinds are `package-tree`, `filesystem`, `git`, `relational-db`, `document-db`, `graph-db`, `object-store`, `http`, `mcp` and `extension`.

A **Locator** is a typed physical address. It is not a semantic identity and SHALL NOT be used as one. Carrier-specific locator fields are defined by the schema. Extension carriers SHALL provide an absolute `extensionId` URI and an extension payload.

A **SnapshotIdentity** pins the state read by a traversal: for example a Git commit OID, database transaction/snapshot token, object version/ETag, HTTP ETag/Last-Modified pair, MCP revision token, or a filesystem inventory digest. A mutable branch name, URL or database name alone is not a snapshot.

## 3.5 Access binding

An **AccessBinding** connects a carrier locator to a protocol and declared capabilities: `list`, `read`, `query`, `subscribe`, `write` or `propose-change`. It SHALL declare its operation class and MAY reference credentials only through an opaque `credentialRef`. Secrets, tokens and passwords SHALL NOT appear in a conforming artifact.

Storage and access are independent. The same Git repository can be read from a local filesystem, a Git transport, an HTTP API or an MCP resource. Mastership is independent of both: it decides where truth may be authored, not where a copy is reachable.

## 3.6 Traversal and query plan

A **TraversalPlan** is a declarative, deterministic enumeration algorithm evaluated against one snapshot. It SHALL declare an algorithm, roots or query, ordering and a coverage policy.

Tree traversal MAY declare includes, excludes, ignore-file semantics, hidden-file policy, maximum depth, case sensitivity, symlink/alias policy, submodule and Git LFS policy. Query traversal MAY declare a parameterized SQL/document/graph query, stable ordering keys, pagination strategy and page size. MCP traversal SHALL distinguish resources (`resources/list`, `resources/read`, including cursor pagination) from tools; tools SHALL declare arguments and `operationClass`, with read-only behavior by default.

Parser selection MAY be ordered by exact media type/profile, path pattern and fallback. A plan SHALL NOT depend on unspecified directory order, database row order or unstable pagination.

## 3.7 Coverage proof

A traversal produces a **CoverageProof**. Under one plan fingerprint and one snapshot it records every addressable unit as `included`, `excluded`, `skipped` or `failed`, with a reason for every non-included unit. It SHALL contain counts and content/inventory digests sufficient to detect omission. The required completeness mode is:

- `semantic-units` for semantic datasets;
- `bytes` for raw/evidence datasets;
- `declared-scope` when an external service cannot prove global completeness, in which case the limitation SHALL be explicit.

Same normalized plan plus same snapshot SHALL produce the same ordered unit identifiers and inventory digest. Pagination SHALL not change set semantics.

## 3.8 Dataset binding and package

A **DatasetBinding** composes exactly one dataset structure with one or more representations, a carrier, access bindings, and traversal/query plans. It SHALL reference its authoritative ARCH-018 mastership-register entry and SHALL NOT redeclare the master. A meta-model MAY publish a compatibility policy listing supported tuples; when the list is present it is a closed allow-list and unsupported tuples fail V1 validation.

A **Semantic Distribution Package (SDP)** embeds content or resolvable references plus its manifest, bindings, coverage proofs and integrity data. The semantic fingerprint remains the MUIF fingerprint of meaning. Package manifests, locators, plans and bytes receive a separate package/content fingerprint and SHALL NOT perturb semantic identity.

# 4. Normative invariants

1. Every dataset has exactly one System of Record; a binding never creates a second master.
2. Logical identities, locators, media types, carrier kinds, file kinds and mastership are mutually independent.
3. Non-master copies are disposable and reproducible from a master snapshot plus declared transforms.
4. A traversal is deterministic only against a declared snapshot and stable ordering.
5. Coverage is total within the declared scope; silent orphans are non-conforming.
6. Write operations target the master only, except an explicit `propose-change` channel.
7. Credentials are references, never embedded values.
8. Symlink/alias behavior is explicit; the default is `error`, and cycles always fail.
9. Queries use parameters rather than secret or user values interpolated into query text.
10. Archives and package trees reject path escape; HTTP/object retrieval rejects undeclared network targets; untrusted HTML is never executed.
11. Unknown carrier kinds use the extension mechanism rather than silently changing the core vocabulary.
12. Semantic and package fingerprints are computed and verified separately.
13. Mastership is asserted only by the Mastership Register; DatasetBindings reference it.

# 5. Validation

- **V0:** descriptors parse and validate against the published schema; referenced profiles use absolute identifiers.
- **V1:** every dataset has a structure, representation, carrier, access and deterministic plan; tuple compatibility and coverage proof are checked.
- **V2:** selectors and parsers recover the declared logical structure without undeclared loss.
- **V3:** bindings preserve domain invariants and mastership.
- **V4:** package and access policies conform to constitutional and security rules.
- **V5:** live snapshots, freshness, pagination and reproducibility are verified where access is available.

# 6. Package-tree profile

The canonical MMAS repository layout remains the default 2.x profile. ARCH-017 defines its entry point, well-known locations, kind/origin classification and canonical walk. In this profile:

- the logical structure is the MMAS composition hierarchy;
- the carrier is `package-tree` (or `git` when pinned to a commit);
- manifests are representations of structural declarations;
- the canonical walk is a TraversalPlan specialization;
- its walk report is a CoverageProof specialization.

Existing 2.0 repositories remain conforming. They SHOULD add an explicit binding when they need non-filesystem sources, portable harvesting, or verifiable multi-carrier distribution.

# 7. Security defaults

Read-only access is the default. Following symlinks, executing MCP tools, running HTML/Markdown scripts, fetching undeclared remote resources, following Git submodules, and database writes are opt-in capabilities. Implementations SHALL enforce traversal roots after canonical path resolution, defend archive extraction against path traversal, parameterize queries, bound page/response sizes, and treat parser/extractor code as part of the trusted computing base.

# 8. Extension and evolution

New media profiles do not require a standard revision. New carrier kinds SHOULD first use `extension`; frequently interoperated kinds MAY be promoted by a minor MMAS revision. Local parser IDs MAY be meta-model-specific, while media types and public profiles SHOULD use registered or stable URI identifiers.

---

# Final Statement

Meaning, encoding, location, access, enumeration and packaging are different facts. Declaring them separately lets the same semantic model travel across files, Git, databases, services and future carriers without losing identity, authority, completeness or verifiability.
