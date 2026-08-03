# Security, Ownership and Access: the S cluster specification

> **Status:** DRAFT v0.1 (2026-07-31). Deepens cluster S of the [World Model Architecture](../World-Model-Architecture.md) (its sections 5 and 6 remain the summary; on conflict, this document governs). Register rows: S1-S8 in [`world-models.csv`](../world-models.csv).
> **Provenance:** drafted by eight parallel specifiers, then attacked by five adversarial reviews (a hostile state, abusive owners, a protocol attacker, the doctrine keeper, a systems pragmatist: 60 findings, 32 critical), then revised under a single resolution charter so the eight sections stay mutually consistent. The findings and resolutions materially shaped every section; the open questions that survived are honest.

---

## 0. How the cluster fits together

S is the gate in front of every other cluster: no meta-model in the Dimension is readable except through it. The eight models form one pipeline plus two cross-cutting guards:

**The read path.** S1 resolves who controls the object (a resolvability rule with a forest of roots: persons self-own, the Polity roots only the constitutional namespaces). S2 turns the controller's permission into a machine-readable access contract (or a judicial or emergency instrument where the law compels access). S3 shapes what actually leaves: a projection in one of four shapes (field subset, summary, aggregate, zero-knowledge predicate), never a raw dump. S4 makes the delivery real: the owner-side gate commit is the single serialization point where authorization is re-validated and the access event is appended, fail-closed, before bytes move; shard roots anchor into the witnessed registrar chain.

**The statistical lens.** S5 is the only lawful route from person-grain reality to state-visible signals: release-eligible cohorts publish k-floored, diversity-checked, budget-debited aggregates along pre-approved frames through a single polity-wide release register; monitor-only cohorts guarantee that floor-breach signals exist for every person and every Charter axis, including minorities too small to aggregate, without identifying anyone. S6 is the sharpest shape: prove the predicate, move no data, leave no trackable trace, even in the audit log.

**The teeth and the substrate.** S7 prices and prosecutes violations (a closed but now sufficient taxonomy, restoration-first remedies, a ladder with no discretion at the entry step, public-interest disclosure protected). S8 keeps the machinery itself sound: keys, compromise cascades, forensic custody, patch duties, so that the guarantees of S1-S7 rest on attested substrate rather than assumption.

Three design commitments recur in every section and are worth naming once:

1. **Honest bounds instead of fictional absolutes.** Revocation propagates within a declared TTL, not "instantly"; audit anchoring has a bounded cadence; staleness horizons are written into the invariants so operators implement the real guarantee instead of quietly approximating a fake one.
2. **Structural protection instead of trusted restraint.** The state logs its own per-person reads even inside its own namespaces; the audit registrar cannot correlate zero-knowledge sessions because the encoding forbids it, not because policy discourages it; cohort definitions are tested against the whole definition lattice by a party independent of the proposer.
3. **Both failure modes priced.** The cluster defends against the surveillant state and against the stonewalling owner with equal force: default deny coexists with civil discovery, probate access, preservation orders, public records and whistleblower safe harbor. A security architecture that only guards one flank is an accomplice of the other.

The sections follow in pipeline order.

---
## S1. Ownership and Control

### Purpose
S1 defines the control fabric of the Dimension: for every meta-object, at every instant, exactly one answerable controller is resolvable. Control is the precondition of every grant (S2), every projection (S3), and every accountability finding (S7). S1 does not confer power to use information freely; it confers answerability for it and the bounded authority to issue contracts over it. Default deny throughout the cluster rests on S1 resolution: no resolution, no grantor, no read.

### Object model
- **controller derivation rule**: the deterministic default by which any meta-object resolves to a controller without a materialized record. An object is controlled by the controller of the register or namespace that contains it; an event is controlled by the controller of the register it was appended to.
- **ownership_record**: a materialized deviation from the derivation default. Fields: subject_ref, controller_ref, basis (transfer, dispute, custodianship, delegation), effective_time, review_date (where basis requires one), registrar signature. It exists only where derivation would give the wrong answer.
- **self_own record**: the root record binding a B1 person to their personal namespaces. Constitutive, not granted.
- **transfer_event**: a signed change-of-controller event. Carries tier class (fast or gated), evidence refs, contest window, and court_leave_ref where S1-I7 requires it.
- **custodianship_record**: court-imposed neutral holding during a dispute (S1-P4) or under a court-appointed technical custodian (S8 interface).
- **guardianship_record**: adjudicated authority of a guardian over a ward's namespaces. Fields: scope, review_date, ward_notification_rule, advocate_ref (mandatory), A6 case ref.
- **post_mortem_policy**: the decedent-authored policy governing sealing of personal namespaces and confirmation of surviving grants (S1-P2).
- **escheat_archive_entry**: holding record for data of dissolved entities, with retention horizon per S1-I12.
- **public_record classification**: a namespace classification for state operational data carrying default world-readable projection policies (S1-I13).

### Invariants
- **S1-I1 (Resolvability).** Every meta-object SHALL resolve to exactly one controller at every instant via the controller derivation rule. An explicit ownership_record SHALL materialize only on deviation: transfer, dispute, custodianship, or delegation. Events recording resolution SHALL NOT themselves require materialized ownership_records; they resolve to the controller of their register.
- **S1-I2 (Forest).** The ownership graph SHALL be acyclic and every chain SHALL terminate in exactly one root of exactly two kinds: (a) a B1 person via self_own, or (b) the Polity, whose root controls only the Dimension, the Charter, and the constitutional namespaces. No chain rooted in a person SHALL pass through the Polity. Federated frames MAY constitute additional roots by treaty under A15/R6.
- **S1-I3 (Self-ownership).** Self-ownership of a B1 person's namespaces is non-transferable, non-waivable, and non-escheatable. It never lapses and never passes to any organ.
- **S1-I4 (Lawful grantors).** A grant over an object issued by a party who is not its S1 controller is void ab initio and books anti-value against the issuer, EXCEPT: (a) a judicial_access_contract issued by an A6 court under S2-I8, and (b) an emergency grant under a statutory basis per S2-I9. The issuing court SHALL verify the S1 resolution of every object in scope and SHALL give joint controllers notice.
- **S1-I5 (Prospective voidability, fast tier).** For fast-tier transfer classes, grants issued in good-faith reliance on the shard register's then-current record are voidable prospectively from correction, not void ab initio. Void-ab-initio treatment is reserved for gated-tier classes and bad-faith reliance.
- **S1-I6 (Controller change and contracts).** The effect of any controller change on existing S2 contracts is governed solely by S2-I13. Judicial and emergency contracts are exempt: they follow the title and bind every successor controller automatically.
- **S1-I7 (Transfer leave).** A transfer_event whose subject lies within the scope of an open A6 case, an open breach_case, or a preservation_order SHALL require prior court leave. A transfer executed without required leave is void and constitutes an audit_evasion aggravator under S7.
- **S1-I8 (Guardianship bounds).** Every guardianship_record SHALL carry a review_date not exceeding the statutory maximum interval. Lapse of review_date automatically suspends all guardian-issued grants pending renewed adjudication. Guardian consent SHALL NOT constitute the consent basis for any per-person read by a state organ (a judicial_access_contract with separate ward representation is required; see S2-I14). Grants where the guardian or a related party is grantee or beneficiary, and any commercial or monetized grant of ward data, require prior A6 approval. The ward_notification_rule SHALL NOT be set to never-notify: where the ward cannot receive notice, the independent ward advocate receives it. The advocate holds independent power to revoke any guardian-issued grant. At majority or on restoring adjudication, the ward holds a restoration right: mandatory deletion of guardian-era commercial projections and their derived artifacts.
- **S1-I9 (Creation and derivatives).** The creating actor is the initial controller of a created object. For a derived_artifact, control confers NO grant-issuing right beyond the intersection of every input's restrictions (purpose, duration, redisclosure), per S3; revocation or expiry of any input propagates, and the derivative expires no later than its shortest-lived input.
- **S1-I10 (Registrar discipline).** Registrar validation SHALL complete within normed processing windows per event class; on expiry the filing is deemed referred to A6 on an expedited track at the registrar's cost. Fees SHALL follow a published cost-based schedule fixed in the A12 mandate. Validation criteria SHALL be published and machine-checkable; every refusal SHALL cite a specific failed criterion. Wrongful or dilatory refusal is registrar_abuse under S7 with compensation for demonstrated transaction loss. The Registrar-General is a Charter Art. 10 concentration-charge subject, with structural plurality and mutual anchoring of registers where feasible.
- **S1-I11 (Death).** On death, personal namespaces seal per the post_mortem_policy, but A6 courts MAY issue post-mortem judicial_access_contracts over sealed namespaces for probate, creditor, criminal, and victim claims, overriding any post-mortem policy. Estate-relevant transactional classes (K2 acts, X5 sides, F-cluster) are seal-exempt for probate scope.
- **S1-I12 (Escheat retention).** Escheat_archive retention SHALL at minimum span all limitation periods for claims against the dissolved entity, including the perpetual-clawback class of S7-I6. Destruction requires a court finding of no pending or reasonably foreseeable claims.
- **S1-I13 (Public record).** State operational namespaces carry the public_record classification: default world-readable projection policies mandated through A12, subject to a closed, enumerated exemption list, each exemption harm-tested, time-bounded, and logged. Any person holds a request right with a statutory response deadline; refusal SHALL cite a specific exemption, is S4-logged, and is appealable to A6 on an expedited track. Unjustified refusal books anti-value against the organ.
- **S1-I14 (Good-faith losers).** A party who held contested ownership in good faith owes restitution of rents captured during the dispute via an S7 remedy_order, with no anti-value component. Anti-value and clawback attach only on a court finding of bad faith, concealment, or grossness under the contemporaneous norm-set.

### Protocols
- **S1-P1 (Transfer).** 1. The transferor signs a transfer_event naming subject, transferee, tier class, and evidence. 2. Fast tier: the event self-executes on the sharded register, valid immediately, with asynchronous registrar validation and a short contest window; gated tier (land, organizations, encumbered or custodial subjects): the registrar validates synchronously within the S1-I10 window before title moves. 3. Where S1-I7 applies, court leave is verified before execution in either tier. 4. Existing S2 grants are handled per S2-I13: org-to-org succession continues grants under the successor by default, with a normed objection window operated at contract-template or class granularity; judicial and emergency contracts follow the title (S1-I6). 5. Encumbrances such as rent_obligations follow the title.
- **S1-P2 (Death).** 1. A registered death event seals personal namespaces per the post_mortem_policy. 2. The post_mortem_policy, not any successor controller, is the confirming authority under S2-I13 for grants over personal namespaces. 3. Claims against the estate proceed via post-mortem judicial_access_contracts per S1-I11. 4. Self-ownership itself never escheats (S1-I3).
- **S1-P3 (Guardianship).** 1. A6 adjudication creates the guardianship_record with scope, review_date, and advocate_ref. 2. Guardian-issued grants are bounded by S1-I8 and expire at review_date, requiring affirmative renewal. 3. The advocate receives S4 visibility over all guardian acts. 4. Review occurs at every review_date, at majority, and on any restoring adjudication; the restoration right of S1-I8 executes at majority.
- **S1-P4 (Ownership dispute).** 1. A filed dispute materializes a custodianship_record freezing disposition. 2. Resolution reassigns control by court order. 3. Rents captured during the dispute are settled per S1-I14.

### Lifecycle and edge cases
- (a) **Creation**: creator becomes initial controller by derivation; no ownership_record materializes unless the object is created directly into deviation (for example, into custody).
- (b) **State as owner**: state organs control their operational namespaces, but under the public_record classification of S1-I13, and their reads of person-subject records they themselves control remain subject-visible and contract-bound per S2-I15 and S4-I13; controlling a namespace never exempts an organ from per-person read logging.
- (c) **Dissolution**: organizational data routes to the escheat archive under S1-I12; dissolution mid-process is a controller change under S1-I6 and S1-I7.
- (d) **Federated roots**: treaty roots under S1-I2 are registered in R6 and reviewable under A15; they never absorb person-rooted chains.
- (e) **Compromise or dispute of the registrar itself**: mutual anchoring per S1-I10 preserves resolvability; courts resolve on anchored peer evidence.

### Interfaces
- **S2**: S1 resolution names the lawful grantor (S1-I4); controller-change effects on contracts defer to S2-I13; guardianship consent limits per S2-I14.
- **S3**: derivative control bounds (S1-I9); court-defined policies for judicial reads are generated under custodianship where the owner fails to generate.
- **S4**: every read of a person-subject record is logged and subject-enumerable regardless of who controls the namespace; registrar acts are S4-audited.
- **S7**: registrar_abuse, audit_evasion aggravators (S1-I7), remedy_order restitution (S1-I14), evidence duties under preservation_orders.
- **S8**: court-appointed technical custodians serve court-scoped projections from escrowed snapshots when a controller's systems are under adverse process.

### External bindings
B1 (persons), O1 (organizations), A6 (courts and case standing), A10 (taxonomy lawmaking), A12 (registrar and public_record mandates), A15/R6 (federation treaties), R3 (event registers), X3 (incidents), Charter Art. 3 (polycentrism), Art. 6 (floors), Art. 10 (concentration self-charge).

