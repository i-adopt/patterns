# Handling of Flux-related Variables

* Status: proposed
* Date: 2025-03-11
* Discussion:

## Context

There are several flux- or flow-related kinds of variables.
This includes variables where immaterial properties (like energy) are exchanged and those involving an actual flow of material (like nitrogen).

So far, both kinds of flux/flow were treated differently depending on whether there is a material entity being exchanged.
This resulted in different patterns for both cases.

Decision here is about whether those two kinds of flux/flow should follow the same pattern or a sufficiently dissimilar that they need to follow different patterns in modelling.

## Decision

*pending*

## Considered Options

### Option A: Same Pattern for all Flux-/Flow-related Variables

All variables use the same pattern:
The "thing" flowing is assigned to the `ObjectOfInterest` while the medium or start and end of the flow is encoded in the `Matrix`.

![visual display Option A](./005/OptionA.drawio.svg)

* **Pros**:
  * Harmonized structure across flux-/flow-related variables.
* **Cons**
  * Some redundance in the description of, e.g., energy-fluxes.
    * For energy-flux, there are dedicated quantity kinds (e.g., in [QUDT](https://qudt.org/vocab/quantitykind/EnergyFluence)).
      Adding `Energy` as the `ObjectOfInterest` adds some redundancy to this.


### Option B: Pattern depending on the Type of a Flux-/Flow-related Variable

Patterns depend on whether the exchanged entity is material or immaterial.

For material exchanges, the material itself would be encoded as the `ObjectOfInterest`.
Here, source and sink would be encoded in the `Matrix`.

For immaterial exchanges, the object of interest is given by both Source and sink in the `ObjectOfInterest`.

![visual display Option B](./005/OptionB.drawio.svg)

* **Pros**:
  * Less redundancy for variables that describe the exchange of properties.
* **Cons**
  * Might require discussions about the nature of the exchanged entity.
