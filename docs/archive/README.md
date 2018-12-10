:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Archive

## Project Definition

The NMOS identity and timing activity was started in order to define an identity and timing model for audio, video and data. The resulting model is intended to be used across the NMOS family of specifications where 'content' needs to be modelled.

The primary focus of the activity was in the area of Sources, Flows and Grains identified within the [JT-NM Reference Architecture](http://www.jt-nm.org/RA-1.0/). It examined their identity and timing characteristics, identifying how aspects should be constrained in order to permit interoperable implementations capable of meeting the needs of the project's user stories. Further details can be found in the [Project Proposal](ProjectProposal.pdf).

Whilst the concepts of Sources and Flows had already been used in NMOS specifications (most notably IS-04) for a significant period, a growing desire to be able to represent end-to-end identity and timing in production systems required a more formal and separable specification.

## The Core Model

In order to re-validate the Source and Flow entities and to firm up their definitions, initial analysis was carried out. Common media (video/audio) streaming and packaging formats were considered, along with a range of non-media scenarios relating to collection of pure 'data'.

These data types can be generalised under the heading of `Time Varying Information` (`TVI`). In other words, any file, stream or other construct conveys some form of information which has an intimate and invariable relationship to time. If the relationship to time is changed, the information itself has changed in some way.

At a base level (in a digital context) this `Time Varying Information` is always represented by a sequence of bytes which could be stored to a digital medium or transported via some means. These byte sequences are referred to as `Timed Data Structure`s (`TDS`s).

Within any `Timed Data Structure`, each sample could be uniquely identified as a `Data Object`, with its position in time recorded via a `Time Value`.

Finally, in order to represent relationships (such as synchronisation) between multiple `Timed Data Structure`s, some scope had to be attached to the `Time Value`s to indicate that any two matching `Time Value`s were actually coincident. This was achieved by associating `Timed Data Structure`s with a common `Time Context`.

Each of the entities which has been briefly described above is considered in far greater depth in documents within this directory as follows:

### Further Reading

*   [User Stories](user-stories.md)
*   The Model
    *   [Overview](overview.md)
    *   [Full Details](definitions.md)
*   [Motivation](motivation.md) for designing the model
*   [Explanation of the principles / approach](explanation-and-principles.md) behind the model

## Building Towards Sources & Flows

Whilst the concepts of `TDS`s and `TVI`s provide modelling entities which identity and timing data could be associated with, they are not necessarily the most useful definitions for the user stories presented within this project.

For example:
*   One computer has a stored `TDS`. In order to transmit it to another computer over a network it converts the bytes into a new layout, which must necessarily be defined as a new `TDS`. Upon reception, the receiving computer, which uses a different processor architecture converts the bytes into a third layout, which is another `TDS`. Despite there being three different byte sequences conveyed here, each one would be considered to be identical when observed at a level which is of interest to the end user (for example a sequence of still images making up a video).

Scenarios like the above, suggest that the `TDS` is too fine grained for common usage. As such, through the analysis of common media operations and the 'content of interest' as far as identity is concerned, the definition of a `Flow` was set at a higher level of abstraction.

At the other end of the spectrum, consideration was given to the very high level concept of `TVI`s. There are very few constraints upon what may be considered to be the same piece of `Time Varying Information`. This may for example relate to the content captured by a single camera, or even the entire scene in a studio which may be captured from any angle. At some level each of these could be considered to be a piece of information which varys with relation to time.

In order to quantify the concept of `Time Varying Information`, a more concrete entity known as a `Similarity Cluster` was coined. This permits a definition to be assigned which limits the level at which two entities could be considered to convey the same information. Through analysis of common media operations, a `Source` is then defined to be a `Similarity Cluster` which is set at a specific level in order to promote interoperability.

Further named `Similarity Cluster`s could be defined by any user in addition to the defined `Source` type, however these would likely be identified in a system via a generic grouping mechanism.

### Further Reading

*   [Similarity Clusters](definitions--Similarity-Cluster.md)
*   [Content Relationships](understanding--Relationships.pptx)
*   Media Operations
    *   [Analysis](media_operations--analysis.md)
    *   [Summary](media_operations--summary.md)
*   [Application Notes](application_notes/README.md)
*   [Sources](Source.md)
*   [Flows](Flow.md)
*   [Ancestry](Ancestry.md)
