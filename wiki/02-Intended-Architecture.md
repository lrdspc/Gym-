# 02 — Intended Architecture

This page documents the **intended TrainFlow system architecture**, as described in the master specification: [trainflow_especifica_o_mestre_do_produto_1.md](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md).

## System Overview

TrainFlow is specified as a **mobile-first Progressive Web Application (PWA)** with two role-based experiences in a single codebase:

- **Student experience**: follow and execute workouts, see guidance, track progress
- **Trainer experience**: manage students, assessments, plans, exercises, and messaging

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L6-L10](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L6-L10)

## Recommended Stack (Planned)

The spec recommends (not implemented in this repo):

- Frontend: React + Vite (SPA)
- Router: TanStack Router
- PWA: Workbox via Vite PWA plugin
- Backend: Supabase (Postgres + Auth + Realtime + Storage)
- Styling: Tailwind + shadcn/ui
- State: Zustand
- Offline storage: idb (IndexedDB)
- Push: web-push (server) + PushManager (client)

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L14-L33](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L14-L33)

## High-Level Component Diagram

```text
┌─────────────────────────┐
│        PWA Client        │
│  (student + trainer UI)  │
│  - router + state         │
│  - offline outbox         │
│  - service worker         │
│  - push client            │
└───────────┬─────────────┘
            │
            │ HTTPS (supabase-js / REST / RPC)
            ▼
┌─────────────────────────┐
│         Supabase         │
│  - Auth (magic link)     │
│  - Postgres + RLS        │
│  - Realtime (chat)       │
│  - Storage (media)       │
└───────────┬─────────────┘
            │
            │ privileged operations
            ▼
┌─────────────────────────┐
│ Minimal Server Endpoints │
│ (service-role protected) │
│ - /api/auth/new-student  │
│ - /api/sync/workout...   │
│ - /api/push/*            │
└─────────────────────────┘
```

## Architectural Responsibilities (Planned Modules)

### 1) Auth + Role Separation

- Use Supabase Auth (magic link) for sessions.
- Use `profiles.role` and inject `user_role` into JWT app metadata using a DB hook.
- Enforce route-level access:
  - trainers: `/t/*`
  - students: `/(student)/*`

Spec references:

- Role-based route protection: [trainflow_especifica_o_mestre_do_produto_1.md:L703-L712](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L703-L712)
- JWT hook: [trainflow_especifica_o_mestre_do_produto_1.md:L714-L726](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L714-L726)

### 2) Trainer-Driven Student Onboarding (Core Business Rule)

Central rule: **the student never creates their own account**.

- Trainer completes a physical assessment form.
- System computes body composition + somatotype + training orientation.
- Server creates/invites the student via Supabase Admin API.

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L285-L320](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L285-L320)

### 3) Offline-First Workout Execution

Workout execution is designed to function reliably offline:

- Persist session state and set logging locally (IndexedDB).
- Append writes to an **outbox** and sync later.
- Sync uses an idempotent `client_uuid` key to avoid duplicates.

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L599-L627](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L599-L627)

### 4) Realtime Messaging

Chat is designed to use Supabase Realtime:

- Subscribe to `messages` inserts filtered by `conversation_id`.
- Clean up channels on unmount.

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L681-L699](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L681-L699)

### 5) Push Notifications

Planned push notification system:

- Client subscribes via Service Worker (`pushManager.subscribe()`).
- Server stores subscriptions in `push_subscriptions` and sends via `web-push`.
- Suppress push if user is active in the relevant conversation (presence).

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L668-L678](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L668-L678)

### 6) PWA Shell + Caching Strategy

Planned PWA behavior:

- `display: standalone`, app icons, install prompt strategy
- Workbox caching strategies for navigation, assets, GIF/audio, and Supabase GET requests
- Background sync triggers outbox sync

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L630-L665](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L630-L665)

## Dependency Relationships (Planned)

Key dependency directions intended by the design:

- UI features (workout, chat, plans) depend on:
  - Auth/session identity
  - Data access layer (Supabase client)
  - Offline subsystem (outbox) for student workout and potentially messaging
- Offline subsystem depends on:
  - IndexedDB schema and serialization
  - Sync endpoint(s) for reconciliation
  - Service Worker / Background Sync for reliability
- Push subsystem depends on:
  - Service Worker registration
  - Stored push subscriptions in the database
  - Server secret keys (VAPID, service role)
- Route protection depends on:
  - JWT role claim injection hook
  - Middleware logic that interprets the role without DB lookups

Environment variable expectations (planned): [trainflow_especifica_o_mestre_do_produto_1.md:L730-L739](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L730-L739)