### Open questions
1. The initial class schedule dividing fast-tier from gated-tier transfers, and its A12 amendment procedure.
2. Recognition, suspension, and revocation mechanics for treaty roots under A15/R6, including exit of a federated frame.
3. Composition, rotation, and attestation of the court-appointed technical custodian pool shared with S8.
4. The initial enumeration of the public_record exemption list and its harm-test methodology.

## S2. Access Contracts and Consent

### Purpose

The Access Contract is the sole authorizing instrument for reads in the Dimension. It governs not only information that leaves an owner's namespace but every read of a record whose subject is a natural person, including reads performed by the S1 controller of its own namespace. Default deny is universal: without an Active contract resolvable at the owner-side gate, no projection is generated and no read occurs. S2 defines who may lawfully issue contracts, what a valid consent basis is, how non-consensual paths (judicial, emergency) are constrained, and how contracts behave across revocation, controller change, guardianship, invalidity and derivation.

### Object model

- **access_contract**: grantor_ref, grantee_ref, scope (object or namespace refs), purpose_set, S3 shape binding (projection_policy_ref), duration, cardinality (use_count), redisclosure_rule, revocation_horizon (contract-declared field, see S2-I11), lifecycle state.
- **contract_template**: pre-approved parameterized contract class registered under an A12 mandate; instantiation is still a grant but MAY be auto-issued per S2-I5.
- **consent_record**: evidence basis of a consensual grant: schema shown, shape shown, purpose shown, and either a ceremony transcript or a consent_policy_agent profile version plus delivered notice.
- **consent_policy_agent**: first-class standing machine-readable preference profile authored by the owner (acceptable purposes, shapes, durations, sensitivity classes), periodically reviewed, with a no-cause cooling-off revocation window on every auto-issued grant.
- **capability_token**: signed token minted at grant time (and on any relevant S1/S2 change) bundling the S1 control snapshot, contract state, policy version and expiry, with a short TTL fixed per sensitivity class.
- **judicial_access_contract**: court-issued contract within an A6 case; subtypes include investigative, civil discovery, creditor asset-disclosure, probate and victim orders; carries per-subject due_process_record, scope_ceiling, review_date, deferred-notice terms and the court-defined projection policy.
- **emergency_access_grant**: grant instantiated from a pre-declared per-emergency-class contract_template, referencing an independently registered X3 incident; always retains a declared S3 shape.
- **guardianship_consent**: consent supplied by a registered guardian within a scope_ceiling, bounded by S2-I14.
- **intra_organ_access_contract**: contract binding internal person-grain reads by a state organ over namespaces it itself controls, with declared purpose and shape, enforced by the same gate as external reads.
- **constitutional_standing_template**: Charter-level, auto-instantiated, registrar-non-revocable, zero-discretion contract classes: (a) owner visibility over access_events (the S4-I6 right exercised in-model), (b) subject-owner co-control of every access_event concerning them, (c) the S5 sealed-evaluator ingestion basis.
- **revocation_event**: grantor-initiated termination; its effective_time is constrained by S2-I12.
- **minimality_schema_ref**: pointer to the K4-registered data-minimality schema for a service class, the sole yardstick of necessity under S2-I4.

### Invariants

- **S2-I1**: Lawful grantors are exhaustively enumerated: (a) the current S1 controller of every object in scope, resolved per S1 derivation rules; (b) a court issuing a judicial_access_contract under S2-I15; (c) the statutory emergency basis of S2-I9 acting through a pre-declared template; (d) a constitutional_standing_template. A grant by any other issuer is void under S2-I16; S1's voidness booking carves out issuers (b) through (d).
- **S2-I2**: Every contract, including judicial and emergency contracts, SHALL bind a declared S3 shape. No instrument in the Dimension confers raw namespace access.
- **S2-I3**: A contract binds exactly one declared purpose_set, one shape, one duration and one cardinality; contradictory overlapping grants resolve to the narrowest shape satisfying both.
- **S2-I4**: Consent SHALL be informed, specific and freely given. Necessity of a demanded scope is judged against the K4-registered data-minimality schema for the service class, never against the provider's self-description. Per-domain prohibited-demand schedules (employment, housing, credit, essential services) apply under A-cluster law. Consent granted to a counterparty holding gatekeeping power over the grantor's livelihood or shelter carries a rebuttable presumption of coercion. Structural detection patterns (grant rate conditioned on service outcome) SHALL auto-open consent_coercion cases in S7.
- **S2-I5**: A consent_policy_agent MAY auto-issue template-conformant grants within its profile for low-sensitivity classes; the profile version plus delivered notice is a valid consent_record basis, backed by a cooling-off revocation window. The full per-grant ceremony is mandatory for high-sensitivity classes (B10, B12, A16, A18) and for any off-profile request.
- **S2-I6**: Delegation SHALL NOT exceed the delegating contract's scope, purpose_set, duration or redisclosure_rule (delegation ceiling); suspension and revocation walk the delegation graph transitively.
- **S2-I7**: Cardinality is enforced at the owner-side gate: use_count decrements in the same atomic commit as the access_event append (S2-I20), so a one-shot contract cannot be double-spent by concurrent requests.
- **S2-I8**: Any per-person read by a state organ requires the person's consent_record or a judicial_access_contract. A per-person read includes reads by the S1 controller of its own namespace: a state organ holding person-subject records SHALL bind internal person-grain reads to an intra_organ_access_contract, and every read of a record whose subject is a natural person SHALL append a subject-visible, subject-enumerable access_event regardless of who controls the namespace.
- **S2-I9**: An emergency_access_grant SHALL (a) reference a pre-existing X3 incident registered by a party other than the invoker; (b) be scoped by a pre-declared per-emergency-class template, retaining a declared S3 shape, never raw access; (c) carry a statutory absolute maximum duration, non-renewable without judicial ratification within a short fixed window; (d) count against a per-organ invocation quota whose exhaustion fails closed; (e) require dual-control invocation above a declared sensitivity class. Wrongful invocation over personal namespaces routes through S7-I10 to an A18 inviolable-rights case; anti-value booking and owner compensation are additional consequences, never alternatives.
- **S2-I10**: Authorization staleness is bounded, not fictionally zero: the read gate verifies capability_tokens locally by signature and TTL. Revocation, suspension, controller-change suspension and key-compromise suspension become effective at worst one TTL after the event, per sensitivity class. This bounded-staleness horizon is the honest guarantee of this cluster.
- **S2-I11**: Projection instances die at the earlier of their own expiry and the contract's revocation_horizon. Obligations that survive revocation govern retention, deletion and confidentiality of already-delivered artifacts, never continued use. This rule is stated identically in S3.
- **S2-I12**: A revocation_event's effective_time SHALL be no earlier than its own append position in the S4 order. Retroactive voiding requires a separate court instrument and SHALL NOT ground S7 charges against a grantee for reads appended before it.
- **S2-I13**: Controller change is governed by this invariant alone. Org-to-org succession: grants CONTINUE under the successor by default, subject to a normed objection window during which the successor may terminate per contract terms and any grantee may exit; confirmation and termination operate at contract_template or class granularity, with notification via a single published succession event. Natural-person death: the decedent's post-mortem policy is the confirming authority for grants over personal namespaces. Judicial and emergency contracts are exempt: they follow the title and bind every successor automatically. Any S1 transfer of a subject within the scope of an open A6 case, breach_case or preservation_order requires court leave; evasive transfer is an S7 audit_evasion aggravator.
- **S2-I14**: Guardianship consent SHALL NOT constitute the S2-I8 basis for any state per-person read concerning a ward; such reads always require a judicial_access_contract with the ward separately represented. Guardian-issued grants expire at the guardianship review_date and require affirmative renewal; a lapsed review_date auto-suspends them all. A statutory maximum review interval applies. Grants where the guardian or a related party is grantee or beneficiary, and any commercial or monetized grant of ward data, require prior A6 approval. The ward_notification_rule has a normed floor: never-notify is impossible, and a court-appointed reviewer receives notifications for wards who cannot. A standing independent ward advocate holds S4 visibility over guardian acts and independent power to revoke any guardian-issued grant. At majority the ward holds a restoration right: mandatory deletion of guardian-era commercial projections and derived artifacts, with guardian-benefit grants presumptively breaching in S7 review.
- **S2-I15**: Any party with standing in an A6 case MAY petition for a judicial_access_contract (investigative, civil discovery, creditor, probate and victim subtypes). The order SHALL name each subject individually with a per-subject necessity and proportionality finding in the due_process_record; orders SHALL NOT issue against a cohort predicate; multi-subject orders are capped by a constitutional parameter changeable only by supermajority. Deferred notice carries a hard statutory maximum with a single renewal and an absolute ceiling, after which notice is automatic and non-waivable. An independent special advocate SHALL be appointed for every petition where the subject is unheard. Each court publishes petition, grant, denial and renewal counts in the S4 transparency report. The issuing court defines the projection policy; generation is compellable through a court-appointed technical custodian; obstruction is a distinct S7 violation carrying adverse inference in the underlying case.
- **S2-I16**: Invalidity never extinguishes restrictive terms. A void or voided contract confers zero authorization while imposing the strictest obligations available in the bound projection_policy, plus mandatory verified destruction of every instance and derived artifact generated under it, logged to S4. Holdings under a void contract are unauthorized_read from the moment of generation.
- **S2-I17**: Control of a derived_artifact confers no grant-issuing right beyond the intersection of every input's redisclosure_rule, purpose_set and duration. Any contract over a derived_artifact SHALL name every input owner as co-grantor or issue under a pre-accepted derivative policy of each input owner. Revocation, suspension and expiry of any input propagate to all grants over the derivative, which expires no later than the shortest input.
- **S2-I18**: Constitutional_standing_templates are auto-instantiated per owner at object creation, registrar-non-revocable and zero-discretion; through them every access_event is co-controlled by the subject-owner it concerns, so S2-I1 remains literally universal. Standing bulk-log contracts are prohibited outright.
- **S2-I19**: The gate SHALL evaluate cumulative disclosure per (owner, grantee cluster) across all active and recently expired contracts, at issuance and before each generation, denying or narrowing any grant whose composition exceeds the strictest applicable floor. Grantee clusters resolve by S1 common control plus adjudicated collusion findings; re-evaluation runs whenever a grant joins an existing cluster; composition denials are themselves S4-logged.
- **S2-I20**: The owner-side gate is the single serialization point for every disclosure: an atomic local append (tamper-evident WAL inside the owner trust boundary) that re-validates contract lifecycle state, current S1 control of every object in scope, purpose membership and cardinality in the same commit, aborting delivery if any revocation_event is ordered before it. Fail-closed applies to this local append; shard roots anchor asynchronously into the Audit Registrar per S4.

### Protocols

- **S2-P1 Consensual issuance**: (1) grantee presents a request naming template, purpose, shape and duration; (2) the gate checks the request against the K4 minimality schema and prohibited-demand schedules; (3) consent is obtained by ceremony, or auto-issued by the consent_policy_agent when S2-I5 permits; (4) the consent_record is sealed and the contract activates; (5) capability_tokens are minted per S2-I10; (6) every generation passes the S2-I20 gate commit.
- **S2-P2 Judicial issuance**: (1) any A6-standing party petitions, naming subjects individually; (2) the court verifies S1 resolution of every object in scope, gives joint owners notice, and appoints a special advocate if any subject is unheard; (3) per-subject necessity and proportionality findings enter the due_process_record; (4) the court defines the projection policy and issues the contract with scope_ceiling, review_date and deferred-notice terms within S2-I15 limits; (5) the owner generates within the deadline, failing which the court-appointed custodian generates inside the trust boundary; non-generation books a distinct S7 violation.
- **S2-P3 Emergency invocation**: (1) invoker cites a pre-registered X3 incident and a per-class template; (2) the engine checks quota and, above the sensitivity threshold, dual control; (3) the grant issues in the template's declared shape with the statutory maximum duration; (4) judicial ratification is sought within the fixed window, absent which the grant lapses non-renewably; (5) review classifies any wrongful invocation per S2-I9.
- **S2-P4 Revocation**: (1) grantor (or cooling-off exercise, or ward advocate under S2-I14) appends a revocation_event; (2) effective_time is set per S2-I12; (3) capability_tokens age out within one TTL; (4) surviving obligations attach per S2-I11; (5) sealed-envelope keys for cached instances stop being served per S3.

### Lifecycle and edge cases

States: Draft, Active, Suspended, Revoked, Expired, Void. (a) Controller change follows S2-I13; no other provision governs it. (b) On death, grants over personal namespaces are confirmed or lapsed by the post-mortem policy; post-mortem judicial contracts over sealed namespaces follow S2-I15 and the S1 estate rules. (c) A voidness finding transitions the contract to Void with S2-I16 consequences from generation, not from the finding. (d) Key compromise follows the S8 role-split cascade: grantor keys suspend issuance and generation, grantee keys suspend that grantee's reads pending re-binding, transitively over delegations; reinstatement restores prior terms unchanged, so re-issuance cannot extract new consent. (e) Concurrent requests against remaining cardinality are resolved by the S2-I20 commit order; the loser receives a denial in the standard indistinguishable envelope. (f) Suspension of a system under confirmed compromise defers to the S8 custodian regime for court-scoped reads.

