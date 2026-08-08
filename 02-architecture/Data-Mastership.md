# Data Mastership

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-018  
**Title:** Meta-Model Architecture Standard - Data Mastership and Systems of Record  
**Document Class:** Normative  
**Version:** 2.1 (Draft)
**Status:** Working Draft  
**Normative References:** MMAS-Core, MMAS-Package, Model-Traversal-and-Layout, Data-Portability-and-Access, Traceability
**Informative References:** Synchronization, Extension-Model, Provenance-Graph, AI-Agent-Guide  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0

---

# 1. Purpose

A Meta-Model rarely lives alone. The same knowledge often also exists in a wiki (Confluence), a tracker (Jira, ClickUp), a CRM, a database or a document store, and those copies are edited by people who never open the model.

This document answers the one question that decides whether such coexistence is order or chaos: **for every dataset, who is the master - the Meta-Model or the external system?**

It defines:

- the **System of Record (SoR)**: the single place where a dataset's truth is authored;
- the three lawful **mastership patterns** (model-mastered, external-mastered, partitioned);
- the **Mastership Register** (`sources.yaml`): the machine-readable declaration of all of the above;
- the flow, freshness, conflict and write rules that follow from each pattern.

Without this declaration, a reader cannot know whether a fact found in the model is authoritative or a possibly stale mirror, and an agent cannot know where a correction must be written. With it, both questions have a mechanical answer.

---

# 2. Scope

This specification governs the relationship between a Meta-Model and **operational systems within the same governance domain**: wikis, trackers, databases, file stores, business applications.

It does not govern:

- **federation between sovereign universes** - that is [Synchronization](../03-federation/Synchronization.md) and MUFP (each peer has its own SoRs; federation never transfers mastership);
- **imported external standards** (Schema.org, FHIR, ISO vocabularies) - those are always externally mastered by their standards bodies and are handled by [Extension-Model](Extension-Model.md).

---

# 3. Design Principles

- **One master per dataset.** Every dataset has exactly one System of Record. "Both places are kind of authoritative" is non-conforming by definition.
- **Mastership is declared, not inferred.** No reader should deduce authority from folder names, habits or team lore.
- **Flow follows mastership.** Data moves *from* the master *to* its copies; a copy is never written except by that flow.
- **Copies are disposable.** Any non-master copy can be deleted and rebuilt from the master without loss.
- **Provenance is mandatory.** Every mirrored datum knows where it came from and when.

---

# 4. Definitions

- **Dataset** - a coherent body of data governed as one unit (a set of Objects, a page tree, a table, a register). The granularity is chosen by the model owner; mastership is declared per dataset.
- **System of Record (SoR)** - the system in which a dataset is *authored* and whose state prevails in any conflict.
- **Mirror** - a copy of an externally mastered dataset held inside the model, produced by harvesting.
- **Harvest** - the pipeline that captures an external dataset into the model (raw capture + semantic transform).
- **Write-back projection** - a copy of a model-mastered dataset published into an external system for convenience of reading, storage or processing.

---

# 5. The Three Mastership Patterns

## 5.1 Pattern M: Model-Mastered

The dataset is **born in the Meta-Model**. Facts are authored directly in the model (edited, reviewed, versioned like code). External systems receive **write-back projections**: rendered pages, exported tables, synchronized records, published for people and tools that prefer to read there.

Rules:

- The flow is **model → external**, always.
- Every projected copy SHALL be marked as generated: it declares its master, its generation time and a "do not edit here" notice in whatever form the target system supports (page banner, record field, file header).
- Edits made in the external copy have **no authority**. An implementation SHOULD either lock the external copy, overwrite it on next publication, or capture such edits as *change proposals* routed back to the model's normal change process; it SHALL NOT silently merge them.
- In any conflict, **the model wins**.

*Example: an architecture decision register authored in the model; Confluence carries a generated, read-only rendering of it because the wider organization lives in Confluence.*

## 5.2 Pattern E: External-Mastered

The dataset **lives and changes in an external system** (a Confluence space that teams update daily, a tracker, a production database). The model holds a **mirror**: a harvested, semantically structured copy that lets the model link to, classify and reason over the data.

Rules:

