# High-Level Architecture

Project: Movie App  
Version: 1.0  
Status: Accepted  
Author: Hardik Vegad  
Last Updated: September 17, 2026

---

## Purpose

This document describes the high-level technical architecture of the Movie App.

The architecture is based on the decisions already made in the previous documents:

- Offline-first approach
- MVVM
- Jetpack Compose
- Coroutines + Flow
- Room
- Retrofit + OkHttp
- Hilt
- Clean Architecture-inspired layering

The goal is to keep responsibilities clear without introducing unnecessary complexity.

---

## Architecture Overview

The application will be organized into four main layers:

    Presentation
        ↓
    Domain
        ↓
    Data
        ↓
    Infrastructure

Each layer has a specific responsibility.

---

## 1. Presentation Layer

The Presentation layer is responsible for displaying the UI and handling user interaction.

### Main responsibilities

- Display screens
- Handle user actions
- Observe UI state
- Show loading, success, empty and error states
- Trigger application actions through ViewModels
- Handle navigation

### Main technologies

- Jetpack Compose
- ViewModel
- StateFlow
- Navigation Compose

### Flow

    User
      ↓
    Compose UI
      ↓
    ViewModel
      ↓
    Domain

The UI should not directly access repositories, databases or APIs.

---

## 2. Domain Layer

The Domain layer contains application-level business logic and models.

### Main responsibilities

- Define application models
- Define business operations
- Coordinate application use cases
- Define repository contracts where appropriate

### Examples

    GetPopularMoviesUseCase
    SearchMoviesUseCase
    GetMovieDetailsUseCase
    GetWatchlistUseCase
    AddToWatchlistUseCase
    RemoveFromWatchlistUseCase

Use Cases will be introduced where they provide meaningful separation or business logic.

Simple operations do not need unnecessary abstraction.

### Flow

    ViewModel
        ↓
    Use Case
        ↓
    Repository Interface

The Domain layer should not depend on Retrofit, Room, Android UI or other infrastructure details.

---

## 3. Data Layer

The Data layer is responsible for retrieving, storing and transforming application data.

It coordinates between local and remote data sources.

### Main responsibilities

- Repository implementations
- Local data access
- Remote data access
- Mapping between models
- Combining local and remote data
- Persisting remote data locally

### Main components

    Repository
       ↙   ↘
    Local   Remote
    Data    Data
    Source  Source

The repository decides when data should come from the local database and when the remote API should be used.

---

## 4. Infrastructure Layer

The Infrastructure layer contains implementations of external technical dependencies.

### Local

- Room Database
- DAO
- Database entities

### Remote

- Retrofit
- OkHttp
- API services
- Network models

### Other

- Hilt dependency injection
- Network configuration
- Application-level technical configuration

Infrastructure details should remain isolated from the higher layers.

---

# Overall Data Flow

The normal application flow will look like:

    Compose UI
        ↓
    ViewModel
        ↓
    Use Case
        ↓
    Repository
       ↙   ↘
    Room   Retrofit
      ↓       ↓
    Local   Remote
      ↑       ↓
      └── Repository
            ↓
       Local Database
            ↓
          Flow
            ↓
        ViewModel
            ↓
        Compose UI

The important principle is that the UI observes application state rather than directly coordinating local and remote data sources.

---

# Offline-First Flow

For content that is stored locally:

    UI
     ↓
    ViewModel
     ↓
    Use Case
     ↓
    Repository
     ↓
    Room
     ↓
    Flow
     ↓
    ViewModel
     ↓
    UI

If fresh remote data is required:

    Repository
        ↓
    Remote API
        ↓
    Map API Model
        ↓
    Save to Room
        ↓
    Room Flow emits update
        ↓
    ViewModel
        ↓
    UI

This allows the UI to receive local data immediately and then automatically reflect updated data when the database changes.

---


# Model Separation

The application will use different models where separation provides value.

    Remote API Model
          ↓
        Mapper
          ↓
    Application Model
          ↓
        Mapper
          ↓
    Local Entity

This prevents external API structures from becoming tightly coupled to the rest of the application.

Not every model needs to be duplicated if there is no meaningful benefit.

---

