# I-ADOPT Variable Design Patterns (VDPs) definition
I-ADOPT Variable Design Patterns (VDPs) are implementation guidelines for modelling I-ADOPT variables similar to how Ontology Design Patterns are used as templates or as inspiration for specific modelling solutions https://gofair-foundation.github.io/fip/Intro.html when creating ontologies. VDPs are domain- independent and theoretic (more abstract) I-ADOPT variables that must be substantiated to be reused as variables. Variables themselves are also abstract as they represent types but, in contrast, these can be directly reused in different observation situations by instantiating them with additional metadata like the location and the time information. VDPs do not include any Constraints, which are used to refine a variable. Properties in VDPs are essentially the same Properties as in Variables. VDPs use for ObjectOfInterest and Matrix concepts that describe the nature of the entities (sometimes in thesauri used as parent concepts)  more than concrete entities used in Variables, e.g. substance instead of nitrogen, organism instead of a species name, part of organism instead of liver.

This repository is work in progress and is supposed to be extended.

# Contributing new VDPs
If you like to suggest new VDPs we invite you to publish a new issue. The I-ADOPT Governance Group will accept the suggestion when proved to be a valuable contribution.

# VDP Catalogue

* [quantitative](quantitative/)
    * [simple](quantitative/simple.md)
    * [complex property](quantitative/complexproperty.md)
    * [concentration](quantitative/concentration.md)
* [VDPs for qualitative variables](qualitative/)
    * [biological](qualitatitve/biological.md)
    * [biological](qualitatitve/boolean.md)


# Decisions

Some of the patterns are preceded by an extensive discussion. The options discussed along each one's pros and cons as well as the final decisions are documented in [application design records](./adrs/).

* [distance](https://github.com/i-adopt/patterns/tree/main/adrs#vdps-for-distance-variables)
   * [Symmetric Systems](000-symmetricSystems.md)
   * [Asymmetric Systems](001-asymmetricSystems.md)
* [I-ADOPT PLUS](https://github.com/i-adopt/patterns/blob/main/adrs/002-I-ADOPT_PLUS.md)
