# Property and Ownership: the P2, M3, U1, F8 specification

> **Status:** DRAFT v0.1 (2026-07-31). Deepens the property-bearing nouns of the [World Model Architecture](../World-Model-Architecture.md): P2 Land Parcel and Cadastre, M3 Tradable Good, U1 Building and Structure, F8 Credit, Debt and Financial Instruments, plus the shared property machinery (ownership, transfer, encumbrance, security interests, insolvency) and the rent and commons overlay. Register rows: P2, M3, U1, F8 in [`world-models.csv`](../world-models.csv). Sits on the S cluster ([Security, Ownership and Access](./Security-Ownership-and-Access.md)), R1/R2 ([Registry and Ledger](./Registry-and-Ledger.md)), K2/X1 ([Actions and Events](./Actions-and-Events.md)), and A18 ([Offense and Enforcement](./Offense-and-Enforcement.md)); it encodes the MOS property doctrine from [Property-Rent-and-Commons](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Property-Rent-and-Commons.md) and [Distributive-Justice-and-Capability-Floors](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Distributive-Justice-and-Capability-Floors.md). On conflict with the architecture summary, this document governs for these models.
> **Provenance:** six parallel specifiers (four model cores plus the shared machinery and the rent overlay), then five adversarial reviews (a property-fraud attacker, a rentier and concentration attacker, the doctrine keeper, a commons-and-access reviewer, a systems pragmatist: 53 findings, 16 critical), then one revision pass under a 33-point resolution charter. Both flanks were treated as load-bearing: a property regime that only stopped fraud, or only stopped rent extraction, would fail the polity.

---

## 0. How the property layer works

These are the things people own and trade, and the whole design exists to let them be owned, transferred, encumbered and financed cleanly on the layers below, while encoding one MOS-specific commitment that ordinary property law lacks: property may never become a pure rent-extraction machine. Each model rests on the same machinery: one controlling meta-object per object (S1); registers are R1 instances (single-subject sequencing so one exclusive claim fails closed, public-faith minimum, indefeasibility by defect type); value and money are R2 (the sovereign Ae ledger is booked-not-transferred, the thin $ rail carries instruments); transfers are K2 acts; fraud is an A18 offense with beneficial-owner criminal liability.

**The four nouns.** A parcel (P2) is a spatial object; the title over it is a usufruct, never freehold, carrying a standing location-rent obligation assessed independently of any improvement so community-created land value returns to the commons. A good (M3) is a physical item in its market aspect; the same instance is both item and good by reference, fungible balances are physically backed and segregated when pledged, and provenance travels as occurrences. A building (U1) is a registrable improvement on a parcel, its structure earned and private while the location rent under it follows the land, not the building. An instrument (F8) is an F2-backed, transferable claim on the $ rail, never Ae, whose yield is decomposed so that money-rent (pure return on holding) is priced as leakage while return on creation is protected.

**The shared machinery and the doctrine (PROP, RENT).** Ownership is S1 resolvability with co-ownership modeled as fractional shares under a single controller of record. Transfer is one canonical flow (K2 act, R1 registration, R2 settlement). Encumbrances are first-class registered claims with a first-to-file priority ladder in which junior liens are lawful and only a concealed senior interest or a second title is fraud. Insolvency runs a waterfall with capability floors and restoration protected first, security interests perfected before the harm kept reliable. Over all four, the rent overlay prices unearned rent (captured minus created) as leakage routed to the commons and the citizen dividend; the commons (land, subsurface, spectrum, and the new land of compute and data) are stewarded, not enclosed; a concentration ceiling and charge apply to accumulated holdings, resolved even across acting-in-concert structures; and capability floors in housing, land and essential goods are delivered, not merely shielded.

Three commitments recur, matching the rest of the model:

1. **Ownership integrity is structural.** A second title or a second claim on an occupied priority slot fails closed at append; fungible pledges segregate; the housing floor is discoverable through a mandatory registered marker so public faith survives.
2. **Anti-fraud reaches the real actor.** Encumbrance authority is verified before perfection, beneficial ownership is disclosed prospectively and traced criminally to the natural person (A18-I45), and the concentration test sees through fragmentation and concert.
3. **Both flanks priced.** Junior lending, home mortgages and secured credit stay reliable, while unearned land, monopoly and money rent are charged, the commons are opened rather than captured, the citizen dividend has a constitutional floor, and no capability floor depends on a holder's registration diligence.

The sections follow: P2 land and cadastre; M3 tradable good; U1 building and structure; F8 credit, debt and instruments; PROP shared machinery; RENT the rent and commons overlay.

---
## P2 land parcel and cadastre

### Purpose
The cadastre is the constitutive register of land parcels and of the usufruct titles held over them. It fixes parcel geometry under single-sequencing, resolves the one controller of record for each parcel and for each co-held share, carries the standing location-rent obligation that returns community-created land value to the commons, and surfaces the capability-floor, encumbrance, possession, and contest markers on which acquirers, lenders, and occupiers rely. Land is stewarded commons: it is held under usufruct, never owned as freehold, and its location value is never privately captured in perpetuity.

### Object model
- parcel: {parcel_id; geometry (single-sequenced footprint, R1-I9); subject_class = land (P2-I2); controller_ref (S1)}.
- title (usufruct): a bounded, rent-bearing, steward-reviewable holding over a parcel; bequeathable and transferable, but never freehold (P2-I1). Carries use_condition and renewable_term fields.
- co_holding: fractional shares of one title, each share a distinct property object with its own single controller (PROP-I2), all shares sitting under one controller of record (PROP-I1 co_ownership_body, or for strata the U2 owners-association controller) that is the sole S1 controller of the parcel object (P2-I1).
- rent_obligation: {location_basis; assessment_ref (public C7 site-value event); cadence; true_up_ledger; arrears_ledger; debtor_ref}.
- floor_protection: an occupancy-floor encumbrance marker auto-registered from the fact of lawful occupation (P2-I10).
- homestead_protection: {floor_quantum (per-cohort capability-floor value of shelter, Art. 6); primary_dwelling_ref; deferred_charge_ledger}.
- extraction_grant_ref: {deposit_ref (P2-P5); grant_terms; rent_basis; expiry (mandatory finite term); revocable (revocation_trigger); restoration_duty (K10); restoration_bond_ref}.
- boundary_contest_marker; possession_marker (dated register entry of a possession start).

### Invariants
- P2-I1 (usufruct, never freehold, with teeth): land SHALL be held under usufruct, never freehold. A usufruct SHALL carry a use or stewardship condition or a bounded renewable term with steward review, so idle-holding or breach of stewardship MAY trigger non-renewal or reversion to the commons; a perpetual, condition-free holding is void by construction. Co-held land SHALL resolve to a single controller of record (a PROP-I1 co_ownership_body, or for strata the U2 owners-association controller) that is the sole S1 controller of the object; the fractional shares are themselves distinct property objects each with a single controller (PROP-I2). "Fractional shares of one title" SHALL NOT be read as direct multi-holder control.
- P2-I2 (exclusive register scope, cross-register sequencing): the cadastre SHALL hold the land subject_class exclusively; U1 building and structure titles live in their own register. A parcel-boundary claim and a building-footprint claim over the same physical space SHALL be ordered in one cross-register single-sequence, and the later exclusive claim over that space fails closed across registers.
- P2-I3 (funded public faith): a title public-faith projection SHALL NOT defeat a subsisting right unless a funded assurance route stands behind the projection.
- P2-I4 (title exclusivity, lawful junior liens): a second TITLE claim over a parcel, and a second security interest asserting an already-occupied priority slot (the sole or first slot where one is perfected), SHALL fail closed at append. Additional security interests SHALL attach at successive received_at ranks per the PROP priority ladder; a ranked junior lien is lawful. The double-pledging offense is registering an interest that conceals or misrepresents an existing senior interest (each represented as sole or first), not granting a ranked junior lien.
- P2-I5 (standing location rent, never lapses): every parcel SHALL carry a standing location-rent obligation computed from the public site-value assessment (P2-I6). Location rent never lapses through possession, and perpetual private capture of location rent is void by construction. Where possession and title diverge, the obligation attaches to the party in beneficial possession or enjoyment from the point a possession or contest marker is registered, not the dispossessed titleholder, with reconciliation at A6 ripening and S1-I14 restitution; the obligation runs with enjoyment of the location. The obligation SHALL always resolve to a computable, appealable figure: where C7 cannot benchmark a unique or illiquid parcel, a fallback (comparable-adjusted or area or zone proxy, or a self-assessed value carrying a public buy-out option) applies, each with an R1 or A6 contest route; it SHALL NOT default silently to zero or to an unbounded estimate.
- P2-I6 (land assessed independently of improvement): the land or location component SHALL be assessed independently of the holder's improvement declaration, using site-value appraisal (the parcel valued as if vacant, from comparable land transactions) as the primary basis with improvement value as the residual, never the reverse. The assessment is a public C7 event and SHALL NOT be reduced by holder-supplied improvement figures; embedding an improvement in the holder's own namespace does not blur the split. Deliberate misallocation of value between land and improvement to depress the land basis is S7 audit_evasion and an A18 offense, with the burden on the holder to justify the split against the public benchmark.
- P2-I7 (extraction grant discipline): a subsurface or extraction grant is a time-bounded, revocable, rent-bearing commons grant. A grant lacking a finite expiry, a revocation trigger, or a rent_basis fails closed at registration. It SHALL carry a funded restoration bond or escrowed security on the $ rail sized to the K10 restoration estimate, revalued over the term, drawable by the steward on breach independent of the grantee's solvency; drawdown of extraction proceeds beyond the point where restoration remains under-funded is barred.
- P2-I8 (boundary contest): during a live boundary contest, disposition of the disputed overlap SHALL carry the contest_marker forward as a binding non-reliance flag, so a transferee cannot take the disputed area free of the contest.
- P2-I9 (adverse possession): ripening SHALL be tested against contemporaneously-registered evidence of the possession's start (a dated register marker), so the norm-set cannot be chosen by an unverifiable asserted start. Possession SHALL NOT ripen against a floor_protection encumbrance or against Polity-stewarded commons land; ripening is available only over ordinary private usufruct titles. Any floor_protection or stewardship duty survives the correction unchanged.
- P2-I10 (housing capability floor): the housing capability floor binds by operation of law from the fact of actual lawful occupation. It is substantively non-defeasible and lexically prior per the rent overlay; it does not depend on the holder's registration diligence. The registrar SHALL auto-register an occupancy-floor marker on the R5 occupancy attestation so it is surfaced in the R1 public-faith minimum and every gated acquirer and F8 lender takes with notice. An occupancy floor whose lawful basis pre-dates a registered security interest binds the enforcing secured party; an occupancy grant created after a registered security interest is subordinate to it for enforcement. The shelter CAPABILITY floor is never collateral (a security interest naming it is void); the dwelling OBJECT above the floor is pledgeable, a mortgage on a floor-protected dwelling is valid, and enforcement is floor-limited: title may transfer, but the occupancy and A9 dignity floors (enforced via A18) persist and cap recovery. (Art. 6.)
- P2-I11 (concentration and beneficial owner): aggregate land holdings resolved to the declared beneficial owner SHALL be checked against the anti-concentration ceiling at append; a holding over the ceiling self-charges as anti-value (Charter Art. 10). A beneficial-owner attestation is a validated field of every gated acquisition; a false or omitted declaration is an A18 concealment offense with perpetual clawback and beneficial-owner tracing (A18-I45).
- P2-I12 (homestead abatement, capped and deferred): homestead abatement of location rent SHALL be capped to the per-cohort capability-floor value of shelter (a floor quantum) on a single registered primary dwelling per person. Location rent on value above the floor quantum, and on any additional dwelling, stays commons-owed. Abatement is disallowed where the holder's aggregate land trips the Art. 10 ceiling. Abatement DEFERS rather than extinguishes: it accrues as a non-punitive charge on the title that crystallizes when the dwelling leaves floor scope or is transferred, so the obligation never lapses (P2-I5) yet never pushes an occupant below the floor.

