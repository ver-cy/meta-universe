# Virtual Projection

**Meta-Universe Specification**

**Document ID:** MU-V2-CORE-012  
**Title:** Virtual Projections and Hot/Cold Descriptive Facts  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, [Projection](../04-core-concepts/Projection.md), [Event](../04-core-concepts/Event.md), [Synchronization](../03-federation/Synchronization.md), [Contract](../04-core-concepts/Contract.md)  
**Informative References:** [Traceability](../02-architecture/Traceability.md), [Validation](../02-architecture/Validation.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

Not all facts move at the same speed. The structure of an API changes rarely; a
latency metric changes every second. Treating both the same way forces a bad
choice: commit volatile facts into the model and drown it in churn ("write
amplification"), or store them outside and break the model as the source of
truth.

This document resolves that by classifying descriptive facts as **cold** or
**hot**, and by defining the **Virtual Projection** — a live, contract-governed
view that exposes hot facts *without materializing them into the model*.

---

# 2. Cold and Hot Descriptive Facts

A **descriptive fact** records something that is true about reality (as opposed to
a normative rule, which prescribes). Descriptive facts are classified by their
volatility:

| Class | Examples | Treatment |
|-------|----------|-----------|
| **Cold** | data-model structure, API schemas, dependencies, ownership | Materialized as ordinary [Objects](../04-core-concepts/Object.md) / [Relationships](../04-core-concepts/Relationship.md); versioned; fingerprinted |
| **Hot** | metrics, logs, alerts, live sessions, current infrastructure state | **NOT** materialized; exposed as a **Virtual Projection** backed by a live source |

The boundary is a modelling decision recorded on the fact; a fact MAY be promoted
from hot to cold (e.g. a stabilized configuration) through an explicit change.

---

# 3. Definition

A **Virtual Projection** is a [Projection](../04-core-concepts/Projection.md)
whose content is **computed on read from a live source**, not stored in the model.

A Virtual Projection SHALL:

- reference the Meta-Object or system it projects (`subject`);
- declare its **source** (a stream, query or endpoint) and a **freshness**
  characteristic (e.g. real-time, sampled, windowed);
- be governed by a [Semantic Contract](../04-core-concepts/Contract.md) like any
  other Projection;
- carry [provenance](../02-architecture/Traceability.md) pointing at the live
  source, so a consumer knows the fact's origin and recency.

A Virtual Projection SHALL NOT mutate canonical state, and reading it SHALL NOT
produce a model change. The model stays stable; the value is live.

---

# 4. Why this matters (no write amplification)

Because hot facts are read through Virtual Projections rather than written into
the model:

- the canonical model is **not** rewritten on every metric tick;
- there is no permanent merge-conflict storm from high-frequency updates;
- the model remains the source of truth for *structure and meaning*, while live
  systems remain the source of truth for *current values*;
- an AI agent can read "what is the error rate right now?" on the fly without the
  model ever claiming to *store* that number.

---

# 5. Hot Facts and Events

A Virtual Projection is the *current value*; when a hot fact crosses a meaningful
threshold it MAY additionally emit an [Event](../04-core-concepts/Event.md) (for
example a `Lifecycle` or `Conflict` event on a breach). Events are the durable,
immutable record; the Virtual Projection is the ephemeral live view. The two are
complementary: the stream is read live, the meaningful moments are remembered.

---

# 6. Federation of Virtual Projections

Across [federation](../03-federation/Synchronization.md), a hot fact is shared as
a **stream**, not as repeated commits: a producer delivers `SyncEvent` updates to
a consumer under contract (the
[MUFP Synchronization](../03-federation/MUFP-Messages.md) path), rather than
forcing the consumer to materialize and re-store every change. This is the
federation expression of the same principle: **synchronize meaning and change,
not raw rows.**

---

# 7. Validation

A Virtual Projection conforms when it:

- is governed by a Contract and declares a purpose (like any Projection);
- declares its source and freshness;
- does not materialize into, or mutate, canonical state;
- carries provenance to its live source.

A model SHALL NOT record a hot fact as a cold, materialized fact without an
explicit promotion (Section 2).

---

# 8. Architectural Invariants

- Reading a Virtual Projection SHALL NOT change the model.
- Hot facts SHALL NOT be committed into the canonical model as if cold.
- A Virtual Projection SHALL be contract-governed and provenance-bearing.
- The model remains authoritative for structure and meaning; live systems remain
  authoritative for current values.

---

# Future Directions

- A **Virtual Stream View** descriptor format (source binding, windowing,
  sampling) in MUIF, so virtual projections are themselves discoverable.
- Standard **Outcome Drift** signals derived from hot facts (see
  [Validation](../02-architecture/Validation.md)).

---

# Final Statement

> A model should remember what things *mean* and how they are *built* — not try to
> remember every value they had a millisecond ago. Virtual Projections let the
> living numbers stay live, while the meaning stays still.
