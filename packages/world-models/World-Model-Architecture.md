# World Model Architecture: the broad-coverage meta-model catalogue

> **Status:** DRAFT v0.2 (breadth-first pass + second gap pass, 2026-07-31). Companion register: [`world-models.csv`](./world-models.csv).
> **Published by the Vercy project** as the architecture of its example world-model library: the set of meta-models sufficient to describe, at instance level, the human world and what happens on planet Earth. The Meta-Orchestrator State (MOS) is the reference Dimension consuming this library and appears throughout as the running example; any Dimension can rebind the doctrine anchors to its own canon.
> **Relation to the core:** [`meta-models.csv`](./meta-models.csv) (38 models, clusters V/A/B/C/D/E) remains the **governance kernel** of the reference Dimension. This document extends it into a **world-coverage catalogue**. The goal of this pass is **breadth, not detail**: every model here is a named, owned, one-line-scoped namespace; full specification comes later, model by model, on demand.

---

## 1. Purpose and stance

The reference Dimension (MOS) models a polity as one Meta-Universe Dimension: Namespaces = meta-models, Objects = instances, Events on a Semantic Timeline. The governance kernel covers the state, society and the value substrate. But a state governs a *world*: land and rivers, buildings and grain, machines and software, actions and accidents, companies and contracts. To sense value flows across that world, the world itself must be representable.

Three commitments shape this catalogue:

1. **Breadth first.** 145 meta-models across 16 clusters, each scoped in one line. It is far cheaper to split or deepen a model later than to discover a missing continent of reality.
2. **Assembly, not authorship.** Nearly every cluster binds existing external standards (GS1, IFC, FHIR, CIM, DCAT, W3C ORG, ISO suites...) via the Meta-Universe composition rules; MOS models the *delta* (value semantics, ownership, governance hooks).
3. **Ownership and access are architecture, not policy.** Every meta-object has exactly one controlling meta-object (its owner), and **nothing is readable without the owner's permission**. Security is a first-class cluster (S), and its rules bind every other cluster (§5, §6).

## 2. The cluster map

| Cluster | Scope | Status |
|---------|-------|--------|
| **V. Value Substrate** | value transformers, Æ-vector, flows, anti-value, frames | core (exists) |
| **A. Polity** | charter, constitution, branches, ministries, law, courts, rights + lawmaking/voting, offices, registry mandates, elections, permits, treaties, borders, defense, enforcement | core + A10-A18 |
| **B. Society** | citizens, roles, families, reputation, needs, parties, experts + health, property, life events, benefits, public health | core + B10-B14 |
| **C. Economy** | business, markets, work, settlement, routing + prices, insurance | core + C7-C8 |
| **D. Civilization** | missions, science, culture, ecology-as-value + sport, religion, tourism, discourse, norms | core + D5-D9 |
| **E. Runtime** | agent-citizens, sim time, observation, control | core (exists) |
| **P. Planet & Nature** | terrain, land, water, weather, subsurface, flora, fauna, hazards, space | new (11) |
| **M. Matter & Artifacts** | materials, items, goods, food, medicines, machines, vehicles, devices | new (9) |
| **U. Built Environment** | buildings, premises, physical networks, settlements, utilities, works, addresses | new (7) |
| **K. Activity & Work** | functions, acts, processes, services, projects, methods, plans + manufacturing, agriculture, extraction, maintenance, care delivery | new (12) |
| **N. Knowledge & Information** | documents, reports, datasets, software, media, models, messages, identifiers + language, statistics, calendars, IP | new (12) |
| **O. Organizations** | organizations, units, membership, mandates, commercial contracts + labor market, procurement | new (7) |
| **R. Registries & Ledgers** | the registry pattern, ledgers, event registers, identity, attestations | new (6) |
| **F. Flows & Resources** | energy, money, logistics, supply, waste, emissions + transit, financial instruments, communications | new (9) |
| **X. Events & Phenomena** | occurrences, phenomena, incidents, situations, interactions | new (5) |
| **S. Security, Ownership & Access** | ownership graph, access contracts, disclosure, audit, aggregation, ZK, enforcement + cyber integrity | new (8) |

