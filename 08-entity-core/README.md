# Entity Core (ecore): a standard-evolution exploration

> **Status: Working Draft exploration on a BRANCH of the Meta-Universe repository.**
> Nothing in `main` is changed by this branch. These documents are explorations,
> written to be reviewed, and become normative only if and when they are accepted
> through the standard [Change Process](../01-constitution/Change-Process.md).

## What this branch explores

A refocus of the standard's core value. The Meta-Universe family already defines
how meta-models are built (MMAS), federated (MUFP) and governed (MUC). This branch
sharpens what all of that machinery is ultimately *for*:

**defining the properties and methods of entities**, providing the **formats** for
structuring and packaging that knowledge (database, `.md`, `.html`, `.json`, ...),
and the **interfaces** for reaching it (`.git`, MCP, SQL), so that any conformant
reader can parse the format, find every Finding, know how to communicate with the
interface, and know how security works there.

The universal shape is a knowledge graph: **Entity -> Bundle -> Layer -> Finding**,
where a Finding is the unit of information answering exactly one specific question
about the entity. All existing federation logic of meta-universes is preserved,
refined and elaborated, never replaced.

## The four documents

| ID | Document | Status |
|----|----------|--------|
| ECORE-001 | [Entity-Core-Direction.md](Entity-Core-Direction.md): the refocused value proposition, principles, and mapping to existing v2 machinery | Working Draft (this branch) |
| ECORE-002 | [Entity-Graph-Model.md](Entity-Graph-Model.md): the normative-draft model of Entity, Property, Method, Bundle, Layer, Finding, Record, edges and invariants | Working Draft (this branch) |
| ECORE-003 | [Packaging-Profiles.md](Packaging-Profiles.md): how the same graph is packaged as files (.md, .html, .json), as database rows, and as interchange documents | Working Draft (this branch) |
| ECORE-004 | [Interface-Bindings.md](Interface-Bindings.md): interface descriptors for .git, MCP and SQL; access groups, the authorization center, policy | Working Draft (this branch) |

All four documents are candidates for the v3 generation of the standard
(candidate IDs MU-V3-ECORE-001 through MU-V3-ECORE-004).

## Compatibility stance

- **Additive profile candidate for v3.** Entity Core is designed as a profile that
  layers on top of MMAS v2 concepts. It introduces no breaking change to MUC,
  MMAS-Core, MUIF or MUFP; it binds to them by reference (ARCH-016, ARCH-017,
  ARCH-018, ARCH-014, ARCH-002, ARCH-003, ARCH-009, CORE-009, CORE-012, V0-V5,
  FED-011..FED-014).
- **Main is unchanged.** Until review, the v2 documents in `main` remain the sole
  citable text of the standard.
- **Adopted decisions are honored, not reopened.** The exploration encodes the
  adopted decisions R1-R6 recorded in the ELMM profile's decision log: version
  identity (major versions are distinct identities; declared compatibility ranges
  act only as publish-time validation predicates), registry-normative enumerations
  (registry id plus CSN is the only normative identity, acronyms are display
  aliases), provenance handling for restricted-access source specifications,
  standalone-repository shipping with change requests filed upstream,
  walking-skeleton-first, and the reconciled `role` (node) and
  `compositional_role` (edge) fields.

## Reading order

Read ECORE-001 first for direction and rationale, then ECORE-002 for the model,
then ECORE-003 for the format and packaging profiles, and ECORE-004 for the
interface and security bindings. All four assume familiarity with MMAS-Core,
ARCH-016 (composition), ARCH-017 (traversal and layout) and ARCH-018 (data
mastership).
