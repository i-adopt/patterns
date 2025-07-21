# Use of Vocabulary terms for Constraints in Variable descriptions

* Status: proposed
* Date: 2025-07-21
* Discussion:
* [Example sick child](https://github.com/w3c/sdw-sosa-ssn/issues/347#issuecomment-3081992665)

## Context

The use of vocabulary terms for Constraints in Variable descriptions was never fully defined.
A Constraint has to be defined by linking it to a Variable component.
When directly reusing a vocabulary term here, that term cannot be used in other variables:
The association to the Variable and component cannot be reliably reconstructed.
```turtle
ex:SickChildTemperature iop:hasConstraint sio:Sick .

sio:Sick iop:constrains ex:Child .
```

So in consequence, Constraints should be modelled as separate nodes (named or blank) for each Constraint and Variable.
Here, several options are possible.
This is independent of Constraint that, e.g., restrict temporal or spatial coverage.
Those have to restricted differently.

## Decision

pending

## Considered Options

### Option A: Using a separate relation (`iop:hasConstraintType`) to link to the generic concept

```turtle
ex:SickChildTemperature iop:hasConstraint [
  a iop:Constraint ;
  iop:hasConstraintType sio:Sick ;
  iop:constrains ex:Child
] .
```

* **Pros**:
  * enables linking to a concept from a semantic resource
  * clear separation between I-Adopt relations and common RDF-/OWL-constructs (not overloading existing relations)
* **Cons**
  * requires a new relation
  * replicates the semantics of `rdf:type` using a custom relation (applied in a restricted setting though)


### Option B: Using `rdfs:subClassOf`

```turtle
ex:SickChildTemperature iop:hasConstraint [
  a iop:Constraint ;
  rdfs:subClassOf sio:Sick ;
  iop:constrains ex:Child
] .
```

* **Pros**:
  * enables linking to a concept from a semantic resource
  * closest to the "direct use of generic concept" approach
* **Cons**
  * mixes instance and class relations within a single concept


### Option C: Using `rdf:type`

```turtle
ex:SickChildTemperature iop:hasConstraint [
  a iop:Constraint, sio:Sick ;
  iop:constrains ex:Child
] .
```

* **Pros**:
  * enables linking to a concept from a semantic resource
  * reusing the standard semantics of `rdf:type`
* **Cons**
  * ?
