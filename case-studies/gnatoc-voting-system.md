[Back to Profile Overview](../README.md)

# GNATOC Voting System: Secure On-Campus Digital Election Platform

[![Flutter](https://img.shields.io/badge/Flutter-Desktop_%7C_Mobile-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3.x-0175C2?logo=dart&logoColor=white)](https://dart.dev)
[![Cryptography](https://img.shields.io/badge/Security-SHA--256_%7C_Secure_Storage-blue)](https://pub.dev/packages/flutter_secure_storage)
[![Firebase](https://img.shields.io/badge/Backend-Firestore_Transactions-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Accessibility](https://img.shields.io/badge/A11y-Text--to--Speech-green)](https://pub.dev/packages/flutter_tts)

**GNATOC Voting System** is a production-complete, cryptographically hardened electronic voting and election administration platform built for the Ghana National Association of Teachers On Campus (GNATOC). The system replaces paper balloting with dedicated digital polling kiosks, real-time audit logs, atomic race-free vote processing, accessible voice guidance, and automated certification reporting.

---

## Abstract and Problem Domain

Campus elections in tertiary institutions regularly encounter security and administrative vulnerabilities:
1. **Ballot Stuffing and Impersonation:** Paper ballots are vulnerable to counterfeit votes, double voting, and voter register manipulation.
2. **Slow, Disputed Manual Tallies:** Physical sorting and hand counts take hours or days, creating election-night tension and allegations of bias.
3. **Physical Accessibility Gaps:** Visually impaired voters frequently require third-party assistance, violating ballot secrecy.
4. **Hardware and Kiosk Tampering:** Unsupervised digital booths running on general-purpose hardware risk unauthorized restarts, network interception, or application closure.

The GNATOC Voting System resolves these issues through **kiosk lockdown enforcement**, **atomic multi-document database transactions**, **hardware-backed local cryptography**, and **Text-to-Speech ballot guidance**.

---

## Core System Architecture and Security Protocols

```text
[Voter Authentication & Kiosk Terminal]
   ├── Hardware Device PIN (Salted SHA-256 via OS Keychain / DPAPI)
   ├── Kiosk Lockdown (Wakelock + Window Close Interception)
   └── Accessible Voice Synthesis (TTS Category & Candidate Reader)
                   │
                   ▼ Server-Only Lookup (Source.server)
[Voter Register Verification]
   └── Verification against active Polling Station register
                   │
                   ▼ Atomic Multi-Document Transaction
[Firestore runTransaction Engine]
   ├── Reads: Verify non-existence of votes/{voterId} audit doc
   ├── Double-Vote Race Guard: Rejects duplicate entries atomically
   ├── Writes (Step 1): Atomic increment (+1) on candidate voteCount
   ├── Writes (Step 2): Anonymized timestamped audit receipt creation
   └── Writes (Step 3): Voter status committed to 'voted'
                   │
                   ▼ Real-Time Aggregation & Certification
[Administrative Reporting & Analytics]
   ├── Live Dynamic Bar & Donut Visualizations (fl_chart)
   └── Certified Vector PDF Election Invoices & Registers (pdf)
```

---

## Technical Highlights and Implementations

### 1. Atomic Double-Vote Prevention and Ballot Secrecy
Implemented in `VotingService.submitBallot()` (`lib/data/services/voting_services.dart`):
- **Server-Only Querying (`Source.server`):** All voter validations bypass local cache layers to guarantee real-time registration accuracy across all concurrent polling stations.
- **Atomic Transaction Isolation (`runTransaction`):** Implements strict "reads-first" Firestore transaction discipline. The system verifies that no audit token exists under `categories/{categoryId}/candidates/{candidateId}/votes/{voterId}` before executing writes.
- **Ballot Secrecy Architecture:** Audit receipts store only the anonymized voter ID and server timestamps. No voter identification is concatenated with candidate choices in the public tally, maintaining constitutional ballot privacy while proving voter participation.
- **Idempotency Guard:** If two polling kiosks attempt to cast ballots with the same voter ID simultaneously, the transaction locks conflict and abort before state mutation occurs.

### 2. Kiosk Hardening and On-Device Cryptography
Implemented in `DevicePinService` (`lib/core/device_pin_service.dart`):
- **Hardware-Level Salted SHA-256 PIN:** Kiosk setup requires a physical installation PIN. Secrets are salted and stored in the OS hardware-backed keychain (Apple Keychain on macOS, DPAPI on Windows) via `flutter_secure_storage`.
- **Physical Booth Lockdown:** Integrates `wakelock_plus` to prevent OS display sleep during active voting hours and `flutter_window_close` to intercept accidental or malicious window termination on desktop clients.

### 3. Universal Accessibility (A11y)
Implemented in `TtsService` (`lib/core/tts_service.dart`):
- **Automated Voice Assistance:** Integrates `flutter_tts` configured with controlled speech rates to read ballot positions, instructions, and candidate profiles out loud, allowing visually impaired voters to cast ballots independently and privately.

### 4. Live Election Analytics and Certified PDF Audits
Implemented in `ResultsInvoiceService` and presentation chart widgets:
- **Dynamic Charting:** Real-time percentage breakdowns, lead margins, and voter turnout visualizations using `fl_chart` (custom bar and donut chart widgets).
- **Official PDF Certification:** Generates multi-page, high-resolution election certificate documents (`pdf`, `open_file`, `file_selector`) containing winner ordinal rankings, candidate vote breakdowns, station registries, and official sign-off areas for electoral commissioners.

---

## Repository Structure

```text
natoc_voting_system/
├── lib/
│   ├── core/                           # Core infrastructure & cross-cutting services
│   │   ├── app_shell.dart              # Global application layout and route guards
│   │   ├── device_pin_service.dart     # Salted SHA-256 cryptographic hardware lock
│   │   ├── firestore_constant.dart     # Firestore schema collections and field keys
│   │   ├── registrar_invoice.dart      # Voter registrar PDF generation service
│   │   ├── result_invoice.dart         # Official election result certificate PDF generator
│   │   ├── theme.dart                  # High-contrast accessible design tokens
│   │   └── tts_service.dart            # Text-to-Speech voice guidance service
│   ├── data/
│   │   └── services/                   # Remote data access & transaction orchestration
│   │       ├── voting_services.dart    # Atomic ballot submission and transaction logic
│   │       ├── candidate_services.dart # Candidate and portfolio metadata management
│   │       ├── voter_services.dart     # Voter register importation and status tracking
│   │       └── results_service.dart    # Live election tally and analytics streams
│   ├── domain/                         # Immutable entity models
│   │   ├── ballot.dart                 # Category, Candidate, and Selection models
│   │   ├── polling_station.dart        # Multi-station timing and state entities
│   │   └── voter_model.dart            # Voter registration models and status enums
│   └── presentation/                   # Presentation layer (MVVM)
│       ├── view_models/                # State management providers (Voting, Station, Results)
│       ├── views/                      # Terminal screens (Voting, Results, Kiosk Lock)
│       └── widgets/                    # Bar charts, donut charts, and export dialogs
```

---

## Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Client Platforms** | Flutter (macOS, Windows, Linux, Android, iOS) |
| **Language & SDK** | Dart (3.x) |
| **Cryptography & Storage** | `crypto` (SHA-256), `flutter_secure_storage` (Keychain / DPAPI) |
| **Backend & Realtime Data** | Cloud Firestore (Atomic Transactions), Firebase Auth |
| **Accessibility** | `flutter_tts` (Text-to-Speech synthesis) |
| **Kiosk Security** | `wakelock_plus`, `flutter_window_close` |
| **Analytics & Visualization** | `fl_chart` (Bar & Donut election charts) |
| **Document Generation** | `pdf`, `file_selector`, `open_file` |

---

## Academic and Engineering Relevance

The GNATOC Voting System demonstrates practical competencies in distributed computing, computer security, and civic technology:
- **Concurrency Control in Distributed Systems:** Designing multi-terminal electronic voting architectures that guarantee consistency and prevent double-spending / double-voting without distributed deadlock.
- **Zero-Knowledge Principle & Ballot Anonymity:** Structuring database schemas that decouple participant identity from ballot choice while preserving verifiable receipt audits.
- **Hardware-Software Boundary Security:** Enforcing physical terminal authorization using OS cryptographic subsystems and kiosk confinement techniques.
- **Inclusive Software Design:** Engineering practical accessibility solutions (voice-guided user flows) for institutional democratic processes.
