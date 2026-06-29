# 26_GIT_WORKFLOW.md

# Montixify Git Workflow Specification

Version: 1.0

## Purpose

This document defines the Git workflow, branching strategy, commit
conventions, release process and repository governance for Montixify.

A predictable workflow ensures high-quality collaboration and traceable
history.

------------------------------------------------------------------------

# Goals

-   Clean history
-   Small reviewable changes
-   Reliable releases
-   Fast rollback
-   Automated validation
-   Consistent collaboration

------------------------------------------------------------------------

# Branch Strategy

Protected branches:

-   main
-   develop

Working branches:

-   feature/\*
-   bugfix/\*
-   hotfix/\*
-   release/\*
-   docs/\*
-   refactor/\*
-   chore/\*

Never commit directly to **main**.

------------------------------------------------------------------------

# Naming Convention

Examples:

feature/timeline-ripple-edit

bugfix/export-progress

hotfix/project-load-crash

docs/architecture-update

------------------------------------------------------------------------

# Commit Convention

Use Conventional Commits.

Examples:

feat: add timeline markers

fix: resolve playback desync

docs: update rendering guide

refactor: simplify export pipeline

test: add media engine tests

build: update dependencies

------------------------------------------------------------------------

# Pull Requests

Every PR should:

-   Target develop (unless hotfix)
-   Reference related issue
-   Describe changes
-   Include testing notes
-   Pass CI checks

Large PRs should be avoided.

------------------------------------------------------------------------

# Code Review

Reviewers should verify:

-   Architecture compliance
-   Coding standards
-   Tests
-   Documentation
-   Performance impact
-   Security impact

Approval required before merge.

------------------------------------------------------------------------

# Merge Strategy

Preferred:

-   Squash Merge for features
-   Merge Commit for releases

Never rewrite shared history.

------------------------------------------------------------------------

# Releases

Release workflow:

develop ↓ release/x.y.z ↓ QA ↓ main ↓ Tag ↓ Merge back to develop

------------------------------------------------------------------------

# Versioning

Use Semantic Versioning.

Major.Minor.Patch

Examples:

1.0.0

1.1.0

1.1.1

------------------------------------------------------------------------

# Tags

Every production release should receive a Git tag.

Example:

v1.0.0

Tags must correspond to released artifacts.

------------------------------------------------------------------------

# Hotfix Workflow

main ↓ hotfix/\* ↓ Review ↓ main ↓ develop

Hotfixes must be merged back into develop.

------------------------------------------------------------------------

# CI Requirements

Every push should:

-   Restore packages
-   Build solution
-   Run automated tests
-   Check formatting
-   Report failures

No failing build may be merged.

------------------------------------------------------------------------

# Repository Protection

Protect:

-   main
-   develop

Require:

-   PR review
-   Passing CI
-   Resolved conversations

------------------------------------------------------------------------

# Release Checklist

-   Build succeeds
-   Tests pass
-   Documentation updated
-   Version bumped
-   Changelog updated
-   Tag created

------------------------------------------------------------------------

# Rollback Strategy

If a release fails:

-   Revert offending commit(s)
-   Publish patch release
-   Document root cause
-   Add regression tests

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   Force pushes to shared branches
-   Large unrelated commits
-   Direct commits to main
-   Skipping code review
-   Ignoring CI failures

------------------------------------------------------------------------

# Definition of Done

Git workflow is complete only if:

-   Branch strategy followed
-   Commits follow convention
-   PR reviewed
-   CI passes
-   Release documented

------------------------------------------------------------------------

End of File
