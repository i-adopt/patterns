# Statistical Modifiers

* Status: proposed
* Date: 2025-03-11
* Discussion:

## Context

A recurring aspect of observations are statistical modifiers to the result.
For example, this might declare a `Variable` to be the minimum, maximum, or average across a certain span of time.


## Decision

*pending*

## Considered Options

### Option A: Omit from Variable

A statistical modifier can be seen as part of the method of deriving a `Variable`.
Observation methods have specifically been excluded from `Variable` descriptions, so in this view statistical modifiers would need to be excluded as well.

![visual display Option A](./006/OptionA.drawio.svg)

* **Pros**:
  * Consequently keeping the "no-method-policy".
* **Cons**
  * Neglects an important aspect of `Variable`s.
  * Inability to distinguish, e.g., between min- and max-temperature.


### Option B: Constraint Property

The statistical modifier can be modelled using a `Constraint` on the `Property` of a `Variable`.

![visual display Option B](./006/OptionB.drawio.svg)

* **Pros**:
  * No changes to current ontology needed.
* **Cons**
  * Rather hidden representation.


### Option C: Introduce new Top-Level Class

The modifier can be introduced as a new (optional) component of a `Variable`.

![visual display Option C](./006/OptionC.drawio.svg)

* **Pros**:
  * Intuitive representation.
* **Cons**
  * Needs extension of the ontology.
  * Needs clear distinction from (still unsupported) other methods.
  * Needs vocabulary to represent (at least) common statistical modifiers.


### Option D: Specialized Properties

In a variation of [ADR-007](./007-ConstraintVsSubconcept.md) and as a complement to Option B, additional subclasses for the corresponding properties could be derived.

For example, this would require a `Minimum Temperature` and `Maximum Temperature` as subclasses of `Temperature`.

![visual display Option D](./006/OptionD.drawio.svg)

* **Pros**:
  * More concise `Variable`s.
  * No change of current ontology or other patterns.
* **Cons**
  * Likely would need an large extension of terminologies for `Property`s.
  * Deviates from the atomic component principle where components of a `Variable` should be decomposed to make them more accessible.
