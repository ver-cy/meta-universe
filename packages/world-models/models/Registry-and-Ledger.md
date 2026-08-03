# Registry and Ledger: the R1 and R2 specification

> **Status:** DRAFT v0.1 (2026-07-31). Deepens R1 (the registry pattern) and R2 (the ledger) of the [World Model Architecture](../World-Model-Architecture.md). Register rows: R1, R2 in [`world-models.csv`](../world-models.csv). Presupposes and reuses the [Security, Ownership and Access spec](./Security-Ownership-and-Access.md) (the S cluster) throughout; on conflict with the summary in the architecture document, this document governs for R1 and R2.
> **Provenance:** six parallel specifiers (R1 core, operations, assurance; R2 core, integrity, access), then five adversarial reviews (a financial-systems attacker, a registry-law red team, the doctrine keeper, a systems pragmatist, a privacy-and-access reviewer: 60 findings, 26 critical), then one revision pass under a 36-point resolution charter that keeps the six sections mutually consistent. The findings shaped every section; the surviving open questions are honest.

---

## 0. How R1 and R2 fit together

R1 and R2 are the polity's system-of-record layer, and both are built on the same S-cluster machinery: the owner-side gate commit, witnessed anchored roots, inclusion promises, S2 access contracts, the S5 release register. Nothing here reinvents integrity or access; it applies the S spec to two shapes.

**R1 is the registry pattern.** Every concrete register (land, civil, commercial, vehicles, identity, IP, elections) instantiates it. A register never holds the world, it holds attested claims about the world, each with a declared legal effect, filed under an A12 mandate, appended forever. The three R1 sections cover: the primitives (register, entry, registrar; the one effect typology of constitutive / declaratory / probative with public_faith as an orthogonal projection attribute; sealed-commitment filing with witnessed received_at; single-subject sequencing that makes a second exclusive entry fail closed rather than become a contest); operations (fast-tier self-execution versus the gated synchronous gate; evidence authenticity as mandatory criteria; contest that sets a marker but never freezes disposition without a court order; correction, appeal, deemed referral with a mass-referral circuit breaker); and assurance (indefeasibility keyed to defect type not to the word fraud, funded only where a mandate names an assurance route; witnessed cross-signed roots with an independence floor; mirrors capped by the source mandate; catastrophic recovery as replica recovery, not reconstruction from hashes).

**R2 is the ledger.** Its two great instances are the sovereign AE-ledger (multidimensional value accounting, ten axes) and the thin $ settlement rail. The three R2 sections cover: the core (accounts and atomic balanced postings; AE that is booked and consumed but never handed holder-to-holder, physically sharded counter-accounts so the economy does not funnel through one sequencer; the AE/$ coupling that references a valuation without converting one into the other; consumption that fails closed on insufficient entitlement against the authoritative fold); integrity and settlement (finality classes with anti-structuring on the aggregate; externality escrow that tolls while any harm indicator is open and releases lazily; continuous anti-value debit; clawback that traces into transferees' hands under the concealment doctrine; revaluation that reopens flows both ways while clawback stays court-gated; witnessed balance checkpoints so post-summarization balances remain provable); and access (holders read their own accounts, counterparties read exactly their shared postings, the state reads nothing per-person without a judicial contract and senses only through S5 frames; solvency answered by parameter-blind zero-knowledge predicates; a cash-like rail tier that structurally omits stable identifiers below a threshold so the polity's transaction graph is not a standing honeypot).

Three commitments recur, matching the S cluster:

1. **Honest bounds, not fictional absolutes.** Reliance protection is capped by mandate ceilings and funded assurance; anchoring has a bounded cadence; balances are witnessed checkpoints plus a fold, not a genesis-to-now replay.
2. **Structural protection, not trusted restraint.** A second exclusive entry fails closed at append; sealed-commitment filing means a registrar cannot front-run what it has not yet seen; the ledger operator gets zero analytic privilege by construction.
3. **Both failure modes priced.** Default deny and public faith coexist with civil discovery, a single cross-register asset-discovery instrument, minimum public-faith content, and a tombstone remedy for adjudicated-false entries. A registry that only served reliance, or only served privacy, would be an accomplice of the other side.

The sections follow in order: R1 core, operations, assurance; then R2 core, integrity, access.

---
## R1 core: the register, the entry, the registrar

### Purpose

R1a fixes the primitives every registry relies on: what a register is, what an entry is, what the registrar may and may not do, and how a filing becomes an effect. It defines the polity-wide effect typology, the sealed filing path, single-subject sequencing, the evidence rules, public-faith projection, and register continuity. R1b (contest, correction, appeal) and R1c (reliance, mirrors, anchoring) build on these primitives and MUST NOT restate them.

### Object model

- **register**: a root-register entry carrying `mandate_ref` (exactly one A12 mandate), an exclusive `subject_class` scope, `tier`, `base_effect`, optional `public_faith_scope`, projection policy, sequencing shard map, and a `witness_set` reference.
- **entry / entry_event**: `subject_ref`, `filer_ref`, `evidence_refs[]`, `as_of`, witnessed `received_at`, `sequence_position`, `status` in {unvalidated, Active, superseded, void}, plus effect fields. Content is referenced, not copied (R1-R1).
- **base_effect**: ONE closed polity-wide enumeration, `base_effect` in {constitutive, declaratory, probative}. `public_faith` is an ORTHOGONAL projection-policy attribute (a boolean plus `field_scope`) on the A12 mandate, NOT a member of this enumeration. Every mandate SHALL declare `base_effect` plus an optional `public_faith_scope`. R1b and R1c reuse these exact terms.
- **filing**: a sealed hash commitment that receives a witness-attested `received_at` and a `sequence_position` BEFORE its content is revealed to the registrar.
- **refusal_record**: `failed_criterion_refs` (a set of published machine-checkable criteria); readable by the filer, A6, and the mandate supervisor only, and never projected.
- **contested marker**: a boolean plus a `case_reference` only; contestant identity, standing_basis, and evidence are case-scoped.
- **public_faith_projection**: the mandate-defined minimum field set per effect class (full specification in R1c).
- **access batch buffer**: a locally hash-chained log of projection reads, sealed into the register's segments on the anchoring cadence.

### Invariants

- **R1-I1** An entry is an event appended to a register; an appended event resolves to the controller of the register it was appended to (S1 derivation). Registers and entries are append-only.
- **R1-I2** No entry is deleted or mutated. Corrections and supersessions are new events linking the superseded version; superseded versions are retained forever and remain queryable subject to the tombstone rule of R1-P2. Integrity commitments and clawback provability are never impaired by projection changes.
- **R1-I3** Each register operates under exactly one `mandate_ref` that fixes its `subject_class` scope, `base_effect`, `public_faith_scope`, tier, projection policy, identity assurance levels, and evidence criteria. An election register holds an ordinary A12 mandate that incorporates its A13 constitutional calendar-compression and effect parameters by reference; it is not constituted by A13 directly.
- **R1-I4** The registrar is recorder, not adjudicator, and SHALL NOT weigh contested substance. Verification is capped at schema conformance, evidence presence and authenticity (R1-R1..R1-R5), filer identity and authority (R1-I8), and criterion-listed preconditions. Every refusal SHALL cite at least one published machine-checkable criterion, recorded in `failed_criterion_refs`.
- **R1-I5** Where a window lapses on registrar inaction, a per-filing deemed referral auto-instantiates to A6 on the expedited track. When deemed referrals from one registrar exceed a published per-window threshold, they consolidate into a single A6 supervisory case against the registrar; the underlying filings toll, with per-filing compensation liability still accruing, and are disposed in bulk under the supervisory order.
- **R1-I6** A register is fast tier or gated tier. A fast-tier entry self-executes at append but is marked `unvalidated` from append until asynchronous validation passes. Reliance on an unvalidated entry is unprotected against the entry's subject. Any acquisition inside the contest window, or from a filer whose entry has not yet been validated, is presumed bad faith, with the burden of rebuttal on the acquirer.
- **R1-I7** Public faith is a projection, not an effect. A12 (not the registrar and not the subject) defines a constitutionally reviewed minimum projection field set per effect class sufficient for the reliance that class grants (R1c). Reads of the projection log via batched hash-chained buffers sealed into the register's segments on the anchoring cadence, a sealed batch satisfies the logging duty, and caches SHALL emit their batch logs to the master; gated and contract-bound reads keep per-read synchronous access_events. Subject-side enumeration of projection reads shows only read count, reader class, and time bucket; reader identity is unmasked to the subject only after a delay window and never for reads that ripen into a judicial or enforcement instrument within it. Bulk-pattern projection access throttles or escalates to an S5-registered release or an A12 bulk-access license; cross-register joining of subject-identifying projection fields, and publication of scraped register-derived aggregates without S5 registration, are `over_collection` or `audit_evasion`. Registrar-side and mirror-side reads of the access_event corpus bind to intra_organ access contracts, are subject-enumerable, and any analytics over reader or subject metadata run only as S5-registered releases. Non-projection entry fields are readable only under an S2 contract issued by the register controller with the subject's `consent_record`: the A12 mandate materializes the subject as co-controller of that non-public field scope (an S1-I1 ownership_record deviation), so subject consent plus registrar gate execution are jointly required.
- **R1-I8** Each mandate fixes a per-entry-class identity assurance level. Every constitutive or disposition-class filing requires (a) proof of the filer's authority over the disposing subject as a precondition distinct from authentication, (b) second-channel confirmation from the currently registered right-holder, and (c) a published pre-effect notice interval before effect attaches. A filing on compromised disposing-party credentials is void ab initio (a C2(a) authority defect) and never attracts reliance protection at any tier.
- **R1-I9** Every `subject_ref` maps deterministically to exactly one sequencing shard with exactly one sequencer; conflicting filings for one subject sequence in a single total order. A second Active entry for an exclusive-claim class on another shard is void ab initio and FAILS CLOSED at append, never becoming a contest. Effects that span shards or registers use a `multi_leg_commit` equivalent.
- **R1-I10** Evidence is a live reference, not a copy (R1-R1), or a marked snapshot bounded by a per-event-class maximum age (R1-R2); authenticity, filing binding, and exclusivity are governed by R1-R3..R1-R5. `as_of` is a required field bounded by the mandate's snapshot-age ceiling, so an unbounded or stale `as_of` is inadmissible.
- **R1-I11** Each register is a root-register entry under an Active root entry; a register without an Active root entry confers no effect and SHALL NOT accept filings. Every root-entry event touching a register's existence (amendment, succession, retirement) carries the A12 instrument as evidence, is witness counter-signed, and observes a published pre-effect notice period. Retirement stops new filings only and never suspends the effect or queryability of existing entries. On registrar failure, refusal, or mandate lapse an interim custodian registrar auto-appoints (courts as default) so windows keep running and filings keep being accepted. The no-reopening rule does not bar review of a predecessor registrar's own entries.
- **R1-I12** Each root entry declares an exclusive `subject_class` scope; the root registrar refuses (with `refusal_record`) or refers to A6 any overlapping mandate. Where overlap already exists, the earlier root append position governs and the later register's conflicting entries carry declarative effect only until A6 resolves. Gated-tier intake runs an R6 cross-reference check, appending automatic contested markers to both entries and referring to A6 on a hit.

