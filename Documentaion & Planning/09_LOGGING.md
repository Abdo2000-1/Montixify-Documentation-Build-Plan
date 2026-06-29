# 09_LOGGING.md

# Montixify Logging & Diagnostics Guide

Version: 1.0

## Purpose

This document defines the official logging strategy for Montixify.

Logging exists to help developers diagnose issues, understand
application behavior, measure performance, troubleshoot production
issues, and improve software quality.

Logging is **not** a replacement for validation or exception handling.

------------------------------------------------------------------------

# Objectives

-   Trace application execution
-   Diagnose failures
-   Record unexpected behavior
-   Assist debugging
-   Support performance analysis
-   Improve maintainability
-   Provide operational insight

------------------------------------------------------------------------

# Technology Stack

Framework:

-   Microsoft.Extensions.Logging

Primary Provider:

-   Serilog

Recommended Sinks:

-   File
-   Debug
-   Console (Development)
-   Seq (Optional)
-   OpenTelemetry (Future)

------------------------------------------------------------------------

# Logging Levels

## Trace

Very detailed diagnostic information.

Use only during development.

------------------------------------------------------------------------

## Debug

Developer-focused diagnostics.

Examples:

-   Dependency resolution
-   Navigation flow
-   Configuration loading

------------------------------------------------------------------------

## Information

Normal application lifecycle.

Examples:

-   Application started
-   Project opened
-   Export completed
-   Theme changed

------------------------------------------------------------------------

## Warning

Unexpected but recoverable situations.

Examples:

-   Missing thumbnail
-   Unsupported codec fallback
-   Slow operation

------------------------------------------------------------------------

## Error

Recoverable failures.

Examples:

-   Failed import
-   Export failure
-   Invalid project

Always include exception details.

------------------------------------------------------------------------

## Critical

Application cannot continue safely.

Examples:

-   Startup failure
-   Corrupted configuration
-   Unhandled fatal exception

------------------------------------------------------------------------

# What To Log

Application

-   Startup
-   Shutdown
-   Version
-   Environment

Project

-   New project
-   Open
-   Save
-   Auto-save
-   Recovery

Media

-   Import
-   Remove
-   Thumbnail generation

Timeline

-   Track creation
-   Clip operations
-   Marker changes

Playback

-   Play
-   Pause
-   Stop
-   Seek

Export

-   Started
-   Progress
-   Completed
-   Failed
-   Cancelled

Plugins

-   Discovery
-   Load
-   Unload
-   Errors

------------------------------------------------------------------------

# What NOT To Log

Never log:

-   Passwords
-   API keys
-   Tokens
-   Personal user data
-   Large binary payloads

Avoid excessive logging inside render loops.

------------------------------------------------------------------------

# Structured Logging

Prefer structured properties.

Good:

``` csharp
_logger.LogInformation(
    "Opened project {ProjectName}",
    project.Name);
```

Bad:

``` csharp
_logger.LogInformation(
    "Opened " + project.Name);
```

------------------------------------------------------------------------

# Exception Logging

Always preserve stack traces.

Good:

``` csharp
_logger.LogError(
    ex,
    "Failed to export project {ProjectId}",
    project.Id);
```

Never swallow exceptions silently.

------------------------------------------------------------------------

# Log File Organization

``` text
Logs/

application.log
application-YYYYMMDD.log
errors.log
```

Enable rolling log files.

------------------------------------------------------------------------

# Correlation

Long-running workflows should generate an OperationId.

Example:

Import

↓

Timeline Processing

↓

Rendering

↓

Export

All log entries should reference the same operation identifier.

------------------------------------------------------------------------

# Performance Logging

Measure:

-   Startup time
-   Import duration
-   Render duration
-   Export duration
-   Thumbnail generation

Use Stopwatch where appropriate.

------------------------------------------------------------------------

# Configuration

Logging configuration should be externalized.

Support:

-   Log level
-   File location
-   Retention period
-   Output template

------------------------------------------------------------------------

# Retention

Recommended:

-   Keep 30 days
-   Compress old logs
-   Delete expired logs automatically

------------------------------------------------------------------------

# Validation Checklist

Before release:

-   Structured logging used
-   Sensitive data excluded
-   Exceptions logged
-   Rolling files enabled
-   Performance events measured

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   Console.WriteLine
-   String concatenation
-   Empty catch blocks
-   Logging secrets
-   Duplicate log messages
-   Logging every frame

------------------------------------------------------------------------

# Definition of Done

Logging implementation is complete only if:

-   Uses ILogger
-   Uses Serilog
-   Structured logging implemented
-   Exceptions recorded
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

End of File
