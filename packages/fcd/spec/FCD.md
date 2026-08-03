# Full Context Development (FCD)

**Vercy Standard**

**Document ID:** VC-FCD-001
**Title:** Full Context Development
**Document Class:** Normative
**Version:** 1.0 (Draft)
**Status:** Working Draft
**Normative References:** Meta-Universe Context, Model-Traversal-and-Layout (ARCH-017), Data-Mastership (ARCH-018)
**Informative References:** AISMM (reference implementation), Agent-Operations
**Copyright:** © Vercy project contributors
**License:** Apache-2.0

---

# 1. Purpose

Full Context Development (FCD) is the discipline of making every change to a system with full awareness of the context held in the meta-model that governs that system.

A task description alone answers "what should I do". FCD requires that the actor, human or AI agent, also holds the answers to "why does this exist", "what will be affected", "which rules constrain this", "what was decided before", and "how will we know it worked", and that whatever the actor learns while working flows back into the model.

FCD originated inside AISMM, the AI-oriented Software Meta-Model, as a practice for software products. This document generalizes it: FCD applies to any system governed by any Vercy-conformant meta-model, whether the system is a software product, an organization, an event portfolio, or a state.

# 2. Definitions

- **Governing model.** The meta-model that is the authoritative semantic description of the system being changed.
- **Context.** The subset of the governing model relevant to one task, as defined by the Meta-Universe Context concept.
- **Context package.** A self-contained, versioned bundle of context assembled for one task: the task itself plus the related objects, rules, decisions, risks and acceptance criteria, with provenance.
- **Context assembly.** The process of selecting and packaging context from the governing model for a task.
- **Context scaling.** Producing the same context at different depths (summary, working, full) so it fits the consumer's window without losing pointers to the full detail.
- **Context fingerprint.** A stable identifier (hash) of the exact context package used for an execution.
- **Write-back.** Recording the results, decisions and learnings of an execution into the governing model.
- **Model debt.** A recorded gap: context that was needed but missing or stale.

# 3. The problem FCD solves

Without FCD, changes are made from task descriptions. The result is familiar in every domain:

- the actor does not know why the current state exists, so it destroys constraints it cannot see;
- the actor does not know what else depends on the changed part, so it breaks neighbors;
- decisions are re-litigated because prior decisions are not at hand;
- what the actor learned evaporates when the task closes;
- AI agents amplify all four, because they start from zero context every session.

FCD closes the loop: the model feeds the work, and the work feeds the model.

# 4. The FCD loop

Every FCD-conformant change follows one loop:

```text
assemble context -> execute with context -> write back -> verify
```

## 4.1 Normative requirements

**FCD-R1 (assembly first).** Every change to the governed system SHALL begin with context assembly from the governing model. An actor SHALL NOT begin execution from a task description alone.

**FCD-R2 (package minimum).** A context package SHALL contain at least: the task and its acceptance criteria; the objects to be changed and the objects that depend on them; the rules and constraints in force; the prior decisions that touch the same objects; the known risks; and the provenance of each element (which record, which version).

**FCD-R3 (scaling with lossless pointers).** When a context package is scaled down to fit a consumer's window, every summarized element SHALL carry a pointer to its full form in the governing model. Scaling MAY drop detail; it SHALL NOT drop pointers.

**FCD-R4 (fingerprint).** Execution SHALL record the context fingerprint of the package actually used, so it is always answerable which context a change was made under.

**FCD-R5 (write-back).** Before a change is considered done, its results SHALL be written back to the governing model: the outcome, new or changed decisions, and learnings that future actors need. Write-back SHALL route through the model's contribution controls and SHALL respect data mastership (ARCH-018): results about data mastered elsewhere are routed to the master system, not written to a mirror.

**FCD-R6 (verification).** The acceptance criteria carried in the context package SHALL be checked after execution. A divergence between the model's expectation and observed reality SHALL trigger the model's actualization process, not be silently ignored.

**FCD-R7 (missing context is debt).** When an actor discovers that needed context is missing, stale or wrong, that gap SHALL be recorded as model debt in the governing model, even if the actor works around it.

**FCD-R8 (agent parity).** The same loop applies to human and AI actors. An AI agent executing under delegation SHALL receive its context package through the same assembly process, and its write-back SHALL pass the same controls, as a human actor's would.

# 5. Context package structure

The reference shape of a context package. Field names are RECOMMENDED; the content classes of FCD-R2 are mandatory.

```yaml
context_package:
  id: ctx-2026-07-31-0001
  task:
    statement: "..."
    acceptance: ["...", "..."]
  scope:
    changing: [object-ids]
    affected: [object-ids]
  rules: [{ id, summary, pointer }]
  decisions: [{ id, summary, pointer }]
  risks: [{ id, summary, pointer }]
  provenance:
    model: <model id and version>
    assembled_by: <actor>
    assembled_at: <timestamp>
  scale: summary | working | full
  fingerprint: sha256:...
```

# 6. Conformance levels

- **FCD Core.** FCD-R1, FCD-R2, FCD-R5, FCD-R6, FCD-R7. The loop runs; context in, results back.
- **FCD Traceable.** Core plus FCD-R3, FCD-R4 and stable identifiers throughout: every change is answerable to the exact context it was made under, and summaries never lose their pointers.
- **FCD Measured.** Traceable plus measured operation: context coverage (how much of the relevant model reached the package), confidence scores on model content, freshness indicators, and model-debt tracking with remediation.

A model or organization claims a level explicitly, for example "FCD Traceable per VC-FCD-001".

# 7. Roles and delegation

FCD uses the shared Vercy role vocabulary: Owner, Steward, Contributor, Consumer, Agent, Auditor. Context assembly, execution and write-back are processes that a Steward MAY delegate to Agents under a delegation contract at tier T1 (human approves each act), T2 (human reviews samples and exceptions) or T3 (autonomous with audit). Accountability for the governing model stays with the Steward at every tier.

# 8. Relation to the Meta-Universe standard

- The **Context** core concept defines what context is; FCD defines the discipline of using it for change.
- **Model-Traversal-and-Layout (ARCH-017)** is the assembly substrate: a conformant model can be walked losslessly, which is what makes reliable context assembly possible.
- **Data-Mastership (ARCH-018)** is the write-back router: results are written where the data is mastered.
- **Projections** are the natural carrier of scaled context; a context package is a task-scoped projection with provenance.
- **Federation** extends FCD across Universes: a context package MAY include elements received from another Owner under consent, and their pointers then carry the federation contract under which they were disclosed.

# 9. Reference implementations

- **AISMM** (AI-oriented Software Meta-Model, github.com/orkestron-ai/software-meta-model): the origin implementation of FCD for software products; its bundles and layers implement context assembly, its traceability graph implements FCD Traceable, its confidence and coverage checks implement FCD Measured.

Other implementations are welcome; see CONTRIBUTING.