### R1 evidence rules

These named rules are the single definition of the reference-not-copy, snapshot, and authenticity obligations; cite them as R1-Rn and never as an unqualified "Rule n".

- **R1-R1 (reference, not copy)**: evidence is stored as a resolvable reference to its issuing register or source and re-resolves live at gate time.
- **R1-R2 (marked snapshot)**: where live resolution is impossible, a snapshot is admitted only if marked with source, `as_of`, and issuer signature, and only within the per-event-class maximum age; gated-tier filings require live re-resolution at gate time at the filer's cost.
- **R1-R3 (authenticity)**: every `evidence_ref` SHALL carry a valid issuer signature, the issuer's mandate Active at `as_of`, non-revoked at gate time, and an R4/R5 chain resolvable.
- **R1-R4 (filing binding)**: every `evidence_ref` SHALL carry a commitment binding the artifact to this `filing_id`, single-use, so a once-valid artifact cannot be replayed.
- **R1-R5 (exclusivity)**: where the entry class is exclusive, an `evidence_ref` is rejected if the same artifact already grounds an Active entry. A `forged_evidence` class voids the entry ab initio at any tier, with liability booked jointly against attester and filer. The accept event records each authenticity result.

### Protocols

- **R1-P1 Filing intake and append**: (1) the filer submits a sealed hash commitment; (2) a witness attests `received_at` and assigns a `sequence_position` before content is revealed; (3) content is revealed and the registrar checks schema, evidence (R1-R1..R1-R5), identity assurance and authority (R1-I8), and criterion-listed preconditions; (4) shard and exclusivity resolve per R1-I9, with a conflicting exclusive-claim filing failing closed; (5) the event appends. Append order SHALL equal attested `received_at` order; any deviation is provable equivocation and void as to priority. An unwitnessed `received_at` is inadmissible for priority, `criteria_version`, and norm-set determination. Fast-tier entries append as `unvalidated`; gated-tier entries pass the synchronous gate. The accept event records each authenticity result.
- **R1-P2 Correction and supersession**: an authorized-initiated or court-ordered correction appends a new event linking the superseded version, retained append-only. A court correction MAY, and on a finding of falsity or bad-faith filing SHALL, reduce the superseded version's public-faith projection to a tombstone (existence, supersession link, and correction reference only), with the full superseded content retained append-only and readable only under S2 contract, case standing, or court order. Integrity commitments and clawback provability are unaffected.
- **R1-P3 Projection read, logging, and discovery**: projection reads are served (caches permitted) with batched sealed access logs per R1-I7; subject enumeration is masked per R1-I7; bulk-pattern access is gated to S5 or an A12 bulk-access license. A single A6 asset-discovery instrument, on judgment or freezing-order standing, executes the subject-enumeration query across the root register's children and both R2 ledgers, returning entry references and encumbrance status under case scope, S4-logged and sealed from the debtor for a court-set window; this is the R1-specified judicial shape, so no individual register demands separate leave.
- **R1-P4 Register lifecycle events**: root-entry amendment, succession, and retirement execute per R1-I11, including interim custodian auto-appointment on failure, refusal, or mandate lapse.

### Lifecycle and edge cases

- (a) **Composite transactions across tiers**: the strictest tier governs, but "touches" means legs that change the status or content of a gated entry; reads, references, and `evidence_refs` never escalate tier. Tier-split execution is allowed: fast legs self-execute escrowed pending the gated leg and unwind automatically if the gate refuses, so the gated leg gates finality rather than serializing the whole transaction.
- (b) **Conflicting filings for one subject**: sequenced in a single total order per R1-I9; a second exclusive-claim Active entry fails closed at append and never becomes a contest.
- (c) **Registrar outage or refusal-flood**: deemed referrals toll and consolidate under the R1-I5 circuit breaker rather than flooding A6 with individual cases.
- (d) **Registrar vacancy or retirement**: an interim custodian auto-appoints; existing entries remain effective and queryable (R1-I11).
- (e) **False or superseded entries**: retained append-only; the public face reduces to a tombstone only on the court order of R1-P2.

### Interfaces

- **A12** mandates: effect class, projection policy, identity assurance, evidence criteria, snapshot-age ceilings, bulk-access licenses.
- **A6** adjudication: referrals, prima-facie orders, asset-discovery instruments, mandate-overlap resolution.
- **R4/R5** identity and attestation chains for R1-R3 authenticity and R1-I8 authority.
- **R6** mirrors and cross-reference checks (R1-I12); mirror reliance discipline is specified in R1c.
- **S1** controller derivation and the ownership_record co-control deviation of R1-I7.
- **S2** access contracts for non-projection fields; **S4** access logging; **S5** aggregate releases.

### External bindings

- **S2 template amendment (explicit)**: the S2-I18 `constitutional_standing_template` enumeration is extended, enacted at Charter level, with (d) a mandate-defined `public_faith_projection` service per register and (e) holder own-statement and own-account plenitude. For an entry's non-public field scope the A12 mandate materializes the subject as co-controller (an S1-I1 ownership_record deviation), so subject consent plus registrar gate execution are jointly required.

### Open questions

1. Calibration of the per-event-class maximum snapshot age (R1-R2) and allocation of live re-resolution cost across evidence classes.
2. Numeric thresholds for the R1-I5 mass-referral circuit breaker and the R1-I7 bulk-read gating quotas per register class.
3. Funding model for the interim custodian registrar and how it composes with the R1c mirror escrow and assurance-route sizing.
4. Length of the subject-side reader-identity unmasking delay window versus the enforcement-instrument ripening period (R1-I7).

## R1 operations: registration, contest, correction, appeal

### Purpose

R1b specifies register operations: how a filing is received and ordered, evaluated against enacted criteria, appended and validated, contested, corrected, and appealed. It fixes the ordering, evidence-authenticity, contest, and notice rules that make the reliance guarantees of R1a and R1c operable, while keeping the registrar a recorder and routing every merits and mens-rea question to A6. Effect classes referenced here use the polity-wide typology base_effect in {constitutive, declaratory, probative} with public_faith as an orthogonal projection-policy attribute (R1a, R1c).

### Object model

- filing: {filing_id, sealed_commitment, revealed_content, subject_ref, entry_class, evidence_refs}. A filing is a sealed hash commitment until reveal.
- received_stamp: {received_at, sequence_position, witness_refs}. received_at is witness-attested; sequence_position is assigned before reveal.
- criteria_version: an A12-enacted instrument carrying a machine-checkable predicate set, including evidence-authenticity predicates and the entry class's identity assurance level; appended as a root-register event, witness counter-signed, after a published pre-effect challenge window.
- refusal_record: {failed_criterion_refs (set), filer_ref}. Restricted readership (R1-I24).
- validation_status: unvalidated | validated | void.
- contest_marker: {public boolean, case_ref}. standing_basis, contestant identity, and evidence are case-scoped, not public.
- correction and supersession_link: link a new event to a retained, append-only superseded version; tombstone is the reduced public_faith projection of a superseded version.
- deemed_referral and supervisory_case: per-filing expedited referrals and their consolidated form.
- effective_notice: a per-party record of confirmed notice from which prejudicing windows run.

### Invariants

R1-I13. A register SHALL evaluate filings only against a versioned, machine-checkable criteria set enacted under its A12 mandate. A criteria version takes effect only as an A12-enacted instrument, appended as a root-register event carrying that instrument as evidence, witness counter-signed, after a published pre-effect challenge window. A6 reviews any challenged criterion on the expedited track for mandate-traceability, necessity, and non-discrimination; a criterion not traceable to a mandate-listed precondition is void, filings are evaluated as if it did not exist, and refusals citing it are per se registrar_abuse. The published criteria set for every evidence class SHALL include evidence authenticity: valid issuer signature, issuer mandate Active at as_of, non-revoked at gate time, R4/R5 chain resolvable, a per-event-class maximum snapshot age with live re-resolution for the gated tier, a commitment binding the artifact to this filing_id, and rejection where the class is exclusive and the same artifact already grounds an Active entry. A refusal SHALL cite at least one failed criterion, each a published machine-checkable criterion, recorded in refusal_record.failed_criterion_refs as a set. The accept event records each authenticity result. The registrar weighs no contested substance (recorder, not adjudicator).

R1-I14. Filings SHALL be submitted as sealed hash commitments that receive a witness-attested received_at and a sequence position before content is revealed to the registrar. Append order SHALL equal attested received_at order; any deviation is provable equivocation and void as to priority. An unwitnessed received_at is inadmissible for priority, criteria_version selection, and norm-set determination. received_at fixes the criteria_version and contemporaneous norm-set applied to the filing.

R1-I15. Reliance protection and indefeasibility are governed by R1-I29 keyed to defect type, not by the word fraud; this invariant states no independent fraud rule. A forged or unauthorized filing is void as against the procurer at every tier (an authority defect under R1-I29(a), with S1-I14 restitution); downstream good-faith protection follows the corrected R1-I29 and the funding condition of R1-I30. An entry is marked unvalidated from append until asynchronous validation passes. Reliance on an unvalidated entry is unprotected against the entry's subject, and any acquisition inside the contest window or from a filer whose entry has not yet validated is presumed bad faith, with the burden of rebuttal on the acquirer.

R1-I16. Standing to contest requires a conflicting registrable claim that is independently evidenced and pre-dates the contested entry; a claim manufactured by a self-executing fast-tier filing after the contested entry does not confer standing. Impersonation and forged-evidence contests are discovery-based and carry no window bar (R1-I21).

R1-I17. A correction SHALL be appended as a new event linked to the superseded version, which is retained append-only and remains queryable; integrity commitments and clawback provability are unaffected. A court-ordered correction MAY, and on a finding of falsity or bad-faith filing SHALL, reduce the superseded version's public_faith projection to a tombstone (existence, supersession link, and correction reference only), with the full superseded content readable thereafter only under an S2 contract, case standing, or court order. Subject-initiated correction is validated against the same published criteria as an original filing; where the disproof lies outside the schema the subject proceeds by contest under R1-P6.

R1-I18. Expiry of a filing's disposition window without resolution auto-instantiates a per-filing deemed referral to A6 on the expedited track. Where deemed referrals from one registrar within a published window exceed the mass-referral threshold, they consolidate into a single A6 supervisory case against the registrar; the underlying filings toll, the registrar's per-filing compensation liability accrues, and they are disposed in bulk under the supervisory order rather than as individual cases.

R1-I19. Filing a contest sets the contest marker only. A disposition freeze attaches solely on an A6 prima-facie order issued within a short published deadline; absent that order, disposition stays free. The holder MAY lift any freeze by substituting security. Further contests on the same entry consolidate into the open case and generate no fresh freeze.

R1-I20. Bulk operations SHALL decompose into per-entry appended events only where legal effect changes. A purely representational migration MAY append one witnessed bulk event carrying the deterministic mapping function; per-entry alias resolution and re-encoding are computed lazily from the mapping. From plan activation, old keys resolve via the mapping and entries are servable in both schemas until the plan's completion event.