- The flow is **external → model**, always.
- Harvesting SHALL land the unmodified capture under `raw/<system>/<dataset>/` with its provenance sidecar, per [Model-Traversal-and-Layout](Model-Traversal-and-Layout.md) §6; the semantic transform then populates the mirror in the model's layers.
- Mirrored content is **read-only inside the model**. A correction is made in the external system and re-harvested; the model may additionally record an annotated deviation ("source says X, we assess Y") as its own, model-mastered statement, clearly separated from the mirrored fact.
- Every mirrored dataset SHALL carry **freshness metadata**: time of last successful harvest, declared cadence, and a staleness limit after which consumers SHALL be warned.
- In any conflict, **the external system wins**; the mirror is corrected by re-harvest, never the other way.

*Example: AI agents continuously harvest a living Confluence space into the model; the model adds structure, links and classification, but the pages themselves are authored in Confluence.*

## 5.3 Pattern H: Partitioned

The knowledge area is split: some datasets (or fields) are model-mastered, others external-mastered. This is the common real-world case and it is lawful **only when the partition is explicit**:

- Each partition SHALL be declared as its own dataset with a single master (Pattern M or E).
- The same field SHALL NOT be writable on both sides. Bidirectional mastership of one datum is non-conforming; if truly needed, split the datum (for example: external system masters `status`, model masters `assessment`).
- Cross-partition references are permitted and encouraged; they are references, not copies.

---

# 6. The Mastership Register (`sources.yaml`)

Every conforming repository SHALL contain a Mastership Register at its root, covering **every dataset the model holds or mirrors**. A dataset absent from the register is treated as model-mastered and fully authored in place; any involvement of an external system without a register entry is non-conforming.

Each entry SHALL declare:

| Field | Meaning |
|-------|---------|
| `id` | Stable dataset identifier |
| `description` | What this data is, in one line |
| `master` | `model` or `external` |
| `system` | For external involvement: system name, URL, scope (space, project, table) |
| `model_location` | Where the dataset (or its mirror) lives in the repository |
| `flow` | `model->external`, `external->model`, or `none` |
| `pipeline` | The harvester or publisher (tool, script, agent) that moves the data |
| `cadence` | How often the flow runs; for mirrors, also `staleness_limit` |
| `conflict_rule` | Restatement of who wins, plus escalation contact (`steward`) |
| `status` | Lifecycle of the flow: `active` (default), `declared`, `suspended`, `retired` |
| `binding_refs` | One or more ARCH-019 DatasetBindings that say where, how and at which snapshot the dataset is accessed |

`system`, `model_location` and `pipeline` remain valid human-oriented summaries. When a dataset uses a non-package-tree carrier, automated traversal, more than one representation, or more than one access protocol, it SHALL provide `binding_refs` (or equivalent inline DatasetBindings). Mastership remains singular even when bindings are plural: a mirror, API and package may expose the same dataset without becoming additional Systems of Record.

**Declared entries.** Real models pass through a transitional state the register must be able to tell the truth about: mastership is decided but the flow is not yet built - a mirror location exists but has never been harvested, or a write-back is agreed but no pipeline publishes it. Such entries SHALL carry `status: declared`. A declared entry is lawful, but it is **open debt, not operation**: a declared mirror SHALL NOT be presented as fresh (it has no harvest time at all), and a declared write-back gives no drift protection. Hiding the transitional state by omitting the entry, or by marking it `active`, is non-conforming; the register exists precisely to make this state visible.

Illustrative register with both Confluence directions:

```yaml
datasets:
  - id: adr-register
    description: Architecture decision records
    master: model
    system: { name: Confluence, url: https://wiki.example.com, scope: SPACE/Architecture }
    model_location: bundles/architecture/decisions/
    flow: model->external
    pipeline: tools/publish-adr-to-confluence
    cadence: on-change
    conflict_rule: model wins; external edits become change proposals
    steward: architecture-owner

  - id: ops-runbooks
    description: Operational runbooks maintained by the ops team in Confluence
    master: external
    system: { name: Confluence, url: https://wiki.example.com, scope: SPACE/Ops }
    model_location: bundles/operations/runbooks-mirror/
    flow: external->model
    pipeline: tools/harvest-ops-runbooks
    cadence: daily
    staleness_limit: 7d
    conflict_rule: Confluence wins; fix at source and re-harvest
    steward: ops-lead
```

