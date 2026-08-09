# Interface Bindings

**Meta-Universe Specification - Entity Core Exploration**

**Document ID:** ECORE-004 (candidate MU-V3-ECORE-004)  
**Title:** Entity Core - Interface Bindings: GIT, MCP, SQL, and the Uniform Security Description  
**Document Class:** Normative draft (pre-normative until accepted)  
**Version:** 0.1  
**Status:** Working Draft (standard-evolution exploration, entity-core branch)  
**Normative References:** Entity-Core-Direction (ECORE-001), Entity-Graph-Model (ECORE-002), Packaging-Profiles (ECORE-003), Data-Mastership (ARCH-018), Policy-Consistency (ARCH-014), Semantic Fingerprint (ARCH-009), MMAS-Interchange (MUIF), Model-Traversal-and-Layout (ARCH-017), Versioning (ARCH-002), Naming-Conventions (ARCH-003), Validation (V0-V5)  
**Informative References:** Projection (CORE-009), Virtual Projection (CORE-012), MUFP-Messages (FED-011), Security-Model (FED-012), Discovery (FED-013), Zero-Knowledge-Attestation (FED-014), Synchronization (FED-007)  
**License:** Apache-2.0

---

# 1. Purpose

[Packaging-Profiles](Packaging-Profiles.md) (ECORE-003) defines how the semantic graph is physically laid out. This document defines how a consumer **reaches** it: the **interface binding**.

An interface binding answers two questions for one access technology:

1. **How does a consumer read Findings?** Discovery, enumeration, projection, freshness.
2. **How does a consumer execute Methods?** The entity methods of ECORE-002 become invocable operations, under a declared write discipline.

Three bindings are specified: **GIT** (the repository is the interface), **MCP** (a Model Context Protocol server exposes the graph to agents), **SQL** (the database is the interface). All three are described by one **uniform security description**: named access groups, an authorization center, and policy bound to ARCH-014. All three obey one synchronization model: mastership per ARCH-018 decides where writes land, staleness is declared, and cross-binding consistency is fingerprint equality per ARCH-009.

Bindings are intra-universe access. Federation between sovereign universes remains the MUFP federation layer and is not changed by this document.

---

# 2. Scope

This specification governs:

- the binding concept and what every binding declaration must contain;
- the GIT, MCP and SQL bindings;
- the uniform security description: access groups, authorization center, policy;
- the continuous synchronization model across bindings;
- the boundary between bindings and federation.

It does not run infrastructure: the standard defines what a binding declares, not a hosted service. It does not redefine packaging (ECORE-003) or the entity model (ECORE-002).

---

# 3. The Interface Binding Concept

A **binding** is a named, versioned declaration that a specific packaging of a specific model version is reachable through a specific access technology, under a specific security description, with a specific staleness contract.

Every binding declaration SHALL state:

| Field | Meaning |
|-------|---------|
| `binding` | The binding type: `git`, `mcp`, `sql`, or a registered extension |
| `profile` | The packaging profile served (ECORE-003): MD or JSON for GIT, DB for SQL, any for MCP |
| `endpoint` | Where the interface lives: repository URL, MCP server address, database connection locator |
| `model` | Registry id plus CSN, Namespace, version of the served model; its Semantic Fingerprint |
| `role` | `master` or `mirror`, per the Mastership Register (ARCH-018) |
| `write_path` | `propose-only` (default), `direct` (only lawful at the master, only where policy allows), or `read-only` |
| `security` | The uniform security description (Section 7) |
| `staleness` | The staleness contract (Section 8.2) |

Binding declarations are data: they live in the model's manifest (or a `bindings.yaml` beside it), are versioned per ARCH-002, and are enumerable so a consumer can discover every door into the model. A binding exposes the graph; it never defines it. Whatever the technology, the Findings read through any binding SHALL be the Findings of the packaged graph, and the fingerprint proves it.

Methods are part of the graph: ECORE-002 defines them as named operations on entities with typed signatures. A binding maps each method to the invocation idiom native to its technology (PR, tool call, stored procedure). The **propose-only default** applies everywhere: a method invocation produces a proposal (a change request against the master) unless the security description explicitly grants direct execution and the binding fronts the master.

---

# 4. The GIT Binding

The repository is the interface. This is the v0.1 workhorse: no long-running services, synchronization is `git pull`.

