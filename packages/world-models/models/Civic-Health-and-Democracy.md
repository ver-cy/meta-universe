# Civic, Health and Democracy: the B10, A10, A13 specification

> **Status:** DRAFT v0.1 (2026-07-31). Deepens the civic layer of the [World Model Architecture](../World-Model-Architecture.md): B10 Personal Health (the most access-sensitive namespace; the person is always the sole controller), A10 Lawmaking and Legislative Voting (bills, readings, amendments, the vote, enactment), and A13 Elections (choosing officeholders). Register rows: B10, A10, A13 in [`world-models.csv`](../world-models.csv). Sits on the S cluster ([Security, Ownership and Access](./Security-Ownership-and-Access.md)), R1/R2 ([Registry and Ledger](./Registry-and-Ledger.md)), K2/X1 ([Actions and Events](./Actions-and-Events.md)), A18 ([Offense and Enforcement](./Offense-and-Enforcement.md)); it operationalizes the governance doctrine of [Value-Axes-Corridors-Voting](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Value-Axes-Corridors-Voting.md) and [Governance-Mechanics](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Governance-Mechanics.md). On conflict with the architecture summary, this document governs for these models.
> **Provenance:** six parallel specifiers (health record; health access; the legislative process; the vote and the voting doctrine; elections; and the shared democratic-integrity substrate), then five adversarial reviews (a surveillance-and-coercion attacker, a democratic-capture attacker, the doctrine keeper, an access-and-inclusion reviewer, a systems pragmatist: 54 findings, 22 critical, the sharpest set of any pass), then one revision under a 30-point resolution charter. Both flanks were load-bearing: a civic layer that only stopped capture, or only protected privacy, would fail the polity.

---

## 0. How the civic layer works

This is where the polity governs itself and where a person's most intimate data lives. Two commitments shape everything: a person is the sole sovereign of their own health record, and the vote is free, equal and coercion-resistant. Both rest on the layers below (S-cluster default-deny and S5 cohort sensing, R4 identity, K2/X1 append-only acts, A18 offenses) and encode the MOS governance doctrine rather than generic law.

