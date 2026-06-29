# 36_RENDER_GRAPH_DESIGN.md

# Montixify Render Graph Design

Version: 1.0

## Purpose

This document defines the internal Render Graph architecture used by
Montixify.

The Render Graph is the execution model responsible for transforming
timeline content into rendered frames through a dependency-driven
pipeline.

Unlike a linear renderer, the Render Graph represents rendering as a
Directed Acyclic Graph (DAG), enabling caching, parallel execution and
future GPU acceleration.

------------------------------------------------------------------------

# Objectives

-   Deterministic rendering
-   Modular execution
-   Node isolation
-   Dependency tracking
-   Parallel scheduling
-   Efficient cache reuse
-   Future Vulkan / DirectX compatibility

------------------------------------------------------------------------

# Core Principles

-   Rendering is graph-based, not sequential.
-   Every operation is represented as a node.
-   Nodes never mutate upstream inputs.
-   Outputs are immutable for the duration of a frame.
-   The graph is rebuilt only when dependencies change.

------------------------------------------------------------------------

# High-Level Architecture

``` text
Timeline
    │
    ▼
Graph Builder
    │
    ▼
Render Graph
    │
 ┌──┴─────────────┐
 │Scheduler       │
 │Dependency Sort │
 │Cache Manager   │
 └──┬─────────────┘
    ▼
Execution Engine
    ▼
Rendered Frame
```

------------------------------------------------------------------------

# Node Types

## Source Nodes

Produce raw data.

Examples:

-   Video Source
-   Audio Source
-   Image Source
-   Color Generator

## Processing Nodes

Transform data.

Examples:

-   Blur
-   Color Correction
-   Crop
-   Resize
-   Transform

## Composite Nodes

Combine multiple inputs.

Examples:

-   Alpha Blend
-   Overlay
-   Mask
-   Merge

## Output Nodes

Produce final targets.

Examples:

-   Preview
-   Export
-   Thumbnail

------------------------------------------------------------------------

# Node Contract

Every node must expose:

-   NodeId
-   NodeType
-   Inputs
-   Outputs
-   Execute()
-   Validate()
-   CacheKey

Nodes must not know about UI components.

------------------------------------------------------------------------

# Dependency Resolution

Execution order is determined by dependency analysis.

``` text
Decode
   │
Color Correction
   │
Blur
   │
Composite
   │
Preview
```

Cycles are invalid and must fail validation.

------------------------------------------------------------------------

# Graph Builder

Responsibilities:

-   Analyze timeline
-   Create nodes
-   Connect dependencies
-   Remove redundant nodes
-   Validate graph

The builder should be deterministic.

------------------------------------------------------------------------

# Scheduler

The scheduler shall:

-   Perform topological sorting
-   Detect independent branches
-   Schedule parallel execution
-   Respect resource limits

------------------------------------------------------------------------

# Frame Context

Every frame execution owns an immutable FrameContext containing:

-   Frame Number
-   Timecode
-   Resolution
-   Color Space
-   Preview/Export Mode
-   CancellationToken

------------------------------------------------------------------------

# Cache Strategy

Cache reusable node outputs using:

-   Node Hash
-   Input Hash
-   Parameters
-   Frame Range

Invalidate only affected subgraphs.

------------------------------------------------------------------------

# Memory Model

-   Reuse frame buffers
-   Pool temporary textures
-   Avoid deep copies
-   Dispose resources promptly

------------------------------------------------------------------------

# Threading Model

Worker Threads:

-   Decode
-   Effects
-   Composition
-   Encoding

UI Thread:

-   Progress
-   Preview presentation

------------------------------------------------------------------------

# Error Handling

Recoverable:

-   Cache miss
-   Missing optional effect

Fatal:

-   Graph cycle
-   Invalid dependency
-   Corrupted node state

------------------------------------------------------------------------

# Future GPU Strategy

Abstract rendering backend through interfaces.

Potential backends:

-   CPU Renderer
-   Direct3D
-   Vulkan
-   WebGPU (future)

No rendering logic should depend directly on a specific backend.

------------------------------------------------------------------------

# AI Extension Points

Reserve interfaces:

-   IGraphOptimizer
-   INodeFusionStrategy
-   IExecutionPlanner

No implementations in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Graph is acyclic
-   Nodes validated
-   Dependencies resolved
-   Cache verified
-   Scheduler tested
-   Thread safety reviewed
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

Render Graph implementation is complete only if:

-   Graph builds successfully
-   Execution order is deterministic
-   Caching works correctly
-   Parallel scheduling functions
-   Preview and export share the same graph model
-   Tests pass
-   Documentation updated

------------------------------------------------------------------------

End of File
