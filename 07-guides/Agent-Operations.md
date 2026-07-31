# Agent Operations

**Meta-Universe Specification**

**Document ID:** MU-V2-GUIDE-010  
**Title:** Operating Instructions for AI Agents Working on a Conformant Model  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** Model-Traversal-and-Layout, Data-Mastership, Validation  
**Informative References:** AI-Agent-Guide, AI-Integration-Patterns, MMAS-Package, Overview  
**Copyright:** © Orkestron.AI  
**License:** Apache-2.0

---

# 1. Purpose

[AI-Agent-Guide](AI-Agent-Guide.md) explains how to *build* agents on the standard. This guide is narrower and more practical: you are an agent that has just been pointed at a **conformant model repository** and asked to read it, answer from it, or change it. These are your operating instructions, distilled from the normative rules of [Model-Traversal-and-Layout](../02-architecture/Model-Traversal-and-Layout.md) (ARCH-017) and [Data-Mastership](../02-architecture/Data-Mastership.md) (ARCH-018) into recipes.

The rules exist so that mixed human-and-agent teams can work on the same knowledge without corrupting it from either side. Every recipe below is a consequence of three facts: every file has a declared meaning, every dataset has exactly one master, and every derived copy is disposable.

---

# 2. Recipe: cold start (first contact with a model)

1. Read **`BOOTSTRAP.md`**. It tells you how this particular model wants to be read, what its local conventions are, and what you must not touch. If an ecosystem entry file exists too (`CLAUDE.md`, `AGENTS.md`), read it after: it carries operating state, BOOTSTRAP carries structure.
2. Read **`manifest.yaml`**: identity, bundle order, classification rules, exclusions.
3. Read **`sources.yaml`**: which datasets are mastered here and which are mirrors of external systems, with freshness and conflict rules. *Do this before reading content*, or you will not know whether what you read is authoritative.
4. Walk the bundles **in declared order** (foundation first), layers in order, layer `README.md` before records.
5. If a coverage walker is present (conventionally `tools/mu-walk*`), run it. A failing walk means the model's own map is broken: report that before trusting anything else.

Time-saving rule: the walk order is dependency order. If you only need one bundle, you still read the manifests and the foundational bundles' READMEs first: they define the vocabulary the later bundles speak.

---

# 3. Recipe: answering questions from a model

1. Resolve the answer to specific records; cite them by path or record ID.
2. Before relying on any fact, check its dataset in the register:
   - **model-mastered** → the record is the truth; answer plainly.
   - **external-mastered mirror** → check freshness. Within the staleness limit: answer, naming the master ("per the Ops Confluence space, as harvested 2026-07-30"). Beyond it: say the mirror is stale and prefer re-harvest over guessing.
   - **`status: declared`** → there is no data yet, only an intention; never present a declared mirror as fact.
   - **`status: retired`** → the source system is gone; the mirror is a frozen archive. Answer historically ("as of the final export"), never as current state.
3. Distinguish origins: a `raw/` capture is evidence of what a source said; a record is the model's own statement. When they disagree, say so; the model may hold an annotated deviation on purpose.

---

# 4. Recipe: writing to a model

1. **Find the master first.** Look the dataset up in `sources.yaml`. Write only to the master; writing to a copy is corruption regardless of convenience:
   - model-mastered → edit the record in place, following the model's naming and record conventions.
   - external-mastered → the correction belongs in the external system. If you cannot reach it, deliver the correction to someone who can (or record it as a clearly-marked model-mastered annotation *about* the mirror; never edit the mirrored bytes).
2. **Respect origins.** Never hand-edit anything harvested (`raw/`, mirrors) or generated (`artifacts/`). The fix goes to the source system or the generator.
3. **Keep the walk true.** If you add, move or delete files, re-run the coverage walker and commit the fresh report. A new file that no rule classifies is an orphan: extend the manifest rules (or place the file correctly), do not ignore the failure.
4. **Keep the registers true.** New dataset, new pipeline, changed mastership → update `sources.yaml` in the same change. Mastership changes are versioned events, not silent edits.
5. If the model feeds write-back projections (a site, a wiki page), run the model's drift check after your edit and republish if it reports drift.

---

# 5. Recipe: harvesting an external system into a model

1. Confirm the dataset's register entry (master, scope, cadence). No entry → create one first; harvesting without declared mastership is how two truths are born.
2. Land the **unmodified capture** under `raw/<system>/<dataset>/` with a provenance sidecar (source, scope, extraction time, tool, count).
3. Apply the transform into the mirror location; never "improve" facts during transform: enrichment is a separate, model-mastered layer.
4. Update freshness metadata; re-run the walker.

## Recipe: publishing a write-back projection

1. Generate from model records mechanically; a hand-tuned projection is a fork, not a projection.
2. Mark the copy: master, generation time, "do not edit here", in whatever form the target supports.
3. Make drift detectable: a content hash over the comparable part, compared by a check command, is the minimum.
4. Prefer automation for the check (a daily job that alerts a human on drift), so divergence is noticed by machinery, not by embarrassment.

---

# 6. When to refuse

Refuse the write and explain, when:

- you cannot determine a dataset's master (missing or ambiguous register entry);
- you are asked to edit a mirror, a raw capture or a generated artifact in place;
- you are asked to bypass the walk (add semantic files as "excluded", hide content from classification);
- the model's coverage check fails and the requested change would build on the unclassified area;
- a proprietary or restricted dataset's conflict rule forbids the requested disclosure.

An agent that cannot tell what it may edit must not edit. This is [ARCH-017 §11](../02-architecture/Model-Traversal-and-Layout.md) in practice.

---

# 7. Multi-agent and human-team etiquette

- **Leave the walk green.** The walker is the shared invariant between sessions and between agents: never hand over a red walk.
- **Registers over memory.** Anything a future session must know about structure or authority belongs in BOOTSTRAP, the manifest or the register, not in a chat log.
- **Small declared changes.** Prefer adding a record over rewriting one; prefer extending a rule over special-casing a file; keep record IDs stable.
- **Provenance on derived work.** If you generated or summarized content from sources, say from what, with what tool, when: the model's trust machinery (validation status, owner review) depends on it.

---

# 8. Worked reality

Two production models exercise every recipe above and are worth reading as executable documentation: the Orkestron.AI product model (write-back projection to a public site with a hash drift check and a daily alerting watch) and the DevTeam.Games platform model (external source-code mirrors, a retired system of record kept as frozen evidence, a proprietary never-publish dataset). See the [Orkestron case study](../06-ecosystem/Case-Study-Orkestron-Ecosystem.md).

---

# Final Statement

A conformant model tells you how to read it, what everything is, and who owns each truth. Your job as an agent is symmetrical: read in the declared order, write only where truth lives, and leave the declarations as true as you found them.