### Interfaces

S1 (control resolution and derivation rules; transfer leave under S2-I13), S3 (shapes, projection policies, gate execution, sealed cache envelopes, S2-I11 stated identically), S4 (access_events, subject enumeration, inclusion promises, per-court statistics), S5 (constitutional ingestion template; aggregate purposes register through the polity-wide release register), S6 (zk_predicate shapes as contract-bound projections), S7 (violation booking, S7-I10 routing, safe harbor), S8 (key compromise cascade, custodian service), A6 (courts, standing, expedited appeals), A10 (constitutional parameters), A12 (template mandates, fee and processing norms), K4 (minimality schemas), X3 (incident registration), R4 (identity verification at ceremony).

### External bindings

Charter Art. 4 (consent inviolable, never priceable: S2-I9 routing), Art. 3 and Art. 10 (no apex organ; concentration self-charges bind the registrars S2 relies on), B-cluster subject classes (B10, B12 sensitivity gating), A15/R6 (treaty roots for federated grantors), A16/A18 (high-sensitivity ceremony classes and inviolable-rights cases).

### Open questions

1. Numeric values of the constitutional parameters (multi-subject cap, TTL per sensitivity class, objection window, deferred-notice maximum, cooling-off length) are reserved to A10 lawmaking; candidate ranges are not yet proposed.
2. Grantee-cluster resolution under S2-I19 when common control spans federated frames rooted by treaty: which frame's S1 resolution governs.
3. Liability allocation when a consent_policy_agent auto-issues a grant the owner did not intend: fault split between owner profile authorship and agent implementation, and its S7 classification.
4. Interaction of the cooling-off window with one-shot contracts already generated: whether cooling-off revocation triggers S2-I16-grade destruction or only S2-I11 surviving obligations.

## S3. Projections and Disclosure Shaping

### Purpose
S3 defines how information lawfully leaves an owner's namespace: never as raw access, always as a projection, a shaped artifact generated inside the owner's trust boundary under an active S2 access contract and a covering projection policy. S3 specifies the shapes, the owner-side gate that serializes every disclosure, the attribution and cache regime, and the rules for artifacts derived from projections. The gate is the single point where authorization, control, purpose and cardinality are checked and where the durable audit record is created.

### Object model
- **projection_policy**: a versioned declaration of shape, field scope, redaction profile and sensitivity class for a namespace scope. Authored by the controlling owner for consensual reads; authored by the issuing court for judicial and emergency-template reads. A policy without a contract discloses nothing.
- **shape**: closed enumeration: `field_subset`, `summary`, `aggregate`, `zk_predicate` (verified through S6). Every disclosure, including emergency disclosure, carries exactly one declared shape.
- **projection_instance**: an ephemeral artifact. `projection_id` is a deterministic high-entropy hash of (contract_ref, policy version, source version, as_of, grantee_ref) and is not derivable by outsiders from policy, source version or grantee. Instances are re-derivable, not stored; the S4 access_event carrying the id is the sole durable per-read record.
- **owner gate**: the enforcement point inside the owner trust boundary. Maintains a tamper-evident write-ahead log (WAL); performs the atomic validate-and-append of S3-I4; seals segments and anchors shard roots into the Audit Registrar root-of-roots on a bounded cadence.
- **capability_token**: a signed token minted at grant time bundling the S1 control snapshot, contract state, policy version and expiry, with a short TTL fixed per sensitivity class.
- **generation_lease**: a lease over a running generation, shorter than the normed revocation propagation window; delivery requires a live lease.
- **attribution_mark**: a per-grantee mark embedded where shape entropy allows. The payload is a commitment: owner_ref, grantee_ref and purpose encrypted or hashed under registrar-held keys, openable by courts and registrars; a finder learns nothing.
- **detached_manifest**: a signed manifest (content_hash, contract_ref, grantee_ref, policy version) issued for low-entropy shapes that cannot carry a robust mark.
- **sealed_cache_envelope**: an encrypted envelope under a short-lived key held by the owner gate, keyed per (contract_ref, grantee_ref, projection_id).
- **derived_artifact**: a registered artifact computed from one or more projection_instances, carrying the intersection of all input restrictions.

### Invariants
- **S3-I1**: No read result SHALL exist except as a projection generated under an active S2 contract and a covering projection_policy. For judicial and emergency instruments the issuing court or the pre-declared emergency template supplies the policy; an owner's failure to author a policy SHALL NOT defeat a compelled read.
- **S3-I2**: The shape set is closed. No path, consensual, judicial or emergency, SHALL produce raw namespace access or an unshaped dump.
- **S3-I3**: Generation SHALL execute inside the owner's trust boundary; no reader process SHALL hold a handle to source objects. This binds every consumer, including the S5 evaluator: cohort computation SHOULD run as distributed local evaluation with only noised per-owner partial contributions crossing under secure aggregation; centralized evaluation is lawful only under the S5 attestation preconditions.
- **S3-I4**: The owner gate's atomic local append is the single serialization point for every disclosure. In one commit the gate SHALL re-validate contract lifecycle state, the grantor's current S1 control of every object in scope, purpose membership and cardinality (decrementing use_count), and SHALL abort delivery if any revocation_event is ordered before the append. Fail-closed applies to this local append: a delivery that cannot be logged, cache hits included, SHALL NOT occur. Shard roots anchor asynchronously into the Audit Registrar on a bounded cadence; anchoring lateness is registrar-visible anomaly per S4.
- **S3-I5**: The gate authorizes against capability_tokens verified locally by signature and TTL. Revocation, suspension, transfer and key compromise are therefore effective at worst one TTL after the event; this bounded-staleness horizon is the honest guarantee and SHALL be stated as such wherever revocation timing is cited.
- **S3-I6**: A projection_instance dies at the earlier of its own expiry and the contract's revocation horizon (a contract-declared field). Surviving obligations govern retention, deletion and confidentiality of already-delivered artifacts, never continued use. This rule is stated identically in S2-I11.
- **S3-I7**: Instances are bound to their contract, grantee and purpose; onward disclosure is prohibited. Possession of data matching a projection content_hash without a corresponding S4 access_event granting it to the possessor is breach evidence under S7.
- **S3-I8**: Disclosed content is deterministic per (source version, policy version, grantee): repeat reads by the same grantee under the same versions are byte-identical. Determinism is not global; different grantees MAY receive differing bytes to enable attribution.
- **S3-I9**: Every shape whose entropy permits SHALL embed a per-grantee attribution_mark with a commitment payload. Low-entropy shapes rely on the detached_manifest plus S4 reconciliation; their attribution is set-attribution requiring corroborating S4 evidence, with explicit joint-and-several rules. Honeytoken instances MAY be seeded into high-risk grants. Ambient scanning of circulating data is prohibited; watermark forensics run only on artifacts entering a case.
- **S3-I10**: Control of a derived_artifact confers no grant-issuing right beyond the intersection of every input's redisclosure rule, purpose set and duration. Any contract over a derivative SHALL name every input owner as co-grantor or issue under a pre-accepted derivative policy. Revocation, suspension and expiry of any input propagate to all grants and instances over the derivative; a derivative expires no later than its shortest input. Unregistered derivation suspends the deriving agent's grant rights over the artifact pending registration. Where an input's governing contract is void, suspended or unresolvable, inheritance defaults to the strictest profile.
- **S3-I11**: Response indistinguishability is mandatory and non-waivable for ordinary readers: every gate outcome (grant, denial, suppression, budget exhaustion, expiry, revocation) returns in a structurally identical envelope with latency and payload size padded to a fixed profile per shape class. Per-(reader, owner) probe rate limits apply, with S7 escalation on breach. Judicial, Audit Registrar integrity, and S7-evidence readers are excluded: they receive true denial semantics plus a signed existence or non-existence assertion.
- **S3-I12**: For declared sensitivity classes, no store outside the owner trust boundary SHALL hold projection plaintext. Cache entries are sealed_cache_envelopes; every serve requires a key fetch from the owner gate, which is simultaneously the revocation check and the logged S4 read event. Cache reuse across contracts, grantees or purposes is unauthorized_read by the cache operator, not staleness. Lower-sensitivity classes keep notice-based purging with residual risk priced in S7.
- **S3-I13**: Exactly one S4 access_event per read is the durable record. Every read of a record whose subject is a natural person, including a read by the S1 controller of its own namespace, SHALL append a subject-enumerable access_event naming reader, purpose and time.
- **S3-I14**: Every aggregate-shaped projection SHALL be registered in the polity-wide release register (S5) before delivery, SHALL debit the shared budget accounts of affected cohorts and members, and SHALL conform to an approved cohort frame. Publication or delivery without prior registration is audit_evasion under S7.
- **S3-I15**: Before issuance and before each generation, the gate SHALL evaluate cumulative disclosure per (owner, grantee cluster) across all active and recently expired contracts, where clusters resolve by S1 common control plus adjudicated collusion findings, and SHALL deny or narrow any generation whose composition exceeds the strictest applicable floor. Composition denials are themselves S4-logged.
- **S3-I16**: A revocation_event's effective_time SHALL be no earlier than its own append position in the gate's log. Retroactive voiding is available only through a court instrument and cannot ground S7 charges against a grantee for reads appended before it.

### Protocols
- **S3-P1 (policy declaration)**: The controlling owner authors or amends a projection_policy inside the trust boundary; the gate validates shape and scope well-formedness; the new policy version appends to the owner's register. Court-authored policies for compelled reads enter through S3-P4.
- **S3-P2 (read execution)**: (1) reader presents capability_token; gate verifies signature and TTL locally; (2) gate acquires a generation_lease and generates the projection inside the trust boundary, applying redaction, marks or manifest; (3) gate performs the S3-I4 atomic validate-and-append; on success it delivers (or releases the envelope key) in the same commit scope; on any failed check or expired lease it aborts and, for ordinary readers, returns the S3-I11 uniform envelope; (4) for aggregate shapes, registration and budget debit per S3-I14 precede the append.
- **S3-P3 (derivation)**: A grantee computing over instances SHALL register the derived_artifact before exercising any right over it, recording input instance refs, owners and the inherited intersection profile. The register propagates input revocations and expiries automatically.
- **S3-P4 (compelled generation)**: For a judicial_access_contract or emergency template, the issuing court defines the projection_policy (shape, scope, redaction). The owner SHALL generate within the instrument's deadline; on failure, a court-appointed technical custodian executes generation inside the trust boundary (or from escrowed snapshots under S8 adverse-process rules), and non-generation is booked as a distinct S7 violation with adverse inference in the underlying case.

### Lifecycle and edge cases
- (a) **Revocation mid-generation**: leases are shorter than the revocation propagation window; a lease that cannot be re-acquired before delivery aborts the read. Completed reads appended before the revocation_event remain lawful per S3-I16.
- (b) **Controller change, death, dissolution**: instance validity follows the governing contract under S2-I13 (org-to-org default continuation with objection window; post-mortem policy as confirming authority; judicial and emergency instruments follow the title and bind successors automatically). The S3-I6 rule governs already-delivered artifacts throughout.
- (c) **Compromise under adverse process**: a system within the scope of a judicial contract, preservation order or breach case that declares compromise owes containment attestation by the normed deadline; thereafter the court-appointed custodian serves court-scoped projections from escrowed snapshots. Artifacts generated during a key-compromise window are flagged disputable per S8.
- (d) **Emergency**: an emergency grant SHALL take its policy from a pre-declared per-emergency-class template and always retains a declared S3 shape; it MAY widen field scope within the template's statutory ceiling but SHALL NEVER produce raw namespace access.
- (e) **Format stripping**: conversion or manifest removal does not launder data. High-entropy shapes remain attributable through embedded marks; low-entropy shapes resolve by set-attribution with corroborating S4 evidence and manifest reconciliation, never by implied single culprit.
- (f) **Void contracts**: a void or voided contract confers zero authorization but imposes the strictest obligations in the bound policy, plus verified destruction of every instance and derivative, logged to S4; such holdings are unauthorized_read from the moment of generation.

### Interfaces
- To **S2**: the gate consumes contract state via capability_tokens and enforces cardinality; revocation semantics per S3-I6 mirror S2-I11.
- To **S4**: the gate's WAL appends are the S4 events of record; shard roots anchor into the registrar root-of-roots; inclusion promises per S4.
- To **S5**: aggregate registration, budget debits and frame checks (S3-I14); secure-aggregation partial contributions as the preferred evaluator input (S3-I3).
- To **S6**: `zk_predicate` generation binds verifier, session and resolved parameters per S6 challenge rules; zk access_events use blinded per-session tags per S6/S4.
- To **S7**: manifests, marks, composition denials and gate abort records are breach evidence; unregistered aggregates and pretextual cache reuse map to the S7 taxonomy.
- To **S8**: role-split key-compromise suspension gates token verification; disputable-artifact flagging; custodian escrow.

