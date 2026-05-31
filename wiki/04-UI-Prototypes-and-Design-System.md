# 04 — UI Prototypes & Design System

This repository's main concrete artifacts are the standalone HTML prototypes under [stitch_modern_application_suite/](file:///workspace/stitch_modern_application_suite).

## Prototype Structure

Each screen lives in its own directory and usually contains:

- `code.html` — the standalone prototype
- `screen.png` — a preview image

Example directories:

- Student login: [login_do_aluno/](file:///workspace/stitch_modern_application_suite/login_do_aluno)
- Student dashboard: [dashboard_do_aluno/](file:///workspace/stitch_modern_application_suite/dashboard_do_aluno)
- Workout player: [player_de_treino/](file:///workspace/stitch_modern_application_suite/player_de_treino)
- Trainer dashboard: [dashboard_do_personal/](file:///workspace/stitch_modern_application_suite/dashboard_do_personal)
- Trainer plan builder: [builder_de_plano_de_treino/](file:///workspace/stitch_modern_application_suite/builder_de_plano_de_treino)

## Screen Families

The screens cluster into product areas that mirror the planned architecture.

### Student-facing screens

- Login and onboarding
  - `login_do_aluno`
  - `boas_vindas_do_aluno`
  - `boas_vindas_e_somat_tipo_onboarding`
- Home and profile
  - `dashboard_do_aluno`
  - `perfil_do_aluno`
- Workout execution
  - `player_de_treino`
  - `player_de_treino_dark_mode_1`
  - `player_de_treino_dark_mode_2`
  - `player_de_treino_modo_foco_total`
  - `timer_tabata_ativo`
- Progress and history
  - `hist_rico_de_avalia_es_do_aluno`
  - `hist_rico_de_avalia_es_com_gr_ficos`
  - `hist_rico_com_gr_fico_de_peso_total`
  - `hist_rico_com_todos_os_gr_ficos_corporais`
- Community and habits
  - `comunidade_e_conquistas`
  - `di_rio_de_h_bitos_saud_veis`

### Trainer-facing screens

- Dashboards and insights
  - `dashboard_do_personal`
  - `insights_de_performance_e_reten_o_coach`
  - `relat_rios_avan_ados_trainer`
- Student management
  - `gest_o_de_alunos_trainer`
  - `lista_de_alunos`
  - `detalhe_do_aluno_coach_1`
  - `detalhe_do_aluno_coach_2`
- Assessment
  - `nova_avalia_o_f_sica`
  - `formul_rio_de_avalia_o_f_sica_profissional`
- Exercise and plan management
  - `biblioteca_de_exerc_cios`
  - `selecionar_exerc_cio`
  - `builder_de_plano_de_treino`
  - `builder_de_plano_de_treino_profissional`
  - `builder_de_treino_com_imagens_reais`
- Messaging
  - `mensagens_do_personal`
  - `mensagens_do_personal_conversa`

## Shared Implementation Pattern

The prototypes are self-contained static documents rather than composable components. Typical dependencies inside a screen:

- Tailwind CDN script
- Google Fonts
- Material Symbols icon font
- Embedded `tailwind.config`
- Embedded CSS rules
- Static HTML markup

Representative files:

- Student dashboard: [dashboard_do_aluno/code.html](file:///workspace/stitch_modern_application_suite/dashboard_do_aluno/code.html)
- Workout player: [player_de_treino/code.html](file:///workspace/stitch_modern_application_suite/player_de_treino/code.html)

## Design System

The shared visual language is documented in [DESIGN.md](file:///workspace/stitch_modern_application_suite/high_performance_athletic/DESIGN.md).

### Key tokens and rules

- Base palette:
  - pure black / dark surfaces
  - electric lime for primary actions and progress
  - off-white/silver for readable body text
- Typography:
  - `Bebas Neue` for display/headlines
  - `Inter` for body, labels, inputs
- Shapes:
  - rounded cards
  - pill-shaped primary buttons
- Depth:
  - glassmorphism panels
  - lime glow on active elements

Reference: [DESIGN.md:L123-L188](file:///workspace/stitch_modern_application_suite/high_performance_athletic/DESIGN.md#L123-L188)

## Prototype Responsibilities by Screen Type

Even though these are static screens, they communicate intended responsibilities for future implementation:

- Login screens define entry into the student and trainer journeys
- Welcome/onboarding screens show somatotype and generated orientation
- Dashboard screens summarize current plan, progress, and messaging previews
- Workout-player screens define the core logging interaction, rest timer, and offline status UX
- Assessment screens define the trainer data-entry flow that drives onboarding
- Builder screens define exercise search, plan composition, ordering, and publishing
- Chat screens define conversation list/detail layouts for realtime messaging

## Quality Caveats

The audit report in [trainflow-ui-audit-report.md](file:///workspace/.trae/documents/trainflow-ui-audit-report.md) shows the prototypes are visually coherent but not yet production-grade UI code. Repeated issues include:

- missing visible focus styles
- non-semantic interactive elements
- missing labels / metadata on form controls
- missing image dimensions
- motion without reduced-motion fallbacks

This matters because the prototypes are useful as UX references, but should not be treated as directly shippable frontend code.