**Health (B10, HACC).** The person is always the sole controller of their health namespace; there is no world-readable health field and every read is a consented or judicial projection, S4-logged and person-enumerable, with population sensing only at S5 cohort grain. The specification then reconciles that strict privacy with the realities that make health law hard: life-saving rescue of someone who cannot consent (a bounded presumed-consent doctrine for the clinical act, distinct from record access), familial genetics whose facts implicate non-consenting kin (loci-granular co-control even inside a relative's own self-disclosure), adolescent confidentiality (reproductive, mental-health and substance-use care ward-controlled by default), break-glass emergency access (organizationally independent, loudest-audit, with a single-responder tier for the field), a fast communicable-disease notify-only path so contact tracing is not stonewalled, and secondary use confined to distributed local evaluation so records never leave the subject boundary. Care and identity are delivered floors: the unregistered and the stateless are actively detected and given reachable care and a provisional franchise rather than left invisible.

**Lawmaking and voting (A10, VOTE).** The legislative process is an append-only chain from bill to enactment that updates A5 law at a version-timestamp for contemporaneous-norms adjudication, with mandatory lobbying disclosure, a discharge path so no committee can silently kill reform, germaneness so capture riders cannot hitch on must-pass bills, quorum bands fixed in law with an anti-boycott floor, and a floor-impact determination recomputed by an organ independent of the sponsor so a bill cannot route around the cohort veto by understating its harm. The vote itself operationalizes the doctrine: individual weighted plus quadratic voting with revocable topic-scoped delegation (liquid democracy), concentration caps pierced to a delegate's beneficial owner, and the load-bearing rule that floors and equity are never weight-scaled, so a minority cohort's protection cannot be voted away and its below-floor signal fires regardless of size.

**Elections and integrity (A13, CIVIC).** Elections grant a bounded office mandate through an independent, sortition-composed electoral body, on an equal franchise that is never scaled by the legislative weight doctrine, with anti-gerrymander tests that add partisan symmetry to cohort-floor protection, independent-expenditure money brought fully on-ledger, and a certified tally that stays exact (only secondary demographic cross-tabs are noised) so recounts remain possible. The shared democratic-integrity substrate carries the cryptography once for both referenda and elections: eligibility is proven without linking a ballot to an identity, weight is proven in zero knowledge without exposing a per-voter bracket, the public artifact is encrypted ballots plus tally proofs backed by a software-independent paper record, and coercion-resistance rests on indistinguishable decoy credentials plus an independent casting path that stays open after the public cutoff, so a coercer who watches the voter to the deadline still cannot force the outcome. Epistemic integrity acts on concealment, coordination and purchased reach in real time during the pre-vote window, and never on the truth of a claim, so manipulation is checked without licensing censorship of dissent.

Three commitments recur, matching the rest of the model:

1. **The sovereign is never overridden silently.** Health control never lapses; guardianship is explicit and never proxies a vote; break-glass and emergency powers are the loudest audits in the polity.
2. **The vote cannot be bought, coerced, or captured.** Decoy credentials and an independent casting path defeat the watching coercer; zero-knowledge weight and encrypted tallies keep the ballot secret; beneficial-owner piercing and on-ledger money defeat accumulation.
3. **Both flanks delivered.** Care, the franchise and identity are funded, reachable floors, not nominal rights; and privacy, secrecy and the cohort floor are structural, not discretionary.

The sections follow: B10 health record; HACC health access; A10 legislative process; VOTE the vote and the voting doctrine; A13 elections; CIVIC democratic integrity.

---
## B10 personal health: the record and the care relationship

### Purpose

B10 governs the personal health record and the care relationship built on it. Health is the most coercion-sensitive namespace: exclusion from care and over-reach into the record are both catastrophic. This section makes the record subject-sovereign, keeps state sensing at cohort grain, disciplines every disclosure to a minimum-necessary projection, and reconciles that discipline with life-safety rescue, familial co-ownership of shared facts, adolescent confidentiality, and the reachability of care for the unregistered. Access-control mechanics (break-glass adjudication, the health-predicate ledger, the public-health-emergency notify path) are specified in HACC; B10 owns the record, the consent floor, the clinical act, export, co-ownership, and custody.

### Object model

- `health_record`: the subject-owned corpus, keyed on a single `B1/R4 subject_ref`.
- `encounter_projection`: a co-owned minimum-necessary view of one encounter, servable independently of its originating provider.
- `genomic_projection`: a genome view decomposed at `locus` granularity; each locus carries a `shared_variant` flag and, where shared, a set of identifiable `co_owner_ref`.
- `basis_binding`: the consent or lawful-basis record for an act or a read; carries a witnessed `record_time`.
- `break_glass_grant`: a scoped, time-boxed emergency access token (adjudicated per HACC-I5), filtered per B10-I13.
- `health_export`: a complete FHIR-conformant subject export; watermarked and traceable.
- `secondary_use_query`: a distributed evaluation descriptor; carries only an aggregation-share contract, never a person-grain pull.
- `provisional_identity`: a low-barrier anchor granting reachable care and franchise pending full R4 registration.
- `custodian_of_last_resort`: a designated B13 or public-health namespace that assumes the serving obligation on provider dissolution.

### Invariants

- **B10-I1** (subject sovereignty): The `health_record` is subject-owned and keys on a single `B1/R4 subject_ref`. The state senses health only at S5 cohort grain; no standing default performs a per-person state read.
- **B10-I2** (person-grain gate): Any per-person state read SHALL rest on the subject's consent or an A6 judicial contract. There is no standing person-grain ingestion default.
- **B10-I3** (minimization): Every disclosure SHALL be a minimum-necessary `encounter_projection` or `genomic_projection`, never a raw corpus dump, save the subject's own export under B10-I9.
- **B10-I4** (registration and identity floor): Absence of an R4 anchor is itself a monitored `floor_breach`, not an unsensed void. B14 field statistics SHALL drive active outreach detection of unregistered persons, and a low-barrier `provisional_identity` SHALL grant reachable access to essential care pending full registration. Care SHALL NOT be conditioned on prior registration.
- **B10-I5** (co-ownership of shared facts): A fact shared across persons (familial, genetic, or joint-encounter) is co-controlled. No co-owner SHALL unilaterally disclose a shared fact about a non-consenting co-owner, even framed as disclosure of the co-owner's own record.
- **B10-I6** (secondary use distributed-only): For B10 secondary use, distributed local evaluation with secure aggregation is MANDATORY: records never leave the subject boundary and only aggregation shares move. Centralized person-grain ingestion is permitted only under an A6 judicial contract, never as a standing default.
- **B10-I7** (sub-k floor sensing): Floor-breach detection SHALL NOT mean-pool a below-floor cohort's signal into a larger balanced ancestor, which hides the breach. A below-floor condition SHALL instead surface via a differential-privacy-noised COUNT of below-floor individuals under a dedicated low-count release exception, or a sealed monitor-only flag, that fires the breach signal without publishing membership. Sensing never lapses for the smallest cohorts.
- **B10-I8** (predicate discipline): Fitness and eligibility questions resolve to a capped, ledgered `zk_health_predicate` per HACC-I8. B10 forbids any predicate whose answer is a catalogued proxy for a protected condition; compound or serialized demands that jointly reconstruct a record raise a coercion signal and book `over_collection`.
- **B10-I9** (export plenitude and anti-coercion): The subject has an unconditional right to a complete, structured, FHIR-conformant `health_export` including all provenance. A compelled self-export or enforced portability demand is a prohibited demand on the S2 schedule, with the same rebuttable presumption of coercion as a coerced grant. Every export delivered to the subject SHALL be watermarked and traceable, so a coerced onward transfer is detectable and books `consent_coercion`.
- **B10-I10** (genomic loci-granularity): A `genomic_projection` SHALL be decomposed at loci. Every locus that is a shared variant with an identifiable co-owner is gated by co-control even inside a co-owner's self-disclosure. A "non-shared projection" means only privately-unique loci, never a raw genome export. Any unavoidable co-owner disclosure fires mandatory post-hoc notification plus objection and redaction rights for each implicated kin.
- **B10-I11** (consent floor and emergency clinical act): An elective clinical act SHALL rest on informed consent whose witnessed `record_time` strictly precedes the act; a true unconsented elective act is the wrong, opening an A18 inviolable-rights case even when it writes nothing. This invariant SHALL NOT criminalize rescue. A presumed-consent doctrine governs necessary life-saving acts on a person unable to consent and with no contrary advance directive: bounded to stabilization and the minimum needed, logged, post-hoc reviewed, honoring any known refusal, with the patient's ratification or objection right on recovery.
- **B10-I12** (adolescent default-confidential): A default-confidential set of decision classes (reproductive and sexual health, mental health, substance use) is ward-controlled by default from an age or maturity floor. An affirmative A6 finding, not a default, is required to override any such class into guardian visibility, so a controlling guardian cannot surveil the most coercion-sensitive care before any finding.
- **B10-I13** (break-glass scope): Break-glass grants record ACCESS, not the physical act (which B10-I11 governs). A single-subject `break_glass_grant` SHALL be filtered to the subject's own non-shared projection; shared-genetic facts are excluded unless a co-controller is independently a life-safety subject. Subject notification carries a hard maximum deferral horizon with automatic notice on expiry and periodic A6 re-justification to extend; the independent advocate receives undeferred real-time notice in every case. Independence, dual control, and the single-responder tier are adjudicated per HACC-I5.
- **B10-I14** (wrongful invocation and non-priceability): Wrongful emergency invocation over B10 routes through S7-I11 to an A18 inviolable-rights case. Health is non-priceable and non-votable: its protection grounds in Charter Art. 4 (bodily integrity and consent) and Art. 6 (per-cohort health floor).
- **B10-I15** (custody of last resort): On provider dissolution, a designated `custodian_of_last_resort` (a B13 or public-health namespace) SHALL assume the serving obligation for co-owned `encounter_projection` data, so the person's portability and access under B10-I9 remain actually reachable, not nominal.

### Protocols

- **B10-P1** (record and consent binding): A clinical write binds a `basis_binding` with a witnessed `record_time`. For an elective act the binding precedes the act; for a life-safety act under B10-I11 the presumed-consent basis is recorded contemporaneously and referred to post-hoc review.
- **B10-P2** (disclosure): A disclosure emits a minimum-necessary projection. Shared loci and shared facts are withheld unless co-control is satisfied; a proxy-for-protected-condition predicate is refused and booked under B10-I8.
- **B10-P3** (secondary use): A `secondary_use_query` executes as distributed local evaluation with secure aggregation. Records stay within the subject boundary; only aggregation shares leave. Any centralized person-grain path requires an A6 judicial contract and is logged as such. Floor sensing over the results follows B10-I7.
- **B10-P4** (break-glass access): An X3 life-safety incident, adjudicated per HACC-I5, opens a scoped time-boxed `break_glass_grant` filtered per B10-I13 to the subject's own non-shared projection. The single-responder tier permits one attester to invoke against a narrower scope with a louder audit, automatic A6 referral, and expedited review. Subject notice is deferred only within the hard horizon; the independent advocate is notified in real time. Kin implicated by any unavoidable shared-locus disclosure receive mandatory post-hoc notice with objection and redaction rights.
- **B10-P5** (export): A `health_export` is assembled complete and FHIR-conformant, watermarked and traceable, and delivered only to the subject. A demand that the subject perform and hand over this export is refused as a prohibited demand under B10-I9 and booked with the coercion presumption.
- **B10-P6** (custody handoff): On provider dissolution, co-owned `encounter_projection` data escheats under S1-I12 and the serving obligation transfers to the `custodian_of_last_resort`, which SHALL keep the person's projections reachable and portable.

### Lifecycle and edge cases

- **Unregistered person seeking care**: `provisional_identity` grants reachable essential care immediately; the R4-absence is flagged as a monitored `floor_breach` under B10-I4, and full registration backfills the anchor without gating the care already given.
- **Unconscious patient, no directive**: The clinician stabilizes under the B10-I11 presumed-consent doctrine and breaks glass only to the subject's own non-shared projection under B10-P4. On recovery the patient ratifies or objects; a standing refusal, if known, is honored and the act that overrode it is the wrong.
- **Break-glass touching the genome**: The grant is filtered to privately-unique loci. If a shared locus is unavoidable and no co-controller is independently a life-safety subject, the disclosure is withheld; where truly unavoidable, each implicated kin receives post-hoc notice, objection, and redaction rights.
- **Adolescent capacity transition**: Default-confidential classes stay ward-controlled from the maturity floor; only an affirmative A6 finding flips a class into guardian visibility, and the flip is class-specific, never blanket.
- **Provider dissolution**: The `custodian_of_last_resort` assumes serving; a person later needing history for new care reaches it through the custodian rather than a dead provider.

### Interfaces

- **Voting doctrine and capability floors**: Health is neither votable nor priceable away (Art. 4 bodily integrity and consent, Art. 6 per-cohort health floor). It is never placed on a measure to price or trade.
- **HACC**: owns break-glass adjudication (HACC-I5), familial co-control (HACC-I9), the health-predicate ledger (HACC-I8), the essential-care floor (HACC-I11), and the X3 public-health-emergency notify-only path; B10 supplies the record, consent floor, and export it acts on.
- **S2**: the prohibited-demand schedule carries compelled self-export and enforced portability (B10-I9).
- **S5 and B14**: cohort-grain sensing and field statistics driving B10-I4 outreach and B10-I7 sub-k breach detection.
- **S6**: `zk_health_predicate` evaluation under the B10-I8 cap and proxy bar.
- **B13**: custodian namespace for B10-I15.

### External bindings

- **S7-I11**: routes wrongful emergency invocation to the A18 inviolable-rights case (B10-I14).
- **A6**: judicial contract for any centralized person-grain read (B10-I6), the adolescent-override finding (B10-I12), and break-glass re-justification and referral (B10-P4).
- **A18**: inviolable-rights case for a true unconsented elective act (B10-I11) and for wrongful invocation (B10-I14).
- **X3**: the declared communicable-disease emergency scoping HACC's person-grain notify-only path.
- **FHIR**: the export conformance standard for B10-I9 and B10-P5.

### Open questions

1. Calibration of the age or maturity floor and the evidentiary standard for the B10-I12 A6 override finding, per default-confidential class.
2. Watermark robustness under B10-I9 against a coercer who re-encodes or paraphrases an export to strip traceability.
3. The beneficial-owner and identifiability threshold for co-owner piercing of shared genomic loci across distant or unlocatable kin (B10-I10).
4. The maximum length and A6 re-justification cadence for the B10-I13 notification deferral horizon before automatic notice fires.

## Health access, consent, emergency and secondary use

### Purpose

HACC governs how any party reaches into the B10 health namespace: for care, for a lawful fitness or eligibility check, for a life-safety emergency, for a declared public-health emergency, and for secondary (population) use. This is the civic and health surface where both exclusion and over-reach are catastrophic. A person denied reachable essential care or the ability to move their own record is a floor breach; a state, employer, insurer, landlord, or kin who reads or reconstructs a record without consent is an inviolable-rights breach. HACC binds every access path to consent primacy, minimization, coercion resistance, and loud audit, while keeping a bounded set of necessity carve-outs that never widen into standing surveillance. Health is neither votable nor priceable away (Charter Art. 4 bodily integrity and consent, Art. 6 per-cohort health floor).

### Object model

- **subject_ref**: the B1/R4 person the record concerns; where R4 personhood is absent, a low-barrier **provisional_identity** anchor stands in (HACC-I11) so access and the essential-care floor remain reachable pending full B12 registration.
- **access_grant**: a consent-bound, minimized, time-scoped projection over subject_ref, carrying purpose, projection spec (locus-level for genomic content), expiry, and provenance.
- **zk_health_predicate (S6)**: a single verified bit answering one lawful fitness or eligibility question without moving data; carries an issuer, a subject, and a **predicate_ledger** entry.
- **break_glass_incident**: an X3 life-safety record keyed to subject_ref, an **independent registering party**, an invoking clinician, a scope, an access horizon, and a **notification_deferral_horizon**.
- **genomic_projection**: decomposed at **loci** granularity; each locus is tagged privately-unique or **shared_variant** with an enumerated set of identifiable **co_owners**.
- **adolescent_capacity_finding (A6)**: a per-decision-class finding that either confirms ward control or affirmatively overrides a default-confidential class into guardian visibility.
- **phe_notice**: a person-grain, notify-only artifact under a declared X3 communicable-disease emergency, carrying an exposure fact, a minimum-necessary payload, a per-organ quota counter, and a hard sunset.
- **secondary_use_job**: a distributed local evaluation over subject-boundary records emitting only secure-aggregation shares; never a person-grain export by default.
- **serving_custodian**: the B13 or public-health namespace that assumes the serving obligation for co-owned encounter projections on provider dissolution (HACC-I12).

### Invariants

- **HACC-I1** (cohort-grain default): The state SHALL sense health only at S5 cohort grain. No standing path SHALL perform a per-person state read of B10. Person-grain access exists only through the four bounded gates: the subject's own consent, an A6 judicial contract, break-glass (HACC-I5), and public-health-emergency notify-only (HACC-I10). Each gate is loud, minimized, and audited under S4.
- **HACC-I2** (consent primacy and minimization): Every access_grant SHALL be consent-bound, purpose-limited, and reduced to the minimum projection sufficient for the stated purpose. A raw or whole-namespace export is never the minimum for a third-party purpose.
- **HACC-I3** (subject portability): A subject SHALL always retain a complete, structured, portable export of their own record. Exports delivered to the subject are watermarked and traceable so a coerced onward transfer is detectable and books consent_coercion (HACC-I8).
- **HACC-I4** (coercion presumption): Any grant, predicate answer, or self-export that a gatekeeper demands as a condition of a benefit, tenancy, employment, insurance, or service carries a rebuttable presumption of coercion; the demanding party bears the burden and an unrebutted demand books over_collection or consent_coercion under S2 and S6.
- **HACC-I5** (break-glass, independent and scoped): Break-glass SHALL require a registered X3 life-safety incident and SHALL fail closed on any shortfall. The registering party SHALL be organizationally independent of the invoker and free of any surveillance or adjudicative interest in the subject (an independent responder, or a treating facility distinct from any employer, insurer, or landlord relationship). Same-organization registration-and-invocation is presumptively wrongful in post-hoc review. A **single-responder tier** permits one attester to invoke with a self-registered incident, traded off against a narrower scope, an even louder audit, automatic A6 referral, and expedited mandatory post-hoc review, so solo field care is never blocked. The break-glass projection SHALL be filtered to the subject's own non-shared projection (HACC-I9); shared-genetic facts are excluded unless a co-controller is independently a life-safety subject. Access is bounded to a statutory horizon and to stabilization need. Subject notification carries a **hard maximum deferral horizon** with automatic notice on expiry and periodic A6 re-justification to extend; the independent advocate receives undeferred real-time notice in every case. Wrongful invocation routes through S7-I11 to an A18 inviolable-rights case.
- **HACC-I6** (adolescent default-confidential): A default-confidential set of decision classes (reproductive and sexual health, mental health, substance use) is ward-controlled by default from an age or maturity floor. A controlling guardian holds no visibility into these classes absent an affirmative A6 adolescent_capacity_finding that overrides the class into guardian visibility. The default is confidentiality; visibility requires the finding, never the reverse.
- **HACC-I7** (secondary use, distributed-only): For B10 secondary use, distributed local evaluation with secure aggregation is MANDATORY: records never leave the subject boundary and only aggregation shares move. Centralized person-grain ingestion is permitted only under an A6 judicial contract, never as a standing default. Floor sensing over secondary output SHALL NOT mean-pool a below-floor cohort into a larger balanced ancestor: instead it computes a differential-privacy-noised count of below-floor individuals under a dedicated low-count release exception, or raises a sealed monitor-only flag, so a sub-k breach still fires without publishing membership.
- **HACC-I8** (predicate ledger and prohibited demands): Every zk_health_predicate a gatekeeper issues against a subject SHALL be capped and ledgered. Compound or serialized demands that jointly reconstruct a record raise a coercion signal and book over_collection. A predicate whose answer is a catalogued proxy for a protected condition is forbidden and books over_collection. Compelled self-export and enforced portability are added to the S2 prohibited-demand schedule under the HACC-I4 coercion presumption; a coerced onward transfer of a watermarked export books consent_coercion.
- **HACC-I9** (genomic loci-granularity co-control): Any genomic projection is decomposed at loci granularity. Every locus that is a shared variant with an identifiable co-owner is gated by co-control even inside a co-owner's own self-disclosure. "Non-shared projection" means only privately-unique loci, never a raw genome export. Any unavoidable co-owner disclosure fires mandatory post-hoc notification plus objection and redaction rights for each implicated kin.
- **HACC-I10** (public-health-emergency notification): Bound to a declared X3 communicable-disease emergency, a narrow person-grain **notify-only** path SHALL exist (never open-record reading). It is minimum-necessary, dual-controlled, subject to a per-organ quota that fails closed, hard-sunset with the declaration, emits the loudest S4 events, and requires mandatory A6 post-hoc ratification. It closes the contact-tracing gap without any general person-grain read power.
- **HACC-I11** (essential-care and registration floor): Reachable essential care is a delivered Art. 6 floor for every person, including the stateless, undocumented, or never-registered. R4-absence is itself a monitored floor_breach: active outreach detection of unregistered persons via B14 field statistics plus a low-barrier provisional-identity path SHALL run, and provisional identity grants reachable access to essential care pending full B12 registration. Non-registration is a sensed breach, never an unsensed void.
- **HACC-I12** (custodian of last resort): On provider dissolution, a designated serving_custodian (a B13 or public-health namespace) assumes the serving obligation for co-owned encounter projections, so the person's portability and access remain reachable rather than nominal.

### Protocols

- **HACC-P1** (consent-bound access): Requester states purpose. The S5 cohort or B10 boundary computes the minimum projection. The subject grants (or an A6 contract authorizes). The grant is minimized, time-scoped, watermarked, and logged. For genomic content the projection is assembled locus by locus, and every shared-variant locus requires co-control from each enumerated co-owner (HACC-I9).
- **HACC-P2** (break-glass): An independent party registers the X3 incident. The invoker attests life-safety necessity. Dual control clears, or the single-responder tier engages with narrowed scope, louder audit, and automatic A6 referral. The projection is filtered to the subject's own non-shared projection. Access opens for the statutory horizon only. The independent advocate is notified in real time and undeferred; subject notice fires on or before the hard deferral horizon. Post-hoc review runs in every case, and any same-organization registration-and-invocation is presumptively wrongful.
- **HACC-P3** (public-health-emergency notify): On a declared X3 communicable-disease emergency, a dual-controlled operator issues person-grain phe_notice artifacts, minimum-necessary, drawing down a per-organ quota that fails closed when exhausted. No record is read open; only the exposure fact and minimal payload move. The path sunsets with the declaration and is A6 post-hoc ratified, with the loudest S4 events throughout.
- **HACC-P4** (secondary use): A secondary_use_job dispatches computation to each subject boundary; local evaluators return only secure-aggregation shares. Floor sensing over the result uses the DP-noised below-floor count or a sealed monitor-only flag (HACC-I7), never mean-pooling. Any person-grain ingestion instead requires an A6 judicial contract and is never a standing default.

### Lifecycle and edge cases

- **Unconscious patient, no directive**: The clinical act itself is governed by the B10-I11 presumed-consent doctrine (life-safety necessity substitutes for prior consent, bounded to stabilization, logged, post-hoc reviewed, honoring any known refusal, ratifiable on recovery). HACC governs only the record access, via break-glass filtered to the subject's own non-shared projection.
- **Break-glass into a genome**: Only the subject's privately-unique loci are exposed. A kin carrier status implicated by a shared variant is excluded unless that kin is independently a life-safety subject; any unavoidable co-owner disclosure fires post-hoc notice plus objection and redaction rights for each kin.
- **Solo field responder**: The single-responder tier (HACC-I5) lets care proceed with a self-registered incident, narrowed scope, louder audit, and automatic A6 referral, so dual control scales to field reality instead of failing closed against care.
- **Deferred notice pushed indefinitely**: The hard maximum deferral horizon fires automatic notice on expiry; extension requires periodic A6 re-justification, and the advocate is always notified undeferred, so a life-safety override can never become covert standing surveillance.
- **Sub-k minority below floor**: A 40-person below-floor cohort inside a balanced 10,000-person ancestor is never mean-pooled away; the DP-noised below-floor count or sealed flag fires the breach signal so the smallest, most vulnerable cohorts are never masked.
- **Adolescent-sensitive care before any finding**: The default-confidential classes are ward-controlled from the maturity floor; a guardian gains visibility only through an affirmative A6 finding, so the most coercion-sensitive care is never surveilled by default.
- **Provider dissolution**: Escheated co-owned projections pass to the serving_custodian (HACC-I12), preserving the subject's portability and access.
- **Stateless or unregistered person**: Outreach detection (B14) flags R4-absence as a floor_breach; provisional identity grants reachable essential care and a route to full registration.

### Interfaces

- **S5 / S6**: cohort lattice for cohort-grain sensing; predicate service enforcing the HACC-I8 ledger, cap, and proxy ban.
- **S2 / S4 / S7 / S8**: prohibited-demand schedule (now including compelled self-export); audit event stream; registrar independent-standing and inviolable-rights routing (S7-I11); attestation for distributed evaluators.
- **A6**: judicial contract for centralized ingestion, adolescent_capacity_finding, break-glass extension re-justification, single-responder referral, and public-health-emergency ratification.
- **B10 / B12 / B13 / B14**: health namespace and its I11 clinical-act doctrine; civil registration; custodian-of-last-resort namespace; field statistics for outreach.
- **X3**: emergency declaration that alone unlocks HACC-I10, and only for its duration.
- **A18**: routing for wrongful break-glass, over_collection, consent_coercion, and unconsented access as inviolable-rights or over-collection offenses.

### External bindings

- **Charter Art. 4** (bodily integrity and consent inviolable): grounds the non-priceability of health access and the inviolable-rights class for unconsented reads and coerced exports.
- **Charter Art. 6** (per-cohort health floor): grounds HACC-I11 essential-care and registration floors and the sub-k floor-breach detection duty.
- **Value-Axes corridor**: health floor at supermajority plus affected-cohort veto; never eliminated, priced, or traded, and never driven below floor.

### Open questions

1. Who maintains and recalibrates the catalogue of proxy predicates (answers that stand in for a protected condition) under HACC-I8, and how is drift audited as new proxies emerge?
2. The per-decision-class age or maturity floor for the HACC-I6 default-confidential set is jurisdiction-sensitive; the cross-jurisdiction baseline and its A6 override calibration remain to be fixed.
3. The differential-privacy budget for repeated HACC-I7 below-floor count releases must be bounded against cumulative re-identification of the smallest cohorts across many releases; the epsilon accounting rule is open.
4. Serving_custodian capacity and funding under a mass simultaneous provider dissolution, and the registration path for cross-border stateless subjects, are not yet fully specified.

## A10 the legislative process: bill to enactment

### Purpose

A10 governs the passage of a bill from introduction to enactment and the versioning of the A5 norm-set. It is the single normative authority for enactment and norm-set versioning: the vote and voting-doctrine section (VOTE) supplies the ballot, weight, secrecy and coercion-resistance envelope, and A13 supplies office elections. A10 protects the minority floor by routing floor-affecting measures through an entrenched path that no ordinary majority can bypass, and by placing the floor-impact determination outside the hands of the party that would breach it.

### Object model

- bill: {bill_id, sponsor_ref, subject_binding, text, measure_class, referral_ref, via_ref, lobbying_disclosure_ref, floor_impact_ref}
- measure_class: one of {ordinary, floor_change, emergency, norm_set_version}; fixes the applicable quorum and threshold band from the A5 norm-set, never sponsor-selectable per instance.
- amendment: {amendment_id, host_bill_ref, text, germaneness_finding, via_delta_ref}
- committee_referral: {referral_ref, committee_ref, received_time, report_deadline, report_ref?}
- value_impact_assessment (VIA): sponsor-authored projected per-cohort corridor impact; an input to deliberation, never the operative floor-routing authority.
- floor_impact_determination: {floor_impact_ref, evaluator_ref (S5 sealed evaluator), a6_gate_ref, recomputed_corridor_impact, discrepancy_flag, affected_cohorts[]}; the operative routing authority.
- discharge_petition: {petition_ref, bill_ref, threshold, signatures}
- quorum_rule_ref / threshold_band: fixed per measure_class in the A5 norm-set.
- emergency_instrument: {instrument_id, declared_time, single_instance_bound, aggregate_cap_ledger_ref, organ_ref}
- enactment_record: {enactment_id, bill_ref, norm_set_version, effective_time, floor_impact_ref}

### Invariants

A10-I1 Enactment is the sole act that writes a new A5 norm-set version. Every enactment_record SHALL bind the enacted text to a monotonically versioned A5 norm-set entry; no other section mints norm-set versions. VOTE and A13 cross-reference this act rather than restating it.

A10-I2 (floor principle vs floor value) The floor-PRINCIPLE is unamendable eternity-core content: no measure of any class SHALL eliminate, price, or trade a per-cohort floor, and no measure SHALL drive any cohort below floor. The floor-VALUE is adjustable only through the entrenched floor_change path (deep supermajority AND affected-cohort veto AND hysteresis, never below-floor). A measure purporting to eliminate, price, or trade a floor is void ab initio and never tallied; a lawful floor_change measure that adjusts a floor value within the entrenched path is expressly carved out and SHALL NOT be voided by this invariant.

A10-I3 (independent floor-impact recomputation) Whether a bill is floor-affecting SHALL be determined by the floor_impact_determination computed by the S5 sealed evaluator and confirmed at an A6 pre-enactment gate, recomputing the per-cohort corridor impact from attested B14 and S5 data. The determination SHALL NOT be read off the sponsor's VIA. A material discrepancy between the sponsor VIA and the independent recomputation blocks enactment and is a concealment signal under A18.

A10-I4 A floor-affecting bill SHALL route to the entrenched path (deep supermajority plus affected-cohort veto plus hysteresis). "Affected cohort" is defined through the S5 cohort-definition lattice under its independent-approver check, not by the sponsor. Any cohort-advocate has standing to force reclassification of a bill to the floor-affecting path.

A10-I5 (sub-k floor sensing) Floor-breach sensing for the corridor impact SHALL NOT mean-pool a below-floor cohort's signal into a larger balanced ancestor, which would mask the breach. Instead the evaluator SHALL compute a differential-privacy-noised count of below-floor individuals under a dedicated low-count release exception, or raise a sealed monitor-only flag, so a sub-k breach fires the floor-affecting routing without publishing cohort membership.

A10-I6 (measure-class parameters fixed) The quorum band and threshold band SHALL be fixed per measure_class in the A5 norm-set and SHALL NOT be selected by the sponsor or the referral committee per instance.

A10-I7 (germaneness) Every amendment SHALL be materially related to the host bill's subject. A non-germane rider SHALL be struck at disposition and MAY be refiled as its own bill with its own VIA, lobbying_disclosure, and vote. Bundling unrelated provisions onto a host bill is a procedural defect, not a permitted tactic.

A10-I8 (discharge) A referred bill SHALL receive a committee report or a floor vote within the report_deadline fixed for its measure_class. Failure to act within the interval is a recorded defect, not a silent death; on expiry a discharge_petition meeting the defined threshold SHALL move the bill directly to reading and vote, and the discharge path SHALL NOT be blockable by the bypassed committee.

A10-I9 (anti-boycott quorum) Repeated failure to reach quorum on a properly noticed measure SHALL, after a bounded number of attempts fixed in the A5 norm-set, convert to a present-and-voting quorum, so a minority cannot freeze the chamber by boycott. Deliberate quorum-denial against a floor-remedy item is a measured defect.

A10-I10 (emergency aggregate cap) Emergency instruments auto-expire unless re-enacted, and each is bounded per instance; additionally a hard aggregate cap SHALL bound cumulative emergency duration and consecutive election postponements per emergency and per organ. The aggregate cap is non-renewable past its limit by any body, including A6. On reaching the cap the ordinary norm-set and the electoral calendar restore automatically, and continued exercise of office is the A18 usurpation offense. Renewal beyond the cap requires the entrenched path plus affected-cohort involvement, never ordinary re-enactment.

A10-I11 (no guardian proxy) A legislative or referendum ballot SHALL NOT be cast by a guardian on a ward's behalf. Incapacity yields a dormant franchise or coercion-resistant assisted casting that renders the ward's own expressed choice; guardianship status alone never grounds franchise exclusion. This harmonizes with VOTE, A13 and CIVIC.

A10-I12 Concealment of floor impact, non-germane smuggling, discharge obstruction, or quorum sabotage each surface as A18 concealment or franchise-denial signals; the operative routing is never controlled by the party the routing constrains.

### Protocols

A10-P1 Introduction. The sponsor files the bill with subject_binding, a measure_class request, VIA, and lobbying_disclosure. The measure_class request is validated against the A5 norm-set; the applicable quorum and threshold bands attach automatically per A10-I6.

A10-P2 Referral and disposition. The bill is referred to committee with a report_deadline. Amendments are checked for germaneness (A10-I7) at disposition; non-germane riders are struck. On deadline lapse the discharge path (A10-I8) is available.

A10-P3 Independent floor-impact gate. Before any vote is scheduled, the S5 sealed evaluator computes the floor_impact_determination from attested data and an A6 pre-enactment gate confirms it (A10-I3, A10-I5). A discrepancy with the sponsor VIA blocks scheduling and books a concealment signal.

A10-P4 Routing and vote. A floor-affecting bill routes to the entrenched path (A10-I4); an ordinary bill routes to its fixed threshold band. Voting, TrackRecord weight (which applies to legislative weight-budget and referendum measures only), secrecy and coercion-resistance are performed under the VOTE envelope; A10 does not restate the ballot mechanics.

A10-P5 Enactment and versioning. On passage the enactment_record binds the text to a new A5 norm-set version (A10-I1) with effective_time and the floor_impact_ref of record.

A10-P6 Emergency instruments. An emergency_instrument records against the aggregate_cap_ledger; on single-instance expiry it auto-lapses, and on aggregate-cap exhaustion the ordinary norm-set and electoral calendar restore automatically (A10-I10).

### Lifecycle and edge cases

- Pocket veto attempt: a committee sitting on a bill past report_deadline triggers the discharge path; the inaction is recorded, not silent.
- Non-germane must-pass rider: struck at disposition, refileable as a standalone measure with its own assessment and vote.
- Sponsor under-reports cohort impact: the independent recomputation catches the discrepancy, blocks enactment, and books a concealment signal; a cohort-advocate may independently force floor-affecting routing.
- Quorum boycott: after the bounded attempt count, the measure proceeds on a present-and-voting quorum.
- Chained emergencies: bounded single instances that would otherwise chain indefinitely are stopped by the aggregate cap; past the cap, continued office is usurpation.
- Sub-k cohort breach: a small below-floor cohort inside a larger balanced ancestor still fires the floor signal via the DP-noised low-count path, never masked by pooling.
- Incapacitated voter: the franchise stays dormant or is exercised through coercion-resistant assisted casting rendering the voter's own choice; no guardian proxy.

### Interfaces

- A5 norm-set: the sole write target of enactment; measure-class quorum and threshold bands are read from it.
- S5 cohort lattice and sealed evaluator: define affected cohorts and compute the floor_impact_determination.
- B14 field statistics: attested data source for the corridor recomputation.
- A6: pre-enactment floor-impact gate, entrenched-path adjudication, and the aggregate-cap ceiling it cannot itself exceed.
- VOTE: ballot, weight, secrecy, and coercion-resistance envelope for legislative and referendum votes; A10 cross-references, never restates.
- A13: office elections and the electoral calendar restored on emergency-cap exhaustion.
- A18: concealment, franchise-denial, and usurpation offense routing.

### External bindings

- Floor principle binds to the Charter eternity core over Art. 4 and Art. 6; the floor value is adjustable only through the entrenched floor_change path.
- Floor-affecting routing binds to the S5 cohort-definition lattice and its independent-approver check.
- Emergency aggregate cap binds to the A13 electoral calendar and the A18 usurpation offense.

### Open questions

1. The exact report_deadline, discharge threshold, and bounded quorum-attempt count per measure_class are to be set in the A5 norm-set; their calibration against genuine deliberative need versus obstruction is unresolved.
2. The materiality threshold for a VIA-versus-recomputation discrepancy that blocks enactment (A10-I3) needs a calibrated definition that neither rubber-stamps nor deadlocks on noise.
3. The germaneness test (A10-I7) needs an operable subject-relatedness metric that a captured chair cannot weaponize to strike good-faith amendments.
4. The aggregate emergency-cap horizon (A10-I10) must be short enough to bar creeping entrenchment yet long enough for a genuine prolonged emergency; the value is not yet fixed.

## VOTE the vote and the voting doctrine: weight, quadratic, delegation

### Purpose
Define the weighted-voting doctrine for A10 weight-budget and referendum measures: TrackRecord-derived weight, a quadratic concentration discount, and receipt-free delegation, all under secret-ballot and coercion-resistance guarantees. Enactment, norm-set versioning, quorum bands, and threshold bands are governed by A10 and are cross-referenced here, not restated. Office elections are governed by A13 at equal unit weight. The shared cryptographic ballot substrate is CIVIC.

### Object model
- measure: classes {weight_budget, referendum, floor_change}; each bound to a measure_class in the A5 norm-set that fixes quorum_band and threshold_band (see A10). Bands are never sponsor- or instance-selectable.
- voting_weight: v_i = f(TrackRecord), capped at v_max. Weight is a private scalar bound to a pseudonymous credential; it is NEVER published as a per-credential bracket and NEVER rides on a ballot in the clear.
- franchise_credential: re-randomizable; carries a weight_commitment whose opening is never disclosed. The same credential proves EQUAL unit weight (v_i identically 1) when spent on an A13 office ballot.
- delegation: per-cycle delegator_pseudonym (never a real-identity delegator_ref), delegate_ref, topic_scope, weight_commitment, revocation token; active-versus-revoked state is decoy/override-style and third-party-indistinguishable.
- delegation_cap: concentration_threshold, quadratic_discount_curve, and a beneficial_owner binding.
- nullifier: per-measure, deterministic per credential-and-measure pair; supersedes any prior ballot from the same credential.
- demand_ledger: counts on-system proof-of-vote demands over blinded tags only.

### Invariants
VOTE-I1 (eligibility): the eligibility predicate proves only enrollment (following from R4 personhood) and franchise-qualification. It SHALL NOT include "not-yet-voted-this-measure." One-effective-vote is enforced at the bulletin board by a per-measure nullifier that supersedes any prior ballot, so re-casting stays permitted and indistinguishable. Stated identically in CIVIC and A13.

VOTE-I2 (weight scope): TrackRecord weight applies ONLY to weight_budget and referendum measures. An A13 office ballot proves v_i identically 1 and SHALL NOT prove or apply TrackRecord weight; the equal office-franchise is never scaled.

VOTE-I3 (weight secrecy): weight is applied at the aggregate without linking identity to choice. No per-credential weight value or bracket SHALL be published. Weight-and-cap conformance is proven in zero knowledge at tally. If any coarse bracket is ever published for audit, it SHALL satisfy a k-floor of holders enforced BEFORE issuance, and issuance of a credential whose bracket is under-populated SHALL be rejected. TrackRecord weight is a quasi-identifier and never a public per-ballot tag.

VOTE-I4 (quadratic discount): accumulated weight past concentration_threshold is quadratically discounted, so apex-by-accumulation is self-defeating.

VOTE-I5 (delegation receipt-freeness): delegation is a revocable instrument keyed to a per-cycle delegator_pseudonym. Its active-versus-revoked state SHALL be cryptographically indistinguishable to any third party (decoy/override-style). Only aggregate delegated weight is public at tally. Delegator identity and standing state are NEVER public or auditable per-credential.

VOTE-I6 (delegation Sybil pierce): the concentration_threshold and quadratic discount apply to the AGGREGATE delegated weight controlled by a common beneficial owner or coordinating cluster, via beneficial-owner piercing and correlated-voting plus control-linkage detection at tally, never per delegate credential in isolation. delegation_cap carries a beneficial_owner binding.

VOTE-I7 (floor principle, eternity core): the floor-PRINCIPLE is unamendable. No measure SHALL eliminate, price, or trade a per-cohort floor (Charter Art. 6), and no measure SHALL drive any cohort below its floor. Such a measure is void ab initio and never tallied. This bars elimination, pricing, and trading only, NOT lawful adjustment.

VOTE-I8 (floor value, entrenched path): the floor-VALUE is adjustable only through a floor_change measure on the entrenched path: deep supermajority AND affected-cohort veto AND hysteresis, never below-floor. This path is expressly carved out of VOTE-I7. Whether a bill is floor-affecting is recomputed by an organ independent of the sponsor (the S5 sealed evaluator and the A6 pre-enactment gate, see A10), never read off the sponsor's assessment; a discrepancy blocks enactment and is a concealment signal under A18.

VOTE-I9 (coercion-resistance primitive): coercion-resistance is load-bearing on decoy / panic-credential indistinguishability. A voter under continuous observation SHALL be able to cast an indistinguishable decoy under the coercer's eye while the real ballot is cast or restored undetectably. Last-vote-counts is a secondary convenience only; revote timing alone does not defeat an end-of-session coercer.

VOTE-I10 (delivered casting floor): an independent, coercer-inaccessible casting path (a supervised in-person booth or an offline re-randomization station) SHALL remain available after the public cutoff; decoy credentials issue there on demand and the last vote cast through it supersedes. Availability of this path is a delivered franchise floor. The demand_ledger detects only on-system proof-of-vote demands; offline face-to-face coercion is defeated by decoy indistinguishability, not by the ledger.

VOTE-I11 (public artifact): the public tally artifact is ENCRYPTED ballots plus zero-knowledge tally proofs, NEVER per-ballot cleartext choices under any pseudonym. Inclusion is verified against sealed ciphertext, not a readable choice. A software-independent voter-verified physical record SHALL back every contest, enabling risk-limiting audits independent of the crypto stack, with a documented voter-complaint path for a ballot not found on the board. Aligned with A13 and CIVIC to this single rule.

VOTE-I12 (certified count exact): a certified referendum or measure result is EXACT per-option counts: no noise, no k-floor. The k-floor and differential privacy apply ONLY to secondary demographic and turnout cross-tabs, never to the certified count, so recounts and close-margin audits stay possible.

VOTE-I13 (personal franchise): the franchise is personal and is NEVER cast by a guardian. Incapacity yields a dormant franchise or coercion-resistant assisted casting that renders the ward's own expressed choice, never a proxy. Harmonized with A13 and CIVIC.

VOTE-I14 (accessible coercion-resistant client): a coercion-resistant accessible client (an audio or tactile device that performs the cryptographic ceremony so no human sees the choice) SHALL be provided. Choice-revealing human-proxy assistance is forbidden; any accessibility gap that forces choice-revealing assistance is a franchise-floor breach, not an acceptable accommodation.

### Protocols
VOTE-P1 (cast): 1) prove eligibility (enrollment plus franchise-qualification, VOTE-I1); 2) form an encrypted ballot bound to the credential with weight proven in zero knowledge (v_i identically 1 for office ballots per VOTE-I2); 3) emit the per-measure nullifier; a later cast reusing the same nullifier supersedes the earlier ballot indistinguishably (VOTE-I1/I9); 4) obtain the software-independent verification record (VOTE-I11).

