# Vercy Repositories

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-010
**Title:** The Vercy Repository Family
**Document Class:** Informative
**Version:** 2.0 (Draft)
**Status:** Working Draft
**Normative References:** Registered-Meta-Models, Model-Traversal-and-Layout, Data-Mastership
**Informative References:** Repository-Structure, Agent-Operations, Known-Implementations
**Copyright:** © Orkestron.AI
**License:** Apache-2.0

---

# 1. Purpose

This document maps the repository family of the Vercy project: which repository holds what, how a meta-model travels from publication to use in someone else's Dimension, and where the operating knowledge (processes, FCD) lives. It is the orientation page for anyone arriving at the ecosystem.

The design follows the standard's own rules: each repository has one semantic responsibility, each dataset has one master (ARCH-018), and every repository that carries a model carries the traversal contract (ARCH-017).

---

# 2. The family

| Repository | Responsibility | Status |
|---|---|---|
| [meta-universe](https://github.com/ver-cy/meta-universe) | **The standard.** MUC, MMAS, MUFP; constitution, architecture, federation, core concepts, guides; the [live register of meta-models](registry/) | Live |
| [world-models](https://github.com/ver-cy/world-models) | **The example library.** 145-model catalogue of the world of people and events on Earth, with 7 deep normative specifications | Publishing |
| [fcd](https://github.com/ver-cy/fcd) | **Full Context Development.** The VC-FCD-001 standard: every change made with full model context, every learning written back | Publishing |
| processes | **The operating palette.** The processes that keep a Universe functioning as the digital reflection of reality: actualization, actuation, contribution, exchange, quality, context operations; execution variants, the mandatory minimum, bootstraps, and BPMN 2.0 diagrams | In preparation |

One dataset, one master: the standard is mastered in `meta-universe`, the register in `meta-universe/06-ecosystem/registry/`, each model in its own repository. Everything else that looks like a copy is a mirror or a rendered artifact (for example, the ver.cy site).

---

# 3. The path of a model

How a meta-model travels through the ecosystem:

1. **Author** it in its own repository, structured per [Repository-Structure](../07-guides/Repository-Structure.md), carrying `BOOTSTRAP.md` and `manifest.yaml` (ARCH-017) and `sources.yaml` (ARCH-018).
2. **Publish** it: the repository becomes the model's System of Record.
3. **Register** it in the [live register](registry/) by pull request: an entry referencing the authoritative source. Registration is discovery, not storage, and does not transfer ownership.
4. **Be found**: consumers search the register's index by kind, domain and conformance.
5. **Be used**: a consumer clones or vendors the source at a pinned ref into their own Dimension, walks it per its bootstrap, binds or adapts it (keeping IDs for federation compatibility), and respects mastership: the registered source stays the master.
6. **Federate**: Dimensions that share a registered model's namespaces can map to each other through it, under the federation protocols (MUFP) and the Owner's consent.

The iron rule applies at every step: information from any meta-model is readable only with the permission of its Owner. `access: restricted` entries register existence without opening content.

---

# 4. People and agents working together

A model is operated by more than one actor: its Owner, accountable Stewards, Contributors, Consumers, delegated AI Agents and Auditors. The standard side of that story lives in [Agent-Operations](../07-guides/Agent-Operations.md) (how any agent reads and changes a conformant model safely: bootstrap first, mastership always, derived copies disposable) and in [Consent-and-Disclosure](../03-federation/Consent-and-Disclosure.md) (what may leave a model and under whose permission).

The operational side, the full process palette with roles, delegation tiers (human-in-the-loop, human-on-the-loop, autonomous-with-audit), execution variants and the mandatory minimum, is the responsibility of the `processes` repository.

---

# 5. Relation to implementations

The Vercy project publishes the standard, the example library, FCD and the process palette. Implementations (products, runtimes, Dimensions built on the standard) are listed in [Known-Implementations](Known-Implementations.md); the reference implementations at the time of writing come from the Orkestron ecosystem, including AISMM (the FCD origin) and the Meta-Orchestrator State (the reference Dimension consuming the world-model library).
