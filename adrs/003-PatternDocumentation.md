# Documentation of the pattern used

* Status:  proposed
* Date: 2025-03-10
* Discussion: 

## Context

The documentation of the pattern used might be useful for associating the logic used to decompose a variable with the actual variable description.

## Decision

*pending*

## Considered Options

### Option A: Pattern as abstract variable

The pattern is described as an abstract variable and published as a machine-readable representation. It is retrievable via its persistent identifier. A library of patterns is published centrally. See e.g.: 

![description option A](./003/pattern.jpg)

* **Pros**:
  * might be helfpul for the service development, as this would require to say which pattern was used.
  * might help also other implementers to understand how this was done.
* **Cons**
  * additional object property needed.

## Considered Options

### Option B: Using sub-properties instead of pattern descriptions

The pattern is translated into subproperties, like "hasSolute" for hasObjectOfInterest or "hasSolvent" for hasMatrix

* **Pros**:
  * you can use the classical queries
* **Cons**
  * it requires many more object properties

### Option C: Describe in skos:notion the pattern

The pattern is described in the notion field of the Variable as simple text.

* **Pros**:
  * it is easy to implement
* **Cons**
  * it is hard to query
  * it is not machine-readable
