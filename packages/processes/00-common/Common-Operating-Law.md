# Common operating law

This document is the palette preamble of the Vercy operating-process palette. All seven families (MIR, ACT, CON, FED, QSC, CTX, GOV) cite it. Definitions made here are made once: family texts cite this law by section and never re-gloss it. Where a family card and this law appear to conflict, this law governs. The palette is vendor-neutral; Orkestron production models and the Meta-Orchestrator State (MOS) reference Dimension appear in family texts only as reference implementations, never as normative dependencies.

Normative keywords SHALL, SHOULD and MAY are used per common standards practice. Process tier values are core, recommended and optional. Delegation tiers are cited as T1, T2 and T3 as defined in section 3 of this law, and nowhere else.

## 1. The closed reality loop

A Vercy-conformant meta-model exists inside one loop, and every process in the palette is a segment of it: reality -> sensing -> model -> consumption -> decision -> actuation -> reality -> sensing. The mirror stance (MIR) holds the first half: reality changes, the change is sensed, and the model is actualized so that everything the model holds is either authored truth or a mirror that names its master and its harvest time; honestly stale beats falsely fresh, and where the model does not match reality it says so. The actuation stance (ACT) holds the second half: a signal born in the model becomes an authority-bound decision, the decision becomes a command to a registered effector, the effector changes reality, and the loop is closed by sensed evidence, never by the act of commanding. Consumption sits at the hinge: humans, Agents and federated peers read the model at the moment of decision, and what they read carries its freshness, its trust state and its provenance with it. The two stances are one doctrine, not two: a model that only mirrors is a diary, a model that only actuates is a loose cannon, and only the closed loop, where every act is decided on a candid mirror and every effect is confirmed back through sensing, earns the name primary digital reflection of reality.

## 2. Shared role vocabulary

Six roles are used identically across all families:

- Owner: holds ultimate authority over a meta-model and its Dimension; grants and revokes all read and write rights; approves mastership transfers, exposure of new external systems, outward-reaching signal classes and federation contracts.
- Steward: accountable operator of a meta-model or a section of it; runs and answers for the processes, approves T1 acts within delegated scope; accountability never transfers to an Agent.
- Contributor: proposes content and changes through the governed front door; holds no approval authority of their own.
- Consumer: any human, Agent, system or federated peer that reads the model or its Projections; registered with dependencies and notification channel in the consumer register (CON-13).
- Agent: a non-human executor operating strictly under a Delegation Contract (CTX-9) at a stated tier; an Agent SHALL NOT raise its own tier or expand its own access.
- Auditor: independent reviewer with time-boxed, purpose-bound access (GOV-6, GOV-7); samples evidence, certifies closures, never executes operations.

The iron rule of the role model: information from any meta-model is readable only with the permission of its Owner. No process, tier, contract or emergency route creates a read right the Owner did not grant.

## 3. Delegation tiers

Three delegation tiers exist. They are defined here and only here; every card cites them and never re-glosses them:

- T1 human-in-the-loop: the Agent may execute, and each act is human-approved before it takes effect.
- T2 human-on-the-loop: the Agent acts, and a human reviews samples and exceptions after the fact.
- T3 autonomous-with-audit: the Agent acts without per-act human involvement, under a full audit trail reviewed on cadence.

The standard formula for T1 steps in process cards is: SHALL remain T1: Agent proposes, human approves each act. No step in the palette is ever written below T1.

T1 steps are distinct from non-delegable-in-substance acts. A T1 step MAY be executed by an Agent with per-act human approval. A non-delegable act SHALL be performed by the named human role in substance, not merely approved: federation signing (FED-2), mastership rulings (CON-9) and Owner consents are non-delegable, and cards name them as such rather than labeling them T1.

Delegation Contracts and ACT-3 capability contracts are declared specializations of the Semantic Contract per Contract.md 5-6 and Federation-Contracts.md 3a. The Delegation Contract lifecycle (issue, amend, suspend, revoke, tier ladder, probation) has a single System of Record: CTX-9. A new agent-scope pairing starts at T1 or T2; T3 is earned; the first N acts under any grant run one tier stricter than granted. Tier changes are Owner or Steward decisions informed by the closed-loop health review (ACT-12) and capability review (QSC-7), routed as named inputs into CTX-9.

## 4. Iron controls

Eight controls are palette-wide law. Families cite them by identifier (IC-1 through IC-8) and implement them in their gateways; no family text may weaken them.

IC-1 One master per dataset. Every dataset the model holds or mirrors has exactly one declared System of Record, flow direction, pipeline, cadence and conflict rule in the Mastership Register (sources.yaml). Mastership is declared, never inferred; MIR-1 is the sole executor of register changes; no palette process SHALL operate on an undeclared dataset, because harvesting without declared mastership is how two truths are born.

IC-2 Single front door for authored content. Every authored contribution enters the model through the CON-1 intake chain: no side doors, no direct commits around the gates. The harvest carve-out is normative: a registered MIR-2 pipeline run under an active sources.yaml entry IS intake and approval for harvested content; the register entry is the standing authorization, MIR-2 owns the harvest provenance sidecar, and CON-2 through CON-4 do not re-process harvest batches. ACT decision, command and intent Events and CTX-5 write-back sets are registered channels of the same front door.