# Dependency Direction

Dependencies should flow toward the inner application logic.

    Presentation
         ↓
      Domain
         ↓
       Data
         ↓
    Infrastructure

Higher-level layers should not depend directly on implementation details such as Retrofit or Room.

For example:

    ViewModel
       ↓
    Repository Interface
       ↑
    Repository Implementation
       ↓
    Room / Retrofit

This keeps the application logic easier to test and change.

---

# Dependency Injection

Hilt will be used to provide dependencies.

Typical dependency relationships:

    ViewModel
        ↓
    Use Case
        ↓
    Repository
        ↓
    Local / Remote Data Source
        ↓
    Room / Retrofit

Hilt will handle object creation and dependency wiring rather than having components manually construct their dependencies.

---

# Error and State Handling

The application should explicitly represent common UI states.

Typical states include:

- Loading
- Success
- Empty
- Error
- Offline with cached data

For example:

    Loading
       ↓
    Success

or:

    Loading
       ↓
    Error

When cached data is available and the network request fails, the application should continue displaying the cached data where appropriate instead of unnecessarily replacing useful content with an error screen.

Exact state models will be finalized during implementation.

---

# Architecture Boundaries

The following boundaries should remain clear:

### UI

Does:

- Display state
- Send user actions
- Handle UI/navigation concerns

Does not:

- Call Retrofit directly
- Query Room directly
- Contain repository implementation logic

### ViewModel

Does:

- Manage presentation state
- Handle user actions
- Call application/domain operations

Does not:

- Know Retrofit implementation details
- Know Room implementation details

### Domain

Does:

- Contain application logic
- Define application models
- Define contracts where appropriate

Does not:

- Depend on Compose
- Depend on Retrofit
- Depend on Room

### Data

Does:

- Coordinate data sources
- Map models
- Persist and retrieve data

Does not:

- Contain UI logic

---

# Technology Stack

The high-level architecture will use:

| Area | Technology |
|---|---|
| Language | Kotlin |
| UI | Jetpack Compose |
| Architecture | MVVM + Clean Architecture-inspired layering |
| Async | Kotlin Coroutines |
| Observable Data | Flow / StateFlow |
| Local Database | Room |
| Networking | Retrofit + OkHttp |
| Dependency Injection | Hilt |
| Navigation | Navigation Compose |
| Testing | JUnit + Android testing tools |

The exact versions and configuration will be decided during Android project setup.

---

# Architecture in One View

    ┌──────────────────────────────┐
    │       Presentation           │
    │                              │
    │  Compose + ViewModel         │
    │  StateFlow + Navigation      │
    └──────────────┬───────────────┘
                   │
                   ↓
    ┌──────────────────────────────┐
    │           Domain             │
    │                              │
    │  Models + Use Cases          │
    │  Repository Contracts        │
    └──────────────┬───────────────┘
                   │
                   ↓
    ┌──────────────────────────────┐
    │            Data              │
    │                              │
    │  Repository Implementations  │
    │  Mappers + Data Sources      │
    └───────────┬───────────┬──────┘
                │           │
                ↓           ↓
        ┌────────────┐ ┌────────────┐
        │   Local    │ │   Remote   │
        │            │ │            │
        │ Room / DAO │ │ Retrofit   │
        │ Database   │ │ + OkHttp   │
        └────────────┘ └─────┬──────┘
                             │
                             ↓
                       External API

---

# What This Architecture Gives Us

The architecture provides:

- Offline-first behavior
- Clear separation of responsibilities
- UI independent of data sources
- Testable application logic
- Replaceable infrastructure
- Consistent local data flow
- A structure that can evolve with the product

At the same time, we will avoid adding layers or abstractions unless they solve an actual problem.

---

# Implementation Principle

The architecture is a guide, not a reason to over-engineer the application.

During implementation:

1. Start with the simplest solution that satisfies the requirement.
2. Add an abstraction when there is a clear reason for it.
3. Keep responsibilities easy to understand.
4. Avoid creating classes only to follow a pattern.
5. Revisit architectural decisions when the product actually requires a change.

The goal is to build a real application with a clean and understandable architecture, not to maximize the number of layers or classes.
