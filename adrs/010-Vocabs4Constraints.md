# Use of Vocabulary terms for Constraints in Variable descriptions

* Status: proposed
* Date: 2025-07-21
* Discussion:
* [Example sick child](https://github.com/w3c/sdw-sosa-ssn/issues/347#issuecomment-3081992665)

## Context

The use of vocabulary terms for Constraints in Variable descriptions was never fully defined. A Constraint must be defined by targeting a description component. But if you use a vocabulary term for this Constraint it cannot be used in other variables. So a generic class from a semantic resource cannot be used directly for the constraint.

First of all the constraint should be modelled as a separate node (named or blank) for each Constraint and Variable. To reuse a generic concept we have three options. The example we are using to illustrate the solutions is: Temperature of a sick child. 

## Decision

pending

## Considered Options

### Option A: Using a separate relation (iop:hasConstraintType) to link to the generic concept

<img width="303" height="96" alt="image" src="https://github.com/user-attachments/assets/0df6253e-43db-4f09-be65-3d33f331e541" />

* **Pros**:
  * Makes it possible to reuse a concept from a semantic resource ([sio](http://semanticscience.org/resource/SIO_000954) in this case)
* **Cons**
  * requires a new relation and a new class, which is not necessary

### Option B: Using rdfs:subClassOf instead: 

<img width="303" height="87" alt="image" src="https://github.com/user-attachments/assets/72c67fdb-24fd-4e2a-b10d-3ec1a18de86a" />


* **Pros**:
  * Makes it possible to reuse a concept from a semantic resource ([sio](http://semanticscience.org/resource/SIO_000954) in this case)
* **Cons**
  * it adds complexity

### Option C: Using rdf:type and inherit from two classes

<img width="296" height="73" alt="image" src="https://github.com/user-attachments/assets/182ad632-81b3-48d0-8c5d-90aa29ed071b" />


* **Pros**:
  * Natural way to describe is of type without having to introduce a new relation
* **Cons**
  * none