### Protocols
- P2-P1 (subdivision and merger): (1) validate the superseding geometry under single-sequencing. (2) resolve controllers and shares of the superseded parcel. (3) recompute rent_obligation on the new geometry. (4) enumerate and atomically re-map ALL cross-register dependents of a superseded parcel_id (U1 building or structure parcel_refs, U2 unit refs, every F8 or PROP security_interest collateral_ref) as one multi_leg_commit; the superseding geometry entry carries these references forward. If any dependent cannot be re-mapped, the whole supersession fails closed.
- P2-P2 (transfer): (1) resolve the current S1 controller and any floor_protection, contest, and arrears markers. (2) require a validated beneficial-owner attestation and check the concentration ceiling (P2-I11) against the declared beneficial owner at append. (3) obtain second-channel disposing-authority confirmation from the registered holder. (4) commit; the transferee takes subject to surfaced floors, contest flags, and deferred homestead charges; any inter-assessment appreciation crystallizes as an assessment-uplift charge on disposition (P2-P4).
- P2-P3 (encumbrance registration): (1) resolve collateral_ref and its priority ladder. (2) before any encumbrance or security interest perfects, synchronously verify the grantor is the current S1 controller of collateral_ref PLUS second-channel consent from the registered holder (identical to the P2-P2 disposing-authority check); a filing failing this fails closed rather than perfecting. (3) perfect at the next received_at rank on the ladder (junior liens lawful, P2-I4); a filing asserting an occupied sole or first slot, or concealing a senior interest, fails closed.
- P2-P4 (rent assessment and debit): (1) run the public C7 site-value assessment (P2-I6) at a mandated maximum interval and on event triggers (nearby transactions, rezoning, or infrastructure that shifts location value). (2) capture inter-assessment appreciation via a true-up or an assessment-uplift charge on disposition. (3) debit the party in beneficial possession or enjoyment (P2-I5), routing recovered location rent to the commons_rent_fund; accrued arrears retain commons priority and ride with the asset.
- P2-P5 (extraction grant registration): (1) validate expiry, revocation_trigger, and rent_basis; a grant lacking any fails closed (P2-I7). (2) escrow the funded restoration bond on the $ rail sized to K10, revalued over the term. (3) meter proceeds drawdown against restoration funding; bar drawdown beyond under-funded restoration.

### Lifecycle and edge cases
- Bequest: the usufruct is bequeathable but carries its use condition, renewable term, rent_obligation, and any deferred homestead charge forward; it never converts to freehold.
- Boundary dispute: geometry is rebuttable; disposition of the disputed overlap carries the contest_marker as a binding non-reliance flag (P2-I8) so a reliance acquirer cannot take the strip free.
- Adverse possession: ripens only over ordinary private usufruct titles, from a contemporaneously-registered start marker, and never against a floor or Polity-stewarded commons (P2-I9); during divergence the rent debtor is the beneficial possessor (P2-I5).
- Idle-holding or stewardship breach: triggers steward review and MAY end in non-renewal or reversion to the commons (P2-I1).
- Homestead crystallization: deferred location-rent charge crystallizes when the dwelling leaves floor scope or transfers (P2-I12).

### Interfaces
- R1: constitutive register; public-faith minimum SHALL surface the occupancy-floor marker, contest flags, and encumbrance ladder.
- S1: controller of record for parcel and shares; S1-I14 restitution on possession or boundary correction.
- A6: adjudication of ripening, contest freezes, and rent contests; judicial_access_contract carve-out for beneficial-owner tracing.
- A18: offense and clawback channel (A18-I45 for beneficial-owner concealment and tracing); A9 dignity floor enforced via A18.
- C7: public site-value assessment events; K10: restoration estimate.
- F8 and PROP: security_interest collateral_refs, priority ladder, floor-limited enforcement.
- U1 and U2: building, structure, and unit refs re-mapped under P2-P1; occupancy floor stated identically in U1-I8.
- RENT: commons_rent_fund destination, housing-floor reinvestment, homestead abatement rules.

### External bindings
This section implements the MOS rent delta: land carries a standing, community-owed location rent independent of the holder's improvement declaration, capability floors are lexically prior and non-defeasible, and usufruct with steward review replaces freehold. It adopts the enforcement-capped-at-secured-obligation discipline so that a floor-protected dwelling can still be pledged while the shelter capability and A9 dignity floors persist.

### Open questions
1. Calibration of the site-value estimator and of the fallback proxy for unique parcels (the figure must stay computable and appealable, P2-I5, P2-I6), pending the C7 appraisal-method mandate.
2. The Art. 6 process and cadence for setting the per-cohort floor_quantum used by homestead abatement (P2-I12).
3. Implementation choice for cross-register single-sequencing (a single land-plus-improvement register root versus an explicit cross-register ordering rule) that preserves the fail-closed guarantee across the cadastre and the U1 register (P2-I2).
4. Binding of the maximum revaluation interval and event triggers (P2-P4) to a named A-mandate parameter.

## M3 tradable good

### Purpose

M3 models tradable goods as property objects: serialized non-fungible goods that each carry their own exclusive-claim R1 title, and fungible goods held as quantities in a backed holding ledger. It fixes single-controller ownership, the gated/fast tier assignment, provenance and physical backing, the anti-fraud discipline for double-pledging and commingling, the monopoly/scarcity and data ("new land") rent overlays, and the concentration ceiling with a paired provision side for essential classes. Land parcels (P2) and buildings/units (U1/U2) are out of scope; goods affixed to them route through those sections.

### Object model

- good: {good_id; gpc_class (K-mandate class); fungibility in {serialized_non_fungible, fungible_balance}; controller_ref (single S1 controller, M3-I1); title_ref (R1, serialized only); custody_ref (M2 attestation); provenance_chain (lawful-acquisition attestations)}.
- fungible_holding: {holding_key = (GTIN, batch_or_lot, grade); free_balance; committed_holds[]; pledged_holds[]; backing_refs (witnessed M2 warehouse/custody attestations); last_checkpoint (witnessed reconciliation)}.
- security_interest: {collateral_ref; grantor_ref; holder_ref; received_at (rank); segregating_hold (fungible only); senior_disclosure (declared existing interests)}.
- gated_acquisition: {acquirer_ref; beneficial_owner_attestation (validated field, M3-I13); consideration}.
- rent_overlay: {basis in {monopoly_scarcity, data_new_land}; benchmark_ref (C7 counterfactual); commons_share; created_vs_aggregate_split (rebuttable, M3-I14)}.

### Invariants

