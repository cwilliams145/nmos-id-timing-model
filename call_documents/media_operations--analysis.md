# Purpose

This document describes common production operations which may be used together in pieces of live equipment or offline processes. It is intended to be used as a set of building blocks to test model implementation proposals against to identify how use cases are met having passed content through a processing chain.

# Operations

Note that these operations have been split up to be as simple as possible. Some common pieces of equipment may perform a collection of these operations together in order to achieve their goal. A secondary analysis of this document will identify where optimisations could be made in how many TDSs or Similarity Clusters are required in order to fully represent the identity and timing changes.

Note also that as TDSs are a digital (time domain sampled) concept, it is assumed here that all operations are performed in the digital domain. Some additional consideration of the impact of analogue signal paths will be necessary later, particularly as we consider practical system timing in more detail.

It is important to note that Time Context shifts are considered as a separate operation in their own right. In all other operations, the TDSs being operated upon must align in terms of Time Values and share the same Time Context.


*   Capture
    *   Converts light, sound or other physical inputs into a digital signal. Intended to signify the points at which content which can be physically processed comes into being. As such it could include the creation of purely synthesised content.
    *   Ancestry:
        *   New TDS (0:1)
        *   New Similarity Cluster (0:1) (first time the TVI can have identity associated)
        *   Same TVI
        *   New Time Values
        *   No Ancestry Mapping


*   Output
    *   Converts a digital signal into light, sound or other physical outputs. Intended to signify the points at which content which can be physically processed goes out of being.
    *   Ancestry:
        *   No New TDS (1:0)
        *   No New Similarity Cluster (1:0) (TVI can no longer have identity associated)
        *   Same TVI
        *   No New Time Values
        *   No Ancestry Mapping


*   Switch
    *   Produces an output which could take any of a number of inputs, but can only ever consist of a single input's data at any one time.
    *   *Note:* This covers the case where we care about associating a single identity with the output TDS, recording editorial decisions. A more system-level operation such as re-tuning a receiver to handle a stream of a different TDS need not change its identity.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New TVI
        *   No New Time Values
        *   Ancestry requires: TDS to TDS and/or Similarity Cluster to Similarity Cluster mapping (1:1 at any instant), including Time Values


*   Mix
    *   Combines multiple inputs to create a new output which is a composite of one or more of the inputs. This may be by performing Switch operations, or by blending a set of inputs together to produce an output which consists of multiple inputs' data at a single point in time. When blending inputs, all of their Time Values must match, and the corresponding output Data Objects must be associated with the same Time Value.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New TVI
        *   No New Time Values
        *   Ancestry requires: TDS to TDS and/or Similarity Cluster to Similarity Cluster mapping (1..\*:1 at any instant), including Time Values


*   Sample Rate Conversion
    *   Takes time domain sampled content and produces a new output with a different sampling rate, but conveying the same content over the same duration. NB: Includes video frame rate conversion which may involve interpolation, but does not include time stretches such as 24Hz->25Hz where the same content is played back without modification, but at a different rate.
    *   Ancestry:
        *   New TDS
        *   Optional New Similarity Cluster - this will depend on the additional constraints applied to the definition of the Similarity Cluster in use. (Same TVI in any case)
        *   Same TVI
        *   Some New Time Values - these will be required for interpolated samples, but would be generated based upon the input Time Values.
        *   Ancestry requires: TDS to TDS mapping (1:1 for all time). No ancestry change required in terms of Similarity Clusters where the same one is used, but a 1:1 mapping in cases where a new Similarity Cluster is created.


*   Slow Motion / Speed Up
    *   Takes content which was recorded at a specific rate and plays it back at a faster or slower rate as desired (i.e. changing its duration). This maintains a 1:1 relationship between input and output Data Objects, and so may not include frame drops / repeats, or interpolation between frames.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New TVI
        *   New Time Values
        *   Ancestry requires: TDS to TDS and Similarity Cluster to Similarity Cluster mapping. Always 1:1 in terms of identity and input to output Data Objects. Time Values at output will refer to different input Time Values.


