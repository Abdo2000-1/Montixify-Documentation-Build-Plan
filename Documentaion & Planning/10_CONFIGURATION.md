# 10_CONFIGURATION.md

# Montixify Configuration Guide

Version: 1.0

## Purpose

This document defines how configuration is stored, loaded, validated and
consumed throughout Montixify.

Configuration must be centralized, strongly typed and environment-aware.

------------------------------------------------------------------------

# Goals

-   Centralized configuration
-   Strong typing
-   Validation
-   Environment awareness
-   Easy deployment
-   Safe defaults

------------------------------------------------------------------------

# Configuration Sources (Highest → Lowest Priority)

1.  Command-line arguments
2.  Environment variables
3.  User configuration file
4.  appsettings.{Environment}.json
5.  appsettings.json
6.  Built-in defaults

------------------------------------------------------------------------

# Configuration Files

``` text
appsettings.json
appsettings.Development.json
appsettings.Production.json
```

Never hardcode configurable values.

------------------------------------------------------------------------

# Options Pattern

Every configuration section should map to a strongly typed Options
class.

Examples:

-   ThemeOptions
-   ExportOptions
-   PlaybackOptions
-   LoggingOptions
-   FFmpegOptions
-   CacheOptions
-   PluginOptions

Bind once during startup.

------------------------------------------------------------------------

# Required Configuration Areas

## Application

-   Name
-   Version
-   Culture
-   Language

## UI

-   Theme
-   Accent color
-   Window state
-   Last layout

## Playback

-   Default quality
-   Hardware acceleration
-   Preview resolution

## Export

-   Codec
-   Bitrate
-   Resolution
-   Output folder

## FFmpeg

-   Executable path
-   Probe path
-   Hardware encoder preferences

## Cache

-   Cache directory
-   Thumbnail cache size
-   Cleanup policy

## Plugins

-   Plugin directory
-   Auto-load
-   Signature validation (future)

------------------------------------------------------------------------

# Validation

All configuration must be validated during startup.

If validation fails:

-   Log the error
-   Notify the user
-   Fall back to safe defaults when possible

Application must never continue with invalid critical settings.

------------------------------------------------------------------------

# Runtime Reload

Configuration that may reload:

-   Theme
-   Logging level
-   Language
-   UI preferences

Configuration that requires restart:

-   FFmpeg path
-   Plugin discovery path

------------------------------------------------------------------------

# Storage Locations

User settings:

%AppData%/Montixify/

Temporary data:

%LocalAppData%/Montixify/Temp/

Logs:

%LocalAppData%/Montixify/Logs/

Cache:

%LocalAppData%/Montixify/Cache/

------------------------------------------------------------------------

# Security

Never store:

-   Passwords
-   Tokens
-   Secrets

Future sensitive settings should use secure OS storage.

------------------------------------------------------------------------

# Anti-Patterns

Avoid:

-   Magic strings
-   Global mutable configuration
-   Reading JSON files repeatedly
-   Hardcoded paths
-   Direct IConfiguration access throughout the application

------------------------------------------------------------------------

# Review Checklist

-   Strongly typed options
-   Validation implemented
-   Defaults documented
-   No hardcoded values
-   Configuration injected via DI

------------------------------------------------------------------------

# Definition of Done

Configuration work is complete only if:

-   Options classes exist
-   Validation passes
-   Configuration loads successfully
-   Build succeeds
-   Documentation updated

------------------------------------------------------------------------

End of File
