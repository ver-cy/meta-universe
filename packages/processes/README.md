# Vercy operating-process palette

The processes that make a meta-model Universe **function as the primary digital reflection of reality**: how the model stays true to the world (actualization), how the world is changed through the model (actuation), how information enters and leaves under control, how quality, consistency and security are kept, how contexts are built and work is executed on them, and how Owners, Stewards and AI Agents share the work without corrupting it.

Published by the [Vercy](https://ver.cy) project as a package of the [meta-universe repository](../../README.md), prepared for its own repository. The palette applies to any Vercy-conformant meta-model, from a one-person Dimension to a state; the Meta-Orchestrator State (MOS) is the stress-test reference Dimension.

## The palette

**81 processes in 7 families**, indexed in [processes.csv](processes.csv), each with a BPMN 2.0 diagram under [bpmn/](bpmn/).

| Family | Prefix | Owns |
|---|---|---|
| [Mirror and actualization](01-families/mirror-and-actualization.md) | MIR | Reality into model: sources of truth, sensing and ingest, refresh tempos, freshness SLAs, drift detection, quarantine, archival, reasons for update, model retirement |
| [Actuation and reality feedback](01-families/actuation-and-reality-feedback.md) | ACT | Model into reality: signals, decisions, commands to effectors, intended change, verification that reality changed, reconciliation, rollback, the closed loop |
| [Contribution and entry control](01-families/contribution-and-entry-control.md) | CON | The front door: intake, provenance, validation gates, approval, versioning, bulk import, correction, disputes, migration, the consumer register |
| [Exchange and federation](01-families/exchange-and-federation.md) | FED | Exchanging with other Owners: consent lifecycle, contracts, sync, semantic mapping, conflict resolution, disclosure review, admission quarantine, trust vectors, clean termination |
| [Quality, consistency and security](01-families/quality-consistency-security.md) | QSC | Protecting the model: quality scoring, consistency and validation runs, audits, access review, leak response, integrity verification, agent-behavior audit, backup and DR, incidents, standing-job operations |
| [Context, execution and collaboration](01-families/context-execution-collaboration.md) | CTX | Working with the model: context extraction and scaling, decomposition and composition, the FCD execution loop, delegation contracts, session bootstrap, multi-actor collaboration |
| [Governance, access and operations](01-families/governance-access-operations.md) | GOV | The Owner's authority made procedural: decisions and appeals, policies and configs, roles and succession, genesis of a Dimension, resourcing, auditor engagement, internal grants, credentials |

## The common operating law

[00-common/Common-Operating-Law.md](00-common/Common-Operating-Law.md) is the preamble every family cites: the closed reality loop doctrine, the shared role vocabulary (Owner, Steward, Contributor, Consumer, Agent, Auditor), the delegation tiers (T1 human-in-the-loop, T2 human-on-the-loop, T3 autonomous-with-audit), the eight iron controls (IC-1..IC-8, from one-master-per-dataset to append-only history), the quarantine glossary, the conformance profiles, the editorial fast lane and the shipped defaults.

The iron rule everywhere: **information from any meta-model is readable only with the permission of its Owner.**

## Execution variants and the mandatory minimum

Every process card states how it runs solo, in a team, and federated; and manual, hybrid or autonomous. Delegation from Stewards to AI Agents is first-class: every card states which steps an Agent may execute and at which tier.

Three conformance profiles (Common law, section 6): **Full**, **Standard**, and the normative **Solo/Minimal** profile, under which the standing load of a one-person Dimension reduces to exactly three obligations: a weekly combined sweep, a quarterly consolidated review, and the declared continuous monitors.

## Bootstraps (worked examples)

| Example | Shows |
|---|---|
| [Solo Dimension](02-bootstraps/solo-dimension.md) | One Owner-Steward with agents runs the whole palette under the Solo/Minimal profile |
| [Enterprise landscape](02-bootstraps/enterprise-landscape.md) | A product organization: multiple models, one Universe, team stewardship |
| [State Dimension](02-bootstraps/state-dimension.md) | A state-scale Dimension (the MOS pattern): thousands of agents, federation, full profile |

## BPMN

Every process has a BPMN 2.0 XML file under `bpmn/<family>/<ID>-<slug>.bpmn` (path per row in [processes.csv](processes.csv)), openable in any BPMN tool (bpmn.io, Camunda Modeler). Diagrams carry the steps, the named gateways and the start/end events of the process card; the card remains the normative text, the diagram is its faithful projection.

## Provenance

Drafted by six parallel family specifiers, attacked by five adversarial reviewers (65 findings: completeness, security and consent, practicality, consistency, doctrine conformance), adjudicated into a 37-point resolution charter, then revised by seven fixers (the seventh family, GOV, was born from the review: every reviewer independently found the same phantom). Full method per the Vercy deep-specification pipeline.

## License

Apache-2.0, inherited from the repository [LICENSE](../../LICENSE).