- M3-I1 Every tradable good is a property object with exactly one S1 controller of record. Co-held goods sit under a single controller of record (a PROP-I1 co_ownership_body) that is the sole S1 controller of the object; the fractional shares are themselves distinct property objects, each with a single controller (PROP-I2). "Fractional shares of one title" SHALL NOT be read as multi-holder direct control.
- M3-I2 A good is classified either serialized_non_fungible (an exclusive-claim subject with its own R1 title) or fungible_balance (a quantity in a (GTIN, batch/lot, grade) holding). Evasive misclassification to escape a rent overlay, a concentration charge, or a tier is an S7 audit_evasion and A18 offense; the burden to justify the classification against the public benchmark rests on the holder.
- M3-I3 Tier precedence: an exclusive-claim or encumbered good takes the gated tier (synchronous, validated) even when it is otherwise an ordinary good, so every serialized non-fungible good and every encumbered fungible holding is gated. Only unencumbered, non-exclusive fungible-balance goods use the fast tier. This resolves the PROP tier assignment for goods.
- M3-I4 Provenance: every good carries a resolvable lawful-acquisition custody chain. For a serialized good a provenance defect voids reliance and shifts the burden of lawful acquisition to the holder. For a fungible good each inbound quantity requires a resolvable lawful-acquisition M2 custody attestation; an unattested quantity is provenance-defective and SHALL NOT commingle into a clean holding, closing the fungible-laundering path.
- M3-I5 Fungible backing: every fungible holding credit SHALL be backed by a witnessed custody or warehouse M2 attestation and reconciled to attested physical stock at periodic witnessed checkpoints. An unbacked or over-attested credit fails closed at append. A "sufficient balance" alone never authorizes a fold; the balance must trace to attested physical stock.
- M3-I6 Title uniqueness: for a serialized good a second title claim, or a second interest asserting an already-occupied priority slot (the sole or first slot where one is perfected), fails closed at append under single-sequencing across the good's register.
- M3-I7 Encumbrance authority: before any security interest over a good perfects, synchronously verify the grantor is the current S1 controller of collateral_ref PLUS second-channel consent from the registered holder (identical to the M3-P2/P2 disposing-authority check). A filing failing this fails closed rather than perfecting.
- M3-I8 Junior liens are lawful: additional security interests attach at successive received_at ranks per the PROP priority ladder. Fail-closed is limited to (a) a second title claim and (b) a second interest asserting an already-occupied priority slot. The double-pledging OFFENSE is registering an interest that conceals or misrepresents an existing senior interest (each represented as sole or first), not merely granting a ranked junior lien (A18-I45 clawback).
- M3-I9 Fungible segregation on pledge: on perfecting a security interest over a fungible holding, place a segregating hold debiting the pledged quantity from the free balance. Any further pledge or transfer whose pledged-plus-committed sum exceeds the holding fails closed, so the same quantity cannot be pledged to multiple lenders while the balance stays nominally sufficient.
- M3-I10 Monopoly and scarcity rent: a concentrated GPC class carries a rent overlay charging captured minus created value. The C7 competitive benchmark SHALL be constructed counterfactually (cost-plus-normal-return floor: marginal cost plus a benchmark risk-adjusted return, or comparable competitive markets), never from observed in-market prices. When a holder's aggregated share exceeds a market-power threshold, the observed price is excluded from its own benchmark; a thin or single-seller market shifts the benchmark to the cost-based reference by construction. Only the resulting commons charge routes via remediation_routing.
- M3-I11 Essential-class floor: an essential good class SHALL carry per-cohort access floors AND a concentration ceiling with a self-charge on accumulation (Charter Art. 10; Art. 6 where the access floor is cited). The floor has a provision side: recovered concentration charges and commons rent on essential classes SHALL fund per-cohort access delivery (procurement or subsidy) through the commons_rent_fund (RENT-P4), so a below-floor cohort receives the good. The ceiling and the delivery obligation are two halves of one floor.
- M3-I12 Acting-in-concert aggregation: the concentration ceiling aggregates not only S1 common control but acting-in-concert or coordinated economic interest. Related parties (kinship, prior coordination, shared financing, option or loan-back arrangements) and holdings assembled to stay sub-threshold are presumptively summed, with the burden on the holders to prove genuine independence. Deliberate fragmentation to stay below the band is an aggravating A18 basis.
- M3-I13 Prospective beneficial-owner disclosure: a beneficial-owner attestation is a validated field of every gated acquisition; the concentration ceiling is checked against the declared beneficial owner at append. A false or omitted declaration is an A18 concealment offense with perpetual clawback (A18-I45). Capacity-mismatch tracing cites A18-I11.
- M3-I14 Data and new-land goods: data value realized through a service, an API, or internal model-training (not only a "sold as a good" event) is flagged to the rent overlay. Aggregate data, foundation-model, and large-compute commons SHALL be held under stewardship (steward duties, no exclusion of legitimate access), never freehold, with a mandatory extraction_grant for private benefit and a duty to disclose or license aggregates. The created-vs-aggregate split is a rebuttable presumption AGAINST the holder: a rebuttable default commons share (a governance-set floor above zero) is charged unless the holder proves a smaller share by audited cohort-grain V3 accounting. An existing privately-held aggregate crossing the scale threshold is brought under stewardship by the conversion route (registration of steward duties plus an extraction_grant).
- M3-I15 Cornering an essential class to breach an access floor, and concealing an existing senior interest under M3-I8, are A18 offenses; recovery and enforcement against any good SHALL respect the A9 dignity floor (enforced via A18) and the housing capability floor where the good is a dwelling input.

### Protocols

- M3-P1 Register a good. Resolve gpc_class and fungibility; for a serialized good open an exclusive-claim R1 title under single-sequencing (M3-I6); for a fungible credit require a backing M2 attestation and a lawful-acquisition provenance attestation (M3-I4, M3-I5), else fail closed. Set the single controller_ref (M3-I1). Flag the rent overlay where the class is concentrated or the good is a data/new-land good (M3-I10, M3-I14).
- M3-P2 Transfer. Verify the grantor is the current S1 controller plus second-channel consent from the registered holder. For a gated acquisition require and validate the beneficial-owner attestation (M3-I13) and check the concentration ceiling against the declared beneficial owner, aggregating acting-in-concert holdings (M3-I12). Carry the provenance chain forward. Fast tier is available only for an unencumbered non-exclusive fungible transfer (M3-I3).
- M3-P3 Pledge or perfect a security interest. Run the M3-I7 encumbrance-authority check; assign a received_at rank on the PROP ladder (junior liens lawful, M3-I8). For a fungible holding place a segregating hold (M3-I9). Concealment of a senior interest is registered as an A18 offense, not silently accepted.
- M3-P4 Rent-overlay assessment. Compute the C7 counterfactual benchmark (M3-I10); charge captured minus created value. For a data/new-land good charge the default commons share unless audited cohort-grain V3 proof rebuts it downward (M3-I14). Route the resulting commons charge via remediation_routing; the good itself never touches the AE ledger.
- M3-P5 Witnessed checkpoint. Reconcile each fungible holding balance to attested physical stock. An over-attested or unbacked balance fails closed and opens an S7 audit_evasion inquiry; segregating and committed holds are re-verified against backing.

### Lifecycle and edge cases

- Co-owned good: control resolves to a single co_ownership_body of record (PROP-I1); the individual shares are separate property objects (PROP-I2) and may be pledged as share-level interests, which bind only that share and its proceeds and rank in the one received_at ladder with any whole-object interest.
- Fungible commingling: only attested inbound quantities pool within a holding_key; provenance-defective quantities are held apart and cannot be laundered into the free balance.
- Serialized good under encumbrance: always gated; its title never self-executes on the fast tier.
- Data aggregate crossing the scale threshold: the conversion route registers steward duties and a rent-bearing extraction_grant; prior freehold framing is superseded.
- Consumption or destruction: the object retires, releasing committed and segregating holds; outstanding rent and concentration charges survive against the controller as running obligations.

### Interfaces

- S1: single controller model, disposing-authority and encumbrance-authority checks.
- R1: exclusive-claim titles, single-sequencing, public-faith projection for gated goods.
- R2: settlement and finality for transfers and charge routing; overlay commons charge via remediation_routing.
- C7: counterfactual competitive benchmark and independent valuation.
- M2: witnessed custody/warehouse attestations backing fungible holdings.
- A18: offense channel for concealment, cornering, misclassification, and beneficial-owner concealment (A18-I45 clawback; A18-I11 capacity-mismatch tracing); A9 dignity floor enforced via A18.
- PROP: priority ladder, co_ownership_body, share/whole-object priority.
- RENT-P4: commons_rent_fund funding per-cohort access delivery.
- F8: goods pledged as collateral; earned/unearned money-rent decomposition is an overlay in the AE ledger, not a property of any instrument.

### External bindings

This section adopts the MOS delta: monopoly and data rent are priced against counterfactual, cost-anchored benchmarks rather than observed prices; aggregate data and large-compute are stewarded, not owned freehold; and every essential-class ceiling is matched by a funded provision obligation. These depart from conventional commercial law, which prices at market and treats data aggregates as ordinary private property.

### Open questions

1. The precise cohort-grain estimator for the aggregate-data commons share (sealed-evaluator marginal contribution over registered frames, S5) is still being specified; the fallback flat data-dividend from a defined share of data-good and compute rent is committed so charging does not wait on the estimator.
2. Calibration of the market-power share threshold above which a holder's observed price is excluded from its own benchmark (a K-mandate parameter) is not yet fixed.
3. The scale threshold and cadence at which an existing privately-held aggregate is compelled into stewardship, and the timing of the witnessed reconciliation checkpoint interval, remain governance-set parameters pending an A-mandate value.

## U1 building and structure

### Purpose

U1 governs buildings and fixed structures as property objects distinct from the P2 cadastral parcel they occupy. A structure is a created improvement: its value is earned and private, whereas the location value of the land beneath it is commons-owed under the rent overlay. This section fixes how a structure is identified and controlled, how it binds to one or more parcels, how it is pledged and enforced against, and how the housing capability floor of an actual occupier is protected without turning that floor into an undiscoverable cloud on the public-faith projection. U1 states the housing/occupancy floor in the SAME terms as P2 so the two sections cannot diverge.

### Object model

- `structure` object: `{ id; register = improvement_register; controller (S1); parcel_ref[] (P2 cadastre); footprint_geometry; use_class; shares_record | strata_scheme (U2); encumbrance[] (F8/PROP security_interest); occupancy_marker[]; rent_link }`. The improvement register is distinct from the P2 cadastre, whose parcel `subject_class` scope is exclusive (P2-I2).
- `parcel_ref[]`: one structure MAY span several parcels; controllers of land and structure MAY differ (P2-I6). `rent_link` carries the location-rent obligation back to the land component, never to the structure value.
- `dwelling`: a `structure` (or a U2 unit within it) held out for residence. A dwelling in actual lawful occupation as an occupier's capability-floor residence carries an `occupancy_marker`.
- `occupancy_marker`: `{ dwelling_ref; occupier; lawful_basis; basis_start; attestation_ref (R5) }`, auto-generated by the registrar on the R5 occupancy attestation; surfaced in the R1 public-faith minimum. It records notice, not the substance, of the floor.
- `co_control`: co-held shares resolve to a single controller of record per U1-I1; the shares are themselves distinct property objects (PROP-I2).

