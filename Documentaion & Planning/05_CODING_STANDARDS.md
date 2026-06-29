# 05_CODING_STANDARDS.md

# Montixify Coding Standards

Version: 1.0

## Purpose

This document defines the mandatory coding standards for every
contributor and AI coding agent.

The primary goals are:

-   Readability
-   Maintainability
-   Consistency
-   Testability
-   Performance

------------------------------------------------------------------------

# Core Principles

1.  Readability is more important than cleverness.
2.  Favor simplicity.
3.  Write code for humans first.
4.  Eliminate duplication.
5.  Refactor continuously.

------------------------------------------------------------------------

# SOLID

Every implementation must respect:

-   Single Responsibility Principle
-   Open / Closed Principle
-   Liskov Substitution Principle
-   Interface Segregation Principle
-   Dependency Inversion Principle

Violations require architectural justification.

------------------------------------------------------------------------

# Naming

Classes: PascalCase

Interfaces: Prefix with I

Methods: PascalCase

Properties: PascalCase

Fields: \_privateField

Parameters: camelCase

Constants: PascalCase

Namespaces: Mirror folder hierarchy.

------------------------------------------------------------------------

# Class Rules

-   One public class per file.
-   Keep classes focused.
-   Avoid God Objects.
-   Prefer composition over inheritance.
-   Prefer immutable models where practical.

------------------------------------------------------------------------

# Method Rules

Methods should:

-   Perform one responsibility.
-   Be small and descriptive.
-   Validate arguments.
-   Return meaningful results.
-   Avoid hidden side effects.

Prefer early returns over deep nesting.

------------------------------------------------------------------------

# Async Rules

Use async/await for I/O.

Never block with:

-   Task.Wait()
-   Task.Result

Always propagate CancellationToken where appropriate.

------------------------------------------------------------------------

# Exceptions

Throw exceptions only for exceptional situations.

Do not swallow exceptions.

Log unexpected exceptions.

Expose user-friendly messages in the UI.

------------------------------------------------------------------------

# Dependency Injection

Use constructor injection exclusively.

Avoid Service Locator.

Avoid static mutable services.

Program against interfaces.

------------------------------------------------------------------------

# Logging

Use structured logging.

Never log secrets.

Log:

-   Startup
-   Shutdown
-   Import
-   Export
-   Playback
-   Rendering
-   Unexpected failures

------------------------------------------------------------------------

# Comments

Comments explain WHY.

Code explains HOW.

Remove obsolete comments immediately.

------------------------------------------------------------------------

# XML Documentation

Every public:

-   Class
-   Interface
-   Method
-   Property

must include XML documentation.

------------------------------------------------------------------------

# Nullability

Nullable reference types remain enabled.

Never silence warnings without justification.

Validate external inputs.

------------------------------------------------------------------------

# LINQ

Prefer readable LINQ.

Avoid overly complex chained expressions.

Materialize collections only when necessary.

------------------------------------------------------------------------

# Performance

Avoid:

-   Unnecessary allocations
-   Blocking UI thread
-   Premature optimization

Measure before optimizing.

------------------------------------------------------------------------

# Security

Validate imported media.

Validate file paths.

Never trust external input.

Use least privilege.

------------------------------------------------------------------------

# Code Review Checklist

Before merging:

-   Builds successfully
-   Tests pass
-   No warnings introduced
-   Naming conventions respected
-   XML docs updated
-   Logging added where appropriate
-   Architecture respected

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   God Classes
-   Long Methods
-   Circular Dependencies
-   Static Global State
-   Copy/Paste Programming
-   Magic Numbers
-   Magic Strings
-   Empty catch blocks

------------------------------------------------------------------------

# Good Example

``` csharp
public sealed class ProjectService : IProjectService
{
    public async Task<Project> OpenAsync(string path, CancellationToken token)
    {
        ArgumentException.ThrowIfNullOrWhiteSpace(path);

        return await _repository.OpenAsync(path, token);
    }
}
```

# Bad Example

``` csharp
public class Utils
{
    public static object DoEverything(object x)
    {
        // lots of unrelated logic...
        return x;
    }
}
```

------------------------------------------------------------------------

# Definition of Done

Code is complete only when it:

-   Compiles
-   Passes review
-   Is documented
-   Is tested
-   Respects this standard

------------------------------------------------------------------------

End of File
