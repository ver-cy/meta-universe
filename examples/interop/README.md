# Interop Appendix

**Meta-Universe Specification**

**Document ID:** MU-V2-EX-010  
**Title:** Interoperability Appendix — Importing and Mapping External Standards  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [Extension-Model](../../02-architecture/Extension-Model.md), [Semantic-Mapping](../../03-federation/Semantic-Mapping.md), [MMAS-Interchange](../../02-architecture/MMAS-Interchange.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# Purpose

Meta-Universe **unifies rather than replaces**. It does not ask the world to abandon
Schema.org, FHIR, FOAF, RDF or OWL and adopt a single new vocabulary. It imports those
standards as [Semantic Packages](../../02-architecture/Extension-Model.md), maps local
concepts to them through [Semantic Mappings](../../03-federation/Semantic-Mapping.md),
and projects its own [Objects](../../04-core-concepts/Object.md) into their formats.

This appendix **demonstrates** that posture with working artifacts rather than asserting
it in prose. Each file below takes the same running concept — a local `employee.person`
Object — and shows it living comfortably alongside external standards.

# Files in this appendix

| File | Shows |
|------|-------|
| [`schemaorg-person.import.json`](schemaorg-person.import.json) | A MUIF-style **Semantic Package** import declaration that brings `schema:Person` (with `givenName`, `familyName`, `birthDate`) into a local model, with a compatible version range and a placeholder Semantic Fingerprint. |
| [`person-mappings.json`](person-mappings.json) | **Semantic Mappings** aligning `employee.person` field-by-field to Schema.org Person, HL7 FHIR Patient and FOAF Person, each link carrying a `relation` (equivalent / broader / narrower). |
| [`object-to-rdf.md`](object-to-rdf.md) | A worked projection of one MUIF Object into (a) **RDF triples** (Turtle) and (b) an **OWL class**, using the concrete `employee.person` example. |

# How to read this together

1. **Import** — `schemaorg-person.import.json` acquires `schema:Person` as a named,
   versioned, fingerprinted dependency. The originating standard remains authoritative;
   Meta-Universe holds a reference, not a copy.
2. **Map** — `person-mappings.json` then states *how* the local `employee.person`
   corresponds to that import and to two further standards (FHIR, FOAF), one field at a
   time, with an explicit relation so consumers know whether the link is exact, broader
   or narrower.
3. **Project** — `object-to-rdf.md` finally shows the same Object rendered into the RDF
   and OWL worlds, so a Semantic-Web consumer can read it without ever learning MUIF.

Together these three steps are the import → map → project loop that lets a sovereign
Meta-Model interoperate with the existing standards ecosystem instead of competing with it.

# Note on fingerprints

The `fingerprint` values in these files are **placeholders** (`sha256:<...>`), not
canonicalized digests. They mark *where* a real
[Semantic Fingerprint](../../02-architecture/MMAS-Interchange.md) would be computed and
recorded, so consumers could detect whether two imports of the "same" standard actually
agree in meaning. The teaching examples under
[`../minimal-person`](../minimal-person/) and
[`../federation-acme-govtax`](../federation-acme-govtax/) carry real, round-tripped
fingerprints.
