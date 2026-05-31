# Code Wiki: TrainFlow Repository

## Overview

This repository is not a conventional application codebase. It is a TrainFlow product archive composed of:

- a master product specification that defines the intended system architecture, data model, security model, and implementation roadmap
- a design system document with tokens and visual rules
- 42 standalone HTML prototypes that represent the student and trainer experiences
- a generated `wiki/` folder with topic-specific repository notes

The most important consequence of that structure is:

- there is no `src/` directory
- there is no package manifest such as `package.json`
- there are no backend services, migrations, or tests checked into this repository
- there are almost no reusable classes or modules in the typical software-engineering sense

This document therefore explains both:

1. the repository as it exists today
2. the application architecture it is clearly intended to become

## Primary Sources

- Master specification: [`stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md`](stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md)
- Design system: [`stitch_modern_application_suite/high_performance_athletic/DESIGN.md`](stitch_modern_application_suite/high_performance_athletic/DESIGN.md)
- Prototype archive: [`stitch_modern_application_suite/`](stitch_modern_application_suite/)
- Existing topic wiki: [`wiki/README.md`](wiki/README.md)

## Repository Structure

```text
/workspace
|-- CODE_WIKI.md
|-- README.md
|-- stitch_modern_application_suite/
|   |-- trainflow_especifica_o_mestre_do_produto_1.md
|   |-- high_performance_athletic/
|   |   `-- DESIGN.md
|   |-- login_do_aluno/
|   |   `-- code.html
|   |-- dashboard_do_aluno/
|   |   `-- code.html
|   |-- player_de_treino/
|   |   `-- code.html
|   |-- dashboard_do_personal/
|   |   `-- code.html
|   `-- ... 38 more screen folders
|-- wiki/
|   |-- README.md
|   |-- 01-Repository-Overview.md
|   |-- 02-Intended-Architecture.md
|   |-- 03-Data-Model-and-Security.md
|   |-- 04-UI-Prototypes-and-Design-System.md
|   |-- 05-Key-APIs-and-Functions.md
|   `-- 06-Running-and-Viewing.md
`-- .trae/
    `-- documents/
```

## Architecture in Two Layers

### 1. Current Repository Architecture

The repository is best understood as four artifact layers:

- **Specification layer**
  - The master spec is the source of truth for the future system.
  - It defines the stack, domain rules, API contracts, database schema, security model, offline strategy, and implementation order.

- **Prototype layer**
  - Each screen folder contains a self-contained `code.html` file and usually a `screen.png`.
  - These are visual and interaction references, not reusable frontend modules.

- **Design-system layer**
  - `DESIGN.md` defines the color palette, typography, spacing, depth model, and component rules.
  - Prototype files re-embed many of these tokens in local `tailwind.config` objects instead of importing them from a shared package.

- **Documentation layer**
  - The `wiki/` directory documents the archive from several angles.
  - `CODE_WIKI.md` serves as the root-level handoff document.

### 2. Intended Application Architecture

The specification describes a future TrainFlow application as a mobile-first PWA with a single codebase and two role-based experiences.

```text
Student UI + Trainer UI
        |
        v
 React/Vite SPA + Router + State
        |
        +--> Offline storage and outbox sync
        +--> Service worker and PWA shell
        +--> Push subscription client
        +--> Realtime chat client
        |
        v
   Supabase platform
   - Auth
   - Postgres
   - Realtime
   - Storage
        |
        v
 Minimal privileged API routes
 - POST /api/auth/new-student
 - POST /api/sync/workout-events
 - POST /api/push/subscribe
 - POST /api/push/send