*   Split (see also Combine)
    *   Takes input content which may consist of multiple components (for example multiple audio channels, or an SDI multiplex) and splits it into smaller units (for example single audio channels, or mono-essence components of a mux), without changing their timing relationship.
    *   Ancestry:
        *   New TDS(s)
        *   New Similarity Cluster(s) (due to a new TVI)
        *   New TVI
        *   Ancestry requires: TDS to TDS and/or Similarity Cluster to Similarity Cluster mapping (1:1..\*). Time Values not necessary.
    *   Extra Notes:
        *   Ancestry is one way of describing what's going on here but some "group" mechanisms may also be useful / more useful.
        *   If using ancestry then you may want to be able to specify extra details along with the ancestry relationship e.g. which channel inside the mux was the source of the extracted channel


*   Combine (see also Split)
    *   Takes multiple pieces of input content which may consist of matching or differing essence formats, merging them into a single entity (TDS). This may include taking several individual audio channels and combining them into a single multi-channel representation, or combining video and audio into an SDI multiplex for example.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to a new TVI)
        *   New TVI
        *   Ancestry requires: TDS to TDS and/or Similarity Cluster to Similarity Cluster mapping (1..\*:1). Time Values not necessary.
    *   Extra Notes:
        *   See notes for the Split operation.


*   Amplify / Attenuate
    *   Applies a multiplier to an aspect of a piece of content.
    *   Ancestry:
        *   New TDS
        *   Possible New Similarity Cluster (may or may not be the same TVI)
        *   Possible New TVI
        *   Ancestry requires: TDS to TDS (1:1) for all time. Potentially Similarity Cluster relationship too.


*   Storage
    *   Takes already captured content and stores it 'to disk' without byte modification. Note that any time re-mapping prior to storage should be handled via another operation.
    *   Ancestry:
        *   Same TDS
        *   Same Similarity Cluster
        *   Same TVI
        *   No ancestry modification


*   Stored Content Access
    *   Provides access to content stored 'on disk' without making any changes to the Data Objects or Time Values. See also Data Transfer
    *   Ancestry:
        *   Same TDS
        *   Same Similarity Cluster
        *   Same TVI
        *   No ancestry modification


*   Stored Content Replay
    *   Retrieves data from a store before re-timing it for playout purposes, for example in order to synchronise it with other data being played out which was initially recorded at a different time.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New TVI
        *   Ancestry requires: TDS to TDS and Similarity Cluster (1:1) for all time. Note that this assumes the re-timing operation uses a constant offset from the recorded content. Any variability in re-timing may need to be modelled separately.


*   Format Conversion (e.g. Transport Mapping)
    *   Takes input data and converts it into another format in a non-destructive reversible fashion. For example the conversion from raw digital video frames into RTP packets, or conversion of a pure coded H.264 bitstream into an MXF file. This may be closely coupled to Storage or Retrieval in some cases.
    *   Ancestry:
        *   See extra notes. This may involve no change to identity, or may 'fork' within the new format's context, producing new identity which is only valid within a certain scope.
    *   Extra Notes:
        *   The mapping here will depend upon the contexts in which it is necessary to refer to the individual Data Objects and Time Values that make up the TDS. If an RTP stream is viewed as an encapsulation format and as such a 'black box' then there is no need to associate new identity and timing with the stream itself.


*   Data Transfer
    *   Copies content from one location to another without performing any changes to the content or its associated metadata. This may take a full 'file' or a segment of it.
    *   Ancestry:
        *   Same TDS
        *   Same Similarity Cluster
        *   Same TVI
        *   Ancestry requires: No changes


