# Actions and Events: the K2 and X1 specification

> **Status:** DRAFT v0.1 (2026-07-31). Deepens K2 (the act) and X1 (the occurrence) of the [World Model Architecture](../World-Model-Architecture.md), the world's verbs. Register rows: K2, X1 in [`world-models.csv`](../world-models.csv). Presupposes the [Security, Ownership and Access spec](./Security-Ownership-and-Access.md) (S cluster) and the [Registry and Ledger spec](./Registry-and-Ledger.md) (R3 event registers, R4 identity); on conflict with the architecture summary, this document governs for K2 and X1.
> **Provenance:** six parallel specifiers (K2 anatomy, attribution, consequences; X1 core, timeline, causation), then five adversarial reviews (an attribution attacker, a courts-and-justice red team, the doctrine keeper, a systems pragmatist, a surveillance reviewer: 60 findings, 20 critical), then one revision pass under a 46-point resolution charter that unifies the ontology and keeps the six sections consistent. Findings shaped every section; surviving open questions are honest.

---

## 0. How K2 and X1 fit together

K2 and X1 are the hinge of the entire world model: almost every occurrence is the trace of an act, almost every value flow (V3) is priced over an act, and the Semantic Timeline that lets any past state of knowledge be reconstructed is the ordered stream of X1 occurrences. They are the layer where doing, happening, valuing and blaming meet, and where the polity's richest and most sensitive data (everything anyone does) lives. Both rest on the same S-cluster and R-cluster machinery: the owner-side gate commit, witnessed anchored roots, S2 access contracts, the S5 release register, R3 event registers, R4 identity keys.

