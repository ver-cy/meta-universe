# BOOTSTRAP

Operating instructions for reading and changing this repository. Read this file first; then [manifest.yaml](manifest.yaml); then [sources.yaml](sources.yaml); then walk in the declared order.

## What this repository is

The Vercy world-model library: a catalogue of 145 meta-models describing the world of people and events on Earth, with 18 models deepened to full normative specifications. It is an **example library** published by the Vercy project; the Meta-Orchestrator State (MOS) is the reference Dimension consuming it.

## Walk order

1. [README.md](README.md): orientation.
2. [World-Model-Architecture.md](World-Model-Architecture.md): the catalogue, clusters, layering and dependency order. This is the map; do not read the deep specifications before it.
3. [world-models.csv](world-models.csv) and [meta-models.csv](meta-models.csv): the machine registers. Status column: `candidate` (catalogued, not deepened) or `draft` (deepened specification exists).
4. `models/`, in dependency order (security first, economy last):
   Security-Ownership-and-Access, Registry-and-Ledger, Actions-and-Events, Offense-and-Enforcement, Property-and-Ownership, Civic-Health-and-Democracy, Economy-and-Markets.

## Local conventions

- Deep specifications use per-section invariant prefixes (S, R1, K2, A18, P2, C1, FVAL, COMP, ...) that never collide across the corpus.
- On conflict between the architecture summary and a deep specification, the deep specification governs for its models.
- Normative keywords SHALL / SHOULD / MAY. No em-dashes or en-dashes anywhere in the corpus; do not introduce them.
- External doctrine anchors (charter, value doctrine) link to the reference Dimension's repository; they are examples of binding, not part of this library's normative core.

## Change rules

- This repository is the System of Record for the library ([sources.yaml](sources.yaml)); edit here, never in a mirror.
- Catalogue changes (new models, status flips) go to the csv registers AND the architecture document together; they must not diverge.
- A model's status flips `candidate -> draft` only when a deep specification lands in `models/`.
- Deepening a cluster follows the published method: parallel drafters, adversarial review, a numbered resolution charter, one revision pass. Record provenance in the specification header.
- Do not renumber existing invariants; add new ones at the end of their section.

## For AI agents

Follow the Agent-Operations recipes of the Vercy standard (cold start, answer-from-model, change-with-mastership). Your context window is smaller than this corpus: assemble context per task (architecture document plus the one specification you work on), do not load the whole corpus.
