# Baseline

* Status: proposed
* Date: 2025-03-10
* Discussion:

## Context

It might be to precise how the property should be interpreted, for example when the property needs to have a baseline.

## Decision

*pending*

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

