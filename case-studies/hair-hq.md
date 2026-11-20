[Back to Profile Overview](../README.md)

# HairHQ: On-Demand Beauty Services and Salon Booking Platform

[![Project Status](https://img.shields.io/badge/Status-In_Development-yellow)](https://github.com/stonardgh/hair_hq)
[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3.x-0175C2?logo=dart&logoColor=white)](https://dart.dev)
[![Architecture](https://img.shields.io/badge/Architecture-Feature--First_Clean_MVVM-green)](https://flutter.dev)
[![Firebase](https://img.shields.io/badge/Backend-Firebase_Suite-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/)

**HairHQ** is a cross-platform mobile marketplace application in active development designed to streamline appointment scheduling, mobile stylist discovery, and verified portfolio browsing for barbershops and hair salons. The platform eliminates physical queue waiting by enabling users to book exact time slots for shop visits or on-demand home visits.

---

## Project Status and Overview

> Note: This repository represents an **architectural prototype and active development codebase**. Core foundational layers, application theming, dependency injection, local caching, and the interactive preference onboarding engine are implemented, with real-time booking and discovery services currently in progress.

### The Problem
Traditional barbershops and salons suffer from prolonged physical wait times, opaque pricing, and fragmented booking workflows. Clients lack visibility into stylist availability and verified portfolios, while independent stylists face logistical challenges managing schedules and home-service appointments.

### The Solution
HairHQ models a two-sided marketplace architecture connecting clients with verified grooming professionals through:
- Real-time time slot reservations calibrated to specific service durations.
- Dual-fulfillment service options (in-shop appointments or mobile home services).
- Verified stylist portfolios with transparent upfront pricing.
- Personalized recommendation feeds tailored during user onboarding.

---

## Implemented Architecture and Technical Foundation

The project strictly follows a **Feature-First Clean MVVM (Model-View-ViewModel)** architectural pattern with modular separation of concerns.

```text
lib/
├── core/                               # Cross-cutting foundational modules
│   ├── constants/                      # Separated constant managers
│   │   ├── app_constants.dart          # App-wide routing, config, asset paths
│   │   ├── app_sizes.dart              # UI dimension tokens, spacing, border radii
│   │   ├── app_strings.dart            # Centralized display copy and titles
│   │   └── pref_keys.dart              # SharedPreferences storage keys
│   ├── di/                             # Service locator setup (get_it)
│   ├── extensions/                     # Unified extension helpers (context, theme, strings)
│   ├── services/                       # Local storage and hardware abstraction
│   └── theme/                          # Color palettes, typography, and theme data
│
└── features/                           # Independent functional modules
    └── onboarding/                     # Preference-driven onboarding engine
        ├── data/                       # Repositories and local persistence mapping
        ├── domain/                     # Immutable state models and abstract contracts
        └── presentation/               # ViewModels, sealed states, and view widgets
```

### Key Engineering Highlights

1. **Preference-Driven Multi-Step Onboarding Engine (`features/onboarding/`)**
   - **Feature Showcase:** Auto-cycling value proposition presentation highlighting zero-queue bookings, flexible delivery, and verified portfolios.
   - **Style and Feed Personalization:** Interactive preference selection (Men's Barbering, Ladies' Salon, or Unified View) that configures feed generation parameters.
   - **Personalized Live Preview:** Dynamic UI preview reflecting user selections prior to entering the main application flow.

2. **Dart 3 Sealed Class State Hierarchy**
   - Screen states are governed by exhaustive sealed class hierarchies (`OnboardingState`), eliminating mutable boolean flags and enforcing compile-time safety across state transitions.

3. **Decoupled ViewModel and Dependency Injection**
   - ViewModels are injected with abstract repository contracts (`domain/repositories/`) via `get_it`, keeping business logic decoupled from the Flutter widget tree and UI context.

4. **Design System and Zero Hardcoding Policy**
   - All visual dimensions, typography scales (`GoogleFonts`), string assets, and spacing tokens are managed centrally in dedicated managers (`AppSizes`, `AppStrings`, `AppTheme`), ensuring strict design consistency.

---

## Planned Architecture and Development Roadmap

```text
[Client Applications (iOS / Android)]
              │
              ▼ HTTPS / WebSocket
[Firebase Authentication & Cloud Firestore]
   ├── User & Stylist Profiles (Role-based access)
   ├── Service Catalogs & Real-Time Availability Calendars
   └── Active Bookings & Transaction Records
              │
              ▼ Storage & Triggers
[Firebase Cloud Storage & Cloud Functions]
   ├── High-Resolution Stylist Portfolios & Image Optimization
   └── Automated Booking Notifications & Reminder Schedulers
```

### Implementation Milestones

- [x] Foundation architecture setup (Clean MVVM, `get_it` DI, Theme Engine).
- [x] Multi-step interactive onboarding and preference configuration engine.
- [x] Local state persistence via `SharedPreferences`.
- [ ] User authentication and profile provisioning (Client vs. Stylist roles).
- [ ] Real-time salon and stylist catalog with location-based filtering.
- [ ] Dynamic calendar reservation engine with slot conflict resolution.
- [ ] Cloud Storage integration for verified stylist portfolio galleries.
- [ ] In-app booking confirmation, push notifications, and customer reviews.

---

## Technology Stack

| Component | Technologies |
| :--- | :--- |
| **Framework & Language** | Flutter (3.x), Dart (3.x) |
| **State Management** | Provider, Dart 3 Sealed Classes |
| **Dependency Injection** | `get_it` Service Locator |
| **Backend & Cloud (In Progress)** | Firebase Authentication, Cloud Firestore, Firebase Storage |
| **Local Persistence** | `shared_preferences` |
| **Typography & UI** | `google_fonts`, `flutter_svg`, `cached_network_image` |

---

## Academic and Engineering Relevance

Even as an evolving codebase, HairHQ demonstrates foundational software engineering practices relevant to applied computer science:
- **Clean Architecture and Design Patterns:** Practical application of the Dependency Inversion Principle (DIP), Single Responsibility Principle (SRP), and clean separation between UI, presentation logic, and domain contracts.
- **State Machine Modeling:** Leveraging modern programming language features (Dart 3 sealed classes and pattern matching) to construct predictable, bug-resilient user state flows.
- **Two-Sided Marketplace System Design:** Structural planning for multi-tenant data schemas balancing consumer discovery with vendor scheduling constraints.