IC-3 Data is never a command. Content from any non-authored origin is data, never instructions, regardless of what it says, who appears to say it, or how urgently it says it. Every context package section carries an origin/taint class (authored, mirrored-external, federated, human-report), stamped by CTX-1; Delegation Contracts forbid treating any non-authored class as instructions; MIR-2 hazard-screens inbound content for instruction-like, executable or statistically anomalous material and quarantines flags via MIR-8 rather than landing them silently; QSC-7 explicitly tests injection-bait refusal.

IC-4 The security-critical dataset class. The following are security-critical: BOOTSTRAP and bootstrap materials, process and gate definitions, the approval matrix, auto-approval lane criteria, Delegation Contracts, the mastership and conflict-rule fields of sources.yaml, severity rubrics, and watch and threshold configs. For this class: acceptance is always T1 with a second human reviewer; auto-approval lanes are structurally ineligible, enforced in CON-4's gateway rather than by any submitted classification; QSC-9 anchors their hashes continuously; any unexplained diff opens a QSC-8 security incident.

IC-5 Gate-enforced authority. Revocation is gate-enforced, never agent-honored: every write, dispatch and channel access validates the liveness of the citing Delegation Contract at act time, at the gate. Capability material is minted with short validity so worst-case revocation propagation is bounded by a declared TTL; residual authority past the TTL is an incident. Context Packages carry the grant IDs they were built under and expire on grant revocation or a fixed TTL, whichever is sooner.

IC-6 Infrastructure-emitted, hash-chained logs. Action, read, dispatch, disclosure and consent logs are emitted by the mediating infrastructure (gate, channel, runtime), never by the acting Agent; Agents hold no write path to their own trails. Security-relevant logs are continuously hash-chained, each entry committing to its predecessor, with external anchoring at a declared short cadence, so tampering is detectable even by a compromised operator.

IC-7 Owner-gated reads, inward and outward. GOV-7 (internal access grants) and FED-3 (federation disclosure) are the two faces of one consent discipline: a read right exists only as an Owner-granted, purpose-bound, TTL-bounded grant recorded in a grant register, whether the reader is a domestic Agent or a federated peer. Grants are Semantic Contracts; auto-issued grants cite the version of the Owner-approved standing consent policy that produced them; QSC-6 diffs actual grants against register plus policy; revocation propagates within a bounded TTL per IC-5.

IC-8 Append-only history. The model may change its mind, but it never loses its memory: supersession, not deletion, per Lifecycle 13 and the canonical state vocabulary. Refused intents, failed actuations, corrected records and retired entries stay on the timeline as superseded history with identity and provenance intact; MIR-9 archival makes every actualization non-destructive, and every transition Event carries its reason code.

## 5. Quarantine and trust-state glossary

Three distinct states share a family resemblance and SHALL NOT be conflated. Each family overview carries this glossary in one line; the definitions live here:

- quarantine: MIR-8's readable-but-flagged trust marking (also surfaced as the MIR-6 freshness state). Quarantined content remains readable; the flag travels with every citation; consumers are told to distrust it accurately.
- admission quarantine: FED-8's inbound holding zone for federated content. Held content is unreadable by the model until promoted; MIR-2's federated variant executes only the post-promotion landing, and a gateway refuses ingest of federated-class content without a promotion record.
- integrity hold: QSC-9's marker for content whose integrity is in question. Held content is excluded from answering and publication until cleared.

freshness_state is a declared palette extension of the Mastership Register schema, distinct from the canonical status enum. Trust state and flow state are independent axes and MAY co-exist on the same entry: a dataset can be active in flow and quarantined in trust at the same time, and both facts are visible at read time.

## 6. Conformance profiles

Three conformance profiles exist (C22, C37). A model declares exactly one.

- Full: every process of every applicable family at its stated tier, full artifact separation everywhere, all recertification loops run individually. Intended for federating, multi-steward, high-consumer-count models.
- Standard: all core processes plus the recommended processes applicable to the model's declared scope; consolidation of mechanical steps MAY follow the Solo/Minimal clauses below where a single Steward is accountable for all the consolidated registers.
- Solo/Minimal: the normative profile for a model operated by one Owner-Steward. It is a lawful conformance target, not a degraded mode.

The Solo/Minimal profile consists of three consolidation clauses:

1. Consolidated quarterly review. One consolidated quarterly review lawfully satisfies the recertification steps of MIR-1, MIR-6, MIR-9, ACT-1, ACT-3, CON-10, CTX-9, QSC-6 and QSC-11 that fall due in the window, executed as the generic register-recertification pattern of section 8 run once across all registers, and thereby satisfying the eight recertification loops that pattern names. Evidence is one combined report plus per-register Events.
2. Combined weekly sweep. One weekly agent-run sweep lawfully satisfies the mechanical steps of MIR-3, MIR-7, QSC-2 and QSC-9, with one combined Event as evidence. Escalations and findings still route individually to their owning processes.
3. Composite actuation event. For T1 actions where decider, dispatcher and executor are the same human, one composite actuation event (intent, decision, command, verification note) satisfies ACT-5, ACT-6, ACT-7 and ACT-9, and the idempotency key and the command-decision hash check are waived. Full artifact separation stays mandatory for all T2/T3 delegated actuation without exception.

