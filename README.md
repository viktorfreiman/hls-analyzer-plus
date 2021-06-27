# HLS Analyzer

Last Updated: 2021-06-27
Current verion is in setup.cfg

Fork of <https://github.com/epiclabs-io/hls-analyzer>

- [HLS Analyzer](#hls-analyzer)
  - [TODO](#todo)
  - [Command line tool syntax](#command-line-tool-syntax)
  - [Example of use](#example-of-use)
  - [Third party libraries](#third-party-libraries)
  - [Changelog](#changelog)
    - [0.1.0-draft](#010-draft)

## TODO

Not working right now

Adds:

- Refreshed and cleaned up code to work with python3
- Dependency update
- JSON printout
- Web api
- Added devcontainer
- Added docker img
- Added lint and formater
- Added semver

Tool for analyzing HTTP Live Streams (HLS) compatible with both VOD and Live content.

It analyzes TS segments of the stream and provide useful information about the content, pretty useful to catch encoding or playback quality issues:

- HLS information. Type of the stream (live or vod), media sequence, type of encryption and number of segments.
- Tracks information. Video and audio tracks information (codecs, profiles, resolution, sample rate, channels, etc)
- Timing information (PTS and segment duration). Useful to check if bitrates and segments are properly aligned.
- Frames information. Keyframe interval, frames sequence. Useful to check if every segment starts with a keyframe. Useful to ensure smooth bitrate switching.

## Command line tool syntax

`python hls-analyzer.py [-h] [-s SEGMENTS] [-l FRAME_INFO_LEN] Url`

- `Url`: Url of the stream to be analyzed

Optional arguments:

- `-s SEGMENTS`        Number of segments to be analyzed per playlist. By default, one segment per playlist is analyzed
- `-l FRAME_INFO_LEN`  Max length per track for frames information
- `-h, --help`         Show help message

## Example of use

`python hls-analyzer.py https://devimages.apple.com.edgekey.net/streaming/examples/bipbop_4x3/bipbop_4x3_variant.m3u8`

Output:

~~~text
Master playlist. List of variants:
    Playlist: https://devimages.apple.com.edgekey.net/streaming/examples/bipbop_4x3/gear1/prog_index.m3u8, bw: 232370
    Playlist: https://devimages.apple.com.edgekey.net/streaming/examples/bipbop_4x3/gear2/prog_index.m3u8, bw: 649879


***** Analyzing variant (232370) *****

    ** Generic information **
    Version: 3
    Media sequence: 0
    Is Live: False
    Encrypted: False
    Number of segments: 181
    Downloading https://devimages.apple.com.edgekey.net/streaming/examples/bipbop_4x3/gear1/fileSequence0.ts, Range: None

    ** Tracks and Media formats **
    Track #0 - Type: video/avc, Format: Video (H.264) - Profile: Main, Level: 64, Resolution: 400x300, Encoded aspect ratio: 0/1, Display aspect ratio: 1
    Track #1 - Type: audio/mp4a-latm, Format: Audio (AAC) - Sample Rate: 22050, Channels: 2

    ** Timing information **
    Segment declared duration: 9.97667
    Track #0 - Duration: 9.943333 s, First PTS: 10.0 s, Last PTS: 19.943333 s
    Track #1 - Duration: 9.473739 s, First PTS: 9.904222 s, Last PTS: 19.377961 s
    Duration difference (declared vs real): 0.502931 s (5.31%)

    ** Frames **
    Track #0 - KF: 0.067, Frames: I-I-P-P-B-B-P-P-B-B-P-P-B-B-P-P-B-B-P-P-B-B-P-P-B-B-P-P-B-B-P-P-B-B-P-P-B-B-P-P-
    Track #1 - KF: 0.046, Frames: I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-


***** Analyzing variant (649879) *****

    ** Generic information **
    Version: 3
    Media sequence: 0
    Is Live: False
    Encrypted: False
    Number of segments: 181
    Downloading https://devimages.apple.com.edgekey.net/streaming/examples/bipbop_4x3/gear2/fileSequence0.ts, Range: None

    ** Tracks and Media formats **
    Track #0 - Type: video/avc, Format: Video (H.264) - Profile: Main, Level: 64, Resolution: 640x480, Encoded aspect ratio: 0/1, Display aspect ratio: 1
    Track #1 - Type: audio/mp4a-latm, Format: Audio (AAC) - Sample Rate: 22050, Channels: 2

    ** Timing information **
    Segment declared duration: 9.97667
    Track #0 - Duration: 9.943333 s, First PTS: 10.0 s, Last PTS: 19.943333 s
    Track #1 - Duration: 9.473739 s, First PTS: 9.904222 s, Last PTS: 19.377961 s
    Duration difference (declared vs real): 0.502931 s (5.31%)

    ** Frames **
    Track #0 - KF: 0.067, Frames: I-I-I-I-I-P-P-P-P-P-B-B-B-B-B-P-P-P-P-P-B-B-B-B-B-P-P-P-P-P-B-B-B-B-B-P-P-P-P-P-
    Track #1 - KF: 0.046, Frames: I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-I-
~~~

## Third party libraries

This project uses m3u8 library created by Globo.com: <https://github.com/globocom/m3u8>

## Changelog

### 0.1.0-draft

- Init work with readme
- Added setup.cfg
