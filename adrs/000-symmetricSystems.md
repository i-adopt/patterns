# Symmetric Systems for `ObjectOfInterest` and `Matrix`

* Status: proposed
* Date: 2025-02-23
* Discussion:
  * [examples #14](https://github.com/i-adopt/examples/issues/14)

## Context

Some observable properties can not associated with a single `ObjectOfInterest` but pertain to multiple ones and describe their relationship.
Here, we consider cases where there are no specific roles for the involved participants or those can be exchanged without affecting the measurement itself.

As an example consider the distance of planets to their central star.
In this case the distance is a symmetric property of a system consisting out of a planet and the central star.
Further, the distance from a planet to its central star is the same property as the distance of a central star to its planet (for most intents and purposes).

This is different from [asymmetric systems](./001-asymemetricSystems.md) where the role of involved objects can not be freely exchanged.

## Decision

*pending*

## Considered Options

### Option A: Combined `ObjectOfInterest`

Both (all) involved objects are combined into a system.
The observation then describes an observable property of this system.

(specific relations to be used, still to be decided)
```turtle
ex:DistanceOfPlanetAndStar
  a                          iadopt:Variable ;
  iadopt:hasProperty         qudt:Distance ;
  iadopt:hasObjectOfInterest [
    ex:hasPart ex:Planet ;
    ex:hasPart ex:Star ;
  ] .
```

![visual display Option A](./000/optionA.drawio.svg)

* **Pros**:
  * Symmetric representation of both (/all) involved objects
    * during search no decision about specific roles
* **Cons**
  * Nesting of `ObjectOfInterest` &rarr; slightly more complex SPARQL queries

### Option B: Using `ContextObject`

Select one involved object and make it the central point of focus in this observation (`ObjectOfInterest`).
Other objects are them moved to `ContextObject`.

```turtle
ex:DistanceOfPlanetAndStar
  a                          iadopt:Variable ;
  iadopt:hasProperty         qudt:Distance ;
  iadopt:hasObjectOfInterest ex:Planet ;
  iadopt:hasContextObject    ex:Star .
```

![visual display Option B](./000/optionB.drawio.svg)

* **Pros**:
  * Flat structure, no nesting necessary
  * Closer to pattern for Concentration
* **Cons**
  * More complex search - "in a system, which object has been selected for `ObjectOfInterest`?"
    * can likely by mitigated by a search system
  * In case of more than 2 participants, would not allow to distinguish their roles within the set of `ContextObject`s

### Option C: Considering a (virtual) `ObjectOfInterest`

Following the example, we can consider a virtual path between star and planet as the `ObjectOfInterest` and the observe one property of this, it's length.

```turtle
ex:DistanceOfPlanetAndStar
  a                          iadopt:Variable ;
  iadopt:hasProperty         qudt:Length ;
  iadopt:hasObjectOfInterest ex:PathBetweenPlanetAndStar .
```

![visual display Option C](./000/optionC.drawio.svg)

* **Pros**:
  * Ontologically cleaner solution (compared to Options A or B)
* **Cons**
  * Requires more mental effort to consider a property of the relation between two or more objects as the property of a (virtual) object connecting them.
    * would further require describing the virtual object (ie., describe its constituents), effectively making this quite similar to Option A
  * Might need a switch of `Property` (e.g., from `Distance` to `Length`)
