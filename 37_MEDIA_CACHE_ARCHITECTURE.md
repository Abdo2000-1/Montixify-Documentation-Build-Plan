# 37_MEDIA_CACHE_ARCHITECTURE.md

# Montixify Media Cache Architecture

Version: 1.0

## Purpose

This document defines the multi-level caching architecture used by
Montixify to accelerate media loading, timeline playback, rendering and
export.

The cache subsystem must reduce redundant work while maintaining
correctness.

------------------------------------------------------------------------

# Objectives

-   Faster playback
-   Faster timeline navigation
-   Lower CPU usage
-   Reduced FFmpeg calls
-   Predictable memory usage
-   Safe cache invalidation

------------------------------------------------------------------------

# Cache Layers

``` text
Application
    │
    ▼
Cache Manager
 ┌──────────────┐
 │ Memory Cache │
 │ Disk Cache   │
 │ Proxy Cache  │
 │ Frame Cache  │
 │ Thumbnail    │
 │ Waveform     │
 └──────────────┘
```

------------------------------------------------------------------------

# Cache Types

## Metadata Cache

Stores:

-   Duration
-   Resolution
-   Frame rate
-   Codec
-   Audio information

Purpose:

Avoid repeated FFprobe execution.

------------------------------------------------------------------------

## Thumbnail Cache

Stores generated thumbnails.

Requirements:

-   Background generation
-   Configurable resolution
-   Lazy loading
-   Automatic regeneration

------------------------------------------------------------------------

## Frame Cache

Stores decoded video frames.

Requirements:

-   LRU eviction
-   Reusable buffers
-   Frame range indexing

------------------------------------------------------------------------

## Waveform Cache

Stores generated audio waveforms.

Benefits:

-   Fast timeline rendering
-   Faster zoom operations

------------------------------------------------------------------------

## Proxy Cache

Stores proxy media for editing.

Support:

-   360p
-   720p
-   User-defined quality

Proxy generation should execute asynchronously.

------------------------------------------------------------------------

# Memory Cache

Designed for active editing.

Rules:

-   Fast access
-   Size limited
-   Automatic eviction
-   Thread-safe

------------------------------------------------------------------------

# Disk Cache

Stores reusable assets between sessions.

Examples:

-   Thumbnails
-   Waveforms
-   Proxy files
-   Intermediate renders

------------------------------------------------------------------------

# Cache Keys

Every cache entry should include:

-   AssetId
-   Hash
-   Version
-   Parameters
-   Timestamp

------------------------------------------------------------------------

# Cache Invalidation

Invalidate when:

-   Source file changes
-   Parameters change
-   Application version changes
-   Cache format changes

Never invalidate unrelated entries.

------------------------------------------------------------------------

# Eviction Policy

Preferred:

-   LRU (Least Recently Used)

Future options:

-   LFU
-   Priority-based eviction

------------------------------------------------------------------------

# Cache Budgets

Memory Cache

-   Configurable upper limit

Disk Cache

-   Configurable maximum size
-   Automatic cleanup threshold

------------------------------------------------------------------------

# Integrity Checks

Verify:

-   File exists
-   Hash matches
-   Version compatible
-   Entry readable

Corrupted entries should be removed automatically.

------------------------------------------------------------------------

# Background Maintenance

Tasks:

-   Cleanup expired entries
-   Compress cache (future)
-   Rebuild indexes
-   Remove orphaned files

Run with low priority.

------------------------------------------------------------------------

# Performance Metrics

Track:

-   Cache hit rate
-   Cache miss rate
-   Eviction count
-   Memory usage
-   Disk usage
-   Average lookup time

------------------------------------------------------------------------

# Threading

Worker Threads:

-   Cache creation
-   Cleanup
-   Validation
-   Proxy generation

UI Thread:

-   Status updates only

------------------------------------------------------------------------

# AI Extension Points

Reserve:

-   ICacheOptimizer
-   IProxyQualityAdvisor
-   ICachePredictionStrategy

No implementations in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Cache limits enforced
-   Integrity verified
-   Eviction tested
-   Invalidation tested
-   Thread safety reviewed
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

Media Cache Architecture is complete only if:

-   Cache improves performance
-   Memory remains bounded
-   Disk cleanup works
-   Corruption is detected
-   Metrics are available
-   Tests pass
-   Documentation updated

------------------------------------------------------------------------

End of File
