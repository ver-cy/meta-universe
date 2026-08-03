# Economy and Markets: the C1, K8, C2 specification

> **Status:** DRAFT v0.1 (2026-07-31). Deepens the economy-production layer of the [World Model Architecture](../World-Model-Architecture.md): C1 Business and Organization, K8 Manufacturing and Production, C2 Market and Exchange, plus the firm value account, the market/civilizational-value doctrine, and the competition/anti-abuse layer. Register rows: C1, K8, C2 in [`world-models.csv`](../world-models.csv). Sits on the value substrate (V1-V5), the S cluster, R1/R2, K2/X1, A18, and the property spec; it operationalizes [Markets-and-Civilizational-Value](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Markets-and-Civilizational-Value.md), [Property-Rent-and-Commons](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Property-Rent-and-Commons.md) and [Value-Money-Coupling](https://github.com/orkestron-ai/meta-orchestrator-state/blob/main/methodology/Value-Money-Coupling.md). On conflict with the architecture summary, this document governs for these models.
> **Provenance:** six parallel specifiers (firm core; firm value and civ-value; production; market core; the market/civ-value doctrine; and competition and anti-abuse), then five adversarial reviews (a market-abuse attacker, an externality-evasion and rent-extraction attacker, the doctrine keeper, a worker-consumer-and-access reviewer, a systems pragmatist: 56 findings, 21 critical), then one revision under a 35-point resolution charter. Both market abuse and over-restriction of legitimate enterprise are catastrophic on this surface, so the review found and the charter closed exploits on both flanks with equal weight.

---

## 0. How the economy layer works

This is where "society as a graph of value transformers" becomes an economy. It encodes one governing idea from the MOS market doctrine: the market clears, the state prices only the residual. The market efficiently clears revealed value (what actors will pay, on the $ rail) and the state never sets a price; it prices the externality residual the market ignores, as a multidimensional Pigou overlay on the Ae vector, and it generates strategic demand where a value dimension is under-served, rather than commanding production. Profit is decoupled from civilizational value: a profitable firm may be civ-value-negative on some axis and is charged for its anti-value, while lawfully created value and genuine efficiency are fully protected.

**The firm and its two ledgers (C1, FVAL).** A firm is a V1 value transformer and an O1 organization with one controller through officers, existing constitutively in the commercial register. Its two ledgers never meet: profit is a $ figure, civilizational position is a pure-Ae per-axis quantity (created value minus anti-value plus attested spillovers), and the two are never netted or inter-converted. Anti-value on a capability-floor axis can never be bought back by a credit on another axis. Unearned and monopoly rent is charged as measured per period against a counterfactual benchmark built on independently attested cost, never the firm's own numbers; the concentration charge attaches to demonstrated pricing power or systemic centrality, never to raw efficient size; and the criminal class follows culpable conduct, not mere ownership. A protected free-competition band between marginal cost and the competitive price carries neither a rent charge nor a predation offense, so legitimate competition and the efficient winner are safe.

**Production and its externalities (K8).** Production transforms materials into goods as append-only acts, and its anti-value (emissions, waste, depletion, labor displacement) is measured at the run, carried on the good's provenance, and priced through the overlay on a running ledger that never double-charges the same residual across the supply chain, includes a producer-attributed use-phase and end-of-life component, follows offshored production back across the border at import-parity, and cannot be laundered by reclassifying waste as a saleable by-product. Labor displacement funds a delivered capability floor to the identified displaced cohort, binding past the end of employment, not merely a charge routed to the commons.

**Markets, competition and the residual (C2, MVAL, COMP).** Markets clear on the $ rail through frequent sealed batch auctions that deny a latency race, with integrity surveilled by the venue steward under seal and any per-participant resolution gated by a judicial contract. The civ-value overlay prices the residual and generates strategic demand on the $ rail (never as transferable Ae), with its own parameters (axis weights, strength dial, the market-power threshold) bound by the same anti-capture discipline and structurally separated from the organs that receive the charges. The anti-abuse layer catches cartels including tacit and algorithmic collusion (located in the deployment decision), monopolization and killer acquisitions, market manipulation, and systemic risk (with a named shortfall waterfall and a hard structural cap where no bond can absorb the cascade), while explicitly protecting the large efficient firm, the new entrant bootstrapped at a sector-default escrow, and the small competitor.

Three commitments recur, matching the rest of the model:

1. **The state prices the residual, never the price.** The market allocates; the overlay corrects the gap between revealed and civilizational value; strategic demand pulls, it does not command; and the parameter layer that could become a hidden price-setting lever is bound by the same anti-capture rules as everything else.
2. **Rent and anti-value are charged, created value is protected.** Efficiency, innovation returns, and genuine spillovers are credited; only pricing-power rent, unpriced externalities, and concealment are charged, on independently attested bases, with suspensive contest so a charge is never an unadjudicated penalty.
3. **Both flanks delivered.** The displaced worker, the consumer and the below-floor cohort get delivered floors funded from a standing reserve, while legitimate competition, the efficient winner and the new entrant are never criminalized for being large or productive.

The sections follow: C1 firm core; FVAL firm value and civ-value; K8 production; C2 market core; MVAL market and civ-value doctrine; COMP competition and anti-abuse.

---
## C1 business and organization: the firm as a value transformer

### Purpose

The firm is the unit that transforms inputs into outputs and, in doing so, both creates civilizational value and generates anti-value. This section defines the firm as a dual-ledger entity, fixes how its position is measured without ever converting between the $ rail and the Ae vector, and sets the firm-level machinery for rent, concentration, externality escrow, labor displacement, and personal accountability. Both market abuse and over-restriction of legitimate enterprise are treated as catastrophic. The section SHALL protect the efficient winner and the new entrant while closing every rent, capture, and concealment channel. It leans on the market to clear and to reveal price, on the state to price only the residual, and on personal liability that follows culpable conduct rather than mere ownership or mere size.

### Object model

- firm: identity plus its S1 control graph resolving to natural-person beneficial_owners. A firm MAY be systemic where its centrality exceeds a defined cascade threshold.
- profit_$: the $-rail financial result. A standalone field, never summed into any Ae quantity.
- Ae_vector: the ten-axis civilizational contribution, carrying per-axis created_value(Ae), anti_value(Ae), and positive_spillovers(Ae).
- net_Ae: the per-axis net civilizational position defined in C1-I3. Never a single scalar netted across axes.
- pricing_power: a rebuttable measure of the firm's demonstrated ability to hold price above the competitive level.
- concentration_position: concert-aggregated share plus systemic centrality, assessed against the declared and independently verified beneficial-owner graph.
- externality_escrow: a pre-funded withhold sized per C1-I15 and held against latent and tail harm.
- TrackRecord: attested settlement history, bootstrapped at the sector default for a new firm.
- theta: a participation-condition diagnostic signal indicating a worse-off cohort. A diagnostic input, never a freestanding charge.
- displacement_cohort: the specifically identified displaced workers carrying a bound, delivered floor obligation.

### Invariants

- C1-I1: A firm is a value transformer whose acts are attributed through its S1 control graph to natural-person beneficial owners. Control links that cannot be attested resolve upward, not into a void.
- C1-I2: The $ rail and the Ae vector SHALL NOT net or inter-convert. profit_$ SHALL NOT be netted against, summed with, or priced from any Ae-vector contribution, and Ae SHALL NOT be converted to a price. The two bookings never meet on one line.
- C1-I3: Civilizational position is a single pure-Ae quantity, per axis: net_Ae = created_value(Ae) minus anti_value(Ae) plus positive_spillovers(Ae). created_value(Ae) is the Ae credit for realized, buyer-revealed created value, NOT the $ revenue figure. Where a formula elsewhere reads "market_revenue" in a civ-value expression, it denotes this Ae credit for revealed created value, never the $ amount. profit_$ remains a separate, never-summed $ field, so a revenue-inclusive figure can never double-count profit_$. This label net_Ae is unified across C1, FVAL and MVAL.
- C1-I4: No cross-axis netting into standing or access. Per-axis net positions SHALL be computed, and anti-value on any capability-floor or hard-limit axis (A9 dignity, Art. 6 cohort floor, Art. 4 safety, depletion beyond a regeneration bound) SHALL NOT be offset by credits on other axes. A floor-axis breach routes to the A18 ladder regardless of a positive aggregate; spillover credits raise standing only within non-floor axes. The standing or access consequence triggers on a per-axis threshold breach, never on an undefined scalar over the vector.
- C1-I5: Concentration aggregation SHALL be positively verified. The beneficial-owner graph at every gated acquisition is checked against independent asset-discovery data (R1-I39) and backed by a forfeitable stake, not accepted on self-declaration. Unverifiable control links default to the concentration-summed, high-scrutiny class until attested. Concert-summing reaches acting-in-concert parties with the burden on the firm to prove independence.
- C1-I6: The concentration charge attaches to unrebutted pricing power or systemic centrality, never to raw size. A firm that rebuts power (demonstrated cost pass-through, a contestable market, all frames improving) faces only systemic-resilience duties (escrow bond, resolution plan), not a size charge. The rent overlay and the concentration charge SHALL NOT both charge the same captured-minus-created value.
- C1-I7: The rent charge is the margin attributable to demonstrated pricing power, meaning price held above the competitive level, not the full gap between observed and normal return. The counterfactual SHALL use an independently attested cost basis (C7), never the firm's self-reported cost; a firm's measured cost or efficiency advantage is credited as created value inside the counterfactual, and innovation-driven super-normal returns are time-limit-protected for a patent-style horizon before any rent charge attaches. The interval between marginal cost and the competitive price is an explicitly protected free-competition band carrying neither a rent charge nor an offense.
- C1-I8: The own-price exclusion that turns observed price into the benchmark operates from activation on a conservative default, never null: a firm's own price is excluded from its own benchmark whenever it is pivotal (non-substitutable for some cohort) OR its concert-aggregated share exceeds a stated fraction (default 40 percent), applied uniformly and published with a review clause. A mandate parameter MAY supersede this, but the machinery is never inoperable while the mandate is pending.
- C1-I9: Any realization of accumulated-but-uncharged rent is a triggering event: asset sales, spin-offs, carve-outs, IP transfers or licenses, and liquidation distributions, not only equity-share sales. The unearned component (realization value minus attested cost basis minus already-charged rent, benchmarked counterfactually) SHALL be priced before the holder keeps the gain. Structuring a rent stream into asset appreciation to defer the charge is an A18 aggravating basis.
- C1-I10: Every same-tick anti-value booking against a firm's standing or escrow is a reversible provisional debit or freeze (soft-rung priced_debit) with SUSPENSIVE effect on contest per A18-I34: accrual suspends once the firm contests and is restored with interest if the finding is not sustained. No forfeiture or continuing debit accrues before an A6 attested or confirmed finding or the close of an uncontested attestation window (A18-I6).
- C1-I11: Any anti-value touching a capability floor (A9 dignity, Art. 6 cohort floor, Art. 4 safety, irreversible or ecological-tipping harm) is presumptively non-priceable, with the burden on the FIRM to prove it a bounded, reversible, priceable residual. Repeated same-class residual charges above a threshold escalate a nominally-priceable harm into floor-breach review, closing the pay-to-continue license.
- C1-I12: A theta signal is a diagnostic, not a freestanding charge. Bookable anti-value from theta SHALL be conditioned on the residual being an independently measured V4 harm and/or a measured Art. 6 cohort-floor breach; otherwise a theta breach routes only to overlay recalibration or A7 incentives, never a priced charge or a ban by itself. Smallness confers no immunity: a complaint- or floor-breach-triggered S2 or A6 judicial-access path MAY authorize measuring theta and the residual for a specifically identified cohort below the k-anonymity floor. The k-floor protects privacy against untriggered surveillance, never a firm against identified-harm inquiry.
- C1-I13: Routing of a firm's floor breach follows the Charter axis. An actual Art. 4 life or bodily-integrity breach routes to the in-kind, non-priceable criminal ladder with no buy-out (A18-I2, A18-I3). An Art. 6 cohort-floor safety or access breach routes to priced-class cohort restitution PLUS the licensed hard ladder via the cohort_floor severity band (A18-I44), never the in-kind criminal class. The conformance_release pre-market gate is unchanged.
- C1-I14: The non-priceable criminal class attaches to the culpable natural persons, meaning whoever knew, directed, or recklessly enabled the offense, be they officer, owner or both, on individualized objective-corroborated evidence (A18-I9). Beneficial ownership triggers clawback of proceeds and standing loss regardless of culpability, but criminal-class consequences require culpable participation, not mere ownership. Deployment of a pricing algorithm that produces sustained coordinated supra-benchmark pricing is itself a provable individualized act by the deploying or licensing beneficial owner, personally attributable under A18-I45, and above-threshold actors carry a disclosure and auditability duty for such algorithms.
- C1-I15: Debt peonage, bonded labor, and total-life capture (bundling employment with debt, housing and essential supply to foreclose exit) are non-priceable A9 and A18 criminal-class offenses that cannot be bought out. A single firm's cross-market capture of one dependent cohort SHALL aggregate as a concentration or theta trigger independent of per-market share, so the smallness of each market confers no immunity.
- C1-I16: The externality escrow SHALL be floored by worst-case or harm-capacity exposure for high-harm, latent-harm and systemic classes, a minimum that TrackRecord cannot erode, with a scale term so absolute exposure sets a hard floor. A new firm bootstraps at the sector-default TrackRecord, not zero (missing history reads as sector-average, never worst-case). The escrow fraction is capped at a stated ceiling of exposure; clean settlements ratchet it down within a bounded band only; detection of any concealed harm resets the multiplier.
- C1-I17: Positive-spillover credits carry an additionality-and-attestation discipline mirroring the rent counterfactual: credited only for demonstrated value that would not have occurred absent the firm, no credit for baseline or state-funded activity, multi-source and revaluable, with the burden on the firm. Materially overstated positive-spillover claims are an A18 concealment-class offense with the same clawback as anti-value concealment, and net self-originated credit against a firm's own anti-value is capped. Credited positive spillovers draw a matching Pigovian subsidy from the commons rent fund on the same $ rail and timescale that harmful production is charged; the Ae credit itself stays non-convertible.

### Protocols

- C1-P1 (dual-ledger booking cycle): each tick, book profit_$ on the $ rail and the Ae vector separately per C1-I2, computing per-axis net_Ae per C1-I3 with no cross-axis netting (C1-I4). Any measured anti-value posts as a reversible provisional debit or freeze with suspensive effect on contest per C1-I10; cross-cite A18-I34 and A18-I6.
- C1-P2 (rent and concentration assessment): apply the own-price exclusion per C1-I8, construct the counterfactual on an independently attested cost basis (C7) crediting the firm's efficiency and innovation advantage as created value (C1-I7), and charge only the pricing-power margin. Attach the concentration charge to unrebutted power or centrality (C1-I6), never to size, and never double-charge the same captured-minus-created value.
- C1-P3 (acquisition and merger review): positively verify the beneficial-owner graph against R1 asset-discovery and require a forfeitable stake (C1-I5); concert-sum the aggregate share; and for any acquirer above a market-power or systemic threshold, run a forward-looking test for loss of nascent or future competitive constraint independent of current-share aggregation, with the burden on the acquirer to show the target is not a nascent competitor.
- C1-P4 (displacement floor delivery): identify the displaced cohort at run and sector grain, apportion cohort displacement that no single run accounts for across contributing firms by automation-intensity or output-share, extend booking to supply-chain-mediated and cross-jurisdiction displacement traceable to the run's controller, and fund a delivered capability floor (income bridge plus retraining or placement) that binds beyond the end of employment. The charge is not discharged until the floor is delivered, not merely routed to the commons; the A9 dignity floor persists post-displacement.
- C1-P5 (realization pricing): on any rent-realization event (C1-I9), price the unearned component before the holder keeps the gain, benchmarked counterfactually against the attested cost basis and already-charged rent.

### Lifecycle and edge cases

- New firm: bootstraps at the sector-default TrackRecord (C1-I16), so absence of history never reads as worst-case and never raises a near-infinite entry barrier. The escrow fraction is capped; the entrant faces the rent overlay and never coercion for efficient scale.
- Systemic node: a firm whose centrality exceeds the cascade threshold where no feasible bond can absorb the cascade faces a HARD STRUCTURAL CAP (mandatory de-concentration, divestiture or split until residual cascade is at most the feasible bond), not a payable charge. A systemic firm in an essential class SHALL maintain a pre-committed, ring-fenced, transferable essential-function unit that continues the function through resolution without the firm's cooperation. Detailed waterfall and bond sizing live in COMP; C1 supplies the firm-level structural duty.
- Toll and contract manufacturing: the commissioning or directing firm is jointly and severally liable for the embodied anti-value of production it directs and profits from, concealment or not. The toll manufacturer's inadequate escrow does not cap recovery; the party that captured the value carries the residual its order generated (see K8 for the run-side machinery).
- Finality: honest and non-gross is final on window close. Concealed or intentional is perpetually clawback-eligible regardless of size. Honest but gross-and-latent is revaluable within a bounded long window (a mandate parameter), with escrow as the honest firm's pre-funded protection. Perpetual liability never attaches to honesty alone.
- Dissolution or shell: standing loss and clawback of proceeds follow the beneficial owner (C1-I14) and pierce the S1 graph per A18-I45; a firm cannot dissolve to shed a concealed or intentional liability.

### Interfaces

- C7 (appraisal, valuation, and counterfactual benchmark): supplies the independently attested cost basis and competitive-price benchmark for C1-I7 and C1-P2. This is the Property-and-Ownership.md use of C7 (appraisal and valuation), not the older "Property and Ownership" code.
- C5 (settlement and escrow) and C6 (routing): C5 settles the provisional and confirmed debits of C1-I10 and holds the externality escrow of C1-I16; C6 routes confirmed charges to the commons rent fund and the citizen dividend, and routes the matching Pigovian subsidy of C1-I17.
- S1 (control graph), R1 (asset discovery): resolve and verify the beneficial-owner graph for C1-I5, C1-I14 and C1-P3.
- A18 (offense ladder): receives floor-breach routing (C1-I11, C1-I13), concealment offenses (C1-I9, C1-I15, C1-I17), and personal attribution (C1-I14); cross-cited invariants A18-I2, A18-I3, A18-I6, A18-I9, A18-I34, A18-I44, A18-I45.
- A6 and S2 (judicial access): gate the small-cohort theta path of C1-I12 and confirm findings for C1-I10.
- K8 (production externality), FVAL, MVAL, COMP, C2: K8-I12 sizes the production externality escrow feeding C1-I16; FVAL and MVAL share the unified net_Ae and the spillover discipline; COMP owns the systemic waterfall and the predation floor; C2 owns venue conformance and market integrity.

### External bindings

- Charter Art. 4 (life and safety), Art. 6 (cohort floor), Art. 9 (A9 dignity), Art. 10 (concentration ceiling), Art. 12 (participation), Art. 13 (Ae non-convertibility).
- The market-power default fraction (C1-I8), the innovation-protection horizon (C1-I7), and the finality long-window (lifecycle) are mandate parameters; C1 ships operable conservative defaults so no guarantee is suspended pending calibration.

### Open questions

- The exact market-power threshold fraction ships at a conservative default (40 percent or pivotal); the recalibration cadence and any per-sector variation remain a mandate question, though the machinery is never inoperable while pending.
- The innovation-protection horizon length (C1-I7) is unset; too short confiscates the innovator's reward, too long shelters entrenched rent.
- Fine-grained apportionment of the responsibility_share between a culpable non-owner officer and a passive owner (beyond the criminal-class attachment fixed in C1-I14) still needs an evidentiary boundary.
- Cross-jurisdiction displacement (C1-P4) and offshored runs whose controller cannot be reached by S1 tracing leave a residual attribution gap where no MOS-reachable controller exists.

## The firm value account: profit, civilizational value and the externality residual

### Purpose

The firm value account is the per-firm ledger that holds, side by side and never
summed, two irreducibly different quantities: profit_$, the money result of a firm's
market activity, and net_Ae, its civilizational position expressed purely in Ae. The
account exists so that a firm can be economically successful and civilizationally
positive, economically successful and civilizationally negative, or any combination,
without either measure laundering the other. It carries the counterfactual rent
decomposition (created value versus captured pricing-power rent), the positive-spillover
credit with its attestation discipline, and the externality residual with its escrow.
Both failure modes are catastrophic here: a leaky account lets a net-harmful firm buy
back standing with cheap credit or launder rent through padded cost, while an
over-tuned account confiscates legitimate efficiency, innovation and entry. The
invariants below are written to hold both flanks.

### Object model

- `firm_value_account`: `{ profit_$, net_Ae_vector, escrow, benchmark_ref, provenance }`.
  profit_$ and net_Ae never occupy one field and never net.
- `net_Ae_vector`: a per-axis vector over the ten Ae axes. Each axis carries
  `created_value(Ae) - anti_value(Ae) + positive_spillovers(Ae)`. There is no scalar
  collapse of the vector for standing or access decisions (see FVAL-I4).
- `profit_$`: the money field. Denominated only in $. Never a summand of net_Ae and
  never a price attached to any Ae quantity.
- `rent_decomposition`: `{ observed_return, created_value, captured_rent,
  competitive_band }` produced against `benchmark_ref` (a C7 appraisal, valuation and
  counterfactual-benchmark model), never against the firm's own reported figures.
- `spillover_claim`: `{ axis, magnitude, counterfactual, attestations, additionality }`,
  a firm-supplied claim carrying the burden of proof.
- `escrow`: withheld externality funding `{ fraction, capacity_floor, track_record,
  multiplier }` settled through C5 (settlement and escrow) and routed through C6
  (routing) to the commons rent fund or a delivered capability floor.
- `realization_event`: any event realizing accumulated-but-uncharged rent (equity sale,
  asset sale, spin-off, carve-out, IP transfer or license, liquidation distribution).

### Invariants

- FVAL-I1: The account holds profit_$ and net_Ae as separate quantities that SHALL NOT
  be netted, summed, or exchanged. profit_$ SHALL NOT offset any Ae anti-value, and no
  Ae credit SHALL raise or lower profit_$. The two bookings never net.
- FVAL-I2: Civilizational position is a single pure-Ae quantity computed per axis as
  `created_value(Ae) - anti_value(Ae) + positive_spillovers(Ae)`. Where a formula in
  C1-I6 or MVAL-I4 names `market_revenue`, that term denotes the Ae credit for revealed
  created value (the citizen-directed contribution the buyer revealed), NOT the $ revenue
  figure carried in profit_$. The label net_Ae is unified across C1, FVAL and MVAL.
- FVAL-I3: Ae SHALL NOT be converted to a price, spent, or transferred. A spillover
  credit is a booked-not-transferred standing credit to the firm's OWN Ae account, never
  consideration a buyer pays or a seller receives. Standing and access consequences read
  from net_Ae only; they never read from profit_$.
- FVAL-I4: The consequence rule operates per axis. Standing or access loss triggers when
  any single axis breaches its published per-axis threshold; there is no undefined scalar
  over the vector. Anti-value on any capability-floor or hard-limit axis (A9 dignity,
  Art. 6 cohort floor, Art. 4 safety, depletion beyond a regeneration bound) SHALL NOT be
  offset by credits on any other axis. A floor-axis breach routes to the A18 ladder
  regardless of a positive aggregate; spillover credits raise standing only within
  non-floor axes.
- FVAL-I5: The cost basis feeding any cost-plus-normal-return counterfactual SHALL be
  independently attested (audited, peer-efficient-frontier, or best-available-technology
  cost model) and SHALL NEVER be the firm's self-reported cost. Inputs from affiliates or
  acting-in-concert parties are re-priced at arm's length, or the affiliate's costs are
  consolidated, recursing the own-price and own-cost exclusion up the supply chain.
  Above-benchmark input prices, related-party compensation above a published norm, and
  rent capitalized as asset carry are stripped from the cost base. Unexplained cost
  inflation is presumptive rent concealment (A18) with the burden of justifying each cost
  line on the firm.
- FVAL-I6: Captured rent equals only the margin attributable to demonstrated pricing
  power (price held above the competitive level), not the full gap between observed and
  normal return. A firm's measured cost or efficiency advantage is credited as created
  value inside the counterfactual, so an efficient winner is rewarded, not confiscated.
  Innovation-driven super-normal returns are time-limit protected (a patent-style horizon
  mandate parameter) before any rent charge attaches. The interval between marginal cost
  and the competitive price is an explicitly protected free-competition band carrying
  neither a rent charge nor an offense; penetration and entry pricing inside it is
  lawful. A firm's own price is excluded from its own benchmark whenever it is pivotal
  (non-substitutable for some cohort) OR its concert-aggregated share exceeds a stated
  fraction; the operable default from activation is 40 percent, uniform and published
  with a review clause, superseded only by a mandate parameter and never inoperable while
  one is pending.
- FVAL-I7: A positive-spillover credit is booked only for demonstrated value that would
  not have occurred absent the firm (additionality), with no credit for baseline or
  state-funded activity. The claim is multi-source, revaluable, and carries the burden of
  proof on the firm, mirroring the rent counterfactual. Materially overstated spillover
  claims are an A18 concealment-class offense carrying the same clawback as anti-value
  concealment. Net self-originated credit is capped against the firm's own anti-value; a
  firm cannot become net-positive on self-declared credit alone.
- FVAL-I8: The overlay is symmetric in money terms. Credited positive spillovers draw a
  matching Pigovian subsidy from the commons rent fund on the same $ rail and timescale
  on which harmful production is charged. The Ae credit stays non-convertible (FVAL-I3);
  the paid reward is a separate $ flow, so beneficial production is rewarded on the same
  rail that harm is charged rather than only in non-spendable standing.
- FVAL-I9: The externality escrow SHALL be floored by worst-case or harm-capacity
  exposure for high-harm, latent-harm and systemic classes, a minimum that TrackRecord
  cannot erode, with a scale term so absolute exposure sets a hard floor. A new firm is
  bootstrapped at the sector-default TrackRecord, never zero; missing history reads as
  sector-average, never worst-case, so escrow never diverges past feasibility at entry.
  The escrow fraction is capped at a stated ceiling of exposure. Clean settlements ratchet
  the fraction down within a bounded band only; detection of any concealed harm resets the
  multiplier. This is the K8-I12 externality escrow and the A18-I45 risk-proportionate
  escrow_bond, not the P2-I7 restoration_bond.
- FVAL-I10: Any anti-value touching a capability floor (A9 dignity, Art. 6 cohort floor,
  Art. 4 safety, irreversible or ecological-tipping harm) is presumptively non-priceable,
  with the burden on the FIRM to prove it a bounded, reversible, priceable residual.
  Repeated same-class residual charges above a threshold escalate a nominally-priceable
  harm into floor-breach review, closing the pay-to-continue license.
- FVAL-I11: The non-priceable criminal class attaches to the culpable natural persons
  (whoever knew, directed, or recklessly enabled the offense, be they officer, owner or
  both) on individualized objective-corroborated evidence (A18-I9). Beneficial ownership
  triggers clawback of proceeds and standing loss regardless of culpability, but
  criminal-class consequences require culpable participation, not mere ownership.
- FVAL-I12: Finality is two-axis. Honest and non-gross anti-value is final on window
  close. Concealed or intentional anti-value is perpetually clawback-eligible regardless
  of size. Honest but gross-and-latent anti-value is revaluable within a bounded long
  window (a mandate parameter), with escrow (FVAL-I9) as the honest firm's pre-funded
  protection. Perpetual liability never attaches to honesty alone.

### Protocols

- FVAL-P1: Same-tick booking. Every same-tick anti-value booking against a firm's
  standing or escrow is a reversible provisional debit or freeze (soft-rung
  priced_debit) with SUSPENSIVE effect on contest per A18-I34. Accrual suspends once the
  firm contests and is restored with interest if the finding is not sustained. No
  forfeiture or continuing debit accrues before an A6 attested or confirmed finding, or
  the close of an uncontested attestation window (A18-I6). The same-tick number is
  provisional, never an immediate unadjudicated penalty.
- FVAL-P2: Rent decomposition. Compute observed_return, then created_value (including the
  firm's attested cost or efficiency advantage and time-limit-protected innovation
  return), then captured_rent as the residual attributable to demonstrated pricing power
  above the competitive level (FVAL-I6), against a C7 benchmark built on an attested or
  efficient-frontier cost base (FVAL-I5). The rent overlay and any concentration charge
  SHALL NOT both charge the same captured-minus-created value.
- FVAL-P3: Spillover credit and matching subsidy. Validate a spillover_claim for
  additionality, attestation and multi-source ground truth (FVAL-I7); book the
  non-convertible Ae credit to the non-floor axis; and release the matching $ Pigovian
  subsidy from the commons rent fund through C6 routing on the same timescale as harm
  charges (FVAL-I8). Overstated claims route to A18.
- FVAL-P4: Escrow sizing and reconciliation. Size escrow from the harm-capacity floor and
  scale term (FVAL-I9). Embodied anti-value includes a producer-attributed use-phase and
  end-of-life component (lifecycle basis, not gate-to-gate), pre-charged to the producer
  via escrow at production and reconciled against actual use where measurable, so
  use-phase harm of intrinsically harmful goods is borne by the producer. The downstream
  money charge equals measured residual minus what was already charged upstream, on a
  running ledger, so total charged over the whole chain never exceeds the run's measured
  total (the money analogue of the K8-I4 mass balance).

### Lifecycle and edge cases

- Retained-rent realization: the triggering event is ANY realization of
  accumulated-but-uncharged rent (equity sales, asset sales, spin-offs, carve-outs, IP
  transfers or licenses, liquidation distributions), not only equity-share sales. Price
  the unearned component (realization value minus attested cost basis minus
  already-charged rent, benchmarked counterfactually) before the holder keeps the gain.
  Structuring a rent stream into asset appreciation to defer the charge is an A18
  aggravating basis.
- Exiting output: any embodied anti-value allocated to an output that leaves traceability
  or is not downstream-chargeable reverts to and settles against the run controller at
  production, so residual cannot be parked on an exiting or low-value output.
- Toll and contract manufacturing: the commissioning or directing firm is jointly and
  severally liable for the embodied anti-value of production it directs and profits from,
  concealment or not; the toll manufacturer's inadequate escrow does not cap recovery
  (K8 lifecycle).
- Border re-entry: offshoring a run whose output re-enters the polity books the full
  residual at import to the importing controller, tracing to the beneficial owner (border
  externality-parity, K8 and MVAL).
- New-firm bootstrap: escrow sized at the sector-default TrackRecord (FVAL-I9), so entry
  is never strangled by absence of history.

### Interfaces

- C1: firm object, concentration and beneficial-owner graph; shares the unified net_Ae
  label (C1-I6) and the no-double-charge between rent overlay and concentration.
- C2: order and venue layer; all clearing is $-only (C2-I3), consistent with FVAL-I3.
- C5 (settlement and escrow) and C6 (routing): escrow settlement and charge or subsidy
  routing to the commons rent fund and citizen dividend.
- C7 (appraisal, valuation and counterfactual benchmark): the benchmark model of
  FVAL-I5 and FVAL-P2.
- K8: externality escrow (K8-I12), mass balance (K8-I4), lifecycle and toll liability.
- MVAL: the published overlay function, its axis weights and strength dial, and the
  Pigovian subsidy fund of FVAL-I8.
- A18: the ladder for concealment, floor breaches, criminal class and clawback; A18-I34
  and A18-I6 (suspensive contest, provisional freeze), A18-I45 (escrow_bond, piercing).
- S-cluster: net_Ae and residual sensed at S5 cohort grain; per-participant resolution
  only via an S2 judicial access contract through an A6 case.

### External bindings

- Charter Art. 13: Ae is never priced or transferred (FVAL-I3).
- Charter Art. 4 and Art. 6: floor axes and the priceable versus non-priceable split
  (FVAL-I4, FVAL-I10, and the K8 routing split).
- Charter Art. 10: concentration ceiling, referenced for the no-double-charge rule.
- Charter Art. 12: worse-off diagnostic, feeding the escalation of FVAL-I10.

### Open questions

- The innovation-protection horizon in FVAL-I6 and the bounded long window in FVAL-I12
  are mandate parameters; their durations per sector are unset and left to calibration.
- The harm-capacity floor and fraction ceiling in FVAL-I9 need per-class magnitudes; the
  structure is fixed but the numbers await sector harm-capacity models.
- The published per-axis thresholds in FVAL-I4 and the same-class escalation threshold in
  FVAL-I10 require a first calibrated set; the default 40 percent power threshold in
  FVAL-I6 governs meanwhile.

## K8 manufacturing and production: the make half of the economy

### Purpose
Production is the "make" half of the economy: firms transform material inputs into goods and, in doing so, generate both created value and anti-value. K8 encodes how the MOS polity measures a production run, carries the run's embodied anti-value on the good, and lets the state price the externality residual the market ignores WITHOUT commanding production or setting prices. The section closes the evasion routes an adversary will exploit: offshoring a dirty run and re-importing the good, laundering waste into a "product", stranding the residual on a thinly-capitalized toll manufacturer, parking the residual on an exiting output, and double-charging the same tonne down a supply chain. Legitimate, efficient, safe production is fully protected; only the uncharged externality residual and its concealment are pursued. This is doctrine, not generic manufacturing management or environmental-permit law.

### Object model
- production_run: a K2 chain of production acts realized over X1 occurrences (plant or site, bill of materials, routing, batch, lot, yield). run_controller is the C1 firm that directs the run and captures its value; it carries the residual the run generates.
- input_line: an M1 material, F1 energy, C3 labor, or compute input, each with EPCIS provenance and an attested embodied-anti-value figure carried from upstream.
- output: an M3 good carrying an embodied_anti_value ledger entry and, where reclassified from waste, a disposal-contingent tail (K8-I10).
- embodied_anti_value: a LIFECYCLE-basis residual (not gate-to-gate): production-phase F6 emissions, F5 waste, D4 depletion and pollution, and a producer-attributed use-phase and end-of-life component (K8-I14), expressed on the V4 axes of the Ae-vector.
- externality_escrow: pre-funded withholding sized per K8-I12 and A18-I45, floored by harm capacity.
- conformance_release: the pre-market eligibility token for a gated class (M4 food, M5 medicine, and peers).
- recall: an X1 chain reversing distribution of a defective or unsafe subject (K8-I9).
- displacement_cohort: the specifically identified S5 cohort whose C3 work the run or the sector displaces (K8-I11).

### Invariants
K8-I1 A production run is a measured value transformation. The run_controller SHALL be identified as the C1 firm that directs and profits from the run, resolved to its beneficial-owner graph (A18-I45), and every run books its inputs (V3), its created value, and its anti-value (V4) against that controller. Value lawfully created in production is fully protected; the section reaches only anti-value and uncharged residual.

K8-I2 Production externalities are first-class V4 anti-value measured AT PRODUCTION: F6 emissions, F5 waste, D4 depletion and pollution, ecological harm, and labor displacement. They are priced by the uniform published MVAL externality overlay (never by the market, never by a per-firm state price), and the money charge is levied via externality escrow and the continuous anti-value debit of Value-Money-Coupling. The Ae-vector booking of anti-value and the $ market booking never net (FVAL-I2).

K8-I3 Input provenance rides into the run. Each input_line carries its upstream embodied anti-value (K8-I4); an input of unverifiable foreign or illicit provenance SHALL default to a high-anti-value figure with the burden on the run_controller to attest a lower one. Inputs sourced from an affiliate or acting-in-concert party are re-priced at arm's length before they enter the cost and residual base (see FVAL benchmark).

K8-I4 Embodied anti-value rides the good and reconciles by MASS BALANCE: the anti-value carried on all outputs plus the anti-value released to the commons SHALL equal the run's measured total. The good carries its embodied anti-value for disclosure and to catch residual not yet charged upstream. The money charge is governed by a RUNNING-LEDGER no-double-charge rule (the money analogue of mass balance): the charge at any downstream M3 transaction equals the measured residual minus what was already charged upstream, so the total charged over the whole supply chain never exceeds the run's measured total. Productive activity is charged once for one tonne of harm, not once per hand it passes through.

K8-I5 The residual cannot be parked on an exiting output. Any embodied anti-value allocated to an output that leaves traceability (exported under A15, consumed, or bought outside the ledger) or is otherwise not downstream-chargeable SHALL revert to and settle against the run_controller at production. Joint-product and by-product allocation SHALL NOT dump a disproportionate residual share onto a low-value or exiting output to launder the charge.

K8-I6 BORDER EXTERNALITY-PARITY. Any imported good, finished or intermediate, is charged at import the difference between its MOS-overlay embodied anti-value (computed by the same published overlay function on attested, or defaulted-high, embodied anti-value) and the anti-value price demonstrably paid in the origin jurisdiction. "Priced abroad" is a credit only against a verified equivalent charge, never a waiver. Offshoring a run whose output re-enters the polity books the FULL residual at import to the importing controller, tracing to the beneficial owner, so carbon and waste leakage is neither a free evasion nor a cost advantage over domestic producers.

K8-I7 SAFETY-CLASS ROUTING SPLIT. An actual Charter Art. 4 life or bodily-integrity breach routes to the A18 criminal, in-kind, NON-priceable ladder with no buy-out (A18-I2, A18-I3). An Art. 6 cohort-floor safety or access breach routes to priced-class cohort restitution PLUS the licensed hard ladder via the cohort_floor severity band (A18-I44), NOT the in-kind criminal class; over-criminalizing an economic access-floor breach is itself a rights catastrophe. A gated-class good is market-eligible only after a valid unexpired conformance_release and with no open recall; the conformance_release pre-market gate is verified at market as a listing precondition (C2), not post-hoc.

K8-I8 PRICEABLE-RESIDUAL vs FLOOR-BREACH. Any anti-value touching a capability floor (A9 dignity, Art. 6 cohort floor, Art. 4 safety, irreversible or ecological-tipping harm) is PRESUMPTIVELY non-priceable, with the burden on the FIRM to prove it a bounded, reversible, priceable residual. Repeated same-class residual charges above a threshold escalate a nominally-priceable harm into floor-breach review, closing the pay-to-continue license. A priceable residual is paid and production continues; a floor breach is stopped, not licensed.

K8-I9 Quality and safety are enforced through the lifecycle: a defect or emergent harm triggers a recall as an X1 chain reversing custody, and the recall cost and residual attach to the run_controller regardless of who holds the good. Gated classes (M4, M5, peers) carry heightened conformance and traceability duties.

K8-I10 WASTE-TO-PRODUCT anti-laundering. An output reclassified from waste to product carries BOTH its embodied anti-value AND a traceable disposal-contingent tail back to the originating producer, released only on demonstrated genuine beneficial use and forfeited to the originator on sham use or downstream dumping. Sham beneficial-use reclassification is externality concealment (A18) with the burden on the producer to prove the by-product's genuine value and safe fate.

K8-I11 LABOR-DISPLACEMENT booking and DELIVERED floor. Displacement anti-value is booked at the run and measured at S5 cohort grain, and additionally by SECTOR-LEVEL attribution: cohort displacement that no single run accounts for is apportioned across the contributing firms by automation-intensity or output-share and booked even where no run is individually pivotal. Booking extends to supply-chain-mediated and cross-jurisdiction displacement traceable to the run_controller. The charge FUNDS a DELIVERED capability floor (an income bridge plus retraining or placement) to the specifically identified displaced cohort, binding beyond the end of employment with the A9 dignity floor persisting post-displacement; the charge is NOT discharged until the floor is delivered, not merely routed to the commons.

K8-I12 EXTERNALITY-ESCROW SIZING (both flanks). Production escrow (A18-I45 primitive) is sized risk-proportionately but FLOORED by worst-case or harm-capacity exposure for high-harm, latent-harm and systemic classes, a minimum that a good TrackRecord cannot erode, with a scale term so absolute exposure sets a hard floor. A new firm is bootstrapped at the sector-default TrackRecord, never at zero (missing history reads as sector-average, never worst-case), so entry is not strangled. The escrow fraction is capped at a stated ceiling of exposure; clean settlements ratchet it down within a bounded band only; detection of any concealed harm resets the multiplier.

K8-I13 TOLL and CONTRACT manufacturing. The commissioning or directing firm is JOINTLY AND SEVERALLY liable for the embodied anti-value of production it directs and profits from, concealment or not. A toll manufacturer's inadequate escrow does not cap recovery; the party that captured the value carries the residual its order generated.

K8-I14 LIFECYCLE basis. Embodied anti-value includes a producer-attributed use-phase and end-of-life component, pre-charged to the producer via escrow at production and reconciled against actual use where measurable at cohort grain, so use-phase harm of intrinsically harmful goods is borne by the producer regardless of who performs the final consumption act and even where no business-side flow exists at the point of harm.

K8-I15 SAME-TICK is a PROVISIONAL FREEZE. Every same-tick anti-value booking against a firm's standing or escrow is a reversible provisional debit or freeze (soft-rung priced_debit) with SUSPENSIVE effect on contest per A18-I34: accrual suspends once the firm contests and is restored with interest if the finding is not sustained; no forfeiture or continuing debit accrues before an A6 attested or confirmed finding or the close of an uncontested attestation window (A18-I6). The over-coercion flank is guarded as strictly as the evasion flank.

K8-I16 Beneficial-owner and provenance verification. At any gated production authorization the beneficial-owner graph is positively verified against independent asset-discovery data (R1) and backed by a forfeitable stake, not accepted on self-declaration; unverifiable control links default to the high-scrutiny class until attested. Critical-production single-point-of-failure and capacity concentration (interface to C4) are a systemic-effect subject and route to COMP.

### Protocols
K8-P1 Run accounting. On run close, compute inputs (V3), created value, and embodied anti-value on a lifecycle basis (K8-I2, K8-I14); resolve the run_controller to its beneficial-owner graph; write the provenance record (EPCIS) and the mass-balance reconciliation (K8-I4).

K8-P2 Externality pricing and escrow. Price the measured V4 residual through the MVAL overlay and debit externality escrow, sized per K8-I12. The debit is booked same-tick as a PROVISIONAL freeze under K8-I15; no forfeiture accrues before an A6 finding or an uncontested window (cross-cite A18-I34, A18-I6).

K8-P3 Downstream reconciliation. Carry embodied anti-value on each output; at each downstream M3 transaction charge only the measured residual minus what was already charged upstream, on the running ledger (K8-I4); settle any exiting or untraceable residual back to the run_controller (K8-I5).

K8-P4 Import parity. At import compute the overlay charge on the good's attested (or defaulted-high) embodied anti-value, credit only a verified equivalent origin charge, and levy the difference on the importing controller (K8-I6).

K8-P5 Conformance and recall. Gate gated-class goods on a valid conformance_release before market eligibility; on a defect or emergent harm run the recall X1 chain and route the safety consequence per the split in K8-I7 (K8-I9).

K8-P6 Displacement attribution and discharge. Attribute displacement at run and sector grain (K8-I11), stand up the delivered capability floor to the identified cohort, and treat the charge as discharged only on delivery of the floor, not on routing to the commons.

### Lifecycle and edge cases
- Joint and by-products: allocation cannot dump the residual on the lowest-value output (K8-I5); a waste-to-product reclassification carries the disposal-contingent tail (K8-I10).
- Offshored run re-entering the polity: full residual at import to the importing controller (K8-I6); origin attestation is a credit only against a verified charge.
- Toll and contract manufacturing: commissioning firm jointly and severally liable irrespective of concealment (K8-I13).
- Exiting or consumed output: residual reverts to the run_controller (K8-I5); use-phase harm is pre-charged to the producer (K8-I14).
- New-firm bootstrap: sector-default TrackRecord, capped escrow fraction, so entry is not walled off (K8-I12).
- Diffuse sub-threshold displacement: sector-level apportionment books the harm no single run is pivotal for (K8-I11).

### Interfaces
- C1 and FVAL: the run_controller and its externality residual feed the firm value account; K8 supplies the V4 anti-value and the embodied-anti-value ledger.
- MVAL: the uniform overlay function, cohort-grain (S5) sensing, and the residual-pricing doctrine; K8 does not set prices.
- C2: market-eligibility gate (conformance_release) and the market booking kept distinct from the Ae booking.
- C3 and C4: labor input and displacement; critical-production resilience and concentration.
- D4, F6, F5, M1, M3: ecology, emissions, waste, material and good primitives.
- A18 and R1: escrow_bond primitive (A18-I45), suspensive contest (A18-I34, A18-I6), criminal routing (A18-I2, A18-I3, A18-I44), and independent asset-discovery for owner verification.
- C5 settlement and escrow (the ledger that holds externality_escrow and settles the anti-value debit) and C6 routing (the rail that routes the recovered charge to the commons or the delivered floor) are defined here at first reference; the counterfactual competitive benchmark is C7 appraisal and valuation as used in Property-and-Ownership.md.

### External bindings
ISA-95 (production and MES semantics), GS1 and EPCIS (provenance and custody occurrences), GHG Protocol (emissions accounting for the F6 residual). Lifecycle-assessment conventions inform the use-phase and end-of-life component (K8-I14) without importing any external permit-to-pollute logic.

### Open questions
1. The escrow harm-capacity floor and fraction ceiling (K8-I12) need a mandate-set schedule per harm class; the conservative interim rule is a sector-default TrackRecord with a worst-case floor for high-harm and latent classes.
2. Use-phase reconciliation granularity (K8-I14): how finely actual use is measured back to the producer where only cohort-grain consumption data exists, versus settling on the escrowed pre-charge.
3. Cross-jurisdiction displacement attribution (K8-I11) depends on data-sharing reach outside the polity; the fallback is default-high attribution to the run_controller with a rebuttal burden.
4. Border-parity origin-charge verification (K8-I6) requires a recognized equivalence standard for foreign anti-value charges; until one exists, only a demonstrably paid, itemized equivalent charge earns the credit.

## C2 market and exchange: clearing and price formation

### Purpose

The market venue exists to clear voluntary $-denominated orders and to reveal price through open exchange. The market clears; the state never sets a transaction price. What the state prices is the RESIDUAL: the externality anti-value a trade carries (K8, MVAL) and the monopoly rent a pricing-power holder extracts (C1, COMP), applied through one published, uniform overlay, never a per-firm verdict. Both flanks are catastrophic here. A rigged or cornered book corrupts the very price signal the residual pricing depends on; an over-restrictive venue that criminalizes ordinary aggressive or penetration pricing strangles legitimate enterprise. C2 governs the clearing surface so that price discovery stays honest and free competition stays lawful, while the residual is caught exactly once and only where power or harm is demonstrated.

### Object model

- order: {subject, side, limit_price ($), quantity, controller (S1), beneficial_owner (verified per C35 / R1), denomination = $}. Every price and settlement field is $-denominated.
- book / venue: a sealed, frequent batch auction over a subject, run by a venue steward as a stewarded commons (not a per-participant state read).
- clearing_price: a single uniform $ price per batch interval.
- embodied_anti_value: the residual carried on the subject for disclosure and downstream reconciliation (a running ledger, the money analogue of the K8 mass balance), never a re-chargeable full re-debit.
- benchmark_state (C7 appraisal/valuation-and-benchmark): the counterfactual competitive price and the independently attested efficient-cost base feeding the rent decomposition; never the firm's own reported price or self-reported cost.
- market_power_state: {pivotal: bool (non-substitutable for some cohort), concert_share: fraction} governing own-price exclusion.
- strategic_demand: a $-denominated demand order (subsidy, procurement bid, or A7 incentive payment) that clears like any $ order; it carries no Ae consideration.
- conformance_release: the K8 pre-market eligibility token required for gated classes.
- C5 (settlement/escrow) and C6 (routing) are defined here at first reference: C5 is the settlement and escrow-withhold rail; C6 is the routing of a booked residual to remediation, commons or cohort restitution.

### Invariants

- C2-I1 (clears, does not price): the venue matches orders and reveals price; the state SHALL NOT set, cap or floor a transaction price. Residual pricing runs only through the published overlay. The interval between marginal cost and the competitive price is a protected free-competition band that carries neither a rent charge nor an offense (aligns C1, COMP).
- C2-I2 (dual booking, no double-charge): a trade MAY carry a residual anti-value debit (V4), but the money charge at any downstream transaction SHALL equal the measured residual minus what was already charged upstream, tracked on the embodied_anti_value running ledger, so the total charged across the whole supply chain never exceeds the run's measured total (C14; money analogue of K8-I4).
- C2-I3 ($-only settlement): every order's limit_price, clearing_price and settlement SHALL be $-denominated. An order that would settle to or draw consideration from the Ae ledger fails closed. Ae is booked-not-transferred, never consideration a buyer pays or a seller receives, and never converted to a price (Charter Art. 13; FVAL, MVAL). Civilizational position is the separate pure-Ae quantity net_Ae; the two rails never net.
- C2-I4 (batch-auction default): the default fair-access matching mechanism SHALL be frequent, discrete, uniform-price, sealed batch auctions, removing the intra-interval latency advantage without imposing a single-sequencer throughput ceiling. Continuous matching is not the default.
- C2-I5 (integrity offenses): spoofing, wash trading, layering, front-running, predatory manipulation and cornering are offenses. Cornering is an offense WHENEVER it corrupts price discovery; breach of an essential-access floor is an aggravating factor, not the trigger (C8). A concerted-effect-without-agreement offense is added (C6): public advance signaling of intended prices or output, information exchange enabling coordination, and deployment of shared or rival-price-ingesting pricing algorithms are all price-signal manipulation regardless of any proven agreement.
- C2-I6 (sealed venue read): continuous order-level pattern surveillance is a venue-steward sealed duty emitting only flagged offense referrals. Any order-flow read beyond the published projection, and any resolution of a flag to a named participant or beneficial owner, SHALL require an S2 judicial access contract through an A6 case. The state senses at cohort grain (S5), never a general per-participant order read (C31).
- C2-I7 (conformance gate at market): a gated-class order (life-safety M4 food, M5 medicine and peers) SHALL fail closed at submission unless a valid, unexpired conformance_release is referenced and no open recall exists for the subject. Market-eligibility is verified as a listing precondition, not post-hoc (C33).
- C2-I8 (own-price exclusion, operable default): a holder's own price SHALL be excluded from its own benchmark whenever it is pivotal OR its concert-aggregated share exceeds a stated fraction (default 40 percent), uniform and published with a review clause. This default governs from activation and remains in force until a mandate parameter supersedes it; the machinery is never inoperable while calibration is pending (C4).
- C2-I9 (strategic demand on the $ rail): all market-clearing strategic demand SHALL route on the $ rail and clear like any $ order. Any retained Ae-credit is strictly a booked-not-transferred standing credit to the serving firm's OWN Ae account, never order consideration (C11). The concentration ceiling extends to the demand side: any single mission's share of a sector's demand field is capped, and demand above the ceiling SHALL be split across independent buyers or tendered so the market still discovers supply and price (guards monopsony and planning creep).
- C2-I10 (border externality-parity): any imported good, finished or intermediate, SHALL be charged at import the difference between its MOS-overlay embodied anti-value and the anti-value price demonstrably paid in the origin jurisdiction, by the same published overlay function on attested (or defaulted-high) embodied anti-value. "Priced abroad" is a credit only against a verified equivalent charge, never a waiver; offshoring a run whose output re-enters the polity books the full residual at import to the importing controller, tracing to the beneficial owner (C13).
- C2-I11 (provisional, suspensive): every same-tick residual or manipulation booking against a firm's standing or escrow is a reversible provisional debit or freeze (soft-rung priced_debit) with SUSPENSIVE effect on contest per A18-I34. Accrual suspends once the firm contests and is restored with interest if the finding is not sustained; no forfeiture or continuing debit accrues before an A6 attested or confirmed finding, or the close of an uncontested attestation window (A18-I34, A18-I6). This is the over-coercion guard (C20).

### Protocols

- C2-P1 (submission validation): on submission verify (1) S1 control and the positively verified beneficial-owner graph (C35 / R1), unverifiable control links defaulting to the concentration-summed high-scrutiny class; (2) $ denomination, else fail closed per C2-I3; (3) for a gated-class subject, a valid unexpired conformance_release and no open recall, else fail closed per C2-I7; (4) market_power_state for own-price exclusion per C2-I8.
- C2-P2 (batch clearing): collect sealed orders over the interval, clear at a single uniform $ price, then reveal. For any multi-venue subject, extend the sealed-reveal sequence to a cross-venue consolidated tape so no watcher can front-run a reveal on another venue (C32).
- C2-P3 (residual booking): at clearing, book the residual as a provisional freeze under C2-I11, charging only measured residual minus already-charged upstream on the embodied_anti_value ledger (C2-I2), and route the charge via C6 (remediation, commons or cohort restitution) only after finality per A18-I34.
- C2-P4 (sealed integrity surveillance): the venue steward runs continuous order-level pattern surveillance under seal for the C2-I5 signatures, emitting only flagged offense referrals; naming a participant or beneficial owner from a flag requires an S2 access contract through an A6 case (C31).
- C2-P5 (strategic-demand clearing): clear strategic demand on the $ rail per C2-I9; where a mission's share would exceed the demand-field ceiling, split across independent buyers or tender before clearing.

### Lifecycle and edge cases

- State as buyer: the state expresses demand only as $-denominated subsidies, procurement bids or A7 incentive payments that clear like any $ order. It never pays or receives an Ae-credit as consideration; a retained Ae-credit is a booked-not-transferred credit to the serving firm's own Ae account.
- Import of a finished or intermediate good: the border transaction books the parity charge under C2-I10; a foreign attestation is a credit only against a verified equivalent origin charge.
- Exiting output: any embodied anti-value allocated to an output that leaves traceability or is not downstream-chargeable reverts to and settles against the run controller at production (C15), so a residual cannot be parked on an exiting or low-value output.
- Recalled or non-conformant gated good: fails closed at submission per C2-I7; not caught only downstream by recall.
- Contested booking: suspends and reverses per C2-I11; a sustained finding routes the settled charge via C6.

### Interfaces

- C1, COMP: consume the free-competition band (C2-I1), the own-price-exclusion state (C2-I8) and the C7 benchmark for the rent and predation lines; predation is a below-cost plus recoupment test, not below cost-plus-normal-return.
- K8, MVAL: the embodied_anti_value ledger, the dual-booking reconciliation (C2-I2) and the overlay function.
- C5 (settlement/escrow), C6 (routing), C7 (appraisal/valuation-and-benchmark) as defined above; C7 is the benchmark/valuation code (as Property-and-Ownership.md uses it), distinct from any legacy property code.
- S2 / A6: judicial access to resolve a sealed flag; S5: cohort-grain sensing.
- A18: offense classes, the A18-I34 / A18-I6 suspensive-contest rule, and beneficial-owner attribution.

### External bindings

- Charter Art. 13 ($-rail non-convertibility of Ae), Art. 4 and Art. 6 (safety and cohort-floor routing behind the conformance gate), Art. 10 (concentration ceiling extended demand-side).
- A7 incentive payments as a lawful $-rail demand instrument.
- A18-I34, A18-I6 (suspensive contest and no unadjudicated continuing debit).
- R1 / C35 asset-discovery for beneficial-owner verification at gated acquisition.

### Open questions

- Batch-auction interval length per subject class: short enough for genuine price discovery, long enough to erase the latency race; calibration is a mandate parameter.
- The 40 percent own-price-exclusion default is operable now; the exact fraction and the pivotal test remain open to mandate refinement under the published review clause.
- Cross-venue consolidated-tape latency and governance for subjects listed on many venues.
- Demand-field share ceiling calibration per sector before a mission must split or tender.

## Markets, civilizational value and the externality residual

### Purpose

The market clears and discovers $ prices; the polity never sets a transaction price. On top of every cleared flow the state applies one uniform, published overlay that prices the two things the price signal cannot internalize on its own: the externality residual (embodied anti-value) and the monopoly rent (the margin attributable to demonstrated pricing power). Civilizational value is booked on a ten-axis Ae vector that is never converted to a price. The market is a diagnostic of citizen-revealed value, never a target the state optimizes by fiat. Both flanks are catastrophic: an under-priced residual or an unchallenged monopoly on one side, and an over-charged legitimate enterprise that strangles competition, entry and beneficial production on the other.

### Object model

- externality_overlay: the published function O(flow) mapping attested embodied anti-value to a $ charge. Parameters are axis_weights (the V5 state frame), strength_dial (E4) and market_power_threshold. Uniform across all flows; carries no per-firm term.
- residual_ledger: a running supply-chain ledger recording each run's measured total residual, embodied anti-value carried on each output, and cumulative $ already charged upstream.
- benchmark: the counterfactual competitive price and cost basis (C7, appraisal, valuation and counterfactual benchmark), built on independently attested efficient cost, never the firm's reported cost.
- civ_value_vector: the ten-axis Ae position; per-axis net_Ae is booked, never collapsed into a scalar for floor decisions.
- net_Ae: created_value(Ae) minus anti_value(Ae) plus positive_spillovers(Ae), a pure-Ae quantity held per axis. profit_$ is a separate, never-summed $ field.
- strategic_demand: a $-denominated order (subsidy, procurement bid or A7 incentive) that clears like any $ order.
- spillover_credit: an attested, additional, revaluable positive-Ae booking paired with a matched $ Pigovian subsidy.
- import_parity_charge: the border residual charge on imported finished or intermediate goods.
- theta: the participation-condition diagnostic signal (worse-off cohort), a first-class diagnostic, not a charge.

Defined at first reference for citation resolution: C5 (the settlement and escrow primitive), C6 (the routing primitive), C7 (appraisal, valuation and counterfactual benchmark, as Property-and-Ownership.md uses the code).

### Invariants

MVAL-I1 The market clears $ prices and the state SHALL NOT set, cap or fix any transaction price. The overlay attaches only after clearing and prices the residual and the rent, never the exchange itself (C6 routing, C7 benchmark).

MVAL-I2 Externality residual dual-booking SHALL run on a no-double-charge ledger, the money analogue of the K8 mass balance: embodied anti-value rides the good for disclosure and to catch residual not yet charged upstream, and the $ charge at any downstream A2A transaction equals the measured residual minus what was already charged upstream, so total charged over the whole supply chain never exceeds the run's measured total (K8-I4, C2-I2).

MVAL-I3 Border externality-parity: any imported good, finished or intermediate, SHALL be charged at import the difference between its MOS-overlay embodied anti-value (computed by the same published O on attested, or defaulted-high, embodied anti-value) and the anti-value price demonstrably paid in the origin jurisdiction. "Priced abroad" is a credit only against a verified equivalent charge, never a waiver. Offshoring a run whose output re-enters the polity books the full residual at import to the importing controller, tracing to the beneficial owner (K8-I2).

MVAL-I4 Lifecycle basis: embodied anti-value SHALL include a producer-attributed use-phase and end-of-life component (lifecycle, not gate-to-gate), pre-charged to the producer via escrow (C5, K8-I12) at production and reconciled against actual use where measurable, so use-phase harm of intrinsically harmful goods is borne by the producer regardless of who performs the final consumption act. Any embodied anti-value allocated to an output that leaves traceability or is not downstream-chargeable SHALL revert to and settle against the run controller at production.

MVAL-I5 The overlay is automatic, published and uniform, applied identically to all flows; it SHALL carry no per-firm verdict. Anti-capture rests on uniformity plus MVAL-I6, not on discretion.

MVAL-I6 Overlay parameters (axis_weights, strength_dial, market_power_threshold) SHALL be bound by the same multi-source, staked, revaluable, no-single-organ, published-change-provenance and contestation discipline as overlay inputs; the parameter-setting organ SHALL be structurally separated from every organ that receives the resulting charges (the commons rent fund and the citizen dividend). A sector's share of influence over a weight that materially reduces its own anti-value charge is flagged and rebuttably presumed capture (mirrors the COMP anti-revenue rule at the parameter layer).

MVAL-I7 Counterfactual benchmark: the cost basis feeding any cost-plus-normal-return counterfactual SHALL be independently attested (audited, peer efficient-frontier, or best-available-technology cost model), never the firm's reported cost; affiliate or acting-in-concert inputs are re-priced at arm's length or the affiliate's costs are consolidated, recursing the own-price exclusion up the supply chain; above-benchmark input prices, related-party compensation above a published norm, and rent capitalized as asset carry are stripped from the cost base, and unexplained cost inflation is presumptive rent concealment (A18) with the burden on the firm. A firm's measured cost or efficiency advantage is credited as created value inside the counterfactual, and innovation-driven super-normal returns are time-limit-protected (a patent-style horizon) before any rent charge attaches, so rent equals the pricing-power margin alone. The interval between marginal cost and the competitive price is a protected free-competition band carrying neither a rent charge nor an offense (FVAL benchmark, COMP-I3, C1-I12).

MVAL-I8 Market-power threshold default (never null): from activation, a firm's own price is excluded from its own benchmark whenever it is pivotal (non-substitutable for some cohort) OR its concert-aggregated share exceeds 40 percent, uniform and published with a review clause; a mandate parameter MAY supersede but the machinery is never inoperable while pending (C2-I9, COMP-I3).

MVAL-I9 Civilizational position is a single pure-Ae quantity, net_Ae = created_value(Ae) minus anti_value(Ae) plus positive_spillovers(Ae), computed per axis; "market_revenue" in the civ-value formula denotes the Ae credit for revealed created value, never the $ revenue figure. profit_$ is a separate $ field that is never summed with net_Ae; the two bookings never net and Ae is never converted to a price (unified with C1-I6 and FVAL-I3, Charter Art. 13).

MVAL-I10 No cross-axis netting into floors: anti-value on any capability-floor or hard-limit axis (A9 dignity, Art. 6 cohort floor, Art. 4 safety, depletion beyond a regeneration bound) SHALL NOT be offset by credits on other axes; a floor-axis breach routes to the A18 ladder regardless of a positive aggregate net_Ae. Spillover credits raise standing only within non-floor axes; the standing or access consequence triggers on a per-axis threshold breach, never an undefined scalar over the vector.

MVAL-I11 Strategic demand SHALL route on the $ rail: $-denominated subsidies, procurement bids or A7 incentive payments that clear like any $ order (C2-I3). An "Ae-credit", if retained, is strictly a booked-not-transferred standing credit to the serving firm's own Ae account, never consideration a buyer pays or a seller receives; Ae-credit is removed from the order-clearing path everywhere. Any single mission's share of a sector's demand field is capped and the concentration ceiling extends to a demand-side or monopsony position; where strategic demand would exceed the ceiling it SHALL be split across independent buyers or tendered so the market still discovers supply and price.

MVAL-I12 Spillover-credit discipline: a credit is booked only for demonstrated additional value that would not have occurred absent the firm (no baseline or state-funded activity), multi-source and revaluable, with the burden on the firm; materially overstated positive-spillover claims are an A18 concealment-class offense carrying the same clawback as anti-value concealment; net self-originated credit against a firm's own anti-value is capped. Credited positive spillovers draw a matching Pigovian subsidy from the commons rent fund on the same $ rail and timescale that harmful production is charged; the Ae credit stays non-convertible, the paid reward is a separate $ flow.

MVAL-I13 Priceable-residual versus floor-breach classification: any anti-value touching a capability floor (A9 dignity, Art. 6 cohort floor, Art. 4 safety, irreversible or ecological-tipping harm) is presumptively non-priceable, with the burden on the FIRM to prove it a bounded, reversible, priceable residual; repeated same-class residual charges above a threshold escalate a nominally-priceable harm into floor-breach review, closing the pay-to-continue license (C1-I11, A18-I2).

MVAL-I14 Theta is a diagnostic, not a freestanding charge: bookable anti-value from a theta signal is conditioned on the residual being an independently measured V4 harm and/or a measured Art. 6 cohort-floor breach; otherwise a theta breach is the C1 diagnostic (overlay recalibration or A7 incentives), never a freestanding priced charge or a ban by itself (C1-I11, A18-I2).

MVAL-I15 Theta small-cohort path: a complaint- or floor-breach-triggered S2 or A6 judicial-access path MAY authorize measuring theta and the residual for a specifically identified small cohort below the k-anonymity floor, so smallness confers no firm immunity; the k-floor protects privacy against untriggered surveillance, never a firm against identified-harm inquiry.

### Protocols

MVAL-P1 Overlay application. At each cleared flow: (1) read attested embodied anti-value and the residual_ledger; (2) compute the $ charge as measured residual minus already-charged upstream (MVAL-I2); (3) book it same-tick as a reversible provisional debit or freeze (soft-rung priced_debit, C5) with SUSPENSIVE effect on contest per A18-I34: accrual suspends once the firm contests and is restored with interest if the finding is not sustained, and no forfeiture or continuing debit accrues before an A6 attested or confirmed finding or the close of an uncontested attestation window (A18-I34, A18-I6).

MVAL-P2 Rent decomposition. Where a firm is above the MVAL-I8 threshold, exclude its own price, build the counterfactual on the MVAL-I7 attested efficient-cost benchmark, credit its measured efficiency and protected innovation returns as created value, and charge only the residual pricing-power margin as rent, routing it to the commons rent fund (C6). The concentration charge and the rent overlay SHALL NOT both charge the same captured-minus-created value.

MVAL-P3 Strategic-demand routing. Express strategic demand as a $ order and clear it on the same Value-Flow ledger as citizen and A2A demand; apply the monopsony ceiling and split or tender any position above it (MVAL-I11). Any retained Ae-credit posts only to the serving firm's own Ae account and never enters settlement.

MVAL-P4 Spillover assessment and symmetric reward. Test each spillover claim for additionality and attestation (MVAL-I12); on pass, book the non-convertible Ae credit and route a matching $ Pigovian subsidy from the commons rent fund (C6) on the same timescale as the harm charge; on material overstatement, route to the A18 concealment ladder with clawback.

MVAL-P5 Finality and realization. Honest and non-gross residual bookings are final on window close; concealed or intentional bookings are perpetually clawback-eligible regardless of size; honest but gross-and-latent bookings are revaluable within a bounded long window (a mandate parameter) with escrow as the honest firm's pre-funded protection; perpetual liability never attaches to honesty alone. Any realization of accumulated-but-uncharged rent (asset sales, spin-offs, IP transfers or licenses, liquidation distributions), not only equity-share sales, triggers pricing of the unearned component (realization value minus attested cost basis minus already-charged rent) before the holder keeps the gain (C1-I8).

### Lifecycle and edge cases

- Imported finished good: charged at import under MVAL-I3 by the same overlay; a foreign attestation of harm "accounted for" is a credit only against a verified equivalent charge.
- Offshored run re-entry: the full residual books at import to the importing controller, tracing to the beneficial owner (MVAL-I3).
- Use-phase and end-of-life harm: pre-charged to the producer via escrow and reconciled against measured use (MVAL-I4); consumption harm measurable at cohort grain books against the good's carried residual, not lost for want of a business-side flow.
- Exit of traceability: residual on an untraceable or non-chargeable output reverts to the run controller (MVAL-I4), so it cannot be parked on an exiting output.
- Waste-to-product laundering and toll or contract manufacturing: the disposal-contingent tail and joint-and-several commissioner liability are booked in K8; MVAL prices the residual they surface on the same no-double-charge ledger (MVAL-I2).
- State as buyer: routes on the $ rail under the monopsony ceiling (MVAL-I11); the state never attaches a price via Ae.
- Theta below the k-anonymity floor: reachable only through the MVAL-I15 triggered judicial path.

### Interfaces

- C1 (firm): net_Ae and profit_$ separation, theta diagnostic, threshold (C1-I6, C1-I11).
- FVAL (firm value): shared benchmark, externality escrow sizing (C5, K8-I12), finality (FVAL-I3).
- K8 (production): mass balance, embodied anti-value, use-phase, waste-to-product, toll manufacturing (K8-I2, K8-I4, K8-I12).
- C2 (market): $-only settlement, sealed venue surveillance, batch auctions, conformance gate (C2-I2, C2-I3).
- COMP (competition): rent ceiling, concentration on power not size, systemic pre-funding bond via A18-I45 and K8-I12 (not M3), tacit and algorithmic collusion.
- A18 (accountability): the ladder, suspensive contest (A18-I6, A18-I34), personal attribution (A18-I45), concealment class.
- A6 / A7 / S2 / S5: case and judicial access, incentive payments, judicial-access contract, cohort-grain sensing.
- V4 / V5 / E4: harm frame, state-frame weights, strength dial.
- R1: independent asset-discovery data backing beneficial-owner verification at gated acquisitions.

### External bindings

- Charter Art. 4 (safety), Art. 6 (cohort floor), Art. 10 (concentration ceiling), Art. 12 (worse-off diagnostic), Art. 13 (Ae non-convertibility); A9 dignity floor.

### Open questions

1. Calibration cadence and evidentiary standard for revising the 40 percent default threshold and the axis weights once the mandate machinery is live, without reopening the capture window (MVAL-I6, MVAL-I8).
2. Precision of producer-attributed use-phase and end-of-life measurement for heterogeneous goods, and the escrow reconciliation lag it implies (MVAL-I4).
3. Minimum attestation quality for origin-jurisdiction anti-value pricing before the defaulted-high import charge applies, and dispute handling with non-MOS jurisdictions (MVAL-I3).
4. The bounded long-window length for honest-but-gross-and-latent revaluability, pending a mandate parameter (MVAL-P5).

## Competition, market power, anti-abuse and systemic risk

### Purpose

This section governs competition, market power, anti-abuse (collusion, price-signal manipulation, predation, cornering, exclusionary conduct, killer acquisitions) and systemic risk on the economy-production surface. Two failures are equally catastrophic and this section is engineered against both flanks: market abuse that lets a dominant actor extract rent, foreclose rivals, or hold the polity hostage; and over-restriction that criminalizes legitimate aggressive pricing, efficiency, scale, or entry. Power itself is never an offense. The overlay charges only the margin attributable to demonstrated pricing power, prices only the residual the market cannot, and reserves the hard A18 ladder for culpable abuse. The efficient firm faces the rent overlay, never coercion; the abusive firm faces both.

### Object model

- `market_power_assessment`: per subject and cohort; fields `pivotal` (non-substitutable for some cohort, boolean), `concert_share` (concert-aggregated share of the relevant frame), `above_threshold` (derived), `benchmark_ref` (C7 counterfactual competitive benchmark), `rebuttal` (pass-through, contestability, all-frames-improving evidence).
- `concentration_position`: concert-aggregated supply-side holdings AND demand-side (monopsony) position across markets, keyed to the positively verified beneficial-owner graph; carries `power_component` and `systemic_centrality`.
- `collusion_case`: `mechanism` (signaling channel, information exchange, shared or rival-ingesting algorithm), `confidence`, `named_owners`, `presumption_state`.
- `predation_case`: `price_vs_avoidable_cost`, `recoupment_feasible`, `foreclosure_effect`.
- `acquisition_review`: `acquirer_power`, `target_nascency`, `future_constraint_loss`.
- `systemic_node`: `cascade_estimate` (independently set), `feasible_bond`, `essential_function_unit`, `resolution_plan`.
- `benchmark` denotes the C7 appraisal, valuation and counterfactual-benchmark primitive (price observations, indices, efficient-frontier cost models); its cost basis is defined in COMP-I3, never the subject's own ledger.

### Invariants

- COMP-I1: Market power, firm size, holdings and systemic centrality are NEVER an offense in themselves. Consequences attach only to demonstrated pricing power, exclusionary conduct, manipulation, or un-bondable systemic exposure. The efficient winner that improves all frames faces the rent overlay and systemic-resilience duties, never coercion (both-flanks guarantee).
- COMP-I2: The market-power threshold SHALL be operable from activation and never null. A firm's own price is excluded from its own C7 benchmark whenever it is `pivotal` OR its concert-aggregated share exceeds a stated fraction (default 40 percent), applied uniformly, published, with a review clause. A mandate parameter MAY supersede this default but the machinery SHALL remain operable while any recalibration is pending.
- COMP-I3: The cost basis feeding any cost-plus-normal-return counterfactual SHALL be independently attested (audited, peer-efficient-frontier, or best-available-technology cost model), NEVER the firm's self-reported cost. Inputs from affiliates or acting-in-concert parties are re-priced at arm's length or the affiliate's costs consolidated, recursing the own-price exclusion up the supply chain. Above-benchmark input prices, related-party compensation above a published norm, and rent capitalized as asset carry are stripped from the cost base. Unexplained cost inflation is presumptive rent concealment (A18) with the burden on the firm to justify each cost line.
- COMP-I4: The RENT ceiling and the PREDATION floor are DIFFERENT lines and SHALL NOT collapse to a single lawful price. The rent ceiling charges only the margin attributable to demonstrated pricing power (price held above the competitive level), not the whole gap between observed and normal return. The interval between marginal cost and the competitive price is an explicitly protected free-competition band carrying neither a rent charge nor an offense.
- COMP-I5: The PREDATION offense is price below avoidable or marginal cost combined with a recoupment-feasibility test (the actor SHALL have power to recoup); it is never triggered by a price merely below cost-plus-normal-return. "Sustained" is not required: a brief targeted below-cost burst with a recoupment path qualifies. Limit-pricing and non-price foreclosure by an above-threshold actor are within scope.
- COMP-I6: A firm's measured cost or efficiency advantage is credited as created value inside the counterfactual, so rent equals the pricing-power margin, never the efficiency gain. Innovation-driven super-normal returns are time-limit-protected (a patent-style horizon, mandate parameter) before any rent charge attaches. The overlay rewards the source of the advantage; it never confiscates it.
- COMP-I7: The concentration charge attaches to unrebutted pricing power or systemic centrality, NEVER to raw size. A firm that rebuts power (demonstrated cost pass-through, contestable market, all frames improving) faces only systemic-resilience duties (C5 escrow bond, resolution plan), not a size charge. The rent overlay (COMP-I4) and the concentration charge SHALL NOT both charge the same captured-minus-created value.
- COMP-I8: Collusion offenses include price-fixing, market allocation and bid-rigging AND an explicit concerted-effect-without-agreement offense: public advance signaling of intended prices or output, information exchange enabling coordination, deployment of shared or rival-price-ingesting pricing algorithms, and all price-signal manipulation, each an offense regardless of any proven agreement.
- COMP-I9: Statistical or correlated-conduct signals alone SHALL NOT ground a hard rung against a natural person, but the individualized act is located in the DEPLOYMENT decision: a beneficial owner who deploys or licenses a pricing algorithm producing sustained coordinated supra-benchmark pricing commits a provable individualized act, personally attributable under A18-I45. Above-threshold actors carry a mandatory disclosure and auditability duty for pricing algorithms. Once cohort-level collusion is established to high confidence AND a plausible coordination mechanism is identified, a rebuttable presumption shifts the burden to the named beneficial owners to prove genuinely independent conduct; the unrebutted presumption is the individualized basis for the hard ladder.
- COMP-I10: Acquisitions by an actor above a market-power or systemic threshold of an actual or potential competitor SHALL face a forward-looking test for loss of nascent or future competitive constraint, independent of current-share aggregation, with the burden on the acquirer to show the target is not a nascent competitor.
- COMP-I11: Cornering is an offense whenever it corrupts price discovery. Breach of an essential-access floor is an aggravating factor, not the trigger.
- COMP-I12: Once a foreclosure effect is shown against an actor above the market-power threshold, the burden shifts to that actor to prove the efficiency or genuine-integration justification AND the unavailability of a less-foreclosing alternative. Absent that showing the conduct is classified exclusionary.
- COMP-I13: The concentration ceiling extends to demand-side and monopsony position. Any single mission's or organ's share of a sector's demand field is capped; where strategic demand would exceed the ceiling it SHALL be split across independent buyers or tendered so the market still discovers supply and price. Strategic demand clears only on the $ rail (see C11 doctrine); no Ae credit is ever order consideration.
- COMP-I14: The beneficial-owner graph at every gated acquisition SHALL be positively verified against independent asset-discovery data (R1-I39) and backed by a forfeitable stake, not accepted on self-declaration. Unverifiable control links default to the concentration-summed high-scrutiny class until attested.
- COMP-I15: The non-priceable criminal class attaches to the culpable natural persons (whoever knew, directed, or recklessly enabled the offense, officer or owner or both) on individualized objective-corroborated evidence (A18-I9). Mere beneficial ownership triggers clawback of proceeds and standing loss regardless of culpability, but never criminal-class consequences absent culpable participation.
- COMP-I16: Systemic loss SHALL NOT be socialized. The shortfall waterfall is: draw the C5 escrow bond first (A18-I45, K8-I12), then personal beneficial-owner clawback (perpetual, piercing the S1 graph per A18-I45), then the sector mutualized systemic-escrow pool, and only a demonstrated-exhausted residual reaches a commons backstop that itself re-attaches as clawback. The cascade estimate is independently set, distributions and buybacks are barred while resolution is under-funded, and under-sizing is concealment. Centrality above a defined cascade threshold where no feasible bond can absorb the cascade is a HARD STRUCTURAL CAP (mandatory de-concentration, divestiture or split until residual cascade is at most the feasible bond), never a payable charge. A systemic firm in an essential class SHALL maintain a pre-committed, ring-fenced, transferable essential-function unit that continues the function through resolution without the firm's cooperation.
- COMP-I17: Essential-class access floors are funded from a standing commons reserve or citizen-dividend buffer that recovered charges REPLENISH, decoupling delivery from same-period recovery volume. A minimum coverage ratio makes the floor a first-charge obligation ahead of discretionary commons routing, never fixed by setting the market price.
- COMP-I18: The multi-source, staked, revaluable, no-single-organ, published-change-provenance, contestation discipline extends to the market-power threshold and the concentration parameters. The parameter-setting organ is structurally separated from every organ that receives the resulting charges (the C6 routing to the commons rent fund and the citizen dividend). A sector's share of influence over a parameter that materially reduces its own charge is flagged and rebuttably presumed capture.

### Protocols

- COMP-P1 (market-power assessment): compute `pivotal` and `concert_share` on the R1-verified beneficial-owner graph (COMP-I14); if above the COMP-I2 threshold, exclude the subject's own price from its C7 benchmark, construct the counterfactual on the COMP-I3 attested cost base, credit measured efficiency and protected innovation as created value (COMP-I6), and decompose captured-minus-created into the pricing-power margin.
- COMP-P2 (anti-abuse detection and ladder): venue-sealed surveillance emits flagged offense referrals only; resolving a flag to a named participant or beneficial owner requires an S2 judicial access contract through an A6 case. For collusion, establish cohort-level effect to high confidence and identify the coordination mechanism, then apply the COMP-I9 rebuttable presumption; unrebutted, route culpable persons to the A18 hard ladder (COMP-I15). Predation and exclusion are tested per COMP-I5 and COMP-I12.
- COMP-P3 (acquisition review): at every gated acquisition run the COMP-I10 forward-looking nascent-constraint test alongside the COMP-I7 concentration check, with acquirer burden; deny or require divestiture where future competitive constraint is lost, independent of current-share aggregation.
- COMP-P4 (systemic resolution): size the C5 bond to the independently-set cascade estimate; where no feasible bond covers the cascade, apply the COMP-I16 hard structural cap; on failure, run the COMP-I16 shortfall waterfall and continue the essential function through the ring-fenced unit.
- COMP-P5 (provisional booking): every same-tick concentration or rent charge is a reversible provisional debit or freeze (soft-rung priced_debit) with SUSPENSIVE effect on contest per A18-I34: accrual suspends once the firm contests and is restored with interest if the finding is not sustained. No forfeiture or continuing debit accrues before an A6 attested or confirmed finding or the close of an uncontested attestation window (cross-cite A18-I34, A18-I6).

### Lifecycle and edge cases

- New entrant: bootstraps at the sector-default TrackRecord, not worst-case; the concentration machinery reads sub-threshold entrants as non-dominant, so aggressive penetration pricing inside the protected free-competition band (COMP-I4) is never an offense.
- Efficient scale rebuttal: a large firm demonstrating pass-through, contestability and all-frames-improving faces only systemic-resilience duties (COMP-I7), never a size charge, and is protected from double-charge by the rent overlay.
- Concealed nominee or shell chain: fails COMP-I14 verification, defaults to the high-scrutiny concentration-summed class, and false declaration is an A18 offense.
- Sub-threshold cross-market capture: a single actor's aggregated capture of one dependent cohort across several small markets is a concentration or theta trigger independent of per-market share, so smallness of each market confers no immunity (debt-peonage and total-life capture route to the non-priceable A9 and A18 criminal class per the labor and capability-floor doctrine).
- Killer acquisition: near-zero present share does not clear COMP-P3; the acquirer bears the burden on the target's nascency.
- Monopsony creep: a strategic-demand position exceeding the COMP-I13 ceiling is split or tendered rather than allowed to set price and quantity.
- Un-bondable systemic node: cannot pay to retain centrality; it de-concentrates under COMP-I16 until residual cascade is at most the feasible bond.

### Interfaces

- C5 (settlement and escrow primitive), C6 (charge routing to the commons rent fund and citizen dividend), C7 (appraisal, valuation and counterfactual-benchmark primitive, as used in Property-and-Ownership.md) are cited at first reference here; the concentration and systemic bonds are the A18-I45 risk-proportionate escrow_bond and the K8-I12 production externality escrow (replacing the earlier dangling "M3 escrow_bond" citation), and RENT restoration_bond is used only where a physical commons is restored.
- A18 investigation and hard ladder (A18-I2, A18-I3, A18-I9, A18-I34, A18-I44, A18-I45, A18-I6); C1 (firm benchmark and displacement floors, C1-I11 theta-diagnostic); FVAL and MVAL (net_Ae doctrine, overlay parameters MVAL-I8, MVAL-I10); C2 (venue microstructure, sealed surveillance, conformance gate, cornering); K8 (production escrow, mass balance); R1-I39 (asset discovery); S-cluster (S1 graph, S2 access, S5 cohort grain); A6 case; A7 incentives.

### External bindings

- Charter Art. 4 (life and bodily integrity, criminal in-kind non-priceable ladder), Art. 6 (cohort floor, priced restitution plus licensed hard ladder), Art. 10 (concentration ceiling on power and centrality), Art. 12 (worse-off diagnostic), Art. 13 (Ae never priced or transferred).

### Open questions

- The default 40 percent share fraction and the pivotal test in COMP-I2 are conservative placeholders; the mandate SHOULD calibrate them per frame under the COMP-I18 discipline without ever suspending the machinery.
- The innovation-protection horizon in COMP-I6 (patent-style time limit) is a mandate parameter; its length and any sector variation remain to be set.
- The cascade threshold in COMP-I16 above which centrality becomes a hard structural cap rather than a bonded exposure needs an independently-set, published value per essential class.
- Whether tacit-collusion rebuttal under COMP-I9 should require a named coordination mechanism in every case, or admit a narrow class of algorithm-only convergence where the deployment act alone suffices, is unresolved.