# 08_DEPENDENCY_INJECTION.md

# Montixify Dependency Injection Guide

Version: 1.0

## Purpose

This document defines the Dependency Injection (DI) strategy for
Montixify.

DI is mandatory throughout the solution. All services, managers,
repositories, providers and infrastructure components must be resolved
through the configured IoC container unless there is a documented
architectural exception.

------------------------------------------------------------------------

# Objectives

-   Loose coupling
-   Testability
-   Maintainability
-   Replaceable implementations
-   Centralized composition
-   Predictable object lifetime

------------------------------------------------------------------------

# Technology

Container:

-   Microsoft.Extensions.DependencyInjection

Application Host:

-   Microsoft.Extensions.Hosting

Configuration:

-   Microsoft.Extensions.Configuration

Logging:

-   Microsoft.Extensions.Logging
-   Serilog

------------------------------------------------------------------------

# Composition Root

The application shall have ONE composition root.

For Montixify this is:

Montixify.Desktop

No other project should build its own ServiceProvider.

------------------------------------------------------------------------

# Registration Policy

All registrations must occur during startup.

Example categories:

-   ViewModels
-   Application Services
-   Infrastructure Services
-   Configuration
-   Logging
-   Navigation
-   Dialog Services

Never register services from random classes.

------------------------------------------------------------------------

# Constructor Injection

Preferred:

``` csharp
public sealed class ProjectService : IProjectService
{
    public ProjectService(
        ILoggerService logger,
        IProjectRepository repository)
    {
    }
}
```

Never instantiate dependencies manually with `new`.

------------------------------------------------------------------------

# Service Lifetimes

## Singleton

Use for:

-   Configuration
-   ThemeService
-   NavigationService
-   Logging
-   Cache

Must be thread-safe.

------------------------------------------------------------------------

## Transient

Use for:

-   Lightweight services
-   Commands
-   Temporary helpers

------------------------------------------------------------------------

## Scoped

Desktop applications normally have no request scope.

Avoid Scoped unless a custom scope is intentionally created.

------------------------------------------------------------------------

# ViewModel Registration

Register ViewModels through DI.

Avoid creating ViewModels directly inside Views.

Example:

MainWindow receives MainViewModel from the container.

------------------------------------------------------------------------

# View Creation

Views may be resolved from DI if they require injected services.

Avoid Service Locator patterns inside XAML code-behind.

------------------------------------------------------------------------

# Configuration

Strongly typed options should be preferred.

Bind configuration once during startup.

Avoid reading configuration files throughout the application.

------------------------------------------------------------------------

# Factory Pattern

Use factories when runtime decisions are required.

Examples:

-   ExporterFactory
-   ImporterFactory
-   EffectFactory
-   RendererFactory

Factories themselves should be injected.

------------------------------------------------------------------------

# Lazy Dependencies

Use Lazy`<T>`{=html} only when:

-   Initialization is expensive.
-   Dependency may never be used.

Do not use Lazy as a workaround for poor architecture.

------------------------------------------------------------------------

# Circular Dependencies

Circular dependencies are prohibited.

If encountered:

1.  Reevaluate responsibilities.
2.  Extract an interface.
3.  Introduce an application service.
4.  Refactor.

Never suppress the problem.

------------------------------------------------------------------------

# Service Locator

Forbidden.

Bad:

``` csharp
var service = ServiceLocator.Get<IProjectService>();
```

Good:

``` csharp
public MainViewModel(IProjectService projectService)
{
}
```

------------------------------------------------------------------------

# Startup Pipeline

Application Startup

↓

Load Configuration

↓

Configure Logging

↓

Register Services

↓

Build Host

↓

Resolve MainWindow

↓

Resolve MainViewModel

↓

Run Application

------------------------------------------------------------------------

# Testing

Unit tests should inject mocks or fakes.

Never require the real container unless performing integration tests.

------------------------------------------------------------------------

# Validation Checklist

Before merging:

-   Constructor injection used
-   No Service Locator
-   Correct lifetime
-   No circular dependency
-   Interfaces preferred
-   Build passes
-   Tests pass

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   Static service instances
-   Global containers
-   Hidden dependencies
-   Manual object graphs
-   Multiple ServiceProviders
-   Runtime registration after startup

------------------------------------------------------------------------

# Definition of Done

A DI implementation is complete only if:

-   Registered correctly
-   Lifetime documented
-   Constructor injection used
-   Tested
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

End of File