*   Encode / Decode
    *   Takes input content and produces an approximation of the input content which may or may not be an entirely reversible operation. The content represented should cover the same time period, but may be reduced in spatial resolution. Includes the reverse operation.
    *   Ancestry:
        *   New TDS
        *   Optional New Similarity Cluster - this will depend on the additional constraints applied to the definition of the Similarity Cluster in use. (Same TVI in any case)
        *   Same TVI
        *   Ancestry requires: TDS to TDS mapping. Always 1:1 for all time.
    *   Extra Notes:
        *   Whilst in the general case this isn't a new TVI, if the operation is being performed in order to generate an 'artistic effect' rather than to optimise it for a particular communications channel, this would be a candidate for a new TVI and Similarity Cluster as a result.


*   Time Shift
    *   Takes some original content and re-positions it to appear at a different time. It should maintain the original playback/recording rate and as such the same duration. This does not include changes of Time Context, or live modification of the Time Value offset being applied.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster
        *   New TVI
        *   Ancestry requires: TDS to TDS and Similarity Cluster to Similarity Cluster mapping. Always 1:1. Any output Time Value can be linked back to its corresponding input Time Value (ie. the same Data Object) via a simple time offset which is constant over the lifetime of the TDS.


*   Content Analysis
    *   Performs an analysis operation on individual media elements or sequences, producing a data set which may be used by other operations. The data set has concrete references to the content which was analysed to produce the results.
    *   Ancestry
        *   New TDS
        *   New Similarity Cluster
        *   New TVI
        *   Ancestry requires: TDS to TDS and Similarity Cluster to Similarity Cluster mapping. Always 1:1. Time Value mapping will depend upon how many input Data Objects were used to generate each output Data Object. As-per the Encode/Decode process, this relationship may be encapsulated within the Data Objects.


*   Video Crop / Zoom
    *   Selects a lower resolution image from within a larger one.
    *   NB: Assumes the picture remains at its lower resolution and isn't mixed with anything else (e.g. a black frame).
    *   Ancestry
        *   New TDS
        *   Likely New Similarity Cluster (if new TVI)
        *   Likely New TVI
    *   Extra Notes:
        *   Whether this is a new TVI or not depends on the intent. If it is for editorial / creative reasons then this should result in a new TVI. If it is a purely technical operation, perhaps to cut out a clean area then there is no strict requirement that it must be. A pan and scan operation (for example) may result in something which is considered as the same TVI, as the operation was only performed to match the technical constraints of a display.


*   Video Squeeze / Squash
    *   Reducing the resolution in one dimension only, modifying the aspect ratio whilst maintaining the original field of view.
    *   NB: Assumes the picture remains at its lower resolution and isn't mixed with anything else (e.g. a black frame).
    *   Ancestry
        *   New TDS
        *   Likely New Similarity Cluster (if new TVI)
        *   Likely New TVI
    *   Extra Notes:
        *   As in many other cases, the identity may depend upon the intent. If the squeeze was performed with the intent of returning the image to its full scale (ie. a lossy encode operation) it may not be a new TVI. If the intent was instead to squash the picture in order to mix it with another (ie. as part of a 'credits squeeze' operation) this would be a new TVI.


*   Video Keying
    *   Takes a 'key' and 'fill' as inputs, merging them to produce a single output image which is a composite of the two.
    *   Ancestry
        *   New TDS
        *   New Similarity Cluster
        *   New TVI
    *   Extra Notes
        *   This has a strong degree of similarity to a mix operation.


*   DOG / Overlay Insertion
    *   This has a strong degree of similarity to a mix operation.


*   Audio / Video Watermarking
    *   This has a strong degree of similarity to a mix operation.


*   Audio / Video Bit Depth Modification
    *   Increasing or decreasing the number of bits available to store each sample.
    *   Ancestry
        *   New TDS
        *   Same Similarity Cluster
        *   Same TVI


*   Chroma Subsampling Modification
    *   Changing the video from 4:4:4 to 4:2:2 subsampling or similar.
    *   Ancestry
        *   New TDS
        *   Same Similarity Cluster
        *   Same TVI