R1-I21. Any window that can prejudice a party (contest, appeal, marker lapse) begins at that party's confirmed effective notice, not at append, and tolls to a long outer limit where delivery is unconfirmed and non-delivery is logged. Impersonation and forged-evidence contests run from discovery with no window bar. Reliance acquired after a filing but before effective notice to the prejudiced party is voidable prospectively at minimum, with the loss routed under R1-I30.

R1-I22. A registrar dismissal of a contest settles the bond as refundable by default. The knowingly-baseless classification, bond forfeiture, and any V4 anti-value or TrackRecord booking require an A6 finding, or an uncontested S7 provisional booking under S7 Protocol 1 with full appeal rights, never a registrar verdict, preserving R1-I4.

R1-I23. The registrar SHALL notify every party whose position a filing changes, before effect where the entry class's A12-fixed identity assurance level mandates a pre-effect notice interval (constitutive and disposition classes). Undeliverable notice routes to the party's registered fallback channel with non-delivery logged; unconfirmed delivery tolls that party's windows under R1-I21. Notices appear in each recipient's enumeration.

R1-I24. Each register class SHALL carry an A12-set maximum contest-marker duration; on lapse, A6 referral is mandatory and the marker clears automatically. Subject-standing contests of identity, civil-status, and encumbrance entries take the expedited track by default, and A6 (not the registrar) MAY order interim suppression of the disputed field from the public_faith projection where continued projection is itself the alleged harm. The public contested marker is a boolean plus case reference only; contestant identity, standing_basis, and contest evidence are case-scoped to the parties, A6, and supervisory organs. refusal_records are readable by the filer, A6, and the mandate supervisor only and never enter any public_faith projection.

### Protocols

R1-P5 Registration.
1. The filer submits a sealed hash commitment; the witness set attests received_at and assigns sequence_position (R1-I14).
2. Content is revealed and evaluated against the criteria_version fixed by received_at, including evidence authenticity (R1-I13), the entry class's identity assurance level, proof of the filer's authority over the disposing subject distinct from authentication, and second-channel confirmation from the registered right-holder for constitutive and disposition-class filings.
3. On any failed criterion the registrar refuses with a refusal_record (failed_criterion_refs set) and routes it under R1-P8.
4. On pass the entry is appended and marked unvalidated; the accept event records each authenticity and assurance result. Any mandated pre-effect notice interval runs before effect attaches.
5. Asynchronous validation runs; on pass the entry is marked validated, on fail it is void ab initio. Forged_evidence and compromised-credential filings are void at any tier, with liability booked jointly against attester and filer.

R1-P6 Contest.
1. A contestant with independently evidenced, pre-dating standing (R1-I16) files a contest; the marker is set as a boolean plus case reference. No freeze attaches.
2. A6 MAY issue a prima-facie freeze within the published deadline; else disposition stays free. The holder MAY substitute security to lift a freeze.
3. Further contests consolidate into the open case. The marker ceiling (R1-I24) triggers mandatory A6 referral and automatic clearance on lapse.
4. A6, not the registrar, makes any knowingly-baseless finding and orders bond forfeiture and V4 or TrackRecord booking (R1-I22).

R1-P7 Correction.
1. A subject or court files a correction, validated against the published criteria (R1-I17); subject contests of identity, civil-status, and encumbrance take the expedited track (R1-I24).
2. The superseded version is retained append-only and linked; a court order MAY or SHALL reduce its public_faith projection to a tombstone (R1-I17).
3. A6 MAY order interim suppression of a disputed field pending resolution (R1-I24).

R1-P8 Appeal.
1. A refused or contesting filer appeals to A6 on the expedited track; the norm-set and criteria_version are those fixed at the witnessed received_at (R1-I14).
2. Window lapse without disposition auto-instantiates a deemed referral (R1-I18); above the threshold these consolidate into one supervisory case.
3. An A6 disposition is appended as a root-register or entry event and propagates to mirrors as an invalidation under R6.

### Lifecycle and edge cases

(a) Unvalidated to validated: an entry carries effect from append, but reliance on it is unprotected against its subject until validation (R1-I15); validation failure voids ab initio with S1-I14 restitution.

(b) Conflicting filings for one subject: every subject_ref maps deterministically to exactly one sequencing shard with one sequencer, so conflicting filings sequence in a single total order; a second Active entry for an exclusive-claim class fails closed at append and is void ab initio, never a contest (R1a single-sequencing). Cross-shard or cross-register effects use a multi_leg_commit equivalent.

(c) Registrar outage, refusal, or mandate lapse: windows keep running; deemed referrals accrue and consolidate under the circuit breaker (R1-I18); an interim custodian registrar auto-appoints, courts as default, so filings keep being accepted and windows keep running. The no-reopening rule does not bar review of the predecessor registrar's own entries.

(d) Migration in flight: old and new schemas both serve reads from plan activation to the completion event via the witnessed mapping (R1-I20); contested entries resolve under their pre-migration key.

(e) Election registers: hold an ordinary A12 mandate that incorporates A13 constitutional parameters (calendar compression, effect timing) by reference, satisfying R1-I3; they are not constituted directly by A13.

### Interfaces

- A6: challenged-criterion review, prima-facie freeze, knowingly-baseless and falsity findings, deemed and mass referrals, interim field suppression.
- A12: mandate parameters, criteria versions, identity assurance levels, marker ceilings, notice intervals, snapshot ages, tombstone triggers.
- A13: constitutional parameters incorporated by reference into election-register mandates.
- R4 and R5: issuer and attestation chains for authenticity resolution.
- R6: mirror propagation of contest markers, corrections, and supersessions as invalidations.
- S2: contract-scoped reads of tombstoned content and non-public entry fields.
- S4: access logging and effective-notice records.
- S7: registrar_abuse and forged_evidence classes; S7 Protocol 1 for provisional bookings pending appeal.
- witness_set and root-of-roots (R1c): received_at attestation and criteria-version enactment.

### External bindings

Relies on R1a for the root-register model, single-sequencing, and identity-at-filing preconditions; on R1c for reliance protection (R1-I29), compensation funding (R1-I30), witness independence, and mirror discipline; on S1-I14 for restitution on void-ab-initio outcomes; on S7 for the registrar_abuse and forged_evidence classes and for provisional bookings with appeal rights.

### Open questions

1. Calibration of per-class identity assurance levels and second-channel confirmation for low-infrastructure or displaced populations that lack a reachable registered right-holder channel.
2. The mass-referral threshold value and the funding and service-level guarantees for A6 expedited-track capacity under a coordinated filing flood.
3. Authenticity resolution when an evidence issuer is a foreign frame (A15) with no live revocation endpoint: whether a cached signed revocation list satisfies the gated-tier live re-resolution rule.
4. Whether a received_at falling inside a criteria_version pre-effect challenge window binds the filing to the prior or the challenged-new criteria pending A6 review.

## R1 assurance and federation: public faith, anchoring, mirrors

### Purpose
This section defines what a register entry is worth to those who did not write it. It fixes the base_effect an A12 mandate assigns to each entry class (constitutive, declaratory, probative) and the orthogonal public_faith projection attribute, the reliance protection third parties receive keyed to defect type rather than to the word fraud, and the integrity machinery (inclusion promises, k-of-n replicated sealed segments, independently witnessed cross-signed roots) that lets anyone verify an entry without trusting any single registrar. It governs R6 mirroring under mandate ceilings, federation with foreign registers under A15 treaty, register continuity across registrar succession and interim custody, cross-register exclusivity and judicial asset discovery, and reconstruction after catastrophic loss.

### Object model

| Object | Key attributes | Notes |
|---|---|---|
| effect_class_declaration | register_ref; entry_class; base_effect (constitutive, declaratory, probative); public_faith (bool); public_faith_scope (field set); a12_mandate_ref; version | base_effect is one closed polity-wide enumeration; public_faith is an orthogonal projection attribute, never a base_effect member; both are mandate-assigned, never registrar discretion |
| public_faith_projection | register_ref; entry_class; field_scope; minimum_field_set_ref; projection_policy_ref | The mandate-defined default-readable slice; SHALL cover the constitutionally reviewed minimum for its effect class (R1-I28); everything beyond it stays gated |
| reliance_certificate | entry_ref; projection content_hash; as_of; root_ref; registrar_signature | Portable proof of what the register showed at reliance time; verifiable against witnessed roots without the registrar |
| inclusion_promise | filing_ref; segment_root; submission_time; registrar_signature | Per S4; delivered to the filer on acceptance; survives registrar failure as filer-held evidence |
| anchoring_commitment | register_root; cadence_window; witness_signatures; replica_attestations | Cross-signed root; accepted for anchoring only after k-of-n segment replication (R1-I31) |
| witness_set | peer_registrar_refs; court_refs (at least one); quorum; independence_attestation | Control and key custody disjoint from the registrar; explicit consistency-checking duty; floor per A12 within the R1-I32 minimum |
| mirror | source_register_ref; entry_class; declared_freshness; staleness_limit; reliance_ceiling; escrow_ref; last_anchored_root; operator_ref | freshness and staleness_limit are mandate ceilings, not operator declarations; reference not copy; never authoritative |
| federation_link | treaty_ref (A15); foreign_register_ref; effect_mapping; reliance_ceiling; status | Sole channel through which foreign entries acquire domestic effect |
| succession_event | outgoing_registrar; incoming_registrar or interim_custodian; a12_instrument; notice_period; chain_handover_attestation; witness_supervision_ref | The register persists; only its steward changes; keys never transfer |
| asset_discovery_order | a6_case_ref; debtor_subject_ref; scope; sealed_until; access_log_ref | Single A6 instrument running the subject-enumeration query across root-register children and both R2 ledgers (R1-I39) |
| recovery_manifest | last_witnessed_root; segment_inventory; replica_inventory; promise_claims; contest_window; provenance_marks | Governs reconstruction; itself an append-only R3-anchored record |