```

## Major Modules and Responsibilities

Because the repository does not contain implemented source packages, the most accurate way to describe "modules" is to separate current artifact modules from planned runtime modules.

### Current Artifact Modules

#### Master Product Specification

File:

- [`stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md`](stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md)

Responsibility:

- defines the product concept
- recommends the technology stack
- declares the database schema
- specifies RLS and JWT role injection
- describes onboarding, workout logging, chat, push, and offline sync
- outlines the future implementation roadmap

Why it matters:

- this is the closest thing the repository has to a domain model, architecture spec, and backend contract combined

#### Design System

File:

- [`stitch_modern_application_suite/high_performance_athletic/DESIGN.md`](stitch_modern_application_suite/high_performance_athletic/DESIGN.md)

Responsibility:

- provides TrainFlow visual identity
- defines color tokens such as pure black, electric lime, surface layers, and warning states
- defines typography scales using Bebas Neue and Inter
- documents layout, spacing, shapes, glassmorphism, and component conventions

Why it matters:

- nearly every prototype screen mirrors this token model inside its own embedded Tailwind configuration

#### Prototype Screens

Files:

- all `stitch_modern_application_suite/*/code.html`

Responsibility:

- communicate intended UX flows
- model feature areas before implementation
- provide layout, content hierarchy, and visual direction for the future app

Representative screen groups:

- **Student journey**
  - login and welcome flows
  - dashboard and profile
  - workout player and timers
  - history, metrics, habits, community

- **Trainer journey**
  - dashboard and analytics
  - student management
  - physical assessment
  - exercise selection and plan builder
  - messaging

Why it matters:

- the prototypes are the only executable artifacts in the repo, but they are static documents rather than a composable application

#### Repository Wiki

Files:

- [`wiki/README.md`](wiki/README.md)
- [`wiki/01-Repository-Overview.md`](wiki/01-Repository-Overview.md)
- [`wiki/02-Intended-Architecture.md`](wiki/02-Intended-Architecture.md)
- [`wiki/03-Data-Model-and-Security.md`](wiki/03-Data-Model-and-Security.md)
- [`wiki/04-UI-Prototypes-and-Design-System.md`](wiki/04-UI-Prototypes-and-Design-System.md)
- [`wiki/05-Key-APIs-and-Functions.md`](wiki/05-Key-APIs-and-Functions.md)
- [`wiki/06-Running-and-Viewing.md`](wiki/06-Running-and-Viewing.md)

Responsibility:

- explain the archive in topic-specific pages
- summarize the planned architecture and data model
- provide viewing instructions for the prototypes

### Planned Runtime Modules

These modules are not implemented as source folders yet, but they are clearly defined by the specification.

#### Auth and Role Management

Responsibility:

- authenticate users with Supabase Auth
- separate student and trainer access
- inject role metadata into JWTs
- enforce route-level access rules

Dependencies:

- `profiles`
- JWT access token hook
- route middleware

#### Trainer-Led Student Onboarding

Responsibility:

- capture the physical assessment
- compute body-composition metrics
- classify somatotype
- generate the student's training orientation
- create or invite the student account through a privileged server route

Dependencies:

- `physical_assessments`
- `trainer_students`
- `profiles`
- Supabase Admin API
- rule-based calculation logic

#### Training Plan Management

Responsibility:

- manage exercises
- create plans
- organize days and ordered exercises
- assign plans to students

Dependencies:

- `exercises`
- `training_plans`
- `plan_days`
- `day_exercises`

#### Workout Execution and Offline Sync

Responsibility:

- present workout guidance
- log performed sets
- persist progress while offline
- store writes in an outbox
- synchronize events later with idempotent keys

Dependencies:

- `workout_sessions`
- `session_sets`
- IndexedDB via `idb`
- service worker and background sync
- `POST /api/sync/workout-events`

#### Messaging and Realtime

Responsibility:

- support trainer-student and group conversations
- receive messages in realtime
- keep client state in sync with database inserts

Dependencies:

- `conversations`
- `conversation_members`
- `messages`
- Supabase Realtime

#### Push Notifications

Responsibility:

- subscribe the browser to push
- persist device subscriptions
- send notifications for new messages, reminders, and plan updates

Dependencies:

- service worker registration
- Push API
- `push_subscriptions`
- `web-push`

#### PWA Shell

Responsibility:

- installable mobile experience
- runtime caching
- background sync integration
- better offline resilience

Dependencies:

- Vite PWA plugin / Workbox
- service worker
- static asset caching strategy

## Key Files to Read First

If someone needs to understand the repository quickly, these files give the highest return:

1. [`stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md`](stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md)
2. [`stitch_modern_application_suite/high_performance_athletic/DESIGN.md`](stitch_modern_application_suite/high_performance_athletic/DESIGN.md)
3. [`stitch_modern_application_suite/dashboard_do_aluno/code.html`](stitch_modern_application_suite/dashboard_do_aluno/code.html)
4. [`stitch_modern_application_suite/player_de_treino/code.html`](stitch_modern_application_suite/player_de_treino/code.html)
5. [`stitch_modern_application_suite/dashboard_do_personal/code.html`](stitch_modern_application_suite/dashboard_do_personal/code.html)
6. [`stitch_modern_application_suite/nova_avalia_o_f_sica/code.html`](stitch_modern_application_suite/nova_avalia_o_f_sica/code.html)

## Key Classes and Functions

### Important Note

There are no implemented application classes in this repository.

There is no:

- React component tree
- service layer
- model layer
- controller layer
- reusable library package
- backend route source

The most meaningful symbols to document are therefore:

1. planned functions and contracts described in the spec
2. inline JavaScript functions embedded in a few prototype HTML files

### Planned Functions and Contracts from the Spec

#### `POST /api/auth/new-student`

Purpose:

- trainer-only onboarding endpoint
- creates or invites the student
- saves assessment data
- computes body metrics and training orientation

Why it matters:

- it encodes the central business rule of the product: students do not self-register

#### `POST /api/sync/workout-events`

Purpose:

- receives offline workout events from the outbox
- upserts sessions and sets using client-generated UUIDs
- guarantees idempotent sync behavior

#### `POST /api/push/subscribe`

Purpose:

- accepts Push API subscriptions from the client
- stores them in `push_subscriptions`

#### `POST /api/push/send`

Purpose:

- sends browser push notifications using VAPID credentials

#### `syncOutbox()`

Purpose:

- reads pending IndexedDB events
- batches and submits them to the workout sync endpoint
- retries failures with backoff

#### `subscribePush()`

Purpose:

- registers the service worker
- requests a push subscription
- submits the subscription to the backend

#### `useChat(...)`

Purpose:

- subscribes to realtime message inserts
- appends new messages to local state
- cleans up the channel when no longer needed

#### `custom_access_token_hook(event jsonb)`

Purpose:

- reads the user role from `profiles`
- injects `user_role` into JWT app metadata

Why it matters:

- it removes the need for route middleware to query the database for authorization context

#### `TrainingOrientation`

Purpose:

- defines the structured output of the training-orientation rule engine
- holds somatotype, summary, goal, focus, nutrition note, highlights, and trainer notes

### Prototype-Level Functions Present in the Repository

The prototype code mostly focuses on layout, but a few screens include lightweight interaction logic.

#### Assessment preview functions

Files:

- [`stitch_modern_application_suite/nova_avalia_o_f_sica/code.html`](stitch_modern_application_suite/nova_avalia_o_f_sica/code.html)
- [`stitch_modern_application_suite/formul_rio_de_avalia_o_f_sica_profissional/code.html`](stitch_modern_application_suite/formul_rio_de_avalia_o_f_sica_profissional/code.html)

Key functions:

- `updateResults()`
  - recomputes preview BMI, body-fat estimate, and somatotype label from form inputs
  - updates the result panel and status text
  - acts as a prototype approximation of the future assessment calculation engine

- `bindInputShells()`
  - toggles active-state styling around focused inputs

- professional assessment preview updater
  - mirrors the same logic in the more polished trainer form variant

Why they matter:

- these are the clearest concrete examples of domain logic currently present in the repository

#### Animated profile counters

File:

- [`stitch_modern_application_suite/perfil_do_aluno_animated/code.html`](stitch_modern_application_suite/perfil_do_aluno_animated/code.html)

Key function:

- `animateValue(obj, start, end, duration)`
  - uses `requestAnimationFrame` to count values upward
  - respects `prefers-reduced-motion`

Why it matters:

- it shows how performance metrics are intended to feel dynamic in the student profile experience

#### Trainer dashboard background effect

File:

- [`stitch_modern_application_suite/dashboard_do_personal/code.html`](stitch_modern_application_suite/dashboard_do_personal/code.html)

Key function:

- `createSpotlight()`
  - creates a decorative radial glow in the background

Why it matters:

- it is a pure presentation helper and demonstrates that most prototype scripting is cosmetic rather than architectural

#### Student detail tab switcher

File:

- [`stitch_modern_application_suite/detalhe_do_aluno_coach_1/code.html`](stitch_modern_application_suite/detalhe_do_aluno_coach_1/code.html)

Key function:

- `switchTab(tabName)`
  - toggles the visual selected state of tab buttons
  - dims or re-enables the workout tab content in the prototype

Why it matters:

- it demonstrates local state behavior for trainer-side student inspection screens

#### Timer modal controls

File:

- [`stitch_modern_application_suite/cron_metros_de_performance/code.html`](stitch_modern_application_suite/cron_metros_de_performance/code.html)

Key functions:

- `openModal(type, trigger)`
  - opens the timer modal and applies focus management

- `closeModal()`
  - closes the modal and restores focus

- `startTimer()`
  - simulates protocol start behavior and temporary visual feedback

Why they matter:

- these are the best examples of accessible interaction handling in the prototype set

## Dependency Relationships

### Current Concrete Dependencies

Each prototype screen usually depends on:

- Tailwind from CDN
- Google Fonts
- Material Symbols
- locally embedded `tailwind.config`
- local HTML and CSS
- remote image assets

This means the current prototype architecture looks like:

```text
DESIGN.md
   |
   +--> copied token ideas into each code.html
   |
code.html
   +--> Tailwind CDN
   +--> Google Fonts
   +--> Material Symbols
   +--> remote images
```

Important implication:

- the screens share visual conventions, but they do not share code

### Planned Dependency Graph

The intended application has a much stronger dependency structure:

```text
Auth and role context
   |
   +--> route protection
   +--> trainer onboarding
   +--> chat authorization
   +--> plan visibility

Physical assessment
   |
   +--> body-composition calculations
   +--> somatotype classification
   +--> training-orientation generation
   +--> student account creation

Training plans
   |
   +--> student dashboard
   +--> workout player
   +--> workout sync

Offline outbox
   |
   +--> workout logging reliability
   +--> background sync
   +--> idempotent server reconciliation

Realtime messaging
   |
   +--> chat screens
   +--> push notification suppression logic
```

## Data Model Summary

The specification defines the future backend as Supabase Postgres with RLS.

Core table groups:

- **Identity**
  - `profiles`
  - `trainer_students`

- **Assessment**
  - `physical_assessments`

- **Training library and plans**
  - `exercises`
  - `training_plans`
  - `plan_days`
  - `day_exercises`

- **Workout execution**
  - `workout_sessions`
  - `session_sets`

- **Messaging**
  - `conversations`
  - `conversation_members`
  - `messages`

- **Notifications**
  - `push_subscriptions`

High-level relationships:

```text
profiles
  +--> trainer_students
  +--> physical_assessments
  +--> training_plans
  +--> conversations
  +--> messages
  `--> push_subscriptions

training_plans
  `--> plan_days
        `--> day_exercises
              `--> exercises

workout_sessions
  `--> session_sets
```

## Running the Repository

### What You Can Run Today

This repository does not contain a runnable app build.

There is no install, build, or test pipeline because the repo is an archive of static assets and documentation.

You can view the prototypes in two ways:

### Option 1: Open a file directly

Open any of these in a browser:

- [`stitch_modern_application_suite/login_do_aluno/code.html`](stitch_modern_application_suite/login_do_aluno/code.html)
- [`stitch_modern_application_suite/dashboard_do_aluno/code.html`](stitch_modern_application_suite/dashboard_do_aluno/code.html)
- [`stitch_modern_application_suite/player_de_treino/code.html`](stitch_modern_application_suite/player_de_treino/code.html)
- [`stitch_modern_application_suite/dashboard_do_personal/code.html`](stitch_modern_application_suite/dashboard_do_personal/code.html)

### Option 2: Serve the archive as static files

```bash
cd /workspace/stitch_modern_application_suite
python3 -m http.server 8000
```

Then open URLs such as:

- `http://localhost:8000/login_do_aluno/code.html`
- `http://localhost:8000/dashboard_do_aluno/code.html`
- `http://localhost:8000/player_de_treino/code.html`

### What Is Required for Correct Prototype Rendering

The screens rely on external network resources:

- Tailwind CDN
- Google Fonts
- Material Symbols
- remote images

Without internet access, the pages may render with missing styles, fonts, or media.

### Planned Future Runtime Environment

The specification expects a future implementation to use:

- React + Vite
- TanStack Router
- Tailwind + shadcn/ui
- Supabase
- IndexedDB via `idb`
- Workbox or Vite PWA plugin
- Zustand
- `web-push`

Planned environment variables:

```env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
NEXT_PUBLIC_VAPID_PUBLIC_KEY=
VAPID_PRIVATE_KEY=
VAPID_SUBJECT=mailto:you@example.com
```

## Implementation Gaps

If this repository is later converted into a real application, the following pieces still need to be created:

- frontend app scaffold
- shared component system
- routing and auth guards
- database migrations
- RLS policies in executable migration files
- server API route implementations
- offline storage layer
- service worker
- tests
- deployment configuration

## Recommended Reading Order

For developers or reviewers entering this repository for the first time:

1. Read the master spec to understand product scope and architecture.
2. Read the design system to understand the visual language.
3. Open the student dashboard, workout player, trainer dashboard, and assessment prototypes.
4. Read the `wiki/` pages for focused breakdowns by architecture, data model, and runtime plan.

## Related Documentation

The repository also includes topic-specific wiki pages:

- [`wiki/01-Repository-Overview.md`](wiki/01-Repository-Overview.md)
- [`wiki/02-Intended-Architecture.md`](wiki/02-Intended-Architecture.md)
- [`wiki/03-Data-Model-and-Security.md`](wiki/03-Data-Model-and-Security.md)
- [`wiki/04-UI-Prototypes-and-Design-System.md`](wiki/04-UI-Prototypes-and-Design-System.md)
- [`wiki/05-Key-APIs-and-Functions.md`](wiki/05-Key-APIs-and-Functions.md)
- [`wiki/06-Running-and-Viewing.md`](wiki/06-Running-and-Viewing.md)

## Bottom Line

TrainFlow's repository is currently a high-quality reference archive rather than an implemented software project. Its true architecture lives in the specification, its UX lives in the prototype screens, and its design language lives in `DESIGN.md`. Any engineering effort built from this repository should treat the spec as the system contract and the HTML screens as visual guidance rather than production-ready frontend code.
