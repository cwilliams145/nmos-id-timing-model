# The Core Model



![Abstract Model UML](images/AbstractModelUML.svg)



Note: "time-point" is used below to refer to a precise (zero duration) instant in time


## `Time Context`

A `Time Context` establishes a common zero-point such that all events at a given time-point in a `Time Context` are considered "co-timed" / "synchronised".

*More info: [notes](notes--Time_Context.md), [examples](examples--Time_Context.md)*

## `Time Value`

Each `Time Value` consists of a `count` (an integer) and a `time_unit` (a "rational": this is a "fraction" consisting of an integer numerator and an integer denominator).

Each `Time Value` represents a period of time that is the following number of seconds in duration (seconds are the SI base unit of time):

`count` &times; `time_unit`

*More info: [notes](notes--Time_Value.md), [examples](examples--Time_Value.md)*

## `Data Object`

A `Data Object` is a sequence of bytes.

The structure and complexity of a `Data Object` is completely unconstrained by this model.

*More info: [notes](notes--Data_Object.md), [examples](examples--Data_Object.md)*


## `Timed Data Structure` (`TDS`) and `TDS Entry`

A `Timed Data Structure` (or `TDS`):

* has an ID
* uses a `Time Context`
* consists of zero or more `TDS Entry`s


Each `TDS Entry` associates a `Time Value` with a `Data Object`. This `Time Value` identifies a time-point within the `Time Context` that is used by the `TDS`.

*More info: [notes](notes--TDS.md), [examples](examples--TDS.md)*

## `Time Varying Information` (`TVI`)

All `TDS`s that are associated with a `Time Varying Information` are considered to be alternative "representations" of the same time-based "information". That is, all these `TDS`s are considered to be conveying the same "message" (the same "information" with the same relationship to time). The precise definition of "the same" here will be application specific (that is, in some applications two `TDS`s can be associated with the same `TVI` even if the "messages" they are conveying are not absolutely identical).

*More info: [notes](notes--TVI.md), [examples](examples--TVI.md), [explanatory presentation (illustrated notes & examples)](understanding--TVI.pptx)*