VOTE-P2 (delegate): 1) mint the delegation under a per-cycle delegator_pseudonym with committed weight (VOTE-I5); 2) revoke or override via a decoy/override token, keeping the standing state third-party-indistinguishable; 3) at tally, pierce delegated weight to the beneficial owner and apply the quadratic discount to the aggregate (VOTE-I6). Only the aggregate is public.

VOTE-P3 (tally): 1) verify each ciphertext's well-formedness and its weight-and-cap conformance in zero knowledge (VOTE-I3); 2) publish encrypted ballots plus the zero-knowledge tally proof, never cleartext choices (VOTE-I11); 3) certify exact per-option counts (VOTE-I12); 4) run a risk-limiting audit against the software-independent record.

VOTE-P4 (enact): the tallied outcome routes to A10 for enactment, norm-set versioning, quorum, and threshold-band application. VOTE does not restate enactment; see A10.

### Lifecycle and edge cases
- Re-vote: any number of re-casts is allowed; the last valid nullifier wins, indistinguishably (VOTE-I1/I9).
- End-of-session coercer: defeated only by decoy credentials plus the post-cutoff coercer-inaccessible path (VOTE-I9/I10), never by revote timing alone.
- Guardianship: a guardian NEVER casts; the ward's franchise is dormant or assisted per VOTE-I13.
- Accessibility: an unmet coercion-resistant-client need is a floor breach (VOTE-I14).
- Floor-change: adjustment only via the entrenched path with independent floor-affecting recomputation (VOTE-I8); a pricing, trading, or elimination measure is void ab initio (VOTE-I7).
- Under-populated bracket: credential issuance is rejected before any bracket could be published (VOTE-I3).

