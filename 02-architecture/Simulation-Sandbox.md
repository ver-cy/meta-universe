# Simulation Sandbox

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-015  
**Title:** Simulated Sandbox Projections  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** MUC, [Projection](../04-core-concepts/Projection.md), [Event](../04-core-concepts/Event.md), [Change-Process](../01-constitution/Change-Process.md), [Policy-Consistency](../02-architecture/Policy-Consistency.md)  
**Informative References:** [Provenance-Graph](../02-architecture/Provenance-Graph.md), [Validation](../02-architecture/Validation.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

A change that is syntactically valid and locally correct can still be globally
harmful: it may break a downstream contract, violate a policy in another context,
or shift a business outcome. This document defines a **Simulation Sandbox** — an
isolated layer in which a proposed change is **tried before it is real**, so its
effects across the whole model can be assessed before a human is asked to approve
it.

It is the semantic equivalent of a dry-run: a *what-if*, not a commit.

---

# 2. Definition

A **Simulation Sandbox** is an isolated set of [Projected Views](../04-core-concepts/Projection.md)
— a digital shadow of the affected part of the model — into which a proposed
change is applied **without touching canonical state**.

A Sandbox SHALL:

- be derived from a known model version (and its [Semantic Fingerprint](../02-architecture/MMAS-Interchange.md));
- be fully **isolated**: nothing in the Sandbox affects the canonical model, live
  systems, or other federations;
- be **discardable**: a Sandbox can be thrown away with no residue;
- be **traceable**: the simulation and its findings are recorded as
  [Events](../04-core-concepts/Event.md) so a decision can cite them.

---

# 3. What a Simulation Does

Within a Sandbox an agent MAY:

1. Apply the proposed change (to code, structure, or a normative rule).
2. Run the [Policy Consistency Check](../02-architecture/Policy-Consistency.md)
   and [Validation](../02-architecture/Validation.md) against the simulated state.
3. Drive **synthetic load / transactions** and **what-if scenarios**.
4. Assess side effects across the model using the
   [Provenance Graph](../02-architecture/Provenance-Graph.md) ("what breaks if
   this changes?").

Only after the simulation succeeds is the change **proposed to a human** through
the [Change Process](../01-constitution/Change-Process.md). The Sandbox produces
evidence; it does not grant authority to apply.

---

# 4. Isolation Guarantees

- A Sandbox SHALL NOT mutate any canonical Object, Relationship, Event, Contract
  or Projection.
- A Sandbox SHALL NOT emit federation messages to real partners; any federation
  it simulates SHALL use simulated counterparts.
- Simulated Events SHALL be marked as simulation and SHALL NOT enter the
  canonical [Semantic Timeline](../04-core-concepts/Event.md).

---

# 5. Output

A simulation produces a **Simulation Report** referencing: the base model version
and fingerprint, the proposed change, the Validation and Policy Consistency
results, the synthetic scenarios run, and the predicted impact set. This report is
attached to the Change Request as evidence.

---

# 6. Architectural Invariants

- Simulation SHALL NOT alter canonical state or real systems.
- A Sandbox SHALL be derived from an identified, fingerprinted model version.
- Simulation results SHALL be traceable and clearly marked as simulated.
- A successful simulation SHALL NOT auto-apply; it informs a human decision.

---

# Future Directions

- A standard **Simulation Report** schema, feeding the Semantic Test Kit.
- **Counterfactual federation**: simulating a federation with a partner's
  published public schema (and fingerprint) without contacting them.
- Coupling with [Outcome Drift](../02-architecture/Validation.md) so a simulation
  can predict business-outcome effects, not only structural ones.

---

# Final Statement

> The cheapest place to discover that a change is a mistake is in a shadow that
> costs nothing to discard. Simulate first; propose second; apply last.
