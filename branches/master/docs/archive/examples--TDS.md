:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Examples of `Timed Data Structure`s

*Note:* All the `TDS` examples given here are valid. However, in typical real-world usage, `Timed Data Structure`s are likely to be defined with some constraints upon the nature of their `Data Object`s (e.g. only JSON payloads, only H.264 coded intra-frame video, only raw audio).

### `TDS` Example 1

*   Each `Data Object` is restricted to being a 10-bit raw video frame given what the active camera produces. The camera samples the scene at 25 frames per second.
*   `Data Object`s in this `TDS` are chosen to be in v210 format only.

```
* TDS Entry
** Time Value: 0 milliseconds
** Data Object Contents: v210 Video Frame @ 1920x1080 4:2:2 10-bit

* TDS Entry
** Time Value: 40 milliseconds
** Data Object Contents: v210 Video Frame @ 1920x1080 4:2:2 10-bit

* TDS Entry
** Time Value: 80 milliseconds
** Data Object Contents: v210 Video Frame @ 1920x1080 4:2:2 10-bit

* TDS Entry
** Time Value: 120 milliseconds
** Data Object Contents: v210 Video Frame @ 1920x1080 4:2:2 10-bit

* TDS Entry
** Time Value: 180 milliseconds
** Data Object Contents: v210 Video Frame @ 1920x1080 4:2:2 10-bit
```

### `TDS` Example 2

A camera exists at a point in space and captures video and audio. It provides access to this video and audio as SDI from which a `TDS` is produced. You could split the two transducers and represent their observations as two different `TDS`s if desired, but in this case we haven't.

*   Each `Data Object` can contain both video and audio, with the audio covering samples for more than just one time instant. The video and audio rate may not align, and so there is no guaranteed mapping between the leading edge of the first video/audio sample in the 'frame' and the `Time Value` which the `Data Object` has in the `TDS`, but the encapsulation format defines the means to map to the `Time Value` with an offset.

```
* TDS Entry
** Time Value: 0 nanoseconds
** Data Object Contents: 29.97Hz SDI payload containing: Video Frame @ 1920x1080 + 1602 L24 audio samples

* TDS Entry
** Time Value: 33366700 nanoseconds
** Data Object Contents: 29.97Hz SDI payload containing: Video Frame @ 1920x1080 + 1601 L24 audio samples

* TDS Entry
** Time Value: 66733400 nanoseconds
** Data Object Contents: 29.97Hz SDI payload containing: Video Frame @ 1920x1080 + 1602 L24 audio samples

* TDS Entry
** Time Value: 100100100 nanoseconds
** Data Object Contents: 29.97Hz SDI payload containing: Video Frame @ 1920x1080 + 1601 L24 audio samples

* TDS Entry
** Time Value: 133466800 nanoseconds
** Data Object Contents: 29.97Hz SDI payload containing: Video Frame @ 1920x1080 + 1602 L24 audio samples
```

*   Device(s) playing this out must be aware of the mapping between the encapsulated data and the `Time Value` in order to play it out correctly in time.

### `TDS` Example 3

This describes a non-standard packing format for video, audio and data. In this specific `TDS`, video is sampled at 25Hz, audio at 48kHz, and GPS lat/lon co-ordinates at 16kHz. This results in a single `Data Object` every 1/48000 seconds, which consists of between one and three elements.

```
* TDS Entry
** Time Value: 0 nanoseconds
** Data Object Contents: v210 format video frame, 8 channels of L24 audio (1 sample per channel), and Lat/Lon co-ordinates

* TDS Entry
** Time Value: 20833 nanoseconds
** Data Object Contents: 8 channels of L24 audio (1 sample per channel)

* TDS Entry
** Time Value: 41666 nanoseconds
** Data Object Contents: 8 channels of L24 audio (1 sample per channel)

* TDS Entry
** Time Value: 62500 nanoseconds
** Data Object Contents: 8 channels of L24 audio (1 sample per channel), and Lat/Lon co-ordinates

* TDS Entry
** Time Value: 83333 nanoseconds
** Data Object Contents: 8 channels of L24 audio (1 sample per channel)
```

### `TDS` Example 4

This `TDS` represents periodically sampled data from a temperature sensor. The sensor reflects the temperature at a point within a room.

*   The system takes measurements from the sensor every 60 seconds and records this in a `Data Object` which is simply a number, known to be measured in degrees centigrade.

```
* TDS Entry
** Time Value: 60 seconds
** Data Object Contents: 16

* TDS Entry
** Time Value: 120 seconds
** Data Object Contents: 17

* TDS Entry
** Time Value: 180 seconds
** Data Object Contents: 19

* TDS Entry
** Time Value: 240 seconds
** Data Object Contents: 24

* TDS Entry
** Time Value: 300 seconds
** Data Object Contents: 26
```

### `TDS` Example 5

This `TDS` is similar to the example in `TDS` 4, but instead `Data Object`s are recorded in an interrupt-driven fashion when the value of the temperature sensor changes by a degree. `TDS` 5 is a more accurate representation of the changing temperature than `TDS` 4. Both `TDS` 4 and `TDS` 5 are associated with the same `TVI`.