The solo core set is recomputed under this profile, applying the charter demotions and promotions:

- ACT-1, ACT-2 and ACT-4 are recommended, not core; the signal catalog is mandatory only where delegated actuation (any T2/T3 decision) exists, and a standing pre-registered owner-directive signal class covers novel T1 human-initiated actions without per-idea cataloging ceremony.
- QSC-1 is recommended, core only above a declared size or consumer-count threshold.
- QSC-10 is core for any model that publishes or federates; otherwise recommended.
- CON-11 is core: it is the sole capture and classification path for intended external edits, triggered by MIR-7 drift Events.
- ACT-12 is core wherever any ACT process runs at T3 or any emergency actuation class is declared; otherwise recommended.

Each family restates its resulting core set in its own overview. Core is a statement of capability, not of calendar load: most core processes are event-driven and run only when their trigger occurs (a correction, a quarantine, an incident, a retirement). What bounds the solo operator is standing obligations, and under this profile they SHALL reduce to exactly three: the weekly combined sweep, the quarterly consolidated review, and the declared continuous monitors of the model's registers. Any palette change that would add a fourth standing obligation to the Solo/Minimal profile is a palette change requiring re-adjudication, not a family-local edit.

## 7. Editorial fast lane

This clause is normative and cross-family. For changes classified editorial or corrective under a declared size threshold, one T3 agent pipeline MAY execute intake, provenance capture, gate checks, auto-approval, versioning and reason stamping end to end, and emit ONE composite Event. That single Event is conformant evidence for CON-1, CON-2, CON-3, CON-4 and CON-6, for MIR-10 reason stamping, and for the CTX-5 execution record. The lane classifier is the mechanical diff-based classifier of the auto-approval control (a GOV-2 owned gate config): classification consumed by the lane gateway SHALL NOT originate from the submitting agent or its orchestrator, and any change touching normative keywords, schemas, identities, register entries, contracts or any security-critical dataset (IC-4) is structurally ineligible regardless of proposed classification. Classification-versus-diff mismatches are logged as findings.

## 8. The register-recertification pattern

One generic pattern covers all periodic recertification of register entries, stated here once and invoked by reference everywhere else:

1. Enumerate the register's entries.
2. Check each entry's age and actual usage against the declared thresholds.
3. Re-approve, amend or retire each entry by the declared approver's decision.
4. Record the outcome as a versioned Event per register.

The pattern is parameterized by register, thresholds and approver. The eight recertification loops of the palette (ACT-1.7, ACT-3.7, CON-10.7, CTX-9.8, FED-3.8, MIR-6.7, the MIR-10 taxonomy review, QSC-6.6) invoke this pattern by reference and add only their register-specific parameters; they do not restate the mechanics. Under the Solo/Minimal profile the pattern runs once per quarter across all registers per section 6, clause 1.

## 9. Shipped defaults

No gateway in the palette may be undecidable at install time. Every gateway predicate is a versioned GOV-2 configuration artifact with a shipped default: a model is conformant from day one by adopting the defaults, and every departure from a default is a versioned, approved GOV-2 change, never an in-place edit. The named shipped defaults are:

- Impact Matrix (cited as a required input by every ACT card): impact classes low, medium and high crossed with reversibility classes reversible, compensable and irreversible; default floors: assessment floor medium, rollback-plan floor medium, separation-of-duties and independent-evidence floor high; solo default: everything reversible and in-scope is below the floor.
- FED-8 floors: default promotion and operating floors expressed as Trust Vector predicates over named trust dimensions, never as scalar scores.
- ACT-2 correlation window: same signal class and same subject within the class's declared cadence.
- ACT-4 assessment schema: the minimal value, cost and risk output schema; the ACT-9 verification record lists the observed affected set in the same schema.
- MIR-4 semantic order: source sequence number, falling back to occurrence time.
- CTX-1 selection rules: anchors plus 1-hop declared relationships plus cited constraints; selection-rule authoring is a named Steward step that starts from this default set.

A model that has changed none of these runs entirely on shipped defaults and SHALL declare so in its manifest; a model that has changed any of them cites the GOV-2 config versions in force.

## 10. Citation discipline

Family texts cite this law as COMMON with a section number (for example: tiers per COMMON 3, IC-3 per COMMON 4). Canon citations use the canon document name and section (Contract.md 5-6, Federation-Contracts.md 3a, Data-Mastership 6, Data-Mastership 7, Lifecycle 13, Trust-Model.md 6a-7, Consent-and-Disclosure 12, Conflict-Resolution 4a). Record time and effect time are introduced in the palette as intent bitemporality, a palette concept without a canon citation, expressed through the Version Lifecycle (Draft and Proposed versus Active) plus Event timestamps. References to the Meta-Orchestrator State point to the external reference Dimension repository, not to the standard.
