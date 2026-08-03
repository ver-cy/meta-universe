# Vercy packages

The Vercy project publishes more than the standard. Each package below is a **separate product with its own System of Record**, kept here today because it has not yet been given its own repository. Each directory is self-contained (its own README, and where it is a model, its own `BOOTSTRAP.md`, `manifest.yaml` and `sources.yaml`), so `git subtree split --prefix=packages/<name>` extracts it into a standalone repository with full history the moment one exists.

| Package | What it is | Intended home |
|---|---|---|
| [fcd](fcd/) | **Full Context Development** (VC-FCD-001): every change made with full model context, every learning written back | `ver-cy/fcd` |
| [world-models](world-models/) | The **example meta-model library**: 145 models describing the world of people and events on Earth, 18 of them deepened into 7 normative specifications | `ver-cy/world-models` |
| [processes](processes/) | The **operating-process palette**: 81 processes in 7 families that keep a Universe functioning as the primary digital reflection of reality, with BPMN 2.0 diagrams | `ver-cy/processes` |

The map of the whole family and the path a model travels from publication to use in another Dimension: [Vercy-Repositories](../06-ecosystem/Vercy-Repositories.md). The live register that makes any of these findable: [06-ecosystem/registry](../06-ecosystem/registry/).

## Why they are not folded into the standard

The standard (this repository's `00-foundation` through `07-guides`) defines what a conformant meta-model **is**. These packages are things built **on** it: a development discipline, an example library, and an operating palette. Merging them would blur that line and break the one-master rule the standard itself sets: each package is mastered by its own directory here and by its own repository once split, never by the standard.