### Invariants

- **U1-I1 (single controller of a co-held structure).** A `structure` is one property object with exactly one S1 controller. Co-holding SHALL be modelled as fractional shares under a `shares_record` or `strata_scheme`, never as two direct controllers of the object. The co-held shares SHALL sit under a single controller of record: a PROP-I1 `co_ownership_body`, or for a strata scheme the U2 owners'-association controller, which is the sole S1 controller of the structure. The fractional shares are themselves distinct property objects, each with its own single controller (PROP-I2). "Fractional shares of one structure" SHALL NOT be read as multi-holder direct control.
- **U1-I2 (structure earned, land commons; split not gameable).** The structure component is created value: earned, private, and free of location rent. Location rent attaches to the land component through `rent_link` (P2, RENT overlay). The land/improvement split SHALL be assessed independently of the holder's improvement declaration, using site-value appraisal as the primary basis with improvement value as the residual (never the reverse), as a public C7 event. A holder-declared or namespace-embedded improvement value SHALL NOT reduce the independently assessed land basis; deliberate over-declaration to depress the land basis is S7 `audit_evasion` and an A18 offense, with the burden on the holder to justify the split against the public benchmark.
- **U1-I3 (footprint exclusivity across registers).** A building-footprint claim over physical space is an exclusive claim. A parcel-boundary claim and a building-footprint claim over the same space SHALL be ordered in ONE received_at sequence spanning the P2 cadastre and the improvement register; the later exclusive claim over that space fails closed even across the register boundary.
- **U1-I4 (encumbrance authority; junior liens lawful).** Before any security interest over a `structure` perfects, the register SHALL synchronously verify that the grantor is the current S1 controller of `collateral_ref` AND obtain second-channel consent from the registered holder (identical to the P2 transfer disposing-authority check); a filing failing either check fails closed rather than perfecting. Additional security interests are lawful and attach at successive received_at ranks on the PROP priority ladder. Fail-closed is limited to (a) a second TITLE claim and (b) a second interest asserting an already-occupied priority slot (the sole or first slot). The double-pledging OFFENSE is registering an interest that conceals or misrepresents an existing senior interest, not granting a ranked junior lien.
- **U1-I5 (capability floor never collateral; object above it pledgeable).** The shelter/housing CAPABILITY floor is never collateral; a security interest naming it is void ab initio. The dwelling OBJECT above the floor is pledgeable: a mortgage on a floor-protected dwelling is VALID. Enforcement is floor-limited: title MAY transfer, but the occupancy floor (U1-I8) and the A9 dignity floor (enforced via A18) persist and cap recovery. F8-I11's "void ab initio" targets an interest naming the capability itself, not a lien on the U1/U2 object.
- **U1-I6 (enforcement discipline).** Enforcement against a pledged structure requires an objective, independently-recorded default occurrence past `cure_window`, with "unmet" defined relative to R2 settlement FINALITY, not initiation (a leg escrowed or pending finality before `cure_window` close does not trigger default). Disposition to a party under S1 common control with the secured party is barred. The sale SHALL carry a C7 independent-valuation reserve. Recovery is capped at the secured obligation with surplus returned to the debtor, subject to the floor cap of U1-I5. A18 restoration primacy ranks ahead of the debtor's unencumbered estate and unsecured claims but is subordinate to security interests perfected BEFORE the harm event, except where the specific collateral is traceable proceeds of the harm (PROP waterfall).
- **U1-I7 (concentration ceiling).** Aggregate structure holdings self-charge as anti-value past the concentration ceiling under Charter Art. 10 (anti-concentration self-charge) and Art. 6 where capability floors are also engaged. Aggregation extends beyond common control to acting-in-concert or coordinated economic interest: related parties (kinship, prior coordination, shared financing, option or loan-back arrangements) and holdings assembled to stay sub-threshold are presumptively summed, with the burden on the holders to prove genuine independence; deliberate fragmentation to stay below the band is an aggravating A18 basis. Aggregation runs through the S5 sealed evaluator, which emits only over-ceiling booleans and charge totals, never the underlying holdings.
- **U1-I8 (housing/occupancy floor: one rule with P2).** The housing capability floor binds by operation of law from the fact of actual lawful occupation of a dwelling as the occupier's capability-floor residence. It is substantively non-defeasible and lexically prior per the rent overlay. It attaches to the person's dwelling, not to holding title, and binds every successor controller, surviving transfer and F8 mortgage enforcement (subject to the timing rule below). The registrar SHALL auto-register an `occupancy_marker` on the R5 occupancy attestation, surfaced in the R1 public-faith minimum, so every gated acquirer and F8 lender takes WITH NOTICE. Registration is the mandatory notice mechanism, NOT a precondition of the floor's survival: there is no "MAY" and no "where registered" gate on the substantive floor. Timing: an occupancy floor whose lawful basis PRE-DATES a registered security interest binds the enforcing secured party; an occupancy grant created AFTER a registered security interest is subordinate to it for enforcement (genuine prior residents are protected; post-mortgage collusive leases cannot strip the mortgagee). The capability floor is never collateral and the pledgeable object above it is treated per U1-I5.
- **U1-I9 (co-owner floor override).** Where a co-owner is in actual lawful occupation of the structure as their capability-floor dwelling, the `co_ownership_body` `decision_rule` (including unanimity) SHALL NOT be usable to exclude or evict that co-owner. An expedited interim-relief partition or use order SHALL be available ahead of full adjudication, mirroring the lexical priority of the floor over ordinary control rules.

### Protocols

