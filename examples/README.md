# Examples

**Meta-Universe Specification**

**Document ID:** MU-V2-EX-000  
**Title:** Examples — Policy and Plan  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [Getting-Started](../07-guides/Getting-Started.md), [Create-a-New-Meta-Model](../07-guides/Create-a-New-Meta-Model.md)  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0

---

# Purpose

This folder holds a small number of **minimal, teaching-oriented** examples that
illustrate the Meta-Universe standards in practice. Every example is machine-checked
(fingerprints round-trip; documents parse and validate).

# Available examples

| Example | Shows |
|---------|-------|
| [`minimal-person`](minimal-person/) | The smallest complete MUIF meta-model; one model in two serializations proving the **Semantic Fingerprint** is serialization-independent; a passing **Validation Report**. |
| [`federation-handshake`](federation-handshake/) | A 10-envelope [MUFP](../03-federation/MUFP-Messages.md) handshake walking the protocol state machine. |
| [`federation-acme-govtax`](federation-acme-govtax/) | **The golden end-to-end example.** Two sovereign universes with different vocabularies federate over one Person — Identity → Mapping → Contract → Projection → Synchronization → Conflict — with real fingerprints, validation reports and a 17-envelope transcript (data moves only at message 14). |
| [`data-bindings`](data-bindings/) | MMAS 2.1 portable bindings for Git + Markdown, SQL and MCP + safe HTML, including deterministic traversal and coverage policy. |

# Why this folder is intentionally small

Examples are an *implementation* of the standard, not the standard itself. People
copy examples, so they are harder to change later than the specification is.
Until the normative documents (MUC, MMAS, MUFP, Core Concepts) stabilize, this
folder is deliberately kept minimal to avoid freezing patterns prematurely.

# Planned minimal examples

A compact set of 5–10 learning examples is planned:

1. `01-minimal-universe` — the smallest valid Universe
2. `02-employee-meta-model` — a tiny domain meta-model
3. `03-federation-example` — two universes establishing a federation
4. `04-projection-example` — one Meta-Object, several projections
5. `05-import-existing-standard` — importing an external standard as a Semantic Package

# Full reference models live elsewhere

Complete, production-grade reference meta-models (Employee, Organization, Product,
Company, Invoice, Contract, Address, Person, AI Agent, Device, …) are **out of scope
for this repository**. They are intended for a separate, independently versioned
repository — **`meta-universe-reference-models`** — so that the specification stays
compact and stable while the library of reference models can evolve freely.

See [Roadmap](../06-ecosystem/Roadmap.md) for how the repository family is expected
to grow.
