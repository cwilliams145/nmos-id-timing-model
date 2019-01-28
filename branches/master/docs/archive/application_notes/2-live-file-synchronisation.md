:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# 2. Live & File Playout Synchronisation

### Aim: Synchronise TDS 2 with TDSs 3 and 4

![Live & File Playout Synchronisation](images/2-live-file-synchronisation.png)

### Scenario

-   Two microphones and a playback device are plugged into an audio mixer
-   The playback device has a stored audio `TDS` 1 (for example a WAV file) which consists of `Data Object`s and `Time Value`s
-   The `Time Value`s in the audio recording exist within `Time Context` A which is scoped within the audio file only, with the first sample occuring at a `Time Value` of zero
-   The `Time Value`s produced by the microphones relate to the time at which audio hit their transducers
-   The microphones and playback device share a timing reference (for example via PTP) and as such can produce `TDS`s which use the same `Time Context` B

### Behaviour & Options

-   At the time of audio playback, a new `TDS` is created by the playback device (`TDS` 2). This contains identical `Data Object`s to the stored `TDS` 1, but the `Time Value`s are created fresh in `Time Context` B to permit synchronisation with other `TDS`s using that `Time Context`.

### Caveats

-   As in (1), audio mixers do not typically automatically compare `Time Value`s at their inputs and perform buffering to synchronise them.
-   As `TDS` 1 is unrelated to the live signals in the system, there is little benefit in this scenario to synchronise `TDS` 2 with `TDS` 3 and 4 prior to the mix. Note however that had the stored `TDS` 1 also contained a video track which was processed by a separate chain this may have been more important. This will likely be the subject of a future application note.
