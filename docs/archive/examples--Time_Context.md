:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Examples of `Time Context`s

* Shared studio time reference
* Clock internal to a camera
* MXF Package
* PTP time reference
* Global time reference
* Shared timing of contents of a video tape


## Further Exploration

In different situations it may be preferable to use `Time Context`s with different scopes. Consider for example a set of mobile phones recording video of a scene. The phones share a time reference via a mobile network, but it does not allow them to maintain clocks which are always well aligned in terms of frequency and phase.

In a professional video production for broadcast, it may be preferable to view each phone in its own `Time Context` as when each phone's recorded content is brought together into a composition it may be undesirable to directly compare the `Time Values` of these `TDS`s. They may be approximately correct, but may need to have time stretches or squashes applied in order to correct for frequency and phase error.

In a consumer setting it may be acceptable to view these phones as having recorded content in the same `Time Context` as these precise re-alignments are less important, and a direct comparison of `Time Values` from each `TDS` to achieve synchronisation may be sufficient.