### External bindings
S1 (control resolution consumed at token mint and re-checked at append), S2 (contracts, judicial and emergency instruments, consent-policy agents), S4 (audit substrate and anchoring), S5 (release register, frames, budgets), S6 (predicate catalog), S7 (violation taxonomy including evidence_spoliation and audit_evasion), S8 (CERT, escrow, attestation), Charter Art. 4, 6 and 10.

### Open questions
1. Calibration authority and revision cadence for the per-shape-class padding profiles of S3-I11 (fixed envelope and latency), and how profile updates avoid becoming themselves an oracle.
2. The feasibility threshold per measure class at which S5 evaluation may fall back from distributed secure aggregation to attested centralized evaluation, shared with S5.
3. Latency budget for grantee-cluster resolution in S3-I15 relative to the capability-token TTL, and where the cluster index lives without becoming a correlation asset.
4. Normed seeding rate and governance for honeytoken instances so they deter re-disclosure without inflating false S7 cases.

## S4. Access Audit: The Log, the Gate Commit, and the Audit Registrar

### Purpose

S4 makes every read observable to the parties it concerns and provably complete to the courts. It defines the access_event as the single durable record of every disclosure, binds authorization and logging into one atomic commit at the owner-side gate, and constitutes the Audit Registrar as an integrity anchor rather than an omniscient observer. The section is written against three failure modes at once: the unlogged read (evasion by readers, including S1 controllers reading their own person-subject holdings), the truncated or equivocating log (evasion by the registrar), and the log as surveillance instrument (the registrar or its grantees mining who-read-what-about-whom). Fail-closed is local, anchoring is asynchronous, and log reads are themselves gated reads.

### Object model

- **access_event**: the sole durable per-read record. Fields: reader_ref, grantee_ref, contract_ref, projection_id (deterministic high-entropy hash per S3; instances are re-derivable, not stored), shape, purpose_code, subject_refs, gate outcome, append position, timestamp. One event per delivery, cache hits included.
- **owner_gate_log**: tamper-evident append-only WAL inside the owner trust boundary; the serialization point for every disclosure from that namespace shard. Seals segments into Merkle roots.
- **inclusion_promise**: registrar-signed receipt (root hash, submission time, signature) issued on anchoring submission, delivered to the shard operator and available to readers and owners.
- **root_of_roots**: the Audit Registrar's chain of anchored shard roots, sealed on a bounded cadence, counter-signed by witnesses.
- **witness_set**: quorum of independent parties (peer registrars under S8 mutual anchoring, plus the courts) that cross-sign roots and carry an explicit consistency-checking duty.
- **standing_audit_contract**: constitutional S2 contract_template, auto-instantiated per owner at object creation and per natural-person subject, non-revocable by the registrar, zero-discretion; the instrument through which enumeration rights are exercised so that S2-I1 and S3-I1 remain literally universal.
- **audit_query**: a read whose object is the log; it is a gated read like any other and produces its own access_event.
- **blinded_tag**: per-session identifier for zk verification events, derived from a subject-held key and a session nonce; unlinkable across sessions without that key.
- **summary_record**: post-contest-window collapse of detail events, carrying sealed per-event commitments.
- **transparency_report**: the registrar's periodic aggregate publication, registered as a release under S5.

### Invariants

- **S4-I1**: Every projection delivery under any S2 contract, every cache-served delivery, every zk verification session, and every read of a record whose subject is a natural person, including reads by the S1 controller of its own namespace and intra-organ reads by state organs, SHALL append exactly one access_event naming reader, purpose, shape and time. The access_event is the sole durable per-read record.
- **S4-I2**: The append is atomic with authorization. The owner-side gate SHALL, in the same commit that appends the access_event, re-validate contract lifecycle state, the grantor's current S1 control of every object in scope, purpose membership and cardinality, decrementing use_count in that commit, and SHALL abort delivery if any revocation_event is ordered before it in the log. The commit is the single serialization point for the disclosure.
- **S4-I3**: Fail-closed binds to the local append: a delivery whose access_event cannot be durably appended to the owner_gate_log SHALL NOT occur. Cache hits satisfy this because key release by the gate is itself a gated, logged read per S3.
- **S4-I4**: Sealed shard roots SHALL be anchored into the registrar root_of_roots within a normed maximum merge delay. The registrar SHALL issue an inclusion_promise on submission. A promised root absent from a sealed root_of_roots after the merge delay is registrar_abuse.
- **S4-I5**: Every root_of_roots seal SHALL be counter-signed by the witness_set and published to it. Presentation of divergent chains to different verifiers is registrar_abuse (equivocation); witnesses SHALL cross-check and report divergence.
- **S4-I6**: Burden shift on absence: an event absent from the anchored log but covered by a valid inclusion_promise held by the reader or shard operator establishes registrar_abuse; absence without such a promise establishes audit_evasion by the reader. Absence alone never establishes reader fault where a promise exists.
- **S4-I7**: Every owner MAY enumerate all access_events over objects they control, and every natural person MAY enumerate all access_events whose subject is that person, regardless of who controls the containing namespace. This right is exercised through the standing_audit_contract, is unconditional, and its exercise is itself logged.
- **S4-I8**: Every access_event is co-controlled by the owner of the object it concerns and, where the subject is a natural person, by that person. Any audit_query by any other party, including the registrar's own analytics beyond content-blind integrity maintenance, SHALL require that co-controller's consent_record or a judicial_access_contract, and SHALL itself be visible to the co-controller. Standing bulk-log contracts SHALL NOT be issued.
- **S4-I9**: The Audit Registrar SHALL be structurally separate from every state organ, regardless of query volume. Any volume threshold applied to readers SHALL aggregate by common control: volumes are summed across all readers sharing a beneficial controller resolved through S1, plus parties under an adjudicated collusion finding.
- **S4-I10**: Access_events of shape zk_predicate SHALL carry no subject-resolvable reference; they SHALL be keyed by blinded_tags. The registrar SHALL hold no index permitting grouping of zk sessions by subject; the audit channel is explicitly inside the S6 unlinkability scope. The subject enumerates by deriving its own tags. Cross-session correlation is permitted only under a judicial order compelling tag derivation by the subject or issuer. Pattern analysis over zk sessions SHALL run subject-side.
- **S4-I11**: For designated high-frequency low-stakes predicate classes under S6 epoch tokens, logging MAY be batched per gate per epoch as counts plus a sampled event stream; all other classes log per session.
- **S4-I12**: Summarization after the contest window SHALL preserve, per event, a sealed commitment (event hash, contract_ref, reader_ref under the Merkle root) sufficient to reconstruct reader, contract, shape and time when a court reopens a clawback-eligible case. Full detail SHALL be retained, owner-and-court visible only, for all events involving actors with open offender_standing or unexpired escrow, and for namespaces whose sensitivity class admits the concealed or gross classification.
- **S4-I13**: Every aggregate the registrar publishes, transparency_reports included, SHALL be registered in the polity-wide release register before publication, SHALL debit the shared budget accounts of affected cohorts, and SHALL conform to the approved cohort frames of S5. Publication without prior registration is audit_evasion.
- **S4-I14**: Transparency_reports SHALL include per-court statistics on judicial_access_contracts: petitions, grants, denials, renewals, and deferred-notice extensions, per petitioner class.
- **S4-I15**: An access_event MAY be sealed from subject enumeration only under a judicial deferred-notice order carrying a hard statutory maximum and at most one renewal; on expiry, notice is automatic and non-waivable, and the event enters the subject's enumeration. The independent special advocate for the underlying order retains visibility throughout the sealed period.
- **S4-I16**: The Audit Registrar mandate is a Charter Art. 10 concentration-charge subject. Its functions SHALL be structurally plural where feasible, and its roots SHALL be mutually anchored with peer registers per S8; no register vouches only for itself.

### Protocols

- **S4-P1 (gated read commit)**: 1. Reader presents capability token (S2) to the owner-side gate. 2. Gate executes the S4-I2 atomic commit: re-validation, use_count decrement, access_event append to the owner_gate_log. 3. Gate returns a shard-signed receipt to the reader and releases the projection (or the cache envelope key). 4. On any validation failure the commit aborts, no delivery occurs, and the denial is recorded in the indistinguishable envelope regime of S3.
- **S4-P2 (anchoring and witnessing)**: 1. Shard seals a segment and submits its root. 2. Registrar returns an inclusion_promise. 3. Registrar seals the root_of_roots within the merge delay. 4. Witness_set counter-signs and publishes; witnesses cross-check chains and file registrar_abuse on divergence or lateness.
- **S4-P3 (enumeration)**: 1. Owner or subject queries under the standing_audit_contract; the query is served from the local shard index and logged. 2. For zk events, the subject derives its tags and queries by tag; no registrar-side subject index exists to consult.
- **S4-P4 (third-party audit query)**: 1. Querent presents consent_record of the co-controller or a judicial_access_contract naming subjects individually. 2. Gate validates scope, executes S4-P1 against the log shard, and the co-controller sees the query event. 3. Bulk or standing requests are rejected at validation.
- **S4-P5 (transparency reporting)**: 1. Registrar registers the candidate aggregate in the release register. 2. Frame conformance and differencing checks run against the register's entire contents; budgets debit. 3. Publication proceeds only on registered approval.

### Lifecycle and edge cases

- (a) Standing_audit_contracts instantiate automatically at object creation and at first record of a natural-person subject; the registrar cannot decline, revoke or condition them.
- (b) Sealed events: at deferred-notice expiry the seal lifts without any action by the subject; a lapsed seal that fails to lift is registrar_abuse.
- (c) Shard operator failure: an owner_gate_log that stops anchoring becomes visible through missed cadence; its reads remain locally valid within the merge delay, after which unanchored segments are disputable and continued unanchored operation is audit_evasion by the shard operator.
- (d) Registrar compromise: handled under S8 key-compromise cascade; witnesses detect truncation and equivocation against counter-signed roots; inclusion_promises held by readers survive as reader-exculpating evidence per S4-I6.
- (e) Epoch-token reconciliation: batched counts reconcile against gate-side sampled streams at epoch close; divergence beyond tolerance opens an S7 case against the gate operator.
- (f) Registrar succession or plural re-constitution transfers the root chain under witness supervision; no gap in the chain is permissible, and the witness_set attests continuity.
- (g) Refusals of public_record requests by state organs are logged as denial events on the requesting person's enumeration, supporting the A6 expedited appeal.

### Interfaces

- **S1**: control resolution per read (default derivation rules; explicit ownership_record only on deviation); common-control resolution for S4-I9 aggregation.
- **S2**: capability tokens with sensitivity-class TTL (bounded-staleness horizon: revocation effective at worst one TTL, honestly stated there); judicial and emergency contracts as audit_query authority; standing_audit_contract as an S2 template; intra-organ access contracts whose reads S4-I1 logs.
- **S3**: gate co-location, projection_id derivation, cache envelope key release as the logged enforcement point, indistinguishable response envelopes for denials.
- **S5**: release register and shared budgets for every registrar aggregate; frame conformance.
- **S6**: blinded_tag construction, epoch-token batching classes, demand ledger aggregation over blinded tags.
- **S7**: registrar_abuse and audit_evasion classifications; S4-I6 burden shift replaces per se absence liability; evidence retention for clawback under S4-I12; preservation_orders freeze summarization of named scopes.
- **S8**: mutual anchoring, witness peering, compromise cascade, CERT notification on anchoring anomalies.

### External bindings

- Charter Art. 10: concentration self-charge on the Audit Registrar mandate (S4-I16).
- A6: judicial_access_contracts over log entries; expedited public_record appeals; deferred-notice ceilings.
- A12: the registrar's mandate instrument, fee schedule, and processing windows, with deemed referral to A6 on expiry.
- R3: shard segment roots and succession events append to the relevant registers.
- Value-Money-Coupling Â§4: S4-I12 retention spans the perpetual-clawback class.

### Open questions

1. Constitutional parameter values: the maximum merge delay per shard class and the witness quorum size are not yet fixed; both must be set before any Art. 10 plurality determination.
2. The minimum sampled-stream rate for epoch-token batched logging that still supports dispute reconstruction has no derivation yet.
3. Subject enumeration of blinded-tag events at population scale: whether tag-derivation query suffices as the normative minimum or private information retrieval must be mandated for some sensitivity classes.
4. Federated frames (A15/R6): whether foreign-frame registrars may count toward the witness quorum, and under what treaty attestation.

## S5. Cohorts, Aggregates and Statistical Sensing

### Purpose

S5 defines the only lawful path by which population-level knowledge leaves the Dimension. It exists to keep the sensing function of the polity (Charter Art. 6 floor monitoring, imbalance measurement, official statistics) alive without ever letting aggregate machinery become a person-grain read channel. Two distinct duties are served by two distinct cohort classes: release-eligible cohorts feed published aggregates under hard disclosure limits, and monitor-only cohorts guarantee that every person is covered by floor sensing at all times, including members of the smallest minorities whose cohorts could never safely publish. All aggregate egress, from every section of the cluster, converges on one release register and one budget discipline, so that no channel can be differenced against another.

### Object model

