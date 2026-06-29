# 40_API_CONTRACTS.md

# Montixify API Contracts

## Purpose

Define stable interfaces between application layers.

## Principles

-   Interface-first
-   Dependency inversion
-   Versionable
-   Backward compatible

## Core Contracts

-   IMediaService
-   ITimelineService
-   IPlaybackService
-   IRenderService
-   IExportService
-   IProjectService
-   ISettingsService
-   ILoggerService
-   IPluginManager

## Rules

-   Never expose infrastructure types.
-   Return domain models or DTOs.
-   Support async APIs.
-   Accept CancellationToken for long operations.

## Versioning

Breaking changes require a major version bump.

## Definition of Done

-   Interfaces documented
-   XML comments added
-   Unit tests updated
-   Consumers compile successfully