**The unified ontology (the charter's first act).** The drafts arrived with three incompatible pictures of the act-to-occurrence relation; the revision fixed one. A K2 act IS a specialization of an X1 occurrence: an agent-authorized, signed, graded state change, not a record that emits a separate trace. The act-occurrence appends to the actor's own register (the actor controls it); the state changes it causes elsewhere are distinct effect-occurrences appended to the affected owners' R3 registers, linked by a cause-ref. One mental-state scale (deliberate, knowing, reckless, negligent, accidental) maps deterministically to the V4 anti-value classification; concealment is a separate aggravator, never a point on the scale. One supersession edge (correction, retraction, revaluation); one occurrence field schema; causal ordering over logical stamps, never the wall clock.

**X1 is the occurrence and the timeline.** An occurrence records that something happened, with source and confidence: an assertion, not ground truth, so competing accounts of one happening coexist and are never merged. Every state change appends its occurrence to the owning register (fail-closed via a durable local write-ahead segment returning an inclusion promise, with a bounded degraded mode so a witnessing outage never freezes safety-critical acts). Three independent times (occurrence, record, valid) are kept distinct. Reconstruction of any past state of knowledge is a fold to a consistent witnessed frontier, not a scalar instant; retraction is a new occurrence, never an edit; phenomena and situations are patterns and conditions built over the stream. Causation is a typed network whose liability-bearing edges are court findings, not self-serving self-assertions.

**K2 is the act and its accountability.** Every act binds to a real identity at append (an R4-key signature; an unsigned act is contested, never authoritative) and cannot be backdated across a norm-epoch or deadline boundary without independent contemporaneous corroboration. Intent is graded and false grading is itself concealment. Responsibility is shared as raw per-owner assertions that only a court normalizes to one. Attribution pierces judgment-proof shells to beneficial owners and floors a deployer's grade for an autonomous agent at the deployment decision. And, crucially for justice, no act touching another's rights depends on the actor choosing to record it: a victim may originate a contested account that opens a case and obligates the named actor to answer, "unknown actor" is a first-class value, omissions are recorded independently of the breacher, and rights-touching acts on a person are the wrong even when they write nothing in the person's namespace.

Three commitments recur, matching the rest of the model:

1. **The record cannot be dodged by whoever benefits from its absence.** Forced dual-channel recordability, victim-originated occurrences, co-witnessed dual-append for rights-touching acts, and non-recording booked as its own anti-value close the master evasion: a bad actor who simply never self-records.
2. **The behavioral log is default-deny, both ways.** Bystanders and named participants co-own and can minimize their appearance; snapshots of others' data are minimized and subject-gated; harm-trace traversal cannot become a cheaper person-sensing channel than the S5 path; and yet victims retain a path to the record of what was done to them.
3. **Runnable at the highest volume in the polity.** Effect fan-out is a bounded declared grain, not one write per touched object; append tokens replace live delegation walks on the hot path; phenomena come from incremental S5 releases, not full-stream scans; durability and hot queryability are separated so "queryable forever" stays affordable.

The sections follow: K2 core, attribution, consequences; then X1 core, timeline, causation.

---
## K2 core: the act, its anatomy and composition

### Purpose
An act is a specialization of an X1 occurrence: an agent-authorized, signed, graded state change. K2a fixes what an act is, its anatomy, and how doings compose into acts. It states the ontology plainly: a K2 act IS an X1 occurrence (X1-I5), not a record that emits or carries a separate trace. The state changes an act causes elsewhere are distinct effect-occurrences linked to it by a cause-ref. Every act binds to a real identity at append, and no act touching another agent's rights depends on the actor choosing to record it.

### Object model
- act (specialization of the X1a occurrence; inherits the canonical occurrence field schema of C6: mandatory source_ref, confidence, norm_set_version_ref, optional logical_stamp, prior_state_ref, new_state_ref). It adds:
  - actor_ref: the performer (B1 or O1 or agent). MAY hold the reserved value `unknown-actor`, a first-class value distinct from an absent field.
  - action_type_ref: an N6-stewarded template.
  - authorizing_context_ref plus append_token: a precompiled, signed S1/N6 capability grant (K1) resolving the delegation, office, contract, or statute out of band.
  - signature: an R4-key signature over the act (K2-I15), binding every act, not only mediated ones.
  - mental_state_grade: exactly one of {deliberate, knowing, reckless, negligent, accidental}. There is no separate 3-value intent_kind.
  - basis_binding: a resolvable access_event, consent, or lawful instrument, required when the act touches another's namespace.
  - participants: act_participation rows.
  - responsibility_share: raw per-owner assertion rows.
  - composition refs: part_of (K3 process, K5 project) and decomposed_into act_refs.
  - effect_index: a bounded, grained descriptor of the effect-set (C39).
- act_participation: role drawn from the closed X1-I6 set {agent, patient, instrument, witness, beneficiary}. An agent-role binding MAY carry an optional liability_role of {principal, joint, aider, abettor, procurer}. Every named natural-person participant co-owns their binding and is subject-enumerable.
- snapshot_reference: a Rule-3 as-of freeze of another's data, minimized, sealed, and subject-gated.

### Invariants
- K2-I1: An act IS an X1 occurrence (X1-I5). It does not emit or own a separate trace. Effects are distinct effect-occurrences carrying a cause-ref to the act.
- K2-I2: An act SHALL be well-formed against its N6 action_type template and SHALL carry a valid append_token; the gate verifies the token signature and template-version hash, not a live delegation-chain walk. Re-validation happens on issuance and on dispute.
- K2-I3: A doing decomposable into differently-attributed or differently-priced parts SHALL be split into multiple acts. V4 evaluation over the aggregated flow of composed acts is per K2c; deliberate fragmentation to keep each act sub-threshold is an aggravating basis, never an escape.
- K2-I4: Every act carries exactly one mental_state_grade from the closed 5-grade scale. The deterministic map to the V4 {negligent, malicious, concealed} classification is: {accidental, negligent} to negligent; {reckless, knowing, deliberate} to malicious. Concealment is never a point on this scale; it is a separate S7 aggravator applied on top of the grade (see K2c).
- K2-I5: The gate SHALL reject any act that does not carry a K2-I15 signature verifiable to the named actor_ref's R4 key. An act that fails verification is recorded as contested, never authoritative. K2-I15 binds every K2 act.
- K2-I6: actor_ref MAY be the reserved `unknown-actor` value. An act is malformed and rejected at append ONLY when the performer field is structurally absent. An unknown-but-named-as-unknown or disputed performer SHALL be accepted and carried contested.
- K2-I7: Participant roles use the closed X1-I6 coarse set. The K2 liability roles {principal, joint, aider, abettor, procurer} refine the agent role as an optional liability_role on an agent-binding, never as new top-level roles.
- K2-I8: The act-occurrence appends to the ACTOR's own act register and the actor controls it (S1 derivation); it does not write another owner's namespace. Once an A6 case references a co-owned interaction record, no co-controller may narrow, revoke, or reduce any counterparty's or the court's projection of that record below its state at interaction time. Co-ownership grants a veto on onward disclosure to strangers, never on a counterparty's own access to a shared interaction, and never on judicial access.
- K2-I9: A Rule-3 as-of snapshot of another person's namespace data SHALL be minimized to the fields the action_type marks required, marked subject-visible and subject-enumerable, and held as a sealed reference that resolves through the subject's gate for any read beyond the actor's own evidentiary use.
- K2-I10: State changes an act causes in other namespaces are distinct effect-occurrences appended to those namespaces' owning R3 registers (their owners control), linked to the act by cause-ref. Such a cross-namespace effect SHALL carry a resolvable basis_binding whose witnessed record_time strictly precedes the act's record_time and whose valid_interval covers occurrence_time; a later-appended basis is invalid and the act is baseless (V4 unauthorized_access). Effect fan-out is bounded: a single occurrence MAY carry a batched effect-set under a declared grain, so "exactly one occurrence" (X1-I1) means one per declared mutation grain, not per touched object. Granularity floors are N6 steward-set per action_type, never owner-settable below the floor; any act whose flow crosses or plausibly crosses a V4 threshold SHALL be recorded at individual-act grain; a grain coarse enough to obscure a state-changing harmful act is rejected as audit_evasion.
- K2-I11: responsibility_share rows are raw per-owner assertions and are NOT constrained to sum to one at append. Normalization to one is a court-computed derived quantity from an A6 finding over the competing entries, recorded as a further occurrence; the constraint binds that finding, not the co-owned raw rows. The co-actor set SHALL include every participant with a traced causal_link (verified against the X5 record and the causal network); a missing traced participant invalidates the partition rather than silently rebasing to one.
- K2-I12: A rights-touching act class is keyed to A18 inviolable rights and bodily or personhood interests, not to a namespace read or write. Its recording is required and victim-originable (K2-P4) independent of any object mutation; the baseless act IS the wrong even when it writes nothing in the subject's namespace.
- K2-I13: Binding an identifiable natural person into any participant role is itself an act touching that person's rights, requiring a resolvable basis_binding or a k-anonymized non-identifying reference. Every named natural-person participant is a co-owner with subject-enumerability, a minimization right (pseudonymous or coarse reference absent a naming basis), and a contest and projection-redaction right.
- K2-I14: S4 access-event occurrences generated by reads of an act record are owned by the reading subject, default-deny and composition-limited; reads of another party's access history require an elevated judicial or consent basis and are recursively S4-logged. Audit-log appends are NOT themselves Rule-4 mutations, closing the read-to-write-to-read regress with a distinct non-recursive audit tier (batched or sampled with per-batch inclusion proof).

### Protocols
- K2-P1 Record an act: (1) verify the append_token signature and template-version hash (K2-I2); (2) verify the K2-I15 signature to actor_ref's R4 key, recording the act contested on failure (K2-I5); (3) if a principal or office is named, verify delegation_ref resolves under S1 to an active delegation covering this action_type for this performer at occurrence_time, else leave full responsibility on the signing performer and never shift it to the named office (C13); (4) if the act touches another owner's namespace, verify basis_binding resolves and its witnessed record_time strictly precedes and its valid_interval covers occurrence_time, else the act is baseless; (5) backdating check: an occurrence_time materially preceding record_time, or crossing a norm-epoch or deadline boundary relative to record_time, is inadmissible for norm and deadline purposes unless corroborated by an independent contemporaneous X1 whose record_time falls in the claimed epoch, with the burden on the asserter; (6) append the act-occurrence to the actor's register via a fail-closed durable write-ahead segment returning an inclusion_promise (record_time is two-phase: provisional local sequence at commit, finalized to non-repudiable on seal and anchor), and append any effects as separate effect-occurrences to the affected registers with a cause-ref.
- K2-P2 Decompose a doing into acts: split at each attribution or pricing boundary (K2-I3), record composition refs, and route aggregate V4 to the composing K3 or K5 structure.
- K2-P3 Read a co-owned act record: the read is S4-logged (K2-I14); third-party onward disclosure of a co-owned joint or X5 record requires consent from ALL co-controllers, and a single co-controller may access but not release onward; the K2-I8 dispute-freeze bars narrowing once an A6 case references the record; on revocation the revoking party's side is rendered non-identifying in all co-owners' projections within a bounded hard-maximum staleness.
- K2-P4 Originate a counterparty or victim account: any agent MAY append to their OWN register a rights-touching occurrence naming another agent in the agent role, carried contested; it is a valid A6 case-opener obligating the named actor to append a counter-account within a bounded window, and non-response triggers an explicit adverse inference (the contested account's confidence is raised, silence not rewarded). For rights-touching and performative acts, the act appends an inclusion-promised occurrence by reference to the affected counterparty's register as a condition of taking effect, so non-appearance becomes detectable non-recording.

### Lifecycle and edge cases
- Unsigned or failed-signature act: recorded contested, never authoritative (K2-I5).
- Unknown or disputed actor: accepted and carried contested via the reserved performer value (K2-I6).
- Omission: recorded as an act-occurrence carrying no state_delta when a duty_ref deadline passes without the required act. The owed_to party or a duty steward MAY append it to a shared X5 duty register (co-owned, not the breacher's sole namespace), and the standing duty_ref plus its unmet K7 commitment auto-generate a breach occurrence at the deadline; recording never depends on the breaching actor. X1-I1 carves the no-state_delta exception for these.
- Attempt: recorded as an act with its own grade and no completed effect-occurrence.
- Mass or high-fan-out act: one grouping occurrence plus a bounded effect-index (K2-I10).
- Conflicting accounts of the same act persist unmerged; the projection surfaces a conflict-tagged multi-value state or a deterministic logical_stamp representative with the losing account retained.
- Degraded mode: emergency acts are admitted against a provisional inclusion_promise with mandatory backfill, so a witnessing outage cannot freeze all state change.

### Interfaces
- X1a: an act IS an occurrence (X1-I5); inherits the canonical occurrence schema (C6); causal order is over logical_stamp, occurrence_time is descriptive contestable evidence (C7).
- X1-I6: the coarse participant-role set, refined here by liability_role (C8).
- K2b: signature (K2-I15), grade semantics and V4 input (K2-I17), delegation and shell/AI-chain attribution, and protocols K2-P5 onward.
- K2c: effect-occurrence ownership (K2-I27), basis_binding (K2-I29), aggregate V4 and concealment.
- S1 register-control derivation; S2 and S3 basis contracts; S4 access logging; S5 person-grain discipline; N6 templates and granularity floors; A6 adjudication; A18 inviolable rights; V4 anti-value; R4 identity keys; K1 capability; K7 commitments; X5 interaction records.

### External bindings
- MU Event two-time model: record_time equals MU Assertion Time; occurrence_time equals MU Occurrence Time; valid_interval is a MOS extension over the two-time model, per MU-V2-CORE-011 Lifecycle. The three times are never collapsed.
- MUC and AISMM meta-object identity for act, action_type, and participant.

### Open questions
1. The N6 de-minimis contribution floor below which a traced causal participant may be excluded from the co-actor set (K2-I11) is not yet fixed.
2. The bounded window and the adverse-inference weighting for a non-responding named actor (K2-P4) await A6 calibration.
3. Whether the deterministic grade-to-V4 map (K2-I4) needs a per-action_type override for strict-liability classes is unresolved.
4. The finalization cadence for two-phase record_time and the trust bound of the unanchored window (K2-P1 step 6) are governance parameters pending N6 and S4 tuning.

## K2 attribution, intent, causation and responsibility

### Purpose

This sub-section fixes who is answerable for an act, with what state of mind, through what causal contribution, and in what share. A K2 act is a specialization of an X1 occurrence (X1-I5); it is not a separate object that "emits a trace." The act-occurrence appends to the actor's own act register (S1 derivation); state changes it causes elsewhere are distinct effect-occurrences carrying a cause-ref, appended by the affected namespaces' owning R3 registers (see K2a K2-I10, K2c). K2b makes attribution non-repudiable, backdating-resistant, and resistant to laundering through shells, claimed autonomy, self-serving causal typing, and atomic fragmentation. Every attribution claim is a signed, staked assertion; contested where not independently established.

### Object model

- attribution: performer_ref, optional principal_ref, optional office_ref, optional delegation_ref, liability_role. performer_ref binds the X1 agent role (X1-I6); K2 liability roles refine that agent role, they do not replace the closed X1 role set.
- performer_ref values: a concrete B1 natural person or O1 organization, OR the reserved first-class value unknown. A structurally absent performer field is a distinct malformed condition (see K2-I13).
- signature: an R4-key signature over the act's canonical form, verifiable to performer_ref (K2-I15). Every co_actor_entry, causal_edge, and account is likewise a signed staked assertion.
- intent_annotation: grade in the single closed scale { deliberate, knowing, reckless, negligent, accidental }. Concealment is NOT a value on this scale; it is a separate S7 aggravator (K2-I17).
- co_actor_entry: actor_ref, liability_role in { principal, joint, aider, abettor, procurer }, causal_link_ref (traced against the X5 record and causal network), asserted_share (raw, unnormalized), signature.
- causal_edge: from_ref, to_ref, kind in { caused, contributed, material-contribution, market-share, enabled, prevented }, apportionment_standard, asserter_ref, confidence, contested flag. caused, contributed, material-contribution, and market-share are liability-bearing.
- operator_chain: ordered deployment/delegation links from the runtime performer up to a terminal responsible party; deployment_record captures the deployment decision and its known-capability grade.
- All occurrence-level fields (source_ref, confidence, norm_set_version_ref, and optional logical_stamp, prior_state_ref, new_state_ref) follow the single X1a occurrence field schema (C6); K2b does not re-list them.

### Invariants

- K2-I13 (malformed vs unknown). An act whose performer field is structurally absent SHALL be rejected at append as malformed. This is the only rejection ground for missing attribution.
- K2-I14 (unknown actor is first-class). An act naming performer_ref = unknown, or asserting a disputed performer, SHALL be accepted and carried contested, never rejected. This reconciles with X1-I13: there are no actorless-by-evasion K2 acts, only acts whose actor is unknown-and-so-named or disputed.
- K2-I15 (mandatory signature). Every K2 act SHALL carry a signature verifiable to the named performer_ref's R4 key; the K2a append gate (K2-P1) SHALL reject any act lacking one, and an unsigned act is recorded contested, never authoritative. K2-I15 binds every act, not only mediated ones. Every causal_edge and account an actor asserts is equally an identity-bound staked assertion; a knowingly false assertion is its own anti-value (perjury-class).
- K2-I16 (record_time and backdating). record_time is the MU Assertion Time: a provisional gate-assigned local sequence at commit, finalized non-repudiable on seal and anchor (see K2-P5, C40); backdating protection derives from the anchor, not the provisional stamp. occurrence_time is actor-supplied, descriptive, and contestable, never the ordering key (ordering is over logical_stamp per X1). An occurrence_time materially preceding record_time, or crossing a norm-epoch or deadline boundary relative to record_time, SHALL be inadmissible for norm and deadline purposes unless corroborated by an independent contemporaneous X1 (a witnessed access_event, a peer register anchor, or a counterparty co-signed X5) whose record_time falls in the claimed epoch. The burden of proving the earlier occurrence_time is on the asserter for any epoch- or deadline-crossing backdate.
- K2-I17 (intent grade, V4 map, concealment). The intent_annotation grade is the actor-side mental-state claim and the sole K2 input to V4 intent classification, mapped deterministically: { deliberate, knowing, reckless } to malicious; { negligent, accidental } to negligent. concealed is never a grade; it is an S7 aggravator applied on top when a knowingly false or materially misleading grade is proven, booked in addition to the corrected grade and routed to the perpetual-clawback/concealment class. The burden of reclassification to a higher grade is on the party asserting it, to a clear-and-corroborated standard. Confidence is an evidence-class scale tied to source type and corroboration and bound to the declarant's calibration TrackRecord; raw self-declared confidence never outweighs corroborated accounts.
- K2-I18 (omission-as-act). An omission SHALL be a K2 act if and only if a duty_ref imposes the required act and its deadline passes unfulfilled. Recording is independent of the breaching actor: the owed_to party or a duty steward may append the omission-act to a shared X5 duty register, and the standing duty_ref plus its unmet K7 commitment auto-generate the breach occurrence at the deadline (see K2c). A duty-breach occurrence carries no state_delta and is the carved X1-I1 exception.
- K2-I19 (contribution and probabilistic causation). Contribution is normally a but-for link. Because but-for fails for long-lag and cohort harm, a first-class material-contribution / market-share edge kind SHALL be available with an explicit apportionment standard, so cohort harm without an individual but-for link still yields a measurable affected set and per-actor share. The default "no edge, no liability" SHALL NOT stand for such cohort harm.
- K2-I20 (intervening cause and remoteness). A liability-bearing causal edge (caused, contributed, material-contribution, market-share) is a court or independent finding; an actor may only assert one as contested, never authoritatively type the edge on their own act. Remoteness SHALL NOT reduce an upstream share where the intervening act was procured, foreseeable, or performed in concert with the upstream actor.
- K2-I21 (responsibility share). Raw asserted_share values are per-owner signed assertions and are NOT constrained to sum to one at append. Normalization to one is a court-computed derived quantity from an A6 finding over the competing entries, recorded as a further occurrence; the invariant binds the adjudicated finding, not the co-owned raw rows. The co-actor set SHALL include every participant with a traced causal_link, verified against the X5 record and the causal network; a missing traced participant invalidates the partition rather than silently rebasing to one.
- K2-I22 (derivative liability). Derivative liability attaches to a principal act that either is recorded OR is established by an A6 finding to have occurred though unrecorded. Deliberately procuring or facilitating non-recording of the principal act is a distinct anti-value (obstruction / audit_evasion) chargeable to the procurer independent of the principal's record status.
- K2-I23 (operator chain and shell piercing). The operator_chain SHALL terminate in a B1 natural person or an O1 with an identified responsible natural officer having capacity. A chain terminating in a judgment-proof shell is a distinct control-defect: it pierces to the controlling beneficial owners and escalates to the deployer or commissioning party, rather than resting the booking on the empty shell.
- K2-I24 (autonomy floor). Autonomy of a deployed agent attenuates the principal's grade only for outcomes outside the agent's foreseeable operating envelope, and never below the deployer's knowledge of the agent's capability. Knowingly deploying a capable autonomous agent into a foreseeable-harm context is at minimum reckless regardless of runtime autonomy.

### Protocols

- K2-P5 (sign, attribute, append). Gate steps at append: (1) verify K2-I15 signature to performer_ref's R4 key, else reject; (2) if performer is unknown or disputed, accept and stamp contested (K2-I14); (3) confirm any cross-namespace effect carries a resolvable basis (K2c) and is recorded by the owning register, not written directly; (4) assign provisional record_time; finalize on seal and anchor.
- K2-P6 (verify mediated attribution). For any principal_ref or office_ref, the gate SHALL reject the attribution unless delegation_ref resolves under S1 to an active delegation covering this action_type for this performer at occurrence_time. An unverifiable delegation leaves full responsibility on the signing performer, never silently shifted to the named office. Resolve the operator_chain per K2-I23; on a shell terminus, pierce and escalate.
- K2-P7 (grade and classify). Record the intent grade; map to V4 per K2-I17; where a higher grade is asserted, run reclassification under the stated burden; on proven false self-grading, book the concealment aggravator in addition to the corrected grade.
- K2-P8 (assert causation and refer shares). Actors append causal_edges and asserted_shares as contested staked assertions; liability-bearing edges and normalization resolve only through an A6 finding (K2-I20, K2-I21). Self-serving superseding-cause and share-shifting edges have their evidentiary weight capped so volume cannot outweigh independently sourced accounts.

### Lifecycle and edge cases

- Forged act: unsigned or mis-signed acts naming a victim are rejected or held contested at the gate (K2-I15); they never stand authoritative.
- Backdate to beat a deadline: rejected for norm/deadline purposes absent independent contemporaneous corroboration; burden on the asserter (K2-I16).
- False principal / office: rejected unless delegation resolves; responsibility stays on the signer (K2-P6).
- Shell or AI chain: pierced to beneficial owners and deployer; deployment grade floors the principal at reckless (K2-I23, K2-I24).
- Unknown actor: accepted as first-class contested, preserved for later attribution (K2-I14).
- Omission: recorded to a co-owned X5 duty register by the owed_to party or steward, auto-generated at deadline (K2-I18).
- Concealed intent: a proven false grade adds the concealment aggravator on top of the corrected grade (K2-I17).
- Intervening / statistical cause: an actor cannot self-type its edge to escape; material-contribution supplies a share where but-for fails (K2-I19, K2-I20).
- Atomic fragmentation: aggregate V4 evaluation over the composing K3/K5 structure is handled in K2c; deliberate fragmentation is an aggravating basis and the aggregate is not defeated by per-act sub-threshold values.

### Interfaces

- K2a: enforces K2-I15 at the K2-P1 append gate; K2b supplies the signature, grade, and attribution objects.
- K2c: supplies the basis_binding precondition, effect-occurrence recording, omission register, and aggregate V4 evaluation.
- X1a: occurrence field schema (C6), closed role set X1-I6, logical_stamp causal order.
- V4: receives the deterministic grade-to-classification map and the concealment aggravator.
- S1 / R4: delegation resolution and identity-key verification. A6: adjudicates liability edges, share normalization, reclassification, unrecorded-principal findings. S7: applies the concealment aggravator. K7 / X5: duty commitments and the co-owned duty register.

### External bindings

- record_time = Meta-Universe Assertion Time (MU Event two-time model); valid_interval, where used, is a MOS extension over that model (cite MU-V2-CORE-011 Lifecycle), never collapsed with the other times.
- Identity keys are R4; delegations are S1; inviolable-rights keying is A18; principals resolve to B1 or O1.

### Open questions

1. The numeric de-minimis contribution floor and the apportionment weights for material-contribution / market-share edges are delegated to N6 and not yet fixed.
2. The exact function binding declared confidence to a declarant's calibration TrackRecord, and the numeric cap on self-serving causal-edge weight, remain to be specified.
3. Whether autonomy may ever attenuate a principal's grade below reckless for envelope-external outcomes, or whether reckless is an absolute floor, is unresolved.

## K2 consequences: outcomes, consent, value and anti-value

### Purpose

This sub-section governs what follows from an act once it is an occurrence: the state changes it causes, the consent basis it must carry, the value it moves, and the anti-value it may incur. It closes the corpus ontology (a K2 act IS an X1 occurrence, per X1-I5) on the consequence side. An act does not "emit a trace"; the act is itself the actor-caused occurrence. Its downstream effects are SEPARATE occurrences, each carrying a cause-ref back to the act. K2c fixes where each of these lands, who controls it, when its supporting basis had to exist, and how value and anti-value attach to the flow record rather than to the actor's bare say-so. It also supplies the anti-evasion machinery for the consequence layer: forced recordability for victims, aggregate anti-value over composing structures, concrete payers for diffuse harm, and minimization of the surveillance surface that recording of consequences would otherwise create.

### Object model

- effect_occurrence: a distinct X1 occurrence recording one state change caused by an act. Carries cause_ref (to the act-occurrence), object_ref (or a batched member set under a declared grain, per X1-I1), optional prior_state_ref and new_state_ref, and the canonical occurrence field schema defined in X1a (mandatory source_ref, confidence, norm_set_version_ref). Appended to the affected namespace's owning R3 register.
- flow_record: the value view of an occurrence. Carries value_flow_ref (V3) and any anti_value_booking. Present on any occurrence, act or actorless.
- anti_value_booking: kind in the V4 classification {negligent, malicious, concealed}, magnitude, axis_ref, and an apportionment set (per-atomic-act shares when the booking attaches to a composing K3/K5 structure). Derived from the K2b mental-state grade via the published deterministic map; concealment is layered as a separate S7 aggravator, never produced by the mental-state scale itself.
- basis_binding: basis_kind in {x5_interaction, consent, statutory, judicial, emergency}, instrument_ref, the instrument's witnessed record_time, and its valid_interval.
- access_event: reader_ref, purpose_binding, minimization_envelope, target_ref. Owned by the reading subject's namespace; a member of the non-recursive S4 audit tier.
- snapshot_ref: a minimized, sealed as-of freeze of counterparty fields marked required by the action_type, subject-visible and subject-gated for any read beyond the actor's own evidentiary use.
- rights_touching marker: set on acts keyed to A18 inviolable rights and bodily/personhood interests, independent of any namespace read/write.
- restoration_binding: payer_ref set, joint_and_several flag, and backstop_fund_ref for genuinely emergent occurrences.
- times: occurrence_time, record_time, valid_interval (see K2-I28).

### Invariants

K2-I26 (value over the flow record). Value flows and V4 bookings attach to an occurrence's flow record, not to the actor identity. For an actorless occurrence, attributable V4 liability is DEFERRED until an act or an apportionment (K2-I36) supplies a responsible transformer; the flow itself is still recorded. This matches Justice and X1-I26.

K2-I27 (act-occurrence versus effect-occurrences). The act-occurrence SHALL append to the ACTOR's own act register, which the actor controls under the S1 derivation rule. Every state change the act causes in another namespace SHALL be a distinct effect_occurrence appended to that namespace's owning R3 register, controlled by that namespace's owner, and linked to the act by cause_ref. No act writes directly into another owner's register; the owning gate records the effect.

K2-I28 (three times, never collapsed). Each occurrence SHALL carry occurrence_time (descriptive, contestable), record_time (= Meta-Universe Assertion Time, the witnessed append position), and, where a validity window applies, valid_interval. valid_interval is a MOS extension over the two-time MU Event model (see MU-V2-CORE-011 Lifecycle); it SHALL NOT be presented as native MU Event vocabulary. The three times are never merged.

K2-I29 (basis precedes the act; baseless act is the wrong). An act that touches another agent's rights SHALL carry a resolvable basis_binding whose supporting instrument (access_event or consent) has a witnessed record_time STRICTLY PRECEDING the act's record_time and a valid_interval covering the act's occurrence_time. A later-appended basis is invalid and the act is baseless (V4 unauthorized_access). "Touching another's rights" is keyed to the A18 inviolable-rights and bodily/personhood interest class, NOT to a namespace read/write: an unconsented act on a person is the wrong even when it writes nothing in that person's namespace.

K2-I30 (reads are owned, audited, non-recursive). Every read of the occurrence stream SHALL emit an access_event owned by the READING subject, default-deny and composition-limited. Reading another party's access history requires an elevated basis (judicial or explicit consent) and is itself recursively S4-logged. Audit-tier appends are NOT Rule-4 mutations and generate no further occurrence; they seal in batches with per-batch inclusion proof. This closes the read-to-write-to-read regress.

K2-I31 (snapshot minimization). A Rule-3 snapshot of another person's namespace data SHALL be minimized to the fields the action_type marks required, marked subject-visible and subject-enumerable, and held as a sealed snapshot_ref that resolves through the subject's gate for any read beyond the actor's own evidentiary use. No snapshot may exfiltrate counterparty fields outside the action_type's required set.

K2-I32 (aggregate V4 threshold; grade map). The V4 anti-value threshold SHALL be evaluated over the AGGREGATED flow of all acts composing one K3 process, one K5 project, or one harmful outcome (resolved through the causal network and composition references), NEVER per atomic act. Deliberate fragmentation to keep each act sub-threshold is an aggravating basis. The aggregate booking attaches to the composing structure with shares apportioned across the atomic acts. The booking kind is derived from the K2b mental-state grade by the deterministic map: {deliberate, knowing} to malicious; {reckless, negligent} to negligent; accidental to no attributable V4 absent another basis. Concealment (K2-I38) is applied on top as a separate S7 aggravator and is never a point on the mental-state scale.

K2-I33 (forced dual-channel recordability). Any agent MAY append to their OWN register a rights-touching occurrence naming another agent in the agent role, carried as contested (never authoritative on its own). Such an occurrence is a valid A6 case-opener obligating the named actor to append a counter-account within a bounded window; non-response triggers an explicit adverse inference (the contested account's confidence is raised, silence is not rewarded). For rights-touching and performative action_types the act SHALL additionally append an inclusion-promised occurrence, by reference, to the affected counterparty's register as a condition of taking effect, so the counterparty independently holds a promise the actor cannot later suppress and non-appearance is detectable non-recording. No act touching another's rights depends solely on the actor choosing to record it.

K2-I34 (unknown actor is first-class). An occurrence SHALL be rejected at append ONLY when the performer field is structurally absent (malformed). An occurrence asserting a harm whose performer is unknown-but-named-as-unknown, or disputed, SHALL be accepted and carried contested, never rejected. "Unknown actor" is a valid performer_ref value distinct from a missing field.

K2-I35 (omission recording independent of the breacher). On a duty_ref deadline passing without the required act, the owed_to party or a duty steward MAY append an omission-act to a shared X5 duty register (co-owned, not the breacher's sole namespace), and the standing duty_ref plus its unmet K7 commitment SHALL auto-generate a breach occurrence at the deadline. Recording never depends on the breaching actor. Duty-breach occurrences carry no state_delta; X1-I1 SHALL admit them as the declared exception to mutation-triggered occurrence creation.

K2-I36 (emergent occurrences resolve to a concrete payer). The emergent classification is barred wherever coordination, a common plan, or an organizer can be shown; any such evidence reclassifies the occurrence to a joint act with named co-actors under the K2b liability roles. For genuinely emergent occurrences, restoration resolves by (a) joint-and-several obligation across all identifiable contributors above a de-minimis floor, and (b) a named collective backstop fund (commons or insurance pool) that discharges restoration to victims when no contributor is individually attributable, then subrogates as contributors are found. A booking against an occurrence SHALL ALWAYS resolve to a concrete payer and never terminate at an ownerless record. Deliberately engineering sub-threshold contributions to a known aggregate harm is itself a K2 act (procurement or reckless contribution), unshielded by the sub-threshold floor.

K2-I37 (dispute-freeze and derivative anchoring). Once an A6 case references a co-owned interaction record, no co-controller may narrow, revoke or reduce any counterparty's or the court's projection of that record below its state at interaction time; co-ownership grants a veto on external onward-disclosure to strangers, never a veto on a counterparty's own access to a shared interaction, and never on judicial access. Derivative liability attaches to a principal act that either is recorded OR is established by an A6 finding to have occurred though unrecorded; deliberately procuring or facilitating non-recording of a principal act is itself a distinct anti-value (obstruction or audit_evasion) chargeable to the procurer independent of the principal's record status.

K2-I38 (concealment as anti-value). A knowingly false or materially misleading intent grade is its own aggravating anti-value (concealment), booked IN ADDITION to the corrected grade, not merely a correctable field. Reclassification to a higher grade bears on the party asserting it, to a clear-and-convincing standard; proven false self-grading routes into the perpetual-clawback/concealment class. A grain declared coarse enough to obscure a state-changing harmful act, or an operator-set granularity below the N6 steward floor, is rejected as audit_evasion.

### Protocols

K2-P9 (act to effect to valuation). (1) Append the act-occurrence to the actor's register with a K2-I15 signature verifiable to the named actor_ref's R4 key; an unsigned act is recorded contested, never authoritative. (2) For each caused state change, the owning gate appends an effect_occurrence with cause_ref (batched under the declared grain for mass acts). (3) Attach the value flow to the flow record. (4) Resolve the composing K3/K5/outcome structure and evaluate the aggregate V4 threshold (K2-I32); if crossed, book anti-value against the composing structure with apportioned shares. (5) Map the K2b grade to the V4 kind and apply any concealment aggravator.

K2-P10 (basis and consent gate). (1) For any rights-touching act, resolve basis_binding and verify its instrument's witnessed record_time strictly precedes the act's record_time and its valid_interval covers occurrence_time; otherwise mark the act baseless (V4 unauthorized_access). (2) For rights-touching or performative acts, append the inclusion-promised occurrence to the counterparty's register as a condition of effect. (3) Minimize any Rule-3 snapshot per K2-I31 and seal it subject-gated. (4) Emit the K2-I30 access_event on every read into another's namespace.

K2-P11 (victim-originated case-opener and omission). (1) Accept a victim-originated contested account naming another in the agent role and open the A6 case (K2-I33). (2) Start the bounded counter-account window; on non-response, apply the adverse inference. (3) On a duty deadline lapse, admit an omission-act to the shared X5 duty register and auto-generate the breach occurrence (K2-I35). (4) For emergent harm, resolve the payer set or route restoration to the backstop fund (K2-I36).

### Lifecycle and edge cases

- Effect fan-out: a high-fan-out act appends one act-occurrence plus one grouping effect_occurrence carrying a bounded effect-index at the declared mutation grain, not one occurrence per touched object (X1-I1 as reconciled).
- Attempt and omission: an attempt that changes state is a recorded act with its own effect_occurrences; a pure omission produces no state_delta and is recorded per K2-I35 against the shared duty register, resolving the former open question on whether omissions need their own occurrence (they do, as no-state-delta breach occurrences).
- Backdated basis: an instrument appended at or after the act's record_time cannot cure baselessness; the act stands baseless regardless of the later reference.
- Actorless-to-act correction: downgrading an agent-caused occurrence to actorless is a contestable, correctable misclassification (a supersession edge of kind correction), never a silent option; V4 liability is deferred, not extinguished, until a transformer is supplied.
- Concurrent conflicting effects: two effect_occurrences asserting different new_state_ref for one object both persist; the projection surfaces a conflict-tagged multi-value state or a deterministic representative by logical_stamp order, with the losing account retained.
- Revocation: a co-controller revoking their side of a co-owned record renders their side non-identifying in all co-owners' projections within the bounded staleness maximum, but never below interaction-time state once an A6 case references it.

### Interfaces

- To X1a/X1c: the act and its effects use the canonical X1a occurrence field schema; harm-tracing over effect_occurrences follows X1c with court-sealed, necessity-bounded projection.
- To K2b: the mental-state grade (K2-I17), signature (K2-I15), liability roles refining the X1-I6 agent role, and delegation checks feed K2c valuation and attribution.
- To V3/V4: flow records carry value; anti_value_booking classifies over the aggregated flow.
- To A6/Courts: victim-originated accounts open cases; shares, superseding-cause edges and grade reclassification are court findings recorded as further occurrences.
- To S1/S4/S5/S7: derivation control, access logging, sensing budgets, and aggravators.

### External bindings

- record_time = Meta-Universe Assertion Time; valid_interval is a MOS extension cited to MU-V2-CORE-011 Lifecycle, not native MU Event vocabulary.
- A18 supplies the inviolable-rights class keying rights-touching acts.
- B1/O1 supply the natural-person or accountable-officer terminus for operator and deployment chains referenced from K2b.
- X5 supplies co-owned interaction and duty registers; K7 supplies the commitments whose breach auto-generates omission occurrences.
- K3/K5 supply the composing structures over which aggregate V4 is evaluated.

### Open questions

1. Capitalization source and subrogation priority of the collective backstop fund used to discharge restoration for genuinely emergent occurrences (K2-I36 (b)).
2. The numeric de-minimis contribution floor for joint-and-several emergent restoration, and whether it varies per V4 axis.
3. The duration of the bounded counter-account window before the K2-I33 adverse inference triggers.
4. The exact magnitude bands separating negligent from malicious in the grade-to-V4 map at a given aggregated flow size.

## X1 core: the occurrence and its relation to acts

### Purpose

X1 is the atomic record of something that happened. This sub-section fixes the occurrence primitive and its one canonical field schema, states how a K2 act relates to an occurrence, and sets the ownership, attribution, causal-order, and subject-protection invariants that X1b (integrity and timeline) and X1c (harm, phenomena, interpretation) build on without redefining. The governing commitments: everything that happens is representable as an occurrence; a K2 act is not a separate object that emits a trace but IS an occurrence that carries an agent; the record cannot be silently withheld, forged, backdated, or minimized below a harmful act's grain; and a named person is never surveilled into another's register without a stake.

### Object model

- occurrence: the atomic happening. Canonical field schema (X1-I3), referenced by X1b/X1c, never re-listed there.
  - Mandatory: `source_ref` (provenance of the assertion), `confidence` (evidence-class grade, X1-I4), `norm_set_version_ref` (the norm epoch under which it is asserted).
  - Optional: `logical_stamp` (causal-order position, the ordering authority), `prior_state_ref`, `new_state_ref`, `value_flow_ref` (flow record for V3/V4 booking), `cause_ref` (link from an effect-occurrence to its causing act), `performer_ref` (may hold the first-class value `unknown`).
- participant binding: `{ participant_ref, role, liability_role? }`. `role` is drawn from the closed X1-I6 set. `liability_role` refines the `agent` role only.
- account_link: `{ from, to, relation }`, `relation` in {corroborates, conflicts} only.
- supersession_edge: `{ from, to, kind }`, `kind` in {correction, retraction, revaluation}; adjudicated_finding supersession is a specialization.
- snapshot_reference: a sealed, minimized as-of freeze of counterparty fields (X1-I7), not a copy.

### Invariants

- X1-I1 (fail-closed, act/effect split, one-per-grain, omission exception): The gate is fail-closed; a state mutation whose occurrence cannot be durably recorded SHALL NOT take effect (write path in X1-P1). A K2 act appends exactly one act-occurrence to the ACTOR's own act register, which the actor controls (per S1 derivation). Each state change the act causes in another namespace is a distinct EFFECT-occurrence appended to that namespace's owning R3 register, controlled by that namespace's owner, linked to the act by `cause_ref`. "Exactly one" binds per declared mutation grain, not per touched object: a mass act appends one grouping act-occurrence plus a bounded batched effect-set or effect-index (X1-I16 grain). A duty-breach occurrence that carries no `state_delta` is an explicit exception: an omission is recorded as an act-occurrence with no target-namespace mutation.
- X1-I2 (account_link narrowed): An account_link relates accounts of the same underlying happening and its `relation` is closed to {corroborates, conflicts}. Correction, retraction, and revaluation never travel on account_link; they travel on the single supersession edge (X1-I8).
- X1-I3 (one canonical occurrence schema): Every occurrence SHALL carry the mandatory fields `source_ref`, `confidence`, `norm_set_version_ref`, plus the optional fields listed in the object model. Absence of `source_ref` is a malformed record. This schema is canonical for the whole X1 meta-object; X1b and X1c reference it and SHALL NOT re-list divergent mandatory fields.
- X1-I4 (confidence is an evidence class): `confidence` is an evidence-class scale tied to source type and corroboration and bound to the declarant's calibration TrackRecord, not a free self-assertion. Raw self-declared confidence SHALL NOT outweigh independently corroborated accounts, and confidence never substitutes for consent to be recorded.
- X1-I5 (an act IS an occurrence): A K2 act is a specialization of an X1 occurrence: an occurrence carrying at least one `agent` binding. An actorless occurrence books no intent against any subject. The gate SHALL bind the authorizing agent in the `agent` role whenever a state-change occurrence results from an agent-authorized mutation request or names an instrument or object under an agent's control; actorless classification SHALL require positive provenance of no agent (natural, sensor, or registrar source). Downgrading an agent-caused occurrence to actorless is a contestable, correctable misclassification, never a silent option.
- X1-I6 (closed roles, agent refinement): Occurrence roles are closed to {agent, patient, instrument, witness, beneficiary} and are asserted, not inferred. The coarse `agent` role MAY carry an optional K2 `liability_role` in {principal, joint, aider, abettor, procurer} refining it; K2 cross-references this enumeration rather than defining its own occurrence roles.
- X1-I7 (snapshot minimization): A Rule-3 as-of snapshot of another person's namespace data SHALL be minimized to the fields the `action_type` marks required, marked subject-visible and subject-enumerable, and held as a sealed reference that resolves through the subject's gate for any read beyond the actor's own evidentiary use.
- X1-I8 (conflict preservation and deterministic fold, one supersession): Conflicting accounts of the same happening both persist and are never merged; adjudication defers to a later occurrence. The projection is a total, deterministic conflict-fold without merging: it either surfaces all live accounts as a conflict-tagged multi-value state, or picks a deterministic representative by `logical_stamp` order while flagging the conflict and retaining the losing account. Determinism holds pre-adjudication. Supersession is one edge type with `kind` in {correction, retraction, revaluation}; an adjudicated_finding supersession is a specialization of that edge.
- X1-I9 (co-ownership and bystander protection): Every named natural-person participant, regardless of role, co-owns the occurrence to at least these rights: subject-enumerability, a minimization right (pseudonymous or coarse reference unless a basis exists to name them), and a contest and projection-redaction right. Binding an identifiable person into any participant role is itself an act touching that person's rights, requiring a resolvable `basis_binding` or a k-anonymized non-identifying reference.
- X1-I10 (subject-enumerability): Any occurrence binding an identifiable natural person in any role is enumerable by that person on request. Person-naming actorless observations require a lawful observation basis or a non-identifying or k-anonymized reference. Occurrences observed inside a person's own namespace are controlled by that person; an observing registrar holds at most a co-owned assertion subject to the owner's gate.
- X1-I11 (value over the flow record): An occurrence MAY carry a `value_flow_ref` booking a V3 flow or V4 anti-value over its flow record. Value is priced over the occurrence's flow record, not restricted to agent-caused occurrences. For an actorless occurrence, attributable V4 liability is deferred until an act or an apportionment (X1c) supplies a responsible transformer. A booking SHALL always resolve to a concrete payer and never terminate at an ownerless record.
- X1-I12 (causal order over logical_stamp): The causal graph SHALL be acyclic and cause-before-effect over the `logical_stamp` causal order. `occurrence_time` is descriptive, contestable evidence of ordering and is never the ordering key.
- X1-I13 (unknown actor is first-class): Reject at append ONLY when the performer field is structurally absent (a malformed record). An occurrence asserting a harm with an unknown-but-named-as-unknown or disputed performer SHALL be accepted and carried contested, never rejected. `unknown` is a valid `performer_ref` value, distinct from a missing field.
- X1-I14 (victim-originated occurrence, forced dual-channel): Any agent MAY append to their OWN register a rights-touching occurrence naming another agent in the `agent` role, carried contested and never authoritative on its own. Such an occurrence is a valid A6 case-opener that obligates the named actor to append a counter-account within a bounded window; non-response triggers an explicit adverse-inference (the contested account's confidence is raised, silence not rewarded). No act touching another's rights depends solely on the actor choosing to record it.
- X1-I15 (co-witnessed dual-append): A rights-touching or performative act SHALL append an inclusion-promised occurrence, by reference, to the affected counterparty's register as a condition of taking effect, so the counterparty independently holds a promise the actor cannot later suppress. Non-appearance in the counterparty register is detectable non-recording, not an invisible omission.
- X1-I16 (granularity floors): Granularity floors are steward-set (N6) per `action_type` and are never owner-settable below the floor. Any act whose flow crosses or plausibly crosses a V4 threshold SHALL be recorded at individual act grain regardless of any declared aggregation. A grain fine enough to individuate a person's movements is person-grain data under S5 and timeline discipline; a grain coarse enough to obscure a state-changing harmful act is rejected as `audit_evasion`.

### Protocols

- X1-P1 (record a state change, write path): Validate the canonical schema and role bindings, bind the agent per X1-I5, then synchronously append to a fast local write-ahead segment that returns an `inclusion_promise`. Fail-closed applies only on failure to durably record the promise. Merkle sealing and witnessing defer to a bounded cadence (X1b). An explicit bounded degraded mode admits emergency acts against a provisional promise with mandatory backfill, so a witnessing outage cannot freeze all state change. `record_time` is two-phase: a provisional gate-assigned local sequence at commit, finalized to non-repudiable on seal and anchor; backdating protection derives from the anchor, not the provisional stamp.
- X1-P2 (record an actorless observation): Assert `source_ref` provenance (natural, sensor, or registrar). Any person-naming binding requires a lawful observation basis or a k-anonymized non-identifying reference (X1-I9, X1-I10). Control of an observation made inside a person's namespace vests in that namespace's owner.
- X1-P3 (take an as-of snapshot, Rule 3): Freeze only the `action_type`-required counterparty fields as a minimized, subject-enumerable sealed reference that resolves through the subject's gate (X1-I7).
- X1-P4 (append an account or supersession): Every account and causal assertion is a staked, identity-bound, K2-I15-signed assertion with a perjury-as-anti-value hook. Same-happening relations use account_link {corroborates, conflicts}; corrections use the supersession edge {correction, retraction, revaluation}. The conflict-fold (X1-I8) is applied deterministically; raw self-serving confidence cannot outweigh corroborated accounts.

### Lifecycle and edge cases

- (a) Omission: on a `duty_ref` deadline passing, the omission is recorded as an act-occurrence with no `state_delta` (X1-I1 exception), referencing the open duty situation; recording does not depend on the breaching actor.
- (b) Actorless to attributable: an actorless occurrence carrying a `value_flow_ref` books no intent until an act or apportionment supplies a transformer; the deferred booking then resolves to a concrete payer (X1-I11).
- (c) Unknown or disputed performer: accepted and carried contested (X1-I13); never a ground for refusing to register a known harm.
- (d) Backdating: an `occurrence_time` materially preceding `record_time`, or crossing a norm-epoch or deadline boundary relative to `record_time`, is inadmissible for norm and deadline purposes unless corroborated by an independent contemporaneous X1 whose `record_time` falls in the claimed epoch; the burden is on the asserter.
- (e) Participant-side revocation: an occurrence persists in co-owners' registers; the revoking party's side is rendered non-identifying within a bounded hard-maximum staleness horizon, and revocation never overrides a counterparty's own access to a shared interaction or judicial access.
- (f) Mass act: fan-out is a bounded, governed effect-set or effect-index under a declared grain (X1-I1, X1-I16), not N independent occurrences.

### Interfaces

- To K2: a K2 act specializes this occurrence (X1-I5); K2 liability roles refine `agent` (X1-I6); the signature, delegation, and basis-timing gates that K2 imposes run on top of X1-P1.
- To X1b: `logical_stamp` is the ordering authority (X1-I12); the canonical schema (X1-I3) and supersession edge (X1-I8) are consumed unchanged; witnessing and two-phase `record_time` finalize the X1-P1 write path.
- To X1c: harm-tracing, phenomena, situations, and interpretations read occurrences and their flow records; value and V4 attach per X1-I11.
- To S1/S4/S5: register control derives from S1; reads are S4-logged; person-grain output is S5-budgeted. To A6/A18: victim-originated occurrences (X1-I14) open cases; rights-touching class keys to A18.

### External bindings

- `record_time` = Meta-Universe Assertion Time (MU Event two-time model).
- `occurrence_time` = Meta-Universe Occurrence Time (descriptive, contestable evidence only).
- `valid_interval` is a MOS extension over the two-time MU Event model, per the MU Lifecycle three-times separation (MU-V2-CORE-011); it is not part of the base MU Event vocabulary.
- The three times SHALL never be collapsed into one another.

### Open questions

1. The magnitude and decay of the adverse-inference confidence raise on non-response to a victim-originated case-opener (X1-I14) awaits A6 calibration.
2. The k-anonymity floor parameters for non-identifying participant and observation references (X1-I9, X1-I10) await N6 and S5 fixing.
3. The operational test for "plausibly crosses a V4 threshold" that forces individual-grain recording (X1-I16) needs a steward-published standard.
4. The hard-maximum staleness horizon for participant-side revocation (lifecycle (e)) is to be bound normatively in S2 and confirmed against X1b bounded-cadence anchoring.

## X1 the Semantic Timeline: registration, time and reconstruction

### Purpose

X1b governs how occurrences defined in X1a are registered onto the Semantic Timeline, how they are ordered in the absence of a global clock, and how any past state is reconstructed deterministically and auditably. It owns the three-time model, the write path, the single supersession mechanism, and the operability envelope (anchoring, durability, blast-radius, read discipline). It does not redefine the occurrence (X1a owns the canonical field schema) and it does not define harm-tracing, phenomena, situations, or interpretations (X1c). A K2 act is not a separate object that emits a trace: the act is itself an occurrence registered here, and each effect it causes is a distinct occurrence carrying a cause-ref back to the act.

### Object model

X1b introduces no new mandatory occurrence fields. Every occurrence conforms to the canonical X1a schema (mandatory source_ref, confidence, norm_set_version_ref; optional logical_stamp, prior_state_ref, new_state_ref). X1b relies on and adds the registration-layer objects:

- **record_time**: two-phase append stamp. Phase one is a provisional gate-assigned local sequence, monotonic within a shard, available at commit. Phase two finalizes to a non-repudiable value on seal and anchor.
- **logical_stamp**: the causal clock (vector or HLC). It is the ordering authority.
- **occurrence_time**: the actor-supplied or observer-supplied wall-clock claim. Descriptive and contestable evidence of ordering, never the ordering key.
- **valid_interval**: the interval over which the recorded fact is asserted to hold. A MOS extension over the two-time MU Event model.
- **inclusion_promise**: a signed receipt returned at durable append, redeemable against later seal and anchor.
- **supersession_edge**: the single revision primitive, kind {correction, retraction, revaluation}, carrying target_ref, basis, and a K2-I15 signature.
- **append_token**: a short-lived signed capability plus resolved authorizing_context, precompiled out of band by S1/N6.
- **reconstruction_frontier**: a witnessed root-of-roots anchor, or a per-shard vector of last-included sequences.
- **effect_index**: a bounded grouping descriptor letting one occurrence carry a batched effect-set under a declared granularity.

### Invariants

- **X1-I14** (three times): record_time (MU Assertion Time), occurrence_time (descriptive claim), and valid_interval (MOS extension) are three distinct first-class times and SHALL NEVER be collapsed into one another.
- **X1-I15** (record_time is two-phase): record_time SHALL be a provisional gate-assigned local sequence at commit, finalized to non-repudiable status only on segment seal and anchor. Backdating protection derives from the anchor, not from the provisional stamp; the unanchored window is bounded by the anchoring cadence of X1-I22.
- **X1-I16** (logical order is the authority): there is no global wall clock. Causal ordering SHALL be taken over logical_stamp; occurrence_time is descriptive, contestable evidence only. Occurrences whose logical_stamps are incomparable are concurrent. The causal graph SHALL form an acyclic order over logical_stamp with every cause preceding its effect over logical_stamp.
- **X1-I17** (write path, fail-closed): a mutation SHALL take effect only after a synchronous durable append to a fast local write-ahead segment returns an inclusion_promise. Fail-closed means failing only on inability to durably record the promise; Merkle sealing and witnessing defer to a bounded cadence. A bounded degraded mode MAY admit emergency acts against a provisional promise with mandatory backfill, so a witnessing outage SHALL NOT freeze all state change.
- **X1-I18** (effect fan-out is bounded): a single occurrence MAY carry a batched effect-set (member object_refs under a shared prior-state and new-state descriptor) at a declared granularity. X1a X1-I1 "exactly one occurrence" means exactly one per declared mutation grain, not one per touched object. A mass act appends one grouping occurrence plus a bounded effect-index, never N independent occurrences.
- **X1-I19** (one supersession mechanism): correction, retraction, and revaluation SHALL be expressed only as a supersession_edge, each a K2-I15-signed staked assertion. account_link is reserved for same-underlying-happening relations {corroborates, conflicts} only and SHALL NOT carry refine or retract semantics. Adjudicated-finding supersession is a specialization of the supersession_edge.
- **X1-I20** (reconstruction cut is a frontier): an as-of view SHALL name a witnessed root-of-roots anchor or a vector/HLC frontier fixing, per shard, the last included sequence. Reconstruction folds each shard to its frontier. Determinism is defined over the frontier, never over an ungrounded scalar wall-clock instant.
- **X1-I21** (conflict-fold is total and deterministic): the projection SHALL, without merging records, either surface all live accounts as a conflict-tagged multi-value state, or pick a deterministic representative by logical_stamp order while flagging the conflict and retaining the losing account. Determinism holds even before adjudication.
- **X1-I22** (anchoring is hierarchical with bounded fan-in): registers SHALL anchor into regional witness tiers, tiers into a higher tier, at a stated cadence per tier. Mutual anchoring is to a bounded rotating quorum of peers, not all-to-all. This yields equivocation detection at bounded per-register cost with no global clock.
- **X1-I23** (durability separated from queryability): all sealed segments SHALL have permanent durability and provable inclusion (cold, proof-retrievable). Hot online queryability is scoped to a governed horizon and declared occurrence classes; older segments are retrievable on demand with proof-of-inclusion. Reconstructability is preserved without unbounded hot storage.
- **X1-I24** (value over the flow record): value flows and V4 bookings attach to any occurrence's flow record. For an actorless occurrence, attributable V4 liability is deferred until an act or an apportionment (X1c) supplies a responsible transformer; the flow is recorded, the liability is not orphaned onto an ownerless record.
- **X1-I25** (blast-radius is bounded): downstream traversal is guaranteed only within a declared depth and breadth inside the owner's own trust boundary. Cross-owner blast-radius is best-effort asynchronous notification: a retraction emits supersession events that downstream owners consume, not a synchronous global query. Per-occurrence causal_deps fan-out is bounded in N6 governance.
- **X1-I26** (read minimization and disclosure): every timeline-read and as-of reconstruction contract SHALL carry an explicit minimization envelope (time window, namespace or act-type scope, purpose binding) enforced by the gate; whole-timeline reconstruction is forbidden absent a specific per-scope judicial necessity finding. Onward disclosure of a co-owned joint or X5 record to a third party requires consent from ALL co-controllers (a single co-controller may access, not release onward); revocation staleness is bounded to a hard maximum, with the revoking party's side rendered non-identifying in all co-owners' projections immediately on revocation.
- **X1-I27** (audit tier is non-recursive): S4 access-events are owned by the reading subject, default-deny and composition-limited. Reads of another party's access history require an elevated basis (judicial or explicit consent) and are recursively S4-logged. Audit-log appends are NOT themselves Rule-4 mutations; the audit tier is a distinct non-recursive tier, batched or sampled with per-batch inclusion proof, closing the read-to-write-to-read regress.

### Protocols

- **X1-P5** (register a change): (1) resolve and verify the append_token signature and template version hash, not a live unbounded delegation-chain walk; (2) verify the occurrence conforms to the X1a canonical schema and, for a K2 act, that it carries a K2-I15 signature verifiable to the named actor_ref R4 key (an unsigned act is recorded as contested, never authoritative); (3) assign a provisional record_time as a local monotonic sequence; (4) durably append to the write-ahead segment and return the inclusion_promise; (5) enqueue for seal and anchor at the bounded cadence. Fail closed only if step 4 cannot durably record the promise.
- **X1-P6** (as-of reconstruction): name a reconstruction_frontier; fold each shard to its frontier position; apply the conflict-fold of X1-I21 to competing accounts; enforce the minimization envelope of X1-I26. Cold segments are rehydrated with proof-of-inclusion as needed.
- **X1-P7** (supersession and propagation): append a signed supersession_edge referencing the target; re-project the bounded downstream set inside the owner trust boundary; emit asynchronous supersession notifications to cross-owner subscribers per X1-I25. The superseded account is retained, queryable for audit.
- **X1-P8** (timeline read): verify a basis (consent or judicial_access_contract) covering the minimization envelope; log an S4 access-event to the reading subject's non-recursive audit tier; enforce all-co-controller consent for onward disclosure of co-owned records; debit the composition and, for person-grain output, an S5-equivalent budget.

### Lifecycle and edge cases

- (a) Unanchored window: between provisional record_time and anchor a record is durable but not yet non-repudiable; trust is bounded by the anchoring cadence.
- (b) Late arrival under clock skew: a late-arriving occurrence MAY carry a true earlier occurrence_time; logical_stamp governs ordering and the causal graph is not reordered by the wall-clock claim.
- (c) Conflict: competing accounts of one happening both persist, conflict-tagged; a deterministic representative is chosen by logical_stamp; adjudication is a later occurrence expressed as a supersession specialization.
- (d) Partition and degraded mode: emergency acts commit against a provisional promise with mandatory backfill on recovery; equivocation is checked at re-anchor against the rotating quorum.
- (e) Backdating: an occurrence_time materially preceding record_time, or crossing a norm-epoch or deadline boundary relative to record_time, is inadmissible for norm and deadline purposes unless corroborated by an independent contemporaneous X1 (a witnessed access_event, a peer register anchor, or a counterparty co-signed X5) whose record_time falls in the claimed epoch. The burden is on the asserter for any epoch or deadline-crossing backdate.
- (f) Mass act and granularity: a high-fan-out act appends one grouping occurrence plus a bounded effect-index. Granularity floors are steward-set (N6) per action_type and are never owner-settable below the floor; any act whose flow crosses or plausibly crosses a V4 threshold SHALL be recorded at individual act grain regardless of any declared aggregation, and a grain coarse enough to obscure a state-changing harmful act is rejected as audit_evasion.
- (g) Cold retrieval: an aged segment is rehydrated on demand and its inclusion proven against its tier anchor.

### Interfaces

- To X1a: X1b consumes the canonical occurrence unchanged. The act IS an occurrence; there is no act_ref field on the occurrence and no separate emitted trace. Effects are distinct occurrences carrying a cause-ref to the act.
- To K2: a K2 act is an occurrence registered by X1-P5. The act-occurrence appends to the actor's own act register; the state changes it causes append as effect-occurrences to the affected namespaces' owning R3 registers, linked by cause-ref. The append gate enforces the mandatory K2-I15 signature.
- To X1c: harm-tracing, phenomena, and situations consume frontiers (X1-P6) and supersession edges (X1-P7); person-grain reachability output is release-registered and budget-debited at production, not on-demand here.
- To S1/N6: append_tokens are issued out of band; granularity floors and causal_deps fan-out bounds are N6-governed.
- To S4/S5: reads route through the non-recursive audit tier (X1-I27); person-grain output debits an S5-equivalent budget.
- To V3/V4: value and anti-value book over the occurrence flow record (X1-I24).

### External bindings

- MU Event model: record_time maps to MU Assertion Time and occurrence_time maps to MU Occurrence Time, satisfying the two-time model that requires at least one time. valid_interval has no basis in the two-time Event model and is declared a MOS extension, introduced under MU-V2-CORE-011 Lifecycle (valid and knowledge time). The three MOS times are never collapsed (X1-I14).
- Anchoring tiers (X1-I22) bind to the R-cluster regional witness tiers and their rotating quorums.

### Open questions

1. Per-tier anchoring cadence and rotating-quorum size (X1-I22) are N6 parameters not yet fixed; the equivocation-detection latency bound depends on them.
2. When logical_stamps are incomparable and confidence classes differ, the conflict-fold representative selection (X1-I21) needs a stated tie-break that does not let raw self-declared confidence outweigh corroborated accounts.
3. The hot-queryability horizon per occurrence class and the cost model for on-demand cold rehydration (X1-I23) are not yet parameterized.
4. The hard maximum on cross-owner supersession staleness (X1-I25, X1-I26) before a retraction is reflected in another owner's default projection is not yet set.

## X1 causation, phenomena, situations and interpretation

### Purpose
X1c is the derived and adjudicative layer over the occurrence record defined in X1a and the register mechanics in X1b. It specifies how causation between occurrences is asserted and adjudicated, how member occurrences aggregate into phenomena, how standing conditions (situations, X4) open and close, how interpretations frame occurrences, and how a booked harm is traced to a bounded affected set. X1c declares no primitive occurrence schema of its own: every object here references the canonical occurrence schema in X1a (C6). A K2 act IS an X1 occurrence, not a trace emitted by a separate act object; each effect it causes is a distinct occurrence carrying a cause_ref (C1).

### Object model
- causal_edge: {from_occurrence_ref, to_occurrence_ref, kind, asserter_ref, signature, confidence, status}. kind in {caused, contributed, enabled, prevented, material_contribution, market_share}. caused/contributed/material_contribution/market_share are liability-bearing; when asserted by a participant about their own act they are carried status=contested until a court or independent finding confirms (C17). enabled/prevented never alone ground responsibility.
- account and account_link: an account is a signed assertion about an occurrence. account_link relates accounts of the SAME underlying happening, relation in {corroborates, conflicts} only (C5).
- supersession_edge: {target_ref, kind, basis_ref}, kind in {correction, retraction, revaluation}. adjudicated_finding supersession is a specialization of this one edge (C5).
- phenomenon: {phenomenon_type, member_aggregate_refs, window, norm_set_version_ref}; references released S5 cohort aggregates, never raw member occurrences (C43).
- situation (X4): {situation_type, subject_ref, status, opened_by_ref, closed_by_ref}.
- interpretation: {over_occurrence_ref, frame, asserter_ref, signature, subject_ref?, status}; status in {asserted, superseded, adjudicated_false}.
- affected_set: a court-sealed projection produced by harm-tracing, not a stored reusable person-list (C29).
- adjudicated_finding: the A6 output that supersedes accounts, confirms edge kinds, and records apportioned shares.
Effect-occurrences caused by an act are separate X1 occurrences appended to the affected namespace's owning R3 register (that owner controls), linked to the act by cause_ref (C1, C2). No object here re-declares or weakens occurrence fields (C6).

### Invariants

X1-I27 Every X1c object references occurrences by the canonical X1a schema (mandatory source_ref, confidence, norm_set_version_ref; optional logical_stamp, prior_state_ref, new_state_ref) and SHALL NOT re-declare or weaken those fields (C6). Effects an act causes are distinct occurrences carrying cause_ref, not a trace of a separate act object (C1).

X1-I28 An interpretation naming a person SHALL be subject-enumerable and subject-contestable. Publishing an adverse interpretation of another agent's act beyond the asserter's own register requires a lawful-interest basis. A superseded or adjudicated_false interpretation carries a status that suppresses it from default projections; it remains queryable for audit but SHALL NOT be surfaced as a live characterization (C33). A knowingly false framing routes into the concealment anti-value class (C20).

X1-I29 The causal graph SHALL be acyclic and SHALL place every cause before its effect over the logical_stamp causal order defined in X1b, never over occurrence_time. occurrence_time is descriptive, contestable evidence of ordering and is never the ordering key (C7).

X1-I30 Liability-bearing causal_edge kinds (caused, contributed, material_contribution, market_share) are court or independent findings. An actor MAY assert such an edge about their own act only as contested; a self-asserted superseding-cause or share-shifting edge SHALL NOT outweigh independently sourced accounts by volume (C17, C21).

X1-I31 The affected_set of a booked harm SHALL be bounded reachability over caused/contributed edges (enabled edges excluded) from the seed act, disclosed only as a court-sealed projection scoped to that specific harm under an A6 necessity and proportionality finding that bounds traversal depth and breadth. The enumerated persons SHALL NOT be returned to a complainant or state organ as a reusable person-list; person-grain reachability output debits an S5-equivalent budget and is release-registered, so the court path is never a cheaper individual-sensing channel than X2 (C29). Remoteness SHALL NOT reduce an upstream share where the intervening act was procured, foreseeable, or performed in concert with the upstream actor (C17).

X1-I32 A probabilistic or exposure causal_edge kind (material_contribution or market_share) SHALL be available with an explicit apportionment standard, so cohort harm with no individual but-for link still yields a measurable affected set and per-actor share; the default "no edge, no liability" SHALL NOT stand for long-lag or statistical harm (C17).

X1-I33 A phenomenon SHALL be inferred only from incrementally maintained, pre-aggregated cohort materializations computed inside each member owner's trust boundary and published as standing S5 releases, referenced by the phenomenon, never an on-demand full-stream scan. A phenomenon is never the sole proof that a member occurrence happened (C43).

X1-I34 Phenomena, situations, and interpretations keyed on a person subject and read for governance or sensing SHALL be surfaced only as S5 cohort aggregates. Per-person reads of any such derived layer by a state organ require consent or a judicial access contract on the same footing as timeline reads; drill-down to an individual requires a fresh S2 basis, never the derived layer itself (C33).

X1-I35 A situation (X4) over a person subject carries the same discipline as X1-I34: it is not readable as an ordinary per-subject projection by a governance reader, and per-person situation reads require consent or judicial access. A situation opens and closes only by referenced occurrences (C33).

X1-I36 The emergent classification SHALL be barred wherever coordination, a common plan, or an organizer can be shown; any such evidence reclassifies the occurrence to a joint act with named co-actors (K2). For a genuinely emergent occurrence, restoration resolves by (a) joint-and-several obligation across all identifiable contributors above a de-minimis floor and (b) a named collective backstop fund (commons or insurance pool) that discharges restoration to victims when no contributor is individually attributable, then subrogates as contributors are found. A booking against an occurrence SHALL always resolve to a concrete payer and never terminate at an ownerless record. Deliberately engineering sub-threshold contributions to a known aggregate harm is itself a K2 act (procurement or reckless contribution), unshielded by the sub-threshold floor (C19).

X1-I37 A V4 threshold over composed harm SHALL be evaluated over the aggregated flow of all occurrences composing one K3 process, K5 project, or single harmful outcome, via the causal network and composition references, never per atomic occurrence. Deliberate fragmentation to keep each part sub-threshold is an aggravating basis; the aggregate booking attaches to the composing structure with shares apportioned across the atomic acts (C18).

X1-I38 Value flows and V4 bookings attach to any occurrence's flow record. For an actorless occurrence, attributable V4 liability is deferred until an act or an apportionment (X1-I36) supplies a responsible transformer; the flow record still carries the measured value (C9).

X1-I39 Correction, retraction, and revaluation across X1 use a single supersession_edge with kind {correction, retraction, revaluation}; account_link is reserved for {corroborates, conflicts} over the same underlying happening. An adjudicated_finding's supersession of an account is a specialization of that one edge; superseded accounts are retained, never deleted (C5).

X1-I40 Every causal_edge, account, and interpretation is an identity-bound K2-I15-signed assertion carrying an anti-value hook for knowingly false assertion (perjury-as-anti-value). confidence is an evidence-class scale tied to source type and corroboration and bound to the declarant's calibration TrackRecord; raw self-declared confidence SHALL NOT outweigh independently corroborated accounts (C21).

X1-I41 Any occurrence, interpretation, situation, or phenomenon-membership binding an identifiable natural person in any role SHALL be enumerable by that person on request. Person-naming actorless observations require a lawful observation basis or a non-identifying or k-anonymized reference; confidence grading never substitutes for consent to be recorded. An occurrence observed inside a person's namespace is controlled by that person; an observing registrar holds at most a co-owned assertion subject to the owner's gate (C35).

### Protocols

X1-P9 Trace harm to an affected set. Given a booked harm and an A6 necessity and proportionality finding, fold caused/contributed edges from the seed to the bounded depth and breadth the finding permits, exclude enabled edges, debit the S5-equivalent budget, and emit a court-sealed affected_set projection release-registered to the case. Never return a reusable person-list.

X1-P10 Infer a phenomenon. Read the standing S5 cohort materializations published by member owners, verify the k-floor and budget were debited at production, and assemble the phenomenon by reference to those releases; do not scan raw member streams.

X1-P11 Open, close, or read a situation. An occurrence opens or closes a situation by reference. A governance read over person subjects returns S5 aggregates only; a per-person read requires consent or a judicial access contract.

X1-P12 Append and adjudicate accounts, edges, and interpretations. Each is appended as a signed, staked assertion (X1-I40); conflicting accounts persist under the deterministic conflict-fold of X1b; an A6 finding supersedes via a supersession_edge (X1-I39), confirms liability-bearing edge kinds (X1-I30), and records apportioned shares as a further occurrence.

### Lifecycle and edge cases
(a) Actorless observation inside a person's namespace is controlled by the namespace owner (X1-I41); a placed sensor or registrar cannot capture control of the resulting record.
(b) Coordinated harm mislabeled emergent: on any coordination evidence, reclassify to a joint act with named co-actors (X1-I36); the emergent path is then unavailable.
(c) Statistical or long-lag harm uses a material_contribution or market_share edge (X1-I32); an empty affected_set is not a valid default.
(d) Self-serving edge flooding: volume of self-asserted edges cannot outweigh corroborated accounts (X1-I30, X1-I40); knowingly false edges book perjury-as-anti-value.
(e) Adjudicated-false interpretation is retained for audit but suppressed from default projections (X1-I28).
(f) Fragmented acts aggregate over the composing K3/K5/outcome (X1-I37); fragmentation is aggravating.

### Interfaces
- X1a: consumes the canonical occurrence schema and the closed role enumeration (X1-I6 {agent, patient, instrument, witness, beneficiary}); K2 liability roles {principal, joint, aider, abettor, procurer} refine the agent role (C8).
- X1b: consumes the logical_stamp causal order, the deterministic conflict-fold, and the single supersession machinery.
- K2: acts are occurrences; effect-occurrences carry cause_ref; co-actor shares are adjudicated (K2-I21), not asserted-final.
- A6 and Courts: adjudicated_finding supersedes accounts, confirms edges, and apportions shares.
- V3 and V4: bookings attach to the flow record (X1-I38) and aggregate over composition (X1-I37).
- S5 and X2: phenomena and person-keyed derived layers route through S5 releases and budgets.

### External bindings
- record_time = Meta-Universe Assertion Time; occurrence_time = MU Occurrence Time; valid_interval is a MOS extension over the two-time MU Event model (cite MU-V2-CORE-011 Lifecycle), never collapsed with the other two (C10).
- A18 inviolable rights key the rights-touching act class that makes victim-originated recording and the adverse-interpretation controls binding.
- S1/N6 govern the norm_set versions and the steward-set granularity floors referenced by phenomena and situations.

### Open questions
1. The apportionment standard distinguishing market_share from material_contribution edges (X1-I32) needs a stated evidentiary threshold per harm class.
2. The de-minimis contribution floor and the backstop-fund subrogation order for genuinely emergent occurrences (X1-I36) are not yet numerically set.
3. The calibration-TrackRecord weighting curve mapping the confidence evidence-class to adjudicative weight (X1-I40) is unspecified.