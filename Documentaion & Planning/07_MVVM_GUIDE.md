# 07_MVVM_GUIDE.md

# Montixify MVVM Development Guide

Version: 1.0

## Purpose

This document defines the official MVVM implementation guidelines for
Montixify. Every View, ViewModel and related component must comply with
these rules.

------------------------------------------------------------------------

# Why MVVM?

MVVM separates:

-   Presentation
-   UI behavior
-   Business logic

Benefits:

-   Testability
-   Maintainability
-   Reusability
-   Designer/Developer separation
-   Clean Architecture alignment

------------------------------------------------------------------------

# Layer Relationship

``` text
View
  |
Binding
  |
ViewModel
  |
Application Services
  |
Core
```

Views never call Infrastructure directly.

------------------------------------------------------------------------

# Responsibilities

## View

Responsible for:

-   XAML
-   Layout
-   Visual states
-   Animations
-   Bindings

Must NOT contain business logic.

Code-behind should only contain UI wiring that cannot be expressed in
XAML.

------------------------------------------------------------------------

## ViewModel

Responsible for:

-   State
-   Commands
-   Validation
-   Navigation requests
-   Calling Application services

Must NOT reference UI controls.

------------------------------------------------------------------------

## Model

Contains business/domain data.

Models should remain framework-independent whenever possible.

------------------------------------------------------------------------

# CommunityToolkit.Mvvm

Preferred base classes:

-   ObservableObject
-   ObservableRecipient

Preferred attributes:

-   ObservableProperty
-   RelayCommand
-   NotifyCanExecuteChangedFor

------------------------------------------------------------------------

# Commands

Use:

-   RelayCommand
-   AsyncRelayCommand

Never handle Button.Click directly unless technically unavoidable.

Commands should:

-   Have a single responsibility.
-   Be testable.
-   Respect cancellation.

------------------------------------------------------------------------

# Data Binding

Prefer:

-   OneWay
-   TwoWay only when editing
-   Explicit UpdateSourceTrigger where appropriate

Never manipulate UI elements from the ViewModel.

------------------------------------------------------------------------

# Dependency Injection

Inject services via constructor.

Example:

``` csharp
public MainViewModel(
    IProjectService projectService,
    ILoggerService logger)
{
}
```

Never instantiate services with `new` inside ViewModels.

------------------------------------------------------------------------

# Navigation

Navigation should be performed through an abstraction:

INavigationService

ViewModels request navigation.

Views do not decide application flow.

------------------------------------------------------------------------

# Dialogs

Use:

IDialogService

Avoid direct MessageBox usage inside ViewModels.

------------------------------------------------------------------------

# Validation

Support:

-   IDataErrorInfo
-   INotifyDataErrorInfo

Validation errors should be surfaced through bindings.

------------------------------------------------------------------------

# Messaging

For loosely coupled communication use:

WeakReferenceMessenger

Avoid direct ViewModel-to-ViewModel references.

------------------------------------------------------------------------

# Async Guidelines

Long-running operations:

-   async
-   await
-   CancellationToken

Never block the UI thread.

------------------------------------------------------------------------

# ViewModel Lifecycle

Initialization

↓

Load data

↓

User interaction

↓

Save state

↓

Dispose resources

------------------------------------------------------------------------

# Folder Organization

``` text
ViewModels/

Base/
Dialogs/
Home/
Inspector/
MediaLibrary/
Preview/
Settings/
Timeline/
```

One primary ViewModel per View.

------------------------------------------------------------------------

# Testing

Every ViewModel should be unit-testable.

Mock:

-   Services
-   Repositories
-   Navigation
-   Dialogs

Never require WPF to test business behavior.

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   Business logic in Views
-   Static ViewModels
-   Service Locator
-   UI control references
-   Massive ViewModels
-   Event-handler driven architecture

------------------------------------------------------------------------

# MVVM Checklist

Before merging:

-   No business logic in View
-   Commands used correctly
-   Constructor injection
-   Observable properties
-   Async where appropriate
-   Unit tests updated
-   Documentation updated

------------------------------------------------------------------------

# Definition of Done

An MVVM feature is complete only if:

-   View is declarative.
-   ViewModel is testable.
-   Services are injected.
-   Build succeeds.
-   Documentation updated.

------------------------------------------------------------------------

End of File
