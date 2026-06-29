# 14_PLAYBACK_ENGINE.md

# Montixify Playback Engine Specification

Version: 1.0

## Purpose

The Playback Engine is responsible for real-time preview of timeline
content. It synchronizes video, audio and timeline state while
maintaining responsive UI performance.

------------------------------------------------------------------------

# Objectives

-   Smooth playback
-   Accurate synchronization
-   Low latency
-   Frame-accurate seeking
-   Extensible playback pipeline

------------------------------------------------------------------------

# Responsibilities

The Playback Engine shall:

-   Play timeline
-   Pause
-   Stop
-   Seek
-   Frame-step
-   Loop playback
-   Synchronize audio/video
-   Notify UI of playback state

------------------------------------------------------------------------

# Architecture

``` text
Timeline
    |
Playback Controller
    |
Playback Engine
 |------ Frame Scheduler
 |------ Audio Clock
 |------ Video Renderer
 |------ Sync Manager
 |------ Buffer Manager
```

------------------------------------------------------------------------

# Playback States

``` text
Idle
 ↓
Loading
 ↓
Ready
 ↓
Playing
 ↔
Paused
 ↓
Stopped
```

Errors transition to:

Faulted

Recovery returns to Ready when possible.

------------------------------------------------------------------------

# Playback Pipeline

``` text
Play Request
      ↓
Validate Timeline
      ↓
Resolve Clips
      ↓
Decode Frames
      ↓
Audio Sync
      ↓
Render Preview
      ↓
Update Playhead
```

------------------------------------------------------------------------

# Frame Scheduler

Responsibilities:

-   Schedule frames
-   Maintain FPS
-   Handle dropped frames
-   Notify renderer

Frame scheduling must prioritize smooth playback over perfect frame
delivery.

------------------------------------------------------------------------

# Audio Synchronization

Audio acts as the primary playback clock.

Video rendering should synchronize to audio whenever practical.

Prevent cumulative drift.

------------------------------------------------------------------------

# Seeking

Support:

-   Absolute seek
-   Relative seek
-   Frame stepping
-   Marker seek
-   Clip boundary seek

Seeking should complete with minimal latency.

------------------------------------------------------------------------

# Loop Playback

Support:

-   Entire timeline
-   In/Out range
-   Selected clip (future)

------------------------------------------------------------------------

# Buffering

Implement buffering for:

-   Video frames
-   Audio samples

Avoid excessive memory consumption.

------------------------------------------------------------------------

# Events

Expose:

-   PlaybackStarted
-   PlaybackPaused
-   PlaybackStopped
-   PositionChanged
-   PlaybackCompleted
-   PlaybackFaulted

------------------------------------------------------------------------

# Performance Targets

-   Responsive controls
-   Stable preview FPS
-   No UI thread blocking
-   Async decoding
-   Efficient buffering

------------------------------------------------------------------------

# Threading Model

UI Thread

-   Input
-   Display updates

Background Threads

-   Decode
-   Buffer
-   Synchronization
-   Media loading

Heavy work must never execute on the UI thread.

------------------------------------------------------------------------

# Error Handling

Recoverable:

-   Temporary decode failure
-   Missing preview frame

Fatal:

-   Decoder initialization failure
-   Unsupported playback backend

------------------------------------------------------------------------

# Future AI Extension Points

Reserve:

-   IPlaybackAdvisor
-   IPlaybackOptimizer
-   ISmartPreviewProvider

No implementations in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Frame stepping tested
-   Seeking tested
-   Audio sync verified
-   Playback state machine validated
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

Playback Engine is complete when:

-   Timeline plays correctly
-   Seeking is accurate
-   Audio/video remain synchronized
-   UI stays responsive
-   State transitions are correct
-   Documentation updated

------------------------------------------------------------------------

End of File
