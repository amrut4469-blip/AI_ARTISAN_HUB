# AI ARTISAN HUB — System Architecture

## Architecture Overview

AI ARTISAN HUB follows a layered application architecture designed for a multi-role AI-powered marketplace and social-commerce platform.

```text
User
  ↓
Android Application
  ↓
Jetpack Compose UI
  ↓
ViewModel / Use Cases
  ↓
Repository
  ↓
Firebase / Backend APIs
  ↓
Firestore / Storage / Cloud Functions / Messaging
  ↓
AI Services / Payment Provider / Maps & Routing
