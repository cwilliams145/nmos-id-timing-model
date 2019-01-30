:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Notes on `Data Object`s

* `Data Object`s may depend on each other (e.g. encoded inter-frame coded video containing B/P frames; with AAC coded audio multiple `Data Object`s are needed in order to be able to decode the audio). Any such inter-dependencies are not covered by this core model.
* `Data Object`s will typically contain data for a single media sample but could contain multiple media samples. Regardless, `Data Object`s may be "packaged" together in real systems (for example, a real system may choose to always transport `Data Object`s in bundles of ten for practical reasons).
* A `Data Object` will typically be mono-essence for practical media applications, but it could be multi-essence. Essence data may exist in both mono-essence and multi-essence `Data Object`s / `TDS`s &ndash; we may wish to map between these entities (such as saying one TDS (V+A) contains all of the data required to create byte identical versions of two other TDSs (V/A)).
* At a base level, two `Data Object`s are considered identical only if they are bit-wise identical.


