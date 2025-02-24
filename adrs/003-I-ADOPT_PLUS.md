# [I-ADOPT PLUS]

* Status: proposed
* Date: 2025-02-24
* Discussion: [examples #13](https://github.com/i-adopt/examples/issues/13)

## Context

Suggestion on how to add additional description components as extensions of I-ADOPT variables. For convenience, we use I-ADOPT Plus for this type of extension.

## Decision

*pending*

## Considered Options

### Option A: [short title]

 * [I-ADOPT Plus](I-ADOPT_plus.jpg)

This approach would require to model a variable as a child of an existing I-ADOPT Variable as demonstrated in this EnvThes example [here](http://vocabs.lter-europe.net/EnvThes/30282). It is not possible to add these extensions (like statistical measures) as constraints, because these apply to the whole variable. 
In EnvThes we have added for now these extensions:
* https://w3id.org/env/puv#statistic for adding statistical measures
* https://w3id.org/env/puv#usesMethod for adding a method
* https://w3id.org/env/puv#uom for adding the used unit
* http://www.w3.org/ns/sosa/madeBySensor for adding the instrument

* **Pros**:
  * easy to implement
* **Cons**
  * not standardised which object properties should be used, but we could write guidelines


# I-ADOPT Plus
Suggestion on how to add additional description components as extensions of I-ADOPT variables.
 * [I-ADOPT Plus](I-ADOPT_plus.jpg)

This approach would require to model a variable as a child of an existing I-ADOPT Variable as demonstrated in this EnvThes example [here](http://vocabs.lter-europe.net/EnvThes/30282). It is not possible to add these extensions (like statistical measures) as constraints, because these apply to the whole variable. 
In EnvThes we have added for now these extensions:
* https://w3id.org/env/puv#statistic for adding statistical measures
* https://w3id.org/env/puv#usesMethod for adding a method
* https://w3id.org/env/puv#uom for adding the used unit
* http://www.w3.org/ns/sosa/madeBySensor for adding the instrument

However, we would be possible, if we would allow properties to be constrained. 
