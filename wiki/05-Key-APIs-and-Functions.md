# 05 — Key APIs & Functions

This repository does **not** contain implemented classes or production source files. There are no concrete application classes, React components, service classes, or exported functions to document from code.

Instead, the master spec defines the most important **planned APIs, hooks, and domain functions**. This page documents those.

Primary source: [trainflow_especifica_o_mestre_do_produto_1.md](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md)

## Important Note

If this repo is later turned into a real application, this page should be updated with actual source-level symbols. Today, the best available "key function" documentation is conceptual.

## Planned Server Endpoints

### `POST /api/auth/new-student`

Core onboarding endpoint for trainer-created student accounts.

Responsibilities:

- Validate trainer-authenticated request
- Receive `{ full_name, email, assessment_data }`
- Compute body-composition metrics
- Compute somatotype
- Generate `TrainingOrientation`
- Invite or create the student account via Supabase Admin API
- Create `profiles`, `trainer_students`, and `physical_assessments` records
- Return the student ID and generated guidance

Why it matters:

- This endpoint encodes the repo's central business rule: the student never self-registers.

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L307-L320](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L307-L320)

### `POST /api/sync/workout-events`

Offline reconciliation endpoint for workout progress.

Responsibilities:

- Receive batched outbox events from the client
- Upsert sessions and sets using client-generated UUIDs
- Preserve idempotency so retries never duplicate data

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L615-L619](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L615-L619)

### `POST /api/push/subscribe`

Push-registration endpoint.

Responsibilities:

- Accept a browser push subscription from the client
- Persist it into `push_subscriptions`

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L670-L676](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L670-L676)

### `POST /api/push/send`

Server-side delivery endpoint for push notifications.

Responsibilities:

- Look up saved subscriptions
- Send web push notifications using VAPID credentials
- Support events like new message, new published plan, workout reminder

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L674-L678](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L674-L678)

## Planned Client/Library Functions

### `syncOutbox()`

The spec identifies `syncOutbox()` as the central offline-sync function.

Responsibilities:

- Read pending events from IndexedDB
- Send a batch to `/api/sync/workout-events`
- Retry with exponential backoff
- Mark failures after max retries

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L615-L619](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L615-L619)

### `registerBackgroundSync('workout-sync')`

Background Sync integration point.

Responsibilities:

- Register deferred workout synchronization when the browser supports it
- Reduce user-visible sync failures after reconnect

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L618-L619](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L618-L619)

### `subscribePush()`

Planned client push helper in `lib/push/client.ts`.

Responsibilities:

- Register the Service Worker
- Call `pushManager.subscribe()`
- POST the subscription to `/api/push/subscribe`

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L670-L675](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L670-L675)

## Planned Realtime Hook

### `lib/chat/useChat.ts`

The spec includes a sample subscription hook for chat.

Responsibilities:

- Open a channel named `messages:${conversationId}`
- Listen to `postgres_changes` inserts on `public.messages`
- Append new messages to local state
- Remove the channel on unmount

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L683-L699](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L683-L699)

## Planned Middleware

### `middleware.ts`

The spec defines an edge middleware contract rather than concrete implementation.

Responsibilities:

- Read `user_role` from JWT app metadata
- Restrict trainer routes to trainers
- Restrict student routes to students
- Redirect unauthenticated users to the proper login screen
- Exclude static paths such as `_next/static`, `sw.js`, and manifest assets

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L703-L712](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L703-L712)

## Planned Database Function

### `public.custom_access_token_hook(event jsonb)`

This is the only concrete function body present in the spec.

Responsibilities:

- Read `role` from `public.profiles`
- Inject `claims.app_metadata.user_role` into the JWT payload

Why it matters:

- It removes the need for route middleware to query the database to determine role.

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L714-L726](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L714-L726)

## Planned Data Contract

### `TrainingOrientation`

The spec defines a TypeScript interface for the generated training-orientation payload.

Fields:

- `somatotype`
- `summary`
- `primary_goal`
- `training_focus`
- `nutrition_note`
- `highlights`
- `trainer_notes`

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L397-L418](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L397-L418)

## Domain Calculation Functions (Implicit)

These are not named in code, but they are clearly required by the business logic:

- `calculateBodyDensity(...)`
  - Pollock-based density from skinfold measurements
- `calculateBodyFatPct(...)`
  - Siri equation
- `calculateBMI(...)`
  - weight / height^2
- `calculateWaistHipRatio(...)`
  - waist / hip
- `classifySomatotype(...)`
  - Heath-Carter component scoring and dominant-type classification
- `generateTrainingOrientation(...)`
  - Rule-based recommendation engine from measurements + somatotype

Formula references:

- Body density and fat %: [trainflow_especifica_o_mestre_do_produto_1.md:L328-L348](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L328-L348)
- Somatotype: [trainflow_especifica_o_mestre_do_produto_1.md:L361-L396](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L361-L396)
- Orientation matrix: [trainflow_especifica_o_mestre_do_produto_1.md:L420-L429](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L420-L429)
