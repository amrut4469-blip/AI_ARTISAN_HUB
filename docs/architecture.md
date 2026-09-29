# 🏗️ Architecture

## Overview

```mermaid
flowchart TD
    UI[📱 Android App<br/>Kotlin + Jetpack Compose] --> VM[ViewModel / Use Cases]
    VM --> REPO[Repository]
    REPO --> API[Firebase / Backend APIs]
    API --> FS[(Cloud Firestore)]
    API --> STG[(Cloud Storage)]
    API --> CF[Cloud Functions]
    API --> FCM[Firebase Cloud Messaging]
    CF --> AI[🤖 AI Service]
    CF --> PAY[💳 Payment Provider]
    CF --> MAP[🗺️ Maps / Routing]
```

## Layers

| Layer | Responsibility |
|---|---|
| UI (Compose) | Screens, navigation, animation |
| ViewModel / Use Cases | UI state and business rules |
| Repository | Single source of data for the app |
| Firebase / Backend | Auth, database, storage, functions, messaging |
| External services | AI model, payment gateway, maps |

## Backend Principles

- The **client is never trusted** for authorization
- Business-critical state transitions happen on the **backend**
- Use **server timestamps** for important events
- Use indexes and query planning for high-volume collections
- Separate **public profile data** from **private account/security data**
- Store large media in **object storage**, not database documents
- Keep **audit logs** append-only and protected

## Order State Machine

```mermaid
stateDiagram-v2
    [*] --> Created
    Created --> PaymentPending
    PaymentPending --> Paid
    PaymentPending --> PaymentFailed
    Paid --> Confirmed
    Confirmed --> Preparing
    Preparing --> ReadyForPickup
    ReadyForPickup --> PickedUp
    PickedUp --> InTransit
    InTransit --> Delivered
    Confirmed --> Cancelled
    Delivered --> ReturnRequested
    ReturnRequested --> ReturnApproved
    ReturnApproved --> Returned
    Returned --> Refunded
```

## Payments

- Payment gateway abstraction (not tied to one provider)
- Server-side payment verification and webhook handling
- Idempotent callbacks to prevent duplicate orders
- Server-side coupon validation
- Invoice / receipt generation
- Refund workflow with full status history

## Real-Time Chat

Message created → backend validates sender → message stored → recipient updated in real time → notification sent → read state updated.

Media: record/select → compress → secure upload → create media reference → send metadata → recipient loads via authorized access.

See also: [Database Design](database-design.md) · [Tech Stack](tech-stack.md) · [Security](security.md)
