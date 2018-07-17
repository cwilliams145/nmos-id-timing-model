# Notes on `TVI`s

`TVI`s are deliberately defined in quite abstract terms. A `TVI` can be thought of as simply a mechanism for identifying a number of `TDS`s that are conveying the same "message".

Given relatively few constraints are applied to `TVI`s, there is the prospect for a number of 'grey areas' in what can be viewed to represent the same `TVI`. This is intended to allow the user to decide the most appropriate degree of 'similarity' between `TDS`s which are permitted to be identified as being approximations of the same `TVI`. In a practical and interoperable implementation it is likely that some additional constraints will need to be applied to how `TVI`s are used in order for them to be useful.

In practical systems it is normally useful to define a `TVI` for each "element" of content (such as a `TVI` for each of the audio and the video that form a programme). These "elements" are chosen to be at a practically "useful" level of granularity (such as defining a `TVI` for the multi-channel audio created for a programme). However, these "elements" can always be decomposed as required (such as breaking down the multi-channel programme audio into its constituent audio channels, with one `TVI` defined for each audio channel &ndash; note that decomposing a `TVI` / extracting a subset of the content logically results in different `TVI`s).

It would not normally be practical to define an entire "scene" (e.g. in a TV studio) as a `TVI`. For most practical purposes this is not "granular" enough, and establishing which items of content relate to this `TVI` would be very difficult to automate. Other mechanisms should be used to describe "scenes" and other high-level concepts such as actors, objects in the scene, etc.