### Invariants
- **R1-I25 (Effect is mandated, declared, queryable).** Every register SHALL carry, for each entry class, exactly one effect_class_declaration assigned by its A12 mandate. base_effect is one closed polity-wide enumeration: constitutive, declaratory, probative. public_faith is an orthogonal projection-policy attribute (a boolean plus a public_faith_scope field set), never a member of the base_effect enumeration; a class carries a base_effect plus optional public_faith over a named field scope. The declaration is data: any reader can query which base_effect and which public_faith_scope an entry class carries. A registrar SHALL NOT upgrade, downgrade, or imply an effect or projection scope the mandate does not assign; doing so is registrar_abuse under S7.
- **R1-I26 (Declaratory and probative effects).** A declaratory entry records a fact existing independently of registration (a birth, a death, an observed result): it creates a rebuttable presumption of the fact as of its append position, and non-registration never negates the fact though it MAY breach a filing duty. A probative entry is conclusive evidence of the recorded fact for official dealings, rebuttable only through the register's own contest and correction machinery, but it too does not constitute the underlying right. Where the mandate assigns public_faith to a declaratory or probative class it confers evidentiary reliance only: rebuttal operates ab initio on the fact, the good-faith relying party is compensated through the R1-I30 route, and the true subject's status is never converted into another's. Rebuttal is always a new evidence-bearing event, never an edit; the rebutted entry stays queryable with its rebuttal linked.
- **R1-I27 (Constitutive effect).** A constitutive entry creates the right or status it records: before the append there is no right. Constitutive entry classes SHALL sit on the gated tier (synchronous registrar gate within the S1-I10 window); a purported constitutive change that bypassed the gate is void ab initio. Only a constitutive class may carry public_faith that defeats a true right (indefeasibility), and then only under R1-I29(b) and R1-I30. A12 assigns constitutive effect at minimum to land title (P2), organization existence (O1), and registered IP rights (N12); civil status (B12) and vehicle registration (M7) default to declaratory. Election registers hold an ordinary A12 mandate that incorporates the A13 constitutional calendar and effect parameters by reference (satisfying R1-I3); the electoral process constitutes the result, the register records it.
- **R1-I28 (Public-faith projection and its minimum).** Where the mandate assigns public_faith, third parties MAY rely on the public-faith projection as correct and complete for the mandated field scope; silence outside that scope warrants nothing. The projection is defined by the mandate, not the registrar and not the subject. For each effect class the A12 mandate SHALL define a constitutionally reviewed minimum projection field set sufficient for the reliance that class grants; a constitutive register SHALL project at least the current right-holder identity, all registered encumbrances, the effect class, and contested and historical markers. R1-I29 protection is conditioned on the register meeting its minimum; a would-be relying party MAY contest a projection as insufficient on the A6 challenge route, and a shortfall is registrar liability under R1-I30. The projection is served under a constitutional standing template: this section amends S2-I18 to extend the constitutional_standing_template enumeration with (d) a mandate-defined public_faith_projection service per register and (e) holder own-statement and own-account plenitude, enacted at Charter level, so S2-I1 remains universal. For an entry's non-public field scope the A12 mandate materializes the subject as co-controller (an S1-I1 ownership_record deviation), so a read there requires subject consent plus registrar gate execution jointly.
- **R1-I29 (Reliance keyed to defect type).** Reliance protection turns on the kind of defect, never on the label fraud, and this rule states it once for the whole polity. (a) Authority defects, in the disposer's authority to dispose (impersonation, forged mandate, dead or non-existent grantor, forged evidence of authority, a filing on compromised disposing-party credentials), are void ab initio at every tier with no reliance protection and S1-I14 restitution; the concealing party enters the perpetual-clawback class, provable forever through the sealed per-event commitments of S4-I12. (b) State defects, in the recorded state of an otherwise-authorized right (an undisclosed prior claim, a registrar mis-entry), leave a gated-tier good-faith acquirer protected with the true holder compensated under R1-I30, but only where the A12 mandate assigns public_faith to the relied field scope and names a funded assurance route; where no funded route is named, protection degrades to prospective voidability and the true holder keeps the right. This narrow carve-out expressly amends S1-I5. Fast-tier reliance is voidable prospectively from correction only (S1-I5); reliance on an entry still marked unvalidated is unprotected against that entry's subject, and any acquisition inside the contest window or from an unvalidated filer is presumed bad faith with the burden of rebuttal on the acquirer. Actual knowledge of the inaccuracy or participation in procuring it destroys protection at any tier.
- **R1-I30 (Register error liability and funded assurance).** A class may carry the gated-tier defeat-of-true-right protection of R1-I29(b) only where its A12 mandate names an operative assurance route (registrar escrow, a polity assurance pool, or both) bearing primary and non-subsidiary liability with a normed payout window, subrogated against the fraudster after payment. Where protected reliance defeats a true right and the defect traces to registrar fault (wrongful acceptance, wrongful refusal, lost filing), the loss is registrar_abuse with compensation per S1-I10 funded through that route. Where the defect traces to filer fraud, the funded route pays the true holder first and subrogates; the fraudster remains liable in the perpetual-clawback class under S7. No funded route, no title-defeating effect.
- **R1-I31 (Inclusion promises, sealed segments, durability).** Every accepted filing SHALL return a registrar-signed inclusion_promise to the filer before the filing is deemed complete. Segments seal into Merkle roots on a bounded cadence; every sealed segment SHALL be replicated k-of-n across the witness set and registered mirrors before its root is accepted for anchoring, so that reconstruction equals replica recovery. A promised filing absent from a sealed, anchored root after the normed merge delay is registrar_abuse, and the filer-held promise shifts the burden per S4-I6. Wallets and agent runtimes SHALL retain promises by default.
- **R1-I32 (Mutual anchoring and witness independence).** No register vouches only for itself: every register root SHALL be anchored into the Audit Registrar root_of_roots and counter-signed by a witness_set of at least N witnesses with control and key custody disjoint from the registrar, including at least one court witness. Quorum counter-signature SHALL precede any root grounding finality or public faith. A counter-signing witness is jointly liable for divergence it could have detected. The duty is scoped: witnesses counter-sign the root_of_roots once per cadence and verify individual register chains by published-schedule sampling, with full verification triggered by any filer promise-claim or divergence report; at least two independent anchoring targets SHALL exist so a root_of_roots outage tolls lateness rather than manufacturing polity-wide registrar_abuse. Reliance on a not-yet-anchored entry is protected only where the relying party holds the registrar's inclusion_promise plus the prior anchored root; equivocation in that window is void as to the later-shown state. Equivocation, lateness, and refusal to witness within the normed window are registrar_abuse.
- **R1-I33 (Mirrors never acquire authority).** An R6 mirror is a reference cache. It SHALL label every answer with source register, anchored root_ref, and as-of time; SHALL serve nothing beyond what the master could lawfully serve the same reader; and SHALL fail closed past its staleness_limit, refusing and referring to the master. Authority moves only by A12 mandate or succession_event, never by any sequence of mirroring. A mirror sits on query metadata and SHALL NOT mine it: registrar-side and mirror-side reads of the access_event corpus bind to intra_organ_access_contracts, are subject-enumerable, and any analytics over reader or subject metadata run only as S5-registered releases (the R2-I27 zero-analytic-privilege rule generalized to R1). Mirror access_events SHALL forward into the master log and the subject's enumeration within the anchoring cadence; R6 registration requires accepting this duty on pain of the R1-I34 liability regime.
- **R1-I34 (Mirror reliance ceilings).** declared_freshness and staleness_limit are ceilings set per entry class by the source register's A12 mandate, not operator declarations; reliance protection never exceeds the ceiling. Contest markers, corrections, and supersessions propagate to mirrors as invalidations under a far tighter limit, past which the mirror suppresses the affected fields and refers to the master. For constitutive and public_faith classes no mirror answer supports reliance unless it carries a master-issued reliance_certificate verified against a witnessed root. Reliance by a party affiliated with the entry's filer or with the mirror operator is unprotected, as is reliance on an expired or unlabeled answer. Mirror registration requires escrow or capital proportional to the reliance exposure the mirror can generate; the operator is liable for staleness-limit breaches and mislabeling.
- **R1-I35 (Foreign federation by treaty).** A foreign register's entries acquire domestic effect only through a federation_link under an A15 treaty registered in R6. The link's effect_mapping caps the domestic effect (a foreign constitutive entry maps to at most an attested reference with a declared reliance_ceiling); foreign entries are referenced, never copied into domestic registers. Treaty suspension freezes recognition prospectively and SHALL NOT retroactively void concluded good-faith reliance.
- **R1-I36 (Continuity, custody, recoverability).** The register is a meta-object distinct from its registrar. Every root-entry event touching a register's existence (mandate amendment, registrar succession, retirement) SHALL carry the A12 instrument as evidence, be witness-set counter-signed, and observe a published pre-effect notice period. Succession transfers stewardship and the root chain under witness supervision with no chain gap (keys never transfer, per S8). Retirement stops new filings only and never suspends the effect or queryability of existing entries. On registrar failure, refusal, or mandate lapse an interim custodian registrar auto-appoints (courts as default) so normed windows keep running and filings keep being accepted. The no-reopening rule bars re-litigating settled entries but does not bar review of the predecessor registrar's own entries. The register SHALL be reconstructible by replica recovery of sealed segments; witnessed roots and filer-held inclusion promises alone yield proof-of-loss and provisional re-filing rights, not content reconstruction.
- **R1-I37 (No title laundering).** Reliance protection is personal to the acquirer and never cleanses the entry. Any successor who procured the defect, is under common control with the procurer, or to whom the benefit of the defect traces (A6 is empowered and required to trace beneficial ownership on the true holder's request) takes void ab initio and enters the perpetual-clawback class, regardless of how many intervening good-faith links exist. An innocent intermediary keeps its consideration or its R1-I30 compensation, but not the power to pass unimpeachable title back toward the procurer's side.
- **R1-I38 (Projection read discipline).** Public-faith projection reads log via locally hash-chained batch buffers sealed into the register's segments on the anchoring cadence, with per-read granularity preserved inside the batch and caches required to emit their batch logs to the master; a sealed batch satisfies the S4 access-logging duty of R1-I7. Gated and contract-bound reads keep per-read synchronous access_events. Subject-side enumeration of public-faith reads shows only read count, reader class, and time bucket; reader identity is unmasked to the subject only after a delay window, and never for a read that ripens into a judicial or enforcement instrument within that window (automatic sealing, no instrument needed pre-filing). Bulk-pattern access to projections throttles or escalates to an S5-registered release or an A12 bulk-access license; cross-register joining of subject-identifying projection fields and publication of scraped register-derived aggregates without S5 registration are over_collection or audit_evasion under S7.
- **R1-I39 (Cross-register exclusivity and asset discovery).** Each root entry declares an exclusive subject_class scope; the root registrar refuses (with refusal_record) or refers to A6 any mandate whose scope overlaps an Active scope, and where overlap already exists the earlier root append position governs while the later register's conflicting entries carry declaratory effect only until A6 resolves. Gated-tier intake runs an R6 cross-reference check and, on a hit, appends contested markers to both entries and refers to A6. A single A6 asset-discovery instrument (on judgment or freezing-order standing) executes the subject-enumeration query across the root register's children and both R2 ledgers, returning entry references and encumbrance status under case scope, S4-logged and sealed from the debtor for a court-set window; this is the R1-specified judicial shape, so no individual register demands separate leave.

### Protocols
**R1-P9 (Anchoring and witnessing round).** 1. The registrar accepts filings and returns inclusion_promises. 2. It seals the segment into a root, and replicates the segment k-of-n across the witness set and registered mirrors before submitting the root for anchoring (R1-I31). 3. The Audit Registrar returns its own inclusion_promise and merges the root into the root_of_roots across at least two independent anchoring targets. 4. The witness_set counter-signs to quorum and publishes; witnesses cross-check by schedule and on any promise-claim or divergence report. 5. Any witness or filer detecting a missing promised filing or a divergent chain files registrar_abuse; the filer's promise decides the burden per S4-I6.

**R1-P10 (Reliance verification).** 1. Before a transaction the relying party reads the public-faith projection (directly or via a mirror within its mandate ceiling) and confirms it meets the class minimum (R1-I28). 2. It obtains a reliance_certificate binding content_hash, as_of, and root_ref. 3. It verifies the root against witness counter-signatures, trusting no single registrar; for a not-yet-anchored entry it additionally holds the inclusion_promise plus the prior anchored root (R1-I32). 4. It completes the transaction; the certificate is retained as reliance evidence. 5. If the entry is later corrected, protection follows R1-I29 by defect type, subject to R1-I37.

**R1-P11 (Mirror provisioning, R6).** 1. A mirror operator registers the mirror with source, entry_class, and escrow or capital proportional to reliance exposure; declared_freshness and staleness_limit bind to the source mandate ceilings, not operator choice. 2. The mirror syncs by root, verifying sealed segments against witnessed roots and never accepting unanchored content. 3. Each answer carries provenance labels and emits a batch access log to the master; contest markers, corrections, and supersessions propagate as invalidations under the tighter limit, past which affected fields are suppressed and referred to the master. 4. On passing the staleness_limit the mirror fails closed. 5. Mislabeling, stale serving, or metadata mining books against the operator per R1-I33 and R1-I34.

**R1-P12 (Catastrophic reconstruction).** 1. Loss or corruption is registered as an X3 incident; serving freezes per S8-I8. 2. A recovery_manifest is opened: last witnessed root, replica inventory of surviving segments, and a public call for filer-held inclusion promises within a contest window. 3. State is rebuilt by replica recovery of sealed segments; filings evidenced only by valid promises after the last root are admitted as provisional entries per S4-I6, with proof-of-loss re-filing where content is unrecoverable. 4. Reconstructed and provisional entries carry recovery provenance marks; the contest window closes provisional entries into ordinary ones absent contest, and disputes route to A6. 5. The witness_set attests chain continuity; recovery SHALL NOT diminish any honest filer's registered rights.

### Lifecycle and edge cases
- A mandate amendment changing an entry class's base_effect or public_faith scope operates prospectively; existing entries keep the effect and scope under which they were made (contemporaneous norms, Charter Art. 19).
- For an exclusive-claim class there is exactly one Active entry per subject (single sequencing per the S-cluster and the R1-I27 gate): a second Active entry on another shard is void ab initio and fails closed at append, so two reliance_certificates can never both hold protection. A certificate citing a void entry confers nothing, and any residue routes through R1-I30, never through a double title.
- Court-found-false or bad-faith content: a court-ordered correction MAY, and on a finding of falsity or bad-faith filing SHALL, reduce the superseded version's public-faith projection to a tombstone (existence, supersession link, and correction reference only), with the full superseded content retained append-only and readable only under S2 contract, case standing, or court order; integrity commitments and clawback provability are unaffected. Subject-standing contests of identity, civil-status, and encumbrance entries take the expedited track, and A6 (never the registrar) MAY order interim suppression of the disputed field from the public projection.
- Registrar succession mid-filing: in-flight filings continue under the S1-I10 windows against the incoming or interim registrar; the deemed-referral clock does not reset.
- A mirror of a mirror MAY exist in R6 but each link declares its true upstream and inherits the tightest staleness_limit; none claims source provenance.
- Federation partner failure: a foreign register that stops anchoring or equivocates has its federation_link auto-suspended on witness report; domestic references become flagged, not deleted, and concluded good-faith reliance is never retroactively voided.

### Interfaces
- **S1**: tier schedule for R1-I29; registrar discipline and compensation (S1-I10, S1-I14); register stewardship versus entry rights via the S1 controller-derivation rule and R1-I36 (no free-standing "ownership rule").
- **S2/S3**: public-faith projection as a constitutional standing template (S2-I18 as amended in R1-I28); subject co-controller materialization for non-public scope; all other reads contract-bound and shaped.
- **S4**: inclusion promises, sealed segments, k-of-n replication, root_of_roots, burden shift (S4-I6), sealed commitments surviving summarization (S4-I12); batched public-faith read logs and per-read gated access_events (R1-I38).
- **S5**: bulk-access releases, register statistics, and any analytics over reader or subject metadata.
- **S7/S8**: registrar_abuse, audit_evasion, and over_collection classes; key non-transfer at succession; compromise and custodian regimes during recovery.
- **R2**: ledger roots anchor through the same witness machinery; R1-I39 asset discovery spans both R2 ledgers; funded assurance routes (R1-I30) settle on R2 accounts.
- **R3/R4/R5/R6**: event substrate; identity anchoring of filers and relying parties; attestations as the vehicle for foreign-entry recognition; the mirror, federation, and cross-reference (R1-I39) objects.
- **A6, A12, A13, A15**: contest adjudication and beneficial-ownership tracing; mandates, effect schedules, minimum projection sets, and assurance routes; electoral parameters incorporated by reference; federation treaties.

### External bindings
Meta-Universe ARCH-018 mastership register (model-mastered registers, declared mirrors) and MUFP federation profile (R1-I35); ISO 19152 LADM and Torrens-system title-assurance funds (gated-tier public faith and the funded assurance route of R1-I29/R1-I30, as analogy not adoption); Certificate Transparency style witnessed append-only logs with independent witnesses (R1-I31, R1-I32); k-of-n and erasure-coded durable log replication (R1-I31); W3C Verifiable Credentials for reliance_certificates and foreign-entry attestations; VCLT via A15 for treaty mechanics.

### Open questions
1. Calibration of the reliance_ceiling and effect_mapping for A15 links to polities lacking S4-grade audit substrate: what minimum anchoring discipline a treaty partner must prove before any domestic effect attaches.
2. Calibration of the witness floor N, the court-witness minimum, and the k-of-n segment replication factor per register criticality class.
3. Who bears mirror S4 batch-logging and staleness-enforcement cost, and the escrow or capital curve, so mirrors stay plural (Art. 10 concentration goal) without becoming under-maintained stale-serving liabilities.
4. Whether the constitutionally reviewed minimum public-faith field set (R1-I28) is fixed uniformly per effect class polity-wide or set per register instance, and its constitutional review cadence.

## R2 core: accounts, postings and the two ledgers

### Purpose

R2a fixes the account model and posting semantics shared by the polity's two value ledgers: the AE ledger, which records sovereign, non-transferable axis value, and the $ rail, which records transferable settlement. It defines what an account is, how postings balance, how balance is derived without an authoritative stored balance, and the anti-abuse rules that keep AE from being minted, moved, or laundered between holders. Tier, finality, escrow and clawback machinery live in R2b; read, extract and privacy machinery live in R2c; this section is the substrate both depend on.

### Object model

- **ledger**: one of {AE, $}. The AE ledger carries holder axis accounts and operator-held counter-accounts; the $ rail carries transferable settlement accounts.
- **holder_axis_account**: one per (holder, value axis). Sovereign, non-transferable. Its balance is a fold, never a stored quantity.
- **counter_account**: one of {recognition_source, consumption_sink, anti_value}, per axis. Logically single, physically sharded: each sequencing shard holds a local **sub_account**. The logical balance is the anchored fold of its sub-accounts.
- **rail_account**: a $ settlement account, transferable, with per-class identity discipline set by the A10 mandate.
- **posting**: an append-only event with an authorizing event reference, one or more **legs**, optional **coupling_refs** to other postings, and an optional **cause_ref**.
- **leg**: a signed movement (credit or debit) against one account, carrying its account_ref, amount, axis and effective_time.
- **checkpoint**: a per-account fold value committed into a segment root at segment seal and witness counter-signed (R1c witness set).
- **segment**: the sealed, anchored unit over which balances checkpoint and summarization operates.

### Invariants

R2-I1. The polity keeps exactly two value ledgers, AE and $. Postings are append-only events; a posting once appended is never mutated, only superseded, reversed or revalued by a later posting. No account balance is stored authoritatively anywhere.

R2-I2. Counter-accounts (recognition_source, consumption_sink, anti_value) are logically single but physically sharded: each sequencing shard holds a local sub-account, and the logical counter-account balance is the anchored fold of its sub-accounts, reconciled at segment-seal cadence. Every holder axis account and every sub-account maps deterministically to exactly one sequencing shard served by exactly one sequencer.

R2-I3. Every posting's legs SHALL sum to zero on its ledger. An ordinary AE or $ posting SHALL balance entirely within one shard and commit without multi_leg_commit; multi_leg_commit is reserved for genuinely multi-holder gated postings whose legs span shards or registers, and cross-shard or cross-register effects SHALL use that multi_leg_commit equivalent atomically.

R2-I4. The $ rail settles transferable value. Rail identity discipline is per-class under the A10 mandate; the cash-like sub-threshold tier (R2c) structurally omits stable counterparty identifiers, while above-threshold and gated classes retain full identification where traceability is the mandated purpose. Anti-structuring per R2b governs aggregation across split postings.

R2-I5. Balance is never stored authoritatively and materializations are caches with no legal weight. A balance is assertable only as the latest witnessed checkpoint plus the fold of legs sequenced after it. At each segment seal the operator SHALL commit per-account fold values into the segment root, witness counter-signed; summarization SHALL preserve the checkpoint chain so that post-summarization balances remain derivable and court-provable from surviving roots and checkpoints.

R2-I6. AE is non-transferable across postings, not merely within one posting. No set of postings sharing an authorizing event, coupling_refs, or a counter_account flow trace may have the effect of funding one holder's AE credit from another holder's AE debit, except remediation routing executed under an S7 remedy_order. recognition_source credits SHALL trace solely to V3 valuation events and SHALL NOT balance against any holder debit. This enforces the Charter Article 13 non-transferability rule against multi-posting composition.

R2-I7. A recognition posting SHALL NOT settle by lapse where its flow is intra-cluster (related or common-controlled parties per R4 or O1) or forms a value cycle within the class window; such a posting stays provisional until an independent V3 attestation and counterparty performance evidence are appended. Recognition magnitude per authorizing event is capped at the published catalog reference, and any excess is unbookable. Consideration given for a recognition attribution is void and clawback-eligible in the concealed class under the S7 recognition_trafficking class.

R2-I8. Consumption and draw legs SHALL be evaluated against the authoritative fold at the sequencer head position, never a materialized cache, and SHALL fail closed on insufficient entitlement. Only an anti_value_debit or a court-ordered leg may drive a holder axis account negative; no consumption or draw leg may.

R2-I9. Coupling to an attestation is bounded, not instantaneous. An AE debit leg coupled to a V3, V4 or R5 attestation SHALL reference that attestation as cause_ref, SHALL carry the attestation's append position as its effective_time, and SHALL sequence before the next segment seal of each target shard. Exceeding this bound is a registrar_abuse trigger. No global tick is assumed; effective_time semantics leave no window in which the coupled state reads clean.

R2-I10. Conflicting legs for one account sequence in a single total order under that account's sole sequencer. A second exclusive-claim leg attempted on another shard for the same account is void ab initio and fails closed at append, never becoming a contest.

R2-I11. On death, personal AE accounts seal per the post_mortem_policy, are readable post-mortem only through judicial_access_contracts, and never enter the estate as value. $ rail accounts and estate-relevant postings are seal-exempt for probate scope per S1-I11; the seal exemption does not reach the AE ledger.

R2-I12. Reopening a settled flow requires new evidence through expert-calibrated revaluation, executed by reversing entries, and MAY move in either direction. Honest error settles as a reversal without anti-value; anti-value attaches only per the S7 good-faith rules. Symmetric over-charge reversal never requires proving the victim's own concealment. Clawback proper, meaning recovery against accumulated assets and entry into the no-limitation class, is gated separately behind the A6 concealment or grossness finding of R2-I19 and is not available on revaluation alone.

### Protocols

R2-P1 (recognition posting). On a V3 valuation event: resolve the contributing holder and axis from the valuation only; credit the holder axis account against the recognition_source sub-account on the holder's shard; clamp the amount to the published catalog reference and mark any excess unbookable; if the flow is intra-cluster, common-controlled, or forms a value cycle in the class window, mark the posting provisional and withhold lapse-settlement until an independent V3 attestation and counterparty performance evidence append; otherwise settle on the ordinary window. Record the V3 event_ref as the sole credit source.

R2-P2 (consumption or draw posting). On an authorizing consumption or draw event: compute the authoritative fold of the target holder axis account at the sequencer head; if entitlement is insufficient, fail closed and append a refusal leg with the failed criterion; otherwise debit the holder axis account against the consumption_sink sub-account on the same shard. The posting balances within one shard and commits without multi_leg_commit. R5 attestations, where present, are consumed as evidence of entitlement.

R2-P3 (revaluation or reversal posting). On new evidence resolved by expert calibration, or on an operator restorative correction under R2b: append reversing legs that reference the original posting via cause_ref and coupling_refs. A revaluation reverses in either direction and rebooks at the calibrated value; anti-value is booked only where the S7 good-faith rules attach it. A clawback reversal executes only under an A6 order per R2-I19 and may carry the tracing and avoidance powers granted in R2b.

### Lifecycle and edge cases

(a) **Wash and round-trip attempts.** Two parties booking inflated planned value-cost across an intra-cluster or cyclic flow cannot harvest recognition by lapse: R2-I7 holds those postings provisional pending independent V3 attestation and counterparty performance, and the catalog cap voids inflated magnitude. Paid-for attribution is void under the S7 recognition_trafficking class.

(b) **Cross-shard multi-holder posting.** Where a gated posting genuinely moves value between holders on different shards, it commits via multi_leg_commit; all legs commit or none do. Ordinary retail postings never take this path, so no global serialization point exists.

(c) **Counter-account reconciliation.** Sub-account folds reconcile into the logical counter-account balance at segment-seal cadence; solvency checks for consumption and draw (R2-I8) still read the head-position fold of the holder axis account, not the reconciled aggregate, so reconciliation lag never relaxes a solvency gate.

(d) **Death.** AE accounts seal per R2-I11 and are unreadable except through a judicial_access_contract; the $ rail and estate-relevant postings remain probate-accessible. AE is never valued into the estate.

(e) **Coupled debit lateness.** If a coupled AE debit cannot sequence before the next segment seal of a target shard (outage, congestion), the bound is exceeded and the condition raises registrar_abuse rather than silently backdating; the debit carries the attestation append position as effective_time regardless.

### Interfaces

- **V3 valuation**: sole source of recognition_source credits (R2-I6, R2-P1).
- **V4 indicators**: source of anti_value debits and, under R2b, escrow tolling.
- **R4 / O1**: cluster, related-party and common-control resolution for R2-I7 and R2-I6.
- **R5 attestations**: entitlement evidence consumed by R2-P2.
- **S7**: remedy_order routing (the only lawful holder-to-holder AE path) and the recognition_trafficking and good-faith rules.
- **A6**: court gate for clawback (R2-I12, R2-I19) and for the concealment or grossness finding.
- **A10**: rail identity thresholds and cash-like tier boundary.
- **R1c witness set and segment sealing**: witnessed checkpoints and anchored folds (R2-I5).

### External bindings

- Charter Article 13 (AE non-transferability), enforced against multi-posting composition by R2-I6.
- S1-I11 (estate seal-exempt enumeration), scoped by R2-I11 so it never reaches the AE ledger.
- S1-I14 (restitution) applies where a coupled or recognition posting is void ab initio.

### Open questions

1. The value-cycle detection horizon for R2-I7 across shards within a class window: what bounded lookback keeps cycle detection tractable without leaving a settlement path for slow-forming rings.
2. Calibration authority and refresh cadence for the published catalog reference used by the R2-I7 recognition cap, and how disputes over the reference price route to A6.
3. Whether counter-account sub-account reconciliation at segment-seal cadence needs a tighter bound for high-velocity axes to keep the logical fold court-provable under contest without approaching per-leg reconciliation cost.

## R2 integrity and settlement: finality, escrow, clawback

### Purpose

Defines how ledger postings acquire finality, how business inflows are held in externality escrow, and how value is recovered by clawback and avoidance once concealment or defect is found. It also fixes the integrity substrate on which settlement rests: single-sequencing of each subject, physically sharded counter-accounts, witnessed balance checkpoints, and witnessed root anchoring. The operator remains a recorder and settlement engine, not an adjudicator; every merits determination routes to A6.

### Object model

- posting: a balanced set of legs; carries authorizing_event, coupling_refs, a counter_account flow trace, good_ref, a party pair, and a finality_class.
- reversing_entry: an append-only entry that undoes a prior posting; cause_ref in {operator_error, revaluation, clawback_order, remedy_order}.
- finality_class: instant or deferred, derived per R2-I14 from the aggregate of related postings, never declared per posting.
- escrow_tranche: a held fraction of a business inflow, sized by exposure, carrying an externality_window; releases lazily per R2-I16.
- externality_window: the interval in which V4 harm may still materialize against a tranche flow class; tolls per R2-I16.
- clawback_order and avoidance_order: A6 instruments driving reversing_entries and reach-back recovery (R2-P7, R2-P8).
- anti_value_debit: the only holder-driving negative leg besides court-ordered legs.
- witnessed_checkpoint: a per-account fold value committed into a segment root at segment seal, witness counter-signed (R2-I13).
- sealed_posting_commitment: the hash commitment produced when aged postings are summarized (R2-I20).
- shard_sequencer: the single sequencer of one sequencing shard (R2-I22).
- multi_leg_commit: the cross-shard atomic commit reserved for genuinely multi-holder gated postings (R2-I23).
- root_of_roots: the Audit Registrar aggregate root into which segment roots anchor on a bounded cadence (R2-I24).

### Invariants

R2-I13 (balance by witnessed checkpoint): A balance SHALL NOT be stored as a single authoritative figure. It is assertable only as the latest witnessed_checkpoint fold plus the fold of legs sequenced after that checkpoint. At each segment seal the operator SHALL commit per-account fold values into the segment root, witness counter-signed per R2-I24. Summarization SHALL preserve the checkpoint chain so post-summarization balances remain derivable and court-provable.

R2-I14 (finality classes; anti-structuring): Only cash-like postings below the A10-set threshold MAY take instant finality; all others take deferred finality with an externality_window. Finality class SHALL be determined on the aggregate of postings sharing a party pair, an authorizing-event cluster, or a good_ref within the class window, so a split series takes the deferred class of its aggregate. Deliberate splitting to obtain instant finality is audit_evasion under S7 and reopens the whole series, including against the T0 epoch-token batching path.

R2-I15 (finality; two reopening paths): A posting whose uncontested window has closed is final against every party, subject only to two paths. (a) Clawback, meaning recovery against accumulated assets and entry into the no-limitation class, is gated by the A6 concealment-or-grossness finding of R2-I19. (b) Expert-calibrated revaluation on new evidence MAY reopen a settled flow in either direction by reversing_entries per R2-I12, with anti_value attaching only under the good-faith rules of S7. Symmetric over-charge reversal SHALL NOT require proving the victim's own concealment.

R2-I16 (escrow tolling, upsizing, lazy release): An escrow_tranche is sized on booking by exposure and offender_standing. Automatic release SHALL be blocked and the externality_window SHALL toll while any V4 indicator, contest, investigation, or preservation_order touching the tranche flow class is open. A TrackRecord downgrade or new offender_standing SHALL re-size every unreleased tranche upward against an absolute minimum exposure floor. Release is lazy and derived: a released tranche materializes on the first subsequent touch of the account (next inflow, statement, spend, or audit), never on an eager timer. Amounts released during a period later found to be concealment are recoverable in the perpetual class, with no limitation running from release.

R2-I17 (bounded coupling of caused legs): Legs caused by an attestation (an anti_value_debit or an escrow adjustment) SHALL reference that attestation as cause_ref, SHALL carry its append position as their effective time, and SHALL sequence before the next segment seal of each target shard. There is no global tick; exceeding the coupling bound is a registrar_abuse trigger. Effective-time semantics leave no window in which the offender's standing reads clean.

R2-I18 (operator-error reversals restorative only): A reversing_entry with cause_ref operator_error SHALL be restorative only, exactly restoring the pre-posting state of the same accounts with no third-party leg. It is available only before finality unless every affected holder consents or A6 orders. It SHALL notify every leg party and appear in their enumerations, and SHALL book a provisional anti_value_debit against the operator that reverses only if the error is confirmed on contest. The operator's error rate remains a public quality signal but is never the sole sanction.

R2-I19 (clawback gate and tracing): The A6 concealment-or-grossness finding gates only clawback (recovery against accumulated assets and the no-limitation class), never ordinary revaluation. A clawback_order carries tracing effect: reversing_entries MAY execute against any transferee who took without value, from a related party (per R4/O1), or with knowledge, and against any transfer made within the published reach-back window before the harm materialized. The burden is on related-party transferees to prove value and independence.

R2-I20 (summarization scoped to postings): Aged postings summarize into sealed_posting_commitments on the normal cadence. Full detail SHALL be retained unsummarized for postings whose own externality_window or tranche is unexpired, and for all postings of an actor with open offender_standing. A holder's newer open tranche SHALL NOT force retention of unrelated postings whose windows closed clean. Summarization preserves the checkpoint chain (R2-I13) and clawback provability.

R2-I21 (remediation routing; AE non-transferability): No set of postings sharing an authorizing_event, coupling_refs, or a counter_account flow trace may fund one holder's AE credit from another holder's AE debit, except remediation routing executed under an S7 remedy_order. recognition_source credits SHALL trace solely to V3 valuation events and SHALL NOT balance against any holder debit. A recognition posting does not settle by lapse where the flow is intra-cluster, common-controlled, or forms a value cycle in the window; it stays provisional until independent V3 attestation and counterparty performance evidence are appended, and recognition magnitude per authorizing event is capped at the published catalog reference with the excess unbookable.

R2-I22 (single sequencing): Every subject_ref maps deterministically to exactly one sequencing shard with exactly one shard_sequencer. Conflicting filings for one subject sequence in a single total order. A second Active entry for an exclusive-claim class arriving on another shard is void ab initio and FAILS CLOSED at append; it never becomes a contest.

R2-I23 (cross-shard atomicity; sharded counter-accounts): The counter_accounts (recognition_source, consumption_sink, anti_value) are logically single but physically sharded, each shard holding a local sub-account. Ordinary postings balance entirely within one shard with no multi_leg_commit, and the logical balance is the anchored fold of sub-accounts reconciled at segment-seal cadence. multi_leg_commit is reserved for genuinely multi-holder gated postings whose effect spans shards or registers.

R2-I24 (anchoring and scoped witness duty): Every segment root anchors on a bounded cadence into the Audit Registrar root_of_roots and SHALL be counter-signed by the witness_set before it grounds finality or public faith. Witness duty is scoped: counter-sign the root_of_roots once per cadence plus sampled per-register chain verification, with full verification triggered by any filer promise-claim or divergence report. At least two independent anchoring targets SHALL exist, so root_of_roots outage tolls lateness rather than manufacturing polity-wide registrar_abuse.

### Protocols

R2-P5 (settlement and finality): 1) On append, assign the posting to its subject's shard (R2-I22) and evaluate finality_class on the related-posting aggregate (R2-I14). 2) Balance legs within-shard; use multi_leg_commit only for multi-holder gated postings (R2-I23). 3) Open the externality_window for deferred-class postings; instant-class postings settle at sequencing. 4) At segment seal, commit witnessed_checkpoints (R2-I13) and anchor (R2-I24). 5) A posting reaches finality when its window closes uncontested and its aggregate carries no open indicator.

