# Overview

A `Timed Data Structure` is a means of conveying time-based information (that is, information with a time component). All `TDS`s that are associated with a `Time Varying Information` (`TVI`) are considered to be alternative "representations" of the same information (or "message") with the same relationship to time.

A `Timed Data Structure` (`TDS`) is a collection where each item in the collection consists of:

* A `Time Value` (a `count` and `time_unit`)
* A `Data Object` (a sequence of bytes)

Each `Time Value` represents a period of "continuous" time (measured in seconds) from the common zero-point of the `Time Context` used by the `TDS` &ndash; it locates the `Data Object` within this `Time Context`.

A `Time Context` may be used by many `TDS`s. `Data Object`s across all of these are considered "co-timed" / "synchronised" if their `Time Value`s are equivalent.

