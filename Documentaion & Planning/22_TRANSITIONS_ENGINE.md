# 22_TRANSITIONS_ENGINE.md

# Montixify Transitions Engine Specification

Version: 1.0

## Purpose

The Transitions Engine defines how two adjacent clips are blended over
time. Transitions are non-destructive, parameter-driven and integrated
into both preview and export pipelines.

------------------------------------------------------------------------

# Design Goals

-   Non-destructive
-   Frame-accurate
-   Extensible
-   Deterministic
-   GPU-ready
-   Plugin-friendly

------------------------------------------------------------------------

# Responsibilities

The engine shall:

-   Detect transition regions
-   Blend adjacent clips
-   Manage transition parameters
-   Preview transitions
-   Serialize transition data
-   Support future plugin transitions

------------------------------------------------------------------------

# Architecture

``` text
Timeline
   |
Transition Manager
   |
Transition Graph
   |
Transition Processor
   |
Rendered Frames
```

------------------------------------------------------------------------

# Lifecycle

Create

↓

Configure

↓

Validate

↓

Preview

↓

Render

↓

Serialize

↓

Dispose

------------------------------------------------------------------------

# Built-in Transition Types

-   Cut
-   Cross Fade
-   Dissolve
-   Fade Through Black
-   Slide
-   Wipe
-   Zoom (future)

------------------------------------------------------------------------

# Transition Model

Each transition contains:

-   TransitionId
-   SourceClipId
-   TargetClipId
-   Type
-   Duration
-   Parameters
-   Enabled

------------------------------------------------------------------------

# Timing Rules

Transitions require overlapping clip regions unless the transition type
explicitly supports gap-based rendering.

Duration must never exceed available overlap.

------------------------------------------------------------------------

# Rendering Pipeline

``` text
Frame A
   |
Blend Function
   |
Frame B
   |
Output Frame
```

Blend algorithms must be deterministic.

------------------------------------------------------------------------

# Parameters

Transitions expose:

-   Duration
-   Direction
-   Softness
-   Border (optional)
-   Easing

All parameters should be serializable.

------------------------------------------------------------------------

# Preview Integration

Preview rendering should:

-   Display transitions in real time when practical
-   Fall back to adaptive quality under heavy load

------------------------------------------------------------------------

# Export Integration

Export rendering must always use full-quality transition processing.

Preview optimizations must never affect final output.

------------------------------------------------------------------------

# Plugin Support

Public contracts:

-   ITransitionPlugin
-   ITransitionFactory
-   ITransitionRenderer

Plugins execute through documented APIs only.

------------------------------------------------------------------------

# Threading

Worker Threads:

-   Transition processing
-   Blend calculations

UI Thread:

-   Editing
-   Parameter updates
-   Progress display

------------------------------------------------------------------------

# Performance Targets

-   Low latency preview
-   Minimal allocations
-   Reusable frame buffers
-   Parallel-safe implementation

------------------------------------------------------------------------

# Error Handling

Recoverable:

-   Invalid parameter
-   Unsupported transition version

Fatal:

-   Transition graph corruption

Log all failures.

------------------------------------------------------------------------

# Future AI Extension Points

Reserve:

-   ITransitionRecommendationProvider
-   ISmartTransitionPlanner

No implementations in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Transition timing verified
-   Serialization tested
-   Preview tested
-   Export tested
-   Plugin compatibility reviewed
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

The Transitions Engine is complete only if:

-   Built-in transitions render correctly
-   Preview and export are consistent
-   Parameters serialize correctly
-   Performance targets are met
-   Documentation updated

------------------------------------------------------------------------

End of File
