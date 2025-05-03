# Hierarchy of Variables

* Status: Decision taken
* Date: 2025-05-03
* Discussion:

## Context

There are frequent relations between `Variable`s in which one `Variable` is a specialization of the other.
This may be due to another `Constraint` being applied or a narrower definition for an `Entity` being used.
The result are multiple hierarchies in which a single `Variable` can be part of multiple hierarchies.
If all permutations are available, generalizing on each individual `Entity` separately results in different parent nodes in the hierarchy.
Effectively, this results in a poly-hierarchy being build.

While some of these relations can be extracted from the corresponding description, it would be easier to make those relations explicit.

## Decision

We decided to go for option A: skos:broader

## Considered Options

### Option A: Use SKOS for Building Hierarchies

[SKOS](https://www.w3.org/TR/skos-reference/) properties like `skos:broader` and `skos:narrower` can be used to describe the relation of two `Variable`s.

* **Pros**:
  * Simpler queries to retrieve all specializations of a given `Variable`.
  * Allows for transitive use of the used properties ("derive children of children").
* **Cons**
  * Redundant information in many cases, as the relation can be deduced from the relation of the atomic components and constraints.
  * Using SKOS effectively makes all `Variable`s to `skos:Concept`s.

### Option B: Use Custom (I-Adopt) Properties for Building Hierarchies

Similarly to Option A, but instead of using SKOS as a basis, there would be specific properties within the I-Adopt namespace

* **Pros**
  * (see above)
  * Not inherit SKOS-related facts (e.g., membership in `skos:Concept`)
* **Cons**
  * (see above)
  * Redundancy in definition; fail to reuse existing terminology