R2-P6 (escrow): 1) On a business inflow, book an escrow_tranche sized by exposure and offender_standing. 2) Hold; block release and toll while any V4 indicator, contest, investigation, or preservation_order on the flow class is open (R2-I16). 3) On a TrackRecord downgrade or new offender_standing, re-size all unreleased tranches upward to at least the floor. 4) Release lazily and derived on the first subsequent account touch after the window closes clean.

R2-P7 (clawback and tracing): 1) On an A6 concealment-or-grossness finding, issue a clawback_order (R2-I19). 2) Execute reversing_entries against the offender and, with tracing effect, against any transferee who took without value, from a related party, or with knowledge, and against any transfer in the reach-back window. 3) Related-party transferees bear the burden to prove value and independence. 4) Book recovered value; amounts released during a concealment period enter the perpetual no-limitation class.

R2-P8 (claim schedule and avoidance): 1) On an established shortfall, open the claim schedule. 2) Exercise the avoidance power over transfers at undervalue and preferential transfers within the reach-back window, converting them to reversing_entries. 3) Rank and satisfy claims. 4) Unsatisfied perpetual-class claims persist against later-surfacing assets and traced transferees, not merely the escheat archive.

Housekeeping note: R2 protocol identifiers run continuously; R2-P4 is the closing settlement-posting protocol of R2a, and R2b continues at R2-P5 through R2-P8 with no gap or collision.

