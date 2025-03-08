# I-ADOPT extended or a separate model to add other description elements not included in I-ADOPT

* Status: proposed
* Date: 2025-02-24
* Discussion: [examples #13](https://github.com/i-adopt/examples/issues/13)

## Context

Suggestion on how to add additional description components as extensions of I-ADOPT variables. For convenience, we use I-ADOPT Plus for this type of extension.

## Decision

*pending*

## Considered Options

### Option A: PLUS extension

![I-ADOPT Plus](002/I-ADOPT_plus.jpg)

This approach would require to model a variable as a child of an existing I-ADOPT Variable as demonstrated in this EnvThes example [here](http://vocabs.lter-europe.net/EnvThes/30282). It is not possible to add these extensions (like statistical measures) as constraints, because these apply to the whole variable. 
In EnvThes we have added for now these extensions:
* https://w3id.org/env/puv#statistic for adding statistical measures
* https://w3id.org/env/puv#usesMethod for adding a method
* https://w3id.org/env/puv#uom for adding the used unit
* http://www.w3.org/ns/sosa/madeBySensor for adding the instrument

![I-ADOPT PLUS implemented in Envthes](002/EnvThes_I-ADOPT_plus.jpg)

* **Pros**:
  * easy to implement
* **Cons**
  * not standardised which object properties should be used, but we could write guidelines

### Option B: Complementing I-ADOPT with ISO 19131 

By using ISO 19131 - Data Product Specification (DPS), requirements for products description can be taken into account.

![Product](002/Product.jpg)

* **Pros**:
  * OMS ObservingProcedure (+ requirements) could be used to better describe the DataCaptureInformation from the DPS which intends to explain how the data needs to be captured.
  * EBV products can be easily created.
    
* **Cons**
  * what are the object properties that can be used for these relationships captured in the UML?
    
### Option C: Constrain on Property
Suggestion on how to add additional description components as constrains of the property

This approach would require to model a variable using constrains of the property. 

* **Pros**:
  * Align it with Entities that can also be constrained in I-ADOPT.
* **Cons**
  * This would require a change of the I-ADOPT ontology.
  * Constrains are not easy to be queried

