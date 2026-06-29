# 39_DOMAIN_MODEL.md

# Montixify Domain Model

## Purpose

Describe the business entities independent of UI and Infrastructure.

## Main Aggregates

-   Project
-   Timeline
-   Track
-   Clip
-   MediaAsset
-   Marker
-   Effect
-   Transition
-   ExportProfile

## Principles

-   Rich domain model
-   No infrastructure dependencies
-   Immutable value objects where possible
-   Domain events for state changes

## Relationships

Project ├── Timeline ├── Media Library └── Export Profiles

Timeline ├── Tracks └── Markers

Track └── Clips

Clip ├── Effects └── Transitions

## Definition of Done

-   Entities defined
-   Value objects defined
-   Aggregate boundaries documented
-   Business rules documented