### Interfaces
- CIVIC: shared ballot substrate, decoy/panic credentials, demand_ledger, and receipt-free delegation; VOTE-I1/I9/I11 mirror CIVIC.
- A13: office elections at equal unit weight (VOTE-I2); a preference-delegation resolves to the delegate's slate ONLY for voters who do not cast their own ballot by the cutoff, and a cast secret ballot supersedes and is never provable to the delegate.
- A10: enactment, norm-set versioning, quorum bands, threshold bands, and the independent floor-affecting recomputation.
- S5: cohort-definition lattice and sealed evaluator for floor sensing. Below-floor detection uses a differential-privacy-noised count of below-floor individuals or a sealed monitor-only flag, never mean-pooling a below-floor cohort into a balanced ancestor.

### External bindings
- Franchise offense taxonomy (A18): vote coercion and intimidation are grounded in the Charter Art. 4 consent-and-liberty breach (non-priceable rights_violation); pure franchise denial or suppression routes through the Art. 6 cohort-floor severity band (priced-class cohort restitution plus the hard ladder per A18-I44). The non-priceable label is reserved for the Art. 4 hook; no "inviolable free-and-equal vote" status is claimed for the franchise.
- Independent expenditure to influence the vote is on-ledger, beneficial-owner-pierced, and counted toward the Art. 10 concentration self-charge under A13/CIVIC regardless of coordination; concealed reach is an A18 offense.

