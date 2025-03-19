# Constraints vs. Subconcepts

* Status: proposed
* Date: 2025-03-18
* Discussion:

## Context

In modelling often there is a decision between choosing a more general `Entity` in conjunction with a `Constraint` versus using a more specialized `Entity`.
Without guidelines this can lead to two `Variable`s using the same terminologies but still differing in their use of `Constraint`s and, hence, making it harder to establish their equivalency.

## Decision

*pending*

## Considered Options

### Option A: Default to Specialized

Via guidelines, users are strongly encouraged to use specialized `Entities` wherever possible.

* **Pros**:
  * Less complex `Variable`s due to less objects needed to describe a `Variable`.
* **Cons**
  * Harder to determine related `Entity`s that only differ by `Constraint`s.


### Option B: Default to Generalized plus Constraint

Via guidelines, users are strongly encouraged to use more general `Entities` in conjunction with `Constraint`s wherever possible.

* **Pros**:
  * Easier to establish relations between `Variable`s (e.g., see [ADR-008 Hierarchies](./008-HierarchiesOfVariables.md)).
* **Cons**
  * More complex `Variable`s due to `Constraint`s being involved.

### Option C: Formalize Translation

If for one `Entity` both representations are possible, a formal way of representing their relation can be established.
Basically boiling down to a semantic representation of `X + [constraint] ⟷ Y`.

* **Pros**:
  * Allow for both options depending on user preference or context.
  * Machine-readable relation between different `Entity`s.
* **Cons**
  * Effort needed to establish relations - yet another level of detail to be stored.
  * Requires new properties (possibly reused from somewhere) to represent relation.