- **cohort_definition**: versioned, public, machine-readable predicate over registered attributes, carrying `class` (release_eligible or monitor_only), `axis_ref`, proposer, approver, status (Proposed, Active, Suspended, Retired). Retired definitions remain in the lattice corpus forever.
- **cohort_frame**: a pre-approved hierarchy of nested, non-overlapping partitions (for example region x age-band x sector), plus an enumerated list of approved intersection cohorts. Frames are versioned; frame version events roll budget windows.
- **cohort_instance**: the evaluated membership of a definition at a population state. Computed preferentially by distributed local evaluation inside each owner's trust boundary with secure aggregation; centrally only under S5-I11 and S5-I12. Member-level state is never exportable and never retained across computations.
- **aggregate_release**: a noised, k-floored statistic over release-eligible cohorts, published only after registration in the release_register.
- **release_register**: the single polity-wide register of every aggregate leaving the Dimension by any channel: S5 releases, S3 aggregate-shaped projections, S4 transparency reports, the S6 demand ledger, S8 incident statistics. Sole authority for frame, floor and budget compliance.
- **privacy_budget_account**: epsilon account keyed to a frame partition and a fixed calendar window enacted by A-cluster rulemaking, with a normed reserve fraction for ad-hoc queries. Shared across all publication channels.
- **adversary_model**: a published, versioned constitutional parameter stating the auxiliary knowledge every disclosure test presumes.
- **floor_breach_signal**: minimal event (axis, severity class, cohort_ref or blinded ref) emitted when a Charter floor is breached; carries no identities, counts or values.
- **sealed_evaluator**: the attested computation environment of the Statistics Steward, operating under the constitutional standing access contract of S5-I11.

### Invariants

- **S5-I1**: No aggregate SHALL be released unless every reported cell meets the k floor AND, for any attribute in a declared sensitivity class, an l-diversity or t-closeness condition. Failure of either SHALL cause suppression of the cell, never relaxation of the test.
- **S5-I2**: Inferability and differencing SHALL be evaluated against an adversary presumed to hold the complete population register, every prior entry in the release_register from every channel, and certain knowledge of any single target's cohort membership. The assumed auxiliary-knowledge set is the adversary_model; weakening it is a constitutional act.
- **S5-I3**: Every cohort_definition SHALL be public, machine-readable and versioned; ad-hoc cohorts are prohibited. Release-eligible definitions require full approval under S5-I4. Monitor-only definitions SHALL be registered ministerially: the registrar SHALL register on well-formedness alone, with no discretionary approval, and monitor-only cohorts SHALL never ground any aggregate_release.
- **S5-I4**: Approval of a release-eligible definition SHALL include a lattice test of the candidate against all active and retired definitions, evaluating intersections, differences and unions for sub-k or low-diversity residuals, rejecting on any residual. The test SHALL be executed and signed by an approver structurally independent of the proposer, SHALL re-run on every population refresh, and a definition that newly fails SHALL auto-suspend.
- **S5-I5**: Releases SHALL occur only along an approved cohort_frame or an explicitly approved intersection cohort. Conformance to the frame is checkable at the gate in constant time. Calibrated differential-privacy noise with per-frame epsilon accounting is the primary protection against residual inference within the frame.
- **S5-I6**: Every aggregate leaving the Dimension by ANY route SHALL be registered in the release_register before publication and SHALL debit the shared privacy_budget_accounts of the affected frame partitions. Publication without prior registration is audit_evasion under the S7 taxonomy.
- **S5-I7**: Budget windows are fixed calendar windows keyed to frame partitions; they roll on frame version events, not on membership churn. A successor or re-versioned definition SHALL inherit the spent epsilon of every overlapping predecessor pro rata; re-definition SHALL never reset an account. Exhaustion of the general allocation yields denial; the reserve fraction is dispensed through a priority queue by the Statistics Steward under its A12 mandate as arbiter, with a reasoned, queued denial appealable to A6.
- **S5-I8**: For every axis carrying a Charter floor, a monitor-only cohort covering every person SHALL exist at all times, auto-instantiated per axis. Absence of such coverage is itself a floor breach.
- **S5-I9**: A floor_breach_signal SHALL carry only axis, severity class and cohort reference. It SHALL never carry identities, member counts or attribute values.
- **S5-I10**: A signal over a sub-k cohort SHALL NOT be emitted at its own cohort_ref: it SHALL be pooled to the smallest ancestor cohort satisfying k, or emitted with the cohort_ref blinded so the receiver sees only axis and severity. Emission SHALL use randomized delay and a calibrated rate of mandatory cover signals over non-breaching cohorts, so the presence of a signal is not evidence of a breach. Every emission SHALL debit both the cohort account and each affected member's namespace account.
- **S5-I11**: The evaluator's ingestion of person-grain attributes SHALL occur only under a constitutional standing access contract enacted at Charter level, scoped strictly to computing registered cohort_definitions, and every ingestion run SHALL append an S4 access_event per source namespace class. No other legal basis exists for evaluator reads.
- **S5-I12**: The evaluator SHALL run on attested compute whose build is court-inspectable; loss of attestation SHALL suspend all releases and all signals until restored. Where distributed local evaluation with secure aggregation is feasible for a measure class, it SHALL be used, so that no single process assembles a person-grain corpus. Member-level working state SHALL be non-exportable and SHALL NOT persist across computations.
- **S5-I13**: Gate outcomes (denials, suppressions, budget exhaustions) SHALL be published only in aggregated, k-floored, budget-debited form. Per-event outcome disclosure on a cohort's public record is prohibited.
- **S5-I14**: An escalation from a floor_breach_signal MAY open an inquiry, but any court petition arising from it SHALL rest on evidence independent of the signal; the signal SHALL never supply the necessity finding for a person-grain order.
- **S5-I15**: The Statistics Steward is a Charter Art. 10 concentration-charge subject. Its functions SHALL be structurally plural where feasible, and its approval acts are S4-audited.

### Protocols

**Protocol 1: cohort definition lifecycle.**
1. Any A12-mandated organ, the Equity Ombudsman, or the Steward MAY propose a definition, declaring its class.
2. Monitor-only: the registrar checks well-formedness and registers; activation is immediate; the definition joins the lattice corpus.
3. Release-eligible: the independent approver of S5-I4 runs the lattice test against the full active and retired corpus and signs the result; the Steward, when proposer, SHALL NOT approve.
4. A public contest window precedes activation; approval, contest and activation events append to S4.
5. On every population refresh the lattice test re-runs; newly failing definitions auto-suspend pending revision.

**Protocol 2: aggregate release.**
1. The requester names frame partition, measure and window; the gate checks frame conformance (S5-I5) in constant time.
2. The gate verifies the release_register for the debit capacity of the affected accounts; exhaustion routes to the S5-I7 reserve path or denies.
3. The evaluator computes under S5-I11 and S5-I12, applies k and diversity tests (S5-I1) with suppression, then applies calibrated noise.
4. The release is registered in the release_register, budgets are debited, and only then is it published. Registration and publication events append to S4.

**Protocol 3: floor sensing and escalation.**
1. Monitor-only cohorts are continuously evaluated; a breach produces a floor_breach_signal shaped by S5-I9 and S5-I10.
2. Signals route to the Equity Ombudsman and to the imbalance function.
3. The Ombudsman MAY open an inquiry; any petition to A6 for person-grain access SHALL present signal-independent evidence (S5-I14) and proceeds as a judicial contract under S2.

### Lifecycle and edge cases

(a) A cohort at or near one member is registrable only as monitor-only; its signals pool or blind under S5-I10, so sensing never lapses and disclosure never occurs. (b) Retirement removes a definition from release eligibility but never from the lattice corpus. (c) Frame revision is an A-cluster rulemaking act; the new frame version rolls budget windows, and in-flight releases complete under the old version. (d) Attestation loss (S5-I12) suspends releases and signals; monitor-only coverage counts as breached under S5-I8 for the duration, which is itself a visible floor condition. (e) A channel outside S5 (transparency report, demand ledger, incident statistics) that publishes without registration commits audit_evasion; the release_register is the sole compliance authority for all of them. (f) Reserve-path denials queue with reasons and are appealable; silent starvation of a lawful statistical program is not a permitted steady state.

### Interfaces

- **S1**: default derivation resolves control of registers and cohort artifacts; the evaluator never becomes a controller of source objects.
- **S2**: the constitutional standing access contract of S5-I11 is an S2 instrument; all other evaluator reads are unlawful.
- **S3**: aggregate-shaped projections under any S2 contract SHALL register and debit per S5-I6; S3 shape discipline governs their form.
- **S4**: ingestion runs, approvals, registrations and emissions append as access_events; S4 transparency reports are themselves S5-I6 subjects.
- **S6**: demand-ledger statistics aggregate over blinded tags and pass the S5 floor before emission.
- **S7**: audit_evasion (unregistered publication), registrar_abuse (wrongful refusal to register a well-formed monitor-only definition) and the escalation limits of S5-I14 bind here.
- **S8**: incident statistics register per S5-I6; substrate attestation underpins S5-I12.

### External bindings

Charter Art. 6 (floors and the balanced-state condition, implemented by S5-I8 through S5-I10), Charter Art. 10 (concentration self-charge on the Steward, S5-I15), A6 (contest, appeal, escalation), A10 (taxonomy extension grounding audit_evasion), A12 (Steward and registrar mandates, annual statistical program and budget allocations), A16/R4 (attribute and population registers presumed known to the adversary_model).

### Open questions

1. Feasibility thresholds per measure class for distributed local evaluation with secure aggregation, and the criteria and authority for declaring a class infeasible under S5-I12.
2. Calibration of the cover-signal rate and randomized delay in S5-I10 against Ombudsman workload and detection latency for genuine breaches.
3. Concrete per-frame epsilon values and window lengths for the first enacted statistical program, and their revision cadence.
4. Migration of aggregates published before the release_register existed: whether and how legacy publications enter the differencing corpus of S5-I2.

## S6. Verification and Zero-Knowledge Attestation

### Purpose

S6 is the projection shape that moves no data: it lets any meta-object prove that a predicate holds (over 18, solvent, licensed, within quota, resident) without disclosing the underlying namespace. It instantiates the Meta-Universe Zero-Knowledge Policy Attestation profile (MU-V2-FED-014) at polity scale: commit to hidden state by fingerprint, prove a catalogued predicate over the commitment, package the proof as a verifiable credential, verify without learning anything else. S6 is the sharpest expression of default deny: the consumer gets exactly one bit, and even that bit leaves an audit trail whose own encoding cannot be turned into a tracker.

### Object model

| Object | Key attributes | Notes |
|---|---|---|
| predicate_definition | predicate_id; semantics_ref; input_schema; parameter_slots; demand_ceiling; freshness_class; epoch_token_eligible (bool); version; steward_ref | Machine-readable meaning of one provable statement; parameters (thresholds, dates, quota_ref) are bound at challenge time and shown to the prover |
| predicate_catalog | catalog; entry_status (candidate, active, deprecated, withdrawn); adoption_event_ref; review_record | The governed registry of all predicates lawful to demand or prove; an R1 instance under an A12 mandate |
| attestation_binding | r5_attestation_ref; subject_ref (R4); issuer_ref; commitment (semantic fingerprint); zk_capability_flags; validity; revocation_ref | Bridges an R5 attestation to ZK use: the issuer anchors a commitment against which proofs verify |
| challenge | nonce (high-entropy); verifier_ref; session_id; predicate_ref (versioned); resolved_parameters; issued_at; expiry | Single-use and short-lived; commits to the verifier identity, the session and the exact resolved parameters, so a relayed challenge cannot re-scope or re-home a proof |
| proof | challenge_ref; commitment_ref; proof_blob; verifier_binding; generated_at; freshness_class | Single-use; cryptographically bound to the challenged verifier; contains no stable subject identifier |
| verification_session | verifier_ref; challenge_ref; result (holds, fails, indeterminate); basis (subject initiative, S2 contract, statutory gate, judicial contract); s4_audit_ref | The verifier-side record; the prover-side record of the same session holds the resolved parameters and claimed basis as consent evidence |
| session_tag | tag_value; derivation (subject-held key + session nonce) | The only subject-referencing key on a zk audit event; unlinkable across sessions without the subject-held key |
| epoch_token | predicate_ref; epoch; re_randomizable_credential; revocation_epoch_ref | Derived once per epoch by the subject for designated high-frequency low-stakes predicates; re-randomized per presentation so cross-verifier unlinkability holds |
| revocation_registry | accumulator_state; epoch; entry_ref; publication_event | Privacy-preserving revocation (accumulator or status list); checking membership must not reveal which entry was checked |
| demand_ledger | verifier_ref; predicate_ref; demand_count over blinded session_tags; window; release_register_ref | Coercion-resistance instrument: counts proof demands aggregated over blinded tags; every emission passes the S5 floor and registers in the polity-wide release register before publication |

### Invariants