### Open questions
1. Calibration of the quadratic discount curve and concentration_threshold against coordinating-cluster detection false-positive and false-negative rates.
2. The exact k-floor and issuance-time population test for any audit bracket, given churn in TrackRecord weight between issuance and tally.
3. Operational hardening and geographic reach of the post-cutoff coercer-inaccessible casting path so it is a delivered floor and not a nominal one.
4. Beneficial-owner and coordinating-cluster definitions for delegation piercing that catch Sybil fronts without penalizing good-faith aligned delegation.

## A13 elections: candidacy, ballot, mandate

### Purpose

A13 governs contests for personal office: who may stand, how the office ballot is cast and counted, and how a mandate is assumed, bounded, contested, and surrendered. The A13 office franchise is EQUAL: every qualified elector casts one unit-weight ballot and the TrackRecord weight doctrine of A10 SHALL NOT touch an office contest. A13 defers to the VOTE section for the shared voting doctrine and to A10 for legislative enactment and A5 norm-set versioning; it restates neither. It relies on the CIVIC cryptographic and secrecy substrate for the ballot envelope and adds only the election-specific object model, districting, candidacy, mandate, and continuity rules.

### Object model

- **election_credential**: a franchise-qualification credential that proves enrollment and franchise-qualification only. For A13 office contests the credential proves an EQUAL unit weight (v_i identically 1); it never carries, proves, or applies a TrackRecord weight bracket. It re-randomizes per cast and supports decoy and panic variants indistinguishable from a genuine credential.
- **candidacy**: a candidate registration binding a person to a contest, carrying eligibility attestations, a conflict declaration, and an on-ledger influence_flow account. Candidacy exclusions are enumerable and narrow.
- **office_ballot**: an encrypted choice over a candidate slate bound to a per-measure nullifier. The ballot never carries a cleartext choice into any public artifact.
- **nullifier**: a per-contest, per-elector deterministic tag that enforces one-effective-vote by supersession: a later cast voids the prior ballot for that nullifier without revealing that a re-cast occurred.
- **district_definition**: a geographic partition carrying both a cohort-floor attestation and a published partisan-symmetry attestation (efficiency gap and mean-median difference over historical and predicted vote shares).
- **preference_delegation**: an advisory instrument keyed to a per-cycle pseudonym (never a real-identity delegator_ref), resolving to a delegate slate only for electors who do not cast their own ballot by the cutoff.
- **influence_flow**: an on-ledger value flow with a mandatory expenditure_target and an optional recipient_campaign_ref, beneficial-owner-pierced, counted toward the Art. 10 concentration self-charge.
- **mandate**: a time-bounded grant of office with a hard term clock and a caretaker-scope enumeration.
- **paper_record**: a software-independent voter-verified physical artifact enabling risk-limiting audits independent of the cryptographic stack.

