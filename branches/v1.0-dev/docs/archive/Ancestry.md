:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Ancestry

## User Stories

The following is a list of user stories that have a clear requirement for ancestry information.

**1. AS A content producer I NEED TO easily identify elements of video, audio and data that come from a range of different sources with global scope SO THAT I can combine the correct elements to create content of value.**

Interpreting `sources` in the more general case of originating from some known entity, and interpreting `correct` to mean it originated from that known `source`. This then means there needs to be way to trace where content originated from.

**17. AS A content producer I NEED TO be able to identify streams of content at the point of use SO THAT I can track ancestry as elements are processed and combined**

This is really a requirement needed to support ancestry rather than ancestry itself.


**28. AS A content producer I NEED TO keep a record of the original material used to create a piece of finished content SO THAT I can obtain the necessary rights to use it.**

This assumes that rights information is associated with the `original material` and therefore a requirement to be able to trace back finished content to the original.


## Requirements from User Stories

From the User Stories it follows that `Ancestry` needs to provide the information needed to answer the question: for a piece of content, which content was used to produce it?

The content in this context is represented by the entities in the T&I Model and therefore the ancestry information is about the relationships between those entities. In a wider context there could be other entities, eg. Programme, Persons, Contracts, and the ancestry could be extended to those entities using other relationships.

`Ancestry` is primarily concerned with identifying the content rather than about every detail about the how the content was derived. `Ancestry` may provide some information about the nature of the relationship, eg. a lossy versus lossless transformation.


## Definitions

### General TDS Ancestry

At the most basic level, an `Ancestry` relationship is between a Data Object at a Time Value in the _output_ TDS and one or more Data Objects at Time Values in the same or other _input_ TDSs. The method by which the output Data Object was derived from the input Data Objects is represented by a function `F`. The level of detail encompassed by the function `F` can vary depending on the requirements. Each Data Object in the output TDS can have an `Ancestry` relationship that defines how it was derived from other Data Objects.


### General Similarity Cluster Ancestry

The general TDS `Ancestry` definition can be applied in a similar way to Similarity Clusters such as Sources and Flows. This is particularly relevant because these will likely be the primary entities used in applications of the T&I Model. In the Similarity Clusters definition of `Ancestry` the Data Objects in the TDS `Ancestry` relationship are replaced with something that is no a longer single 'byte stream' instance but rather a set of instances that conform the Similarity Cluster definition.


### Ancestry Simplifications

In an ideal world all information about how content was derived from other content is retained. However, the cost of retaining and processing is likely to exceed the benefits. Focusing on the key questions that need to be answered using `Ancestry` will help reduce the information set so that they contain sufficient detail to provide the answers to the questions.

The general `Ancestry` relationship can be reduced in the following ways:
* simplify `F`. Eg. `F` could simply state that the output `was derived from` the input
* group a time range of input or output Data Objects so that the relationship refers to that time range rather than individual Data Objects. The time range could be extended to cover the complete range
* reference inputs or outputs using higher level Similarity Clusters. The relationship then applies to all members of the Similarity Cluster
* the input in the relationship could be omitted. Eg. a `generation number` records how many lossy encodes resulted in the output.

The simplified `Ancestry` relationship may include entities that did not contribute to the output. Eg. not all Data Objects in an input time range were used. However, for the purpose of answering the ancestry question is may not matter. Eg. the question, `was Similarity Cluster A used to produce a TDS B`, doesn't require exact time range information or which specific input TDS was used.

An `Ancestry` relationship can be derived from a concatenation of `Ancestry` relationships. The concatenation process can eliminate some of the details of the intermediate `Ancestry` relationships. This simplification process can be used to reduce the ancestry information and is also a component of the ancestry discovery process.


## Common Ancestry Relationships

A common `Ancestry` relationship will be between 2 Similarity Clusters at the same level, eg. Source to Source or Flow to Flow. It would generally limit `F` by simply stating that the input was derived from output. It could additionally specify the input and output time ranges.

Below are examples of `Ancestry` relationships specified using a simple notation. The notation is intended to identify the key parts of the relationship and is not meant to show how it should be implemented.

* a complex set of operations with Source B, C and D as input resulted in a Source A. The details of the operations are ultimately not important at the edges of the production process and therefore the relationship is recorded as: **{Source A} was derived from {Source B}, {Source C} and {Source D}**
* Flow B was time shifted for use in a composition, resulting in Flow A: **{Flow A} is {Flow B} time shifted by T**
* the Source relationship follows from the above Flow relationship: **{Source A} is {Source B} time shifted by T**
* Flow A is a transcode of Flow C. The intermediate Flow B, which is Flow A decoded, is not recorded in the relationship: **{Flow A} is a transcode of {Flow C}**
* Flow A is a lossy transcode of another Flow in the same Source, resulting in a new generation number: **{Flow A} generation number is 2**
* a time range of Source B was converted to monochrome video to produce a time range in Source A: **{Source A, [Ta1, Ta2]} is {Source B, [Tb1, Tb2]} converted to monochrome**
* a time range of Source B and Source C were mixed together to produced a time range in Source A: **{Source A, [Ta1, Ta2]} is a mix of ({Source B, [Tb1, Tb2]} and {Source C, [Tc1, Tc2]})**
* Source A switches between Source B and Source C. An Ancestry relationship is recorded for each time value or time range: **{Source A, [Ta1, Ta2]} is {Source B, [Tb1, Tb2]}, {Source A, [Ta3]} is {Source C, [Tc3]}, {Source A, [Ta4]} is {Source B, [Tb4]}, etc.**
