# Assets — Canonical Diagrams

**Meta-Universe Specification**

**Document ID:** MU-V2-ASSET-000  
**Title:** Canonical Diagram Assets  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [Reference-Diagrams](../05-reference-architecture/Reference-Diagrams.md), [MUDL](../05-reference-architecture/MUDL.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# Purpose

This folder holds the **canonical diagrams** of the Meta-Universe specification as
Mermaid sources. Each file is a self-contained `.md` with a title, one ```mermaid block,
and a one-line caption. Keeping the diagrams as Mermaid text (rather than binary SVG)
means they can be versioned, diffed and reviewed like any other specification artifact —
and, per [MUDL](../05-reference-architecture/MUDL.md), regenerated from the model so they
cannot drift from the semantics they depict.

# Diagram set

| File | Illustrates |
|------|-------------|
| [`stack.md`](stack.md) | The MUC → MMAS → MUFP → Domain → Applications dependency stack. |
| [`federation-lifecycle.md`](federation-lifecycle.md) | The 9-stage federation lifecycle, Discovery through Termination. |
| [`projection.md`](projection.md) | One Meta-Object projecting into many Projections under Contracts. |
| [`identity-binding.md`](identity-binding.md) | A Canonical identity bound to multiple Local identities. |
| [`event-flow.md`](event-flow.md) | Events accumulating into a Semantic Timeline from which state is derived. |

# Rendering

Every file contains a ```mermaid fenced block and renders directly on GitHub and in any
Mermaid-aware viewer. The [MUDL](../05-reference-architecture/MUDL.md) specification
defines how such diagrams are generated deterministically from a MUDL source document, so
the same model produces the same picture across Mermaid, PlantUML and SVG.

# Conventions

Diagrams follow the conventions in
[Reference-Diagrams](../05-reference-architecture/Reference-Diagrams.md) Section 13:
rectangles for semantic artifacts, rounded rectangles for processes, solid arrows for
semantic relationships, dashed arrows for references.
