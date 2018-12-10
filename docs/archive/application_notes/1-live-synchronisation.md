:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# 1. Live Synchronisation

### Aim: Synchronise TDS 1 with TDS 2

![Live Synchronisation](images/1-live-synchronisation.png)

### Scenario

-   Two microphones are plugged into an audio mixer
-   The `Time Value`s produced by the microphones relate to the time at which audio hit their transducers
-   The microphones share a timing reference (for example via PTP) and as such can produce `TDS`s which use `Time Context` A.
-   When `TDS` 1 and `TDS` 2 arrive at the mixer, it can compare their `Time Value`s in order to mix `Data Object`s (ie audio samples) which were coincident at the capture point of the microphones (*).

### Behaviour & Options

The creation of `Time Value`s for `TDS` 3 could be carried out using multiple methods:

1.  If the mixer does not share a timing reference with the microphones it may create new `Time Value`s at its output using a different `Time Context`, with no relation to the incoming `TDS`s. In this case the mixer produces `TDS`s in `Time Context` B.

2.  The mixer may share a timing reference with the microphones but choose to create fresh `Time Value`s at its output. The relationship between `TDS` 3 and the incoming `TDS` 1 and `TDS` 2 could as a result be identified via a simple time offset. In this case the mixer produces `TDS`s in `Time Context` A.

3.  The mixer may select an incoming `TDS` as a notional 'master' to take `Time Value`s from and re-use at its output. This avoids the requirement for the mixer to share a timing reference with the rest of the system, but still allows it to maintain a relationship between the input `TDS` `Time Value`s and the output. In this case there is a zero time offset between `TDS` 3 and the corresponding audio samples (`Data Object`s) in `TDS` 1 and `TDS` 2. In this case the mixer produces `TDS`s in `Time Context` A.

### Caveats

-   In practice the audio mixer is likely to carry out more complex processing operations which may include timing offsets. The effect that this processing has on `TDS`s and their `Time Value`s may be explored in a later example.
-   (*) Audio mixers do not typically automatically compare `Time Value`s at their inputs and perform buffering to synchronise them. Whilst this is unlikely to change, it may be useful for future devices to indicate where mixes have been performed slightly out of sync due to the reported `Time Values`. This may allow the user to impose manual delays upon the various inputs prior to the mix operation.
