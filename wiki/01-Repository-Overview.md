# 01 — Repository Overview

## Purpose of This Repository

This repository is an artifact bundle for a product called **TrainFlow**:

- **Product spec**: defines the target architecture, database schema, offline strategy, push, realtime, routing, and core flows.
- **UI prototypes**: 42 standalone HTML screens representing product flows for both student and trainer roles.
- **Design system**: tokens and guidelines used by the prototypes.

There is **no application source code** in the typical sense (no `src/`, no package manifests like `package.json`, no backend server, no tests). The authoritative “source of truth” is the specification document.

## Top-Level Structure

- Root placeholder: [README.md](file:///workspace/README.md)
- Main archive folder: [stitch_modern_application_suite/](file:///workspace/stitch_modern_application_suite)
  - UI screens (42 total): `stitch_modern_application_suite/*/code.html`
  - Per-screen preview images: `stitch_modern_application_suite/*/screen.png`
  - Design tokens/guidelines: [high_performance_athletic/DESIGN.md](file:///workspace/stitch_modern_application_suite/high_performance_athletic/DESIGN.md)
  - Master specification: [trainflow_especifica_o_mestre_do_produto_1.md](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md)
- Meta documents (generated as part of prior work in this workspace):
  - UI audit plan: [trainflow-ui-audit-plan.md](file:///workspace/.trae/documents/trainflow-ui-audit-plan.md)
  - UI audit report: [trainflow-ui-audit-report.md](file:///workspace/.trae/documents/trainflow-ui-audit-report.md)

## “Modules” in This Repo

Because the repo is not an implemented app, “modules” fall into two categories:

1. **Specification modules (intended system)** — described in the spec as subsystems (Auth, Offline, Realtime Chat, PWA, etc.). These are documented in [02 — Intended Architecture](02-Intended-Architecture.md).
2. **Prototype screen modules (current artifacts)** — each folder under `stitch_modern_application_suite/` is a standalone screen. These are documented in [04 — UI Prototypes & Design System](04-UI-Prototypes-and-Design-System.md).

## Current Implementation Style (Prototypes)

Most screens follow the same pattern:

- Tailwind via CDN: `https://cdn.tailwindcss.com?...`
- Google Fonts: Bebas Neue + Inter
- Material Symbols (icons)
- A per-page embedded Tailwind theme extension that duplicates the design tokens

Example prototype files:

- Student dashboard: [dashboard_do_aluno/code.html](file:///workspace/stitch_modern_application_suite/dashboard_do_aluno/code.html)
- Workout player: [player_de_treino/code.html](file:///workspace/stitch_modern_application_suite/player_de_treino/code.html)
- Trainer plan builder: [builder_de_plano_de_treino/code.html](file:///workspace/stitch_modern_application_suite/builder_de_plano_de_treino/code.html)

## What’s Missing (If You’re Expecting an App)

- No dependency manifests (no Node/Python/Go/Rust project definition)
- No runnable frontend app scaffold (no router implementation, no build step)
- No backend endpoints implementation
- No database migrations in the described `supabase/migrations/` path (only SQL embedded in the spec)

The spec does provide a recommended stack and module boundaries, which can be used to build a real implementation.