- **Layout**: the repository content is a conformant MD-profile or JSON-profile packaging (ECORE-003 Sections 5, 6). The ARCH-017 entry point (`BOOTSTRAP.md`, `manifest.yaml`) doubles as the binding's discovery surface; the binding declaration lives in the manifest.
- **Read**: clone or pull; then the canonical walk (ARCH-017 Â§10) and the Findings enumeration of the profile. Model versions are tags per ARCH-002; a consumer pins a version by tag and verifies the fingerprint.
- **Propose**: a pull request. The PR is the native propose-only write path: a method whose effect is a change to the graph is executed by committing the proposed change on a branch and opening a PR; review and merge are the application step, governed by policy. A Twin Composition Snapshot committed in the repository pins the composition the proposal was made against.
- **Sync**: pull cadence. A consumer or a mirror records `observed_at` (the time of its last successful pull and the commit it landed on) and surfaces both. This is the entire v0.1 synchronization machinery, a constraint this exploration fixes: git pull, no services.
- **Authn**: the forge's own authentication (SSH keys, forge tokens). The binding does not replace it; the security description declares the forge as the operative authorization center for this binding, or declares an external center whose identities are mapped to forge accounts.
- **Authz mapping**: access groups (Section 7.1) map to forge constructs: a group with `read` becomes repository read permission; `propose` becomes fork-and-PR or branch push rights; `apply` becomes merge rights on protected branches; `admin` becomes repository administration. **Declared limitation**: forge permissions are repository- and branch-grained; a layer-scoped read group cannot be enforced inside one repository. Where layer-scoped confidentiality is required, split the packaging across repositories along the group boundary, or front the model with the MCP or SQL binding, which can enforce it. Pretending a forge enforces what it cannot is non-conforming; declaring the limitation is.

---

# 5. The MCP Binding

An MCP server exposes the entity graph to AI agents and tools. This is the natural home of **methods-as-tools**.

- **Resources**: the server exposes the graph as MCP resources: entities, bundles, layers, questions, findings, records, addressed by stable URIs built from registry id, CSN, Namespace and version (ARCH-003). Projections (CORE-009) and virtual projections (CORE-012) are first-class resources: a consumer asks for the projection it needs, not the raw graph. Context packs are served as projection resources: task-anchored, pinned by version and Semantic Fingerprint, provenance-carrying; the pack field set and the seven context rules are normatively defined by the ELMM profile and adopted here by reference, not restated.
- **Tools**: each entity Method of ECORE-002 is exposed as one MCP tool. The tool name derives from the method's canonical name; the input schema derives from the method signature; the tool description carries the method's declared meaning. Under the propose-only default a tool invocation returns a **proposal object** (the change it would make, against a pinned fingerprint), not a mutation; a separate `apply` capability, granted only by the security description and only on the master, turns proposals into changes.
- **Discovery**: the MCP server manifest. The server's initialize response and resource listing SHALL embed the ECORE-003 description protocol manifest, so an agent that connects learns the profile, the entity roots, the findings enumeration, the fingerprint, the mastership role and the staleness contract without out-of-band knowledge. Listing resources and reading the manifest SHALL require no more than the lowest read grant.
- **Auth**: the authorization center token flow. The binding declaration names the center (Section 7.2); the server accepts identities and tokens issued there and maps token scopes to access groups. The server SHALL NOT mint identities of its own.
- **Freshness**: every resource response carries `observed_at` and the fingerprint of the graph version it was served from; a server fronting a mirror SHALL surface staleness per ARCH-018 Â§8 rather than hide it.

---

# 6. The SQL Binding

The database is the interface; the DB profile (ECORE-003 Section 8) is its schema.

- **Read**: SELECT over the profile views: `v_findings` for the total enumeration of Findings, `v_walk` for the canonical order, `v_entities` for the graph, plus any projection views. Consumers read views, not base tables; base tables are the packaging, views are the interface.
- **Discovery**: the `_vercy_manifest` table (ECORE-003 Section 8.3). A connecting consumer reads it first: profile, schema map, entity roots, fingerprint, mastership role, `last_sync_at`, cadence, staleness limit. Every role granted any access SHALL be granted SELECT on `_vercy_manifest`.
- **Methods**: entity Methods map to stored procedures. Under the propose-only discipline a procedure SHALL write a proposal row (into a `proposals` table declared in the schema map) rather than mutate base tables; the proposal carries the invoking identity, the method, the arguments, the pinned fingerprint and a timestamp. Direct-writing procedures are lawful only where the security description grants `apply` or `execute-direct` AND the database is the master per ARCH-018; a direct write on a mirror is non-conforming regardless of grants.
- **Authz mapping**: access groups map to database roles; rights map to GRANTs: `read` becomes SELECT on the group's views, `propose` becomes EXECUTE on proposal-writing procedures, `apply` becomes EXECUTE on applying procedures, `admin` becomes DDL. Layer and entity scoping is enforced by per-group views or row-level security policies generated from the group's scope declaration; the generator, not hand-written GRANTs, is the source of truth, so the security description and the database never drift apart silently.
- **Audit**: proposal rows and an append-only audit table (declared in the schema map) record every method invocation and every apply, satisfying Section 7.3.

