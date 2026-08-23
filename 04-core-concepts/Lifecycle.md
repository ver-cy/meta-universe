# Lifecycle

**Meta-Universe Specification**

**Document ID:** MU-V2-CORE-011  
**Title:** Lifecycle — Three Independent Times  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, MUFP  
**Informative References:** [Object](../04-core-concepts/Object.md), [Event](../04-core-concepts/Event.md), [Projection](../04-core-concepts/Projection.md), [Contract](../04-core-concepts/Contract.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the canonical Lifecycle Model for semantic artifacts within the Meta-Universe.

A Lifecycle describes the meaningful states through which a semantic artifact progresses from its creation to its retirement. Lifecycle management enables consistent governance, traceability, federation and long-term semantic continuity.

---

# 1a. Three Independent Times

A single Meta-Object does not advance along one timeline but along **three independent times**, which SHALL NOT be conflated:

- **Object Lifecycle** — the existence of the entity itself: *Created → Active → Retired*. This answers *does the thing exist and is it in use?*
- **Version Lifecycle** — the evolution of its definition: *v1.0 → v1.1 → v2.0*. This answers *which revision of its meaning is current?*
- **Projection Lifecycle** — the existence of a particular exposed view: for example, *temporarily published to a partner, then revoked.* This answers *is this specific [Projection](../04-core-concepts/Projection.md) currently available, and to whom?*

These three times run in parallel and combine freely. One Meta-Object MAY, at the same instant, be **Active** as an object, carry an **active version 3.2**, expose a **Deprecated** public projection, and expose an **Active** internal AI projection — all simultaneously and without contradiction.

Keeping the three times separate prevents *concept-mixing* — the common error of treating "the object was retired", "the definition changed" and "the partner's access ended" as one event. It also grounds federation and [Semantic Contract](../04-core-concepts/Contract.md) execution: a contract may, for instance, permit a partner Projection only while the Object Lifecycle is Active and the consumed version remains within an agreed range, terminating the Projection Lifecycle without affecting the Object or its versions.

Every transition in each of the three times SHALL be recorded through the [Event](../04-core-concepts/Event.md) primitive on the Semantic Timeline, so that the three histories remain independently reconstructable.

---

# 2. Scope

This specification applies to all lifecycle-aware semantic artifacts, including:

- Meta-Objects
- Relationships
- Events
- Contracts
- Projections
- Meta-Models
- Semantic Packages

Domain Meta-Models MAY define additional lifecycle states and transitions.

---

# 3. Lifecycle Principles

Every Lifecycle SHALL be:

- explicit;
- traceable;
- version-aware;
- technology independent;
- governed by Events;
- compatible with the Meta-Universe Constitution.

Lifecycle SHALL describe semantic state rather than implementation state.

---

# 4. Canonical Lifecycle

The recommended canonical lifecycle is:

Created

↓

Draft (optional)

↓

Proposed (optional)

↓

Active

↓

Suspended (optional)

↓

Deprecated (optional)

↓

Archived

↓

Retired

Domain-specific models MAY omit or extend intermediate states while preserving semantic consistency.

---

# 5. State Definitions

## Created

The artifact has been assigned a canonical Identity.

## Draft

The artifact exists but is not yet authoritative.

## Proposed

The artifact is awaiting approval or publication.

## Active

The artifact is authoritative and available for normal use.

## Suspended

The artifact is temporarily inactive but remains valid.

## Deprecated

The artifact remains usable but replacement is recommended.

## Archived

The artifact is retained for historical purposes.

## Retired

The artifact is no longer active and SHALL NOT be reused.

Retirement SHALL NOT invalidate historical references.

---

# 6. Lifecycle Transitions

Transitions SHALL occur through explicit Events.

Typical transitions include:

- Create
- Submit
- Approve
- Publish
- Suspend
- Reactivate
- Deprecate
- Archive
- Retire

Silent state transitions SHALL NOT occur.

---

# 7. Identity

Lifecycle transitions SHALL NEVER modify canonical Identity.

Identity survives every lifecycle state.

Only semantic replacement creates a new Identity.

---

# 8. Ownership

Ownership MAY change during the lifecycle.

Ownership changes SHALL be represented through traceable Events.

Ownership changes SHALL NOT affect Identity.

---

# 9. Versioning

Lifecycle and Version are independent concepts; they are two of the three independent times defined in section 1a, and the Projection Lifecycle is the third.

A new version MAY remain in Draft while an older version remains Active.

Version history SHALL remain reconstructable.

The Object Lifecycle, the Version Lifecycle and the Projection Lifecycle SHALL each be tracked independently. A transition in one SHALL NOT imply a transition in another.

---

# 10. Traceability

Every lifecycle transition SHALL preserve:

- transition Event;
- timestamp;
- initiating actor;
- governing authority;
- previous state;
- new state;
- rationale (when available).

Lifecycle history SHALL remain auditable.

---

# 11. Federation

Lifecycle state MAY influence federation.

Federation participants SHOULD evaluate lifecycle state before consuming semantic artifacts.

Retired or Deprecated artifacts MAY still be exchanged for historical or analytical purposes.

---

# 12. Validation

A conforming implementation SHOULD validate:

- permitted transitions;
- lifecycle completeness;
- transition Events;
- temporal consistency;
- version consistency.

Validation SHALL evaluate lifecycle behavior without modifying historical records.

---

# 13. Historical Preservation

Historical lifecycle states SHALL remain reconstructable.

Archived and Retired artifacts SHALL preserve:

- Identity;
- provenance;
- ownership history;
- relationships;
- Events;
- semantic references.

Historical integrity SHALL take precedence over physical deletion.

---

# 14. Architectural Invariants

Lifecycle SHALL preserve:

- canonical Identity;
- semantic meaning;
- provenance;
- traceability;
- constitutional compliance.

Lifecycle SHALL govern state, not truth.

---

# 15. Typical Examples

Examples include:

- Employee: Candidate → Active Employee → On Leave → Former Employee → Archived
- Contract: Draft → Active → Expired → Archived
- Product: Planned → Active → Deprecated → Retired
- AI Agent: Draft → Published → Active → Suspended → Retired

These examples are informative rather than normative.

---

# Future Directions

The separation into three independent times anticipates a future **Three-Times state model** that formally defines the permitted transitions within each timeline, the cross-timeline conditions a Semantic Contract may reference (for example, "Projection permitted only while Object is Active and version ∈ range"), and how the three histories are projected onto a single Semantic Timeline for audit. Such a model would make multi-timeline reasoning — central to federation and Executable Semantic Contracts — explicit and verifiable. This direction is anticipated but not yet normative.

---

# Final Statement

Lifecycle provides the temporal dimension of semantic existence within the Meta-Universe.

By defining explicit states and traceable transitions, Meta-Universe enables semantic artifacts to evolve without losing identity, historical integrity or constitutional continuity. Lifecycle transforms static semantic definitions into living knowledge that can be governed, audited and federated throughout its entire existence.
