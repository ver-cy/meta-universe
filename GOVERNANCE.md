# Governance

How the **Meta-Universe specification** is stewarded. This is the *operational*
companion to the normative [Governance](01-constitution/Governance.md) document:
that one defines governance *as a constitutional principle*; this one says *how
the project is actually run today*.

## 1. Guiding principle

Meta-Universe aims to be an **organization-independent** open standard, like the
work of W3C/IETF/ISO. It is currently **steward-led** by Vercy during the
Working Draft phase, with the explicit intent to migrate to neutral, multi-party
governance as adoption grows. Steward-led today; community-governed by design.

## 2. Bodies (roles, not yet a legal organization)

These are roles in the governance architecture; they may be filled by one or many
parties:

| Body | Owns | Mandate |
|------|------|---------|
| **Constitution Council** | MUC | Changes to the Constitution only |
| **Architecture Board** | MMAS (incl. MUIF, Validation) | Meta-model architecture |
| **Federation Working Group** | MUFP (incl. Messages, Security) | Federation protocol |
| **Domain Registry Authority** | Registries | Compatible-model registry stewardship |
| **Certification Authority** | Conformance levels | Certification criteria |

## 3. Decision-making

- Changes follow the [Change Process](01-constitution/Change-Process.md) and are
  proposed as Change Requests (CRs) via pull request.
- A CR to a Normative document requires review by the owning body (Section 2) and
  a **public review period**. Editorial CRs may be merged by maintainers.
- Decisions are made by **rough consensus**; where consensus fails, the owning
  body decides, records the rationale, and the decision is auditable.
- All decisions are public and traceable. Nothing is decided in private.

## 4. Maintainers

Maintainers triage issues, review CRs, and steward releases. During the Working
Draft phase, maintainers are appointed by the steward; the path to community
maintainership will be published before the first stable release.

## 5. Intellectual property and patents

- The specification text and all code/schemas are licensed under
  **[Apache License 2.0](LICENSE)**, which includes an explicit **patent grant**
  from contributors.
- By contributing, you agree your contribution is licensed under Apache-2.0 and
  that you have the right to license it (a Developer Certificate of Origin–style
  affirmation; see [CONTRIBUTING.md](CONTRIBUTING.md)).
- Implementations are free, including commercial implementations. There are no
  royalty or membership requirements to implement Meta-Universe.
- If a future neutral body is formed, an explicit IPR policy (covering essential
  claims and a non-assertion covenant) will be adopted at that time.

## 6. Releases and versioning

Releases follow [Versioning](02-architecture/Versioning.md) and the
[Freeze Rule](README.md#freeze-rule). A document becomes *Frozen* only after its
owning body approves it; *Stable* releases bundle frozen documents.

## 7. Naming decision (recorded)

The name **"Meta-Universe"** and the *Universe / Dimension / Namespace* vocabulary
are a deliberate, retained choice: they convey sovereignty and bounded semantic
worlds. The project explicitly distinguishes itself from consumer "metaverse"
(VR/AR) products; positioning materials state this up front. This decision is
recorded here so it is not silently revisited.

## 8. Evolution of this document

This governance model will itself evolve toward neutrality. Changes to it are
made transparently and announced through the normal Change Process.
