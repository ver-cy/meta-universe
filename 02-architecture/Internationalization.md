# Internationalization

**Meta-Universe Specification**

**Document ID:** MU-V2-ARCH-012  
**Title:** Internationalization and Localization Model  
**Document Class:** Normative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** [Naming-Conventions](../02-architecture/Naming-Conventions.md), [MMAS-Interchange](../02-architecture/MMAS-Interchange.md), [MMAS-Core](../02-architecture/MMAS-Core.md), BCP 47, RFC 2119  
**Informative References:** [Traceability](../02-architecture/Traceability.md), [Projection](../04-core-concepts/Projection.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

This document defines the **internationalization (i18n) model** of the
Meta-Universe: how a single language-independent meaning carries human-readable
labels, descriptions and documentation in many languages without those
localizations ever affecting identity or the
[Semantic Fingerprint](../02-architecture/MMAS-Interchange.md).

The governing principle is already stated by
[Naming-Conventions](../02-architecture/Naming-Conventions.md): the
[Canonical Semantic Name (CSN)](../02-architecture/Naming-Conventions.md) is
language-independent, while Display Names may be localized. This document makes
that principle complete and normative across Objects, Properties and Projections.

---

# 2. Scope

This specification applies to:

- the separation of language-independent meaning from localizable presentation;
- the attachment of localized labels, descriptions and documentation to Objects,
  Properties and Projections;
- the language-tagging rules for localized content;
- the guarantee that localization is non-semantic.

It does not define translation workflows or the rendering of localized content in
user interfaces.

---

# 3. Principles

- **Meaning is language-independent.** A concept's identity is its CSN, not any
  word in any human language.
- **Presentation is localizable.** Everything a human reads — labels,
  descriptions, documentation — MAY be translated.
- **Localization is non-semantic.** Adding, changing or removing a translation
  SHALL NOT change what a concept means or its Semantic Fingerprint.

---

# 4. The Canonical Semantic Name Is Not Localized

A [Canonical Semantic Name (CSN)](../02-architecture/Naming-Conventions.md) SHALL
be language-independent and SHALL NOT be localized.

- A concept SHALL have exactly one CSN regardless of how many languages it is
  presented in.
- A CSN SHALL NOT be translated, transliterated per-language, or varied by locale.
- All [federation](../03-federation/MUFP.md) interactions SHALL exchange CSNs,
  never localized Display Names, for identity.

The CSN commits to no human language just as it commits to no programming
language: it expresses position in a semantic hierarchy and nothing more.

---

# 5. What Is Localizable

The following are presentation and SHALL be treated as **non-semantic**:

- **Display Names** — the human-friendly label for a concept;
- **Descriptions** — short human-readable explanations;
- **Documentation** — long-form human-readable text;
- **labels** and UI captions attached to Properties and Projections.

These keys are already enumerated as non-semantic and excluded from
canonicalization by [MMAS-Interchange §5](../02-architecture/MMAS-Interchange.md).
Localization adds *more values* to these same non-semantic fields; it never
introduces semantic content.

---

# 6. Language Tags

Localized content SHALL be tagged with a language tag conforming to **BCP 47**
(for example `en`, `ru`, `zh`, `zh-Hans`, `pt-BR`).

- Each localized value SHALL declare its language tag.
- A model SHOULD declare a default language tag for content whose tag is absent.
- Language tags SHALL be compared case-insensitively per BCP 47 and SHOULD be
  stored in their canonical BCP 47 form.

A localized field is therefore a map from BCP 47 language tag to text, attached
to the concept's non-semantic presentation.

---

# 7. Attaching Localized Labels Without Affecting the Fingerprint

Localized labels SHALL attach to Objects, Properties and Projections as values of
the non-semantic presentation keys of Section 5. Because those keys are excluded
from canonicalization:

- a concept with one CSN and ten translated Display Names SHALL produce the
  **same Semantic Fingerprint** as the same concept with one translation, or with
  none;
- adding, editing or removing a translation SHALL NOT require a
  [migration Event](../02-architecture/Semantic-Migration.md), because no meaning
  changes;
- two Universes that present a concept in different languages SHALL still resolve
  to the same CSN and the same fingerprint, and therefore agree that they mean
  the same thing.

User interfaces SHOULD present the localized Display Name appropriate to the
user's locale while resolving it to the underlying CSN; if no translation exists
for a requested locale, they SHOULD fall back to the default language.

---

# 8. Worked Example

A single compensation concept, presented in three languages over one immutable
CSN:

```text
CSN          : employee.compensation.salaryAgreement   (language-independent)

displayName  :
  en : "Salary Agreement"
  ru : "Соглашение об оплате труда"
  zh : "薪资协议"

description  :
  en : "The agreed terms of an employee's base compensation."
  ru : "Согласованные условия базовой оплаты труда сотрудника."
  zh : "员工基本薪酬的约定条款。"
```

The Semantic Fingerprint is computed over the semantic core, which contains the
CSN and structural facts but **none** of the `displayName` or `description`
values. Therefore all three presentations — and any subset of them — yield the
identical fingerprint. Removing the `zh` translation, or adding a `de` one,
changes nothing semantic.

---

# 9. Validation

A model conforms to this specification when:

- every public concept has exactly one language-independent CSN;
- no CSN is localized;
- every localized value carries a BCP 47 language tag;
- localized content occupies only non-semantic presentation keys;
- the Semantic Fingerprint is invariant under addition, change or removal of any
  translation.

See [Validation](../02-architecture/Validation.md) for the applicable levels.

---

# 10. Architectural Invariants

- The CSN SHALL be language-independent and SHALL NOT be localized.
- Localized content SHALL be non-semantic and SHALL NOT affect the Semantic
  Fingerprint.
- Localized values SHALL carry BCP 47 language tags.
- Federation SHALL exchange CSNs, never localized Display Names, for identity.
- Changing a translation SHALL NOT constitute a semantic change.

---

# Future Directions

A future revision could define a **localization package** format that lets
translations be published, versioned and federated independently of the model
they decorate — so a community can contribute a language without touching the
authoritative semantic model — together with a quality signal for translation
coverage that could feed the [Semantic Coherence Score](../06-ecosystem/Semantic-Coherence-Score.md)'s
documentation-completeness dimension, and locale-aware
[Projection](../04-core-concepts/Projection.md) selection.

---

# Final Statement

> A concept means one thing; the world reads it in many languages. The
> Meta-Universe keeps these apart: one Canonical Semantic Name carries the
> meaning, and any number of localized labels carry the words — so that
> translating a model never changes what it says.
