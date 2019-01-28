:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Notes on `Similarity Cluster`s

All of the `TDS`s associated with a `Similarity Cluster` use the same `Time Context`. This means that it makes sense to consider querying a `Similarity Cluster` with a `Time Value` or range of `Time Value`s &ndash; this could be useful, for example, in designing an API that allows a `Similarity Cluster` to be queried by time range without consideration of the video codecs of the associated `TDS`s.

`Similarity Cluster`s have been designed such that the member `TDS`s are to some degree "similar" and so are alternatives than can be switched between in the right scenario. `Similarity Cluster`s can be nested to communicate different degrees of similarity. The model doesn't restrict the structure of the graph of `Similarity Cluster`s, but in reality a structure that is hierarchical (or close to hierarchical) is likely to be useful.