This is exactly the artifact that answers "there is a Confluence - what is in it, and who is more authoritative, the meta-model or Confluence?" for every dataset, mechanically.

---

# 7. Conflict and Drift

- **Detection.** Implementations SHOULD detect drift between master and copy (content comparison, fingerprints, timestamps) at least at each flow run.
- **Resolution.** Drift is resolved **only** in the direction declared by `conflict_rule`; resolving "by judgment" per incident is non-conforming.
- **Escalation.** Drift that cannot be resolved mechanically (the partition itself is wrong, the master is disputed) goes to the dataset's steward and, if mastership changes, produces a new register entry version - mastership changes are versioned events, never silent edits.

---

# 8. Freshness and Trust

A consumer of a mirrored dataset SHALL be able to see, without leaving the model: the master system, the last harvest time, and whether the staleness limit is exceeded. Stale mirrors SHALL be flagged, not hidden. A statement sourced from a stale mirror carries that staleness in its provenance; downstream trust decisions (see Trust-Model) MAY weight it accordingly.

---

# 9. AI Agent Rules

An agent working with a conforming model:

- **Before relying on a dataset**: SHALL consult the register; for mirrors, SHALL check freshness and prefer re-harvest over guessing when stale.
- **Before writing**: SHALL write only to the dataset's master. A correction to an external-mastered fact goes to the external system (or to a human with access); a correction to a model-mastered fact goes to the model. Writing to a copy is non-conforming regardless of convenience.
- **When citing**: SHOULD state the master ("per Confluence Ops space, as harvested 2026-07-30") rather than presenting a mirror as origin.

These rules are what allow mixed human-and-agent teams to work on the same knowledge without corrupting it from either side.

---

# 10. Relation to Other Standards

- **[Model-Traversal-and-Layout](Model-Traversal-and-Layout.md)** gives mirrors and projections their physical places (`raw/`, layer mirrors, `artifacts/`) and origins (harvested / generated); this document gives them authority.
- **[Synchronization](../03-federation/Synchronization.md)** governs peers *across* sovereignty boundaries; this document governs tools *inside* one. Federation never moves mastership; a universe exposes only what it masters or clearly labels as mirrored.
- **[Extension-Model](Extension-Model.md)**: imported standards are a fixed special case of Pattern E (master: the standards body; flow: versioned releases in).
- **[Traceability](Traceability.md) / [Provenance-Graph](Provenance-Graph.md)**: harvest and publication runs are provenance events; the register tells you the policy, the provenance graph tells you what actually happened.

---

# 11. Validation

Structural validation (V1) SHALL check: the register exists, parses, and every declared `model_location` exists. Semantic validation (V2) SHOULD check: every mirror has provenance and freshness metadata; no file is writable under two entries; flows match masters (`master: external` never has `flow: model->external`); and every `status: declared` entry is reported as open debt. Runtime validation (V5) MAY check staleness limits against actual harvest history, and SHOULD downgrade an entry whose declared cadence has never actually run to `declared`.

---

# 12. Architectural Invariants

Mastership SHALL preserve:

- a single System of Record per dataset at any moment;
- declared, versioned mastership transitions;
- provenance and freshness of every mirror;
- disposability of every non-master copy;
- constitutional compliance.

Mastership SHALL NEVER be implied by physical location alone: a DatasetBinding says where and how; the register says whose truth wins.

---

# 13. Future Directions

ARCH-019 DatasetBindings provide the common connector surface for files, Git, databases, object stores, HTTP and MCP. Future ecosystem profiles may standardize vendor-specific capabilities without changing mastership law. Surfacing register entries and bindings in an SDP lets a consumer see immediately which parts are authored knowledge and which are mirrors of an external source.

---

# Final Statement

Every dataset has exactly one home for its truth. The Mastership Register makes that home explicit, the flow rules keep copies honest, and the freshness rules keep readers honest about copies.

A model that declares its masters can safely coexist with wikis, trackers and databases; a model that does not is one edit away from two truths.