Full per-model tables are in [`world-models.csv`](./world-models.csv); the sections below give each cluster's intent, owner archetypes and the highest-signal models.

## 3. The clusters

### P. Planet & Nature

The physical substrate that exists whether or not anyone governs it: terrain and landforms, cadastral land parcels, water bodies and hydrology, atmosphere/weather/climate, subsurface and mineral resources, soil and agricultural land, flora, fauna, ecosystems, and natural phenomena/hazards. D4 (ecology as a *value* dimension) keeps its role; P models the physical referents those values are about.

*Owner archetypes:* nature has no owner in the property sense at the model level: P namespaces are stewarded by **commons stewards** (the Ecology and Territory sub-agents), consistent with the commons doctrine in [Property, Rent and the Commons](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Property-Rent-and-Commons.md). Parcel-level *rights* over land and subsoil are not stored here; they are S1-ownership records referencing P2/P5 objects.

*Bind:* GeoSPARQL/INSPIRE, ISO 19152 LADM (cadastre), GeoSciML/UNFC (subsurface), CF/WMO (climate), Darwin Core (species), ENVO/SWEET (ecosystems), CAP/EM-DAT (hazards).

### M. Matter & Artifacts

Everything made or extracted that can be held: materials and substances, generic physical items, tradable goods, food and drink, medicines, equipment and machinery, vehicles, devices/sensors/computing hardware, cultural artifacts. The line between M2 (item) and M3 (good) is market-facing: a good is an item in its tradable aspect (GS1-classified, priced); the same instance can appear in both aspects by reference.

*Owner archetypes:* the item's owner per S1 (person, organization, commons). The *class-level* models are stewarded by the Economy sub-agent; instance data belongs to whoever holds the thing.

*Bind:* GS1 GPC/GTIN, FoodOn/INFOODS, ATC/RxNorm, eCl@ss, SSN/SOSA (devices), CIDOC-CRM (heritage), CAS/ChEBI (substances).

### U. Built Environment

Buildings and structures, premises and spatial units, physical infrastructure networks (roads, rail, pipes, grids), settlement/urban form, utility service points, construction works in progress. C4 (infrastructure as economic capacity) references U for the physical inventory.

*Owner archetypes:* building/premise owners per S1; network infrastructure typically organization- or state-owned; the Urban/Territory sub-agent stewards the class models and the settlement fabric.

*Bind:* IFC, CityGML, INSPIRE transport networks, IEC CIM (grid).

### K. Activity & Work

What agents *do*: functions and capabilities (what an agent can do), acts (atomic actions: who did what, to what, when, where), processes and workflows, services (defined offerings and their delivery), projects, methods and procedures, plans and schedules. K2 (Act) is the hinge of the whole world model: almost every Event (X1) is the trace of an Act, and almost every Value Flow (V3) is priced over one.

*Owner archetypes:* the acting agent owns the act record it performs; service definitions belong to their providers; projects to their sponsoring organizations.

*Bind:* BPMN (processes), CPSV/schema:Service, PROV (attribution), iCalendar (schedules).

K2 (Act) and X1 (Occurrence) are deepened together in [`Actions-and-Events.md`](models/Actions-and-Events.md) (v0.1, K2/X1 rows promoted to `draft`): the act is a specialization of the occurrence, both resting on the S and R machinery.

### N. Knowledge & Information

