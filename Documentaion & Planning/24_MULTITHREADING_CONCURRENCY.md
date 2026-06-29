# 24_MULTITHREADING_CONCURRENCY.md

# Montixify Multithreading & Concurrency Specification

Version: 1.0

## Purpose

This document defines the threading model and concurrency rules used
throughout Montixify. All long-running operations must execute safely
without blocking the UI.

------------------------------------------------------------------------

# Objectives

-   Responsive UI
-   Safe concurrency
-   Predictable scheduling
-   Efficient resource usage
-   Deadlock prevention
-   Scalable background processing

------------------------------------------------------------------------

# Threading Model

``` text
UI Thread
 |
 +-- User Input
 +-- Rendering Updates
 +-- Data Binding

Background Workers
 |
 +-- Media Import
 +-- Metadata Extraction
 +-- Thumbnail Generation
 +-- Playback Decode
 +-- Rendering
 +-- Export
```

Heavy work must never execute on the UI thread.

------------------------------------------------------------------------

# UI Thread Rules

Allowed:

-   Update controls
-   Raise UI notifications
-   Dispatch ViewModel updates

Forbidden:

-   FFmpeg execution
-   File I/O
-   Rendering
-   Thumbnail generation
-   Long loops

------------------------------------------------------------------------

# Async Strategy

Use:

-   async / await
-   Task
-   ValueTask (where appropriate)
-   IAsyncEnumerable for streaming data

Never use:

-   Task.Wait()
-   Task.Result
-   Thread.Sleep() on the UI thread

------------------------------------------------------------------------

# Task Scheduling

Background tasks should be coordinated through dedicated services.

Prefer producer/consumer pipelines for high-throughput operations.

------------------------------------------------------------------------

# Cancellation

Every long-running operation must accept a CancellationToken.

Supported operations:

-   Import
-   Export
-   Playback preparation
-   Thumbnail generation
-   Cache cleanup

Cancellation must be cooperative.

------------------------------------------------------------------------

# Synchronization

Use synchronization only when required.

Preferred tools:

-   SemaphoreSlim
-   Channel`<T>`{=html}
-   ConcurrentDictionary
-   ConcurrentQueue

Minimize lock duration.

------------------------------------------------------------------------

# Deadlock Prevention

Guidelines:

-   Avoid nested locks
-   Keep critical sections short
-   Never block async code
-   Avoid synchronous waits

------------------------------------------------------------------------

# Race Condition Prevention

Protect shared mutable state.

Prefer immutable data transfer objects between threads.

------------------------------------------------------------------------

# Progress Reporting

Background operations should report:

-   Percentage
-   Current stage
-   ETA (when available)

Throttle updates before sending them to the UI.

------------------------------------------------------------------------

# Thread Safety

Services must clearly document whether they are:

-   Thread-safe
-   Thread-affine
-   Single-thread only

------------------------------------------------------------------------

# Performance Guidelines

-   Avoid creating excessive tasks
-   Reuse workers where practical
-   Batch operations
-   Avoid context switching when unnecessary

------------------------------------------------------------------------

# Testing

Concurrency tests should verify:

-   Cancellation
-   Thread safety
-   No deadlocks
-   No race conditions
-   Correct progress reporting

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   Fire-and-forget tasks without supervision
-   Global locks
-   Shared mutable static state
-   Blocking the Dispatcher thread
-   Busy waiting

------------------------------------------------------------------------

# Validation Checklist

-   UI never blocks
-   Cancellation verified
-   Shared state protected
-   Async APIs used correctly
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

Concurrency implementation is complete only if:

-   UI remains responsive
-   Long-running work is asynchronous
-   No deadlocks detected
-   Thread safety documented
-   Tests pass
-   Documentation updated

------------------------------------------------------------------------

End of File
