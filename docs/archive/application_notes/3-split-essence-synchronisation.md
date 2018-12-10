:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# 3. Split Essence Synchronisation

### Aim: Synchronise TDS 3 with TDS 4

![Split Essence Synchronisation](images/3-split-essence-synchronisation.png)

### Scenario

In order to permit synchronisation of `TDS` 3 with `TDS` 4 in an automated fashion, it must be possible to relate them to each other.

### Behaviour & Options

In (1), three options were presented for the production of `Time Value`s for `TDS` 3.

1.  `TDS` 3's `Time Value`s have no recorded relationship to `TDS` 1 and `TDS` 2.

2.  `TDS` 3's `Time Value`s can be related to corresponding `Data Object`s in `TDS` 1 and `TDS` 2 via a fixed time offset advertised by the mixer (link scoped timing).

3.  `TDS` 3's `Time Value`s exactly match the `Time Value`s used in `TDS` 1 and `TDS` 2 where corresponding `Data Object`s occur (end to end timing).

Assuming `TDS` 4 is created in the same `Time Context` as `TDS` 1 and `TDS` 2, it should be clear that option 1 is inappropriate.

Both options 2 and 3 provide potential means of achieving synchronisation, with the following key differences:

2.  The time offsets introduced by each processing device in the chain must be identified. The sum of these offsets for a given chain (for example the audio chain) must then be used to delay the output in corresponding chains (for example the video chain) to ensure the same level of delay is applied prior to the output device.

3.  The offset between the incoming `TDS` `Time Value`s and the current wall clock time must be identified at each output device (speaker and display). The largest of these values must then be set into all output devices to ensure they all delay the output of `Data Object`s by the appropriate time.
