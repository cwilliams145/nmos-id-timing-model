:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Notes on `Time Context`s

* There may, or may not, be a relationship between a `Time Context` and "calendar" / "wall-clock" time. In other words, a `Time Context` may be used for "relative" or "absolute" time.
* The "distance" between any two time-points in a `Time Context` can be measured in SI seconds. Be aware that units of systems such as UTC are not always of constant duration because they do not purely aim to measure the passage of "continuous" time (and so contain discontinuities such as "leap seconds"). There are no discontinuities in a `Time Context` because a `Time Context` is used to measure "continuous" time &ndash; there are no discontinuities in the actual passage of time.
* The entity `Time Context` is intended to be very close in meaning to the term "timeline", used casually in relation to audio or video editing to describe the common time grid onto which media clips are placed. 
* "Time scale" is a term often used casually , or formally, in relation to time, audio or video editing, etc. Definitions do vary &ndash; however, the following could be considered a means of producing a "time scale": you choose a `Time Context` and a `time_unit`, and then create a time-point within that `Time Context` at every possible multiple of the `time_unit`.
* There may be more than one `TDS` associated with a `TVI`. These `TDS`s may not all use the same `Time Context` &ndash; if more than one `Time Context` is used then the relationship between these `Time Context`s must be expressed / captured. For example, within a studio, most cameras use a `Time Context` which has a zero-point in 1970, whereas one camera uses a `Time Context` which has a zero-point in 2018.


* If two `TDS`s use the same `Time Context` then they are synchronised &ndash; `Time Value`s in these `TDS`s can be directly compared (of course `time_unit` conversions may need to take place in the process of carrying out these comparisons). 
* A single `Time Context` may be used by `TDS`s that are associated with multiple `TVI`s. The fact that the same `Time Context` is used does not mean that the content of the `TDS`s is related (for example, all the cameras in a production centre may produce `TDS`s that use the same `Time Context` &ndash; however, many of the pictures being captured will most likely be for different programmes).