### Invariants

- **A13-I1** (equal franchise floor): the office franchise is a delivered floor, equal, and SHALL NOT be scaled by the A10 weight-voting doctrine; every A13 office ballot proves v_i identically 1. This equal floor is never scaled, priced, or traded away.
- **A13-I2** (coercion-resistance): coercion-resistance rests on decoy and panic-credential indistinguishability per CIVIC-I5, not on re-vote timing. An elector under continuous observation SHALL be able to cast an indistinguishable decoy under the coercer's eye and have the real ballot cast or restored undetectably. An independent, coercer-inaccessible casting path (a supervised in-person booth or offline re-randomization station) remains available after the public cutoff, issues decoy credentials on demand, and its last vote supersedes. Last-vote-counts is a secondary convenience only; revote timing alone does not defeat an end-of-session coercer.
- **A13-I3** (public artifact): the public tally artifact is encrypted ballots plus zero-knowledge tally proofs, never per-ballot cleartext choices under any pseudonym. Inclusion is verified against sealed ciphertext. A paper_record backs every contest for risk-limiting audit, and a documented voter-complaint path exists for a ballot not found on the board.
- **A13-I4** (eligibility predicate): eligibility proves only enrollment and franchise-qualification. It SHALL NOT include a not-yet-voted term. One-effective-vote is enforced by a per-contest nullifier that supersedes any prior ballot, so re-casting stays permitted and indistinguishable. Stated identically to VOTE-I1 and CIVIC.
- **A13-I5** (capacity and conflict exclusion): every capacity-based franchise or candidacy exclusion is an individualized A6 adjudication with a mandatory independent advocate, decision-class-specific to voting, never cohort-wide or bulk-issuable, with a rebuttable presumption of franchise capacity and automatic roll-restoration if not finally adjudicated before the contest. Guardianship status alone never grounds franchise exclusion. Any bulk capacity purge is an A18 franchise-denial matter.
- **A13-I6** (districting test): a district_definition SHALL satisfy both the S5 cohort-floor test (no protected cohort isolated or diluted below its representational floor) and a published partisan-symmetry metric (bounded efficiency gap and mean-median difference over historical and predicted vote shares), recomputed on every population refresh. Failure of either auto-suspends the district.
- **A13-I7** (districting body): the districting body is structurally independent: sortition-selected from a screened pool, term-limited, barred from candidacy during and adjacent to service, and A6-supervised. Independence is constructed, not asserted.
- **A13-I8** (continuity on suspension): on auto-suspension the prior district_definition stays in force for FRANCHISE DELIVERY only, never for certifying a result under the defective map, until an independently approved replacement passes A13-I6. Suspension blocks certification, never the ballot.
- **A13-I9** (preference-delegation): a preference-delegation resolves to the delegate slate ONLY for electors who do not cast their own ballot by the cutoff; a cast secret ballot supersedes and is never provable to the delegate. The concentration cap and quadratic discount apply to the resolved non-casting weight aggregated to a common beneficial owner or coordinating cluster (beneficial_owner binding, correlated-voting and control-linkage detection at tally), never per delegate credential in isolation. The delegation is keyed to a per-cycle pseudonym; its active-versus-revoked state is cryptographically indistinguishable to any third party; only aggregate resolved weight is public at tally.
- **A13-I10** (expenditure reach): influence_flow covers any expenditure to influence the vote regardless of coordination, with expenditure_target mandatory and recipient_campaign_ref optional. All such flows are on-ledger, beneficial-owner-pierced, and counted toward the Art. 10 concentration self-charge. Coordinated and independent spending are both capped; concealed independent reach is an A18 offense.
- **A13-I11** (registration and identity floor): R4-absence is a monitored floor_breach, sensed by active B14 field-statistics outreach detection of unregistered persons over a low-barrier provisional-identity path. Provisional identity grants reachable access to the franchise pending full registration. Non-enrollment of a detectable person is a breach, not an unsensed void.
- **A13-I12** (mandate expiry): a mandate auto-expires at term. Continued exercise of office past expiry, without a validly assumed successor mandate or an A13-I13 caretaker grant, is the usurpation offense under A18.
- **A13-I13** (contest and caretaker): a successor result stays provisional through the contest window. On term expiry with an unresolved contest, powers reduce to a pre-enumerated caretaker set for a hard-capped interval under A6 supervision, never a full-mandate overstay and never a lapse of essential continuity.
- **A13-I14** (offense taxonomy): vote coercion and intimidation are grounded in the Charter Art. 4 consent and liberty breach (non-priceable rights_violation). Pure franchise denial or suppression routes through the Art. 6 cohort-floor severity band (priced-class cohort restitution plus the hard ladder per A18-I44). The non-priceable label is reserved for the Art. 4 hook; the franchise is not framed as an Art. 4 inviolable status the Charter does not grant it.
- **A13-I15** (certified tally is exact): the certified electoral tally is EXACT per-candidate counts, the definitive public act, with no noise and no k-floor, so recounts and close-race audits stay possible. The k-floor and differential-privacy protection apply ONLY to secondary demographic and turnout cross-tabs: a small or lopsided unit pools to a k-satisfying ancestor or is suppressed in the cross-tabs alone, never in the certified result.
- **A13-I16** (personal franchise and accessible client): the franchise is personal and NEVER cast by a guardian; incapacity yields a dormant franchise or coercion-resistant assisted casting that renders the elector's own expressed choice, never a proxy. A coercion-resistant accessible client (an audio or tactile device performing the cryptographic ceremony so no human sees the choice) is mandatory; choice-revealing human-proxy assistance is forbidden, and any accessibility gap that forces it is a franchise-floor breach, not an acceptable accommodation.
- **A13-I17** (emergency postponement cap): consecutive election postponements are capped in aggregate per emergency and per organ, non-renewable past the cap by any body including A6. After the cap the electoral calendar restores automatically and continued exercise of office is the A13-I12 usurpation offense. Renewal beyond the cap requires the entrenched path plus affected-cohort involvement, never ordinary re-enactment.

