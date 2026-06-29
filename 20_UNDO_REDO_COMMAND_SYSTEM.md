# 20_UNDO_REDO_COMMAND_SYSTEM.md

# Montixify Undo / Redo Command System Specification

Version: 1.0

## Purpose

This document defines the architecture of the Undo/Redo subsystem.

Every user action that mutates project state must be reversible.

------------------------------------------------------------------------

# Objectives

-   Unlimited undo (configurable)
-   Deterministic replay
-   Fast execution
-   Low memory usage
-   Transaction support

------------------------------------------------------------------------

# Architecture

``` text
UI
 |
Command
 |
Command Dispatcher
 |
Undo Manager
 |--------- Undo Stack
 |--------- Redo Stack
```

------------------------------------------------------------------------

# Command Contract

Every command must implement:

-   Execute()
-   Undo()
-   CanExecute()
-   Description
-   Timestamp

Commands must be idempotent where practical.

------------------------------------------------------------------------

# Supported Operations

-   Add Clip
-   Delete Clip
-   Move Clip
-   Split Clip
-   Trim Clip
-   Add Track
-   Delete Track
-   Add Marker
-   Remove Marker
-   Property Changes
-   Effect Changes
-   Transition Changes

------------------------------------------------------------------------

# Execution Flow

``` text
User Action
 ↓
Create Command
 ↓
Validate
 ↓
Execute
 ↓
Push Undo Stack
 ↓
Clear Redo Stack
 ↓
Notify UI
```

------------------------------------------------------------------------

# Undo Flow

``` text
Pop Undo Stack
 ↓
Undo Command
 ↓
Push Redo Stack
 ↓
Refresh Timeline
```

------------------------------------------------------------------------

# Redo Flow

``` text
Pop Redo Stack
 ↓
Execute Command
 ↓
Push Undo Stack
```

------------------------------------------------------------------------

# Composite Commands

Support transactions that combine multiple commands into one logical
action.

Examples:

-   Paste multiple clips
-   Ripple delete
-   Multi-track move

------------------------------------------------------------------------

# History Policy

-   Configurable history size
-   Oldest commands discarded first
-   History cleared only when opening another project

------------------------------------------------------------------------

# Serialization

Undo history is runtime state only.

Do NOT serialize command stacks into .mtxproj.

------------------------------------------------------------------------

# Performance

Commands should store only the minimal state required for reversal.

Avoid copying entire timelines.

------------------------------------------------------------------------

# Error Handling

If Undo fails:

-   Log error
-   Preserve project integrity
-   Prevent history corruption

------------------------------------------------------------------------

# Future AI Extension Points

Reserve:

-   ICommandOptimizer
-   IHistoryAnalyzer
-   IMacroRecorder

No implementations in Version 1.

------------------------------------------------------------------------

# Validation Checklist

-   Execute tested
-   Undo tested
-   Redo tested
-   Composite commands tested
-   History limits verified
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

The Undo/Redo system is complete when:

-   Every editing operation is reversible
-   History remains consistent
-   Redo behaves predictably
-   Memory usage is controlled
-   Documentation updated

------------------------------------------------------------------------

End of File
