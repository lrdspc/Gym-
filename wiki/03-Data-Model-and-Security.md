# 03 — Data Model & Security

This page summarizes the **planned database model and access-control strategy** described in the TrainFlow spec.

Primary source: [trainflow_especifica_o_mestre_do_produto_1.md](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md)

## Data Architecture

The planned backend is **Supabase Postgres** with:

- Auth-backed user identities
- Application data in `public.*` tables
- Row Level Security (RLS) on all user-facing tables
- Realtime on `messages`
- Storage for media assets such as exercise GIFs/audio

Schema reference: [trainflow_especifica_o_mestre_do_produto_1.md:L90-L269](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L90-L269)

## Core Tables and Responsibilities

### Identity and relationships

- `profiles`
  - One row per authenticated user
  - Stores `role`, `full_name`, `avatar_url`
  - Role values: `trainer` or `student`
- `trainer_students`
  - Links a trainer to a student or invited email
  - Tracks onboarding state: `invited`, `active`, `inactive`

These two tables form the core authorization and ownership graph for the app.

### Assessment and body-composition domain

- `physical_assessments`
  - Stores anthropometric inputs
  - Stores computed outputs:
    - body density
    - body fat percentage
    - lean mass
    - BMI
    - waist/hip ratio
    - somatotype
    - generated training orientation

This table is central to the onboarding rule because the trainer-created assessment triggers the student account invite flow.

### Exercise and training-plan domain

- `exercises`
  - Exercise library
  - Supports both global exercises and trainer-owned custom exercises
  - Media fields include `gif_url` and `audio_url`
- `training_plans`
  - Plan header assigned from a trainer to a student
- `plan_days`
  - Named days within a plan
- `day_exercises`
  - Ordered exercises within a given day
  - Stores set/reps/rest metadata

Relationship chain:

```text
training_plans
  └─ plan_days
       └─ day_exercises
            └─ exercises
```

### Workout-execution domain

- `workout_sessions`
  - One logical workout execution session
  - Includes `client_uuid` for idempotent sync
- `session_sets`
  - Individual logged sets for a session
  - Also keyed with `client_uuid` for safe replay/resubmission

This design supports offline capture first and server reconciliation later.

### Chat and notifications domain

- `conversations`
  - Direct and group conversation containers
- `conversation_members`
  - Membership table
- `messages`
  - Chat messages
- `push_subscriptions`
  - Browser/device push endpoints for each user

## Security Model

RLS is intended to be enabled for all tables, with policies summarized in the spec:

- `profiles`: own row; trainer can read linked students
- `physical_assessments`: trainer of the student has full access; student reads own records
- `exercises`: everyone reads global; trainer manages own exercises
- `training_plans`: trainer full access; student reads assigned plan
- `workout_sessions` and `session_sets`: student owner only
- `conversations` and `messages`: members only
- `push_subscriptions`: own row only

Policy summary reference: [trainflow_especifica_o_mestre_do_produto_1.md:L271-L282](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L271-L282)

## JWT Role Injection

The spec proposes a `custom_access_token_hook` function that injects `user_role` into JWT app metadata during authentication:

- Avoids runtime DB lookups in edge middleware
- Enables fast route gating for trainer vs student areas

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L714-L726](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L714-L726)

## Domain Logic Embedded in the Spec

Although not implemented as code in this repo, the specification defines important business logic that would normally live in services or domain modules:

- Pollock 7-site / fallback 3-site body-density formulas
- Siri body-fat calculation
- BMI and waist-hip ratio calculation
- Heath-Carter somatotype classification
- Rule-based training-orientation generation

Calculation references:

- Body composition: [trainflow_especifica_o_mestre_do_produto_1.md:L326-L360](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L326-L360)
- Somatotype: [trainflow_especifica_o_mestre_do_produto_1.md:L361-L396](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L361-L396)
- Training orientation contract: [trainflow_especifica_o_mestre_do_produto_1.md:L397-L429](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L397-L429)

## Practical Dependency Relationships

From a future implementation standpoint, data dependencies flow like this:

- Auth depends on `profiles`
- Trainer onboarding depends on:
  - `profiles`
  - `trainer_students`
  - `physical_assessments`
  - Supabase Admin API
- Workout execution depends on:
  - `training_plans`
  - `plan_days`
  - `day_exercises`
  - `workout_sessions`
  - `session_sets`
- Chat depends on:
  - `conversations`
  - `conversation_members`
  - `messages`
  - Realtime subscriptions
- Push depends on:
  - `push_subscriptions`
  - Service Worker registration
  - server-side `web-push`
