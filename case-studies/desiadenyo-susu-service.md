[Back to Profile Overview](../README.md)

# Desiadenyo Susu Service: Digital Microfinance and Field Ledger Platform

[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3.x-0175C2?logo=dart&logoColor=white)](https://dart.dev)
[![Firebase](https://img.shields.io/badge/Firebase-Auth_%7C_Firestore-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Architecture](https://img.shields.io/badge/Architecture-Feature--First_Clean_MVVM-green)](https://flutter.dev)
[![Security](https://img.shields.io/badge/Security-RBAC_%26_Firestore_Rules-red)](https://firebase.google.com/docs/firestore/security/get-started)

**Desiadenyo Susu Service** is a production-grade, client-commissioned financial ledger and microfinance management mobile application designed for field agents and administrators in informal banking and rotating savings ecosystems (Susu). The system digitizes paper collection cards, daily field deposits, withdrawals, commission rates, and reconciliations with strict double-entry integrity, real-time analytics, and role-based access control.

---

## Abstract and Problem Domain

In West African informal finance, the traditional *Susu* system provides vital micro-savings and micro-credit services to small traders and market merchants. However, manual paper-card collection suffers from systemic vulnerabilities:
1. **Ledger Discrepancies and Fraud:** Paper entries lack immutable audit trails, making reconciliation between field agents and central management prone to disputes.
2. **Delayed Cash Flow Visibility:** Administrators lack real-time oversight of daily field cash collections and agent balances.
3. **Operational Bottlenecks:** Physical ledger books impede customer onboarding, card number lookup, and daily rate calculations.

Desiadenyo Susu Service resolves these challenges by introducing a centralized, real-time digital ledger with cryptographically secured cloud synchronization, strict role-based authorization, and analytical dashboards.

---

## Core System Capabilities

### 1. Multi-Tier Role-Based Access Control (RBAC)
- **Field Agents:** Authenticated field interface tailored for daily route collections, customer lookups by physical card number or name, transaction logging (deposits/withdrawals) against predefined customer rates, direct customer calling via dialer integration, and personal daily collection summaries (`MyActivityScreen`).
- **Administrators:** Comprehensive managerial dashboard featuring aggregate deposit and withdrawal metrics, agent activity auditing, customer rate configuration, transaction reversals with audit notes, and agent activation controls.

### 2. Transaction Integrity and Ledger Accounting
- **Immutable Transaction Records:** Every entry records `amount`, `customerId`, `customerCardNumber`, `agentId`, `agentName`, `type` (`deposit`, `withdrawal`, `openingBalance`, `reversal`), and server timestamps.
- **Strict Transaction Reversals:** Erroneous transactions cannot be mutated or deleted; instead, compensatory `reversal` entries are logged referencing the original `reversesId` with required audit notes.
- **Atomic Balance Updates:** Customer balances are dynamically recalculated and verified to prevent inconsistent state transitions.

### 3. Financial Analytics and Reporting
- **30-Day Cash Flow Visualization:** Interactive time-series charts powered by `fl_chart` mapping daily inflows, outflows, and net collection trends.
- **Drill-Down Reconciliation:** Interactive filtering by agent, date ranges, and transaction modalities.
- **Automated CSV Export:** Ledger statement generation and sharing via `csv`, `path_provider`, and `share_plus` for off-app bookkeeping and audits.

---

## Software Architecture and Engineering Design

The project strictly implements a **Feature-First Clean MVVM (Model-View-ViewModel)** architectural pattern with decoupled domain layers, zero UI logic in ViewModels, and dependency injection.

```text
lib/
├── core/                               # Cross-cutting foundational modules
│   ├── constants/                      # Strict constant separation (No magic values)
│   │   ├── app_constants.dart          # Currency configurations, defaults, routes
│   │   ├── app_sizes.dart              # Spacing tokens, dimensions, border radii
│   │   ├── app_strings.dart            # User-facing localized string catalogs
│   │   ├── firestore_constants.dart    # Database schema collections and fields
│   │   └── pref_keys.dart              # Local storage cache keys
│   ├── di/                             # Service locator dependency injection
│   ├── errors/                         # Structured failure models and domain exceptions
│   ├── extensions/                     # Unified app extensions (context, dates, currency)
│   ├── theme/                          # Theme definitions, color tokens, typography
│   └── widgets/                        # Globally reusable atomic UI components
│
└── features/                           # Independent, decoupled feature packages
    ├── auth/                           # Authentication, role resolution, session lifecycle
    ├── customers/                      # Customer profile management, card numbers, rates
    ├── transactions/                   # Ledger operations, reversals, analytics dashboards
    └── agent_management/               # Agent creation, status toggles, performance tracking
```

### Architectural Highlights

- **Domain Isolation:** Each feature is organized into strict `data/`, `domain/`, and `presentation/` boundaries. ViewModels depend exclusively on abstract repository contracts (`domain/repositories/`), never concrete implementations.
- **Dart 3 Sealed States:** Screen and process states are modeled via exhaustive sealed class hierarchies (`Initial`, `Loading`, `Success`, `Error`), eliminating mutable boolean flags ("boolean soup") and guaranteeing compile-time pattern matching exhaustiveness.
- **Clean Provider State Management:** ViewModels are clean classes decoupled from the Flutter widget tree. `BuildContext` is never passed into ViewModels, preserving unit testability.
- **Lean Views and Rebuild Optimization:** Screens delegate rendering to extracted stateless sub-widgets, minimizing rebuild scopes across high-frequency data streams.

---

## Security, Rules, and Data Protection

The system enforces cloud-native security at the database boundary via production-hardened `firestore.rules`:
- **Server-Side Role Verification:** User roles (`admin` vs. `agent`) are verified against administrative records before granting collection or query rights.
- **Field-Level Validation:** Incoming transaction writes must adhere to strict type schemas, positive amount thresholds, and non-empty agent attributions.
- **Ledger Immutability:** Update and delete operations on the `transactions` collection are rejected at the rule level; all corrections must proceed via verified reversal transactions.
- **Customer Card Uniqueness:** Ensures card numbers remain consistent and uniquely indexed to prevent duplicated accounts in the field.

---

## Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Framework & Language** | Flutter (3.x), Dart (3.x) |
| **State Management** | Provider, Dart 3 Sealed Classes |
| **Architecture** | Feature-First Clean MVVM, Service Locator DI |
| **Backend & Database** | Firebase Authentication, Cloud Firestore (Real-time NoSQL) |
| **Data Visualization** | `fl_chart` (Time-series cash flow charts) |
| **Data Export & I/O** | `csv`, `path_provider`, `share_plus`, `url_launcher` |
| **Security & Auditing** | Cloud Firestore Declarative Security Rules (RBAC) |

---

## Academic and Industry Relevance

This project showcases critical competencies in enterprise software engineering, fintech systems, and distributed applications:
- **Financial Software Engineering:** Implementing immutable audit trails, compensating transactions, and atomic state reconciliations under field network constraints.
- **Role-Based Authorization Architecture:** Designing secure multi-tenant client interfaces backed by serverless declarative security rules.
- **Clean Architecture Implementation:** Demonstrating practical mastery of SOLID principles, dependency inversion, and strict layer decoupling in cross-platform mobile development.
- **Emerging Market Financial Inclusion:** Digital transformation of informal financial systems, bridging physical cash collection with real-time digital accounting.