- **U1-P1 (register a structure).** Resolve `parcel_ref[]` against the P2 cadastre; sequence the `footprint_geometry` in the shared land+improvement sequence (U1-I3), failing closed on a later overlapping exclusive claim; set the single S1 controller (U1-I1, routing co-holding through a `co_ownership_body` or U2 owners'-association controller); link `rent_link` to the land component.
- **U1-P2 (transfer a structure).** Confirm disposing authority by second-channel consent from the registered holder; project the gated tier for an encumbered or exclusive-claim structure (fast tier is reserved for unencumbered non-exclusive goods, not for titled structures); carry every `occupancy_marker`, floor_protection, and rent obligation forward to the acquirer, who takes subject to and with notice of them.
- **U1-P3 (perfect a security interest / mortgage).** Run the U1-I4 authority check (current S1 controller plus second-channel holder consent) synchronously; verify the interest names the dwelling OBJECT, not the shelter capability (U1-I5); assign the next received_at rank on the PROP ladder; a junior lien perfects, a concealed-senior or occupied-slot filing fails closed.
- **U1-P4 (enforce).** Require the independently-recorded default past `cure_window` measured to R2 finality (U1-I6); bar disposition to a commonly-controlled party; run the sale under a C7 independent-valuation reserve; apply the floor cap so occupancy and A9 dignity floors survive the sale and limit recovery.
- **U1-P5 (cross-register re-map on parcel supersession).** On P2 subdivision or merger of a `parcel_id`, the parcel protocol SHALL enumerate and atomically re-map ALL cross-register dependents, including this structure's `parcel_ref[]`, U2 unit refs, and every F8/PROP `security_interest.collateral_ref`, as one `multi_leg_commit`. The superseding geometry entry carries these references forward; if any dependent cannot be re-mapped the whole supersession fails closed, so no charge is left pointing at a vanished parcel.

### Lifecycle and edge cases

- **Eviction.** No enforcement, foreclosure sale, or co-owner decision may push an occupier below the A9 dignity floor (enforced via A18) or breach the U1-I8 occupancy floor. Title may pass while the occupier remains, with recovery capped accordingly.
- **Post-mortgage collusive lease.** A lease or occupancy grant created after a registered security interest ranks behind it (U1-I8 timing) and does not defeat the mortgagee on enforcement; a genuine occupancy whose lawful basis pre-dates the interest does bind it.
- **Structure spanning several parcels.** Footprint claims sequence across registers (U1-I3); on subdivision or merger all `parcel_ref[]` re-map atomically (U1-P5).
- **Land and structure controllers differ.** Permitted (P2-I6); location rent stays on the land controller through `rent_link` while the structure value stays private to the structure controller; the split is assessed independently (U1-I2).
- **Discoverability.** The `occupancy_marker` resolves the former invisible-cloud problem: the floor binds regardless of registration, but its existence is always surfaced in the R1 minimum so lenders and gated acquirers can price and rely on a complete projection.

### Interfaces

- **P2 (cadastre):** `parcel_ref`, the land/improvement split, and the shared single-sequencing root; extraction and location-rent obligations flow from the parcel.
- **U2 (strata / units):** owners'-association controller for a strata scheme; unit refs re-mapped under U1-P5.
- **M3 (goods):** boundary at which a fixture affixes to or severs from the structure (see Open questions).
- **F8 (instruments):** mortgage perfection and enforcement; the dwelling object is collateral, the shelter capability is not (U1-I5); default measured to R2 finality (U1-I6).
- **PROP (shared machinery):** priority ladder, `co_ownership_body` (PROP-I1), fractional-share objects (PROP-I2), waterfall and restoration ranking.
- **R1/R5:** public-faith minimum and occupancy attestation carrying the auto-registered marker.
- **S1/S5/A6/A9/A18:** controller identity, sealed concentration aggregation, adjudication, the dignity floor, and the offense/clawback channel (A18-I45 for beneficial-owner clawback tracing).

### External bindings

- Charter Art. 10 (anti-concentration self-charge) for the ceiling and charge; Art. 6 for capability floors.
- Distributive-Justice section 3 for the A9 inviolable-rights (dignity) floor, enforced via A18.
- The rent overlay for lexical priority of the housing floor and for the site-value-primary land/improvement assessment.

### Open questions

1. **Fixture boundary.** The threshold at which a movable M3 good affixes and becomes part of the U1 structure (and the converse on severance) is not yet a bright-line test; edge affixations may need an A6 route.
2. **Multi-steward footprint.** Where a structure spans parcels with different stewards or rent bases, the apportionment of the location-rent debtor across the footprint needs a defined rule.
3. **Interim-relief threshold.** The evidentiary bar for the U1-I9 expedited co-owner floor order, short of full partition adjudication, is not yet calibrated.
4. **Deeply embedded improvements.** Calibrating the site-value residual estimator when an improvement is embedded in the holder's own namespace (shared with the P2 assessment estimator) remains open.

## F8 credit, debt and financial instruments

### Purpose

F8 governs credit, debt and financial instruments as transferable claims. An instrument is a claim on future settlement, priced through the money-rent overlay so that the earned service of credit is separated from unearned time-rent. Instruments settle exclusively on the $ rail and are kept off the AE ledger; the overlay measures rent over the underlying value events and routes only the resulting commons charge. F8 also governs the security interests that collateralize instruments, subject to the same anti-fraud, anti-concentration and capability-floor machinery that binds every property section.

### Object model

- instrument: {issuer_ref; obligor_ref; holder_ref (the single S1 controller of record); principal; schedule (ordered settlement legs); yield_terms; performance_status; beneficial_owner_ref (validated); collateral_ref (optional)}.
- security_interest: {grantor_ref; secured_party_ref; collateral_ref; received_at (priority rank); perfection_status; segregating_hold (fungible collateral); floor_limited (dwelling collateral)}.
- yield_decomposition: an AE-ledger OVERLAY record over V2/V3 events, splitting realized yield into earned components (deferral, risk premium, origination, service and monitoring) and unearned time-rent, with the resulting commons_charge. Not a property of the instrument.
- default_record: an auto-generated X1 raised when a leg is unmet past its cure_window, measured to R2 finality.

### Invariants

F8-I1 (AE boundary). An instrument SHALL NOT be denominated in, collateralized by, credited or debited to, or settled on the AE ledger; the $ rail is its sole settlement asset. The F8-I6 earned/unearned decomposition is an overlay measurement in the AE ledger over V2/V3 events, not an AE property of the instrument; only the resulting commons charge routes via remediation_routing (the R2 exception), and the instrument itself never touches AE.

F8-I2 (single controller). Each instrument and each security interest SHALL resolve to exactly one S1 controller of record. Co-held claims sit under a single PROP-I1 co_ownership_body controller; fractional participations are themselves distinct property objects, each with one controller (PROP-I2).

F8-I3 (encumbrance authority). Before any security interest perfects, the registrar SHALL synchronously verify the grantor is the current S1 controller of collateral_ref AND obtain second-channel consent from the registered holder, identical to the P2 transfer disposing-authority check. A filing failing either check fails closed rather than perfecting.

F8-I4 (junior liens lawful; double-pledging offense). Only two cases fail closed at append: (a) a second TITLE claim on the collateral, and (b) a second interest asserting an already-occupied priority slot (the sole or first slot where one is perfected). Additional security interests SHALL attach at successive received_at ranks per the PROP priority ladder. The double-pledging OFFENSE is registering an interest that conceals or misrepresents an existing senior interest (each represented as sole or first), an A18 concealment offense; merely granting a ranked junior lien is lawful.

F8-I5 (fungible backing and segregation). Every fungible holding credit pledged as collateral SHALL be backed by a witnessed custody or warehouse M2 attestation and reconciled to attested physical stock at periodic witnessed checkpoints; an unbacked or over-attested credit fails closed. On perfecting a security interest over a fungible holding, a segregating hold SHALL debit the pledged quantity from the free balance; any further pledge or transfer whose pledged-plus-committed sum exceeds the holding fails closed.

F8-I6 (yield decomposition and benchmark). Every instrument's realized yield SHALL be decomposable in the AE-ledger overlay into earned components versus unearned time-rent. The earned components SHALL be benchmarked against C7 competitive references (risk priced against a comparable-risk market rate constructed counterfactually, service and monitoring fees against arms-length cost), never against a concentrated holder's own observed price; any excess over benchmark is unearned and charged.

F8-I7 (substance over form). Fees, points and affiliated-service charges economically tied to the credit SHALL be pulled into the instrument's yield for F8-I6 decomposition, so interest cannot be laundered into fee income outside the overlay.

F8-I8 (default occurrence). performance_status SHALL flip to default only on an objective, independently-recorded occurrence: a scheduled leg unmet past its cure_window, where "unmet" is defined relative to R2 settlement FINALITY, not initiation. A leg escrowed or pending finality before cure_window close does not trigger default; only a leg with no pending settlement at close flips, via the auto-generated default_record X1.

F8-I9 (equity-side rent timing). An organization's unearned rent SHALL be commons-charged as MEASURED per period (flow assessment on the firm), independent of distribution, so retained rent is charged when captured. A share sale realizing accumulated-but-uncharged rent is a triggering event: the unearned component is priced before the equity holder keeps the gain. Distributions and buybacks settle on the $ rail.

F8-I10 (enforcement cap and restoration ranking). Enforcement recovery is capped at the secured obligation, with surplus returned to the debtor. A18 restoration primacy ranks ahead of the debtor's unencumbered estate, unsecured claims, avoidable or fraud-linked transfers and the residual, but is SUBORDINATE to security interests perfected BEFORE the harm event, EXCEPT where the specific collateral is traceable proceeds of the harm; the super-priority over pre-existing perfected security is otherwise capped to a bounded commons-funded pool, so pre-harm pledged collateral stays reliable.

F8-I11 (shelter capability floor versus dwelling object). The shelter and housing CAPABILITY floor SHALL NEVER be collateral; a security interest naming it is void ab initio. The dwelling OBJECT above the floor MAY be pledged: a mortgage on a floor-protected dwelling is valid, and enforcement is floor-limited, so title may transfer but the occupancy floor and the A9 dignity floor (enforced via A18) persist and cap recovery. An occupancy floor whose lawful basis PRE-DATES a registered security interest binds the enforcing secured party; an occupancy grant created AFTER a registered security interest is subordinate to it for enforcement. Every F8 lender takes with notice of the registrar's auto-registered occupancy-floor marker on the R5 attestation.

F8-I12 (concentration). Aggregate credit exposure and pledged holdings self-charge above the Charter Art. 10 ceiling (anti-concentration self-charge). Aggregation extends beyond common control to acting-in-concert and coordinated economic interest; related parties and holdings assembled to stay sub-threshold are presumed summed, with the burden on the holders to prove genuine independence. Holdings are committed into per-owner-cluster frames the S5 sealed evaluator sums under seal, emitting only over-ceiling booleans and charge totals to any state organ, never the underlying holdings.

F8-I13 (beneficial owner). A beneficial-owner attestation is a validated field of every gated instrument acquisition; the concentration ceiling is checked against the declared beneficial owner at append. A false or omitted declaration is an A18 concealment offense with perpetual clawback and tracing (A18-I45), routed through the A6 judicial_access_contract carve-out.

F8-I14 (priority and tier). A whole-object security interest perfected before any share-level interest outranks later share pledges; a share-level interest binds only that share and its proceeds; both register in one received_at-ordered ladder so a share pledge and a whole-object pledge can never each claim the same value. An encumbered or exclusive-claim instrument or collateral subject takes the gated tier; only unencumbered, non-exclusive fungible-balance holdings use the fast tier.

### Protocols

F8-P1 (issuance and settlement). 1: the issuer registers the instrument with obligor_ref, schedule, yield_terms and a validated beneficial_owner_ref. 2: the concentration ceiling is checked against the declared beneficial owner (F8-I12, F8-I13); over-ceiling or false declaration fails closed. 3: principal settles on the $ rail with deferred finality. 4: schedule legs are monitored, each cure_window running to R2 finality (F8-I8).

F8-P2 (security interest perfection). 1: the grantor files; the registrar verifies grantor is the current S1 controller of collateral_ref plus second-channel holder consent (F8-I3), else fail closed. 2: resolve collateral, if fungible verify M2 backing and place the segregating hold (F8-I5), if a dwelling mark floor_limited (F8-I11). 3: assign the received_at priority rank on the PROP ladder, rejecting a second title claim or an occupied sole/first slot (F8-I4). 4: perfect.

F8-P3 (leg and coupon settlement). Each leg settles on the $ rail. The yield decomposition is appended to the AE overlay per period (F8-I6, F8-I7); any unearned excess routes as a commons charge via remediation_routing. The instrument object never touches AE.

F8-P4 (enforcement). 1: require an objective default_record past cure_window (F8-I8) as precondition. 2: bar disposition to any party under S1 common control with the secured party and require a C7 independent-valuation reserve on the sale. 3: apply the pre-existing occupancy floor and the A9 dignity floor (enforced via A18); recovery is capped at the secured obligation and floor-limited (F8-I10, F8-I11). 4: return surplus to the debtor.

F8-P5 (tracing and clawback). A concealed senior interest, a false beneficial-owner declaration, or a capacity mismatch triggers A18 tracing (A18-I45 for beneficial-owner clawback; A18-I11 for capacity-mismatch tracing), routed through the A6 judicial_access_contract carve-out, with perpetual clawback of proceeds.

### Lifecycle and edge cases

- Residential mortgage: the dwelling object is pledgeable and the mortgage valid; on enforcement title may transfer but the occupancy and A9 dignity floors persist and cap recovery (F8-I11).
- Post-mortgage collusive lease: an occupancy grant created after a registered security interest is subordinate for enforcement and cannot strip the mortgagee; a genuine prior resident's floor binds (F8-I11).
- Fungible inventory double-financing: blocked structurally by the segregating hold; a further pledge exceeding free balance fails closed (F8-I5).
- Cross-register re-map: on parcel subdivision or merger, every F8 security_interest collateral_ref pointing at a superseded parcel_id is enumerated and atomically re-mapped as one multi_leg_commit; a dangling ref fails the whole supersession closed (C28).
- Retain-and-sell: rent retained inside a firm is charged as measured; a share sale realizing uncharged rent triggers pricing of the unearned component before the seller keeps the gain (F8-I9).
- False default trigger: a leg escrowed or pending R2 finality before cure_window close does not raise a default_record (F8-I8).

### Interfaces

- R2 settlement rail and finality; remediation_routing for the commons charge.
- PROP priority ladder and multi_leg_commit; P2 disposing-authority check.
- S5 sealed evaluator for concentration aggregation; A6 judicial_access_contract for beneficial-owner tracing.
- A18 offense channel (A18-I45 beneficial-owner clawback, A18-I11 capacity mismatch); A9 dignity floor.
- R5 occupancy attestation and the auto-registered occupancy-floor marker; M2 custody attestation; U1/U2 dwelling objects.

### External bindings

- The $ rail is the sole settlement asset; the AE ledger carries only the rent overlay measurement.
- Charter Art. 10 grounds the concentration ceiling and self-charge; Charter Art. 6 grounds the capability floors.
- Rent doctrine delta: money-rent is the unearned time-rent component of yield, benchmarked counterfactually against C7 competitive references.

### Open questions

1. Governance calibration of the cost-plus-normal-return benchmark for money-rent (the risk-adjusted return reference and the market-power threshold above which a holder's observed price is excluded from its own benchmark).
2. Per-class checkpoint cadence for fungible-collateral backing reconciliation (F8-I5) across commodity, receivable and warehouse-receipt classes.
3. Sizing of the bounded commons-funded pool that caps restoration super-priority over pre-harm perfected security (F8-I10), against the traceable-proceeds carve-out.
4. Treatment of instruments spanning rails or jurisdictions outside a single $ rail (deferred pending a cross-rail settlement model).

## Shared property machinery: ownership, transfer, encumbrance, security interests, insolvency

### Purpose

PROP holds the machinery that P2 (parcels), U1 (buildings and strata), M3 (goods), F8 (instruments) and RENT (the rent overlay) share: how an object resolves to a single controller, how co-holding is modeled, how encumbrances and security interests perfect and rank, how enforcement and insolvency distribute value, and how the capability floors and the commons rent charge bind through transfer, foreclosure and insolvency. Consuming sections cite these invariants rather than restating them, so the property flanks stay coherent.

### Object model

- co_ownership_body: the single S1 controller of record for a co-held object; carries a decision_rule fixed at formation. For strata the U2 owners'-association controller plays this role.
- fractional_share: a distinct property object over a co-held object, each with its own single controller, separately transferable and pledgeable.
- security_interest: {collateral_ref; grantor_ref; holder_ref; priority_rank; received_at; secured_obligation; kind = title-transferring | non-possessory lien | easement | floor_protection}.
- priority_ladder: the received_at-ordered ranking of all interests over one collateral, spanning whole-object and share-level interests.
- multi_leg_commit: an atomic all-or-nothing commit spanning more than one register.
- estate and waterfall: the insolvency distribution structure, with a capability-floor carve-out taken before ranking.
- avoidance_record: a preferential or undervalue transfer inside the reach-back window, subject to clawback.

### Invariants

PROP-I1: Every co-held object SHALL resolve to exactly one S1 controller of record: a co_ownership_body (or, for strata, the U2 owners'-association controller) that is the sole S1 controller of the object. Co-holding is never modeled as N direct controllers.

PROP-I2: Each fractional_share is itself a distinct property object with its own single controller (S1-I1 preserved), separately transferable and pledgeable. Share-level and whole-object interests register in ONE received_at-ordered priority_ladder: a whole-object security interest perfected before any share-level interest outranks later share pledges; a share-level interest binds only that share and its proceeds; the two can never each claim the same value. A share is a non-exclusive claim over the object but an exclusive claim over itself.

PROP-I3: An encumbrance or security_interest exists only once perfected through PROP-P2. Resolution of collateral_ref and the absence of a conflicting senior slot are necessary but never sufficient for perfection.

PROP-I4: Tier assignment. An exclusive-claim OR encumbered subject SHALL take the gated (synchronous, validated) tier even when it is otherwise an ordinary good; only unencumbered, non-exclusive (typically fungible-balance) goods use the fast tier. Serialized non-fungible goods carrying an R1 title are gated. Land, buildings, shares and all security-bearing subjects are gated. This rule is stated identically in M3.

PROP-I5: multi_leg_commit. Any operation touching more than one register SHALL commit atomically or fail closed. On supersession of a parcel_id the operation SHALL enumerate and atomically re-map ALL cross-register dependents (U1 building or structure parcel_refs, U2 unit refs, every F8 or PROP security_interest collateral_ref); the superseding geometry entry carries these references forward. If any dependent cannot be re-mapped the whole supersession fails closed, leaving no dangling collateral_ref.

PROP-I6: Encumbrance authority. Before any encumbrance or security interest perfects, the register SHALL synchronously verify the grantor is the current S1 controller of collateral_ref AND obtain second-channel consent from the registered holder, identical to the P2 transfer disposing-authority check. A filing failing either check fails closed rather than perfecting.

PROP-I7: Capability-floor and object boundary. The shelter and housing CAPABILITY floor SHALL NEVER be collateral; a security interest naming it is void ab initio. The dwelling OBJECT above the floor is pledgeable: a mortgage on a floor-protected dwelling is valid, and enforcement is floor-limited. Title MAY transfer, but the occupancy floor and the A9 dignity floor (enforced via A18) persist and cap recovery.

PROP-I8: Priority ladder and junior liens. Multiple security interests over one collateral attach at successive received_at ranks; junior liens are lawful. fail-closed is limited to (a) a second TITLE claim and (b) a second interest asserting an already-occupied priority slot (the sole or first slot where one is perfected). The double-pledging OFFENSE is registering an interest that conceals or misrepresents an existing senior interest (each represented as sole or first), not granting a ranked junior lien. This fixes F8-I3 and P2-I4.

PROP-I9: Enforcement discipline. Disposition under a security interest SHALL be barred until an objective, independently-recorded default occurrence past cure_window, with "unmet" defined against R2 settlement FINALITY not initiation: a leg escrowed or pending finality before cure_window close does not trigger default. Disposition to any party under S1 common control with the secured party is barred. A C7 independent-valuation reserve SHALL be set on the sale. Recovery is capped at the secured obligation; surplus returns to the debtor; the occupancy floor and the A9 dignity floor (enforced via A18) persist.

PROP-I10: Fungible security segregation. On perfecting a security interest over a fungible holding, a segregating hold SHALL debit the pledged quantity from the free balance; any further pledge or transfer whose pledged-plus-committed sum exceeds the holding fails closed. Physical backing and provenance of the holding itself are M3 machinery.

PROP-I11: Occupancy-floor timing. An occupancy floor whose lawful basis PRE-DATES a registered security interest binds the enforcing secured party; an occupancy grant created AFTER a registered security interest is subordinate to it for enforcement. The registrar SHALL auto-register an occupancy-floor marker on the R5 occupancy attestation so it is surfaced in the R1 public-faith minimum and every gated acquirer and F8 lender takes with notice.

PROP-I12: Insolvency carve-out and waterfall. Essential housing and goods at the per-cohort capability floor are carved out of the estate ahead of all claims and are never available for distribution. After that carve-out the estate distributes: (1) A18 restoration of harmed parties; (2) accrued location-rent arrears, which retain commons priority, rank ahead of ordinary unsecured claims immediately after the capability-floor carve-out and A18 restoration, ride with the asset into any acquirer's hands, and never fall into the pro-rata unsecured pool; (3) security interests by perfected rank; (4) ordinary unsecured claims pro rata; (5) residual to the debtor. A18 restoration primacy ranks ahead of the debtor's unencumbered estate, unsecured claims and avoidable or fraud-linked transfers, but is SUBORDINATE to security interests perfected BEFORE the harm event, EXCEPT where the specific collateral is traceable proceeds of the harm; the super-priority over pre-harm perfected security is additionally capped to a bounded commons-funded pool, so pre-harm pledged collateral stays reliable and the F8 enforcement-capped-at-secured-obligation promise holds. The A9 dignity floor (enforced via A18) binds throughout.

PROP-I13: Avoidance and clawback. Preferential or undervalue transfers inside a reach-back window before insolvency SHALL be avoidable and clawed back into the estate. Default reach-back is 24 months for transfers to related parties and 12 months otherwise; default undervalue threshold is consideration below 70% of the C7 assessed value. Both bind to the A-mandate parameter PROP.avoidance and are revaluable via A6. Beneficial-owner criminal-class liability and clawback tracing route through A18-I45; capacity-mismatch tracing uses A18-I11. Clawback is perpetual for concealment offenses.

PROP-I14: Concentration resolution. Aggregate holdings self-charge under Charter Art. 10 (anti-concentration self-charge). Aggregation extends beyond S1 common control to acting-in-concert or coordinated economic interest: related parties (kinship, prior coordination, shared financing, option or loan-back arrangements) and holdings assembled to stay sub-threshold are presumptively summed, with the burden on the holders to prove genuine independence; deliberate fragmentation to stay below the band is an aggravating A18 basis. Aggregation is computed by the S5 sealed evaluator over per-owner-cluster frames, emitting only over-ceiling booleans and charge totals to any state organ, never the underlying holdings; beneficial-owner tracing routes through the A6 judicial_access_contract carve-out.

PROP-I15: Co-owner floor override. Where a co-owner is in actual lawful occupation of the object as their capability-floor dwelling, the co_ownership_body decision_rule SHALL NOT be usable to exclude or evict that co-owner. An expedited interim-relief partition or use order is available ahead of full adjudication.

### Protocols

PROP-P1: co_ownership_body formation. On co-holding an object, (1) mint a co_ownership_body (or bind the U2 owners'-association controller) as the sole S1 controller; (2) fix decision_rule at formation, subject to the PROP-I15 floor override; (3) mint fractional_share objects as distinct property objects (PROP-I2), each with a single controller.

PROP-P2: Encumbrance and security-interest perfection. (1) Resolve collateral_ref. (2) Verify grantor is the current S1 controller AND obtain second-channel holder consent (PROP-I6); on failure, fail closed. (3) If collateral is a fungible holding, place the segregating hold (PROP-I10). (4) Assign priority_rank at received_at on the single ladder; a second title claim or an occupied-slot claim fails closed, a ranked junior lien attaches (PROP-I8). (5) Auto-surface the perfected interest, and any occupancy-floor marker, in the R1 public-faith minimum.

PROP-P3: Enforcement and foreclosure. (1) Confirm an objective, independently-recorded default past cure_window against R2 finality (PROP-I9); else abort. (2) Set the C7 independent-valuation reserve. (3) Bar any bidder under S1 common control with the secured party. (4) Dispose. (5) Apply proceeds capped at the secured obligation; the occupancy and A9 dignity floors persist and cap recovery; surplus returns to the debtor.

PROP-P4: Insolvency distribution. (1) Carve out capability-floor housing and goods (PROP-I12). (2) Run avoidance clawback (PROP-I13) into the estate. (3) Distribute per the PROP-I12 waterfall. (4) Carry rent arrears with the asset into the acquirer's hands as a running charge.

### Lifecycle and edge cases

- Phantom-lien attack: a filing against a stranger's clean title fails at the PROP-I6 authority check and never perfects.
- Post-mortgage collusive lease: an occupancy grant created after a registered security interest is subordinate on enforcement (PROP-I11); a genuine prior resident binds the secured party.
- Traceable-proceeds collateral: A18 restoration reaches specific collateral that is traceable proceeds of the harm even against a pre-harm perfected interest (PROP-I12).
- Share versus whole-object contest: both interests share one received_at ladder, so no value is claimed twice (PROP-I2).
- Cross-register supersession: a subdivision or merger commits as one multi_leg_commit and fails closed if any dependent ref would dangle (PROP-I5).
- Co-owner deadlock over a floor dwelling: the decision_rule cannot evict the occupying co-owner; expedited interim relief is available (PROP-I15).

### Interfaces

- S1: single controller-of-record model; restitution via S1-I14.
- R1: the public-faith projection surfaces every perfected encumbrance and the auto-registered occupancy-floor marker (PROP-I11), so gated acquirers and F8 lenders take with notice.
- R2: settlement finality defines "unmet" for default (PROP-I9).
- R5: occupancy attestation triggers the floor marker.
- A18: restoration primacy in the waterfall; A18-I45 beneficial-owner clawback tracing; the A9 dignity floor is enforced via A18 as the offense channel.
- A6: judicial_access_contract carve-out for beneficial-owner tracing; ratification of PROP.avoidance; interim-relief orders.
- S5: sealed per-owner-cluster concentration aggregation.
- C7: independent valuation reserve and counterfactual concentration benchmark.
- P2, U1, M3, F8, RENT: consume PROP-I1 to PROP-I15 as their shared property machinery.

### External bindings

- Charter Art. 10 grounds the anti-concentration self-charge (PROP-I14); Charter Art. 6 grounds the capability floors (PROP-I7, PROP-I11, PROP-I12, PROP-I15).
- MOS delta: credit stays reliable because A18 restoration is subordinated to security interests perfected before the harm event (except traceable proceeds) and capped by a bounded commons-funded pool, preserving the F8 enforcement-capped-at-secured-obligation promise while restoration keeps primacy over the unencumbered estate.

### Open questions

1. Calibration of PROP.avoidance: the defaulted 24 or 12 month reach-back and the 70% undervalue threshold are operative but await A6 ratification of the named parameter.
2. Whether the standing rule for restoration over pre-harm perfected security should be the traceable-proceeds carve-out alone or the bounded commons-funded-pool cap, or both in combination as currently written.
3. Cross-register single-sequencing latency: how one received_at order is coordinated across the cadastre and the building register without a shared sequencer root, so a boundary claim and a footprint claim over the same space cannot both perfect.
4. The market-power threshold and the evidentiary standard for rebutting the acting-in-concert independence presumption (PROP-I14).

## Rent, the commons and the distributive overlay

### Purpose

This section defines the MOS delta over ordinary property: the overlay that measures economic rent, the unearned share of captured value, and routes it to the commons. It governs location rent on land, monopoly and scarcity rent on concentrated classes, money rent on credit instruments, and the "new land" of aggregate data, foundation models and large compute. It fixes how rent is assessed, who owes it when possession and title diverge, how the housing capability floor is funded and protected, and how recovered rent returns to persons as a floored citizen dividend. It states the doctrine identically where P2, U1, M3 and F8 must implement their side.

### Object model

- location_rent_obligation: {parcel_ref (P2); site_value (independent appraisal); improvement_residual; rent_amount; assessment_event (C7); last_refresh; next_refresh_by; contest_ref (R1 or A6)}. A standing, never-zero, appealable charge on the land component only.
- benchmark_reference: {class; basis in {counterfactual_cost_plus_return, comparable_competitive_market, comparable_adjusted, zone_proxy, self_assessed_with_buyout}; market_power_flag}. Observed in-market price is excluded once market power is present.
- homestead_protection: {person_ref; primary_dwelling_ref (single registered); floor_quantum (per-cohort capability-floor shelter value, Art. 6); deferred_accrual; crystallization_trigger}. Attaches on placement or occupation, defers rather than extinguishes.
- new_land_steward: {aggregate_ref (data, model weights, large compute); steward (Polity-rooted); no_exclusion_duty; extraction_grant_ref; disclose_or_license_duty; default_commons_share (governance floor, above zero)}.
- extraction_grant: {deposit_or_aggregate_ref; grant_terms; expiry (mandatory, finite); revocable (mandatory trigger); rent_basis (mandatory); restoration_bond (funded, $ rail, K10-sized, revalued); restoration_duty (K10)}.
- commons_rent_fund: {inflows; housing_floor_reinvestment; essential_access_delivery; citizen_dividend_paid; civilizational_reinvestment; per_period_report}.
- citizen_dividend: {period; net_recovered_rent; floor_share (hard, Art. 6 or A10 floor); per_capita_settlement ($ rail); floor_weighting; cohort_estimator (S5); fallback_flat_component}.
- concentration_frame: {owner_cluster; sealed_holdings (S5); over_ceiling_bool; charge_total}. State organs read only booleans and totals.

### Invariants

- RENT-I1 (measurement doctrine): rent SHALL be measured as unearned = value_captured minus value_created, computed as an OVERLAY in the AE ledger over V2 and V3 events. The underlying object or instrument is never AE-denominated; only the resulting commons charge routes via remediation_routing (the R2 exception). This mirrors the F8-I boundary: the instrument itself never touches the AE ledger.
- RENT-I2 (location rent standing): every parcel SHALL carry a standing location_rent_obligation on the LAND component alone; the structure is earned and private. Community-created location value is commons-owed and never lapses through possession or delay.
- RENT-I3 (land/improvement split): the land component SHALL be assessed INDEPENDENTLY of the holder's improvement declaration, using site-value appraisal (the parcel valued as if vacant, from comparable land transactions) as the primary basis, with improvement value as the residual, never the reverse. The assessment is a public C7 event not reducible by holder-supplied improvement figures. Deliberate misallocation to depress the land basis is S7 audit_evasion and an A18 offense, with the burden on the holder to justify the split against the public benchmark.
- RENT-I4 (monopoly and money-rent benchmark): the C7 competitive benchmark for a concentrated class SHALL be constructed COUNTERFACTUALLY (marginal cost plus a benchmark risk-adjusted return, or comparable competitive markets), never from observed in-market prices. When a holder's aggregated share exceeds a market-power threshold the observed price is excluded from its own benchmark; a thin or single-seller market shifts the benchmark to the cost-based reference by construction. This applies identically to F8 money rent: earned components (risk premium, service and monitoring fees) are benchmarked against C7 references and any excess is charged as unearned; fees, points and affiliated-service charges economically tied to the credit are pulled into the instrument's yield (substance over form) so interest cannot be laundered into fee income outside the overlay.
- RENT-I5 (new-land stewardship): aggregate data, foundation-model and large-compute commons SHALL be held under stewardship (steward duties, no exclusion of legitimate access), NOT freehold, paralleling the no-freehold-land rule. Private benefit requires a mandatory extraction_grant plus a duty to disclose or license aggregates. An existing privately held aggregate crossing a governance-set scale threshold SHALL be brought under stewardship by the conversion route (register the steward, attach the extraction_grant, open legitimate access). The created-versus-aggregate split is a rebuttable presumption AGAINST the holder. The data-rent flag applies to data value realized through a service, API or internal model-training, not only a "sold as a good" event. A rebuttable DEFAULT commons share applies to each new-land basis (the network-effect and aggregate-data component is presumptively commons-owed at a governance-set floor percentage above zero); the holder bears the burden of proving a smaller share by audited cohort-grain V3 accounting, and absent proof the default is charged.
- RENT-I6 (extraction-grant discipline): an extraction_grant SHALL carry a finite expiry, a revocation trigger, and a rent_basis; a grant lacking any of the three fails closed at registration. It SHALL carry a funded restoration bond or escrowed security on the $ rail, sized to the K10 restoration estimate, revalued over the term, drawable by the steward on breach independent of the grantee's solvency. Drawdown of extraction proceeds beyond the point where restoration remains under-funded is barred.
- RENT-I7 (concentration ceiling and aggregation): aggregate holdings above the ceiling self-charge as anti-value under Charter Art. 10 (the anti-concentration self-charge). Aggregation extends from common control to acting-in-concert or coordinated economic interest: related parties (kinship, prior coordination, shared financing, option or loan-back arrangements) and holdings assembled to stay sub-threshold are presumptively summed, with the burden on the holders to prove genuine independence. Deliberate fragmentation to stay below the band is an aggravating A18 basis.
- RENT-I8 (homestead cap and deferral): the location-rent abatement SHALL be capped to the per-cohort capability-floor value of shelter (a floor quantum) on a single registered primary dwelling per person. Location rent on value above the floor quantum, and on any additional dwelling, stays commons-owed. Homestead abatement is disallowed where the holder's aggregate land trips the Art. 10 ceiling. The abatement DEFERS rather than extinguishes: it accrues as a non-punitive charge on the title that crystallizes when the dwelling leaves floor scope or is transferred, so the obligation never lapses (P2 location-rent permanence) yet never pushes an occupant below the floor.
- RENT-I9 (housing floor, lexically prior): the housing and shelter capability floor binds by operation of law from the fact of actual lawful occupation, substantively non-defeasible and lexically prior to ordinary property rules. The registrar SHALL auto-register an occupancy-floor marker on the R5 occupancy attestation so it is surfaced in the R1 public-faith minimum and every gated acquirer and F8 lender takes with notice; registration is the mandatory notice mechanism, not a precondition of the floor's survival. An occupancy floor whose lawful basis PRE-DATES a registered security interest binds the enforcing secured party; an occupancy grant created AFTER a registered security interest is subordinate to it for enforcement. The shelter CAPABILITY floor is never collateral (a security interest naming it is void); the dwelling OBJECT above the floor is pledgeable, so a mortgage on a floor-protected dwelling is valid, and enforcement is floor-limited: title may transfer but the occupancy floor and the A9 dignity floor (enforced via A18) persist and cap recovery.
- RENT-I10 (arrears priority): accrued location-rent arrears retain commons priority and ride with the asset, ranking ahead of ordinary unsecured claims immediately after the capability-floor carve-out and A18 restoration, and never falling into the pro-rata unsecured pool.
- RENT-I11 (equity-side timing): the commons charge attaches to an organization's rent as MEASURED per period (a flow assessment on the firm), independent of distribution, so retained rent is charged when captured. A share sale realizing accumulated-but-uncharged rent is a triggering event, with the unearned component priced before the equity holder keeps the gain.
- RENT-I12 (sealed aggregation, no per-person read): no state organ SHALL perform a per-person read of an actor's holdings without consent or an A6 judicial_access_contract. Holdings are committed into per-owner-cluster concentration_frames that the S5 sealed evaluator sums under seal, emitting only over-ceiling booleans and charge totals, never the underlying holdings. Beneficial-owner tracing routes through the A6 judicial_access_contract carve-out this rule already names, with criminal-class liability and clawback under A18-I45.
- RENT-I13 (citizen-dividend floor): a hard floor on the dividend share SHALL bind: a minimum fraction of net recovered commons rent settles per-capita on the $ rail each period, floor-weighted toward persons nearest a capability floor. The A10 dial MAY raise this share but SHALL NOT breach the floor. Fund inflow, dividend paid and reinvestment SHALL be publicly reported per period so a nominal-but-undelivered dividend is detectable. The data component is estimated by a cohort-grain sealed-evaluator marginal-contribution estimator over registered frames (S5); a fallback flat data-dividend from a defined share of data-good and compute rent SHALL pay so the dividend does not depend on the unsolved attribution before it can pay anything.
- RENT-I14 (possession-divergence debtor): where possession and title diverge, the rent_obligation attaches to the party in beneficial possession or enjoyment from the point a possession or contest marker is registered, not the dispossessed titleholder, with reconciliation at A6 ripening and S1-I14 restitution to a good-faith prior holder. The obligation runs with enjoyment of the location, not the paper title.
- RENT-I15 (illiquid fallback): for property C7 cannot benchmark, a fallback valuation SHALL apply (comparable-adjusted or zone proxy, or a self-assessed value carrying a public buy-out option), each with an R1 or A6 contest route. The rent_obligation SHALL always resolve to a computable, appealable figure and SHALL NEVER default silently to zero or to an unbounded estimate.
- RENT-I16 (revaluation cadence): a maximum revaluation interval SHALL bind, with event-triggered reassessment on nearby transactions, rezoning, or infrastructure that shifts location value. Inter-assessment appreciation SHALL be captured via a true-up or an assessment-uplift charge on disposition, so community-created value between refreshes is commons-owed rather than pocketed.

### Protocols

- RENT-P1 (rent decomposition and routing): 1) resolve the C7 benchmark for the class per RENT-I4 (counterfactual for concentrated or thin markets). 2) Compute unearned = captured minus created against the benchmark; for new-land bases apply the RENT-I5 default commons share unless the holder discharges the burden. 3) Book only the resulting commons charge, routing it via remediation_routing (the R2 exception); the object or instrument never touches the AE ledger.
- RENT-P2 (location assessment): 1) run the independent site-value appraisal (RENT-I3) as a public C7 event; use RENT-I15 fallback where no benchmark exists. 2) Set or refresh the standing location_rent_obligation, stamping next_refresh_by within the RENT-I16 maximum interval. 3) On a triggering event (nearby transaction, rezoning, infrastructure) reassess ahead of cadence and apply a disposition uplift for appreciation since last refresh. 4) Debit the current beneficial possessor per RENT-I14.
- RENT-P3 (extraction grant): 1) validate expiry, revocation trigger and rent_basis, else fail closed. 2) Require and lock the funded restoration bond on the $ rail, sized to K10 and revalued over the term. 3) Meter proceeds; bar drawdown past the point restoration is under-funded. 4) On breach, the steward revokes and draws the bond independent of grantee solvency and books anti-value.
- RENT-P4 (commons fund and delivery): 1) collect location rent, monopoly and money-rent charges, concentration charges and extraction rent into the commons_rent_fund. 2) Settle the RENT-I13 floored per-capita citizen dividend on the $ rail, floor-weighted. 3) Discharge the housing-floor reinvestment obligation: fund acquisition or lease of dwellings for below-floor cohorts, with homestead_protection attaching on placement. 4) Fund per-cohort access delivery (procurement or subsidy) for essential-good classes from recovered concentration charges and commons rent, so a below-floor cohort receives the good; the ceiling and the delivery obligation are two halves of one floor. 5) Publish the per-period report.
- RENT-P5 (sealed concentration charge): 1) commit holdings into per-owner-cluster frames including acting-in-concert presumptions (RENT-I7). 2) The S5 evaluator sums under seal and emits only over-ceiling booleans and charge totals. 3) Charge the excess under Art. 10; route beneficial-owner tracing and A18-I45 clawback through the A6 judicial_access_contract carve-out only.

