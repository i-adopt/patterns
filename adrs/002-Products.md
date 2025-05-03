# Products - Variables with more context beyond I-ADOPT

* Status: decided
* Date: 2025-05-03
* Discussion: [examples #13](https://github.com/i-adopt/examples/issues/13)

## Context

Suggestion on how to add additional description components as extensions of I-ADOPT variables. 

## Decision

We decided to go for option A1 - to only include a statistical modifier in the I-ADOPT ontology, but everything else remains outside the ontology. 

## Considered Options

### Option A: Extending I-ADOPT 

#### Option A1: Extending I-ADOPT for modifier only
This approach would require to extend I-ADOPT with an additional object property for statistical modifiers and an additional class for modifiers (could be a controlled list, we provide) which should only be used to indicate the aggregation value as provided by sensors to allow to include this information to the variable. It is not possible to add these extensions (like statistical measures) as constraints, because these apply to the whole variable. 

![I-ADOPT Plus](002/002A.drawio.svg)

* **Pros**:
  * easy to implement
* **Cons**
  * modifiers could be misused to representy any postprocessing aggregation after the observation, which is not the scope of I-ADOPT
  * a new class and a new property would be required
 
#### Option A2: Extending I-ADOPT with external object properties
We could use object properties from other ontologies like PUV or SOSA, see
* https://w3id.org/env/puv#statistic for adding statistical measures
* https://w3id.org/env/puv#usesMethod for adding a method
* http://www.w3.org/ns/sosa/madeBySensor for adding the instrument
* https://w3id.org/env/puv#uom for adding the used unit 

See an example in EnvThes [here](http://vocabs.lter-europe.net/EnvThes/30282):

![I-ADOPT PLUS implemented in Envthes](002/EnvThes_I-ADOPT_plus.jpg)

* **Pros**:
  * easy to implement
* **Cons**
  * not standardised which object properties should be used, but we could write guidelines
  * might lead potentially to an explosion of descriptions (especially true for units!)
  * method is part of the observation procedure and not intended to be included in I-ADOPT

### Option B: Creating a concept on top of I-ADOPT (I-ADOPT PLUS):

Here we add these additional object properties in another concept (I-ADOPT PLUS) that links to an I-ADOPT Variable and additional components.

![I-ADOPT Plus](002/option002B.drawio.svg)

* **Pros**:
  * keeps I-ADOPT clean from other information
* **Cons**
  * not standardised which object properties should be used, but we could write guidelines
  * might lead potentially to an explosion of descriptions (especially true for units!)
  * namespace is not clear and outside of I-ADOPT governance

### Option C: Complementing I-ADOPT with ISO 19131 

By using ISO 19131 - Data Product Specification (DPS), requirements for products description can be taken into account. In this case the product description links to the I-ADOPT variable. This can be combined with Option A1.

![Product](002/Product.jpg)

* **Pros**:
  * OMS ObservingProcedure (+ requirements) could be used to better describe the DataCaptureInformation from the DPS which intends to explain how the data needs to be captured.
  * EBV products can be easily created.
    
* **Cons**
  * what are the object properties that can be used for these relationships captured in the UML?
    