### Lifecycle and edge cases

(a) Colluding ring or wash flow: a recognition posting does not settle by lapse where the flow is intra-cluster or forms a value cycle (R2-I21), so the deferred class holds until independent V3 attestation; the finality aggregate (R2-I14) prevents splitting the currency leg to buy instant finality.

(b) Captured-operator reversal: a self-asserted operator_error cannot re-route value, since R2-I18 forces restorative-only legs, notice, and a provisional anti_value_debit; after finality it needs holder consent or A6.

(c) TrackRecord gaming then release: inflating TrackRecord no longer frees held value, because tolling (R2-I16) blocks release while any indicator is open and downgrades re-size unreleased tranches upward.

(d) Layered extraction through shells: instant finality does not shield the chain, since tracing (R2-I19, R2-P7) and avoidance (R2-P8) reach without-value, related-party, knowing, and reach-back transferees; the perpetual claim follows traced assets, not an empty archive.

(e) Stale-cache draw: consumption solvency is enforced against the sequencer head on the R2a side, and single sequencing (R2-I22) guarantees one authoritative order per subject, so no cross-shard stale fold exists to draw against.

(f) Sequencer outage: windows and coupling bounds toll on proven outage via the anchored public outage-interval register; lapse-eligibility is derived (R2-I16), so no timer-driven posting flood occurs.

