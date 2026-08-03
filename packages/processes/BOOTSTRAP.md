# BOOTSTRAP

Operating instructions for this repository. Read this, then [manifest.yaml](manifest.yaml), then [sources.yaml](sources.yaml), then walk in declared order.

## What this repository is

The Vercy operating-process palette: 81 processes in 7 families that keep a meta-model Universe functioning as the primary digital reflection of reality. Normative text lives in the family documents; BPMN files are faithful projections of the cards; `processes.csv` is the machine index.

## Walk order

1. [README.md](README.md): orientation.
2. [00-common/Common-Operating-Law.md](00-common/Common-Operating-Law.md): the preamble every family cites (roles, tiers, iron controls, profiles). Nothing in a family text may weaken it.
3. `01-families/`, in this order: mirror-and-actualization, actuation-and-reality-feedback, contribution-and-entry-control, exchange-and-federation, quality-consistency-security, context-execution-collaboration, governance-access-operations.
4. [processes.csv](processes.csv): the index (id, family, name, tier, bpmn path).
5. `02-bootstraps/`: worked examples, read after the palette.
6. `bpmn/`: diagrams, one per process, path per the csv.

## Local conventions

- Process IDs are `<FAMILY>-<n>` with family prefixes MIR, ACT, CON, FED, QSC, CTX, GOV. IDs are never renumbered; new processes take the next free number.
- Family FILES use full names (never the bare prefix): `CON` is a reserved device name on Windows, so `contribution-and-entry-control.md`, `bpmn/contribution-and-entry-control/`.
- Delegation tiers T1/T2/T3 and the roles are defined once, in the Common operating law section 3; family texts cite, never re-gloss.
- Normative keywords SHALL/SHOULD/MAY. No em-dashes or en-dashes anywhere; do not introduce them.
- Card format is fixed: Purpose, Trigger, Actors, Inputs / Outputs, Steps, Controls, Tier, Variants, Metrics, Failure modes.

## Change rules

- The card is normative; the BPMN file is derived. Change the card first, regenerate the diagram in the same change set.
- `processes.csv` and the family documents must not diverge: a card change that renames, retires or adds a process updates the csv in the same commit.
- Iron controls (IC-1..IC-8) and anything listed in the security-critical dataset class change only by explicit adjudicated decision, never in passing.
- Cross-family edits (interfaces, shared artifacts) name the counterpart process IDs on both sides.

## For AI agents

Assemble context per task: the Common operating law plus the one family you work on. Follow the Agent-Operations recipes of the Vercy standard. Note that this palette itself defines how you should be operated (CTX-9 delegation contracts, IC-3 data-never-command, IC-5 gate-enforced authority); working on it under those same rules is the intended state.
