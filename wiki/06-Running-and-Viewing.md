# 06 — Running / Viewing This Repo

## Current State

This repository does **not** contain a runnable application.

What is present:

- standalone HTML prototypes
- design documentation
- a product/master spec

What is not present:

- `package.json`
- `pyproject.toml`
- `go.mod`
- `Cargo.toml`
- frontend build config
- backend service source
- test runner config

Because of that:

- there is no `npm install`
- there is no `npm run dev`
- there is no build command
- there is no automated test command

## How to View the Prototype Screens

The HTML screens can be opened directly in a browser from their file paths, for example:

- [login_do_aluno/code.html](file:///workspace/stitch_modern_application_suite/login_do_aluno/code.html)
- [dashboard_do_aluno/code.html](file:///workspace/stitch_modern_application_suite/dashboard_do_aluno/code.html)
- [player_de_treino/code.html](file:///workspace/stitch_modern_application_suite/player_de_treino/code.html)
- [builder_de_plano_de_treino/code.html](file:///workspace/stitch_modern_application_suite/builder_de_plano_de_treino/code.html)

You can also serve the folder with any static file server if you prefer browser-like URL routing.

Example with Python:

```bash
cd /workspace/stitch_modern_application_suite
python3 -m http.server 8000
```

Then open:

- `http://localhost:8000/login_do_aluno/code.html`
- `http://localhost:8000/dashboard_do_aluno/code.html`
- `http://localhost:8000/player_de_treino/code.html`

## External Assets Required by the Prototypes

Many screens depend on network-hosted assets:

- Tailwind CDN
- Google Fonts
- Material Symbols
- remote image assets

If opened without internet access, visual styling and images may degrade.

Representative dependency usage:

- [dashboard_do_aluno/code.html:L7-L10](file:///workspace/stitch_modern_application_suite/dashboard_do_aluno/code.html#L7-L10)
- [player_de_treino/code.html:L7-L10](file:///workspace/stitch_modern_application_suite/player_de_treino/code.html#L7-L10)

## Planned Run/Build Environment (From the Spec)

Although not implemented here, the spec expects a future application to use:

- React + Vite SPA
- TanStack Router
- Tailwind + shadcn/ui
- Supabase backend
- PWA plugin / Service Worker support

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L14-L33](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L14-L33)

## Planned Environment Variables

The specification defines the following environment variables for a future implementation:

```env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
NEXT_PUBLIC_VAPID_PUBLIC_KEY=
VAPID_PRIVATE_KEY=
VAPID_SUBJECT=mailto:seuemail@dominio.com
```

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L730-L739](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L730-L739)

## If You Want to Convert This Repo Into a Real App

The spec includes an implementation order that effectively acts as a bootstrap roadmap:

1. Create SQL schema, migrations, RLS, and JWT hook
2. Create Supabase server/client adapters
3. Implement route middleware
4. Build assessment form + calculation logic
5. Implement `POST /api/auth/new-student`
6. Build login and welcome flows
7. Build student home
8. Build workout player
9. Build exercise library and plan builder
10. Build chat, profile/history, PWA, and push

Reference: [trainflow_especifica_o_mestre_do_produto_1.md:L767-L784](file:///workspace/stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md#L767-L784)