Documents and records, reports and statements, datasets and data registers, **software products and systems** (bound to AISMM: a software product's full-context model plugs in here as-is), media and creative works, models-and-ontologies as first-class objects (this catalogue itself is an N6 instance), messages and communications, identifier/naming systems.

*Owner archetypes:* authors and publishing organizations; the Knowledge sub-agent stewards class models and the identifier systems.

*Bind:* Dublin Core, XBRL (financial reports), DCAT (datasets), AISMM (software), schema:CreativeWork, the Meta-Universe standard itself (N6).

### O. Organizations

Generalizes C1 beyond businesses: any organization (company, cooperative, NGO, religious community, association, institution), organizational units, employment and membership, organizational mandates/charters, and commercial contracts between parties. Ministries (A3) are organizations too: A3 EXTENDS O1 with the public mandate.

*Owner archetypes:* the organization itself (acting through its authorized officers per S1 delegation); the commercial register (R1 instance) is stewarded by the Registry sub-agent.

*Bind:* W3C ORG, LEI, NACE/ISIC, ESCO (employment), UNCITRAL texts (contracts).

### R. Registries & Ledgers

The system-of-record layer, made generic: **R1 Registry** is the reusable pattern (what may be registered, by whom, on what evidence, with what legal effect) that every concrete register instantiates (land register, commercial register, civil register, vehicle register...). R2 Ledger holds append-only accounts (the Æ-ledger and the $ rail are its two great instances). R3 Event Register stores Semantic-Timeline events per domain. R4 Identity Register anchors persons/organizations/things. R5 Attestations, certificates and licenses. R6 the federation/mirroring rules between registries (reference, never copy).

*Owner archetypes:* each register has a **registrar** meta-object (usually a state sub-agent or licensed organization); the *entries* remain referenced to their subjects, whose S-cluster rights still gate disclosure.

*Bind:* ISO 20022 (accounts), W3C DID (identity), W3C Verifiable Credentials (attestations), Meta-Universe registry doctrine.

R1 and R2 are deepened in [`Registry-and-Ledger.md`](models/Registry-and-Ledger.md) (v0.1, R rows promoted to `draft`).

### F. Flows & Resources

The moving quantities: energy (carriers, generation, consumption, grid balance), money and monetary instruments (the $ side of the two-layer system; Æ stays in V), goods movement and logistics, water and food supply chains, waste and circular flows, emissions and environmental flux. F models are where physical flows meet V3 value flows: every F flow MAY carry an Æ-delta annotation.

*Owner archetypes:* flow records belong to the parties of the flow; grid/network aggregates to their operators; the Economy and Ecology sub-agents steward class models.

*Bind:* IEC CIM (energy), ISO 4217/20022 (money), UN/CEFACT + EPCIS (logistics), GHG Protocol (emissions).

### X. Events & Phenomena

The generic occurrence layer: X1 Occurrence (what happened: time, place, participants, causal links) specializing the Meta-Universe Event for the world model; X2 Observed Phenomenon (recurring natural or social patterns: a drought, a migration wave, an inflation episode); X3 Incident and Emergency; X4 Situation (a condition holding over an interval: a state of repair, an epidemic status); X5 Interaction (meetings, transactions, encounters between agents). Every other cluster's state changes are recorded as X1 events in the owning R3 register.

*Owner archetypes:* the event's primary actor or the observing registrar; emergencies to the Emergency sub-agent.

*Bind:* Meta-Universe Event, OWL-Time, CAP.

### S. Security, Ownership & Access

The cluster the rest of the catalogue depends on. Sections 5 and 6 below remain the summary; the full deep specification (S1-S8, adversarially hardened) is [`Security-Ownership-and-Access.md`](models/Security-Ownership-and-Access.md), which governs on conflict.

### The second gap pass (v0.2): the unnamed necessities

A systematic sweep for what the first pass and the original brief both missed. Thirty additions, by the hole they close:

- **Rule of law has verbs, not just nouns.** A5 held laws-in-force; now **A13 Elections** (choosing officeholders, distinct from A10 legislative voting), **A14 Permits and Authorizations** (the application-to-grant machinery behind every regulated activity), and **A18 Offense, Investigation and Enforcement** (crimes, cases, penalties, corrections: the largest single omission of pass one; deepened in [`Offense-and-Enforcement.md`](models/Offense-and-Enforcement.md), A18 row `draft`) complete the loop from choosing rulers to enforcing rules.
- **The polity has an outside.** **A15 Interstate Relations and Treaties** (federation between polities: MUFP applied to states) and **A16 Border, Customs and Migration**; **A17 Defense** enters as a breadth placeholder (detail stays in the G3 backlog).
- **The economy produces before it trades.** **K8 Manufacturing**, **K9 Agriculture and Husbandry**, **K10 Extraction Operations** (the *operation* over a P5 deposit, under an S1 commons grant, with restoration duties) and **K11 Maintenance** (the quiet half of every asset's life). **K12 Health Care Delivery** gives B10 (personal health) its system side.
- **Finance is more than money.** **F8 Credit, Debt and Financial Instruments** (loans, bonds, equity, collateral: F2 held only money itself); **C7/C8 already covered prices and insurance.**
- **Movement of people, not only goods.** **F7 Passenger Mobility and Transit**; and the invisible infrastructure everything else rides on: **F9 Communications and Data Transmission** (spectrum as an S1 commons grant).
- **Civil society exists.** **D5 Sport and Recreation**, **D6 Religion and Belief Institutions** (self-owned, strong S defaults), **D7 Tourism and Hospitality**, **D8 Public Discourse and Opinion** (ties to the epistemic axis and B8), **D9 Social Norms and Customs**: the informal "rules" the original brief asked for that are not laws.
- **Reference systems people forget until they break.** **N9 Language and Terminology**, **N10 Official Statistics and Census** (S5-bound by construction), **N11 Time and Calendar** (time zones, holidays), **N12 Intellectual Property**, **U7 Addresses and Location References**, **P11 Space and Orbital Objects**.
- **Work about work.** **O6 Labor Market and Vacancies**, **O7 Procurement and Tendering** (public tenders A12-registered by default).
- **Security of systems, not only of data.** **S8 Cyber Integrity** (vulnerabilities and incidents of N4 software and M8 devices: S1-S7 govern *who may read*; S8 governs *whether the substrate itself is sound*).

Deliberately still out: taxation (MOS replaces it by design), sub-object detail everywhere, and military depth (G3).

### The canonical meta-object roster

Meta-models are classes; the polity also needs its named **singleton meta-objects**: the concrete owners and stewards the S1 graph bottoms out in. The roster (each is an O1/A3 object with an A-cluster mandate):

| Meta-object | Controls / stewards |
|---|---|
| **The Polity** (root) | the Dimension itself; the Charter and constitution (A0/A1) |
| **The Legislature** | A10 lawmaking, A5 laws |
| **The Courts** | A6 cases, judicial S2 access contracts, S7 breach adjudication |
| **The Meta-Orchestrator** (coordinator, not sovereign) | E4 control policies, the balancing loop |
| **State Sub-Agents** (Demography, Science, Cognitive, Infrastructure, Ecology, Territory, Urban, Economy, Health, Social, Knowledge, Energy, Space, Emergency, Foreign Affairs, Border, Defense, Enforcement) | their value axis + the clusters marked to them in §3 |
| **The Statistics Steward** | N10, S5 aggregation (independent by mandate, S5-bound by construction) |
| **The Registrar-General** and per-domain registrars (land, civil, commercial, vehicles, identity, IP, elections) | R1 instances under A12 mandates |
| **The Ledger Operator** (Æ) and **Settlement Rail Operator** ($) | R2 instances |
| **The Audit Registrar** | S4 access logs (reads everything about reads, nothing about content) |
| **The CERT Steward** | S8 coordination |
| **Commons Stewards** | P-cluster nature, spectrum (F9), orbital slots (P11) |
| **Every citizen** (B1) | their personal namespaces: the most numerous sovereigns in the system |
| **Every organization** (O1) | its own namespaces, through officers |

The roster is itself data: an R1 register of mandates, so "who stewards what" is a query, never lore.

### Extensions to existing clusters

- **A10 Lawmaking & Legislative Voting**: bill, draft versions, readings, amendments, the vote itself (ballots, quorum, weights per the voting doctrine), enactment and entry into force. Closes the loop between B7 (parties/delegation) and A5 (law-in-force): a law is the *output event* of an A10 process. Bind: Akoma Ntoso (bills), the MOS voting mechanics.
- **A11 Public Office & Officials**: offices as positions (mandate, term, powers, accountability), officeholders (the official-agents), appointment/dismissal events, conflict-of-interest declarations. A11 objects are B1/B2 persons in O1 organizations holding A-cluster mandates: pure composition.
- **A12 State Registry Mandates**: which registers the state is obliged to keep, under which registrar, with what guarantees: the constitutional shell around R1 instances.
- **B10 Personal Health**: health status, encounters, conditions (FHIR-bound). The single most access-sensitive namespace in the catalogue; owner: the person, always.
- **B11 Personal Property & Assets**: the person-side view of S1 ownership over M/U/F objects.
- **B12 Life Events & Civil Status**: birth, marriage, divorce, death; the civil register (R1 instance) records them, the person owns them.
- **C7 Price, Valuation & Appraisal**: price observations, appraisals, indices; the bridge between market clearing (C2) and value measurement (V2).
- **C8 Insurance & Risk Pooling**: policies, pools, claims; a value-routing mechanism the settlement doctrine needs.

## 4. Interaction rules between meta-models

Six rules govern how the ~115 namespaces compose. They apply the Meta-Universe composition standard (ARCH-016) with MOS-specific defaults.

**Rule 1: the substrate mixes into everything.** V1-V5 are foundational: every domain object IS a value transformer (V1 MIX-IN), every flow MAY carry an Æ-delta (V3), every harm is bookable as anti-value (V4), every perspective is a frame (V5). No domain model redefines value semantics; they annotate with them.

**Rule 2: cross-owner links are references, always.** Within one owner's namespace, part-of relations MAY EMBED (a building embeds its premises if one owner holds both). Across owners: REFERENCE only. Copying another owner's data into your namespace is not integration, it is theft-shaped drift; the lawful alternative is a projection under an S2 contract.

**Rule 3: snapshots at contract boundaries.** When an interaction must freeze state (the address at delivery time, the price at sale time), a snapshot is lawful and REQUIRED to be marked as such (source reference + as-of time). Snapshots are evidence, not living data.

**Rule 4: every state change is an event.** Any mutation in any namespace appends an X1 event to the owning R3 register: actor, object, time, prior/new state reference. Registers are append-only; corrections are new events. This is what makes the world model auditable and the courts' contemporaneous-norms doctrine executable.

**Rule 5: dependency flows one way.** Physical clusters (P, M, U) do not depend on anyone. K acts (by B/O/A agents) act *on* the physical and *emit* X events *into* R registers, are described *in* N artifacts, valued *by* V, governed *by* A, and gated *by* S. A model lower in this chain never imports semantics from higher up; it is referenced by them. S and V are cross-cutting: they bind all clusters but define no domain objects themselves.

**Rule 6: external standards enter once.** Each external standard is imported as one Semantic Package with one mapping, stewarded by the cluster's steward; domain models reference the import. Two models binding the same standard independently is a defect (two drifting copies of schema.org is how meaning dies).

## 5. Ownership: the meta-object system

**S1 (Ownership & Stewardship) is the root of authority.** Its rules:

1. **Every meta-object has exactly one controlling meta-object**: its *owner* (or *steward* for commons). Ownership is itself data: an S1 record with full history; transfers, delegations and inheritance are events.
2. **Persons self-own.** A citizen (B1) is the controlling meta-object of their own personal namespaces (B10 health, B12 life events, their K2 acts, their side of X5 interactions). Guardianship (minors, incapacity) is an explicit, bounded, auditable S1 delegation, never a silent default.
3. **Organizations own through officers.** An O1 organization controls its namespaces; natural persons act for it under S1 delegations bound to A11/O2 positions (the officer acts *as* the office, and the audit trail records both).
4. **The commons are stewarded, not owned.** P-cluster nature objects have stewards with duties (maintain, disclose aggregates, prevent harm) rather than owners with exclusion rights; extraction rights over commons are separate, explicit, rent-bearing S1 grants per the property doctrine.
5. **Registrars hold registers, not the registered.** The land registrar controls the land register (R1 instance) as a data structure; the *entries'* disclosure still follows the subjects' S2 rights, except where A12 mandates public faith (and then the mandate, not the registrar's whim, defines the public projection).
6. **Ownership of a meta-model (the class) is stewardship of its schema**: the steward evolves the model's definition under the Meta-Universe versioning rules; instance owners are unaffected in their data rights by schema stewardship.

## 6. Security: nothing is readable without the owner

The user-facing rule is one sentence: **information from any meta-model can be read only with the permission of its owner: the meta-object that controls it.** The architecture behind it:

1. **Default deny.** There are no world-readable namespaces by default. Absence of a grant is a denial, for every reader including the state.
2. **Reads are projections under access contracts (S2 + S3).** A grant is a machine-readable Access Contract issued by the controlling meta-object: to whom, over what scope, in what shape, until when, revocable how. Data leaves only as a Projection in the contracted shape: field subset, summary, or aggregate: never as a raw namespace dump. Data minimization is structural, not aspirational.
3. **The state sees cohorts, not persons (S5).** Governance sensing (the imbalance signal, corridor monitoring) consumes cohort-aggregated projections with a k-anonymity floor; per-person reads by any state organ require either the person's consent or a judicial access contract issued through due process (itself an auditable S2 object referencing the court's A6 case). This encodes the sensing-vs-coercion synthesis: rich vision at cohort grain, hard limits at person grain.
4. **Every read is an event (S4).** Access is logged append-only: who read what projection of whose data under which contract, when. The owner can always answer "who has looked at my data": disclosure of reads to the owner is itself a right, not a feature.
5. **Prove without revealing (S6).** Where a consumer needs only a predicate (over 18; solvent; licensed; emissions under quota), zero-knowledge attestation is the preferred projection shape: the fact is verified, the data never moves.
6. **Violations are anti-value with teeth (S7).** Unauthorized reads, scope creep and contract breaches book V4 anti-value against the violator, trigger the enforcement ladder (annotation, restriction, standing loss, prosecution for rights violations per the Charter), and are adjudicable in courts under the contemporaneous norms of the access contract. Security failures are not incidents to be managed; they are value events to be paid for.
7. **Emergency access is narrow and loud.** Life-safety overrides (X3 emergencies) exist, are bounded by A-cluster law, and produce the loudest audit events of all: reviewed after the fact, compensated when wrongly used.

## 7. Relation to the Meta-Universe standard

Every model in this catalogue is a Namespace of the MOS Dimension and is expected, as it matures, to become an ARCH-017-conformant package (manifest, classification, coverage) with an ARCH-018 mastership register (most world registers are model-mastered; external scientific/standards feeds are declared mirrors). Composition follows ARCH-016; access machinery (S2/S3/S6) instantiates the standard's Contract, Consent-and-Disclosure and Zero-Knowledge-Attestation documents; R6 instantiates the registry federation doctrine. Nothing here invents new machinery; it applies the standard at world scale.

## 8. Status and next steps

- v0.1: 77 new models named and scoped. v0.2 (gap pass): **+30 more, 107 new + 38 core = 145 total**, plus the canonical meta-object roster. All new entries carry `status: candidate` in the register.
- **Deepened so far** (v0.1 each): [`Security-Ownership-and-Access.md`](models/Security-Ownership-and-Access.md) (S), [`Registry-and-Ledger.md`](models/Registry-and-Ledger.md) (R1/R2), [`Actions-and-Events.md`](models/Actions-and-Events.md) (K2/X1, the world's verbs), [`Offense-and-Enforcement.md`](models/Offense-and-Enforcement.md) (A18, the sharpest rights surface), [`Property-and-Ownership.md`](models/Property-and-Ownership.md) (P2/M3/U1/F8, the property-bearing nouns), [`Civic-Health-and-Democracy.md`](models/Civic-Health-and-Democracy.md) (B10/A10/A13, the civic layer), [`Economy-and-Markets.md`](models/Economy-and-Markets.md) (C1/K8/C2, the economy-production layer; K8 row promoted to `draft` in `world-models.csv`, and C1/C2 are core-kernel models in `meta-models.csv` now covered by this spec). World-coverage rows are promoted to `draft` as each is deepened; core-kernel models (C1, C2) keep their `Formalize`/`Priority` flags in the kernel register. Next passes (on demand, by priority): the flows layer (F1 energy, F3 logistics, F6 emissions), then the civilization layer (D1 missions, D2 science, D4 ecology).
- Deliberate omissions at this stage: taxation (replaced by value balancing, by design), military/defense detail (G3 backlog; A17 is a breadth placeholder), and anything at sub-object granularity (fields and attributes come with per-model specs).
