# Semantic Migration

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-010  
**Title:** Semantic Migration Standard (SMS)  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** [MMAS-Core](../02-architecture/MMAS-Core.md), [Versioning](../02-architecture/Versioning.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md), [Event](../04-core-concepts/Event.md), [Traceability](../02-architecture/Traceability.md), RFC 2119  
**Informative References:** [Migration from v1](../07-guides/Migration-from-v1.md), [Naming-Conventions](../02-architecture/Naming-Conventions.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the **Semantic Migration Standard (SMS)** — the normative
rules under which a Meta-Model moves from one version, structure or vocabulary
to another *without losing or silently changing meaning*.

The [Migration from v1](../07-guides/Migration-from-v1.md) guide introduces
migration as an evolutionary, three-level activity and names SMS as its future
formalization. This document realizes the concept: it specifies migration
levels, records every migration as a traceable [Event](../04-core-concepts/Event.md),
defines a **Migration Manifest**, and fixes the invariant that *meaning SHALL
NOT change without an explicit migration event*.

---

# 2. Scope

This specification applies to:

- migration of Meta-Models, Bundles, Layers, Objects, Properties, Relationships,
  Events, Contracts and Projections across versions;
- the renaming, splitting, merging and reclassification of concepts;
- the structural reorganization of repositories and documents;
- the federation re-binding of a migrated model.

It does not define the storage technology used to persist migration records, nor
the human review process (see [Migration from v1](../07-guides/Migration-from-v1.md)).
The Semantic Fingerprint and canonicalization it relies upon are defined in
[MMAS-Interchange](../02-architecture/MMAS-Interchange.md).

---

# 3. The Three Migration Levels

A migration SHALL be reasoned about at three distinct levels, which MAY progress
independently and at different speeds:

- **Structural Migration** — the *repository and document structure*: folder
  layout, file organization, document identifiers and headers. Structural change
  MAY be quiet: it does not, by itself, change meaning.
- **Semantic Migration** — the *terminology, concepts, relationships and rules*:
  how a concept is renamed, split, merged, reclassified or re-defined. Semantic
  change SHALL NOT be quiet (see Section 5).
- **Federation Migration** — *how the migrated model interacts with other
  Universes*: re-binding Trust, Identity, Semantic Mappings, Contracts and
  Projection Synchronization so the model can rejoin the wider ecosystem.

A complete migration SHALL address all three levels. Structural migration moves
the files; Semantic Migration preserves the meaning inside them; Federation
Migration restores how the model relates to others.

---

# 4. Migration as a Traceable, Reversible-Explainable Operation

A Migration SHALL be recorded as one or more immutable
[Event](../04-core-concepts/Event.md)s of category *Semantic Event* (and, where
applicable, *Lifecycle Event*). Each migration Event SHALL declare:

- its subject — the artifact being migrated;
- the **from-version** and **to-version**;
- a reference to the governing **Migration Manifest** (Section 6);
- its [provenance](../02-architecture/Traceability.md) — who performed the
  migration and under what authority.

A Migration SHALL be:

- **traceable** — every change SHALL be followable from its source to its result
  through the migration Event and its Manifest;
- **reversibly explainable** — the prior state, the rationale and the mapping
  SHALL be recorded so the change can be understood and, where the mapping is
  invertible, reversed. SMS does not require that every migration be *executable*
  in reverse; it requires that every migration be *explainable* in reverse.

Corrections to a migration SHALL themselves be expressed as new migration Events
that reference the Event being corrected. A migration Event SHALL NOT be edited
or deleted once recorded.

---

# 5. The No-Silent-Meaning-Change Rule

Meaning SHALL NOT change without an explicit migration event.

Specifically:

- A change that alters the [Semantic Fingerprint](../02-architecture/MMAS-Interchange.md)
  of any concept SHALL be accompanied by a migration Event and a Migration
  Manifest entry that classifies it.
- Renaming a concept SHALL produce a new [Canonical Semantic Name (CSN)](../02-architecture/Naming-Conventions.md);
  the old CSN SHALL NOT be silently rewritten, and the mapping old → new SHALL be
  recorded in the Manifest.
- A change that affects only non-semantic content (Display Names, descriptions,
  documentation, file location) SHALL NOT change the fingerprint and MAY be
  performed as Structural Migration without a semantic migration Event.

The asymmetry is deliberate: **structural change is allowed to be quiet, but
semantic change is not.**

---

# 6. The Migration Manifest

Every Semantic Migration SHALL be governed by a machine-readable **Migration
Manifest** that describes, declaratively, how meaning is carried from one version
to the next. A Manifest SHALL contain:

| Field | Meaning |
|-------|---------|
| `fromVersion` | The source version of the Meta-Model. |
| `toVersion` | The target version of the Meta-Model. |
| `fromFingerprint` | The [Semantic Fingerprint](../02-architecture/MMAS-Interchange.md) of the source model. |
| `toFingerprint` | The Semantic Fingerprint of the target model. |
| `conceptMappings` | The ordered set of changed concepts, each mapping a source CSN to its target CSN(s) and a change kind. |
| `compatibility` | The overall compatibility classification (Section 7). |
| `events` | References to the migration Event(s) that enact this Manifest. |
| `provenance` | Author, authority and creation time of the Manifest. |

Each entry in `conceptMappings` SHALL declare a **change kind**: `renamed`,
`split`, `merged`, `reclassified`, `redefined`, `added`, `deprecated` or
`removed`, together with the source and target CSNs it relates. A concept that
is unchanged need not appear; absence from `conceptMappings` SHALL mean *meaning
preserved unchanged*.

A Migration Manifest SHALL itself be expressible as [MUIF](../02-architecture/MMAS-Interchange.md)
so that it can be exchanged, fingerprinted and validated like any other
artifact.

---

# 7. Compatibility Classification

Every Migration SHALL declare a compatibility classification, aligned with the
Semantic Change Classification of [Versioning](../02-architecture/Versioning.md):

- **Compatible** — no concept changes meaning; consumers of the source model can
  consume the target model without adaptation. The model fingerprint MAY change
  only through additive, non-breaking concepts.
- **Conditionally Compatible** — meaning is preserved but representation changes
  (for example a rename with a recorded CSN mapping); consumers MAY continue
  using the source through the Manifest's mappings.
- **Breaking** — at least one concept changes meaning, is removed, or is merged
  in a way that loses distinctions; consumers SHALL adapt, guided by the
  Manifest's `conceptMappings`.

The classification SHALL be derivable from the `conceptMappings` and SHALL be
consistent with the change in Semantic Fingerprints.

---

# 8. Preservation of Canonical Identity

Migration SHALL NOT break **Canonical Identity**.

- The stable identity of an Object, Relationship, Event or Contract SHALL survive
  a migration unchanged, even when its CSN or Display Name changes.
- Where a concept is split, each resulting concept SHALL declare its derivation
  from the original identity; where concepts are merged, the resulting concept
  SHALL reference each source identity it absorbs.
- Historical [Event](../04-core-concepts/Event.md)s and prior versions SHALL
  remain available and SHALL NOT be rewritten by migration.

Identity continuity is what allows [Semantic Lineage](../02-architecture/Traceability.md)
to be traced across a version boundary.

---

# 9. Worked Example: v1 Galaxy → v2 Namespace

The canonical v1→v2 evolution renames the v1 organizing concept *Galaxy* to the
v2 [Namespace](../02-architecture/Naming-Conventions.md). The meaning — *how
concepts are organized and published* — is preserved; only the name and its
governance status change. This is a **Conditionally Compatible** Semantic
Migration.

Outline of the Migration Manifest:

```text
fromVersion     : 1.4
toVersion       : 2.0
fromFingerprint : sha256:<source>
toFingerprint   : sha256:<target>
compatibility   : Conditionally Compatible
conceptMappings :
  - source: galaxy.<x>          target: namespace.<x>     kind: renamed
  - source: object.<x>          target: metaObject.<x>    kind: renamed
  - source: identity.<x>        target: canonicalIdentity.<x>  kind: renamed
  - source: projection.<x>      (unchanged — omitted)
events          : [ evt:migration/1.4→2.0/namespace ]
provenance      : { author: <steward>, authority: <MUC>, at: <time> }
```

Enacting migration Event (Semantic Event):

```text
id        : evt:migration/1.4→2.0/namespace
type      : SemanticEvent (migration)
subject   : metaModel:<id>
payload   : { manifest: <manifest-ref>, kind: renamed, from: galaxy, to: namespace }
causality : [ evt:release/2.0 ]
provenance: { actor: <steward>, authority: MUC, source: SMS }
```

Because the rename is recorded as an explicit migration Event with a Manifest
mapping `galaxy.* → namespace.*`, a consumer of the v1 model can resolve any
v1 Galaxy CSN to its v2 Namespace CSN, the change is reversible-explainable, and
Canonical Identity is preserved across the boundary. No meaning changed silently.

---

# 10. Validation

A migration conforms to this specification when:

- every Semantic Migration is recorded as an immutable migration Event;
- a Migration Manifest exists with both fingerprints, a complete
  `conceptMappings` set for every changed concept, and a compatibility
  classification consistent with the fingerprint change;
- no concept changes meaning without a corresponding migration Event;
- Canonical Identity is preserved across the migration;
- historical versions and Events remain available and unrewritten.

See [Validation](../02-architecture/Validation.md) for the validation levels that
apply.

---

# 11. Architectural Invariants

- Meaning SHALL NOT change without an explicit migration Event.
- Every Semantic Migration SHALL be governed by a Migration Manifest.
- Migration Events SHALL be immutable; corrections SHALL be new Events.
- Canonical Identity SHALL survive migration unchanged.
- The compatibility classification SHALL be consistent with the change in
  Semantic Fingerprints.
- Structural Migration MAY be quiet; Semantic Migration SHALL NOT be.

---

# Future Directions

This document fixes the concept of the **Semantic Migration Standard (SMS)**
inline. A dedicated SMS specification could extend it with: a complete vocabulary
of migration-Event types and change kinds; a normative schema for the Migration
Manifest as a first-class [MUIF](../02-architecture/MMAS-Interchange.md)
artifact; machine-verifiable invertibility rules for reversible migrations;
cross-Universe migration choreography so that a federated partner can re-resolve
CSNs automatically when an upstream model migrates; and conformance test vectors
that prove no meaning changed without a recorded event.

---

# Final Statement

> Migration is not the loss of a past meaning but the documented passage of a
> meaning into its next form. SMS makes that passage explicit: every change of
> meaning leaves an event behind it, every event points to a manifest, and every
> manifest lets anyone reconstruct exactly what changed, why, and how to get
> back.
