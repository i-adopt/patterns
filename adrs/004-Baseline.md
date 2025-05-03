# Baseline of Observation

* Status: decision taken
* Date: 2025-05-03
* Discussion:

## Context

It might be to precise how the property should be interpreted, for example when the property needs to have a baseline.

## Decision

We decided to go for Option A: to be able to constrain all description components, including properties

## Considered Options

### Option A: Constrained property

The property is constrained with a Constraint to describe that the property has a baseline.

![baseline](https://github.com/i-adopt/patterns/raw/main/adrs/004/baseline.drawio.svg)

* **Pros**:
  * Does not require more complex structures
  * Possibly dedicated subclass of `Constraint` for baselines
* **Cons**
  * Constraints are currently not well-defined
  * Requires a change of the ontology


### Option B: Using system for the object of interest

The object of interest is represented as a system of two entities where one is the baseline of the observation.

![system](https://github.com/i-adopt/patterns/raw/main/adrs/004/systemreference.drawio.svg)

* **Pros**:
  * In line with the other asymmetric system pattern
* **Cons**
  * Requires additional object properties

