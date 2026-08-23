# Connector Catalogue

**Meta-Universe Specification**

**Document ID:** MU-V2-ECO-009  
**Title:** Catalogue of Composition Connectors Between Meta-Models  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [Meta-Model-Composition](../02-architecture/Meta-Model-Composition.md), [Extension-Model](../02-architecture/Extension-Model.md), [Semantic-Mapping](../03-federation/Semantic-Mapping.md), [External-Models-Registry](../06-ecosystem/External-Models-Registry.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

The [External Models Registry](External-Models-Registry.md) lists 1180 standards as
a flat catalogue. On its own that catalogue does not say **how the standards connect**
— which ones are meant to be nested inside others, which referenced, which applied
as cross-cutting facets. This document supplies those connections.

A **connector** is a recurring concept (an address, a country, a money amount, a
provenance record) for which a canonical external model exists and which many
Meta-Models should reuse rather than re-model. For each connector this catalogue
records its **compositional role**, its **default link type**, the **host concepts**
that should use it, and **why it must not be a flat field** — applying the rubric and
role typology of [Meta-Model-Composition](../02-architecture/Meta-Model-Composition.md).

This is an informative, curated subset of the registry — its *joints*, not its full
inventory. A machine-readable copy is [`composition-connectors.csv`](composition-connectors.csv).

---

# 2. How to Read This Catalogue

- **Role** — the compositional role (R1–R8) from
  [Meta-Model-Composition §7](../02-architecture/Meta-Model-Composition.md).
- **Link** — the default mechanism: **EMBED** (nested value object), **REFERENCE**
  (entity or code by identifier), **MIX-IN** (cross-cutting facet), **ALIGN**
  (ontological grounding).
- **Host concepts** — typical Meta-Models that should connect to the connector.
- The default link is a recommendation, not a constraint; a connector MAY be linked
  differently in a justified context (for example an Address EMBEDed normally, but
  snapshot-EMBEDed in an audit record).

---

# 3. R1 — Foundational Value-Objects (default: EMBED)

Structured, identity-free concepts that recur across domains. Embed the canonical
model; never flatten its parts into host fields.

| Connector | Canonical model(s) | Link | Host concepts | Why not a flat field |
|-----------|--------------------|------|---------------|----------------------|
| Postal Address | OASIS CIQ xAL · schema:PostalAddress · vCard ADR | EMBED | Person, Organization, Facility, Shipment, Invoice party | Multi-part, recurs everywhere, governed shape; flattening forks it |
| Personal Name | OASIS CIQ xNL · schema name parts · FOAF | EMBED | Person, Patient, Author, Contact | Given/family/prefix/suffix travel together; ordering is culture-specific |
| Organization Name | OASIS CIQ xNL (org) · schema:legalName | EMBED | Organization, Supplier, Issuer | Legal vs trading vs display names are one structured unit |
| Contact Point | vCard · JSContact · schema:ContactPoint | EMBED | Person, Organization, Support desk | Channel + value + purpose belong together |
| Monetary Amount | schema:MonetaryAmount · ISO 20022 amount | EMBED | Invoice, Price, Salary, Transaction | An amount without its currency is meaningless |
| Quantity / Measure | QUDT QuantityValue · schema:QuantitativeValue | EMBED | Product, Observation, Ingredient, Spec | A number without its unit is ambiguous |
| Geographic Point | GeoJSON Point · ISO 6709 · geo: | EMBED | Place, Asset, Event location | Lat/lon/CRS are one tuple |
| Geometry / Shape | GeoJSON · GML geometry | EMBED | Parcel, Region, Route, Coverage | Coordinate arrays + CRS are a unit |
| Pose (position + orientation) | OGC GeoPose | EMBED | Robot, Vehicle, AR anchor | Position and orientation co-define a frame |
| Temporal Interval / Instant | OWL-Time · ISO 8601 interval | EMBED (or MIX-IN as valid-time) | Event, Contract term, Employment | Start/end/duration are interdependent |
| Phone Number | ITU-T E.164 · vCard TEL | EMBED | Contact, Person, Organization | Country code + number + type form one value |
| Bibliographic Reference | schema:CreativeWork · Dublin Core | EMBED / REFERENCE | Citation, Dataset, Document | Title/author/date/identifier cohere |

---

# 4. R2 — Reference Data, Code Lists & Classifications (default: REFERENCE)

Curated value sets maintained by an authority. Reference the scheme (term + URI +
version); never copy its members into a local enum.

| Connector | Canonical model(s) | Link | Host concepts | Why not a flat field |
|-----------|--------------------|------|---------------|----------------------|
| Country | ISO 3166-1 · OMG LCC · UN M49 | REFERENCE | nationality, jurisdiction, origin, place | Authority-maintained; a copied list drifts |
| Subdivision / Region | ISO 3166-2 | REFERENCE | Address region, jurisdiction | Same authority, changes over time |
| Language | ISO 639 · BCP 47 | REFERENCE | i18n labels, content, preference | Tag space owned by a registry |
| Script | ISO 15924 | REFERENCE | Multilingual labels, transliteration | Closed code space |
| Currency | ISO 4217 | REFERENCE | Money, Price, Account | Codes + minor units maintained centrally |
| Units of Measure | UCUM · UN/CEFACT Rec 20 · QUDT unit | REFERENCE | Quantity, Observation, Spec | Computable unit grammar, not local strings |
| Product Classification | GS1 GPC · UNSPSC · eCl@ss | REFERENCE | Product, Catalogue, Procurement | Large evolving taxonomies |
| Industry / Activity | NACE · ISIC · NAICS | REFERENCE | Organization, Statistics, ESG | Official statistical classifications |
| Occupation / Skill | ESCO · O*NET | REFERENCE | Employee, Job posting, CV | Maintained labour-market taxonomies |
| Clinical Concept | SNOMED CT · LOINC · ICD-11 | REFERENCE | Patient, Condition, Observation | Vast governed terminologies |
| Medication Concept | ATC · RxNorm · NDC | REFERENCE | Medication, Prescription | Authority-curated drug codes |
| Packaging / Status Codes | UN/CEFACT Rec 21 · Rec 24 | REFERENCE | Shipment, Consignment | Trade code lists |

---

# 5. R3 — Identifier Schemes (default: REFERENCE as typed key)

Keys that point at entities. Reference the key; resolve the entity through it.

| Connector | Canonical model(s) | Link | Host concepts | Why not a flat field |
|-----------|--------------------|------|---------------|----------------------|
| Legal Entity | ISO 17442 LEI | REFERENCE | Organization, Counterparty, Issuer | Global resolvable key; do not inline the entity |
| Security / Instrument | ISO 6166 ISIN · OMG FIGI | REFERENCE | Holding, Trade, Portfolio | Identifies an instrument entity |
| Bank Account / Institution | ISO 13616 IBAN · ISO 9362 BIC | REFERENCE | Payment, Settlement | Validated account/institution keys |
| Trade Item | GS1 GTIN | REFERENCE | Product, Order line, Inventory | Identifies a product entity |
| Party / Location (GS1) | GS1 GLN | REFERENCE | Ship-to, Supplier, Store | Resolvable location/party key |
| Researcher / Person | ORCID · ISO 27729 ISNI | REFERENCE | Author, Contributor, Reviewer | Disambiguates a person entity |
| Publication / Object | DOI · ISBN · ISSN · Handle | REFERENCE | Citation, Dataset, Serial | Persistent resolvable identifiers |
| Digital Identity | W3C DID | REFERENCE | Agent, Wallet, Universe, Issuer | Self-sovereign identifier; resolve to a document |

---

# 6. R4 — Entity Models (default: REFERENCE; snapshot-EMBED only for audit)

Things with identity and lifecycle. Reference them; embed only as a marked,
immutable snapshot when audit demands a frozen copy.

| Connector | Canonical model(s) | Link | Host concepts | Why not inlined |
|-----------|--------------------|------|---------------|-----------------|
| Organization | schema:Organization · W3C ORG · FIBO Legal Entity | REFERENCE | employer, supplier, issuer, owner | Shared entity; inlining yields stale copies |
| Person / Patient | schema:Person · FHIR Patient · FOAF | REFERENCE | author, subject, contact, guardian | Independent identity and lifecycle |
| Place / Facility | schema:Place · GeoSPARQL Feature | REFERENCE | location, site, jurisdiction | Referenced by many; governed externally |
| Product (as entity) | schema:Product · GS1 (via GTIN) | REFERENCE | order line, listing, asset | Has its own catalogue lifecycle |

---

# 7. R5 — Cross-cutting Facets (default: MIX-IN)

Concerns applied across many Objects regardless of domain. Mix them in under their
own namespace; never re-invent them as domain fields.

| Connector | Canonical model(s) | Link | Applies to | Why a facet, not a field |
|-----------|--------------------|------|------------|--------------------------|
| Provenance | W3C PROV-O | MIX-IN | every Object | Who asserted it, when, derived from what — about the data |
| Valid-time / Temporal validity | OWL-Time · MU Lifecycle | MIX-IN | every versioned Object | Orthogonal to domain payload |
| Usage / Access Policy | W3C ODRL | MIX-IN | Contract, Projection, Dataset | Governs use, not content |
| Security / Classification Marking | data-classification labels | MIX-IN | any sensitive Object | Handling concern across domains |
| Multilingual Labels | SKOS-XL · RDF langString | MIX-IN | any labelled concept | Same concept, many languages |
| Meaning Annotation | SKOS concept · schema type | ANNOTATE | any Property | Fixes meaning without structure |

---

# 8. R7 — Upper Ontologies & Foundations (default: ALIGN / ANNOTATE)

Provide ontological grounding under domain models. Align or annotate against them;
they are not nested.

| Connector | Canonical model(s) | Link | Role | Note |
|-----------|--------------------|------|------|------|
| Top-Level Ontology | BFO (ISO/IEC 21838-2) · DOLCE | ALIGN | R7 | Grounds domain root types (continuant/occurrent, etc.) |
| Process / Plant Upper Model | ISO 15926 upper | ALIGN | R7 | 4D grounding for industrial/process domains |
| Logic Substrate | ISO/IEC 24707 Common Logic | ALIGN | R7 | Axiom interchange under ontologies |

> **R6 Aggregate / Document** models (UBL Invoice, C-CDA, EPCIS Event, Order) and
> **R8 Mapping / Lifting** tooling (R2RML, RML, SAWSDL) are not connectors to embed:
> R6 models *compose* the connectors above into a document, and R8 models *implement*
> the MAP mechanism. They appear in the [Registry](External-Models-Registry.md) but
> are out of scope as embed/reference targets.

---

# 9. Using a Connector

1. Identify the concept's **kind** via the rubric
   ([Meta-Model-Composition §5](../02-architecture/Meta-Model-Composition.md)).
2. Find the matching connector here; note its role and default link.
3. Import the canonical model as a [Semantic Package](../02-architecture/Extension-Model.md)
   (for EMBED/EXTEND) or record the scheme URI + version (for REFERENCE).
4. Declare the Property's **composition kind** and the connector identifier/version
   ([Meta-Model-Composition §8](../02-architecture/Meta-Model-Composition.md)).
5. For federation across heterogeneous models, publish a
   [Semantic Mapping](../03-federation/Semantic-Mapping.md) to the connector as the
   canonical meaning.

---

# Final Statement

These connectors are the joints of the Meta-Universe. Wiring a Meta-Model to them —
embedding the value objects, referencing the entities and code lists, mixing in the
facets — is what lets a thousand independently authored standards be used together
without duplicating a single field or surrendering a single authority.
