# Full Context Development (FCD)

**FCD** is the discipline of making every change with full awareness of the context held in the meta-model that governs the system, and of writing what was learned back into that model.

```text
assemble context -> execute with context -> write back -> verify
```

Instead of handing an actor (a developer, an operator, an AI agent) only a task description, FCD hands it the task **plus** the related rules, affected objects, prior decisions, risks and acceptance criteria, with provenance. And it does not consider the change done until the results and learnings are back in the model.

- **The specification:** [spec/FCD.md](spec/FCD.md) (VC-FCD-001, Working Draft 1.0)
- **Conformance levels:** FCD Core, FCD Traceable, FCD Measured
- **Applies to:** any system governed by a [Vercy](https://ver.cy)-conformant meta-model: a software product, an organization, an event portfolio, a state

## Why it exists

Task-only development destroys constraints the actor cannot see, breaks unseen dependents, re-litigates settled decisions, and lets learnings evaporate. AI agents amplify all four failure modes because they start each session from zero. FCD closes the loop in both directions: the model feeds the work, the work feeds the model.

## Origin and stewardship

FCD originated inside [AISMM](https://github.com/orkestron-ai/software-meta-model), the AI-oriented Software Meta-Model, as a software-product practice. This repository publishes the generalized standard as part of the Vercy project; AISMM remains the reference implementation.

## Related Vercy repositories

| Where | What it is |
|---|---|
| [the standard](../../README.md) | Vercy itself: Dimensions, Namespaces, Objects, Projections, Events, federation |
| [the live register](../../06-ecosystem/registry/) | The searchable register of published meta-models |
| [world-models](../world-models/) | Example meta-model library: describing the world of people and events |
| [processes](../processes/) | The operating-process palette that runs a model day to day |

## License

Apache-2.0, inherited from the repository [LICENSE](../../LICENSE).
