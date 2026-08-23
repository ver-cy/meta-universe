# Provenance Graph

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-011  
**Title:** The Queryable Provenance Graph  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** [Traceability](../02-architecture/Traceability.md), [Event](../04-core-concepts/Event.md), [MMAS-Core](../02-architecture/MMAS-Core.md), RFC 2119  
**Informative References:** [MMAS-Interchange](../02-architecture/MMAS-Interchange.md), [Contract](../04-core-concepts/Contract.md), [Projection](../04-core-concepts/Projection.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

[Traceability](../02-architecture/Traceability.md) introduces **Semantic
Lineage** as the history of the origin of meaning and notes that it may be
promoted to a first-class, queryable artifact. This document realizes that:
it makes Semantic Lineage a **Provenance Graph** — a navigable, queryable
structure in which every conclusion is connected to the evidence that grounds
it, and the consequences of any change can be traced forward and backward.

The Provenance Graph turns *"why is this fact true?"* and *"what breaks if this
changes?"* from manual investigations into deterministic graph queries.

---

# 2. Scope

This specification applies to:

- the node and edge types that compose the Provenance Graph;
- its relationship to [Event](../04-core-concepts/Event.md) causality;
- the standard query patterns a conforming implementation SHALL support;
- the cross-Universe behavior of provenance under federation.

It does not mandate a graph-storage technology; any implementation that answers
the queries of Section 6 over the model of Sections 4–5 conforms.

---

# 3. Principles

- **Lineage is a graph, not a log.** A conclusion may derive from many facts, and
  a fact may influence many conclusions.
- **Edges are explicit.** Provenance relationships SHALL be declared, not
  inferred after the fact.
- **The graph is append-only.** It grows through immutable
  [Event](../04-core-concepts/Event.md)s; it is never silently rewritten.
- **The graph is queryable.** Impact, dependency and justification SHALL be
  answerable by traversal.

---

# 4. Node Types

The Provenance Graph SHALL recognize the following node types:

| Node | Meaning |
|------|---------|
| **Object** | A Semantic Point of Truth — *what exists*. |
| **Event** | An immutable record of *what happened* (see [Event](../04-core-concepts/Event.md)). |
| **Projection** | A context-specific view derived from one or more Objects. |
| **Contract** | The rule under which knowledge was used or disclosed. |
| **Source** | An external origin (an upstream system, document, observation or another Universe) that is not itself a Meta-Universe Object. |

Every node SHALL carry a stable identity and the
[minimum traceability metadata](../02-architecture/Traceability.md) appropriate
to its kind.

---

# 5. Edge Types

The Provenance Graph SHALL recognize the following directed edge types:

| Edge | From → To | Meaning |
|------|-----------|---------|
| `derivedFrom` | Object/Projection/Event → Object/Event/Source | The target is an input from which the source was produced. |
| `influences` | Object/Event → Object/Projection | The source contributed to, but did not solely determine, the target. |
| `assertedBy` | Object/Event/Projection → Source (actor) | The target was asserted by the named actor or authority. |
| `governedBy` | Projection/Event/Object → Contract | The use or disclosure was governed by the referenced Contract. |

`derivedFrom` and `influences` capture *semantic* dependency (origin of meaning);
`assertedBy` captures *authorship* (provenance); `governedBy` captures *authority*
(the rules in force). An edge SHALL be created as part of, or referenced by, an
immutable Event, so that the graph itself remains traceable and unrewritable.

---

# 6. Relationship to Event Causality

The Provenance Graph and Event **causality** are two views of the same history:

- **Causality** links Events across *time* — *this Event happened because that
  Event happened* (see [Event §9](../04-core-concepts/Event.md)).
- **Provenance** links facts across *meaning* — *this conclusion is true because
  those facts are true*.

A `derivedFrom` edge between two conclusions SHALL be consistent with the
causality between the Events that produced them: if conclusion B derives from
conclusion A, the Event that asserted B SHALL causally follow the Event that
asserted A. Lineage explains the origin of meaning across entities; causality
explains the origin of change across time. Together they make the graph both a
*semantic* and a *temporal* explanation of any fact.

---

# 7. Standard Query Patterns

A conforming implementation SHALL be able to answer the following over the
Provenance Graph:

## 7.1 Impact — "what breaks if X changes?"

A **forward** traversal from node X along `derivedFrom` and `influences` edges
(reversed) yields every Object, Projection and conclusion whose meaning depends
on X, transitively. This identifies the downstream facts that become stale if X
changes and SHALL be re-evaluated.

## 7.2 Dependency — "show all conclusions depending on Event Y."

A traversal from Event Y following the Events and facts it `influences` /
that are `derivedFrom` it yields the dependency cone of Y — every conclusion that
rests, directly or transitively, on Y.

## 7.3 Justification — "why is this fact true?"

A **backward** traversal from a fact along `derivedFrom`, `influences`,
`assertedBy` and `governedBy` edges yields its justification: the inputs it was
derived from, the actor that asserted it, and the Contract that governed its
use — back to the originating Sources. This is the machine-readable answer to
*"why is this true?"*

---

# 8. Worked Example

Consider an *Employee Competency Score* derived through several steps, each
recorded as an Event and connected by provenance edges:

```text
(Source: Sprint Retrospectives)
        ▲ derivedFrom
(Object: Project Feedback) ──assertedBy──▶ (Source: Team Lead)
        ▲ derivedFrom
(Object: Performance Review) ──governedBy──▶ (Contract: HR Disclosure)
        ▲ derivedFrom
(Object: Employee Competency Score)
        │ influences
        ▼
(Projection: Promotion Recommendation)
```

- **Justification** — *why is the Promotion Recommendation what it is?* Backward
  traversal returns: it `derivedFrom` the Competency Score, which `derivedFrom`
  the Performance Review (`governedBy` the HR Disclosure Contract), which
  `derivedFrom` Project Feedback (`assertedBy` the Team Lead), grounded in Sprint
  Retrospectives.
- **Impact** — *what breaks if a Sprint Retrospective is corrected?* Forward
  traversal returns: Project Feedback, the Performance Review, the Competency
  Score and the Promotion Recommendation — all flagged for re-evaluation.
- **Dependency** — *which conclusions depend on the Event that recorded the
  Performance Review?* The Competency Score and the Promotion Recommendation.

Each answer is produced by traversal, not by reading prose — which is what makes
provenance *operational* rather than merely documented.

---

# 9. Federation Behavior

Across a federation, the Provenance Graph SHALL preserve traceability without
surrendering sovereignty. A `derivedFrom` edge MAY point to a Source in another
Universe; that edge SHALL be disclosed only through a
[Projection](../04-core-concepts/Projection.md) governed by a
[Contract](../04-core-concepts/Contract.md), as recorded by `governedBy`. A
Universe therefore exposes *that* a conclusion depends on an external Source —
and under which Contract — without necessarily exposing the Source's full
internal lineage.

---

# 10. Validation

A Provenance Graph conforms to this specification when:

- every edge is one of the defined types and is backed by an immutable Event;
- `derivedFrom` consistency with Event causality holds (Section 6);
- impact, dependency and justification queries (Section 7) return correct,
  transitive results;
- cross-Universe edges are disclosed only under explicit Contracts.

See [Validation](../02-architecture/Validation.md) for the applicable levels.

---

# 11. Architectural Invariants

- The Provenance Graph SHALL be append-only and backed by immutable Events.
- Provenance edges SHALL be explicit, never inferred silently.
- `derivedFrom` SHALL be consistent with Event causality.
- Impact, dependency and justification SHALL be answerable by traversal.
- Cross-Universe provenance SHALL NOT bypass Contracts and Projections.

---

# Future Directions

A future revision could define a standard **provenance query language** and an
interchange format for graph fragments so that impact and justification queries
can run across federated Universes; integrate the graph with the
[Semantic Fingerprint](../02-architecture/MMAS-Interchange.md) so that a source
change is *detected* automatically and its downstream cone *invalidated*; and
attach confidence and Trust Vectors to edges so that justification can be weighed,
not merely listed. These extensions would make automated invalidation of stale
conclusions a first-class, federation-wide capability.

---

# Final Statement

> Provenance stops being a story we tell after the fact and becomes a structure we
> can ask. The Provenance Graph lets any participant trace a conclusion back to
> the evidence that grounds it and forward to everything that would break if that
> evidence changed — across time, across meaning, and across federated Universes.
