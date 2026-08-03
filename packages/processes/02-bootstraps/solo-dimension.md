# Solo dimension: one Owner-Steward, four agents, the whole palette

Mira runs an independent consulting practice: strategy work for mid-size manufacturers, three to six live engagements at a time, no employees. She wants her practice model to be the thing she asks first when she needs to know what is true about her own business, and she wants her AI agents to work from that model rather than from her memory. So she declares the Solo/Minimal conformance profile (COMMON 6) and runs the shipped defaults unmodified (COMMON 9). What follows is one Dimension, one model, one human, four agents.

## The practice and its dimension

The Mastership Register (sources.yaml, mastered solely by MIR-1) is short, and nothing lives outside it, because mastership is declared and never inferred and no palette process operates on an undeclared dataset (IC-1):

- service catalogue, engagement records, method library, positioning notes: model-mastered, authored in place;
- invoices and payments: external-mastered, master her accounting SaaS, harvested by MIR-2 on a weekly cadence;
- calendar: external-mastered, master the calendar provider, harvested daily;
- the public service catalogue on her website: a write-back projection of the model-mastered catalogue, generated, marked do-not-edit, master named (Pattern M, published through ACT-7);
- the palette's own registers (grants, contracts, effectors, jobs, debt, consumers): model-mastered, and several of them security-critical (IC-4).

Two entries sit in the consumer register (CON-13): her own agents, and the quarterly client-facing report generated from the model. CON-13 is only recommended, but she treats it as core because she publishes, and without it the completeness of a CON-8 correction notice is unmeasurable.

She runs MIR-3 and MIR-5 and no MIR-4 subscriptions, which is the ordinary solo shape: cadence plus on-demand refresh at the moment of consumption, no event streams to keep alive.

## Day one: genesis (GOV-4)

Half a day with the conformant template. Nine steps, nine concrete artifacts.

1. The founding decision goes into the ledger (GOV-1): purpose, scope, conformance target Solo/Minimal, governing standard version (GOV-4 step 1).
2. She appoints herself Owner and Steward (GOV-3 step 1) and, before anything else exists, writes the succession skeleton: named executor, escrowed recovery material under the quorum rule, incapacity criteria, invocation procedure (GOV-3 step 4). The solo variant is blunt about why: without it the model dies with its human. Genesis does not proceed to activation without it (GOV-4 step 2).
3. The scaffold: BOOTSTRAP.md, manifest.yaml, an empty Mastership Register, the Event log, the well-known locations. The agent executes, she reviews each stage output at T2. Nothing in genesis runs at T3, because the tier ladder has no track record to draw on at birth (GOV-4 step 3).
4. The GOV-2 policy set instantiated from shipped defaults: Impact Matrix, approval matrix, lane criteria and the diff-based classifier, tier maps, gate configs, retention policy, decision SLAs, severity rubrics. She localizes exactly two things: the editorial size threshold, and the declared cooling period that stands in for the second human reviewer on GOV-2 policy acceptances (the GOV-2 solo variant), with the next peer engagement sampling every policy change made since the last one. For the rest of the security-critical class the second reviewer is a real other person: the CON-4 solo rule binds even here, satisfied by an external peer or the Auditor. Both localizations are recorded as diffs against the shipped default, visible as such to an Auditor; the manifest declares that everything else runs as shipped (GOV-4 step 4, COMMON 9).
5. Registers initialized and machinery declared (GOV-4 step 5), all of them empty on day one but existing:
   - the GOV-7 grant register, the GOV-8 credential inventory (references, never values), the GOV-3 role register, the CON-13 consumer register, the QSC-11 debt register;
   - the QSC-15 job registry, which is why there are no unregistered crons from day one;
   - the signal catalog (ACT-1), seeded with exactly one entry: the standing owner-directive class that covers novel T1 human-initiated actions without per-idea cataloging;
   - the effector register (ACT-3), seeded with three: the site publisher script, the invoicing API caller, and Mira herself as a human effector who explicitly accepts her own capability contract, because a person commanded is a person who agreed to be commandable (ACT-3 step 5).
6. Seed content by lawful paths only. Her existing engagement notes enter through CON-7 bulk import, which invokes MIR-1 before any byte moves; the invoicing mirror is declared in sources.yaml first, then harvested by MIR-2 under that entry. Genesis itself moves no content (GOV-4 step 6).
7. The first QSC-4 validation run, green through V2 at the declared target. This gate is unwaivable: activation on a red, waived or skipped first validation leaves every later audit without a clean baseline (GOV-4 step 7).
8. Registration in the Dimension registry, the identity a future FED-1 discovery would resolve (GOV-4 step 8).
9. The activation Event: model identity, standard version, conformance target, validation report reference, register states (GOV-4 step 9). Genesis closes, and its scaffold grants expire on their activation-bound TTL. The first QSC-6 pass verifies that zero genesis grants are still live.

