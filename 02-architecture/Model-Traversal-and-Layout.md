# Model Traversal and Well-Known Locations

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-017  
**Title:** Meta-Model Architecture Standard - Lossless Traversal and Well-Known Locations  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MMAS-Core, MMAS-Package, Versioning, Validation, Data-Mastership  
**Informative References:** Traceability, AI-Agent-Guide, Repository-Structure  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0

---

# 1. Purpose

[MMAS-Package](MMAS-Package.md) defines *where things live* in a Meta-Model repository. This document defines the two guarantees that layout alone cannot give:

1. **Lossless traversal.** A reader (human or AI agent) SHALL be able to walk the entire model bundle by bundle, layer by layer, visiting **every file exactly once**, knowing **what each file means**, and **proving that nothing was missed**.
2. **Well-known locations.** Content that is not a semantic definition (raw source data, canonical source texts, generated artifacts, operating instructions) SHALL live in reserved locations with predefined meaning, so a reader never has to guess what a file is.

Together with [Data-Mastership](Data-Mastership.md), which declares *who owns the truth* for every dataset, this makes a Meta-Model fully mechanically readable: nothing lost, nothing ambiguous, nothing of unknown authority.

---

# 2. Scope

This specification applies to:

- Meta-Model repositories and Semantic Distribution Packages;
- manifests at repository, bundle and layer level;
- all files contained in a model repository, without exception;
- walkers: any tool or agent that enumerates model content.

It does not redefine the semantics of Objects, Relationships, Events, Contracts or Projections; it governs how their carrier files are found, ordered and classified.

---

# 3. Design Principles

- **One entry point.** Every walk starts at the same place; there is no tribal knowledge about where to begin.
- **Declared order.** The reading order is data, not convention: manifests declare it, walkers follow it.
- **Total classification.** Every file is classified. A file whose meaning cannot be determined from the manifests and this specification is a defect, not a curiosity.
- **Meaning travels with structure.** Each enumerated unit carries a stated meaning; a reader should never need to open a file to discover what kind of thing it is.
- **Authored, harvested and generated content never mix.** Their lifecycle rules differ, so their locations differ.

---

# 4. The Entry Point

A conforming repository SHALL be readable starting from exactly two files at its root:

1. **`BOOTSTRAP.md`** - the operating instructions: how to read this model, in what order, with what tools, and what an agent is expected to do and not do here. A walker SHOULD read it first. `BOOTSTRAP.md` MAY delegate to a `bootstrap/` directory for extended instructions (agent prompts, onboarding, checklists). Bootstrap content SHALL NOT define semantics; it explains, it never declares.
2. **`manifest.yaml`** - the machine entry point defined in [MMAS-Package](MMAS-Package.md) §5, extended by this document with the walk declaration (§5) and the exclusion list (§7).

If `BOOTSTRAP.md` is absent, the walker proceeds from the manifest alone; absence of the manifest makes the repository non-conforming.

Repositories that already use an ecosystem-specific entry file (for example `README.md`, `AGENTS.md` or `CLAUDE.md`) SHOULD make it a thin pointer to `BOOTSTRAP.md` and `manifest.yaml` rather than a second source of truth.

---

# 5. The Walk Declaration

Traversal order is declared top-down:

- The **repository manifest** SHALL declare the ordered list of bundles (`bundles:` in reading order).
- Each **bundle manifest** (`bundle.yaml`) SHALL declare the bundle's single semantic responsibility and the ordered list of its layers.
- Each **layer manifest** (`layer.yaml`) SHALL enumerate the layer's content: files or glob patterns, each with a **kind** (§8) and a one-line **meaning**.