### Protocols

- **A13-P1** (candidacy): register the candidacy, attach eligibility attestations and a conflict declaration, open the on-ledger influence_flow account, and resolve any capacity or conflict exclusion through the A13-I5 individualized A6 path before ballot printing.
- **A13-P2** (cast): the accessible coercion-resistant client re-randomizes the election_credential, forms the encrypted office_ballot with its nullifier, and emits the paper_record. A decoy or panic credential produces an indistinguishable transcript. A later genuine cast supersedes via the nullifier without revealing supersession.
- **A13-P3** (districting): on every population refresh recompute both the A13-I6 cohort-floor and partisan-symmetry tests. On failure auto-suspend, hold the prior map for franchise delivery only per A13-I8, and route a replacement through the A13-I7 independent body.
- **A13-P4** (tally and certify): recompute the exact per-candidate count from encrypted ballots under the committed aggregation function, publish encrypted ballots plus zero-knowledge tally proofs, and run a risk-limiting audit against the paper_record. Certify the exact count; publish secondary cross-tabs only under k-floor and differential-privacy per A13-I15.
- **A13-P5** (mandate): assume the mandate on certification, keep it provisional through the contest window, and on unresolved contest at term expiry invoke the A13-I13 caretaker set for the capped interval.

### Lifecycle and edge cases

- **Re-vote and coercion**: a re-cast appends a fresh nullifier binding that voids the prior ballot; the two casts are indistinguishable, and the A13-I2 coercer-inaccessible path guarantees a final true cast even when a single channel is controlled through poll close.
- **Sub-k unit**: a below-floor or near-unanimous unit never perturbs the certified count; only the secondary cross-tabs pool to a k-satisfying ancestor or are suppressed, so close-race recounts remain exact.
- **District auto-suspension**: voters in a suspended district still receive a ballot under the frozen prior map, but no result is certified under a defective map until a replacement passes.
- **Provisional-identity elector**: a person detected by B14 outreach votes on a provisional identity; the franchise is delivered pending full registration and the R4-absence is booked as a floor_breach until closed.
- **Capacity exclusion pending**: if a capacity adjudication is not finally decided before the contest, the roll is restored and the elector votes under the rebuttable presumption of capacity.
- **Unresolved contest at term expiry**: caretaker powers apply for a hard-capped interval; overstay past the cap is usurpation.
- **Emergency postponement**: postponements accumulate against the A13-I17 aggregate cap; past the cap the calendar restores automatically.

### Interfaces

- **VOTE**: the shared voting doctrine, ballot envelope, and delegation crypto; A13 restates none of it and inherits its coercion-resistance primitive.
- **A10**: legislative enactment and A5 norm-set versioning; A13 cross-references rather than restates enactment.
- **CIVIC**: the cryptographic and secrecy substrate, decoy and nullifier machinery, and receipt-freeness guarantees.
- **S5**: the cohort-definition lattice and floor sensing used by the districting test.
- **A6**: capacity adjudication, districting supervision, postponement review, and post-hoc gates.
- **A18**: usurpation, bulk franchise-denial, concealed-reach, and coercion offenses.
- **B12 and R4**: enrollment anchor and the provisional-identity path.
- **B14**: field statistics powering registration-floor outreach.

### External bindings

- The certified per-candidate count is exact and carries no differential-privacy noise or k-floor.
- Differential-privacy and k-floor protections bind only to secondary demographic and turnout cross-tabs via S5.
- influence_flow beneficial-owner piercing binds to the Art. 10 concentration self-charge.
- Franchise offenses bind to the A18 severity bands per A13-I14 (Art. 4 for coercion, Art. 6 cohort-floor for suppression).
- Risk-limiting audits bind the paper_record to the cryptographic tally as an independent check.

### Open questions

1. The precise definition of "affected cohort" for candidacy and districting impact still resolves through the S5 cohort-definition lattice; the calibration of the independent-approver threshold is unsettled.
2. Deployment coverage of the accessible coercion-resistant client (audio and tactile hardware) is incomplete; until universal, isolated accessibility gaps risk being scored as franchise-floor breaches under A13-I16.
3. The integrity of the sortition pool feeding the A13-I7 districting body (screening without enabling exclusion of dissidents) needs an adversarial specification.
4. Diaspora and cross-jurisdiction franchise delivery under the coercer-inaccessible-path requirement of A13-I2 is not yet specified.

## Democratic integrity: identity, coercion-resistant balloting, anti-capture, epistemic integrity

### Purpose

CIVIC is the shared integrity substrate beneath A10 referenda and A13 elections. It defines who holds the franchise, how identity is anchored without becoming a surveillance handle, how a ballot is cast and tallied so that no third party can learn or be shown a choice, how money and coordinated deception are kept from capturing the vote, and how the smallest cohorts stay sensed. One ballot ceremony serves both processes, but only in its cryptographic and secrecy envelope: equality and weight differ by measure class. An A13 office ballot proves an equal unit weight; only A10 weight-budget and referendum measures ever apply TrackRecord weight, and never in the clear. CIVIC cross-references A10 for enactment and A13 for contest resolution rather than restating them.

### Object model

- franchise_credential: {subject_ref (B1/R4 or provisional_identity), enrollment_proof, franchise_qualification_proof, weight_commitment}. The weight_commitment binds a capped v_i usable ONLY on A10 weight-budget and referendum measures; it carries no third-party-readable value and no per-credential bracket. There is NO not-yet-voted field.
- ballot: {encrypted_choice (sealed ciphertext), per_measure_nullifier, zk_wellformedness_proof, zk_weight_conformance_proof, paper_record_ref}. The nullifier is deterministic per (credential, measure); a later ballot with the same nullifier supersedes the earlier one indistinguishably.
- delegation_token: {delegator_pseudonym (fresh per cycle), delegate_ref, scope, beneficial_owner, standing_state, revocation_token}. standing_state (active versus revoked) is a decoy/override construction, cryptographically indistinguishable to any third party.
- decoy_credential / panic_credential: issuable on demand, indistinguishable from a real credential to any observer including one watching the entire session.
- influence_flow: {source, beneficial_owner, expenditure_target (mandatory), recipient_campaign_ref (optional), amount}. Covers spending to influence a vote whether or not coordinated with a campaign.
- demand_ledger: counter of on-system proof-of-vote demands over blinded tags; scoped to on-system demands only.
- tally_artifact: {encrypted_ballots, zk_tally_proof, certified_counts}. certified_counts are exact per-candidate or per-option. Secondary demographic and turnout cross-tabs are a separate, k-floored and DP-protected artifact.
- floor_breach_signal: emitted from a DP-noised count of below-floor individuals or a sealed monitor-only flag; never from mean-pooling a sub-floor cohort into a balanced ancestor.
- epistemic_marker: {provenance, coordination_signal, concealed_or_purchased_reach}; annotative, never a truth verdict.

### Invariants

