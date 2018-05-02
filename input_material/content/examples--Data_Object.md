# Examples of `Data Object`s

Each example `Data Object`s given below is intended to represent a fixed sequence of bytes. For many of these examples alternative `Data Object`s could be created &ndash; for example, by introducing extra padding or by changing the order in which items occur inside the `Data Object`. These alternative `Data Object`s would consist of a different sequence of bytes and so, at a base level, would not be considered identical. This holds true even if the same piece of content at the same level of detail (e.g. spatial and temporal resolution) is represented by the alternative `Data Object`.

* Raw 10-bit 4:2:2 1920x1080 progressive video frame in v210 format (5,529,600 bytes)
* Raw 10-bit 4:2:2 1920x1080 interlaced video frame (both fields) in v210 format (5,529,600 bytes)
* Raw 10-bit 4:2:2 1920x1080 interlaced video field (single field) in v210 format
* H264 10-bit format video I frame
* H264 8-bit format video B frame
* H264 8-bit format video GOP of length 25 frames
* 1 raw 24 bit linear PCM audio sample from a single mono audio channel (3 bytes)
* 1920 raw 24-bit linear PCM audio samples covering a single mono audio channel (5760 bytes)
* 1920 raw 24-bit linear PCM audio samples per-channel covering 16 channels, packed with channels in an interleaved format (92,160 bytes)
* AAC encoded 960 sample block of 8 audio channels at 64kb/s
* JSON payload representing the value sampled from a temperature sensor in degrees C, with separate keys/values for the integer and fractional part of the measurement
* JSON payload containing the same content as previous, but with the keys listed in the opposite order (fractional part first, then integer)
* SDI (ST.292M) bit-stream contents representing a single video frame plus associated audio samples (including Line Count, CRC, HANC, SAV, Video, VANC and EAV)
* Non-standard structure containing a 10-bit video frame in v210 format, and a single 3 byte L24 audio sample across 8 channels, plus GPS coordinates (lat/lon) in 32 bit containers. Each `Data Object` may consist of one or more of these elements.

By way of one further example, a v210 format 1920x1080 4:2:2 10-bit black video frame which is byte identical to another black video frame can be viewed as a duplicate of the same `Data Object` at this level of data modelling. This holds true even if these two black frames originated from different devices in different countries at different times. In a practical implementation of this model these entities may be treated as distinct `Data Object`s despite being identical.