### Lifecycle and edge cases

- Prime-location primary residence: abatement is capped at the floor quantum (RENT-I8); rent on value above the quantum is charged and the abated portion defers as a title accrual crystallizing on transfer or exit from floor scope. A holder cannot park concentrated location value in nominal floor status.
- Post-mortgage collusive lease: an occupancy grant created after a registered security interest is subordinate for enforcement (RENT-I9), so it cannot strip the mortgagee, while a genuine pre-dating resident binds the enforcing party.
- Hyperscaler self-attribution: a data or model holder asserting near-total own-creation carries the burden against the RENT-I5 default commons share and the presumption-against split; absent audited cohort-grain proof, the default is charged, and value realized through a service, API or internal training is in scope.
- Cornered market: because the benchmark is counterfactual (RENT-I4), a more complete monopoly does not shrink the measured rent toward zero; observed price is excluded from its own benchmark.
- Retain-and-sell: rent retained inside a firm is charged as measured per period; a later share sale realizing uncharged accumulation is itself a triggering event (RENT-I11).
- Adverse possession before ripening: the rent debtor is the beneficial possessor from the contest marker forward, not the dispossessed titleholder (RENT-I14); floor and stewardship duties survive any correction.
- Shell extractor: revocation and anti-value against an empty shell are backstopped by the pre-funded, solvency-independent restoration bond (RENT-I6).

