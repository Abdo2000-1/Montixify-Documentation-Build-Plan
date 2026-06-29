# 18_IMPORT_EXPORT_PIPELINE.md

# Montixify Import & Export Pipeline Specification

Version: 1.0

## Purpose

This document defines the architecture, workflow, validation rules, and
engineering standards for importing media into Montixify and exporting
finished projects.

The pipeline must be modular, testable, asynchronous, fault-tolerant,
and extensible.

------------------------------------------------------------------------

# Objectives

-   Reliable media import
-   Fast metadata extraction
-   Consistent export behavior
-   Deterministic output
-   Progress reporting
-   Cancellation support
-   Extensible import/export providers

------------------------------------------------------------------------

# High-Level Architecture

``` text
User
 |
Import / Export Service
 |
Pipeline Coordinator
 |-------------------------------|
 |                               |
Import Pipeline          Export Pipeline
 |                               |
Validators              Render Queue
Metadata                Encoder
Registry                FFmpeg
Cache                   Output Writer
```

------------------------------------------------------------------------

# Import Pipeline

## Workflow

``` text
Select Files
    ↓
Validate Paths
    ↓
Detect Media Type
    ↓
Read Metadata
    ↓
Generate Thumbnail
    ↓
Register Asset
    ↓
Update Media Library
    ↓
Notify UI
```

### Validation

Every imported file must be checked for:

-   Existence
-   Read permission
-   Supported format
-   File integrity (basic)
-   Duplicate detection

Failures should never crash the application.

------------------------------------------------------------------------

# Import Providers

The system should support pluggable providers.

Examples:

-   Video Import Provider
-   Audio Import Provider
-   Image Import Provider
-   Image Sequence Provider
-   Future Cloud Provider

------------------------------------------------------------------------

# Export Pipeline

## Workflow

``` text
Validate Project
      ↓
Build Render Graph
      ↓
Prepare Encoder
      ↓
Render Frames
      ↓
Encode Media
      ↓
Write Output
      ↓
Verify Result
      ↓
Notify User
```

------------------------------------------------------------------------

# Export Profiles

Built-in profiles:

-   YouTube 1080p
-   YouTube 4K
-   TikTok Vertical
-   Instagram Reel
-   Lossless
-   Custom

Profiles should be serializable and user-editable.

------------------------------------------------------------------------

# Progress Reporting

Expose:

-   Overall percentage
-   Current stage
-   Current frame
-   Estimated remaining time
-   Encoding speed
-   Output size

Progress events must be throttled before reaching the UI.

------------------------------------------------------------------------

# Cancellation

Users must be able to cancel long-running imports and exports safely.

Cancellation should:

-   Stop background work
-   Release resources
-   Preserve existing project data
-   Leave partial exports clearly marked

------------------------------------------------------------------------

# Retry Strategy

Automatically retry only transient failures.

Do NOT retry:

-   Invalid codec
-   Corrupted media
-   Invalid output path

------------------------------------------------------------------------

# Output Validation

After export:

-   Verify file exists
-   Verify non-zero size
-   Verify expected duration (where practical)
-   Log completion summary

------------------------------------------------------------------------

# Performance Targets

-   Asynchronous processing
-   Minimal UI blocking
-   Streaming where possible
-   Efficient memory usage
-   Parallel preparation stages when safe

------------------------------------------------------------------------

# Logging

Log:

-   Import started/completed
-   Export started/completed
-   Validation failures
-   Cancellation
-   Output summary
-   Performance metrics

------------------------------------------------------------------------

# Future AI Extension Points

Reserve interfaces:

-   IImportAdvisor
-   IExportAdvisor
-   IAutoProfileSelector
-   IQualityRecommendationProvider

No implementations in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Import validation complete
-   Export validation complete
-   Progress reporting verified
-   Cancellation tested
-   Logging verified
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

The Import/Export Pipeline is complete only if:

-   Supported media imports successfully
-   Exports complete reliably
-   Progress is accurate
-   Cancellation works
-   Output validation passes
-   Documentation is updated

------------------------------------------------------------------------

End of File
