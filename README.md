<div align="center">

# Innocent Agbadi

### AI & Mobile Systems Engineer | Flutter & Dart 3 | Google Cloud Vertex AI & Firebase | Clean Architecture

**Ghana / Remote** &nbsp;|&nbsp; **Production AI & Mobile Systems** &nbsp;|&nbsp; **Software Engineer**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/innocent-agbadi-080222350)
[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:stonard5560@gmail.com)
[![S Learning](https://img.shields.io/badge/Flagship_App-S--Learning-2EA043?style=for-the-badge&logo=googleplay&logoColor=white)](https://slearning.app)

</div>

---

## About Me

I am an **AI and Mobile Systems Engineer** focused on designing reliable, production-ready intelligent applications and distributed mobile systems across **EdTech**, **FinTech / Microfinance**, **Civic Cryptography**, and **Service Marketplaces**.

- **Applied AI Systems Engineering:** Experienced in building deterministic LLM orchestration pipelines with **Google Cloud Vertex AI** (`gemini-3.1-flash-lite`), dense vector embeddings (`gemini-embedding-001`), **Cosine KNN vector search**, schema-constrained JSON generation, defensive score verification guardrails, and non-blocking token telemetry.
- **Production Cross-Platform Delivery:** End-to-end engineering from architectural design and offline local persistence (`SQLite`) to **Firebase** backends, **Cloud Functions v2 (TypeScript)**, **Google Cloud Platform**, and live releases on **Google Play** and the **Apple App Store**.
- **Software Craft and Security:** Committed to **Feature-First Clean MVVM**, **Dart 3 Sealed States**, dependency injection (`get_it`), declarative RBAC security rules, and hardware-backed local cryptography.

---

## Tech Stack & Tools

**AI & Machine Learning**  
![Vertex AI](https://img.shields.io/badge/Vertex_AI-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini_LLM_%26_Embeddings-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)
![Firebase AI Logic](https://img.shields.io/badge/Firebase_AI_Logic-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![Vector Search](https://img.shields.io/badge/Cosine_KNN_Search-0F9D58?style=for-the-badge)
![Schema Engineering](https://img.shields.io/badge/Prompt_%26_Schema_Engineering-333333?style=for-the-badge)

**Mobile & Frontend**  
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart_3-0175C2?style=for-the-badge&logo=dart&logoColor=white)
![Provider](https://img.shields.io/badge/Provider-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![GetIt](https://img.shields.io/badge/GetIt_DI-0175C2?style=for-the-badge)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

**Backend, Cloud & Security**  
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![Cloud Firestore](https://img.shields.io/badge/Cloud_Firestore-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![Cloud Functions](https://img.shields.io/badge/Cloud_Functions_v2-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white)
![Eventarc](https://img.shields.io/badge/Eventarc-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white)

---

## Featured Projects & Technical Case Studies

> **Portfolio Note:** To protect client confidentiality and commercial intellectual property, the full source code repositories for production and client engagements remain private. Complete technical architecture case studies, system diagrams, verification algorithms, and UI mockups are documented publicly in [`case-studies/`](./case-studies/). Full repository access can be provisioned upon request for graduate admissions or technical review.

---

### 1. S-Learning — AI-Powered Adaptive Educational Ecosystem *(Flagship Production App)*

> Live cross-platform mobile application combining Google Cloud Vertex AI, dense vector embeddings, and structured LLM orchestration to deliver automated subjective grading, adaptive quiz generation, and semantic search.

- **Links:**
  [![Technical Case Study](https://img.shields.io/badge/Read-Technical_Case_Study-1F6FEB?style=flat-square&logo=readthedocs&logoColor=white)](./case-studies/s-learning-ai-architecture.md)
  [![Website](https://img.shields.io/badge/Website-slearning.app-2EA043?style=flat-square&logo=googlechrome&logoColor=white)](https://slearning.app)
  [![Google Play](https://img.shields.io/badge/Google_Play-Download-34A853?style=flat-square&logo=googleplay&logoColor=white)](https://play.google.com/store/apps/details?id=com.agbadiinnocent.slearning)
  [![App Store](https://img.shields.io/badge/App_Store-Download-0D96F6?style=flat-square&logo=apple&logoColor=white)](https://apps.apple.com/app/s-learning/id6764841176)

| AI Tutor and Tool Hub | Curriculum-Aligned Lesson Planner | AI-Synthesized Study Notes | AI Flashcard Generator |
| :---: | :---: | :---: | :---: |
| <img src="docs/images/ai_assistant_home.png" width="180" alt="S-Learning AI Assistant Home" /> | <img src="docs/images/lesson_plan_preview.jpg" width="180" alt="Lesson Plan Preview with AI Assistant" /> | <img src="docs/images/ai_notes.png" width="180" alt="AI Notes with Rich Text and TTS" /> | <img src="docs/images/flashcards.png" width="180" alt="AI Generated Flashcards" /> |

- **Key AI & Engineering Highlights:**
  - **Server-Side Subjective Assessment Orchestrator:** Automates open-ended quiz grading using Vertex AI (`gemini-3.1-flash-lite`, `temperature: 0.1`, JSON Response Schema) with server-side authoritative rubric hydration, exponential backoff retries, 45-second timeout guards, defensive score clamping (`[0, totalMarks]`), atomic Firestore `WriteBatch` persistence, and Node.js unit tests.
  - **Semantic Search & Vector Recommendation Engine:** Uses a pooled Vertex AI `gemini-embedding-001` client paired with native Firestore Cosine KNN retrieval (`findNearest`) for personalized feeds, semantic forum search, and course discovery.
  - **Adaptive Quiz Engine:** Dynamically synthesizes question batches conditioned on learner history, difficulty, and XP across 6 rotating modalities using type-scoped JSON schemas and multimodal document ingestion (PDF, DOCX, PPTX, URLs).
  - **AI Token Telemetry & Governance:** Records non-blocking daily token and image metrics (`TokenUsageTracker`) per AI tool alongside Firebase App Check, Crashlytics, and Eventarc triggers.

---

### 2. Desiadenyo Susu Service — Digital Microfinance and Field Ledger Platform

> Client-commissioned financial ledger platform digitizing informal rotating savings (Susu) operations for field agents and microfinance administrators.

- **Documentation:**
  [![Technical Case Study](https://img.shields.io/badge/Read-Technical_Case_Study-1F6FEB?style=flat-square&logo=readthedocs&logoColor=white)](./case-studies/desiadenyo-susu-service.md)
  `Private Client Production` &nbsp;|&nbsp; *Flutter • Dart 3 • Provider • Firebase Auth • Cloud Firestore*

- **Key Engineering Highlights:**
  - **Feature-First Clean MVVM:** Strict `data/`, `domain/`, and `presentation/` boundaries with abstract repository contracts, zero `BuildContext` in ViewModels, and **Dart 3 `sealed class` states**.
  - **Multi-Tier RBAC & Immutable Ledger:** Distinct workflows for Field Agents and Administrators enforced by hardened `firestore.rules`, immutable transaction entries, and non-destructive compensating reversals with audit notes.
  - **Analytics & Reconciliation:** 30-day cash flow trend visualization (`fl_chart`), drill-down transaction audits, and CSV report exporting.

---

### 3. GNATOC Voting System — Secure On-Campus Digital Election Platform

> Production-complete, cryptographically hardened electronic voting kiosk and election administration system built for the Ghana National Association of Teachers On Campus (GNATOC).

- **Documentation:**
  [![Technical Case Study](https://img.shields.io/badge/Read-Technical_Case_Study-1F6FEB?style=flat-square&logo=readthedocs&logoColor=white)](./case-studies/gnatoc-voting-system.md)
  `Private / Production Complete` &nbsp;|&nbsp; *Flutter • Cloud Firestore Transactions • Crypto • Secure Storage • TTS*

- **Key Engineering Highlights:**
  - **Atomic Double-Vote Race Prevention:** Uses server-only queries (`Source.server`) and reads-first Firestore `runTransaction` locks over `votes/{voterId}` audit documents to guarantee single-vote consistency across concurrent kiosks.
  - **Constitutional Ballot Secrecy:** Decouples anonymized voter audit receipts from candidate vote tallies while preserving verifiable participation logs.
  - **Hardware Kiosk Hardening & A11y:** Enforces salted SHA-256 device PINs stored in OS keychains (`flutter_secure_storage`), kiosk lockdown (`wakelock_plus`, `flutter_window_close`), Text-to-Speech ballot guidance (`flutter_tts`), real-time `fl_chart` analytics, and certified PDF election reports.

---

### 4. HairHQ — On-Demand Beauty Services and Salon Booking Platform *(In Development)*

> Architectural prototype and active development codebase for a two-sided salon appointment and mobile stylist marketplace.

- **Documentation:**
  [![Technical Case Study](https://img.shields.io/badge/Read-Technical_Case_Study-1F6FEB?style=flat-square&logo=readthedocs&logoColor=white)](./case-studies/hair-hq.md)
  `Private / In Development` &nbsp;|&nbsp; *Flutter • Dart 3 • Provider • GetIt DI • SharedPreferences*

- **Key Engineering Highlights:**
  - **Clean Architecture Prototype:** Built on Feature-First Clean MVVM, `get_it` service locator dependency injection, Dart 3 sealed states, and centralized constant/theme token managers.
  - **Preference-Driven Onboarding Engine:** Interactive multi-step user preference configuration and live feed personalization preview.

---

## GitHub Activity

<div align="center">

![Innocent's GitHub Stats](https://github-readme-stats.vercel.app/api?username=stonardgh&show_icons=true&count_private=true&theme=tokyonight&hide_border=true)
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=stonardgh&layout=compact&theme=tokyonight&hide_border=true)

[![GitHub Streak](https://streak-stats.demolab.com?user=stonardgh&theme=tokyonight&hide_border=true)](https://git.io/streak-stats)

</div>

---

## Let's Connect

- **LinkedIn:** [linkedin.com/in/innocent-agbadi-080222350](https://www.linkedin.com/in/innocent-agbadi-080222350)
- **Email:** [stonard5560@gmail.com](mailto:stonard5560@gmail.com)
- **Location:** Ghana (Available for Remote Opportunities & Graduate Research)
