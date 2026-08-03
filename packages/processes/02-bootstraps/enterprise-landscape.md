# Enterprise landscape: six products, one Universe, forty people

Northwind Instruments builds and sells six software products for laboratory equipment. Forty people: three product teams, a platform group, a small data team, and a two-person architecture function that nobody wants to be a bottleneck. Their problem is not that knowledge is missing, it is that it lives in six places and disagrees with itself: the API described in a wiki, the retention rule in a compliance spreadsheet, the true dependency graph in one architect's head.

They run one Universe with seven models: a product-landscape model that describes the portfolio, and one model per product. They declare the Standard conformance profile (COMMON 6), because they federate with one partner and publish nothing publicly. This is one quarter of that operation.

## The shape of the Universe

The landscape model is the parent: it holds products, the teams accountable for them, shared platform components, and the cross-product dependencies. Each product model holds that product's own semantics. Nothing is duplicated between them: the landscape references product namespaces, it does not copy them, so exactly one master exists per dataset (COMMON iron control IC-1) and the Mastership Register in each repository declares it (MIR-1).

Genesis happened a year ago, one model at a time (GOV-4): scaffold, appoint, initialize the registers, run the first validation, activate. Two of the six product models were born by importing an existing wiki export in bulk (CON-7), which invoked MIR-1 first so the wiki was declared an external master before a single byte moved, not after.

## Who is accountable for what

The roles are not org-chart roles. The Owner is the CTO, one person, because ownership of the Universe cannot be a committee (COMMON 2). Each product model has one accountable Steward, usually the product's tech lead; the landscape model's Steward is one of the two architects. Appointments, and the deputies that keep every T1 gate from failing closed when someone is on leave, are recorded in GOV-3.

Roughly twenty AI agents work in the Universe: per-product context agents, a harvest fleet, two review agents, one landscape-wide consistency agent. Every one of them holds a Delegation Contract issued and monitored in CTX-9, which is the single System of Record for delegation; onboarding, identity and entry rights come from CON-10 and reference the contract rather than reissuing it. New agent-scope pairings start at T1 or T2 and earn T3, and the first acts under any grant run one tier stricter than granted.

## The approval matrix in action

The approval matrix is not a wiki page here, it is a versioned GOV-2 artifact that CON-4 executes. It says, in effect: editorial and corrective changes to product documentation run in the auto-approval lane; anything touching an API contract, a data-retention rule or the landscape dependency graph requires the accountable Steward plus an architect; anything in the security-critical dataset class requires T1 plus a second human reviewer (COMMON iron control IC-4).

A concrete week. A platform engineer proposes changing the shared authentication component's token lifetime, filed as a contribution (CON-1) with provenance captured (CON-2) and the validation gates run (CON-3). At CON-4 the diff-based lane classifier does the thing that saves them: the submitter classified it "corrective", but the diff touches a contract dataset, so the classifier forces human review regardless of the proposed classification, and logs the mismatch as a finding rather than merely as an escape. Two products depend on that component, so the matrix pulls in both product Stewards. The Agent supplies the impact analysis from the provenance graph (CON-4 step 5), listing what references the component. The change is approved with rationale, versioned (CON-6), and the reason code is stamped (MIR-10).

The month before, the same mechanism caught something less innocent: an agent's proposed classification would have auto-merged an edit that quietly changed the meaning of "active customer" in the landscape model. Classification-versus-diff mismatch findings are reviewed at the quarterly audit; that one became a lane-criteria amendment in GOV-2.

## An FCD task, executed by an agent

A developer is asked to add a field to the sample-tracking API of one product. This is a Full Context Development task and it runs the CTX-5 loop, executed by that product's development agent under a T2 contract.

The agent asks for context (CTX-1). The package it gets is not the ticket text: it is the affected API objects, the domain rules that constrain them, the two prior decisions that explain why the current shape exists, the risks filed against that area, and the acceptance criteria, each element carrying provenance and a pointer to its full form. Every section carries an origin class (authored, mirrored-external, federated, human-report), and the contract forbids treating non-authored content as instructions.

The loop then does what the discipline requires. The agent checks that the context is sufficient and does not proceed on guesses (CTX-5 step 3). It plans the change and looks up each affected dataset's master before writing (step 4). One planned write targets the API reference page, which is a generated projection, not the master, so the gateway at step 5 redirects it to the source of record instead of editing the copy. The code change itself is executed, results are written back through the CON chain as a registered channel (step 7), the coverage walker and the MIR-7 drift check run and stay green (step 8), and the execution event records which context package was used (step 9).

