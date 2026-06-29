# 16_FFMPEG_INTEGRATION.md

# Montixify FFmpeg Integration Specification

Version: 1.0

## Purpose

This document defines how Montixify integrates with FFmpeg and FFprobe.

FFmpeg is the media processing backend responsible for decoding,
encoding, transcoding, frame extraction and metadata analysis.

The integration layer must isolate FFmpeg-specific implementation
details from the rest of the application.

------------------------------------------------------------------------

# Design Goals

-   Backend abstraction
-   Replaceable implementation
-   High performance
-   Reliable process management
-   Extensible encoder support
-   Future GPU acceleration

------------------------------------------------------------------------

# Responsibilities

The FFmpeg integration layer shall:

-   Discover FFmpeg binaries
-   Validate versions
-   Execute FFmpeg commands
-   Execute FFprobe commands
-   Parse progress
-   Parse metadata
-   Handle cancellation
-   Report errors
-   Log execution

------------------------------------------------------------------------

# Architecture

``` text
Application
      |
Media Services
      |
IFFmpegService
      |
--------------------------
| Command Builder        |
| Process Runner         |
| FFprobe Service        |
| Progress Parser        |
| Encoder Registry       |
--------------------------
      |
FFmpeg / FFprobe
```

The rest of the application must never invoke FFmpeg directly.

------------------------------------------------------------------------

# Binary Discovery

Search order:

1.  Configured path
2.  Application tools folder
3.  Environment PATH
4.  User-defined location

If binaries are unavailable:

-   Log the failure
-   Notify the user
-   Disable dependent features

------------------------------------------------------------------------

# FFprobe Integration

FFprobe shall be used for:

-   Duration
-   Resolution
-   Frame rate
-   Bitrate
-   Codec
-   Audio streams
-   Subtitle streams
-   Rotation metadata

Metadata should be cached after extraction.

------------------------------------------------------------------------

# Command Builder

Construct commands using a dedicated builder.

Avoid manual string concatenation.

Responsibilities:

-   Validate arguments
-   Escape paths
-   Apply presets
-   Select codecs
-   Configure hardware acceleration

------------------------------------------------------------------------

# Process Runner

The Process Runner shall:

-   Start processes
-   Capture stdout
-   Capture stderr
-   Support cancellation
-   Enforce timeouts
-   Return exit codes

No UI code may execute process logic.

------------------------------------------------------------------------

# Progress Parsing

Read FFmpeg progress information.

Expose:

-   Percentage
-   Current frame
-   FPS
-   Speed
-   ETA
-   Bitrate

Progress updates should be throttled before reaching the UI.

------------------------------------------------------------------------

# Encoding

Support:

Video

-   H.264
-   H.265
-   VP9
-   AV1 (future)

Audio

-   AAC
-   MP3
-   FLAC
-   PCM

The encoder registry must allow future additions.

------------------------------------------------------------------------

# Hardware Acceleration

Architecture should support:

-   NVIDIA NVENC
-   Intel Quick Sync
-   AMD AMF

Hardware availability should be detected at runtime.

Fallback gracefully to CPU encoding.

------------------------------------------------------------------------

# Error Mapping

Map FFmpeg exit codes into domain-specific exceptions.

Examples:

-   EncoderNotFoundException
-   InvalidCodecException
-   MediaDecodeException
-   ExportFailedException

Avoid exposing raw FFmpeg errors directly to end users.

------------------------------------------------------------------------

# Logging

Log:

-   Command start
-   Command finish
-   Exit code
-   Duration
-   Parsed warnings
-   Parsed errors

Never log sensitive file paths unless diagnostic mode is enabled.

------------------------------------------------------------------------

# Security

-   Escape command arguments
-   Validate file paths
-   Prevent command injection
-   Reject unsupported protocols

Never execute arbitrary user commands.

------------------------------------------------------------------------

# Threading Model

Worker Threads

-   Process execution
-   Metadata parsing
-   Progress parsing

UI Thread

-   Progress display
-   User interaction

Heavy operations must remain off the UI thread.

------------------------------------------------------------------------

# Testing Strategy

Test:

-   Missing binaries
-   Invalid media
-   Large files
-   Cancellation
-   Progress parsing
-   Hardware encoder detection

Mock process execution where appropriate.

------------------------------------------------------------------------

# Future AI Extension Points

Reserve interfaces:

-   IEncodingAdvisor
-   ICodecRecommendationProvider
-   IAdaptiveExportPlanner

No implementations in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Binary discovery tested
-   Progress parser verified
-   Cancellation works
-   Errors mapped
-   Hardware detection verified
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

FFmpeg integration is complete only if:

-   Commands execute reliably
-   Metadata extraction works
-   Progress is reported
-   Errors are mapped correctly
-   Logging is complete
-   Build and tests succeed
-   Documentation updated

------------------------------------------------------------------------

End of File
