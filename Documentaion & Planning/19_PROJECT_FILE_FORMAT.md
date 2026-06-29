# 19_PROJECT_FILE_FORMAT.md

# Montixify Project File Format Specification

Version: 1.0

## Purpose

This document defines the `.mtxproj` project format used by Montixify to
persist editing sessions. The format must be human-readable, versioned,
resilient to future changes, and capable of recovering projects across
software updates.

------------------------------------------------------------------------

# Design Goals

-   Human-readable
-   Versioned
-   Backward compatible
-   Extensible
-   Fast to load
-   Safe against corruption

------------------------------------------------------------------------

# File Extension

Primary project file:

``` text
.mtxproj
```

Optional future companion files:

``` text
.mtxcache
.mtxbackup
.mtxautosave
```

------------------------------------------------------------------------

# Storage Format

Version 1 uses UTF-8 encoded JSON.

Future versions may optionally support compressed archives while
preserving the same logical schema.

------------------------------------------------------------------------

# High-Level Structure

``` text
Project
│
├── Metadata
├── Settings
├── Media
├── Timeline
├── Effects
├── Transitions
├── Markers
├── Export Profiles
└── Custom Data
```

------------------------------------------------------------------------

# Metadata

Required fields:

-   ProjectId
-   ProjectName
-   FormatVersion
-   CreatedAt
-   ModifiedAt
-   CreatedBy
-   ApplicationVersion

------------------------------------------------------------------------

# Settings

Store:

-   Timeline FPS
-   Resolution
-   Theme preference
-   Autosave interval
-   Preview quality

------------------------------------------------------------------------

# Media Section

Each asset shall contain:

-   Id
-   RelativePath
-   AbsolutePath (optional)
-   FileHash
-   Duration
-   Resolution
-   MediaType

The application should prefer relative paths whenever possible.

------------------------------------------------------------------------

# Timeline Serialization

Serialize:

-   Tracks
-   Clips
-   Track order
-   Clip positions
-   Selections (optional)
-   Timeline settings

Runtime caches must never be serialized.

------------------------------------------------------------------------

# Clip Serialization

Each clip contains:

-   ClipId
-   MediaId
-   StartTime
-   EndTime
-   Offset
-   TrackId
-   IsMuted
-   IsLocked

Effects are stored separately.

------------------------------------------------------------------------

# Effects

Each effect entry should contain:

-   EffectId
-   TargetClipId
-   EffectType
-   Parameters
-   Enabled

Unknown effects should be preserved during load/save where possible.

------------------------------------------------------------------------

# Transitions

Serialize:

-   TransitionId
-   SourceClip
-   DestinationClip
-   Type
-   Duration
-   Parameters

------------------------------------------------------------------------

# Markers

Store:

-   MarkerId
-   Timecode
-   Name
-   Color
-   Notes

------------------------------------------------------------------------

# Project Validation

During load:

-   Validate schema version
-   Validate required fields
-   Detect missing media
-   Detect duplicate IDs
-   Reject malformed JSON

------------------------------------------------------------------------

# Versioning

Every project must contain:

FormatVersion

Example:

``` json
{
  "FormatVersion": 1
}
```

Migration handlers should upgrade older versions automatically.

------------------------------------------------------------------------

# Autosave

Autosave files should:

-   Use dedicated extension
-   Never overwrite the main project
-   Be recoverable after crashes

------------------------------------------------------------------------

# Backup Strategy

When saving:

1.  Validate project
2.  Create backup
3.  Write new project
4.  Verify write
5.  Replace previous backup if successful

------------------------------------------------------------------------

# Corruption Recovery

If loading fails:

-   Attempt backup
-   Attempt autosave
-   Report recoverable items
-   Log diagnostics

------------------------------------------------------------------------

# Compression

Future support may compress projects while preserving the internal
schema.

Compression must remain optional.

------------------------------------------------------------------------

# Future AI Extension Points

Reserve metadata sections:

-   AIHistory
-   PromptHistory
-   SuggestedEdits
-   SceneAnnotations

These sections remain empty in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Schema valid
-   Version verified
-   Missing media detected
-   Serialization tested
-   Deserialization tested
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

Project File Format work is complete only if:

-   Projects save correctly
-   Projects load correctly
-   Older versions migrate
-   Corruption recovery functions
-   Documentation updated

------------------------------------------------------------------------

End of File
