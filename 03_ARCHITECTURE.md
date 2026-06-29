# 03_ARCHITECTURE.md

# Montixify Software Architecture

Version: 1.0

------------------------------------------------------------------------

# Purpose

This document defines the architectural blueprint of Montixify. Every
design decision must comply with this document unless superseded by an
approved Architecture Decision Record (ADR).

------------------------------------------------------------------------

# Architectural Goals

-   Maintainability
-   Extensibility
-   Testability
-   Scalability
-   Performance
-   Separation of Concerns
-   AI-ready foundation
-   Plugin-first mindset

------------------------------------------------------------------------

# Architectural Style

Montixify adopts:

-   Clean Architecture
-   MVVM
-   Dependency Injection
-   SOLID Principles
-   Repository Pattern (where appropriate)
-   Strategy Pattern
-   Factory Pattern
-   Command Pattern
-   Observer Pattern

Avoid introducing patterns without a clear need.

------------------------------------------------------------------------

# Solution Layout

``` text
Montixify.sln

src/
    Montixify.Desktop
    Montixify.Core
    Montixify.Application
    Montixify.Infrastructure
    Montixify.Shared

tests/
    Montixify.Tests

docs/
```

------------------------------------------------------------------------

# Layer Responsibilities

## Desktop

Responsibilities:

-   WPF
-   XAML
-   Views
-   ViewModels
-   User interaction
-   Navigation

Must NOT contain business rules.

------------------------------------------------------------------------

## Core

Contains:

-   Entities
-   Value Objects
-   Domain Models
-   Contracts
-   Enums

Must have no dependency on UI frameworks.

------------------------------------------------------------------------

## Application

Contains:

-   Use Cases
-   Services
-   Commands
-   Validation
-   Interfaces

Coordinates business workflows.

------------------------------------------------------------------------

## Infrastructure

Contains:

-   FFmpeg integration
-   File system
-   Logging
-   Persistence
-   External libraries
-   Plugin loading

Implements interfaces defined in Core/Application.

------------------------------------------------------------------------

## Shared

Contains reusable utilities:

-   Constants
-   Extensions
-   Helpers
-   Shared models
-   Common exceptions

------------------------------------------------------------------------

# Dependency Rule

Dependencies always point inward.

``` text
Desktop
   |
Application
   |
Core

Infrastructure ---> Core
Infrastructure ---> Application
```

Core must never reference any outer layer.

------------------------------------------------------------------------

# MVVM

View ↓

ViewModel ↓

Application Service ↓

Core

No business logic inside Views.

No code-behind except UI wiring.

------------------------------------------------------------------------

# Dependency Injection

Use Microsoft.Extensions.DependencyInjection.

Rules:

-   Constructor Injection only
-   No Service Locator
-   Register services centrally
-   Prefer interfaces

------------------------------------------------------------------------

# Event Flow

User Action

↓

Command

↓

ViewModel

↓

Application Service

↓

Domain Logic

↓

Infrastructure

↓

UI Refresh

------------------------------------------------------------------------

# Plugin Architecture

Future plugin loading must be isolated.

Required extension points:

-   Effects
-   Exporters
-   Importers
-   Media Readers
-   Timeline Tools

Plugins must not directly modify application internals.

------------------------------------------------------------------------

# Future AI Layer

Reserved only.

Interfaces should exist for:

-   IEditingPlanProvider
-   IPromptParser
-   ISceneAnalyzer
-   IVoiceCommandProvider

Version 1 must not contain implementations.

------------------------------------------------------------------------

# Architectural Constraints

-   No circular dependencies.
-   No business logic in UI.
-   No direct Infrastructure access from Views.
-   No static global mutable state.
-   All dependencies injectable.
-   Every public API documented.

------------------------------------------------------------------------

# Validation Checklist

Before merging:

-   Builds successfully
-   No circular references
-   No architecture violations
-   Dependency rule respected
-   Naming conventions respected
-   Documentation updated

------------------------------------------------------------------------

# Architecture Decision Records

Major architectural changes require an ADR describing:

-   Context
-   Decision
-   Alternatives
-   Consequences

Store ADRs under:

docs/adr/

------------------------------------------------------------------------

# Definition of Done

Architecture work is complete when:

-   Layers compile
-   References are correct
-   Documentation updated
-   Tests pass
-   No dependency violations

------------------------------------------------------------------------

End of File
