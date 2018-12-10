:warning: **This file is part of the "archive" &ndash; it could contain statements or terms which are incompatible with the main body of the specification and the identity and timing model.** :warning:

# Production Operations

This document explores a range of common production operations and the requirements for tracking identity and timing through them.

## Basic Operations

The following set of basic operations have been identified (and grouped).

**Grey SCs &amp; TVIs:** If the content is modified for purely technical reasons, it's likely to be the same TVI / SC. If it's modified for editorial reasons it's likely to be a new TVI / SC. If in doubt, considering each case as a new TVI / SC would avoid errors, but might mean additional steps for users in navigating between similar media.

### No Identity Change

*   Storage
*   Stored Content Access (ie. no re-timing)
*   Internal Lossless Format Conversion (ie. within 'black box')
*   Data Transfer
*   Buffer / Highly Latent Connection

### 0:1 TDS

#### New TDS, New SC, Same TVI

*   Capture

### 1:0 TDS

#### No New TDS, No New SC, Same TVI

*   Output

### 1:1 TDS

#### New TDS, New SC, New TVI

*   Slow Motion / Speed Up
*   Stored Content Replay (ie. with re-timing)
*   Time Shift
*   Content Analysis
*   Frame Synchroniser / Rate Conforming Operation
*   Variable Time Shift (including Delay Line)

#### New TDS, New SC, Same TVI

*   Time Context Re-Mapping

#### New TDS, Same SC Permitted (due to same TVI), Same TVI

*   Audio / Video Bit Depth Modification
*   Chroma Subsampling Modification
*   Byte Packing Modification
*   Colorspace Conversion
*   Colour Encoding Conversion
*   Video Resolution Modification
*   Sample Rate Conversion
*   Encode / Decode

#### New TDS, Grey SC (due to grey TVI), Grey TVI

*   Amplify / Attenuate
*   Video Crop / Zoom
*   Video Squeeze / Squash
*   Conversion to monochrome
*   EQ Modification

### 1..\*:1 TDS

#### New TDS, New SC, New TVI

*   Switch
*   Mix
*   Combine
*   Video Keying
*   DOG Overlay / Insertion
*   Audio / Video Watermarking

### 1:1..\* TDS

#### New TDS, New SC, New TVI

*   Split
