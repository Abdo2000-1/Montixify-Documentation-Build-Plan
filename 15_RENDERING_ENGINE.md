# 15_RENDERING_ENGINE.md

# Montixify Rendering Engine Specification

Version: 1.0

## Purpose

The Rendering Engine is responsible for composing timeline content into
visual frames for both real-time preview and final export. It
orchestrates media decoding, effects, transitions, compositing and
encoding while remaining independent from the UI layer.

------------------------------------------------------------------------

# Objectives

-   Frame-accurate rendering
-   Modular render pipeline
-   Deterministic output
-   GPU-ready architecture
-   High performance
-   Extensible effects system

------------------------------------------------------------------------

# Responsibilities

The Rendering Engine shall:

-   Build render graphs
-   Composite layers
-   Apply effects
-   Apply transitions
-   Blend video and graphics
-   Produce preview frames
-   Produce export frames
-   Report render progress

------------------------------------------------------------------------

# High-Level Architecture

``` text
Timeline
    |
Render Coordinator
    |
+--------------------------+
| Render Graph             |
| Effect Pipeline          |
| Transition Pipeline      |
| Compositor               |
| Encoder                  |
+--------------------------+
```

------------------------------------------------------------------------

# Render Pipeline

``` text
Timeline
 ↓
Resolve Clips
 ↓
Decode Frames
 ↓
Apply Clip Effects
 ↓
Apply Transitions
 ↓
Composite Layers
 ↓
Render Frame
 ↓
Encode (Export) / Present (Preview)
```

Each stage must be replaceable and independently testable.

------------------------------------------------------------------------

# Render Graph

The engine shall build a render graph describing frame dependencies.

Benefits:

-   Parallel execution
-   Cache reuse
-   Selective invalidation
-   Future GPU acceleration

------------------------------------------------------------------------

# Composition

Support:

-   Multiple video tracks
-   Alpha blending
-   Opacity
-   Transform
-   Cropping
-   Layer ordering

Composition order must be deterministic.

------------------------------------------------------------------------

# Effects Pipeline

Each effect should:

-   Receive an input frame
-   Produce an output frame
-   Be stateless where possible
-   Support parameter serialization

Effects should not modify source media.

------------------------------------------------------------------------

# Transition Pipeline

Support:

-   Cross Fade
-   Dissolve
-   Wipe
-   Slide

Future transitions should implement a common interface.

------------------------------------------------------------------------

# Preview Rendering

Preview mode should prioritize responsiveness.

Allow:

-   Reduced resolution
-   Frame skipping
-   Adaptive quality

The preview engine must never modify export quality settings.

------------------------------------------------------------------------

# Export Rendering

Export mode prioritizes correctness over speed.

Requirements:

-   Frame accuracy
-   Deterministic output
-   Configurable encoder settings
-   Progress reporting
-   Cancellation support

------------------------------------------------------------------------

# Caching

Cache:

-   Decoded frames
-   Intermediate compositions
-   Effect outputs (when beneficial)

Invalidate cache only when dependencies change.

------------------------------------------------------------------------

# Memory Management

-   Reuse frame buffers
-   Limit cache growth
-   Dispose unmanaged resources promptly
-   Avoid unnecessary allocations

------------------------------------------------------------------------

# Threading Model

UI Thread

-   Progress updates

Worker Threads

-   Decode
-   Effects
-   Composition
-   Encoding

No heavy rendering work may execute on the UI thread.

------------------------------------------------------------------------

# Performance Targets

-   Stable preview
-   Efficient cache usage
-   Parallel processing where safe
-   Minimal frame latency
-   Scalable to long timelines

------------------------------------------------------------------------

# Error Handling

Recoverable:

-   Missing effect
-   Corrupted frame
-   Cache miss

Fatal:

-   Encoder failure
-   Render graph corruption

All failures must be logged.

------------------------------------------------------------------------

# Future AI Extension Points

Reserve interfaces:

-   IRenderOptimizer
-   IEffectSuggestionProvider
-   IAutoColorCorrectionProvider

Version 1 contains interfaces only.

------------------------------------------------------------------------

# Validation Checklist

-   Render graph validated
-   Preview tested
-   Export tested
-   Memory usage reviewed
-   Thread safety verified
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

Rendering Engine is complete when:

-   Frames compose correctly
-   Preview and export share the same pipeline
-   Effects execute in order
-   Memory remains stable
-   Performance targets achieved
-   Documentation updated

------------------------------------------------------------------------

End of File
