# 33_CONTRIBUTING_GUIDE.md

# Montixify Contributing Guide

Version: 1.0

## Purpose

This guide defines how contributors should participate in the Montixify
project. It establishes a consistent workflow, coding expectations,
review process and community standards.

------------------------------------------------------------------------

# Goals

-   Welcome contributors
-   Maintain code quality
-   Preserve architecture
-   Ensure predictable reviews
-   Encourage constructive collaboration

------------------------------------------------------------------------

# Before You Start

Contributors should:

-   Read the README
-   Read the Architecture documents
-   Read Coding Standards
-   Read AI Development Rules
-   Build the solution successfully

------------------------------------------------------------------------

# Development Workflow

``` text
Fork Repository
      ↓
Create Branch
      ↓
Implement Changes
      ↓
Run Build
      ↓
Run Tests
      ↓
Update Documentation
      ↓
Open Pull Request
      ↓
Review
      ↓
Merge
```

------------------------------------------------------------------------

# Branch Naming

Examples:

-   feature/media-cache
-   bugfix/playback-sync
-   docs/readme-update
-   refactor/render-engine

------------------------------------------------------------------------

# Commit Messages

Follow Conventional Commits.

Examples:

-   feat: add timeline markers
-   fix: correct export progress
-   docs: update plugin guide
-   refactor: simplify cache manager

------------------------------------------------------------------------

# Coding Expectations

Every contribution must:

-   Respect Clean Architecture
-   Follow MVVM
-   Follow SOLID
-   Pass all tests
-   Avoid breaking public APIs
-   Include documentation updates when needed

------------------------------------------------------------------------

# Pull Requests

Each PR should include:

-   Summary
-   Motivation
-   Screenshots (if UI changes)
-   Testing performed
-   Related issue
-   Breaking changes (if any)

Keep PRs focused and reasonably small.

------------------------------------------------------------------------

# Code Review

Reviewers verify:

-   Correctness
-   Architecture
-   Readability
-   Performance
-   Security
-   Documentation
-   Test coverage

Review feedback should remain respectful and actionable.

------------------------------------------------------------------------

# Reporting Issues

Issue reports should contain:

-   Expected behavior
-   Actual behavior
-   Steps to reproduce
-   Environment
-   Logs (when available)

------------------------------------------------------------------------

# Feature Requests

Include:

-   Problem statement
-   Proposed solution
-   Alternatives considered
-   Expected user benefit

------------------------------------------------------------------------

# Documentation

Documentation must be updated whenever:

-   Public APIs change
-   Architecture changes
-   User workflows change
-   New modules are introduced

------------------------------------------------------------------------

# Community Standards

Contributors should:

-   Be respectful
-   Be constructive
-   Ask questions
-   Share context
-   Prefer evidence over assumptions

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   Large unrelated PRs
-   Direct commits to main
-   Ignoring review comments
-   Introducing undocumented behavior
-   Skipping tests

------------------------------------------------------------------------

# Contributor Checklist

Before opening a PR:

-   Build succeeds
-   Tests pass
-   Documentation updated
-   Formatting verified
-   No unnecessary files
-   Commit history reviewed

------------------------------------------------------------------------

# Definition of Done

A contribution is complete only if:

-   Code reviewed
-   CI passes
-   Documentation updated
-   Architecture preserved
-   Pull request approved and merged

------------------------------------------------------------------------

End of File