Enumeration MAY be **centralized instead of per-layer**: a repository whose file names carry the kind by convention (for example `{kind}-{id}-{memo}.md`) MAY declare classification once, as an ordered list of match rules in the repository manifest (`kind_rules`): each rule maps a glob pattern to a kind and an origin (§9); the first matching rule wins. In such rules the placeholder `{prefix}` denotes the file-name segment before the first delimiter, so a single rule like `kind: "object/{prefix}"` classifies a whole naming convention. Centralized rules are equivalent to per-layer enumeration for the coverage check (§7); a file matched by no rule is an orphan either way.

Ordering rules:

- Bundles SHALL be ordered so that a bundle appears **after** every bundle it depends on (foundation first). Cyclic bundle dependencies are non-conforming.
- Layers within a bundle SHALL be ordered the same way.
- Forward references (a file mentioning a concept defined later in the walk) are permitted, but the *declaration* order SHALL remain dependency-first, so that a single sequential pass reads definitions before heavy use.

A walker that visits bundles, then layers, then enumerated files, each in declared order, performs the **canonical walk**. Two walkers performing the canonical walk over the same repository version SHALL visit the same files in the same order.

---

# 6. Well-Known Locations

Beyond the structural directories of [MMAS-Package](MMAS-Package.md) §4 (`bundles/`, `imports/`, `mappings/`, `schemas/`, `examples/`, `diagrams/`, `docs/`, `tools/`), this document reserves the following locations. Each has a fixed default meaning; a walker MAY rely on it without further declaration.

| Location | Meaning | Lifecycle |
|----------|---------|-----------|
| `BOOTSTRAP.md`, `bootstrap/` | Operating instructions for readers and agents: how to read, update and validate this model | Authored |
| `canon/` | Canonical source texts this model treats as ground truth: doctrine, adopted decisions, normative inputs, source specifications | Authored or adopted; versioned; never generated |
| `raw/` | Unprocessed captures from external systems: exports, dumps, transcripts, crawl results | Harvested; NEVER hand-edited |
| `artifacts/` | Derived, regenerable outputs: compiled views, rendered documents, computed indexes, reports | Generated; NEVER authored |
| `sources.yaml` | The Data Mastership Register: every dataset's System of Record (see [Data-Mastership](Data-Mastership.md)) | Authored |

Rules:

- **`canon/`** holds the texts the model is *about* or *bound by*, when those texts must travel with the model. Layers SHALL reference canon files rather than paraphrase them; if a layer statement and a canon text conflict, the canon text wins within that model.
- **`raw/`** SHALL be organized as `raw/<source-system>/<dataset>/...`. Every dataset directory SHALL carry a provenance sidecar (`_provenance.yaml`: source system, scope, extraction time, extracting tool, record count). Raw content is evidence; correcting it by hand destroys its evidentiary value and is non-conforming. Corrections happen in the source system (then re-harvest) or in the semantic layer (as an annotated deviation).
- **`artifacts/`** entries SHALL declare their generator and inputs (a sidecar or a header line suffices). A conforming repository can delete `artifacts/` entirely and rebuild it; if it cannot, something is misfiled.
- A repository SHOULD NOT invent parallel locations for these purposes (`_raw/`, `generated/`, `sources/` and similar). Where legacy layouts exist, the manifest SHALL map them to the reserved meanings.

---

# 7. The Completeness Rule (No File Left Behind)

Every file in the repository SHALL fall into exactly one of three classes:

1. **Enumerated** - matched by a layer manifest's content declaration (§5), or a structural directory of MMAS-Package §4 with its defined role;
2. **Well-known** - located under a reserved location of §6, inheriting its default meaning;
3. **Excluded** - matched by the manifest's exclusion list (`exclude:`), which names infrastructure files with no semantic content (VCS internals, CI configuration, editor settings, build caches).

The **coverage check**: a walker SHALL be able to compare the full recursive file listing of the repository against the union of the three classes. Files in no class ("orphans") and files in more than one class ("ambiguous") are validation failures. The coverage check is part of **structural validation (V1)** in [Validation](Validation.md).

The exclusion list is a declaration, not a dumping ground: excluding a file asserts it carries **no model meaning**. Excluding semantic content to pass the coverage check is non-conforming.