*   Byte Packing Modification
    *   Converting between v210 and 10 bit planar, or between UYVY and YUY2, maintaining the original samples in tact.
    *   Ancestry
        *   New TDS
        *   Same Similarity Cluster
        *   Same TVI


*   Colorspace Conversion
    *   Converting between (for example) BT.2020 to BT.709.
    *   Ancestry
        *   New TDS
        *   Same Similarity Cluster
        *   Same TVI
    *   Extra Notes
        *   Typically as this covers the case of an HDR to SDR downconversion it would be the same TVI, but the differences between the TDSs would be identified via technical metadata and ancestry.


*   Colour Encoding Conversion
    *   Converting between (for example) YUV and RGB.
    *   Ancestry
        *   New TDS
        *   Same Similarity Cluster
        *   Same TVI


*   Loss of Chroma
    *   Generating a black and white signal from a colour one.
    *   Ancestry
        *   New TDS
        *   Likely Same Similarity Cluster (if same TVI)
        *   Likely Same TVI
    *   Extra Notes
        *   This sort of operation may typically be used for purely technical reasons (e.g. to match a display's capabilities). If carried out for editorial effect, this should be a new TVI.


*   Video Resolution Modification
    *   For example a UHD to HD modification, maintaining the original aspect ratio.
    *   Ancestry
        *   New TDS
        *   Same Similarity Cluster
        *   Same TVI
    *   Extra Notes
        *   Ancestry would assist here with identifying poor quality pictures (for example after a sequence of upscales).


*   EQ Modification
    *   Amplify or attenuate using filters affecting particular frequency ranges (NB: a real EQ may result in a more complex end result).
    *   Ancestry
        *   New TDS
        *   Likely New Similarity Cluster (if new TVI)
        *   Likely New TVI
    *   Extra Notes
        *   This is usually performed for creative / editorial reasons and as such would be a new TVI. Where this is performed for purely technical reasons (e.g. EQ of a room) it may be the same TVI, but this 'specialism' should be recorded against the TDS via some form of tag or attribute.


*   Time Context Re-Mapping
    *   Creates a copy of a TDS, but with different Time Values which are relevant to a different Time Context.
    *   Ancestry
        *   New TDS
        *   New Similarity Cluster
        *   Same TVI


*   Frame Synchroniser / Rate Conforming Operation
    *   Creates a new TDS which is well aligned to a time grid where the input had an unintentional frequency or phase offset from the intended rate. This is likely to involve frame drops or repeats, Time Value re-assignment, and potentially a Time Context change.
    *   Ancestry
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New TVI


*   Audio Echo Sound Effect
    *   Plays back an attenuated and delayed version of an input TDS several times in order to produce the output TDS.
    *   Note: This could be built as a composite of attenuation, delay and mix operations (in the basic case).
    *   Ancestry
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New TVI


*   Buffer / Highly Latent Connection
    *   Stores content for a period of time before allowing it to flow out without any byte modification. See also Storage and Stored Content Access. Changes to Time Values are not permitted.
    *   Ancestry
        *   Same TDS
        *   Same Similarity Cluster
        *   Same TVI


*   Variable Time Shift (including Delay Line)
    *   A Time Shift operation which includes a user control to modify the offset between the input and output TDS. This will modify the ancestry between individual Data Objects / Time Values over the running time of a system.
    *   NB: Unlike a pure buffer, a traditional delay line modifies the implicit Time Values in a sequence in order to change its relationship to time (and as a result match up with other sequences' timing).
    *   Ancestry
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New TVI
    *   Extra Notes
        *   Output Time Values are expected to be monotonic and not repeating. A naive implementation may permit repeats which would result in a confusing TDS if stored. Some implementations may however repeat frames (in the video case) after an adjustment until the correct Data Object was ready. In this case the ancestry between output and input Data Objects would be more complex.