---

# 7. The Uniform Security Description

One security description, three enforcements. The description is declared with the binding and is the single source from which forge permissions, token scopes and database GRANTs are derived.

## 7.1 Access groups

An **access group** is a named set of rights over a scope:

- **Name**: stable, per ARCH-003; the unit that identities are assigned to and that enforcement artifacts are generated from.
- **Scope**: entity- and layer-scoped: which entities (by registry id, with `*` permitted) and which layers or bundles the group covers. Scope narrows, never widens: a right not in scope is denied.
- **Rights vocabulary**: `read` (Findings and projections), `propose` (submit method proposals), `apply` (turn proposals into changes at the master), `execute` (run methods whose declared effect is computation, not graph mutation), `admin` (manage the binding itself).

Illustrative declaration:

```yaml
security:
  access_groups:
    - name: public-readers
      scope: { entities: ["*"], layers: ["overview", "published"] }
      rights: [read]
    - name: maintainers
      scope: { entities: ["aismm@5"], layers: ["*"] }
      rights: [read, propose]
    - name: stewards
      scope: { entities: ["*"], layers: ["*"] }
      rights: [read, propose, apply]
  authorization_center:
    issuer: https://auth.example.org
    protocol: oidc
  policy:
    default: deny
    write_path: propose-only
    consistency: ARCH-014
    audit: required
```

## 7.2 The authorization center

The **authorization center** is the party that issues identities and tokens. The standard's position is deliberately narrow:

- The binding declaration SHALL name **where** the center is (issuer, protocol). The standard does not run one, host one, or prefer one; a forge's account system, an OIDC provider, or a database's native authentication may each serve.
- All bindings of one model SHOULD name the same center, so one identity spans GIT, MCP and SQL; where a binding uses the technology's native authentication (the forge, the database), the declaration SHALL state the mapping from center identities to native accounts.
- Tokens and credentials live in the center and its stores, never in the graph, never in a packaging, never in a binding declaration. A packaging that embeds a credential fails V0.

## 7.3 Policy

- **Consistency and precedence** bind to ARCH-014: where multiple policies could apply (model-level, binding-level, group-level), ARCH-014's consistency and precedence rules decide; contradictory grants are a validation failure, not a runtime surprise.
- **Least privilege**: groups SHOULD be scoped to the narrowest entity and layer set that serves their purpose; `*` scopes are for genuinely public or genuinely stewarding groups, not for convenience. Context packs served to agents inherit this: least privilege is one of the seven context rules of the ELMM profile.
- **Default deny**: an identity in no group has no access; a right not granted is denied.
- **Audit trail expectations**: every method invocation, every proposal, every apply, and every grant change SHALL be attributable: who (center identity), what (method, arguments or diff), against which fingerprint, when, through which binding. Bindings satisfy this with their native mechanisms (forge PR history, MCP server logs, proposal and audit tables); the expectation is uniform, the mechanism is not.

---

# 8. The Continuous Synchronization Model

## 8.1 Mastership decides the write home

ARCH-018 is the law: every dataset has exactly one System of Record. In binding terms: exactly one binding fronts the master of any dataset; every other binding fronts a mirror. The binding declaration's `role` field states which. Writes, including applied method proposals, land only at the master; a mirror binding forwards proposals toward the master's change process, it never applies them locally. Proposals themselves may originate at any binding: proposing is not writing.

## 8.2 The staleness contract

Every binding SHALL declare a staleness contract:

- `cadence`: how often the binding's content is refreshed from the master (for the master binding: `on-change`);
- `staleness_limit`: the age past which the binding SHALL warn consumers (ARCH-018 Â§8);
- `observed_at` surfacing: how a consumer sees the last refresh time (commit metadata for GIT, response fields for MCP, `_vercy_manifest` for SQL).

A consumer SHALL be able to answer, at any binding, without out-of-band knowledge: what version am I seeing, how old is it, and where do corrections go.

## 8.3 Cross-binding consistency

When all bindings are synchronized to the same model version, the Semantic Fingerprint recovered through each SHALL be identical. Cross-binding consistency is **fingerprint equality, not byte equality**: the GIT working tree, the MCP resource set and the SQL tables share nothing physically and everything semantically. Drift between bindings is detected by fingerprint comparison at each sync run and resolved only in the master's favor, per ARCH-018 Â§7; resolving by judgment per incident is non-conforming.