```
* TDS Entry
** Time Value: 52 seconds
** Data Object Contents: 16

* TDS Entry
** Time Value: 115 seconds
** Data Object Contents: 17

* TDS Entry
** Time Value: 153 seconds
** Data Object Contents: 18

* TDS Entry
** Time Value: 174 seconds
** Data Object Contents: 19

* TDS Entry
** Time Value: 191 seconds
** Data Object Contents: 20
```

### `TDS` Example 6

This is a duplicate of `TDS` 5. It uses `Data Object`s which are byte-identical, in the same sequence, but the `TDS` `id` is different as the `Time Value`s differ. **It is associated with the same `TVI`, but using a different `Time Context`**. Here the `Time Context` uses an origin set to 01/01/1970 with a 'TAI' scale, along with a global reference.

```
* TDS Entry
** Time Value: 1520423775 seconds
** Data Object Contents: 16

* TDS Entry
** Time Value: 1520423838 seconds
** Data Object Contents: 17

* TDS Entry
** Time Value: 1520423876 seconds
** Data Object Contents: 18

* TDS Entry
** Time Value: 1520423897 seconds
** Data Object Contents: 19

* TDS Entry
** Time Value: 1520423914 seconds
** Data Object Contents: 20
```

### `TDS` Example 7

A user wants to set the temperature of a heater. They choose five temperatures and choose times in the future for each of these temperatures to take effect. This is a `TDS` with `Data Object`s containing temperatures.

The user later decides to move all of these `Time Value`s by one hour to account for a daylight savings change they had forgotten about. This results in new `Time Value`s and as such creates a new `TDS` whose `Data Object`s are each offset from each other by the same time period which they were previously. In this instance the same `Time Context` is used in both cases, but there may be a mapping defined externally to indicate that the two `TDS`s are in some way related.

### `TDS` Example 8

A user has a raw video `TDS` containing v210 format `Data Object`s. The user creates a matching H264 intra-coded sequence of `Data Object`s representing the same content. This is necessarily a different `TDS` with a different `id`, but may have the same `Time Value`s as the original v210 `TDS`. Both of these `Timed Data Structure`s are associated with the same `Time Varying Information`.

A further `TDS` is created using the original v210 `Data Object`s in the same sequence, but with the time period between each `Time Value` halved. This produces a double frame rate video representation. **This is a new `TDS` with new `Time Value`s and is associated with a different `Time Varying Information`, but uses the same `Data Object`s.**

### `TDS` Example 9

A camera is creating 50Hz 10-bit raw 1920x1080 4:2:2 video output, producing `Data Object`s and a resultant `Timed Data Structure`. The camera is reconfigured to output at half the rate. This can be modelled as the same `TDS` (associated with the same `TVI`) but consists of a lower frequency of generation of `Data Object`s and `Time Value`s after this point.

### `TDS` Example 10

The output of a vision mixer represents the bringing together of several `TDS`s (each of which is associated with a different `TVI`). This 'mix' operation may be performed live with streams of data coming in, or may be performed in a non-linear editor. In either case, the new output `TDS` will be a mix of identical `Data Object`s to those provided to the inputs, and some new `Data Object`s which may be a composite of multiple input `Data Object`s.s

Depending on the application, `Time Value`s assigned to output `Data Object`s may match the values used at inputs or may be coined fresh in order to associate this composition with a particular point in time.

### `TDS` Example 11

A `TDS` is stored on disk with its corresponding `Data Object`s and `Time Value`s. It is played out onto a network using RTP. The RTP payload type and "maximum transmission unit" mean that the data cannot be carried exactly as it is laid out in the existing `Data Object`. As such a new set of `Data Object`s and as such a new `TDS` must be created for transmission via RTP, however the `Time Value`s for the RTP encapsulated `Data Object`s may be chosen to remain the same as previous. Once data reaches a receiving system, it may be possible to reconstruct an identical `TDS` with identical `Data Object`s and `Time Value`s to the one which was originally stored on disk. This entity could as a result use the same `TDS` `id`.

### `TDS` Example 12

This example shows a `TDS` which is very unlikely to ever exist in reality. It is intended to show that at this level of modelling it doesn't matter what the data is, but that it is binary data which has had a `Time Value` associated with it. This differs from a playlist in that a playlist alone does not usually define precisely when each item must play out.

```
* TDS Entry
** Time Value: 92785 seconds
** Data Object Contents: Still image of an elephant in JPEG format

* TDS Entry
** Time Value: 104829 seconds
** Data Object Contents: WAV format audio file containing 5 seconds worth of 1kHz tone

* TDS Entry
** Time Value: 104934 seconds
** Data Object Contents: Extract of Lorem Ipsum covering 500 characters in UTF8

* TDS Entry
** Time Value: 582056 seconds
** Data Object Contents: 2 lines extracted from an Apache web server log file

* TDS Entry
** Time Value: 983632 seconds
** Data Object Contents: AVI format video file covering 1 minute at 25fps
```