(g) Summarized decades-old account: the balance remains provable from the latest witnessed_checkpoint plus subsequent legs (R2-I13), even after content is summarized to commitments (R2-I20).

### Interfaces

- A6: issues concealment-or-grossness findings, clawback_orders, avoidance orders, prima-facie freeze orders, and reversal orders; sole adjudicator of merits.
- A10: sets the cash-like instant-finality threshold (R2-I14).
- R3 (V4): supplies harm indicators that toll and re-size escrow (R2-I16).
- V3: supplies valuation events that alone ground recognition credits (R2-I21) and calibrate revaluation (R2-I15).
- R4 and O1: resolve related-party and common-control status for tracing and non-transferability.
- Audit Registrar: holds the root_of_roots; the witness_set counter-signs per R2-I24.
- S7: books audit_evasion (structuring), recognition_trafficking, and remedy_orders.

### External bindings

- Charter Art. 13 AE non-transferability binds R2-I21 and R2-I23.
- S1-I14 restitution attaches to void-ab-initio outcomes surfaced through settlement.
- S4 cadence bounds the segment-seal, checkpoint, and coupling deadlines (R2-I13, R2-I17, R2-I24).
- S8 key-custody separation underlies the witness_set independence relied on by R2-I24.

### Open questions

1. The absolute minimum exposure floor and the reach-back window length are per-class parameters; their calibration across register classes is unresolved.
2. Whether the outage-interval register should anchor to more than two targets to bound correlated-outage tolling abuse.
3. Cross-register clawback ordering when a traced transferee's assets sit under a foreign frame (A15) remains open.

## R2 access, privacy and sensing

### Purpose

A ledger that anyone can browse is a surveillance instrument; a ledger nobody can query is not a system of record. This section fixes the read side of R2 for both great instances (the sovereign AE-ledger and the thin $ settlement rail): who may see accounts, postings and balances, in what S3 shape, under what S2 basis, and how the polity senses the economy without ever reading a person. The write side and account structure are specified in the preceding R2 sections; everything here is a projection discipline layered on the S cluster, adding only what is ledger-specific: the counterparty leg, the solvency predicate, the pair-graph, the judicial asset-discovery shape, and the clawback-grade retention rule.

### Object model

| Object | Key attributes | Notes |
|---|---|---|
| own_statement | holder_ref; account_scope; period; as_of; projection_id | Full-fidelity field_subset projection of the holder's own accounts, postings and balances, across all axes and both instances |
| shared_posting_extract | posting_refs; requesting_party_ref; leg_filter; period | The only counterparty shape: exactly the requester's legs of X5 interactions with the holder, nothing adjacent |
| posting_metadata | party_pair; time; axis_set; amount_class | Who transacted with whom and when: bilateral X5 data co-owned by both parties; the raw material of the pair-graph |
| ledger_predicate | predicate_ref (S6 catalog); parameter_slots (threshold, band, as_of, methodology_ref C7); freshness_class | Catalogued solvency and means predicates: balance above T, income in band, no arrears, escrow adequately funded |
| ledger_attestation_binding | issuer_ref (Ledger Operator); commitment; validity; revocation_ref; cadence_epoch | R5 binding to ledger state, issued parameter-blind for all active holders on a fixed published cadence; predicate, threshold and as_of resolve prover-side |
| judicial_asset_discovery | case_ref; standing (judgment or freezing order); subject_ref; scope; seal_window | A6 instrument executing the subject-enumeration query across the root register children and both R2 ledgers in one act |
| ledger_release | frame_partition; measure; epsilon_debit; release_register_ref | An aggregate over ledger data, lawful only through the S5 release register |
| ledger_summary_record | period; merkle_root; sealed per-posting commitments | Post-window collapse of aged detail per S4-I12; commitments reconstruct parties, amounts and time under court order |

### Invariants

