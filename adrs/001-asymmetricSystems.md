# Asymmetric Systems for `ObjectOfInterest`

* Status: proposed
* Date: 2025-02-23
* Discussion:
  * [examples #16](https://github.com/i-adopt/examples/issues/16)

## Context

Some observable properties can not associated with a single `ObjectOfInterest` but pertain to multiple ones and describe their relationship.
Here, we consider those cases where each participant has a specific role in that relationship.
Changing those roles would then alter the observation itself.

As an example consider the ratio of Oxygen-18 to Oxygen-16.
Here, Oxygen-18 is assigned the role of numerator while Oxygen-16 is the denominator in the computation of this ratio.

This is different from [symmetric systems](./000-symmetricSystems.md) where the role of involved objects can be freely exchanged.

## Decision

*pending*

## Considered Options

### Option A: Combined `ObjectOfInterest`

Both (all) involved objects are combined into a system.
The observation then describes an observable property of this system.
The role of each participant would be encoded within the relationships used to construct the system.

(specific relations to be used, still to be decided)
```turtle
ex:RatioOfOxygen18toOxygen16
  a                          iadopt:Variable ;
  iadopt:hasProperty         qudt:Ratio ;
  iadopt:hasObjectOfInterest [
    ex:hasNumerator   ex:Oxygen-18 ;
    ex:hasDenominator ex:Oxygen-16 ;
  ] .
```

![visual display Option A](./001/optionA.drawio.svg)

* **Pros**:
  * Possibly consistent with Option A of [symmetric systems](./000-symmetricSystems.md)
* **Cons**
  * May require a rather large set of custom relations for the roles to represent all possible roles in such cases.

### Option B: Using `ContextObject`

By convention, select the numerator for `ObjectOfInterest` and the denominator for `ContextObject`.

```turtle
ex:RatioOfOxygen18toOxygen16
  a                          iadopt:Variable ;
  iadopt:hasProperty         qudt:Ratio ;
  iadopt:hasObjectOfInterest ex:Oxygen-18 ;
  iadopt:hasContextObject    ex:Oxygen-16 .
```

![visual display Option B](./001/optionB.drawio.svg)

* **Pros**:
  * Follows the same principle for modelling concentrations (which is similar in structure, anyway)
* **Cons**
  * In case of more than 2 participants, would not allow to distinguish their roles within the set of `ContextObject`s


### Option C: Constrain the `Property`

Select a focus participant as the `ObjectOfInterest` and use `Constraint`s on the `Property` to represent roles of all other participants.

```turtle
ex:RatioOfOxygen18toOxygen16
  a                          iadopt:Variable ;
  iadopt:hasProperty         qudt:Ratio ;
  iadopt:hasObjectOfInterest ex:Oxygen-18 ;
  iadopt:hasConstraint [
    a                 iadopt:Constraint ;
    iadopt:constrains qudt:Ratio ;
    ex:denominator    ex:Oxygen-16 ;
  ] .
```

![visual display Option C](./001/optionC.drawio.svg)

* **Pros**:
  * Allows for multiple participants (assuming each role has a unique relation)
* **Cons**
  * Requires the ability to use `Constraint`s on `Property`s which is not yet possible within I-Adopt
  * Would still require additional relations to encode the role within the `Constraint` (see Option A)