### Interfaces

- P2 and U1: implement the RENT-I9 housing floor and RENT-I2 land-rent permanence; P2 carries the extraction_grant_ref schema in conformance with RENT-I6 and the usufruct use-or-reversion teeth; the co_ownership_body floor override implements the lexical priority stated here.
- M3 and F8: essential-good access delivery is funded via RENT-P4; F8 money-rent decomposition is benchmarked per RENT-I4; the AE boundary of RENT-I1 aligns with F8's instrument boundary.
- C7 supplies site-value and counterfactual benchmarks; S5 supplies the sealed concentration and dividend estimators; A10 dials the dividend and reinvestment split above the hard floor; A18-I45 is the clawback and criminal-class channel; A9 is the dignity floor enforced via A18.

### External bindings

The overlay adopts the MOS delta openly: rent is treated as unearned and commons-owed, and the doctrine accepts a heavier assessment and disclosure burden than ordinary property regimes in exchange for closing the location, monopoly, money and new-land capture channels. Governance parameters (the maximum revaluation interval, the default commons share floor, the market-power threshold, the dividend floor and the Art. 6 shelter floor quantum) bind to named A-mandate parameters rather than being left to discretion.

### Open questions

1. Calibration of the RENT-I5 default commons share per new-land basis and of the RENT-I4 market-power threshold: pending governance parameter-setting under Art. 6.
2. Precision of the S5 cohort-grain marginal-contribution data estimator relative to the RENT-I13 fallback flat dividend: how quickly the estimator can replace the fallback without a per-person read.
3. Interaction of the RENT-I8 deferred homestead accrual with long-horizon compounding: whether crystallized accruals need a cap indexed to the floor quantum to remain non-punitive.