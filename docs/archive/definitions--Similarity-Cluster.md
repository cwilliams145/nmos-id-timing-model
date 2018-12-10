:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# `Similarity Cluster`

A `Similarity Cluster` is an addition on top of the [core model](definitions.md) in order to provide additional capability



![Similarity Cluster UML](images/Similarity-Cluster.svg)



The purpose of `Similarity Cluster`s is to provide a means for associating an ID with a collection of `TDS`s.

The members of a `Similarity Cluster` can be `TDS`s , `Similarity Cluster`s or a combination of the two.

All `TDS`s associated with a `Similarity Cluster` are associated with a single `Time Varying Information` and a single `Time Context` (this applies to all `TDS`s that are both directly and indirectly associated with a `Similarity Cluster`).

*More info: [notes](notes--Similarity-Cluster.md)*