---

# 8. File Kinds

Every enumerated file SHALL carry one kind. The base vocabulary:

`object` · `relationship` · `event` · `contract` · `projection` · `canon` · `raw` · `artifact` · `mapping` · `import` · `schema` · `example` · `diagram` · `doc` · `tool` · `bootstrap` · `manifest`

Kinds answer "what is this file *in the model*", not "what format is it". A CSV may be `raw` (an export), `artifact` (a computed index) or `object` (a definition table); the kind, not the extension, decides how a reader treats it. Ecosystems MAY refine the vocabulary with sub-kinds (`object/policy`, `doc/adr`) but SHALL preserve the base kind as prefix. Sub-kinds MAY be derived mechanically from declared naming conventions via the `{prefix}` placeholder of §5.

---

# 9. Authored, Harvested, Generated

Orthogonal to kind, every file has exactly one **origin**:

- **Authored** - written by a human or an agent acting as author; edited in place; reviewed like code.
- **Harvested** - captured from an external system by a pipeline; replaced by re-harvesting; never edited in place.
- **Generated** - computed from other files in this repository; replaced by re-generation; never edited in place.

The origin is implied by location for the well-known directories (§6) and SHALL be declared in the layer manifest elsewhere. Editing harvested or generated files in place is non-conforming: the fix belongs in the source system or the generator.

This distinction is what makes mastership (see [Data-Mastership](Data-Mastership.md)) enforceable in practice: a file's origin tells a reader immediately whether *this* copy can ever be the truth.

---

# 10. The Canonical Walk (Informative)

A conforming walker:

1. Reads `BOOTSTRAP.md` (context, constraints, local conventions).
2. Reads `manifest.yaml`: identity, versions, bundle order, exclusion list.
3. Reads `sources.yaml`: which datasets are mastered here and which are mirrors (with freshness).
4. Visits `canon/` as declared or referenced, so ground truth is loaded before interpretation.
5. Walks bundles in declared order; within each, layers in declared order; within each, enumerated files, reading kind and meaning before content.
6. Resolves `imports/` and `mappings/` when a layer references them.
7. Treats `raw/` as evidence (consulted, not recited) and `artifacts/` as disposable views.
8. Runs the coverage check (§7) and reports orphans, ambiguities and stale mirrors.

The walk is complete when every file is accounted for and every dataset's authority is known.

---

# 11. AI-Native Requirements

A conforming repository SHALL allow an AI agent, without out-of-band knowledge, to:

- find the entry point and operating instructions;
- enumerate all content in a deterministic order;
- state, for any file, its kind, origin and one-line meaning;
- prove coverage: name every file it did not read and why (excluded, generated, raw evidence);
- distinguish what it may edit (authored, in the model's mastery) from what it must not (harvested, generated, externally mastered).

An agent that cannot satisfy the last point SHOULD refuse write operations on the model.

---

# 12. Architectural Invariants

Traversal and layout SHALL preserve:

- semantic identity and ownership;
- provenance of harvested and generated content;
- the single-entry-point property;
- determinism of the canonical walk;
- constitutional compliance.

Layout and traversal SHALL NEVER redefine semantic meaning; they only make it reachable.

---

# 13. Future Directions

A reference walker (`mu-walk`) is a natural companion to the existing tools: it would perform the canonical walk, emit a machine-readable walk report (files, kinds, origins, coverage result, mirror freshness) and serve as the executable definition of this document. A walk report could become part of the Semantic Distribution Package, letting consumers verify completeness before trusting a package.

---

# Final Statement

A Meta-Model is only as trustworthy as a reader's ability to know that they have seen all of it and understood what each part is.

This standard turns that ability from diligence into a contract: one entry point, a declared order, a total classification of files, reserved places for instructions, canon, raw evidence and derived artifacts, and a coverage check that makes silent loss impossible.
