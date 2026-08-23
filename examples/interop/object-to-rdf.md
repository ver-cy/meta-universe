# Object → RDF / OWL Projection

**Meta-Universe Specification**

**Document ID:** MU-V2-EX-011  
**Title:** Worked Appendix — Projecting a MUIF Object to RDF and OWL  
**Document Class:** Informative  
**Version:** 2.0 (Draft)  
**Status:** Working Draft  
**Normative References:** None  
**Informative References:** [MMAS-Interchange](../../02-architecture/MMAS-Interchange.md), [Object](../../04-core-concepts/Object.md), [Projection](../../04-core-concepts/Projection.md), [Semantic-Mapping](../../03-federation/Semantic-Mapping.md)  
**Copyright:** © Vercy  
**License:** Apache-2.0

---

# 1. Purpose

A MUIF [Object](../../04-core-concepts/Object.md) is a single Semantic Point of Truth. A
[Projection](../../04-core-concepts/Projection.md) is how that Object appears in a given
context. An RDF graph and an OWL ontology are two such contexts: this appendix shows how
the same `employee.person` Object projects into each, so a Semantic-Web consumer can read
it without learning MUIF.

This is a *projection*, not a redefinition: the Object remains authoritative in the
Meta-Model, and the RDF/OWL forms are derived views governed by the
[Semantic Mappings](person-mappings.json) in this appendix.

---

# 2. The source Object

The running example is the `employee.person` Object (the same one used across this
appendix and in [`../federation-acme-govtax`](../federation-acme-govtax/)):

```json
{
  "muifType": "Object",
  "id": "employee:Person",
  "csn": "employee.person",
  "kind": "Entity",
  "namespace": "employee",
  "provenance": { "owner": "urn:mu:universe:acme" },
  "properties": [
    { "name": "employee.givenName",  "valueType": "string", "required": true },
    { "name": "employee.familyName", "valueType": "string", "required": true },
    { "name": "employee.birthDate",  "valueType": "date",   "required": false }
  ]
}
```

For the projection we bind two prefixes:

```text
@prefix emp:  <https://acme.example/ns/employee#> .
@prefix mu:   <https://meta-universe.org/ns/core#> .
```

---

# 3. Projection (a) — RDF triples (Turtle)

The Object projects to RDF in two parts: the **schema** triples (the class and its
properties as terms) and an **instance** showing one individual. The mappings from
[`person-mappings.json`](person-mappings.json) are emitted as `owl:equivalentClass` /
`rdfs:subClassOf` and `owl:equivalentProperty` links so the graph stays connected to the
external standards.

```turtle
@prefix emp:   <https://acme.example/ns/employee#> .
@prefix mu:    <https://meta-universe.org/ns/core#> .
@prefix schema:<https://schema.org/> .
@prefix foaf:  <http://xmlns.com/foaf/0.1/> .
@prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl:   <http://www.w3.org/2002/07/owl#> .
@prefix xsd:   <http://www.w3.org/2001/XMLSchema#> .

# --- schema: the Object as an RDF class ---
emp:Person a rdfs:Class, owl:Class ;
    rdfs:label "Employee Person" ;
    mu:csn "employee.person" ;
    mu:owner <urn:mu:universe:acme> ;
    rdfs:subClassOf schema:Person ;      # employee.person is narrower than schema:Person
    rdfs:subClassOf foaf:Person .

emp:givenName a rdf:Property, owl:DatatypeProperty ;
    rdfs:domain emp:Person ;
    rdfs:range xsd:string ;
    owl:equivalentProperty schema:givenName, foaf:givenName .

emp:familyName a rdf:Property, owl:DatatypeProperty ;
    rdfs:domain emp:Person ;
    rdfs:range xsd:string ;
    owl:equivalentProperty schema:familyName, foaf:familyName .

emp:birthDate a rdf:Property, owl:DatatypeProperty ;
    rdfs:domain emp:Person ;
    rdfs:range xsd:date ;
    owl:equivalentProperty schema:birthDate .

# --- instance: one employee.person individual ---
<urn:mu:object:acme:person:42> a emp:Person ;
    emp:givenName  "Ada" ;
    emp:familyName "Lovelace" ;
    emp:birthDate  "1815-12-10"^^xsd:date .
```

A consumer who only speaks Schema.org or FOAF can follow the `owl:equivalentProperty` and
`rdfs:subClassOf` links and read the individual entirely through their own vocabulary.

---

# 4. Projection (b) — OWL class

The same Object projects to an OWL class definition. Required MUIF properties become
`owl:Restriction` cardinality constraints; optional ones do not. Functional-Syntax is used
here for clarity, with the same prefixes as Section 3.

```text
Class: emp:Person

    Annotations:
        rdfs:label "Employee Person",
        mu:csn "employee.person"

    SubClassOf:
        schema:Person,                              # narrower than the Schema.org concept
        foaf:Person,

        # required: employee.givenName  (exactly 1 string)
        emp:givenName exactly 1 xsd:string,

        # required: employee.familyName (exactly 1 string)
        emp:familyName exactly 1 xsd:string,

        # optional: employee.birthDate  (0..1 date)
        emp:birthDate max 1 xsd:date

DatatypeProperty: emp:givenName
    EquivalentTo: schema:givenName, foaf:givenName
    Domain: emp:Person
    Range:  xsd:string

DatatypeProperty: emp:familyName
    EquivalentTo: schema:familyName, foaf:familyName
    Domain: emp:Person
    Range:  xsd:string

DatatypeProperty: emp:birthDate
    EquivalentTo: schema:birthDate
    Domain: emp:Person
    Range:  xsd:date
```

---

# 5. What is preserved across the projection

| MUIF concept | RDF / OWL projection |
|--------------|----------------------|
| Object `employee:Person` | `emp:Person` as `owl:Class` |
| `csn` / `provenance.owner` | `mu:csn` / `mu:owner` annotations |
| Property (`required: true`) | `owl:DatatypeProperty` + `exactly 1` restriction |
| Property (`required: false`) | `owl:DatatypeProperty` + `max 1` restriction |
| Mapping `relation: equivalent` | `owl:equivalentProperty` |
| Mapping `relation: broader` (target) | `rdfs:subClassOf` (local ⊑ external) |

The projection is **lossless for meaning and lossy for nothing semantic**: identity,
ownership, required-ness and the external mappings all survive. As with every Projection,
the RDF/OWL forms are derived views; the authoritative truth stays in the MUIF Object.

---

# 6. See also

- [`schemaorg-person.import.json`](schemaorg-person.import.json) — the Schema.org import that makes `schema:Person` available as a Semantic Package.
- [`person-mappings.json`](person-mappings.json) — the field-by-field mappings emitted above as `owl:equivalentProperty` / `rdfs:subClassOf`.
- [MMAS-Interchange](../../02-architecture/MMAS-Interchange.md) — the MUIF document model these Objects come from.
