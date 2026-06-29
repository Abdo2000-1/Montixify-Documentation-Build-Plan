# 38_EVENT_BUS_SPECIFICATION.md

# Montixify Event Bus Specification

## Purpose

Define a centralized Publish/Subscribe system that enables loose
coupling between modules.

## Architecture

Publisher → Event Bus → Subscribers

### Event Types

-   Domain Events
-   Application Events
-   UI Events
-   Integration Events

### Rules

-   Events are immutable.
-   Publish asynchronously by default.
-   UI updates are marshalled to the UI thread.
-   Subscribers must be independent.

### Core Interfaces

-   IEventBus
-   IEvent
-   IEventHandler`<T>`{=html}
-   IEventPublisher
-   IEventSubscriber

### Requirements

-   Thread-safe
-   No memory leaks
-   Weak subscriptions where appropriate
-   Logging support
-   Event replay (future)

### Definition of Done

-   Publish/Subscribe works
-   Thread-safe
-   Unit-tested
-   Documented
