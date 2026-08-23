# AI Integration Patterns

**Meta-Universe Specification**

**Document ID:** MU-V2-GUIDE-009  
**Title:** AI Integration Patterns  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [AI-Agent-Guide](../07-guides/AI-Agent-Guide.md), [Contract](../04-core-concepts/Contract.md), [Projection](../04-core-concepts/Projection.md), [Event](../04-core-concepts/Event.md), [Provenance-Graph](../02-architecture/Provenance-Graph.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This guide gives **concrete patterns** for building AI agents on the
Meta-Universe. It is the implementation companion to the
[AI-Agent-Guide](../07-guides/AI-Agent-Guide.md): where that document explains the
reasoning loop and the principles, this one shows how to wire a real LLM-based
agent — tool-calling schemas, RAG, an enforced Contract inside the agent loop,
vector and graph stores — onto those principles.

The patterns assume the agent uses the language model as a *reasoning engine*, not
as the store of knowledge: knowledge, rules and history live in managed semantic
models outside the model weights.

---

# 2. The Reasoning Loop, Implemented

Every pattern here serves one loop, taken from the
[AI-Agent-Guide](../07-guides/AI-Agent-Guide.md):

```text
Task → Context → Meta-Models → Contracts → Projections
     → Reasoning → Events → Traceable Result
```

The sections below map each stage to a concrete technique:

- **Meta-Models** → loaded into the LLM as tool-calling schemas and
  structured-output constraints (Section 3);
- **Projections + Events** → retrieved through RAG over meaning, not raw rows
  (Section 4);
- **Contracts** → enforced as an Executable Semantic Contract inside the loop
  (Section 5);
- **Reasoning + Traceable Result** → grounded in vector and graph stores
  (Section 6).

---

# 3. Pattern: Load a Meta-Model into an LLM

A Meta-Model is loaded into the language model in two complementary ways:

- **As tool-calling schemas.** Each Object, Projection request and Event-recording
  action the agent may perform is exposed as a tool whose parameter schema is
  derived from the Meta-Model's [MUIF](../02-architecture/MMAS-Interchange.md)
  definitions. The CSN of a concept becomes the canonical tool/field name, so the
  model calls tools in the *vocabulary of the domain* rather than inventing one.
- **As structured-output constraints.** When the agent must emit a Projection or
  an assertion, the expected output is constrained to the relevant primitive's
  schema. The model fills a known shape; it does not free-form a JSON blob the
  caller must then guess at.

Because tool names and field names are CSNs, the same agent retargets to a new
domain by loading a different Meta-Model — the loop is unchanged, only the schemas
differ.

---

# 4. Pattern: RAG over Projections and Events

Conventional RAG retrieves raw rows or document chunks. A Meta-Universe agent
retrieves **meaning**:

- Index and retrieve over [Projection](../04-core-concepts/Projection.md)s — the
  minimal, context-appropriate views — instead of raw internal records. The agent
  receives only what the task needs, already shaped for its Context.
- Index and retrieve over [Event](../04-core-concepts/Event.md)s and the
  [Semantic Timeline](../04-core-concepts/Event.md) so the agent can retrieve
  *what happened and why*, and reconstruct historical state, rather than only the
  current snapshot.
- Carry each retrieved item's provenance edge into the prompt, so retrieved
  context is already traceable through the
  [Provenance Graph](../02-architecture/Provenance-Graph.md).

The effect: retrieval returns interpretable, contract-shaped knowledge with its
lineage attached — not anonymous text the model must re-interpret.

---

# 5. Pattern: An Executable Semantic Contract in the Agent Loop

A [Contract](../04-core-concepts/Contract.md) is enforced as an **Executable
Semantic Contract** *inside* the agent loop, not merely documented around it. The
Contract is consulted on every step:

- **Allowed Projections** — the loop only requests Projections the Contract
  permits for the Task's Purpose; a request outside that set is refused before any
  data is read.
- **Hidden fields** — fields the Contract marks non-disclosable are filtered out of
  retrieved Projections before they reach the model's context window, so the LLM
  never sees what it may not use.
- **Owner-notified Events** — actions the Contract designates as significant emit
  immutable [Event](../04-core-concepts/Event.md)s that notify the owning Universe,
  so disclosure and consequential decisions leave an auditable trail.

Concretely, the contract wraps every tool call:

```text
for each step in the agent loop:
    proposed_action ← LLM(context)
    contract.check(proposed_action.purpose, proposed_action.projection)
        → allow | deny | redact
    if allow/redact:
        result ← execute(proposed_action)            # redact hidden fields
        if action is significant: emit Event → notify owner
    else:
        return refusal to the model with the reason
```

The Contract is thus a runtime guardrail: the agent *cannot* exceed its disclosure
permissions even if the model's reasoning tries to.

---

# 6. Pattern: Vector Stores and Graph Databases

The two stores play complementary roles in the loop:

- **Vector store** — powers the RAG retrieval of Section 4: embeddings of
  Projections and Event summaries enable semantic search for *the meaning the task
  needs*. It answers "what is relevant?"
- **Graph database** — holds the
  [Provenance Graph](../02-architecture/Provenance-Graph.md) and the Relationship
  structure of the Meta-Model. It answers the structural questions of
  [Provenance-Graph §7](../02-architecture/Provenance-Graph.md) — justification
  ("why is this true?"), impact ("what breaks if X changes?") and dependency — that
  similarity search cannot.

A capable agent uses both: the vector store to *find* candidate context, the graph
to *justify and bound* it. Retrieve by similarity; verify and trace by traversal.

---

# 7. Worked Agent-Task Walkthrough

**Task:** "Draft a promotion recommendation for employee E."

```text
Task     : draft a promotion recommendation for employee E
Context  : purpose = HR review; audience = E's manager; constraint = internal only
Meta-Models : Employee + Organization Meta-Models loaded as tool schemas (CSNs)
Contracts : HR Disclosure Contract bound to the loop (Purpose = HR review)
Projections : vector store retrieves E's Competency Projection and the
              Promotion-Policy Projection — already filtered of salary fields the
              contract hides
Reasoning : the LLM applies the policy to the competency evidence; the graph store
            supplies the justification chain (Competency ← Reviews ← Feedback)
Events   : agent emits a Disclosure Event (recommendation drafted under HR
           Contract); owner is notified
Result   : a recommendation, explainable back through Context, Contract,
           Projections and the Provenance Graph to its source observations
```

What makes the result trustworthy is not the prose: it is that every claim traces
through the [Provenance Graph](../02-architecture/Provenance-Graph.md) to grounding
evidence, the salary the model never saw was excluded by the Contract, and the
draft itself is recorded as an [Event](../04-core-concepts/Event.md). The same
agent, given a different Meta-Model and Contract, performs an entirely different
task with the same guarantees.

---

# 8. Integration Checklist

When building an agent on these patterns, confirm:

- Meta-Models are exposed as tool-calling schemas with CSN names.
- Outputs are constrained to primitive schemas.
- RAG retrieves Projections and Events, not raw rows.
- A Contract is enforced inside the loop (allowed Projections, hidden fields,
  owner-notified Events).
- A vector store handles relevance; a graph store handles provenance and impact.
- Every significant action emits an immutable Event.
- Every result is traceable through the Provenance Graph.

---

# 9. Future Directions

These patterns could converge into a reusable **agent runtime profile**: a
standard tool-schema generator from [MUIF](../02-architecture/MMAS-Interchange.md),
a reference Executable Semantic Contract enforcement library, and a retrieval
contract that binds vector and graph stores to Projections and the Provenance
Graph. Combined with autonomous federation negotiation from the
[AI-Agent-Guide](../07-guides/AI-Agent-Guide.md), such a profile would let any
conforming agent plug into any Universe with provenance, disclosure limits and
explainability guaranteed by construction.

---

# Final Statement

Building an AI agent on the Meta-Universe is not about a cleverer prompt. It is
about wiring the language model into a loop where the domain, the rules, the views
and the history live in managed semantic models around it — so that what the agent
retrieves is meaning, what it may disclose is enforced, and what it concludes can
always be traced back to the evidence that made it true.
