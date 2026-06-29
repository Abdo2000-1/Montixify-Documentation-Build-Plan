# 12_MEDIA_ENGINE.md

# Montixify Media Engine Specification

Version: 1.0

## Purpose

The Media Engine is responsible for importing, indexing, validating,
managing, and exposing all media assets used by Montixify.

It is the foundation of the editor and must remain independent from the
UI.

------------------------------------------------------------------------

# Objectives

-   Fast media import
-   Reliable metadata extraction
-   Thumbnail generation
-   Asset indexing
-   Duplicate detection
-   Offline media detection
-   Future extensibility

------------------------------------------------------------------------

# Supported Media Types

## Video

-   MP4
-   MOV
-   MKV
-   AVI
-   WEBM

## Audio

-   MP3
-   WAV
-   FLAC
-   AAC
-   OGG

## Images

-   PNG
-   JPG
-   JPEG
-   BMP
-   TIFF
-   WEBP

Future support must be added through import providers.

------------------------------------------------------------------------

# Responsibilities

The Media Engine shall:

-   Import media
-   Validate files
-   Read metadata
-   Generate thumbnails
-   Detect duplicates
-   Monitor missing files
-   Cache metadata
-   Notify application services of changes

------------------------------------------------------------------------

# Architecture

``` text
UI
 |
Application
 |
Media Engine
 |------ Metadata Reader
 |------ Thumbnail Generator
 |------ Cache Manager
 |------ Asset Registry
 |------ File Validator
```

------------------------------------------------------------------------

# Import Pipeline

``` text
Select File
    ↓
Validate
    ↓
Extract Metadata
    ↓
Generate Thumbnail
    ↓
Create Media Asset
    ↓
Store Registry
    ↓
Notify UI
```

Every stage must be independently testable.

------------------------------------------------------------------------

# Media Asset Model

Minimum properties:

-   Id
-   FilePath
-   FileName
-   MediaType
-   Duration
-   Resolution
-   FrameRate
-   Codec
-   Bitrate
-   AudioChannels
-   ThumbnailPath
-   CreatedDate

------------------------------------------------------------------------

# Metadata

Metadata extraction should occur once.

Cache results to avoid repeated FFprobe execution.

------------------------------------------------------------------------

# Thumbnail Generation

Requirements:

-   Background processing
-   Configurable size
-   Cache thumbnails
-   Regenerate when missing

Never block the UI thread.

------------------------------------------------------------------------

# Cache

Cache should contain:

-   Metadata
-   Thumbnails
-   Waveforms (future)
-   Proxy information (future)

Support automatic cleanup.

------------------------------------------------------------------------

# Missing Media

Detect:

-   Deleted files
-   Renamed files
-   Offline drives

Provide relink workflow.

------------------------------------------------------------------------

# Duplicate Detection

Identify duplicates using:

-   Hash (preferred)
-   Size
-   Creation date
-   Filename (fallback only)

------------------------------------------------------------------------

# Events

Expose events for:

-   Asset Imported
-   Asset Removed
-   Asset Updated
-   Thumbnail Ready
-   Metadata Updated

------------------------------------------------------------------------

# Performance Targets

Import should remain responsive.

Metadata extraction should execute asynchronously.

Thumbnail generation should be queued.

------------------------------------------------------------------------

# Error Handling

Recoverable:

-   Unsupported format
-   Missing codec
-   Thumbnail failure

Fatal:

-   Corrupted registry
-   Invalid cache database

------------------------------------------------------------------------

# Future AI Extension Points

Reserve interfaces only:

-   IMediaAnalyzer
-   ISceneClassifier
-   IObjectDetector
-   ITranscriptProvider

No implementations in Version 1.

------------------------------------------------------------------------

# Review Checklist

-   Async import
-   Metadata cached
-   Thumbnails cached
-   Validation complete
-   Build passes
-   Tests updated
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

Media Engine work is complete when:

-   Assets import successfully
-   Metadata available
-   Thumbnails generated
-   Duplicate detection functional
-   Missing media detection implemented
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

End of File
