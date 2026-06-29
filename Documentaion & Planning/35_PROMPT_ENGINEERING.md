# 35_PROMPT_ENGINEERING.md

# Montixify Prompt Engineering Guide

Version: 1.0

## Purpose

This document defines how AI coding agents should receive, interpret and
execute tasks while working on the Montixify codebase.

Its goal is to maximize correctness, consistency and architectural
integrity.

------------------------------------------------------------------------

# Objectives

-   Reduce ambiguity
-   Produce deterministic results
-   Preserve architecture
-   Encourage self-verification
-   Minimize hallucinations

------------------------------------------------------------------------

# AI Role

The AI acts as:

-   Software Architect
-   Senior .NET Engineer
-   Code Reviewer
-   QA Engineer
-   Technical Writer

The AI is responsible for quality, not just code generation.

------------------------------------------------------------------------

# Prompt Structure

Every implementation prompt should contain:

1.  Objective
2.  Context
3.  Constraints
4.  Inputs
5.  Expected Outputs
6.  Acceptance Criteria
7.  Files to Modify
8.  Files Not to Modify

------------------------------------------------------------------------

# Context Rules

Before writing code the AI should understand:

-   Current architecture
-   Related modules
-   Existing interfaces
-   Coding standards
-   Relevant ADRs
-   Project roadmap

Never ignore project documentation.

------------------------------------------------------------------------

# Execution Workflow

``` text
Understand
    ↓
Analyze
    ↓
Design
    ↓
Identify Impact
    ↓
Implement
    ↓
Build
    ↓
Test
    ↓
Refactor
    ↓
Document
    ↓
Review
```

------------------------------------------------------------------------

# Prompt Templates

## Feature Prompt

Include:

-   Feature description
-   Requirements
-   UI impact
-   Architecture impact
-   Test expectations
-   Documentation updates

------------------------------------------------------------------------

## Bug Fix Prompt

Include:

-   Reproduction steps
-   Expected behavior
-   Root cause analysis
-   Proposed fix
-   Regression test requirement

------------------------------------------------------------------------

## Refactoring Prompt

Include:

-   Motivation
-   Constraints
-   Public API impact
-   Performance considerations
-   Validation steps

------------------------------------------------------------------------

# Self-Verification

Before responding, the AI should verify:

-   Architecture preserved
-   Code compiles (when executable)
-   Naming consistent
-   Documentation updated
-   No duplicated logic
-   Error handling considered

------------------------------------------------------------------------

# Hallucination Prevention

Never invent:

-   APIs
-   Framework behavior
-   Build success
-   Test results
-   Package capabilities

When uncertain:

-   State assumptions
-   Request clarification if necessary
-   Prefer documented behavior

------------------------------------------------------------------------

# Quality Gates

Every completed task should satisfy:

-   Builds successfully
-   Tests pass
-   Documentation updated
-   Logging reviewed
-   Error handling reviewed
-   Security considered

------------------------------------------------------------------------

# Prompt Anti-Patterns

Avoid prompts that are:

-   Ambiguous
-   Overly broad
-   Missing constraints
-   Missing acceptance criteria
-   Missing architectural context

------------------------------------------------------------------------

# Example High-Quality Prompt

Goal: Implement timeline markers.

Constraints:

-   Preserve MVVM.
-   No business logic in Views.
-   Update documentation.
-   Add unit tests.
-   Do not modify unrelated modules.

Acceptance Criteria:

-   Build succeeds.
-   Tests pass.
-   Timeline markers visible.
-   Serialization supported.

------------------------------------------------------------------------

# Continuous Improvement

After each completed task:

-   Capture lessons learned
-   Update documentation if needed
-   Refine prompts for future work
-   Record architectural decisions when appropriate

------------------------------------------------------------------------

# Definition of Success

A prompt is successful only if it consistently enables an AI agent to
produce:

-   Correct code
-   Maintainable architecture
-   Passing builds
-   Passing tests
-   Complete documentation
-   Predictable implementation

------------------------------------------------------------------------

End of File
