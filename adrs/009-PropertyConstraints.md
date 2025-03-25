# Constraints of Property or not

* Status: proposed
* Date: 2025-03-25
* Discussion:

## Context

The I-ADOPT Ontology does not allow to use `Constraint` on `Property` but we got requests to change this. 


## Decision

*pending*

## Considered Options

### Option A: Keep it as it is now

We leave the `Property` without `Constraint`, making it necessary to specialize `Properties`. E.g. "downwelling radiation"

* **Pros**:
  * No change required.
* **Cons**
  * Requires many specialized `Properties`.


### Option B: Allow constraints on `Properties` 

Examples: Radiation as `Property` with a `Constraint` on it ("downwelling", "upwelling", "longwave", shortwave")

* **Pros**:
  * Easier to establish relations between `Properties`.
* **Cons**
  * More complex `Variable`s due to `Constraint`s being involved.
  * Change of the I-ADOPT ontology required
