# 03 — Data Model & Security

This repository does not include database migrations. The database schema and security model are specified inside: [trainflow_especifica_o_mestre_do_produto_1.md](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md).

## Core Entities (Planned)

Spec reference (SQL block): [trainflow_especifica_o_mestre_do_produto_1.md:L90-L269](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L90-L269)

### Identity and Roles

- `profiles`
  - `id` references `auth.users(id)`
  - `role`: `trainer` | `student`

### Trainer ↔ Student Relationship

- `trainer_students`
  - `trainer_id` (trainer profile)
  - `student_id` (student profile, nullable until accepted/created)
  - `email` (used for invite workflow)
  - `status`: `invited` | `active` | `inactive`
  - uniqueness: `(trainer_id, email)`

### Physical Assessments (Onboarding Source of Truth)

- `physical_assessments`
  - created by trainer for a student
  - stores raw anthropometrics (skinfolds, circumferences)
  - stores computed values (density, body fat %, BMI, etc.)
  - stores computed classification (`somatotype`) and JSON `training_orientation`

This table is the anchor for the core business rule “trainer initiates student onboarding”: [trainflow_especifica_o_mestre_do_produto_1.md:L285-L305](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L285-L305)

### Exercise Library

- `exercises`
  - global exercises: `is_global = true`
  - trainer custom exercises: `trainer_id != null`
  - optional media: `gif_url`, `audio_url`

### Training Plans

- `training_plans` (trainer → student)
- `plan_days` (ordered)
- `day_exercises` (ordered within a day; references `exercises`)

### Workout Execution Logging

- `workout_sessions`
  - server record of a workout instance
  - has a `client_uuid` for idempotency across offline sync
- `session_sets`
  - records executed sets, also keyed by `client_uuid` for idempotent upsert

### Messaging

- `conversations`
  - direct or group
  - `trainer_id` as the “owner”
- `conversation_members`
  - `(conversation_id, user_id)` primary key
- `messages`
  - `conversation_id`, `sender_id`, `content`, `sent_at`, `read_at`

### Push Notifications

- `push_subscriptions`
  - per-user endpoint + keys
  - uniqueness: `(user_id, endpoint)`

## Access Control (RLS)

The spec expects **Row Level Security enabled on all tables** with policies summarized as:

- `profiles`: user can read their own row; trainer can read linked students
- `physical_assessments`: trainer has full access for their students; student can read their own
- `exercises`: everyone reads global; trainer CRUD on their own
- `training_plans`: trainer full access; student reads own
- `workout_sessions` + `session_sets`: student owns their rows
- `conversations` + `messages`: members only
- `push_subscriptions`: user owns their rows

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L271-L281](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L271-L281)

## Role Claim Injection (JWT Hook)

To avoid route-guard DB lookups, the spec proposes injecting the user role into the JWT at auth time via a Postgres function.

Spec reference: [trainflow_especifica_o_mestre_do_produto_1.md:L714-L726](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L714-L726)

## Notes on Secrets

The spec calls out secrets that must never reach the client:

- `SUPABASE_SERVICE_ROLE_KEY` used for Admin API operations (invites/links)
- VAPID private key for `web-push`

Spec reference (env vars): [trainflow_especifica_o_mestre_do_produto_1.md:L730-L739](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L730-L739)

