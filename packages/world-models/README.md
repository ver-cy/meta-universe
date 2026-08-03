# Vercy world-model library

An example corpus of meta-models describing **the world of people and what happens on planet Earth**: persons, organizations, property, actions and events, markets and production, health, democracy, security and enforcement.

Published by the [Vercy](https://ver.cy) project as a worked example of meta-modeling at civilization scale. It shows what a serious Dimension looks like when the standard is applied to the hardest subject there is: reality itself.

> This is a **library, not a government program**. Any Dimension may download these models and adapt them. The [Meta-Orchestrator State (MOS)](https://github.com/orkestron-ai/meta-orchestrator-state) is the reference Dimension consuming this library, and the deep specifications carry its doctrine as the running example; your Dimension can rebind them to its own doctrine.

## What is inside

| Artifact | What it is |
|---|---|
| [World-Model-Architecture.md](World-Model-Architecture.md) | The architecture: **145 world-coverage models in 16 clusters** (values, actors, bodies, economy, civilization, environment, property, materiality, utilities, activity, nature, organizations, registries, flows, events, security), layering, dependency order, deepening roadmap |
| [world-models.csv](world-models.csv) | Machine-readable register of the world-coverage models (cluster, model, scope, status) |
| [meta-models.csv](meta-models.csv) | Machine-readable register of the core kernel models |
| [models/](models/) | The deep normative specifications, one dependency-ordered pass each |

## The deep specifications

18 models deepened to full normative depth (invariants, protocols, adversarially reviewed), in dependency order:

| Specification | Models | Covers |
|---|---|---|
| [Security, ownership and access](models/Security-Ownership-and-Access.md) | S1-S8 | The gate for everything: information from any meta-model is readable **only with the permission of its owner** |
| [Registry and ledger](models/Registry-and-Ledger.md) | R1, R2 | How the world is recorded: constitutive registries, append-only ledgers |
| [Actions and events](models/Actions-and-Events.md) | K2, X1 | The world's verbs: acts, events, causality, attribution |
| [Offense and enforcement](models/Offense-and-Enforcement.md) | A18 | The sharpest rights surface: offenses, due process, sanctions |
| [Property and ownership](models/Property-and-Ownership.md) | P2, M3, U1, F8 | The property-bearing nouns: land, objects, infrastructure, claims |
| [Civic, health and democracy](models/Civic-Health-and-Democracy.md) | B10, A10, A13 | The civic layer: housing, health, democratic participation |
| [Economy and markets](models/Economy-and-Markets.md) | C1, K8, C2 | Firms, production, markets: two never-netted ledgers, externality pricing, competition |

Each specification was produced by parallel drafters, adversarially attacked by red-team reviewers (350+ findings total), and revised under numbered resolution charters.

## How to use this library in your Dimension

1. **Find it**: the library is registered as `vercy.world-models` in the [live register](../../06-ecosystem/registry/); registration points here, the authoritative source.
2. **Download it**: clone the repository and take `packages/world-models/`, or vendor a pinned commit into your model's `imports/`. The library is prepared for `git subtree split` into its own repository once one exists.
3. **Read it**: start from [BOOTSTRAP.md](BOOTSTRAP.md); the walk order is declared in [manifest.yaml](manifest.yaml).
4. **Adapt it**: keep the model IDs (S1, R1, K2, ...) for federation compatibility; rebind doctrine anchors to your own canon; record your changes as your Dimension's deltas rather than editing history.
5. **Federate**: two Dimensions that both speak this library's IDs can map their worlds to each other through it.

## Conformance

The repository carries the ARCH-017 traversal contract ([BOOTSTRAP.md](BOOTSTRAP.md), [manifest.yaml](manifest.yaml) with centralized kind rules) and the ARCH-018 mastership register ([sources.yaml](sources.yaml)). This repository is the System of Record for the library; every copy elsewhere is a mirror.

## License

Apache-2.0, inherited from the repository [LICENSE](../../LICENSE).
