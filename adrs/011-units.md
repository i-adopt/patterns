# Integration of Units

* Status: proposed
* Date: 2026-06-23
* Discussion:


## Context

Units are integral part of observations.
There specific position within the description of such an observation can be discussed.
This ADR is concerned whether the unit of measure is part of an I-Adopt Variable or to be used alongside it.


## Decision

pending

## Related Approaches

For context, some anecdotal evidence from existing ontologies to describe observations are described in the following.
<!---
### The RDF Data Cube Vocabulary

[The RDF Data Cube Vocabulary](https://www.w3.org/TR/vocab-data-cube/) is a W3C recommendation to represent the content of data cubes (i.e. multidimensional collections of observations or data in general).

Although not part of the actual actual vocabulary, several examples provide a glimpse of how the authors envision the inclusion of units into their model.
In general, the unit is attached via `sdmx-attribute:unitMeasure` to either an individual observation or collections thereof in form of subclasses of `qb:DataSet`, `qb:ComponentProperty`, or `qb:Slice`.

The kind of a component is usually given via relations and is defined in the `qb:DataStructureDefinition`.

[Example 5 of the RDF Data Cube specification](https://www.w3.org/TR/vocab-data-cube/#h4_dsd-mm-obs) describing the structure of a dataset:

```turtle
eg:dsd1 a qb:DataStructureDefinition;
    rdfs:comment "shipments by time (multiple measures approach)"@en;
    qb:component
        [ qb:dimension  sdmx-dimension:refTime; ],
        [ qb:measure    eg-measure:quantity; ],
        [ qb:measure    eg-measure:weight; ] .
```

[Example 12 of the RDF Data Cube specification](https://www.w3.org/TR/vocab-data-cube/#h3_slices) describing an entire dataset:
```turtle
eg:dataset-le2 a qb:DataSet;
    rdfs:label "Life expectancy"@en;
    rdfs:comment "Life expectancy within Welsh Unitary authorities - extracted from Stats Wales"@en;
    qb:structure eg:dsd-le-slice2 ;
    sdmx-attribute:unitMeasure <http://dbpedia.org/resource/Year> ;
    qb:slice eg:slice2;
    .

eg:o1b a qb:Observation;
    qb:dataSet  eg:dataset-le2 ;
    eg:refArea                 ex-geo:newport_00pr ;
    eg:refPeriod               <http://reference.data.gov.uk/id/gregorian-interval/2004-01-01T00:00:00/P3Y> ;
    sdmx-dimension:sex         sdmx-code:sex-M ;
    eg:lifeExpectancy          76.7 ;
```

[Example 9 of the RDF Data Cube specification](https://www.w3.org/TR/vocab-data-cube/#h3_dataset-basic) describing individual observations:
```turtle
eg:dataset-le1 a qb:DataSet;
    rdfs:label "Life expectancy"@en;
    rdfs:comment "Life expectancy within Welsh Unitary authorities - extracted from Stats Wales"@en;
    qb:structure eg:dsd-le ;
    .

eg:o1 a qb:Observation;
    qb:dataSet  eg:dataset-le1 ;
    eg:refArea                 ex-geo:newport_00pr ;
    eg:refPeriod               <http://reference.data.gov.uk/id/gregorian-interval/2004-01-01T00:00:00/P3Y> ;
    sdmx-dimension:sex         sdmx-code:sex-M ;
    sdmx-attribute:unitMeasure <http://dbpedia.org/resource/Year> ;
    eg:lifeExpectancy          76.7 ;
    .
```
-->
### QUDT

[Quantities, Units, Dimensions and DataTypes (QUDT)](https://www.qudt.org/) distinguishes between [`qudt:Quantity`](https://qudt.org/schema/qudt/Quantity) that describes the measured value and [`qudt:QuantityKind`](https://qudt.org/schema/qudt/QuantityKind) that abstracts this to general types of such measurements.

Observations are then instances of (subclass of) `qudt:Quantity` and may either link directly to the corresponding `qudt:QuantityKind` via [`qudt:hasQuantityKind`](https://qudt.org/schema/qudt/hasQuantityKind) or indirectly via the associated the unit (chaining `qudt:hasUnit` and )

[Example from the advanced QUDT User Guide](https://github.com/qudt/qudt-public-repo/wiki/Advanced-User-Guide) (<span title="replaced qudt:unit with qudt:hasUnit as the former is deprecated">corrected</span>) to describe an individual quantity.
```turtle
mySchema:MeasuredTriplePoint
  rdf:type owl:Class ;
  rdfs:label "The set of triple point measurements" ;
  rdfs:subClassOf qudt:Quantity ;
.

myMeasurements:TriplePoint_Propane
  rdf:type mySchema:MeasuredTriplePoint ;
  qudt:hasQuantityKind myQuantityKinds:TriplePointTemperature ;
  rdfs:label "Propane triple point" ;
  qudt:hasUnit unit:DEG_C ;
  qudt:value "-187.68" ;
.
```

[Example from the Introductory QUDT User Guide](https://github.com/qudt/qudt-public-repo/wiki/User-Guide-for-QUDT) and excerpt of the [definition of `unit:DEG_F` within the vocabulary](https://qudt.org/vocab/unit/DEG_F.ttl) to describe an individual quantity.
```turtle
unit:DEG_F
  a qudt:Unit ;
  qudt:hasQuantityKind quantitykind:Temperature ;
  rdfs:label "Degree Fahrenheit" .

wiki-examples:MyThermostatSetting
  rdf:type qudt:Quantity ;
  qudt:hasUnit unit:DEG_F ;
  qudt:value "72.0"^^xsd:float ;
.
```


### SOSA
[SOSA (Sensor, Observation, Sample, and Actuator)](https://www.w3.org/TR/vocab-ssn/) is part of the module of the Semantic Sensor Network ontology (SSN).

SOSA contains [`sosa:observedProperty`](https://www.w3.org/TR/vocab-ssn/#SOSAobservedProperty) to describe the property that has been measured, [`sosa:hasFeatureOfInterest`](https://www.w3.org/TR/vocab-ssn/#SOSAFeatureOfInterest) for the phenomenon a observation is made of, and via [`sosa:hasResult`](https://www.w3.org/TR/vocab-ssn/#SOSAhasResult) the observed value itself.

Excerpt of [Example 8](https://www.w3.org/TR/vocab-ssn/#b-1-iphone-barometer) describing a single observation:
```turtle
<Observation/346345> rdf:type sosa:Observation ;
  sosa:observedProperty <sensor/35-207306-844818-0/BMP282/atmosphericPressure> ;
  sosa:hasFeatureOfInterest  <earthAtmosphere> ;
  sosa:madeBySensor <sensor/35-207306-844818-0/BMP282> ;
  sosa:hasResult [
    rdf:type qudt-1-1:QuantityValue ;
    qudt-1-1:numericValue "101936"^^xsd:double ;
    qudt-1-1:unit qudt-unit-1-1:Pascal ] ;
  sosa:resultTime [
    rdf:type time:Instant ;
    time:inXSDDateTimeStamp "2017-06-06T12:36:13+00:00"^^xsd:dateTimeStamp ] .
```

## Considered Options

### Option A: Integration of Units with a Re-Used Relation

```turtle
ex:heightOfTree a iop:Variable ;
  iop:hasObjectOfInterest   ex:tree ;
  iop:hasProperty           qudtQK:Length ;
  qudt:hasUnit              qudtUnit:M
```


* **Pros**
  * collect more information relevant for describing variables at the same place
    * no need to introduce another layer (see example Option C) to combine all relevant information
* **Cons**
  * mixes between Quantity/Result and Property/ObservedProperty (using QUDT/SOSA terminology)
  * would start a similar discussion about method and likely other aspects of Variables


### Option B: Integration of Units with Custom Relation

Units would be attached via a custom (i.e. I-Adopt-specific) relation like `iop:hasUnit` on the `iop:Variable` level.
This follows mostly the same approach as Option A but omits the link to an existing ontology.
Consequently, most of the discussed pros and cons apply here as well.

```turtle
ex:heightOfTree a iop:Variable ;
  iop:hasObjectOfInterest   ex:tree ;
  iop:hasProperty           qudtQK:Length ;
  iop:hasUnit               qudtUnit:M .
```

* **Pros**
  * (see Option A)
  * control of the semantic meaning of `hasUnit` within the I-Adopt namespace
    * no unwanted side effects (e.g., assigning a Quantity-like class to I-Adopt Variables)
  * no specific preference for one unit ontology
* **Cons**
  * (see above)


### Option C: Deferring Units to other Artifacts

```turtle
ex:heightOfTree a iop:Variable ;
  iop:hasObjectOfInterest   ex:tree ;
  iop:hasProperty           qudtQK:Length .

ex:Column1 a ex:Column ;
  ex:describes        ex:heightOfTree ;
  ex:hasUnit          qudtUnit:M .
```


* **Pros**
  * separation of "type of measurement" from actual measurement or representation thereof
    * following the distinction between Quantity and Quantity Kind in QUDT or Result and Observed Property in SOSA
    * allows for a drop-in replacement of, e.g., `qudt:QuantityKind` or `om:Quantity`
  * more generic variables; less mapping effort to map, e.g. `heightOfTreeInMeter` vs `heightOfTreeInFoot`
* **Cons**
  * increased overhead when describing individual measurements or collections thereof (See above example)