- S6-I1: Whenever a consumer's declared purpose is satisfiable by a catalogued predicate, the S2 access contract SHALL specify shape zk_predicate, and demanding any data-moving shape for that purpose SHALL be bookable as over_collection under S7.
- S6-I2: Audit, investigative, adjudicative and verification-of-the-attestation-itself purposes are exempt from S6-I1: predicate sufficiency for these purposes SHALL be judged against the requester's stated purpose including its evidentiary needs, is contestable before A6, and a good-faith data-shape request SHALL NOT book over_collection absent a prior ruling that the predicate sufficed for that purpose class.
- S6-I3: A verifier SHALL only demand predicates whose catalog entry is active, and a prover MAY refuse any predicate not in the catalog without penalty.
- S6-I4: Every proof SHALL verify against a commitment anchored in a valid, unrevoked, unexpired R5 attestation whose issuer held the required mandate at issuance time.
- S6-I5: Every challenge SHALL be high-entropy, single-use and short-lived, and SHALL commit to verifier_ref, session_id, the versioned predicate_ref with its exact resolved parameters, and a timestamp; a proof over a challenge missing any of these commitments SHALL verify as invalid.
- S6-I6: Every proof SHALL be bound to the challenging verifier's identity, and a proof presented by any party other than that verifier SHALL fail verification; a verifier that accepts a proof not bound to its own identity bears the resulting liability as its own act.
- S6-I7: Before generating, the prover SHALL be shown and SHALL durably record the resolved parameters and the claimed basis of the demand; this record is the consent evidence for S6-I10 and is authoritative over the verifier's account in any dispute.
- S6-I8: Two proofs generated by the same subject for different verification sessions SHALL be cryptographically unlinkable: no proof element, revocation check, transport metadatum, or audit-channel encoding may serve as a stable cross-verifier identifier; the audit channel is explicitly inside the unlinkability scope.
- S6-I9: The S4 access_event of a zk verification session SHALL be keyed by a per-session blinded session_tag derived from a subject-held key, SHALL carry no subject-resolvable reference, and the registrar SHALL hold no index permitting grouping of zk sessions by subject; the subject enumerates their sessions by deriving their own tags, and cross-session correlation is lawful only under a judicial contract compelling tag derivation by the subject or issuer.
- S6-I10: No meta-object, including any state organ, SHALL compel proof generation except through a subject-accepted S2 contract (including one auto-issued by the subject's consent-policy agent within its profile), a statutory gate enacted under A-cluster law, or a judicial contract under A6 due process.
- S6-I11: A verifier SHALL check revocation status no earlier than the freshness window declared by the predicate's catalog entry, SHALL treat an unverifiable revocation status as proof failure, and revocation or key compromise is effective against verification at worst one freshness window (or one epoch, for epoch tokens) after the revocation event; this bounded staleness is declared, not fictional.
- S6-I12: Proof demands exceeding the catalogued demand_ceiling for a predicate class SHALL be flagged in the demand_ledger and SHALL be bookable as coercive_demand under S7; the ledger itself emits only blinded-tag aggregates that pass the S5 floor, register in the polity-wide release register, and debit the shared release budgets before publication.
- S6-I13: A verifier that accepts any substitute for a verifying proof (visual inspection, self-declaration, cached prior result beyond freshness or epoch validity) at a gate where a proof is mandated SHALL bear the resulting liability as its own act.
- S6-I14: For predicate classes the catalog designates epoch_token_eligible (high-frequency, low-stakes), a subject MAY derive one epoch_token per epoch, re-randomized per presentation, verifiable offline against the last synchronized revocation epoch; S4 logging for these classes MAY be batched per gate per epoch (counts plus a sampled stream of blinded-tag events); full challenge-response with live revocation SHALL remain mandatory for all other classes.
- S6-I15: An issuer SHALL revoke an attestation binding within the catalogued notification window after learning that its underlying facts no longer hold, and the revocation SHALL be an auditable R5 event.
- S6-I16: Retaining the proof_blob or the challenge transcript beyond the session SHALL be bookable as over_collection under S7; the durable record of the session is the S4 access_event alone.
- S6-I17: Liability for a false positive verification SHALL attach in order of fault: to the subject if inputs were fraudulent, to the issuer if verification of facts was negligent or the revocation duty was breached, to the verifier if challenge, binding, freshness or epoch duties were skipped; each attachment books V4 anti-value and enters the S7 ladder.

### Protocols

Protocol 1: predicate catalog governance.
1. Any meta-object MAY propose a predicate_definition (semantics, schema, parameter slots, demand_ceiling, freshness_class, epoch_token eligibility claim).
2. The catalog registrar checks well-formedness and non-duplication against active entries within its normed processing window; expiry of the window without decision is deemed referral to A6 on the expedited track.
3. The steward of the referenced domain model (for example the Health sub-agent for a B10-derived predicate) reviews for minimality: the predicate must reveal no more than its stated bit; epoch_token eligibility additionally requires a low-stakes finding recorded in the review_record.
4. Adoption is an A-cluster rulemaking event; the entry becomes active with a version and an effective date.
5. Deprecation follows the same path; proofs against deprecated versions remain verifiable for adjudication under contemporaneous norms (Charter Art. 19).

Protocol 2: attestation issuance (binding to R5).
1. The subject requests an attestation from a mandated issuer (a registrar, an A14 authorizing sub-agent, a licensed organization).
2. The issuer verifies the underlying facts through its own lawful access (its register, or an S2-contracted projection).
3. The issuer writes the R5 attestation and an attestation_binding: subject anchor (R4), commitment to the attested values, ZK capability flags, validity, revocation method.
4. The subject receives and holds the credential; the issuance is an S4-visible event on the subject's timeline.
5. The issuer registers the binding in the revocation_registry at the current epoch.

Protocol 3: proof presentation and verification.
1. The verifier issues a challenge committing to its own identity, the session, the versioned predicate and the exact resolved parameters, plus its claimed basis.
2. The prover checks the demand: catalog entry active, verifier within demand_ceiling, basis stated; the prover is shown the resolved parameters and records them with the claimed basis (S6-I7), and MAY refuse if any check fails.
3. The prover derives the per-session session_tag from its subject-held key, then generates the verifier-bound proof over the committed attestation, bound to the challenge, including an unlinkable non-revocation argument for the current epoch.
4. The verifier checks proof validity, challenge binding including its own identity, issuer mandate at issuance, and revocation freshness; any missing binding fails the verification.
5. The verifier records the verification_session and the S4 access_event keyed by the session_tag (batched per S6-I14 for epoch classes); it acts on the single resulting bit; the proof_blob is discarded at session end (S6-I16).

Protocol 4: revocation and re-proof.
1. On learning of a fact change, the issuer revokes the binding and publishes the new accumulator epoch.
2. Verifiers whose freshness windows are open learn nothing retroactively; sessions concluded before the epoch remain valid as historical facts; the at-worst-one-window staleness of S6-I11 bounds the exposure.
3. Where a standing S2 contract requires a maintained predicate (for example quota compliance), the contract names a re-proof cadence; the subject re-proves against the new epoch, and failure to re-prove within the cadence reads as predicate failure, not as a data breach.
4. On subject key compromise (S8 role-split cascade), outstanding epoch_tokens and the tag-derivation key rotate with the R4 anchor; issuers re-bind, and proofs from the estimated compromise window are flagged disputable.

### Lifecycle and edge cases

An attestation binding lives from issuance to expiry, revocation, or issuer mandate loss; loss of the issuer's mandate freezes new proofs but does not erase concluded verifications. Guardianship (S1 delegation) lets a guardian prove predicates about a ward; the session record names both, and the event is visible to the ward and to the ward's independent advocate. Offline gates MAY verify epoch_tokens against the last synchronized epoch within the predicate's declared offline tolerance; beyond it the result is indeterminate, never a pass. Emergency access never fabricates a proof and never widens a predicate: an emergency grant under a pre-declared per-class S2 template with a declared S3 shape MAY stand in for a mandated proof at a gate, and every such crossing emits the loudest S4 events and enters mandatory post-hoc review. If a subject's proving keys are lost, the R4 identity register rotates the anchor and issuers re-bind; old commitments are revoked wholesale; loss of the tag-derivation key costs the subject convenient enumeration of past sessions but creates no linkage for anyone else, and the registrar cannot reconstruct one. A predicate whose semantics depend on versioned methodology (solvency over C7 valuations) always names the methodology version it was proved under.

### Interfaces

- S1: who may prove (owner or delegated guardian, within guardianship bounds and advocate visibility) and who may demand (grantee under contract).
- S2 and S3: zk_predicate is a contract shape; S3 projection policy SHALL rank it above all data-moving shapes when sufficient; consent-policy agents MAY auto-accept template-conformant low-sensitivity predicate demands.
- S4: every session logs through the owner-side gate as an access_event keyed by a blinded session_tag; the registrar holds no subject-resolvable index over zk sessions.
- S5: demand_ledger emissions are blinded-tag aggregates under the S5 floor, registered and budget-debited in the polity-wide release register before publication.
- S7: over_collection, coercive_demand, replay, binding-skips and false attestation land on the enforcement ladder under the extended taxonomy.
- S8: soundness of the cryptographic substrate (proof system, accumulator, key hygiene) and transport-level unlinkability (no per-subject channels, no stable session identifiers) are explicit S8 obligations; key compromise follows the S8 role-split cascade.
- R4 and R5: identity anchoring and the attestation registry; A14 (licensure), A16 (residence), A6 (judicial bases), C7 and F8 (solvency semantics), K10 and F6 (quota predicates), B1 and B12 (age).

### External bindings

- Meta-Universe MU-V2-FED-014 Zero-Knowledge Policy Attestation: commitment by semantic fingerprint, proof-as-credential packaging, revocability, attestation chaining.
- W3C Verifiable Credentials and W3C DID for credential and anchor formats (via R5 and R4).
- ISO/IEC 18013-5 mdoc selective disclosure as the pragmatic profile for in-person age and licensure gates.
- Re-randomizable anonymous credential schemes (BBS-family signatures) for epoch_token mechanics.
- Privacy-preserving revocation practice (cryptographic accumulators, status lists with unlinkable lookup).
- The concrete proof suite is deliberately unpinned here, pending the joint S8 cryptographic profile, per the MU document's own status note.

### Open questions

1. Who pins and rotates the cryptographic suite (proof system, commitment scheme, accumulator, tag derivation), the S8 CERT steward or a standards steward under A12, and how is suite migration executed without invalidating long-lived attestations or orphaning subjects' tag-derivation keys?
2. When a predicate's underlying methodology changes mid-validity (a C7 valuation revision shifting what "solvent" means), does an outstanding proof keep its as-proved semantics until expiry or fail at the next freshness check?
3. How long may offline tolerance windows lawfully stretch in disconnected regions before indeterminate results effectively deny services, and who bears that denial's anti-value?
4. What review catches misdesignation of a predicate class as epoch_token_eligible (a "low-stakes" gate that turns out to concentrate harm), and does discovered misdesignation retroactively reclassify the batched logs?

## S7. Access Enforcement and Breach

### Purpose

S7 is where the security cluster acquires consequences: it defines what counts as an access violation, how violations are detected and attested, how anti-value is booked against violators, and how remedies flow back to the harmed. It turns the one-sentence rule (nothing is readable without the owner) from a promise into an accounting invariant with a court behind it. S7 owns no data about content; it owns the breach case, the sanction, the remedy, and the evidence-preservation instruments that keep breaches provable.

### Object model

| Object | Key attributes | Notes |
|---|---|---|
| violation_class | class_code; definition_ref; base_sensitivity; ladder_entry_step | Closed taxonomy (see below), extensible only by A10 lawmaking; this section is the constituting A10 act for the listed classes |
| detection_signal | source (s4_anomaly, s3_watermark, manifest_reconciliation, honeytoken_hit, probe_rate_alarm, whistleblower, self_report, victim_complaint); confidence; evidence_refs; case_ref | The raw trigger; never itself a verdict; forensics are targeted and case-driven, never ambient scanning of circulating data |
| breach_case | case_id; violation_class; accused_ref; victim_refs; contract_ref (S2, nullable); norm_set_ref; status | Lifecycle provisional, attested, settled, revalued; contested cases become A6 cases |
| anti_value_booking | v4_charge_ref; magnitude; scope_factor; sensitivity_factor; reach_factor; provisional_flag | Same-tick V4 debit per Value-Money-Coupling; formula public and uniform |
| sanction | ladder_step (annotation, restriction, standing_loss, prosecution_ref); duration; conditions; issuing_authority | Steps compose; prosecution_ref points into A18 |
| remedy_order | victim_ref; restoration_plan; compensation_flow_ref; funding_source (escrow, clawback, restitution); anti_value_component (nullable); trace | Earmarked to the measured-harmed parties, fully traceable; MAY issue as pure restitution with no anti-value component for good-faith conduct (S7-I15) |
| preservation_order | issuer (court, accident_investigation_organ); scope_refs; trigger (petition, x3_auto); version_anchor (R3) | Freezes mutation of named scopes with R3-anchored versioning; auto-triggered against an owner's relevant scopes by any X3 incident involving that owner's systems or products |
| offender_standing | subject_ref; repeat_count; systemic_flag; escrow_exposure_multiplier; track_record_ref (B4) | Drives the trust-ramp: repeat offense tightens escrow automatically |
| safe_harbor_grant | reporter_ref (pseudonymous R4 binding); scope (report, evidence_conveyance); immunity_terms; validity | Covers both the report and conveyance of evidencing projections to a court, the audit registrar, or a competent oversight organ; revocable only by court finding of bad faith; contract terms purporting to waive it are void |
| publicity_event | case_ref; audience (public); trigger (state_organ_violation, gross_class) | Automatic, non-suppressible R3 event |

Violation taxonomy (violation_class values, each with a defined ladder_entry_step):

- **unauthorized_read**: no valid S2 authorization at generation time; includes every holding generated under a void or voided contract, from the moment of generation, and reuse of a cached projection by a cache operator outside the contract whose gate sealed it.
- **scope_creep**: a contract exists, the projection exceeded it in fields, grain, or time.
- **purpose_violation**: a lawful projection used outside the contracted purpose.
- **onward_disclosure**: passing a projection to a party outside the contract; also the class for breach of an S8 disclosure embargo, charged against the disclosure case's contract.
- **consent_coercion**: a grant extracted under duress or as an unlawful condition of service, judged against the K4 data-minimality schema per S2.
- **audit_evasion**: reading outside the S4 log, tampering with it, or structuring reads to defeat it; also publishing an aggregate through any channel without prior registration in the polity-wide release register (S5), an evasive S1 transfer of a subject inside an open case or preservation order, and a pretextual compromise declaration by a party under adverse process (S8).
- **registrar_abuse**: a registrar exploiting register custody beyond its A12 mandate; also wrongful or dilatory refusal of a well-formed filing (with compensation for demonstrated transaction loss), root equivocation, exceeding the normed anchoring cadence, and failure to seal a promised event (S7-I5).
- **state_organ_overreach**: any state organ reading person-grain data without consent basis or judicial contract; also unjustified refusal of a public_record request under S1's public_record classification.
- **evidence_spoliation**: destruction or mutation of data the holder knew or should have known was evidence, including breach of a preservation_order; carries an adverse-inference presumption in the underlying case.
- **over_collection**: demanding or retaining more than the least-knowledge shape sufficient for the declared purpose (S6-I1), subject to the oversight exemption of S7-I17.
- **coercive_demand**: proof or grant demands exceeding catalogued ceilings, including repeat-proof harassment under S6.
- **custodial_negligence**: breach of S8 substrate duties that enabled exposure, chargeable without any read having occurred.

### Invariants

- S7-I1: Every attested access violation SHALL book a V4 anti-value charge against the violator in the same tick as attestation.
- S7-I2: Charge magnitude SHALL be computed by one public, uniform, versioned function of scope (records touched), sensitivity (namespace class, B10-grade highest), and reach (parties the data could propagate to), with no per-case official discretion.
- S7-I3: Remedies SHALL flow restoration-first: the victim's position is restored (deletion downstream, correction, compensation in the harmed dimensions) before any punitive component, and every remedy flow SHALL be traceable to the specific victims.
- S7-I4: Every breach case SHALL be adjudicated under the norm-set and contract text in force at the time of the read, per the contemporaneous-norms doctrine; new evidence MAY reopen pricing, new norms SHALL NOT.
- S7-I5: Absence of a read from the sealed S4 log SHALL shift burden, not decide alone: absence accompanied by a valid registrar-signed inclusion promise is registrar_abuse by the registrar; absence without such a promise is audit_evasion by the reader.
- S7-I6: No charge SHALL be grounded on a revocation or voiding whose effective position in the S4 log is later than the read's append position; retroactive voiding operates only through a court instrument, and reads appended before that instrument are judged under the contract state at their append position.
- S7-I7: Concealment of a breach SHALL flip its charges into the perpetual-clawback class with no limitation period; honestly self-reported breaches settle finally.
- S7-I8: Sanctions SHALL follow the ladder (annotation, restriction, standing loss, prosecution) from the violation class's defined entry step; a step MAY be skipped upward only by court order, and never downward silently.
- S7-I9: State organs are subject to the same charge function as any violator; a settled state_organ_overreach or registrar_abuse finding SHALL emit an automatic, non-suppressible publicity_event.
- S7-I10: The audit registrar SHALL have independent standing: no organ under its active investigation may sanction, restrict, defund, or reassign it, and any attempt is itself state_organ_overreach; this shield SHALL NOT apply against courts or constitutional review, and any investigation invoked as a shield SHALL be validated by an independent court within a fixed normed window or lapse for shielding purposes.
- S7-I11: A breach that violates an inviolable right under Charter Art. 4, including wrongful emergency invocation over a personal namespace (B10, B11, B12, or any consent-protected scope), SHALL open an A18 criminal case and SHALL NOT be settleable as a value transaction alone; anti-value booking and owner compensation are additional consequences, never alternatives.
- S7-I12: A good-faith reporter SHALL book no anti-value even when the report is unsubstantiated, and disclosure of projections or derived artifacts that reasonably evidence an S7 or A18 violation to a court, the audit registrar, or a competent oversight organ SHALL book no anti-value; public disclosure is likewise protected where those channels are shown captured, exhausted, or complicit; knowingly false reporting is itself a violation charged under this model.
- S7-I13: Every detection, charge, sanction, and remedy SHALL itself be an append-only S4-audited event visible to both accused and victim.
- S7-I14: Repeat and systemic offenders SHALL have their externality-escrow exposure multiplier raised automatically by offender_standing; no separate enforcement decision is needed for the tightening.
- S7-I15: Invalidity SHALL never extinguish restrictive terms: a void or voided contract confers zero authorization while imposing the strictest obligations available in the bound projection policy, plus mandatory verified destruction of every instance and derived artifact generated under it, logged to S4; such holdings are unauthorized_read from the moment of generation, not from the finding. Conversely, a party who held or exploited in good faith under a later-reversed title or contract SHALL owe restitution and disgorgement via remedy_order with no anti-value component; anti-value and clawback attach only on a court finding of bad faith, concealment, or grossness under the contemporaneous norm-set.
- S7-I16: Obstruction of a granted judicial_access_contract or of a preservation_order (non-generation past the deadline, withholding, or degradation of ordered projections) SHALL be a distinct S7 violation carrying an adverse-inference presumption in the underlying case, and generation SHALL then be compellable through a court-appointed technical custodian.
- S7-I17: Data-shape or proof demands made for audit, investigative, adjudicative, or attestation-verification purposes SHALL NOT book over_collection absent a prior ruling that a catalogued predicate sufficed for that purpose class.
- S7-I18: Namespace classes designated accountability-critical (safety telemetry, financial ledgers, and peers listed in the A12 register) SHALL be append-only by norm, and their mutation outside a versioned correction event is evidence_spoliation per se.

### Protocols

Protocol 1: detection to attestation.
1. A detection_signal arrives: an S4 anomaly (reads without matching contracts, volume or pattern outliers, probe-rate breaches at owner gates), an S3 watermark commitment or detached manifest reconciled against S4 (possession of data matching a content hash with no matching access_event), a honeytoken hit, or a whistleblower or victim complaint under a safe_harbor_grant.
2. The audit registrar opens a breach_case in provisional status, freezes the accused's relevant escrow tranche, and notifies both the data owner (victim) and the accused; where the accused holds a registrar-signed inclusion promise for the contested read, the case routes against the registrar per S7-I5.
3. A provisional anti_value_booking is computed by the S7-I2 function and debited per Value-Money-Coupling mechanics (standing plus escrow, same tick, provisional); the charge is verified against S4 append order per S7-I6 before it books.
4. The accused MAY contest within the appeal window; an uncontested case attests and settles; a contested case becomes an A6 case with an independent reviewer, judged under the contemporaneous norm-set.
5. The court upholds, adjusts, or reverses; reversal voids the charge, restores escrow, and books the mispricing for calibration of the charging function.

Protocol 2: remedy and restoration.
1. On settlement, a remedy_order issues: first restoration (revocation of downstream projections, verified deletion where feasible, correction of derived records; for void-contract holdings, the verified destruction of S7-I15), then compensation to victims in the dimensions harmed.
2. Funding draws from the forfeited escrow tranche; shortfall triggers clawback against the violator's accumulated assets when the case is in the concealed or gross class; good-faith restitution cases fund from disgorged proceeds only.
3. Reopened clawback-eligible cases reconstruct reader, contract, shape, and time from the sealed per-event commitments S4 retains through summarization; the reach factor uses the court-set presumption where tracing is exhausted.
4. All remedy flows are earmarked and traced to the specific victims or victim cohorts; nothing routes to a general treasury.
5. The sanction ladder applies from the class's entry step; offender_standing updates, and the escrow multiplier tightens per S7-I14.

Protocol 3: state organ as violator.
1. Detection follows Protocol 1, but the audit registrar SHALL route the case directly to a court whose reviewer is independent of the accused organ and of its supervising branch.
2. Charges book against both the acting officer (personal standing) and the organ's mandate standing; the officer acts as the office and the audit trail records both, so both pay.
3. Wrongful emergency invocation over a personal namespace routes to A18 per S7-I11; repeat invocation against the same subject is a per se case regardless of individual justifications.
4. On settlement a publicity_event publishes the case summary automatically (S7-I9); suppression attempts are audit_evasion.
5. Systemic findings (a pattern of overreach) escalate to constitutional review of the organ's A12 or A-cluster mandate, up to mandate revocation.

Protocol 4: preservation and spoliation.
1. A preservation_order issues on petition by any party with A6 standing, or automatically when an X3 incident involves the owner's systems or products; it names scopes, anchors current versions in R3, and freezes mutation outside versioned corrections.
2. The owner acknowledges within a normed deadline; silence or non-compliance is evidence_spoliation and triggers appointment of a technical custodian who serves court-scoped projections from escrowed snapshots.
3. Later destruction or mutation of preserved scopes books evidence_spoliation with the adverse-inference presumption; a court finding of no pending or foreseeable claims is required before any preserved or escheated scope is destroyed.

### Lifecycle and edge cases

A breach_case follows provisional, attested, settled, revalued; revaluation reopens pricing on new evidence only. Edge cases: (a) wrongly used emergency access splits by scope: overreach on non-personal scopes is scope_creep with the emergency as context, not excuse; invocation over a personal namespace without lawful basis is an inviolable-rights breach under S7-I11 and goes to A18, with anti-value and compensation stacked on top; (b) a dissolved violator organization leaves its escrow and assets attached; successor liability follows the S1 transfer graph for the clawback-eligible class, and the escheat archive is retained across all limitation periods including perpetual clawback; (c) onward disclosure beyond the audit horizon caps provable reach, so the reach factor uses a court-set presumption when tracing is exhausted; (d) weaponized accusation is guarded by the uniform charge function, the good-faith test, the log-order rule of S7-I6 (backdated revocations cannot manufacture charges), and the symmetric mispricing charge of Protocol 1 step 5; (e) low-entropy leaks (small field subsets, ZK results) that cannot carry a per-grantee mark attribute to the holder set, not a single culprit: attribution requires corroborating S4 evidence, watermark commitments are opened only by courts and registrars (a finder learns nothing), and joint-and-several liability attaches only on a court finding; (f) who guards the audit registrar: its own reads are content-free by construction (it reads about reads), it is S4-logged like everyone, its cases are heard by courts, its standing shield carries the S7-I10 carve-outs, and as a singleton organ it carries a standing Charter Art. 10 concentration self-charge with mutual anchoring by peer registrars where feasible.

### Interfaces

- S1: preservation orders and custody interact with transfer freezes (court leave for transfers inside open cases); public_record refusals book here as state_organ_overreach; good-faith contested-ownership restitution uses remedy_order per S7-I15.
- S2, S3: the breached contract and projection policy are the norm the case is judged against; void-contract holdings inherit S7-I15 obligations; watermark commitments and detached manifests are primary detection sources.
- S4: evidence backbone; anomaly feeds open cases; inclusion promises drive the S7-I5 burden shift; sealed per-event commitments survive summarization for clawback reconstruction; every S7 action logs back into S4.
- S5: publication of any aggregate without release-register registration books audit_evasion; k-floor violations by a state reader surface as state_organ_overreach.
- S6: forged proofs enter as unauthorized_read; excessive proof demands as coercive_demand; the over_collection exemption of S7-I17 covers oversight purposes.
- S8: a cyber intrusion is an S8 incident; data actually read through it additionally books here; substrate-duty breaches book custodial_negligence; pretextual compromise declarations under adverse process book audit_evasion.
- V4, Value-Money-Coupling: charge, escrow, clawback, and remediation mechanics are reused, not redefined.
- A6, A18: contested cases and rights-violating breaches respectively; B4 reputation consumes offender_standing.

### External bindings

ODRL (duty, remedy, and prohibition semantics for contract breach), ISO/IEC 27035 (incident response lifecycle for case handling), ISO/IEC 27050 (electronic discovery and preservation, for preservation_order handling), GDPR Art. 33/34 breach-notification pattern (owner notification duty, as analogy not adoption), W3C Verifiable Credentials (safe_harbor_grant and sanction attestations), Merkle-anchored logs (tamper-evidence for S4-derived evidence), MOS Value-Money-Coupling and Courts-and-Adjudication doctrines (normative, internal).

### Open questions

1. Who calibrates the per-namespace sensitivity factors in the charge function, and through what contestation path, given that miscalibration is itself a capture surface?
2. How is whistleblower pseudonymity reconciled with the accused's right to confront evidence when the report is the only detection source?
3. What presumption should cap the reach factor for onward disclosure once data has propagated beyond the audit horizon, and who bears the burden of proving lesser reach?
4. When a violator organization dissolves and re-forms, does clawback-eligible successor liability follow assets, control, or both, and how is deliberate re-formation distinguished from ordinary succession without chilling legitimate restructuring?

## S8. Security Substrate: Keys, Incidents and Forensic Custody

### Purpose

S8 is the load-bearing layer beneath the access architecture: it governs the keys that sign grants, tokens and attestations, the conduct required of every actor operating infrastructure that holds or moves projections, the handling of security incidents (X3) and key compromise, the forensic custody of evidence when systems fail or are attacked, and the mutual anchoring that prevents any single register from vouching only for itself. S8 exists so that a cryptographic failure, a hostile intrusion, or a pretextual "incident" cannot be converted into either an unlogged read channel or a lawful stonewall against courts and auditors. Fail-closed at the gate is only as strong as the substrate under the gate; S8 is that substrate.

### Object model

- **key_binding**: the registered association of an actor to a signing key, typed by role: grantor, grantee, issuer, registrar, gate. Role typing drives the compromise cascade of S8-I4.
- **capability_token**: the signed, short-TTL authorization artifact minted at grant time (S2 side); S8 governs its key layer and the bounded-staleness horizon of S8-I3.
- **compromise_report**: a claim that a key or system is compromised, carrying reporter identity, evidence, an estimated compromise window, and a computed blast-radius estimate.
- **suspension_cascade**: the derived set of grants, reads, tokens and attestations suspended by a confirmed compromise, computed as a transitive walk over delegation and attestation-chain graphs.
- **x3_incident**: a registered security incident. Registration is append-only and names the registrant; the registrant is a first-class field because S2 emergency grants may only cite incidents registered by a party other than the invoker.
- **forensic_snapshot**: a sealed, R3-anchored, append-only capture of an affected system's relevant state, taken at incident declaration; carries an escrow_ref when the owner is under adverse process.
- **containment_attestation**: the signed assertion that a compromised system is contained, with the attesting party and evidence basis; subject to the deadline regime of S8-I8.
- **technical_custodian**: a court-appointed operator who serves court-scoped projections from escrowed snapshots when an owner fails or refuses to restore service under adverse process.
- **vulnerability_disclosure_case**: a coordinated-disclosure record with embargo terms, patch obligations and publication schedule.
- **anchoring_commitment**: a cross-signed register root published to a witness quorum, the unit of mutual anchoring under S8-I12.
- **envelope_key_service**: the owner-gate facility issuing short-lived keys for sealed cache envelopes (S8-I13).
- **incident_statistics**: aggregate threat and incident figures; publishable only through the polity-wide release register (S8-I11).

### Invariants

- **S8-I1**: Every actor operating infrastructure that holds, moves or serves projections, tokens, keys or audit material owes custodial duties of care defined per infrastructure class. Breach of those duties that enables exposure or loss SHALL be bookable as custodial_negligence under the S7 taxonomy, with its defined ladder entry, whether or not any read occurred.
- **S8-I2**: Key bindings SHALL be registered, rotated on normed schedules per role, and never shared across roles. A signature from an unregistered or role-mismatched key authorizes nothing.
- **S8-I3**: Authorization staleness is bounded, not fictional: revocation, suspension and key-compromise events become effective at worst one capability-token TTL after the event, with TTLs fixed per sensitivity class as published constitutional parameters. No component SHALL advertise instantaneous revocation; the bounded horizon is the honest guarantee.
- **S8-I4**: Key compromise cascades by role. Compromise of a grantor key suspends issuance and generation under that key's grants. Compromise of a grantee key suspends that grantee's reads across all contracts pending a new binding. Compromise of an issuer key suspends the attestation chain and every commitment anchored to it. Suspension SHALL walk delegations and attestation chains transitively, and projections and derived artifacts produced during the estimated compromise window SHALL be flagged disputable.
- **S8-I5**: Suspensions whose blast radius exceeds a declared threshold SHALL NOT auto-execute on report alone: they require corroborated evidence and immediate CERT and court review, and SHALL proceed as a tiered response, read freeze first, suspension second. Reinstatement SHALL restore prior grant and contract terms unchanged; re-issuance SHALL NOT be an occasion to extract new consent or renegotiated terms.
- **S8-I6**: An x3_incident SHALL exist as an independently registered event before any instrument relies on it. An emergency grant citing an incident registered by its own invoker is invalid at issuance (S2 enforces the matching gate).
- **S8-I7**: Registration of an x3_incident involving an owner's systems or products SHALL auto-trigger preservation over the relevant scopes: forensic snapshots sealed and R3-anchored, named scopes frozen against mutation under the preservation_order object (S7/S4 side). Where the owner is within the scope of an active judicial contract, preservation order or breach case, snapshots SHALL be escrowed outside owner control.
- **S8-I8**: A system in confirmed compromise SHALL NOT serve projections until containment is attested. For systems under adverse process, containment attestation is due within a normed deadline; on expiry the court MAY appoint a technical_custodian to serve court-scoped projections from escrowed snapshots, with the court-defined projection policy of the judicial contract governing shape. A pretextual compromise declaration SHALL be booked as audit_evasion.
- **S8-I9**: Discovered vulnerabilities in gate, registrar or steward software carry a patch duty with normed remediation windows per severity. Failure to remediate within the window SHALL be bookable as custodial_negligence; embargo breach within a vulnerability_disclosure_case SHALL be booked as onward_disclosure against the case's contract.
- **S8-I10**: No register vouches only for itself. Shard and register roots SHALL anchor on a bounded cadence into the Audit Registrar root-of-roots, and every published root SHALL be counter-signed by a quorum of independent witnesses, including peer registrars and the courts, each bearing an explicit consistency-checking duty. Anchoring lateness and root equivocation SHALL be booked as registrar_abuse. The authoritative log-integrity invariant lives in S4; S8 supplies and mandates the anchoring substrate.
- **S8-I11**: Threat and incident statistics SHALL leave the Dimension only through the polity-wide release register, debiting the shared budget accounts and passing the frame and k-floor checks like any other aggregate. Publication without prior registration SHALL be booked as audit_evasion.
- **S8-I12**: Transport unlinkability for zk verification sessions is an S8 obligation: no per-subject channels, no stable session identifiers, no transport metadata usable as a cross-verifier correlator. The audit channel is explicitly inside the unlinkability scope; S8 infrastructure SHALL hold no index permitting grouping of blinded session tags.
- **S8-I13**: For declared sensitivity classes, no store outside the owner trust boundary SHALL hold projection plaintext. Cache entries SHALL be sealed under short-lived keys from the envelope_key_service; every key fetch is simultaneously the revocation check and the logged read. Cache reuse across contracts, grantees or purposes SHALL be booked as unauthorized_read by the cache operator.
- **S8-I14**: Gate responses SHALL be served in fixed envelopes with padded latency per shape class, so that grant, denial, suppression, exhaustion and revocation outcomes are indistinguishable on the wire; S8 enforces the transport half of the mandatory indistinguishability that S3 declares. Probe rate limits per (reader, owner) apply at the substrate.
- **S8-I15**: Attestation infrastructure for sealed computation (the S5 evaluator and any successor) SHALL be court-inspectable, with reproducible builds; loss of attestation SHALL signal S5 to suspend releases and floor signals until restored.
- **S8-I16**: The CERT steward and Registrar-General, like the Audit Registrar and Statistics Steward, are Charter Art. 10 concentration-charge subjects: their mandates self-book concentration anti-value, and their functions SHALL be structurally plural where feasible, with mutual anchoring across peers as the minimum plurality.

### Protocols

**Protocol 1: Coordinated vulnerability disclosure.** (1) A reporter files a vulnerability_disclosure_case with the CERT steward. (2) The steward triages severity and sets embargo terms and the patch window per S8-I9. (3) Affected operators receive notice under the embargo contract. (4) Patches deploy within the window; the steward verifies. (5) On window expiry or verified remediation, the case publishes through the release register. (6) Missed patch windows book custodial_negligence. (7) Embargo breach books onward_disclosure against the disclosure case's contract.

**Protocol 2: Key compromise handling.** (1) A compromise_report is filed by the key holder, a counterparty, the CERT steward, or automated detection. (2) The engine computes the blast radius; below the S8-I5 threshold, the role-split suspension of S8-I4 executes immediately; above it, a read freeze executes while CERT and court review the evidence. (3) The suspension_cascade walks delegations and attestation chains transitively. (4) Projections, tokens and derived artifacts from the estimated window are flagged disputable in S4. (5) The holder re-binds under a fresh key with R4 verification proportionate to role and blast radius. (6) Reinstatement restores prior terms unchanged per S8-I5; the whole episode is S4-visible to affected owners.

**Protocol 3: Incident containment and custody.** (1) An x3_incident is registered; the registrant is recorded and S8-I6 applies. (2) Preservation auto-triggers per S8-I7: snapshots sealed, scopes frozen, escrow engaged where adverse process exists. (3) The operator contains; serving is suspended per S8-I8. (4) Containment_attestation is filed and reviewed; for systems under adverse process the normed deadline runs from registration. (5) On deadline expiry without attestation, the court appoints a technical_custodian who serves court-scoped projections from escrow. (6) Closure emits incident_statistics through the release register only.

### Lifecycle and edge cases

(a) **Pretextual incidents.** An incident declared by a party under adverse process triggers automatic review; a finding of pretext books audit_evasion and does not pause the custodian path.
(b) **Compromise claims as denial of service.** Repeated or induced compromise_reports against a registrar or large issuer meet the S8-I5 evidence gate; a bad-faith reporter is bookable under the S7 ladder, and the tiered freeze limits the damage of any single false claim to one TTL of read capability.
(c) **Compromise during an open judicial read.** The judicial contract survives the suspension_cascade; service resumes via re-bound keys or the custodian path, never by lapsing the court's access.
(d) **Registrar-spanning incidents.** Where an incident touches a witness of another register's roots, the witness quorum re-forms without the affected party and re-anchors; a quorum that cannot re-form is itself an x3_incident.
(e) **Attestation loss.** Loss of evaluator attestation is not an offense but suspends S5 outputs per S8-I15 until re-attestation; concealing the loss is audit_evasion.
(f) **Succession of the CERT steward or Registrar-General.** Mandate transfer follows A12; keys never transfer, successors bind fresh keys and the cascade rules of S8-I4 apply to the predecessor's bindings.

### Interfaces

- **S1**: custodianship and control resolution feed blast-radius computation; preservation freezes interact with S1 disposition rules.
- **S2**: capability-token TTLs implement S8-I3; emergency grants validate their cited x3_incident against S8-I6; judicial contracts survive cascades per edge case (c).
- **S3**: envelope sealing (S8-I13) and response indistinguishability transport (S8-I14) implement S3's cache and anti-inference invariants; watermark commitment keys are registrar-held key_bindings.
- **S4**: owner-side WAL appends, shard-root anchoring, inclusion promises and witness cross-signing ride on S8-I10; disputable flags from Protocol 2 are S4 annotations.
- **S5**: evaluator attestation (S8-I15); incident_statistics flow through the same release register as all aggregates (S8-I11).
- **S6**: transport unlinkability for zk sessions (S8-I12); epoch-token revocation sync is a substrate duty.
- **S7**: S8 events book through the extended taxonomy: custodial_negligence, audit_evasion, registrar_abuse, onward_disclosure, unauthorized_read.
- **A6 / X3**: courts appoint custodians and review blast-radius suspensions; the X3 incident cluster is the registration authority Protocol 3 writes into.

### External bindings

- Charter Art. 10 (anti-concentration): S8-I16 concentration self-charges for CERT steward and Registrar-General.
- A12 mandates: steward appointments, patch-window and deadline parameters, witness-quorum composition.
- A10 lawmaking: TTL schedules, blast-radius threshold and containment deadlines are enacted constitutional parameters, published and machine-readable.
- R3 / R4 registers: snapshot anchoring and re-binding verification.
- A15 / R6 treaties: cross-frame witness participation where federated roots exist.

### Open questions

1. **Attestation trust roots.** Which hardware and build attestation roots the courts accept for S8-I15, and who audits the attesters themselves, remains open; structural plurality bounds but does not eliminate the trusted base.
2. **Federated incident response.** How CERT duties, witness quorums and cascade propagation operate across treaty frames (A15/R6) when a compromise spans polities is unresolved.
3. **Parameter calibration procedure.** The method for setting and revising TTLs per sensitivity class, the blast-radius threshold and containment deadlines (evidence base, revision cadence, who proposes) needs an A10 procedural annex.
4. **Long-horizon cryptography.** Watermark commitments and sealed per-event commitments must remain openable across perpetual-clawback horizons; the migration path for aging or quantum-vulnerable primitives without re-exposing sealed content is undesigned.