What the model gains is not just a field. It gains the decision behind the field, and the fact that the ticket's original framing was wrong, recorded as a learning (CTX-11) and as a small piece of model debt (QSC-11) where the domain rule turned out to be underspecified.

Three teams work concurrently on the landscape model that quarter. That is CTX-6 partitioning by bundle, with merges going through CTX-7, which is the concurrency-integration step feeding CON-4, not a second approval authority. One genuine conflict (two teams renaming the same shared concept in opposite directions) is arbitrated by the landscape Steward and recorded, not silently resolved by whoever merged last.

## The quarterly audit finds something

The audit is QSC-5, run by an Auditor engaged through GOV-6 with time-boxed access provisioned via GOV-7 and verified torn down at closure. The Auditor is an architect from a different part of the company, and cannot audit work they supervised.

Evidence collection is agent work at T2, read-only. Judgment is not. The Auditor verifies that every declared process ran at its cadence (step 3), including the backup jobs and drills (QSC-13) and the heartbeat operations (QSC-15), and reconciles every alarm against an incident record (QSC-14). Then re-performance, which the card calls mandatory: recompute a sample of quality scores, re-run validation on a pinned past version, re-decide a sample of access verdicts (QSC-6), re-trace a sample of agent actions against their CTX-9 contracts (QSC-7).

The finding: one product's harvest pipeline had been failing silently for five weeks. The dataset was mirrored from an issue tracker, its freshness state should have flipped to stale, and the monitor that would have flipped it had died. The data kept being read, and being read confidently, which is the failure the whole MIR family exists to prevent.

The remediation is not "be more careful". The dead monitor is a QSC-15 finding (a standing job whose own heartbeat was not watched), it becomes a QSC-14 incident with a blameless postmortem, and the postmortem's lesson is routed as a versioned change into the monitor rules rather than into a memo. The stale dataset is quarantined (MIR-8) so that every citation of it carries the flag, and the affected records are re-harvested. All of it lands in the quality debt register (QSC-11) with owners and deadlines, and the Owner receives the report directly, not only the audited Steward.

## Federating with a partner

Northwind's largest customer, a contract lab, wants their instrument fleet's configuration to stay in sync with Northwind's product model. This is a federation, and it runs the FED sequence compressed into about six weeks.

Discovery and evaluation first (FED-1): what the partner publishes, what they need, and what their trust profile looks like, evaluated per dimension rather than as one score, so the answer is not "trusted" but "identity and contract dimensions strong, operational history unknown". Then negotiation and signing (FED-2), which is a non-delegable act: the Owner signs, no agent, no tier.

The consent lifecycle (FED-3) grants exactly two projections, purpose-bound, with a TTL and a renewal date, and every auto-issued grant under the standing policy cites the policy version that produced it. Disclosure review (FED-4) runs before anything leaves: what is included, what is redacted, and the cumulative check that asks what this release composes to when combined with everything the partner already holds, so consent cannot be salami-sliced into something the Owner never approved. Establishment and initial sync follow (FED-5).

The inbound direction is where the discipline shows. The partner also sends fleet telemetry. It does not land in the model. It lands in admission quarantine (FED-8), unreadable until promoted, screened for hazards including instruction-like content, and only after promotion does MIR-2 execute the landing with provenance. The two things called quarantine are kept distinct on purpose (COMMON 5): FED-8's admission quarantine is unreadable until promoted, MIR-8's quarantine is readable but flagged.

## What it costs, and what standing obligations remain

The Standard profile allows the consolidation clauses where a single Steward is accountable for the consolidated registers, so recertification of grants, contracts, effectors, entry rights and SLAs happens in one quarterly sitting per model rather than eight separate rituals (COMMON 8, the register-recertification pattern). Capacity is not assumed: steward hours, agent compute quotas and storage projections are planned in GOV-5, which is what keeps the whole apparatus from quietly decaying into ceremony that nobody has time to perform honestly.

The measurable change after a year is not that documentation improved. It is that when someone asks "what depends on this component", the answer comes from the model, it is current, and if it is not current, the model says so.
