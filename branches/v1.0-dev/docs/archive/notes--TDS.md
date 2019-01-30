:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Notes on `Timed Data Structure`s

## `TDS` &ndash; a generalised abstract model

The model of a `TDS` is an abstract model &ndash; it in no way predetermines how practical `TDS`s should be implemented.

It is also a general model &ndash; there are special cases of this general case that may be important e.g. periodic data. It may be that these special cases are treated differently in practice &ndash; for example, with specially designed `TDS` implementations.

## Not necessarily mono-essence

`TDS`s can represent any kind of data. For media, each `TDS` is typically mono-essence but in the general case this is not required.

## `time_unit`s within a `TDS` do not all have to be the same

Within a `TDS`, each `Time Value`s can use any `time_unit`. However, in real implementations, each media `TDS`s is likely to use only one `time_unit` throughout.

## A `TDS` is a "collection" of `TDS Entry`s

The `TDS Entry`s that constitute a `TDS` are not "ordered" &ndash; however, they can of course be ordered by `Time Value` if desired. (The point is that they do not have any order other than the one given by their `Time Value`s)


## The `Data Object`s

A `Data Object` could appear in a `Timed Data Structure` more than once. `Data Objects` are not "owned" by a `Timed Data Structure` and so a `Data Object` could be used by more than one `Timed Data Structure`.

To handle such cases in a practical system, each `Data Object` could well be assigned an ID (such as an UUID &ndash; something that is independent of any `Timed Data Structure` or `Time Value`) and then this could be used when forming `Timed Data Strcuture`s so that `Data Object`s themselves (which could be very large) do not need to be duplicated.


## "Interpreting" `TDS`s ("rendering" of their data etc)

Interpretation (e.g. "rendering") of a `Timed Data Structure` will depend on the exact representation used. For example:
* A `Data Object` may still contain some time-based information (e.g. information about how long the "effect" of the `Data Object` should persist for when rendered).

* The exact interpretation of the `Time Value` with which a `Data Object` is associated will depend on the representation being used:

  * For example, for an SD video frame captured from SDI the `Time Value` could conceivably be the time at which the frame signal begins (Line 1) or it could be the time at which the visible picture for the frame begins (Line 23).
  * In some scenarios each `Time Value` will correspond with the time at which the `Data Object` came into existence. However, this is certainly not the case for all scenarios. For example each `Time Value` may be used to map the `Data Object` onto a future point in time.



## Re-timing

"Re-timing" a `TDS` involves performing an operation on its `Time Value`s. For example, a `TDS` could be "re-timed" to perform a time shift. "Re-timing" generates a new `TDS` (with a new `id`) that would be associated with a new `TVI`.


