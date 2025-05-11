# Asymmetric Systems for `ObjectOfInterest` and `Matrix`

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

Could also be used for fluxes between two environmental compartments: see [Carbon dioxide molar flux between peatland and atmosphere](https://w3id.org/ozcar-theia/c_405693da)


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


### Option D: Constrain the `ObjectOfInterest`

(after [examples#16](https://github.com/i-adopt/examples/issues/16))

This uses a system as the `ObjectOfInterest` but unlike [Option A](#option-a-combined-objectofinterest) then uses `Constraint`s to connect components to that.

```turtle
ex:RatioOfOxygen18toOxygen16
  a                          iadopt:Variable ;
  iadopt:hasProperty         qudt:Ratio ;
  iadopt:hasObjectOfInterest ex:Oxygen-18 ;
  iadopt:hasConstraint [
    a                 iadopt:Constraint ;
    iadopt:constrains ex:Oxygen-18-to-Oxygen-16 ;
    ex:hasComponent      ex:Oxygen-16 ;
    ex:hasRole           ex:Denominator
  ] ;
  iadopt:hasConstraint [
    a                 iadopt:Constraint ;
    iadopt:constrains ex:Oxygen-18-to-Oxygen-16 ;
    ex:hasComponent      ex:Oxygen-18 ;
    ex:hasRole           ex:Numerator
  ] .

ex:Oxygen-18-to-Oxygen-16
  a           iadopt:Entity ;
  rdfs:label  "Oxygen-18 / Oxygen-16" .
```

![visual display Option C](./001/optionD.drawio.svg)

* **Pros**:
  * ?
* **Cons**
  * Structurally similar to [Option A](#option-a-combined-objectofinterest) but requires more additional relationships and concepts to describe the structure.
  * `Variable` and `ObjectOfInterest` are almost identical.

### Option E: Add Top Level Properties

Similar to Option A but removing the intermediate node representing the system in its entirety.

Notes:
* possibly, `iadopt:hasObjectOfInterestNumerator` etc. are sub-properties of `iadopt:hasObjectOfInterest` in this case. However, this would have implications on cardinalities.
* The use of "system-properties" replaces the use of `iop:hasObjectOfInterest` or `iop:hasMatrix` depending on which context they are used in.

```turtle
ex:DistanceOfPlanetAndStar
  a                                     iadopt:Variable ;
  iadopt:hasProperty                    qudt:Length ;
  iadopt:hasObjectOfInterestNumerator   ex:Oxygen-18 ;
  iadopt:hasObjectOfInterestDenominator ex:Oxygen-16 .
```

![visual display Option E](./001/optionE.drawio.svg)

* **Pros**:
  * Flat structure, does not need intermediate objects (systems)
  * does not require new system classes/instances
  * (Consistent with [Option D in ADR 001](./001-asymmetricSystems.md#option-e-add-top-level-properties))
* **Cons**
  * Requires to create equivalent properties for each role.
  * If applied to `iadopt:ContextObject`s, only allows for at most one