In v0.1 synchronization is pull-based, a fixed constraint of this exploration: mirrors regenerate from the master repository on a pull cadence; no long-running sync services are required for conformance.

---

# 9. Federation

Bindings are **intra-universe**: doors into one sovereign universe's models, for that universe's identities, under that universe's policy. Federation between sovereign universes remains the **MUFP** federation layer with its message vocabulary (MUFP-Messages, FED-011), and this document changes none of it: federation never transfers mastership, a universe exposes only what it masters or clearly labels as mirrored, and inter-universe trust remains the business of the federation trust layer.

A federation peer is not a binding consumer; a binding consumer is not a federation peer. When universe A grants universe B access to a model, that is a federation contract over MUFP, even if the transport underneath happens to be a repository or a server that also serves local bindings.

**Refinements the federation layer will need** (recorded for the federation editors, not resolved here):

1. **Discovery (FED-013)**: a universe SHOULD be able to advertise, at its federation edge, which packaging profiles and bindings its shared models are available in, so a peer can negotiate a preferred carrier instead of assuming one.
2. **Federation identity**: the mapping between federation-level identities and a universe's authorization center identities needs a declared form, so a disclosed model's access groups can name external principals without absorbing them.
3. **Security-Model (FED-012)**: access groups are a natural unit for disclosure decisions; the federation security model SHOULD recognize a group-scoped disclosure, aligning its consent and disclosure machinery with the same scopes bindings enforce.
4. **Synchronization (FED-007)**: the federation staleness vocabulary and the binding staleness contract of Section 8.2 SHOULD converge on one set of fields, so `observed_at` means the same thing on both sides of a sovereignty boundary.
5. **Zero-Knowledge-Attestation (FED-014)**: fingerprint equality across bindings and packagings is a natural attestation subject: a universe could prove to a peer that its disclosed mirror equals its master without disclosing the master.

---

# 10. Validation

- **V0 (constitutional)**: no credentials in packagings or declarations; mirrors labeled; no binding claims mastership the register does not grant it.
- **V1 (structural)**: every binding declaration parses and is complete per Section 3; discovery works from a cold start at each binding (manifest reachable with the lowest read grant).
- **V2 (semantic)**: security scopes reference existing entities and layers; the groups-to-enforcement generation is consistent (no GRANT, permission or scope without a group, no group silently unenforced).
- **V3 (compositional)**: method-to-tool and method-to-procedure mappings match the ECORE-002 method signatures.
- **V4 (interchange)**: cross-binding fingerprint equality at declared sync points.
- **V5 (runtime)**: staleness limits honored; audit trail present for every apply; propose-only discipline observed (no mutation outside the master's apply path); a binding whose declared cadence has never run is downgraded to `declared`, mirroring ARCH-018 Â§11.

---

# 11. Invariants

- **ECORE-I40**: A binding exposes, never defines: the same graph, with the same Semantic Fingerprint (ARCH-009), is readable through every binding of a model.
- **ECORE-I41**: Every binding is discoverable from a cold start: endpoint plus the profile's manifest mechanism yields identity, roots, enumeration, fingerprint, role and staleness, with no out-of-band knowledge.
- **ECORE-I42**: One uniform security description per model: named access groups, entity- and layer-scoped, enforced natively by each binding and generated from the single declaration.
- **ECORE-I43**: The write path defaults to propose-only; direct execution exists only where policy explicitly grants it and only at the mastership home (ARCH-018).
- **ECORE-I44**: Every binding declares a staleness contract, and every consumer can see `observed_at`; a mirror that hides its age is non-conforming.
- **ECORE-I45**: Cross-binding consistency is fingerprint equality, never byte equality; drift resolves only toward the master.
- **ECORE-I46**: Policy consistency and precedence bind to ARCH-014; default deny; least privilege; contradictory grants are validation failures.
- **ECORE-I47**: Every method execution, proposal and apply is attributable to an identity issued by the declared authorization center; unattributable change is non-conforming.
- **ECORE-I48**: Bindings never cross a sovereignty boundary; inter-universe access is the MUFP federation layer, and federation never transfers mastership.
- **ECORE-I49**: No secrets in the graph, in any packaging, or in any binding declaration; credentials live only in the authorization center.

---

# Final Statement

A model earns its keep when it can be reached: cloned by an engineer, called by an agent, queried by a report. Three doors, one graph, one security description, one fingerprint. The door you enter through changes how the model feels; it must never change what the model says.