## The agents and their contracts

Four agents, four Delegation Contracts, issued by her personally through CTX-9, the single System of Record for delegation (issuance and revocation are non-delegable in substance: an agent may draft the scope, she performs the act). Every contract names processes, steps, datasets, tier per step type, rate and impact limits, and an expiry, and every one carries the data-never-command clause (IC-3).

New pairings start at T1 or T2, T3 is earned, and the first N acts under any new or upgraded contract run one tier stricter than granted (CTX-9 step 3, the palette's single probation rule). Entry rights live in the CON-10 register by contract ID, never copied (CON-10 step 4). Each agent and each pipeline holds a real scoped GOV-7 grant with a TTL, minted from the register and never before it, because otherwise QSC-6 has nothing true to audit. Liveness is validated at the gate at act time, never honored by the agent (IC-5).

| Agent | Work | Tier |
|---|---|---|
| Scribe (entry) | CON-1 registration and acknowledgment; the editorial fast lane end to end (COMMON 7) | T3 |
| Scribe | CON-1 classification and routing; CON-4 pre-review as the second pair of eyes | T2 |
| Harvester | MIR-2 for registered, previously proven pipelines; MIR-3 steps 1 to 5 and 7 | T3 |
| Harvester | first run of any new or changed MIR-2 pipeline; MIR-3 step 6 (downgrade to status declared) | T2 |
| Warden (sweep) | MIR-7 steps 1 to 4; QSC-2 mechanical checks; QSC-9 checks and anchoring; QSC-6 diffing; QSC-15 registry ops and meta-monitoring; MIR-8 threshold flagging | T3 |
| Warden | MIR-7 step 5 mechanical resolution; QSC-6 revocation of benign excess; QSC-11 remediation drafting; MIR-8 hard-block proposals | T2 |
| Warden | MIR-7 step 6 escalation; MIR-8 release; QSC-6 expansions (proposes, she approves each act) | T1 |
| Clerk (governance) | GOV-1 decision-file assembly and SLA tracking; GOV-7 registration and expiry sweeps; QSC-11 register hygiene; CTX-1 extraction; CTX-10 session bootstrap | T3 |
| Clerk | GOV-1 options drafting; GOV-8 rotation batches (references only, never secret values) | T2 |

No agent holds a write path to its own trail: action, read and dispatch logs are emitted by the gate, channel and runtime (IC-6). That is what makes the quarterly QSC-7 audit worth running.

## The standing setup: exactly three obligations

COMMON 6 bounds a Solo/Minimal operator to three standing obligations, and any palette change that would add a fourth is a re-adjudication, not a local edit. Hers are these.

### The declared continuous monitors

Five, all registered as QSC-15 standing jobs with independent, cross-watched heartbeats:

- the MIR-6 freshness monitor, computing freshness_state per mirrored dataset and warning before the staleness limit is crossed (MIR-6 steps 3 and 4 at T3);
- the QSC-6 permission drift monitor, diffing actual access against the GOV-7 register plus standing policy (QSC-6 step 2 at T3);
- continuous QSC-9 anchoring of the security-critical class: BOOTSTRAP, gate definitions, the approval matrix, lane criteria, Delegation Contracts, the mastership and conflict_rule fields of sources.yaml, severity rubrics, watch configs (QSC-9 step 6, IC-4);
- the QSC-13 backup jobs to an offsite immutable target whose custody is separate from the writer (QSC-13 steps 1 and 2 at T3);
- QSC-15's own meta-monitoring, because a dead monitor is an incident, not a log line (QSC-15 step 4, escalating into QSC-14).

The alert path is tested end to end on cadence, including the receiving human, which in a solo Dimension means her phone actually has to buzz (QSC-15 step 5).

### The weekly combined sweep

One agent-run sweep, Monday morning, one combined Event as evidence, lawfully satisfying the mechanical steps of MIR-3, MIR-7, QSC-2 and QSC-9 (COMMON 6, clause 2). Escalations and findings still route individually to their owning processes: a retry-exhausted pipeline hands its countdown to MIR-6 monitoring and, if the pattern repeats, opens a QSC-14 incident (MIR-3 step 4); drift open past its age limit reaches her at T1 (MIR-7 step 6); a confirmed contradiction is hers to adjudicate, never an agent's to resolve by deleting one side (QSC-2 step 6); an unexplained diff on an anchored artifact opens QSC-8 immediately.

### The quarterly consolidated review

One sitting, one combined report plus per-register Events, executed as the generic register-recertification pattern (COMMON 8) run once across all registers (COMMON 6, clause 1). Four mechanical moves per register: enumerate the entries, check age and actual usage against the declared thresholds, re-approve or amend or retire each by her decision, record the outcome as a versioned Event.

It satisfies the recertification steps of MIR-1, MIR-6, MIR-9, ACT-1, ACT-3, CON-10, CTX-9, QSC-6 and QSC-11 that fall due in the window. She schedules into the same sitting the things those steps consume:

- the QSC-7 agent-behavior audit, whose tier recommendations are named inputs to CTX-9 step 8, and which tests injection-bait refusal explicitly rather than assuming it;
- the QSC-13 restore-drill review, since a backup that has never restored is treated as nonexistent;
- the one-page GOV-5 capacity plan: the hours she really has, the storage the retention policy really implies, and the honest cadence reductions that follow;
- the GOV-8 inventory reconciliation, hunting orphan credentials (no anchor) and shadow credentials (in use, not inventoried);
- the GOV-1 step 8 look at recurring decisions that should stop being decisions and become standing policy.

ACT-12 stays recommended rather than core here, because she declares no emergency actuation class and runs no ACT process at T3. Its findings ride the same sitting.

## A typical week

### Monday: the sweep

Warden runs the combined sweep and emits one Event. MIR-3 finds two cadences due and invokes MIR-2 for the invoicing mirror; the capture lands raw and unmodified with its provenance sidecar, and the capture-time attestation comes from the pipeline runner's own log, which the operator does not edit (MIR-2 step 3, solo variant). QSC-2 resolves every reference and finds no dangling ones. QSC-9 recomputes the fingerprint and verifies that the raw captures still hash to their attestations.

MIR-7 compares master state against copy state on both mirror surfaces and finds one divergence: the published service catalogue page differs from its master, because a client's assistant fixed a phone number directly in the site CMS. MIR-7 is the sole drift engine and does not decide what the edit means; it hands the drift Event to CON-11, the sole capture and classification path for intended external edits. Scribe classifies it as an intended improvement at T3 and packages a sponsored proposal into CON-1, with the external editor recorded in provenance as the source of the assertion, never as a rights-holding Contributor (CON-11 step 4). Sponsored proposals are structurally ineligible for auto-approval, so it waits for her decision at CON-4. The mirrored bytes are never touched, and a repeat of the same drift on the same copy would be a mastership smell escalated as a CON-9 dispute (CON-11 step 8).

### Tuesday: a harvest correction

The Monday harvest landed a corrected invoice amount: the accounting SaaS had reissued an invoice. The mirror self-corrected, as it should, because the external system is the master and the conflict rule resolves in the declared direction. But her engagement summary, model-mastered and hand-authored, quotes the old figure. That is a CON-8 trigger (an upstream source correction arriving by re-harvest). Clerk runs the impact analysis over the provenance graph at T3 (CON-8 step 3), Scribe authors the fix as a new version through CON-3 and CON-4 at T2, the Event carries exactly one primary reason code from the MIR-10 taxonomy, MIR-9 keeps the superseded version reachable with identity and provenance intact (IC-8), and the notification goes to the addressees resolved against CON-13, not against memory. Had this been a retraction rather than a correction, approval would have stayed at T1.

### Wednesday: an owner-directive actuation

She decides to retire the legacy monthly retainer from her published catalogue and replace it with a fixed-scope package. This is a novel, human-initiated action, so no cataloging ceremony is needed: the decision cites the standing owner-directive class and states the intent (ACT-5 step 1, branch b). The service catalogue is model-mastered, so the register selects intent-ahead (ACT-7): the new catalogue version is authored as Proposed while the current version stays Active, and it is not presented as current state. Before deciding she triggers MIR-5 on the invoicing mirror, so the decision rests on a mirror whose freshness she checked rather than assumed.

Because she is decider, dispatcher and executor, one composite actuation event carries the intent, the decision, the command and the verification note, lawfully satisfying ACT-5, ACT-6, ACT-7 and ACT-9, with the idempotency key and the command-decision hash check waived (COMMON 6, clause 3). Under the shipped Impact Matrix the change is reversible and in scope, therefore below the assessment and rollback-plan floors, so ACT-4 is not required. The site publisher, a registered effector (ACT-3), publishes. Verification is her looking at the live page, not at the script's exit code (ACT-9 solo variant), and only that evidence promotes the Proposed version to Active (ACT-7 step 6). The following Monday's MIR-7 pass compares the published hash against the master and records a clean check.

Had the target been external-mastered, the register would have selected the other lawful pattern: reality-ahead (ACT-8), where she changes the external system first and the model follows by a forced out-of-cycle re-harvest, never by hand-editing the mirror to show the expected result. The intention would still be model-mastered and recorded before dispatch. That invariant does not bend with mastership.

The waiver is narrow and she knows where it ends: full artifact separation stays mandatory for any T2 or T3 delegated actuation, without exception.

### Thursday: an editorial fast-lane change, and one that is not

She rewrites two sentences in a method-library page for clarity. The diff-based classifier, a GOV-2 gate config executed by CON-4's gateway, marks it editorial and under the declared size threshold, so Scribe runs intake, provenance capture, gate checks, auto-approval, versioning and reason stamping end to end at T3 and emits one composite Event. That single Event is conformant evidence for CON-1, CON-2, CON-3, CON-4 and CON-6, for MIR-10 reason stamping, and for the CTX-5 execution record (COMMON 7). Crucially, the classification did not come from Scribe or its orchestrator.

An hour later Scribe proposes a one-word change to a conflict_rule field in sources.yaml. Same size, same apparent triviality, entirely different lane: the mastership and conflict_rule fields are the security-critical dataset class, structurally ineligible for any auto-approval lane regardless of proposed classification (IC-4). It routes to T1 acceptance with a second human reviewer, which solo means her peer, not her cooling period, since the cooling period substitutes only for GOV-2 policy acceptances. The change then lands only through MIR-1, the sole executor of register changes, with a GOV-1 decision Event behind it. A silent mastership edit in a routine commit is exactly the failure this refuses.

### Friday: handback and debt

Every agent session this week opened with CTX-10: verify the bootstrap materials against their QSC-9 hash anchors, read BOOTSTRAP.md and the manifest and the register before reading content, run the coverage walker, load one's own boundaries from the CTX-9 contract and the GOV-7 grants, declare readiness in a session log Event. It is a short ritual solo, and it is the same ritual in the same order every time, which is the point.

She closes the week's FCD loops (CTX-5): every task ran from a recorded Context Package built by Clerk under CTX-1, with origin and taint classes on every section, freshness and quarantine stamps on every mirror, a gap list, and the grant IDs the package was built under, so the package dies when a grant is revoked or its TTL expires, whichever comes first. Handback (CTX-11) turns what she learned into model content rather than chat history. One learning is a better harvest checklist, which is method-level and therefore targets bootstrap materials: security-critical class, T1 acceptance, cooling period, re-anchored by QSC-9. Two findings from the week (an aging status declared register entry, a warning aged past its cycle in QSC-4) land in the QSC-11 debt register with severity, age, source report identifier and due date. Nothing closes without re-check evidence.

## What never delegates

Solo does not mean informal. These acts she performs in substance, whatever drafting support an agent gives her:

- appointment, handover and succession invocation (GOV-3);
- deciding, and ruling on appeal (GOV-1);
- consent to any read, inward or outward, purpose-bound and TTL-bounded (IC-7, GOV-7);
- mastership rulings (CON-9), executed only through MIR-1, the sole register executor;
- issuance, amendment and revocation of Delegation Contracts (CTX-9);
- risk acceptance, always with an expiry date, never indefinite (QSC-11 step 6);
- approval of custody arrangements and signing-key succession (GOV-8);
- engaging the Auditor and accepting the report (GOV-6), run solo as a reciprocal peer arrangement with rotation by alternating peers;
- signing the conformance statement, labeled self-declared rather than certified (QSC-10, core for her because she publishes).

## When Solo/Minimal stops fitting

The profile is a lawful conformance target, not a degraded mode, but it has edges. Her first federation contract brings FED-2 signing (non-delegable in substance), FED-3 consent lifecycle and FED-8 admission quarantine, which is a different state from MIR-8 quarantine and from a QSC-9 integrity hold. The first delegated actuation at T2 or T3 ends the composite actuation event, makes full artifact separation mandatory and makes the ACT-1 signal catalog mandatory; any ACT process running at T3, or a declared emergency actuation class, promotes ACT-12 to core. A second Steward makes the cooling-period substitution unnecessary and gives her a real second reviewer. Growth past her declared size or consumer-count threshold promotes QSC-1 to core. Each of those is a profile change she declares, records in GOV-1 and re-validates through QSC-4, not a drift she notices later at audit.