- CIVIC-I1: The franchise is a delivered floor. Every enrolled R4 person SHALL have a reachable, accessible casting path; absence of a reachable path is a franchise-floor breach, not a mere gap.
- CIVIC-I2: Registration and identity floor. The system SHALL actively detect unregistered persons via B14 field statistics and offer a low-barrier provisional_identity path. R4-absence for a detected person is itself a monitored floor_breach, never an unsensed void. provisional_identity grants reachable access to essential care and the franchise pending full registration.
- CIVIC-I3: The eligibility predicate proves ONLY enrollment and franchise-qualification. It SHALL NOT include "not-yet-voted-this-measure". One-effective-vote is enforced at the board by a per-measure nullifier that supersedes any prior ballot, so re-casting stays permitted and indistinguishable. This is stated identically in VOTE and A13.
- CIVIC-I4: A delegation_token and its revocation SHALL be receipt-free. The delegator is a per-cycle pseudonym; the active-versus-revoked standing_state SHALL be cryptographically indistinguishable to any third party. Only aggregate delegated weight is public at tally. Delegator identity and standing state are NOT public or auditable.
- CIVIC-I5: Decoy and panic-credential indistinguishability is the LOAD-BEARING coercion-resistance mechanism. A voter under continuous observation SHALL be able to cast an indistinguishable decoy under the coercer's eye while the real ballot is cast or restored undetectably. Last-vote-counts is demoted to a secondary convenience; revote timing alone does NOT defeat a coercer present at the close of polling.
- CIVIC-I6: The public tally_artifact is encrypted ballots plus zero-knowledge tally proofs, NEVER per-ballot cleartext choices under any pseudonym. Inclusion is verified against sealed ciphertext, not a readable choice. A software-independent physical record (voter-verified paper or equivalent) SHALL exist to enable risk-limiting audits independent of the crypto stack, and a documented voter-complaint path SHALL exist for a ballot not found on the board.
- CIVIC-I7: Weight-and-cap conformance is proven in zero knowledge at the tally; no per-credential weight value or bracket is published. TrackRecord weight is election-inert: on an A13 office ballot the ballot proves v_i identically 1 and NEVER proves or applies TrackRecord weight; weight applies only to A10 weight-budget and referendum measures. If any bracket is ever public it SHALL satisfy a k-floor of holders enforced before issuance, and issuance of an under-populated bracket is rejected.
- CIVIC-I8: Floor principle versus floor value. A measure SHALL NOT eliminate, price, or trade a per-cohort floor, and SHALL NOT drive any cohort below floor; such a measure is void ab initio and never tallied. This expressly carves out the entrenched floor_change path (deep supermajority plus affected-cohort veto plus hysteresis, never below floor), which lawfully adjusts a floor VALUE without touching the eternity-core floor PRINCIPLE.
- CIVIC-I9: influence_flow covers expenditure-to-influence-the-vote regardless of coordination. expenditure_target is mandatory and recipient_campaign_ref optional; all such flows are on-ledger, beneficial-owner-pierced, and counted toward the Art. 10 concentration self-charge. Concealed independent reach is an A18 offense. Coordinated and independent spending are both capped.
- CIVIC-I10: The delegation concentration cap and quadratic discount apply to the AGGREGATE delegated weight controlled by a common beneficial owner or coordinating cluster (beneficial-owner piercing, correlated-voting and control-linkage detection at tally), never per delegate credential in isolation. delegation_token carries a beneficial_owner binding.
- CIVIC-I11: Epistemic integrity annotates, never censors, and NEVER adjudicates truth. "Coordinated inauthenticity" turns strictly on concealment or deception of identity or funding, never on coordination itself. During the pre-vote quiet-and-scrutiny window, real-time coordination, provenance, and concealed-or-purchased-reach markers SHALL trigger immediate provenance and coordination annotations without waiting for falsification; "later-falsified" is NOT an independent trigger. Any false-claim booking requires contemporaneous falsity, scienter, and an objective amplification element, with the burden on the accuser and A6 review before any anti-value is booked, so legitimate minority organizing and good-faith heterodox dissent are never penalized. A6 MAY extend the contest or override window on a material last-window coordinated-manipulation matter.
- CIVIC-I12: The certified referendum or electoral count is EXACT per-option or per-candidate counts, the definitive public act, with no noise and no k-floor. The k-floor and differential privacy apply ONLY to secondary demographic and turnout cross-tabs; a small or lopsided unit affects only the cross-tabs (pooled to a k-satisfying ancestor or suppressed), never the certified result, so recounts and close-race audits stay possible.
- CIVIC-I13: Sub-k floor-breach detection SHALL NOT mean-pool a below-floor cohort into a larger balanced ancestor. Floor sensing SHALL instead emit a DP-noised count of below-floor individuals under a dedicated low-count release exception, or a sealed monitor-only flag, that fires the breach signal without publishing membership. This aligns with HACC and A10 floor sensing so the smallest cohorts are never masked.
- CIVIC-I14: Franchise offense taxonomy. Vote coercion and intimidation are grounded in the Charter Art. 4 consent and liberty breach (non-priceable rights_violation). Pure franchise denial or suppression routes through the Art. 6 cohort-floor severity band (priced-class cohort restitution plus the hard ladder per A18-I44). The non-priceable label is reserved for the Art. 4 hook. "Inviolable free-and-equal vote" phrasing is dropped; the franchise is an Art. 6 and Art. 12 floor, not an Art. 4 status.
- CIVIC-I15: The franchise is personal and NEVER cast by a guardian. Incapacity yields a dormant franchise or coercion-resistant assisted casting that renders the ward's own expressed choice, never a proxy. Guardianship status alone never grounds franchise exclusion.
- CIVIC-I16: A coercion-resistant accessible client (an audio or tactile device performing the cryptographic ceremony so no human sees the choice) SHALL be provided. Choice-revealing human-proxy assistance is forbidden. Any accessibility gap that forces choice-revealing assistance is a franchise-floor breach under CIVIC-I1, not an acceptable accommodation.

### Protocols

- CIVIC-P1 (enrollment and identity): Enrollment follows from R4 personhood; B14 field statistics drive outreach detection of unregistered persons; a detected R4-absence books a floor_breach and opens a provisional_identity that grants interim franchise and essential-care access pending full registration.
- CIVIC-P2 (unified ballot ceremony): A single ceremony serves A10 referenda and A13 elections identically in its cryptographic and secrecy envelope ONLY. The client proves enrollment and franchise-qualification (CIVIC-I3), seals the choice, emits a per-measure nullifier, and proves well-formedness in zero knowledge. For A10 weight-budget and referendum measures it additionally proves capped weight conformance in zero knowledge (CIVIC-I7); for A13 office contests it proves v_i identically 1. A voter-verified paper_record is produced (CIVIC-I6).
- CIVIC-P3 (delegation and revocation): A delegation issues a per-cycle delegator_pseudonym bound to a beneficial_owner; delegation and revocation are receipt-free with a decoy-indistinguishable standing_state (CIVIC-I4). At tally, aggregate delegated weight is pierced to beneficial owner and coordinating clusters for the concentration cap and quadratic discount (CIVIC-I10); only the aggregate is public.
- CIVIC-P4 (tally and audit): The board publishes encrypted ballots and a zero-knowledge tally proof; certified counts are exact (CIVIC-I12). A risk-limiting audit reconciles the certified count against the software-independent paper record (CIVIC-I6). Secondary cross-tabs are released only k-floored and DP-noised; sub-k floor sensing uses CIVIC-I13.
- CIVIC-P5 (in-window epistemic response): During the quiet-and-scrutiny window, real-time coordination, provenance, and concealed-reach markers surface immediate annotations (CIVIC-I11); a false-claim booking requires contemporaneous falsity, scienter, and amplification, with accuser burden and A6 review; A6 MAY extend the window on a material last-window manipulation matter.
- CIVIC-P6 (coercion-resistant casting paths): decoy and panic credentials issue on demand (CIVIC-I5); an independent, coercer-inaccessible casting path (a supervised in-person booth or offline re-randomization station) remains available after the public cutoff as a delivered franchise floor, where the last vote supersedes; the accessible client (CIVIC-I16) performs the ceremony with no human seeing the choice.

### Lifecycle and edge cases

- Re-vote and supersession: any later ballot with the same per-measure nullifier voids the prior one indistinguishably; exactly one effective vote counts (CIVIC-I3). No eligibility gate blocks a re-cast.
- Coercion at the cutoff: because a channel-and-timing coercer defeats last-vote-counts, CIVIC-I5 plus the CIVIC-P6 independent path carry the guarantee; a final true vote is always castable outside any single controlled channel.
- Small or lopsided unit: the certified count stays exact and recountable (CIVIC-I12); only cross-tabs pool or suppress; a near-unanimous small unit never de-anonymizes a choice because no per-unit cleartext is published.
- Sub-k cohort breach: the smallest below-floor cohort surfaces via a DP-noised count or sealed flag, never via pooling that hides it (CIVIC-I13).
- Guardianship: no guardian ever substitutes a ballot; a ward votes through assisted casting rendering the ward's own choice, or the franchise lies dormant (CIVIC-I15).
- Offline face-to-face coercion: the demand_ledger detects only on-system proof-of-vote demands; the offline case rests entirely on decoy/override indistinguishability (CIVIC-I5), not on the ledger.
- Provider or registrar absence: reachable access and portability degrade to the provisional_identity and custodian-of-last-resort pathways so no person is stranded.

### Interfaces

- A10: enactment, norm-set versioning, and floor-affecting classification are normative in A10; CIVIC supplies the integrity substrate and cross-references A10 rather than restating enactment.
- VOTE: the vote and voting doctrine section; CIVIC-I3, CIVIC-I5, CIVIC-I6, CIVIC-I7, and the guardian rule are stated identically across VOTE, A13, and CIVIC.
- A13: elections and districting; CIVIC-I12 governs the certified-versus-cross-tab split; capacity exclusions are A6-adjudicated per A13.
- S5 cohort-definition lattice and S6 zk predicate: cohort grain and predicate discipline for floor sensing and eligibility.
- A6: pre-enactment and adjudicative gate for floor classification, capacity exclusion, epistemic booking review, and window extension.
- A18: franchise-denial and concealment offenses, severity bands per CIVIC-I14.
- B14: field statistics feeding registration outreach (CIVIC-I2).
- X3: declared emergencies bounding any emergency electoral action.

### External bindings

- Charter Art. 4 (consent and liberty; the non-priceable hook for vote coercion), Art. 6 (cohort floor; franchise suppression band), Art. 10 (concentration self-charge for influence_flow), Art. 12 (franchise floor), Art. 21 (eternity core over the floor principle).
- Software-independent paper record and risk-limiting audit standards for CIVIC-I6.
- Differential-privacy release standards for secondary cross-tabs (CIVIC-I12) and sub-k breach counts (CIVIC-I13).
- Zero-knowledge proof system for weight-and-cap conformance and tally correctness (CIVIC-I7, CIVIC-P4).

### Open questions

1. Parameter governance for the k-floor and DP epsilon on secondary cross-tabs versus the low-count release exception for sub-k breach detection: who sets and audits these so protection and floor-sensing stay jointly satisfiable.
2. Certification and supply-chain trust for the coercion-resistant accessible client (CIVIC-I16): how the audio or tactile ceremony device is attested so the accommodation does not become the weakest link.
3. Detection thresholds for beneficial-owner and coordinating-cluster piercing in delegation (CIVIC-I10) and independent expenditure (CIVIC-I9) that catch Sybil fronts without chilling lawful coalitions or good-faith joint organizing.
4. Operational definition of "affected cohort" via the S5 lattice and the exact bounds of the quiet-and-scrutiny window (CIVIC-I11), set so neither can be gamed by strategic timing.