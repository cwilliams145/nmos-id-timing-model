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
        *   New Time Values
        *   No Ancestry Mapping


*   Output
    *   Converts a digital signal into light, sound or other physical outputs. Intended to signify the points at which content which can be physically processed goes out of being.
    *   Ancestry:
        *   No New TDS (1:0)
        *   No New Similarity Cluster (1:0) (TVI can no longer have identity associated)
        *   No New Time Values
        *   No Ancestry Mapping


*   Switch
    *   Produces an output which could take any of a number of inputs, but can only ever consist of a single input's data at any one time.
    *   *Note:* This covers the case where we care about associating a single identity with the output TDS, recording editorial decisions. A more system-level operation such as re-tuning a receiver to handle a stream of a different TDS need not change its identity.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   No New Time Values
        *   Ancestry requires: TDS to TDS and/or Similarity Cluster to Similarity Cluster mapping (1:1 at any instant), including Time Values


*   Mix
    *   Combines multiple inputs to create a new output which is a composite of one or more of the inputs. This may be by performing Switch operations, or by blending a set of inputs together to produce an output which consists of multiple inputs' data at a single point in time. When blending inputs, all of their Time Values must match, and the corresponding output Data Objects must be associated with the same Time Value.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   No New Time Values
        *   Ancestry requires: TDS to TDS and/or Similarity Cluster to Similarity Cluster mapping (1..\*:1 at any instant), including Time Values


*   Sample Rate Conversion
    *   Takes time domain sampled content and produces a new output with a different sampling rate, but conveying the same content over the same duration. NB: Includes video frame rate conversion which may involve interpolation, but does not include time stretches such as 24Hz->25Hz where the same content is played back without modification, but at a different rate.
    *   Ancestry:
        *   New TDS
        *   Optional New Similarity Cluster - this will depend on the additional constraints applied to the definition of the Similarity Cluster in use. (Same TVI in any case)
        *   Some New Time Values - these will be required for interpolated samples, but would be generated based upon the input Time Values.
        *   Ancestry requires: TDS to TDS mapping (1:1 for all time). No ancestry change required in terms of Similarity Clusters where the same one is used, but a 1:1 mapping in cases where a new Similarity Cluster is created.


*   Slow Motion / Speed Up
    *   Takes content which was recorded at a specific rate and plays it back at a faster or slower rate as desired (i.e. changing its duration). This maintains a 1:1 relationship between input and output Data Objects, and so may not include frame drops / repeats, or interpolation between frames.
    *   Ancestry:
        *   New TDS
        *   New Similarity Cluster (due to new TVI)
        *   New Time Values
        *   Ancestry requires: TDS to TDS and Similarity Cluster to Similarity Cluster mapping. Always 1:1 in terms of identity and input to output Data Objects. Time Values at output will refer to different input Time Values.


*   Split (see also Combine)
*   Combine (see also Split)
*   Amplify / Attenuate
*   Storage / Retrieval
*   Format Conversion
*   Data Transfer
*   Encode / Decode
*   Time Shift
*   Content Analysis
*   Video Crop / Zoom
*   Video Squeeze / Squash
*   Video Keying
*   Audio / Video Bit Depth Modification
*   Chroma Subsampling Modification
*   Byte Packing Modification
*   Colorspace Conversion
*   Video Resolution Modification
*   EQ Modification
*   Time Context Re-Mapping
*   Frame Synchroniser / Rate Conforming Operation
*   Audio Echo Sound Effect
