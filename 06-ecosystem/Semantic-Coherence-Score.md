# Semantic Coherence Score

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-006  
**Title:** Semantic Coherence Score  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [Validation](../02-architecture/Validation.md), [Certification](../06-ecosystem/Certification.md), [Traceability](../02-architecture/Traceability.md), [Event](../04-core-concepts/Event.md), [Provenance-Graph](../02-architecture/Provenance-Graph.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document describes the **Semantic Coherence Score** — an automated,
transparent measure of *how well a conforming Meta-Model uses the semantic
capabilities available to it*. Where [Validation](../02-architecture/Validation.md)
answers a binary question (does the model conform?), the Semantic Coherence Score
answers a graded one (how rich, traceable and trustworthy is its content?).

The score enables **graded certification**: two models can both pass validation
yet differ greatly in how completely they record Events, document concepts or
carry provenance. The score makes that difference visible and comparable.

---

# 2. What the Score Measures — and What It Does Not

The Semantic Coherence Score measures **content quality**, not architecture.

- It does not re-check conformance; a model is scored only after it passes the
  pass/fail levels of [Validation](../02-architecture/Validation.md).
- It does not judge whether the *modeled domain* is correct; it judges how
  coherently the model expresses what it claims.
- A high score is not a substitute for certification, and a low score does not
  imply non-conformance — a minimal but valid model can score low and still be
  perfectly usable.

In short: validation asks *is it well-formed?*; the score asks *is it
well-developed?*

---

# 3. Contributing Dimensions

The score is composed from independent dimensions, each measurable from the model
and its history:

- **Event completeness** — the share of significant state changes recorded as
  immutable [Event](../04-core-concepts/Event.md)s rather than implied by current
  state alone.
- **Relationship consistency** — the proportion of Relationships that are
  well-typed, bidirectionally resolvable and free of dangling endpoints.
- **Projection coverage** — whether the Objects that are meant to be shared have
  appropriate Projections defined for their intended contexts.
- **Provenance presence** — the share of significant facts carrying provenance and
  participating in the [Provenance Graph](../02-architecture/Provenance-Graph.md).
- **Semantic Mapping quality** — for federated models, how completely and
  cleanly concepts map to the standards and partners they declare interoperability
  with.
- **Documentation completeness** — the share of public concepts with Display
  Names, descriptions and documentation (including localized coverage).
- **Data trust** — the strength of the Trust Vector attached to the model's
  sources and assertions.
- **Freshness** — how recently the model and its high-impact facts were reviewed
  or updated relative to their expected cadence.

---

# 4. The Scoring Model

The score is a transparent **weighted sum** over the dimensions, normalized to a
**0–100** scale:

```text
Score = round( Σ ( weight_d × dimension_d ) )           dimension_d ∈ [0, 1]
                d
```

A reference weighting (publishers and communities can adjust and publish their
own, since the model is transparent):

| Dimension | Weight |
|-----------|-------:|
| Event completeness | 20 |
| Provenance presence | 18 |
| Relationship consistency | 15 |
| Projection coverage | 12 |
| Semantic Mapping quality | 12 |
| Documentation completeness | 10 |
| Data trust | 8 |
| Freshness | 5 |
| **Total** | **100** |

Reported bands give the number an interpretation:

| Band | Range | Reading |
|------|-------|---------|
| Exemplary | 90–100 | Rich, fully traceable, federation-ready content. |
| Strong | 75–89 | Well-developed; minor gaps. |
| Adequate | 60–74 | Usable; noticeable gaps in history or provenance. |
| Developing | 40–59 | Valid but thin; significant content gaps. |
| Minimal | 0–39 | Conformant skeleton; little semantic richness. |

A coherence report publishes the total, the band, and the per-dimension
sub-scores, so the number is never opaque: a reader can always see *which*
dimension lowered it.

---

# 5. How It Complements Validation and MMQS

The score sits between binary validation and a future graded-quality standard:

- [**Validation**](../02-architecture/Validation.md) is the **gate** — V0–V5,
  pass or fail. A model must pass before it is scored.
- The **Semantic Coherence Score** is the **gradient** — a comparable number over
  the same evidence, surfaced through [Certification](../06-ecosystem/Certification.md)
  so that certification can report *graded* quality rather than a single
  pass/fail.
- The **Meta-Model Quality Standard (MMQS)** is the **future standard** that would
  make this gradient normative across the ecosystem (see Future Directions).

Because every dimension is computed from artifacts that validation already
produces — Events, Relationships, Projections, provenance, mappings,
documentation — the score reuses existing evidence and reproduces the same way a
[Validation Report](../02-architecture/Validation.md) does.

---

# 6. Worked Sample Scoring

Consider an *Employee* Meta-Model that has passed Validation. Measured dimensions
(each on 0–1) and the reference weights:

```text
Event completeness        0.90 × 20 = 18.0
Provenance presence       0.80 × 18 = 14.4
Relationship consistency  1.00 × 15 = 15.0
Projection coverage       0.75 × 12 =  9.0
Semantic Mapping quality  0.60 × 12 =  7.2
Documentation completeness 0.70 × 10 =  7.0
Data trust                0.85 ×  8 =  6.8
Freshness                 0.40 ×  5 =  2.0
                                     ------
Total                                 79.4  → 79  (Strong)
```

The published report shows the total (79, "Strong") *and* the breakdown, which
makes the improvement path obvious: Freshness (2.0/5) and Semantic Mapping
quality (7.2/12) are the weakest contributors, so reviewing stale facts and
completing the federation mappings would raise the score the fastest — without
changing the model's architecture at all.

---

# 7. Architectural Position

The Semantic Coherence Score preserves the ecosystem's invariants: it reads
published evidence without modifying the scored model, it does not centralize
authority (any party can recompute it from the same evidence), and it never
overrides conformance. It is a lens on quality, layered on top of validation —
never a replacement for it.

---

# 8. Future Directions

The Semantic Coherence Score is the concrete seed of a future **Meta-Model
Quality Standard (MMQS)**. MMQS could standardize the dimension definitions and
their measurement, publish reference weight profiles per domain, define how
graded scores surface in [Certification](../06-ecosystem/Certification.md) and
the Registry, and integrate with a **Semantic Validation Framework (SVF)** so
that the same test runs produce both the pass/fail verdict and the coherence
gradient. It could also let the [Trust Vector](../02-architecture/Traceability.md)
and the [Provenance Graph](../02-architecture/Provenance-Graph.md) feed
freshness and provenance scoring automatically.

---

# Final Statement

The Semantic Coherence Score turns "is this model good?" from an opinion into a
transparent, reproducible number. By measuring how completely a model records its
history, grounds its facts and documents its meaning — and by always showing the
breakdown behind the total — it lets the ecosystem reward semantic richness
without ever compromising the binary clarity of conformance.