- **R2-I25 (Holder plenitude).** An account holder SHALL be able to read their own accounts in full: every posting, every leg, every balance, every axis, on both the AE-ledger and the rail, at any history point, as an own_statement. This right is unconditional, non-waivable and fee-free at the statutory cadence. It rests on the S2-I18 constitutional_standing_template as amended by this section (see the S2 amendment note below), which extends the enumeration to (e) holder own-statement and own-account plenitude, enacted at Charter level. Where the holder is a natural person, operator-side and organ-side reads of the same records remain subject-enumerable per S2-I8.
- **R2-I26 (Counterparty leg only).** A counterparty to a posting SHALL read exactly the shared legs of its own X5 interactions with the holder: the shared_posting_extract is the sole counterparty shape. It SHALL NOT expose balances, non-shared postings, third-party legs, axis values outside the shared flow, or existence of other accounts. The extract right arises from the posting itself, a bilateral standing basis formed at commit, and needs no fresh grant. A leg-party re-reading its own shared legs is exempt from the R2-I32 composition gate, since the data was lawfully its at commit. Any denial of a standing-basis extract read SHALL cite at least one published machine-checkable criterion and carry an expedited A6 appeal route, never the S3-I11 indistinguishable envelope, which is reserved for readers with no standing basis.
- **R2-I27 (No sovereign gaze, zero analytic privilege).** No state organ SHALL read any person-grain account, posting, balance or posting_metadata without the holder's consent_record or a judicial_access_contract naming the subject (S2-I8, S2-I15). The Ledger Operator's own operational reads bind to intra_organ_access_contracts and log subject-visibly; operating the ledger confers zero analytic privilege. The Operator SHALL issue ledger_attestation_bindings parameter-blind on a fixed published cadence for all active holders, independent of any proof event, and SHALL retain no per-holder issuance analytics outside an S5 release. Registrar-side and mirror-side reads of the access_event corpus likewise bind to intra_organ_access_contracts, are subject-enumerable, and any analytics over reader or subject metadata run only as S5-registered releases; mirror access_events forward into the master log and the subject enumeration within the anchoring cadence. Emergency instruments never yield raw ledger access: pre-declared templates with declared shapes only (S2-I9).
- **R2-I28 (Sensing at frame grain).** Governance sensing over the ledger (imbalance measurement, corridor monitoring, escrow-adequacy statistics, concentration monitoring below the self-charge trigger) SHALL consume only k-floored, noised aggregates registered in the S5 release_register along approved cohort_frames, debiting the shared privacy budgets. The balancing loop has no other lawful ledger input; Charter floor coverage runs through S5 monitor-only cohorts, never through per-person balance reads.
- **R2-I29 (Closed shape set).** Every ledger query SHALL be an S3 projection in exactly one of five shapes: own_statement, shared_posting_extract, aggregate (S5-registered), zk_predicate (S6), or judicial_asset_discovery (R2-I35). No path, for any reader including both operators, yields raw ledger access or an unshaped export.
- **R2-I30 (Prohibited demands and predicate-first).** Per-domain prohibited-demand schedules (S2-I4: employment, housing, credit, insurance, essential services) SHALL apply to ledger shapes. Where a gatekeeping party's declared purpose is a solvency or means question satisfiable by a catalogued ledger_predicate, demanding an own_statement or extract SHALL be bookable as over_collection (S6-I1); demanding any ledger shape as a condition of employment or shelter carries the S2-I4 coercion presumption. Proofs are verifier-bound, single-use and cross-verifier unlinkable per S6-I5 through S6-I8. The predicate catalog SHALL carry an extension procedure: any party MAY petition A12 for a new ledger_predicate against a published decision deadline, refusal citing criteria. A holder MAY volunteer an own_statement only on the holder's own initiative, recorded with an anti-coercion attestation in the S2 contract and inadmissible as a basis for any demand a gatekeeper makes toward another holder.
- **R2-I31 (Every read logged, shaped by volume).** Every ledger read of any shape SHALL be logged, holder-enumerable per S4-I7; zk verification sessions key by blinded_tags per S4-I10; absence from the anchored log resolves by the S4-I6 burden shift. Gated, contract-bound, extract and zk-verification reads keep per-read synchronous access_events. For high-volume read shapes (routine own-account polls, catalogued low-stakes T0 attestations, and any rail-served public projection) the gate MAY log via locally hash-chained batch buffers sealed into the register segments on the anchoring cadence (generalizing S4-I11), with per-read granularity preserved inside the batch and any cache required to emit its batch logs to the master; a sealed batch satisfies this invariant. Subject-side enumeration discloses reader identity outright only where the reader already stands in a known relation to the subject (a counterparty extract, a contract-bound read, or the holder's own read); for organ and third-party projection reads the subject's enumeration shows read count, reader class and time bucket only, with reader identity unmasked after a published delay window and never for a read that ripens into a judicial or enforcement instrument within that window (automatic sealing, no instrument needed pre-filing).
- **R2-I32 (Pair-graph protection).** Posting_metadata is co-owned bilateral data: each party controls its own legs, and a grant by one party discloses only that party's legs, never the counterparty's wider position. Neither party MAY grant, sell or publish the pair-graph wholesale. Composition is enforced by published mechanical quotas per (owner, declared grantee organization resolved through R4), counting extract volume and distinct-counterparty coverage per window with O(1) gate state; cluster-level collusion (several grantees pooling extracts) is caught retrospectively by S5/S4 audit over the access logs and booked as over_collection or audit_evasion, not adjudicated in the read path. Quotas apply to third-party grants and to aggregation or graph tooling over extracts, not to a leg-party's re-read of its own legs (R2-I26). A party's corpus of its own legs remains subject-co-owned: onward disclosure of counterparty-identifying legs requires the counterparty's consent or issues as an S5-registered aggregate. Cross-register or cross-class joining of subject-identifying projection fields, and publication of scraped ledger-derived aggregates without S5 registration, are over_collection or audit_evasion (S7); bulk-pattern access throttles or escalates to an S5-registered release or an A12 bulk-access license.
- **R2-I33 (Research by release only).** Researcher and analyst access to ledger data SHALL run exclusively through the S5 release_register: approved frames, differential-privacy noise, budget debits, lattice-tested cohort definitions. No anonymized-dump path exists; pseudonymization is not a lawful basis; publication of any ledger-derived aggregate without prior registration is audit_evasion (S5-I6).
- **R2-I34 (Clawback-grade retention).** Summarization of aged postings SHALL preserve, per posting, a sealed commitment (parties, amounts, axes, time under the segment Merkle root) per S4-I12, sufficient to reprove a flow when a court reopens a clawback-eligible case; since concealed or gross systemic anti-value is clawback-eligible forever, these commitments are perpetual. Full detail SHALL be retained, holder-and-court visible, for postings whose own externality window or escrow tranche is unexpired and for all postings of actors with open offender_standing; postings whose windows closed clean summarize on the normal cadence even while the holder has newer open tranches. Summarization never deletes: retired detail stays queryable to the holder and compellable by court order, and preservation_orders freeze summarization of named scopes.
- **R2-I35 (Judicial asset discovery).** A single A6 asset-discovery instrument, issued on judgment or freezing-order standing, SHALL execute the subject-enumeration query across the root register children and both R2 ledgers in one act, returning entry and account references and encumbrance status under case scope, S4-logged and sealed from the debtor for a court-set window. This is the R1-specified judicial shape, so no individual ledger or register may demand separate leave. It yields no raw postings beyond the enumerated references without a further case-scoped contract.
- **R2-I36 (Rail cash-like tier).** Below an A10-set threshold, $ rail postings SHALL use per-epoch rotating counterparty pseudonyms, holder-resolvable through R4 only under a judicial instrument, and the rail schema SHALL structurally omit stable identifiers for that class. Full identification is retained only for above-threshold and gated classes where traceability is the mandated purpose. The anti-structuring rule (R2-I14 as amended) applies: a series of sub-threshold postings sharing a party pair, authorizing-event cluster or good_ref within the window takes the finality and identification class of its aggregate, and deliberate splitting to obtain the cash-like shape is audit_evasion that reopens the series.

**S2 amendment note.** This section extends the S2-I18 constitutional_standing_template enumeration, at Charter level, with (d) a mandate-defined public_faith_projection service per register and (e) holder own-statement and own-account plenitude. For an entry's non-public field scope the A12 mandate materializes the subject as co-controller (an S1-I1 ownership_record deviation), so subject consent plus registrar gate execution are jointly required.

### Protocols

**R2-P9: own-statement read.**
1. The holder queries under the constitutional_standing_template, naming account scope and period.
2. The owner-side gate executes the S4-I2 atomic commit and generates the own_statement inside the trust boundary.
3. Delivery follows in the same commit scope; the holder MAY in the same session enumerate all access_events over their accounts, subject to the R2-I31 masking of not-yet-ripened organ and third-party reads.

**R2-P10: counterparty extract.**
1. A posting party requests a shared_posting_extract citing the posting refs or period of its interactions with the holder.
2. The gate verifies each cited posting names the requester as a leg party and filters strictly to shared legs; a leg-party re-read bypasses the composition quota (R2-I26), while third-party grants and graph tooling are checked against the R2-I32 mechanical quota with O(1) gate state.
3. On pass, the gate commits, logs to both parties' enumerations, and delivers; a standing-basis denial cites a machine-checkable criterion with an expedited A6 appeal route, and only a no-standing read denies in the S3-I11 indistinguishable envelope.

**R2-P11: solvency proof.**
1. The Ledger Operator issues ledger_attestation_bindings parameter-blind on the published cadence, committing to ledger state for all active holders without reference to any predicate, threshold or proof event.
2. The verifier issues an S6 challenge committing to its identity, the session, the versioned ledger_predicate and its claimed basis; the specific threshold, band and as_of resolve prover-side inside the ZK circuit against the current binding.
3. The prover checks the demand against the prohibited-demand schedule and demand_ceiling, records the resolved parameters (S6-I7), and MAY refuse any off-catalog demand.
4. The prover generates the verifier-bound proof with the non-revocation argument for the current epoch; the verifier checks binding freshness and issuer mandate, acts on the single bit, discards the proof_blob (S6-I16); the session logs by blinded_tag. Any on-demand binding issuance is an S4-logged access_event enumerable by the holder, and the Operator retains no per-holder issuance analytics outside S5.

**R2-P12: ledger release.**
1. A requester (Statistics Steward, sub-agent, researcher) names frame partition, measure and window; the gate checks frame conformance and budget capacity.
2. The evaluator computes under S5-I11 and S5-I12, preferring distributed local evaluation over holder-side gates with secure aggregation, so no process assembles a person-grain corpus.
3. K-floor and diversity tests apply with suppression; calibrated noise applies; the release registers, debits, then publishes.

### Lifecycle and edge cases

- (a) **Death**: split by instance. The $ rail accounts and estate-relevant postings are seal-exempt for probate scope (S1-I11); heirs read them through post-mortem judicial_access_contracts, never by inheriting the standing template. Personal AE accounts seal under the post_mortem_policy, are readable post-mortem only through judicial_access_contracts, and never enter the estate as value.
- (b) **Guardianship**: a guardian reads the ward's statements within the S1-I8 scope; every such read is advocate-visible; guardian-granted ledger disclosures to related parties require prior A6 approval.
- (c) **Dissolution**: organizational accounts route to the escheat archive with retention spanning the perpetual-clawback class (S1-I12); creditor reads proceed via judicial contracts.
- (d) **Reclamation (ValueDisputed)**: a contested posting opens both parties' shared legs plus the provisional revaluation record to the T2 reviewer under a case-scoped contract; the reviewer never sees either party's wider ledger.
- (e) **The rail's thin view**: the $ rail operator processes only the settlement leg (payer ref, payee ref, amount, instrument); it SHALL NOT enrich rail postings with AE-axis data, and its operational corpus is bound by R2-I32 like any party's leg collection. For the sub-threshold cash-like class the rail carries only the R2-I36 rotating pseudonyms, not stable identifiers.
- (f) **High-frequency T0 reads**: routine checkout attestations MAY use S6 epoch tokens with batched logging (R2-I31, S4-I11) where the predicate class is catalogued low-stakes; the R2-I14 anti-structuring rule prevents splitting postings to farm instant-finality or cash-like shape through this path.
- (g) **Judgment-creditor discovery**: a judgment or freezing-order creditor proceeds by the single A6 asset-discovery instrument (R2-I35), which enumerates the debtor's entries and accounts across the registers and both ledgers under case scope and is sealed from the debtor for the court-set window, so the debtor cannot watch the search and dissipate.

### Interfaces

- **S1**: holder and operator control resolution; escheat and post-mortem paths; subject co-control deviation for non-public entry scope.
- **S2**: standing templates (amended enumeration (d) and (e)), prohibited-demand schedules, intra-organ contracts, cumulative-disclosure clusters.
- **S3**: the five shapes, gate commit, indistinguishable envelopes reserved for no-standing reads, derived-artifact intersection over extracts.
- **S4**: per-read events, batched public-projection buffers, blinded tags, sealed summarization, inclusion promises for ledger shards.
- **S5**: release register, frames, budgets, monitor-only floor sensing over economic axes, retrospective collusion audit.
- **S6**: ledger predicate catalog and extension procedure, parameter-blind attestation bindings, demand ledger against repeat-proof harassment.
- **S7**: over_collection, coercive_demand, audit_evasion, unauthorized_read; clawback evidence per R2-I34.
- **A6/A10/A12**: asset-discovery instrument, cash-like threshold, predicate catalog and bulk-access license.
- **R1/R3/R4/R5**: registry pattern discipline, event anchoring, holder identity and pseudonym resolution, operator-issued attestations.
- **X5, F2, F8, C7, B4, V**: interaction legs, rail instruments, credit context, solvency methodology, standing effects, axis semantics.

### External bindings

ISO 20022 (statement and extract semantics: camt-family messages as the field_subset vocabulary), W3C Verifiable Credentials via R5/S6 (solvency proofs), differential privacy practice via S5, Charter Art. 4 (consent inviolable), Art. 6 (floors sensed at cohort grain), Art. 10 (operator concentration self-charge and cash-like threshold), Value-Money-Coupling (escrow, clawback classes grounding R2-I34), Consumption-and-Settlement (T0 default-trust windows and reclamation tiers).

### Open questions

1. Fee economics of the parameter-blind cadence: whether the Operator's periodic binding-issuance load is fee-recoverable under the S1-I10 cost-based schedule, and how stale a cadence commitment may lawfully be per predicate class.
2. Calibration of the R2-I32 mechanical quotas: concrete extract-volume and distinct-counterparty ceilings per (owner, grantee) window before the gate narrows, and whether a merchant's lawful own-leg corpus needs a statutory pseudonymization duty for routine T0 retail counterparty refs.
3. Length and design of the R2-I31 enumeration delay window: how long reader identity stays masked to a subject, and the exact ripening test that seals a read which becomes a judicial or enforcement instrument.
4. Migration of pre-MOS financial records into the ledger: whether imported histories enter the S5 differencing corpus and whether their subjects gain retroactive enumeration rights over legacy reads that predate S4.