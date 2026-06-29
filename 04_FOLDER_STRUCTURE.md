# 04_FOLDER_STRUCTURE.md

# Montixify Folder & Repository Structure Standard

Version: 1.0

## Purpose

This document defines the official repository layout, project layout,
folder hierarchy, namespace conventions, and organizational rules.

Any contributor or AI agent must follow this structure.

------------------------------------------------------------------------

# Repository Layout

``` text
Montixify/

├── .github/
├── assets/
├── docs/
├── src/
├── tests/
├── tools/
├── scripts/
├── build/
├── temp/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
└── Montixify.sln
```

------------------------------------------------------------------------

# src/

``` text
src/

Montixify.Desktop/
Montixify.Core/
Montixify.Application/
Montixify.Infrastructure/
Montixify.Shared/
```

Every production project lives inside **src**.

------------------------------------------------------------------------

# tests/

``` text
tests/

Montixify.Tests/
```

Only automated tests belong here.

------------------------------------------------------------------------

# docs/

Contains:

-   Architecture
-   ADRs
-   API docs
-   Specifications
-   Sprint documents

------------------------------------------------------------------------

# tools/

Contains helper utilities:

-   FFmpeg
-   Build tools
-   Packaging tools
-   Developer scripts

Never place source code here.

------------------------------------------------------------------------

# Desktop Project Layout

``` text
Montixify.Desktop/

Assets/
Controls/
Converters/
Extensions/
Helpers/
Resources/
Services/
Styles/
Themes/
ViewModels/
Views/
```

------------------------------------------------------------------------

# Assets

``` text
Assets/

Fonts/
Icons/
Images/
Animations/
```

Rules

-   SVG preferred where supported.
-   PNG for compatibility.
-   No duplicate assets.

------------------------------------------------------------------------

# Resources

``` text
Resources/

Brushes/
Colors/
Localization/
Strings/
Templates/
```

Only reusable resources.

------------------------------------------------------------------------

# Styles

``` text
Styles/

Buttons/
ComboBox/
DataGrid/
Dialogs/
Menu/
TextBox/
Window/
```

Each control family owns its own style file.

------------------------------------------------------------------------

# Themes

``` text
Themes/

Dark/
Light/
```

Every new control must support both themes.

------------------------------------------------------------------------

# Views

``` text
Views/

Home/
Timeline/
Preview/
MediaLibrary/
Inspector/
Settings/
Dialogs/
```

Views contain XAML only.

Business logic is prohibited.

------------------------------------------------------------------------

# ViewModels

``` text
ViewModels/

Base/
Home/
Timeline/
Preview/
MediaLibrary/
Inspector/
Settings/
Dialogs/
```

One ViewModel per View whenever practical.

------------------------------------------------------------------------

# Core Layout

``` text
Entities/
Enums/
Events/
Exceptions/
Interfaces/
Models/
ValueObjects/
```

Core must remain framework-independent.

------------------------------------------------------------------------

# Application Layout

``` text
Commands/
DTOs/
Interfaces/
Services/
UseCases/
Validation/
```

Coordinates application workflows.

------------------------------------------------------------------------

# Infrastructure Layout

``` text
Caching/
Configuration/
Export/
FFmpeg/
FileSystem/
Import/
Logging/
Persistence/
Plugins/
Playback/
Rendering/
```

Implements technical concerns.

------------------------------------------------------------------------

# Shared Layout

``` text
Constants/
Extensions/
Helpers/
Utilities/
```

Shared code must remain generic.

------------------------------------------------------------------------

# Generated Data

Runtime folders:

``` text
Logs/
Cache/
Temp/
Exports/
Autosave/
Projects/
```

Must be created automatically if missing.

------------------------------------------------------------------------

# Namespace Convention

Project:

Montixify.Application

Folder:

Services

Namespace:

Montixify.Application.Services

Mirror folder hierarchy whenever possible.

------------------------------------------------------------------------

# Naming Convention

Classes

PascalCase

Interfaces

Prefix with I

Enums

PascalCase

Methods

PascalCase

Private fields

\_camelCase

Constants

PascalCase

Avoid abbreviations.

------------------------------------------------------------------------

# File Organization Rules

One public class per file.

Filename must equal class name.

Avoid partial classes unless required.

------------------------------------------------------------------------

# Forbidden Practices

Do NOT:

-   Mix UI and business logic.
-   Create God classes.
-   Use random utility folders.
-   Store binaries in src.
-   Duplicate assets.
-   Create circular namespaces.

------------------------------------------------------------------------

# Folder Validation Checklist

Before merging:

-   Correct folder
-   Correct namespace
-   Correct filename
-   No duplicates
-   Documentation updated

------------------------------------------------------------------------

# Future Expansion

Reserved folders:

``` text
AI/
Marketplace/
Cloud/
Telemetry/
Extensions/
```

These folders remain empty until their roadmap phase.

------------------------------------------------------------------------

# Definition of Done

A structural change is complete only if:

-   Folder exists
-   Namespace matches
-   Documentation updated
-   Build succeeds
-   No broken references

------------------------------------------------------------------------

End of File
