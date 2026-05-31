# TrainFlow UI Audit Report

## Scope

- Audited `42` standalone HTML screens under `stitch_modern_application_suite/**/code.html`.
- Rubric: Vercel Web Interface Guidelines fetched during the review.
- Constraint: preserve the existing TrainFlow visual direction; findings focus on compliance, semantics, accessibility, interaction, and performance risk.

## Screen Inventory

- Student-oriented screens: `22`
- Trainer-oriented screens: `19`
- Shared/mixed screens: `1`
- Reference-only screens: `0`

## Recurring Patterns

- `button focus missing`: `194` findings
- `transition-all`: `110` findings
- `images missing dimensions`: `88` findings
- `non-semantic interactive`: `80` findings
- `icon button missing label`: `79` findings
- `form name missing`: `68` findings
- `autocomplete missing`: `62` findings
- `missing skip link`: `42` findings
- `missing focus-visible`: `42` findings
- `touch-action missing`: `42` findings
- `reduced-motion missing`: `41` findings
- `icon span interactive`: `18` findings

## Rollout Order

- Fix non-semantic interactive elements and icon controls first; they block keyboard and screen-reader access across navigation, cards, and media controls.
- Fix form labeling, `name`, `autocomplete`, and email metadata next; these affect login, chat, search, plan-builder, and assessment flows.
- Add explicit image dimensions and motion fallbacks after that; these improve stability and accessibility without changing the visual design.
- Replace `transition-all` and add consistent `focus-visible` treatment as a final sweep across the suite.

## Findings By File

## biblioteca_de_exerc_cios/code.html
biblioteca_de_exerc_cios/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
biblioteca_de_exerc_cios/code.html:1 - missing skip link for main content
biblioteca_de_exerc_cios/code.html:1 - motion present without `prefers-reduced-motion` fallback
biblioteca_de_exerc_cios/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
biblioteca_de_exerc_cios/code.html:140 - interactive icon span needs button semantics and accessible name
biblioteca_de_exerc_cios/code.html:140 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
biblioteca_de_exerc_cios/code.html:144 - interactive icon span needs button semantics and accessible name
biblioteca_de_exerc_cios/code.html:144 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`

## boas_vindas_do_aluno/code.html
boas_vindas_do_aluno/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
boas_vindas_do_aluno/code.html:1 - missing skip link for main content
boas_vindas_do_aluno/code.html:1 - motion present without `prefers-reduced-motion` fallback
boas_vindas_do_aluno/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
boas_vindas_do_aluno/code.html:135 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
boas_vindas_do_aluno/code.html:141 - button lacks explicit visible focus styling
boas_vindas_do_aluno/code.html:235 - button lacks explicit visible focus styling
boas_vindas_do_aluno/code.html:235 - `transition: all`/`transition-all` used; list explicit properties

## boas_vindas_do_aluno_animated/code.html
boas_vindas_do_aluno_animated/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
boas_vindas_do_aluno_animated/code.html:1 - missing skip link for main content
boas_vindas_do_aluno_animated/code.html:1 - motion present without `prefers-reduced-motion` fallback
boas_vindas_do_aluno_animated/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
boas_vindas_do_aluno_animated/code.html:185 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
boas_vindas_do_aluno_animated/code.html:191 - button lacks explicit visible focus styling
boas_vindas_do_aluno_animated/code.html:285 - button lacks explicit visible focus styling
boas_vindas_do_aluno_animated/code.html:285 - `transition: all`/`transition-all` used; list explicit properties

## boas_vindas_do_aluno_dark_mode/code.html
boas_vindas_do_aluno_dark_mode/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
boas_vindas_do_aluno_dark_mode/code.html:1 - missing skip link for main content
boas_vindas_do_aluno_dark_mode/code.html:1 - motion present without `prefers-reduced-motion` fallback
boas_vindas_do_aluno_dark_mode/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
boas_vindas_do_aluno_dark_mode/code.html:132 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
boas_vindas_do_aluno_dark_mode/code.html:138 - button lacks explicit visible focus styling
boas_vindas_do_aluno_dark_mode/code.html:232 - button lacks explicit visible focus styling
boas_vindas_do_aluno_dark_mode/code.html:232 - `transition: all`/`transition-all` used; list explicit properties

## boas_vindas_e_somat_tipo_onboarding/code.html
boas_vindas_e_somat_tipo_onboarding/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
boas_vindas_e_somat_tipo_onboarding/code.html:1 - missing skip link for main content
boas_vindas_e_somat_tipo_onboarding/code.html:1 - motion present without `prefers-reduced-motion` fallback
boas_vindas_e_somat_tipo_onboarding/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
boas_vindas_e_somat_tipo_onboarding/code.html:139 - interactive icon span needs button semantics and accessible name
boas_vindas_e_somat_tipo_onboarding/code.html:139 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
boas_vindas_e_somat_tipo_onboarding/code.html:141 - `<img>` missing explicit `width` and `height`
boas_vindas_e_somat_tipo_onboarding/code.html:159 - `<img>` missing explicit `width` and `height`

## builder_de_plano_de_treino/code.html
builder_de_plano_de_treino/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
builder_de_plano_de_treino/code.html:1 - missing skip link for main content
builder_de_plano_de_treino/code.html:1 - motion present without `prefers-reduced-motion` fallback
builder_de_plano_de_treino/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
builder_de_plano_de_treino/code.html:128 - button lacks explicit visible focus styling
builder_de_plano_de_treino/code.html:137 - input missing `autocomplete` metadata
builder_de_plano_de_treino/code.html:137 - `...` should use the ellipsis character `…`
builder_de_plano_de_treino/code.html:137 - form control missing meaningful `name`

## builder_de_plano_de_treino_profissional/code.html
builder_de_plano_de_treino_profissional/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
builder_de_plano_de_treino_profissional/code.html:1 - missing skip link for main content
builder_de_plano_de_treino_profissional/code.html:1 - motion present without `prefers-reduced-motion` fallback
builder_de_plano_de_treino_profissional/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
builder_de_plano_de_treino_profissional/code.html:125 - button lacks explicit visible focus styling
builder_de_plano_de_treino_profissional/code.html:125 - `transition: all`/`transition-all` used; list explicit properties
builder_de_plano_de_treino_profissional/code.html:134 - input missing `autocomplete` metadata
builder_de_plano_de_treino_profissional/code.html:134 - `...` should use the ellipsis character `…`

## builder_de_treino_com_imagens_reais/code.html
builder_de_treino_com_imagens_reais/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
builder_de_treino_com_imagens_reais/code.html:1 - missing skip link for main content
builder_de_treino_com_imagens_reais/code.html:1 - motion present without `prefers-reduced-motion` fallback
builder_de_treino_com_imagens_reais/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
builder_de_treino_com_imagens_reais/code.html:128 - button lacks explicit visible focus styling
builder_de_treino_com_imagens_reais/code.html:137 - input missing `autocomplete` metadata
builder_de_treino_com_imagens_reais/code.html:137 - `...` should use the ellipsis character `…`
builder_de_treino_com_imagens_reais/code.html:137 - form control missing meaningful `name`

## comunidade_e_conquistas/code.html
comunidade_e_conquistas/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
comunidade_e_conquistas/code.html:1 - missing skip link for main content
comunidade_e_conquistas/code.html:1 - motion present without `prefers-reduced-motion` fallback
comunidade_e_conquistas/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
comunidade_e_conquistas/code.html:128 - `<img>` missing explicit `width` and `height`
comunidade_e_conquistas/code.html:132 - button lacks explicit visible focus styling
comunidade_e_conquistas/code.html:132 - icon-only button missing `aria-label`
comunidade_e_conquistas/code.html:193 - button lacks explicit visible focus styling

## cron_metros_de_performance/code.html
cron_metros_de_performance/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
cron_metros_de_performance/code.html:1 - missing skip link for main content
cron_metros_de_performance/code.html:1 - motion present without `prefers-reduced-motion` fallback
cron_metros_de_performance/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
cron_metros_de_performance/code.html:133 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
cron_metros_de_performance/code.html:134 - `<img>` missing explicit `width` and `height`
cron_metros_de_performance/code.html:138 - button lacks explicit visible focus styling
cron_metros_de_performance/code.html:138 - icon-only button missing `aria-label`

## dashboard_do_aluno/code.html
dashboard_do_aluno/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
dashboard_do_aluno/code.html:1 - missing skip link for main content
dashboard_do_aluno/code.html:1 - motion present without `prefers-reduced-motion` fallback
dashboard_do_aluno/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
dashboard_do_aluno/code.html:131 - `<img>` missing explicit `width` and `height`
dashboard_do_aluno/code.html:136 - button lacks explicit visible focus styling
dashboard_do_aluno/code.html:136 - icon-only button missing `aria-label`
dashboard_do_aluno/code.html:173 - button lacks explicit visible focus styling

## dashboard_do_aluno_dark_mode/code.html
dashboard_do_aluno_dark_mode/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
dashboard_do_aluno_dark_mode/code.html:1 - missing skip link for main content
dashboard_do_aluno_dark_mode/code.html:1 - motion present without `prefers-reduced-motion` fallback
dashboard_do_aluno_dark_mode/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
dashboard_do_aluno_dark_mode/code.html:127 - `<img>` missing explicit `width` and `height`
dashboard_do_aluno_dark_mode/code.html:131 - button lacks explicit visible focus styling
dashboard_do_aluno_dark_mode/code.html:131 - icon-only button missing `aria-label`
dashboard_do_aluno_dark_mode/code.html:168 - button lacks explicit visible focus styling

## dashboard_do_personal/code.html
dashboard_do_personal/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
dashboard_do_personal/code.html:1 - missing skip link for main content
dashboard_do_personal/code.html:1 - motion present without `prefers-reduced-motion` fallback
dashboard_do_personal/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
dashboard_do_personal/code.html:142 - button lacks explicit visible focus styling
dashboard_do_personal/code.html:142 - icon-only button missing `aria-label`
dashboard_do_personal/code.html:146 - `<img>` missing explicit `width` and `height`
dashboard_do_personal/code.html:158 - button lacks explicit visible focus styling

## dashboard_do_personal_animated/code.html
dashboard_do_personal_animated/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
dashboard_do_personal_animated/code.html:1 - missing skip link for main content
dashboard_do_personal_animated/code.html:1 - motion present without `prefers-reduced-motion` fallback
dashboard_do_personal_animated/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
dashboard_do_personal_animated/code.html:200 - button lacks explicit visible focus styling
dashboard_do_personal_animated/code.html:200 - icon-only button missing `aria-label`
dashboard_do_personal_animated/code.html:203 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
dashboard_do_personal_animated/code.html:204 - `<img>` missing explicit `width` and `height`

## detalhe_do_aluno_coach_1/code.html
detalhe_do_aluno_coach_1/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
detalhe_do_aluno_coach_1/code.html:1 - missing skip link for main content
detalhe_do_aluno_coach_1/code.html:1 - motion present without `prefers-reduced-motion` fallback
detalhe_do_aluno_coach_1/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
detalhe_do_aluno_coach_1/code.html:146 - button lacks explicit visible focus styling
detalhe_do_aluno_coach_1/code.html:146 - icon-only button missing `aria-label`
detalhe_do_aluno_coach_1/code.html:152 - `<img>` missing explicit `width` and `height`
detalhe_do_aluno_coach_1/code.html:161 - `<img>` missing explicit `width` and `height`

## detalhe_do_aluno_coach_2/code.html
detalhe_do_aluno_coach_2/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
detalhe_do_aluno_coach_2/code.html:1 - missing skip link for main content
detalhe_do_aluno_coach_2/code.html:1 - motion present without `prefers-reduced-motion` fallback
detalhe_do_aluno_coach_2/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
detalhe_do_aluno_coach_2/code.html:132 - button lacks explicit visible focus styling
detalhe_do_aluno_coach_2/code.html:132 - icon-only button missing `aria-label`
detalhe_do_aluno_coach_2/code.html:138 - `<img>` missing explicit `width` and `height`
detalhe_do_aluno_coach_2/code.html:147 - `<img>` missing explicit `width` and `height`

## di_rio_de_h_bitos_saud_veis/code.html
di_rio_de_h_bitos_saud_veis/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
di_rio_de_h_bitos_saud_veis/code.html:1 - missing skip link for main content
di_rio_de_h_bitos_saud_veis/code.html:1 - motion present without `prefers-reduced-motion` fallback
di_rio_de_h_bitos_saud_veis/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
di_rio_de_h_bitos_saud_veis/code.html:169 - `<img>` missing explicit `width` and `height`
di_rio_de_h_bitos_saud_veis/code.html:173 - button lacks explicit visible focus styling
di_rio_de_h_bitos_saud_veis/code.html:173 - icon-only button missing `aria-label`
di_rio_de_h_bitos_saud_veis/code.html:196 - `transition: all`/`transition-all` used; list explicit properties

## formul_rio_de_avalia_o_f_sica_profissional/code.html
formul_rio_de_avalia_o_f_sica_profissional/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
formul_rio_de_avalia_o_f_sica_profissional/code.html:1 - missing skip link for main content
formul_rio_de_avalia_o_f_sica_profissional/code.html:1 - motion present without `prefers-reduced-motion` fallback
formul_rio_de_avalia_o_f_sica_profissional/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
formul_rio_de_avalia_o_f_sica_profissional/code.html:144 - `<img>` missing explicit `width` and `height`
formul_rio_de_avalia_o_f_sica_profissional/code.html:153 - input missing `autocomplete` metadata
formul_rio_de_avalia_o_f_sica_profissional/code.html:153 - form control missing meaningful `name`
formul_rio_de_avalia_o_f_sica_profissional/code.html:155 - input missing `autocomplete` metadata

## gest_o_de_alunos_trainer/code.html
gest_o_de_alunos_trainer/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
gest_o_de_alunos_trainer/code.html:1 - missing skip link for main content
gest_o_de_alunos_trainer/code.html:1 - motion present without `prefers-reduced-motion` fallback
gest_o_de_alunos_trainer/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
gest_o_de_alunos_trainer/code.html:141 - button lacks explicit visible focus styling
gest_o_de_alunos_trainer/code.html:141 - icon-only button missing `aria-label`
gest_o_de_alunos_trainer/code.html:143 - `<img>` missing explicit `width` and `height`
gest_o_de_alunos_trainer/code.html:152 - input missing `autocomplete` metadata

## hist_rico_com_gr_fico_de_peso_total/code.html
hist_rico_com_gr_fico_de_peso_total/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
hist_rico_com_gr_fico_de_peso_total/code.html:1 - missing skip link for main content
hist_rico_com_gr_fico_de_peso_total/code.html:1 - motion present without `prefers-reduced-motion` fallback
hist_rico_com_gr_fico_de_peso_total/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
hist_rico_com_gr_fico_de_peso_total/code.html:130 - button lacks explicit visible focus styling
hist_rico_com_gr_fico_de_peso_total/code.html:130 - icon-only button missing `aria-label`
hist_rico_com_gr_fico_de_peso_total/code.html:136 - `<img>` missing explicit `width` and `height`
hist_rico_com_gr_fico_de_peso_total/code.html:288 - button lacks explicit visible focus styling

## hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:1 - missing skip link for main content
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:1 - motion present without `prefers-reduced-motion` fallback
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:130 - button lacks explicit visible focus styling
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:130 - icon-only button missing `aria-label`
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:136 - `<img>` missing explicit `width` and `height`
hist_rico_com_gr_ficos_de_per_metros_cintura_bra_o/code.html:333 - button lacks explicit visible focus styling

## hist_rico_com_metas_nos_gr_ficos/code.html
hist_rico_com_metas_nos_gr_ficos/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
hist_rico_com_metas_nos_gr_ficos/code.html:1 - missing skip link for main content
hist_rico_com_metas_nos_gr_ficos/code.html:1 - motion present without `prefers-reduced-motion` fallback
hist_rico_com_metas_nos_gr_ficos/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
hist_rico_com_metas_nos_gr_ficos/code.html:130 - button lacks explicit visible focus styling
hist_rico_com_metas_nos_gr_ficos/code.html:130 - icon-only button missing `aria-label`
hist_rico_com_metas_nos_gr_ficos/code.html:136 - `<img>` missing explicit `width` and `height`
hist_rico_com_metas_nos_gr_ficos/code.html:412 - button lacks explicit visible focus styling

## hist_rico_com_todos_os_gr_ficos_corporais/code.html
hist_rico_com_todos_os_gr_ficos_corporais/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
hist_rico_com_todos_os_gr_ficos_corporais/code.html:1 - missing skip link for main content
hist_rico_com_todos_os_gr_ficos_corporais/code.html:1 - motion present without `prefers-reduced-motion` fallback
hist_rico_com_todos_os_gr_ficos_corporais/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
hist_rico_com_todos_os_gr_ficos_corporais/code.html:130 - button lacks explicit visible focus styling
hist_rico_com_todos_os_gr_ficos_corporais/code.html:130 - icon-only button missing `aria-label`
hist_rico_com_todos_os_gr_ficos_corporais/code.html:136 - `<img>` missing explicit `width` and `height`
hist_rico_com_todos_os_gr_ficos_corporais/code.html:424 - button lacks explicit visible focus styling

## hist_rico_de_avalia_es_com_gr_ficos/code.html
hist_rico_de_avalia_es_com_gr_ficos/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
hist_rico_de_avalia_es_com_gr_ficos/code.html:1 - missing skip link for main content
hist_rico_de_avalia_es_com_gr_ficos/code.html:1 - motion present without `prefers-reduced-motion` fallback
hist_rico_de_avalia_es_com_gr_ficos/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
hist_rico_de_avalia_es_com_gr_ficos/code.html:130 - button lacks explicit visible focus styling
hist_rico_de_avalia_es_com_gr_ficos/code.html:130 - icon-only button missing `aria-label`
hist_rico_de_avalia_es_com_gr_ficos/code.html:136 - `<img>` missing explicit `width` and `height`
hist_rico_de_avalia_es_com_gr_ficos/code.html:264 - button lacks explicit visible focus styling

## hist_rico_de_avalia_es_do_aluno/code.html
hist_rico_de_avalia_es_do_aluno/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
hist_rico_de_avalia_es_do_aluno/code.html:1 - missing skip link for main content
hist_rico_de_avalia_es_do_aluno/code.html:1 - motion present without `prefers-reduced-motion` fallback
hist_rico_de_avalia_es_do_aluno/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
hist_rico_de_avalia_es_do_aluno/code.html:130 - button lacks explicit visible focus styling
hist_rico_de_avalia_es_do_aluno/code.html:130 - icon-only button missing `aria-label`
hist_rico_de_avalia_es_do_aluno/code.html:136 - `<img>` missing explicit `width` and `height`
hist_rico_de_avalia_es_do_aluno/code.html:199 - button lacks explicit visible focus styling

## insights_de_performance_e_reten_o_coach/code.html
insights_de_performance_e_reten_o_coach/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
insights_de_performance_e_reten_o_coach/code.html:1 - missing skip link for main content
insights_de_performance_e_reten_o_coach/code.html:1 - motion present without `prefers-reduced-motion` fallback
insights_de_performance_e_reten_o_coach/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
insights_de_performance_e_reten_o_coach/code.html:141 - button lacks explicit visible focus styling
insights_de_performance_e_reten_o_coach/code.html:141 - icon-only button missing `aria-label`
insights_de_performance_e_reten_o_coach/code.html:143 - `<img>` missing explicit `width` and `height`
insights_de_performance_e_reten_o_coach/code.html:215 - `transition: all`/`transition-all` used; list explicit properties

## lista_de_alunos/code.html
lista_de_alunos/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
lista_de_alunos/code.html:1 - missing skip link for main content
lista_de_alunos/code.html:1 - motion present without `prefers-reduced-motion` fallback
lista_de_alunos/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
lista_de_alunos/code.html:141 - button lacks explicit visible focus styling
lista_de_alunos/code.html:141 - icon-only button missing `aria-label`
lista_de_alunos/code.html:143 - `<img>` missing explicit `width` and `height`
lista_de_alunos/code.html:152 - input missing `autocomplete` metadata

## login_do_aluno/code.html
login_do_aluno/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
login_do_aluno/code.html:1 - missing skip link for main content
login_do_aluno/code.html:1 - motion present without `prefers-reduced-motion` fallback
login_do_aluno/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
login_do_aluno/code.html:143 - input missing `autocomplete` metadata
login_do_aluno/code.html:143 - email input should disable spellcheck
login_do_aluno/code.html:143 - form control missing meaningful `name`
login_do_aluno/code.html:143 - `transition: all`/`transition-all` used; list explicit properties

## login_do_aluno_animated/code.html
login_do_aluno_animated/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
login_do_aluno_animated/code.html:1 - missing skip link for main content
login_do_aluno_animated/code.html:1 - motion present without `prefers-reduced-motion` fallback
login_do_aluno_animated/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
login_do_aluno_animated/code.html:248 - input missing `autocomplete` metadata
login_do_aluno_animated/code.html:248 - email input should disable spellcheck
login_do_aluno_animated/code.html:248 - form control missing meaningful `name`
login_do_aluno_animated/code.html:248 - `transition: all`/`transition-all` used; list explicit properties

## login_do_aluno_dark_mode/code.html
login_do_aluno_dark_mode/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
login_do_aluno_dark_mode/code.html:1 - missing skip link for main content
login_do_aluno_dark_mode/code.html:1 - motion present without `prefers-reduced-motion` fallback
login_do_aluno_dark_mode/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
login_do_aluno_dark_mode/code.html:140 - input missing `autocomplete` metadata
login_do_aluno_dark_mode/code.html:140 - email input should disable spellcheck
login_do_aluno_dark_mode/code.html:140 - form control missing meaningful `name`
login_do_aluno_dark_mode/code.html:140 - `transition: all`/`transition-all` used; list explicit properties

## mensagens_do_personal/code.html
mensagens_do_personal/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
mensagens_do_personal/code.html:1 - missing skip link for main content
mensagens_do_personal/code.html:1 - motion present without `prefers-reduced-motion` fallback
mensagens_do_personal/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
mensagens_do_personal/code.html:144 - interactive icon span needs button semantics and accessible name
mensagens_do_personal/code.html:144 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
mensagens_do_personal/code.html:144 - click handler on non-semantic element; use `<button>` or `<a>`
mensagens_do_personal/code.html:147 - `<img>` missing explicit `width` and `height`

## mensagens_do_personal_conversa/code.html
mensagens_do_personal_conversa/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
mensagens_do_personal_conversa/code.html:1 - missing skip link for main content
mensagens_do_personal_conversa/code.html:1 - motion present without `prefers-reduced-motion` fallback
mensagens_do_personal_conversa/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
mensagens_do_personal_conversa/code.html:128 - `<img>` missing explicit `width` and `height`
mensagens_do_personal_conversa/code.html:132 - button lacks explicit visible focus styling
mensagens_do_personal_conversa/code.html:132 - icon-only button missing `aria-label`
mensagens_do_personal_conversa/code.html:143 - input missing `autocomplete` metadata

## nova_avalia_o_f_sica/code.html
nova_avalia_o_f_sica/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
nova_avalia_o_f_sica/code.html:1 - missing skip link for main content
nova_avalia_o_f_sica/code.html:1 - motion present without `prefers-reduced-motion` fallback
nova_avalia_o_f_sica/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
nova_avalia_o_f_sica/code.html:144 - `<img>` missing explicit `width` and `height`
nova_avalia_o_f_sica/code.html:164 - input missing `autocomplete` metadata
nova_avalia_o_f_sica/code.html:164 - form control missing meaningful `name`
nova_avalia_o_f_sica/code.html:164 - `transition: all`/`transition-all` used; list explicit properties

## perfil_do_aluno/code.html
perfil_do_aluno/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
perfil_do_aluno/code.html:1 - missing skip link for main content
perfil_do_aluno/code.html:1 - motion present without `prefers-reduced-motion` fallback
perfil_do_aluno/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
perfil_do_aluno/code.html:134 - `<img>` missing explicit `width` and `height`
perfil_do_aluno/code.html:138 - button lacks explicit visible focus styling
perfil_do_aluno/code.html:138 - icon-only button missing `aria-label`
perfil_do_aluno/code.html:180 - `<img>` missing explicit `width` and `height`

## perfil_do_aluno_animated/code.html
perfil_do_aluno_animated/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
perfil_do_aluno_animated/code.html:1 - missing skip link for main content
perfil_do_aluno_animated/code.html:1 - motion present without `prefers-reduced-motion` fallback
perfil_do_aluno_animated/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
perfil_do_aluno_animated/code.html:181 - `<img>` missing explicit `width` and `height`
perfil_do_aluno_animated/code.html:185 - button lacks explicit visible focus styling
perfil_do_aluno_animated/code.html:185 - icon-only button missing `aria-label`
perfil_do_aluno_animated/code.html:227 - `<img>` missing explicit `width` and `height`

## player_de_treino/code.html
player_de_treino/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
player_de_treino/code.html:1 - missing skip link for main content
player_de_treino/code.html:1 - motion present without `prefers-reduced-motion` fallback
player_de_treino/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
player_de_treino/code.html:134 - button lacks explicit visible focus styling
player_de_treino/code.html:134 - icon-only button missing `aria-label`
player_de_treino/code.html:151 - `<img>` missing explicit `width` and `height`
player_de_treino/code.html:169 - input missing `autocomplete` metadata

## player_de_treino_dark_mode_1/code.html
player_de_treino_dark_mode_1/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
player_de_treino_dark_mode_1/code.html:1 - missing skip link for main content
player_de_treino_dark_mode_1/code.html:1 - motion present without `prefers-reduced-motion` fallback
player_de_treino_dark_mode_1/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
player_de_treino_dark_mode_1/code.html:140 - button lacks explicit visible focus styling
player_de_treino_dark_mode_1/code.html:140 - icon-only button missing `aria-label`
player_de_treino_dark_mode_1/code.html:157 - `<img>` missing explicit `width` and `height`
player_de_treino_dark_mode_1/code.html:175 - input missing `autocomplete` metadata

## player_de_treino_dark_mode_2/code.html
player_de_treino_dark_mode_2/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
player_de_treino_dark_mode_2/code.html:1 - missing skip link for main content
player_de_treino_dark_mode_2/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
player_de_treino_dark_mode_2/code.html:170 - `transition: all`/`transition-all` used; list explicit properties
player_de_treino_dark_mode_2/code.html:186 - button lacks explicit visible focus styling
player_de_treino_dark_mode_2/code.html:186 - icon-only button missing `aria-label`
player_de_treino_dark_mode_2/code.html:203 - `<img>` missing explicit `width` and `height`
player_de_treino_dark_mode_2/code.html:219 - `transition: all`/`transition-all` used; list explicit properties

## player_de_treino_modo_foco_total/code.html
player_de_treino_modo_foco_total/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
player_de_treino_modo_foco_total/code.html:1 - missing skip link for main content
player_de_treino_modo_foco_total/code.html:1 - motion present without `prefers-reduced-motion` fallback
player_de_treino_modo_foco_total/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
player_de_treino_modo_foco_total/code.html:151 - interactive icon span needs button semantics and accessible name
player_de_treino_modo_foco_total/code.html:151 - non-semantic interactive `div`/`span`; use `<button>` or `<a>`
player_de_treino_modo_foco_total/code.html:156 - `<img>` missing explicit `width` and `height`
player_de_treino_modo_foco_total/code.html:158 - interactive icon span needs button semantics and accessible name

## relat_rios_avan_ados_trainer/code.html
relat_rios_avan_ados_trainer/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
relat_rios_avan_ados_trainer/code.html:1 - missing skip link for main content
relat_rios_avan_ados_trainer/code.html:1 - motion present without `prefers-reduced-motion` fallback
relat_rios_avan_ados_trainer/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
relat_rios_avan_ados_trainer/code.html:148 - button lacks explicit visible focus styling
relat_rios_avan_ados_trainer/code.html:148 - icon-only button missing `aria-label`
relat_rios_avan_ados_trainer/code.html:156 - `<img>` missing explicit `width` and `height`
relat_rios_avan_ados_trainer/code.html:301 - `<img>` missing explicit `width` and `height`

## selecionar_exerc_cio/code.html
selecionar_exerc_cio/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
selecionar_exerc_cio/code.html:1 - missing skip link for main content
selecionar_exerc_cio/code.html:1 - motion present without `prefers-reduced-motion` fallback
selecionar_exerc_cio/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
selecionar_exerc_cio/code.html:136 - button lacks explicit visible focus styling
selecionar_exerc_cio/code.html:136 - icon-only button missing `aria-label`
selecionar_exerc_cio/code.html:142 - `<img>` missing explicit `width` and `height`
selecionar_exerc_cio/code.html:152 - input missing `autocomplete` metadata

## timer_tabata_ativo/code.html
timer_tabata_ativo/code.html:1 - no visible `:focus-visible` treatment found for interactive UI
timer_tabata_ativo/code.html:1 - missing skip link for main content
timer_tabata_ativo/code.html:1 - motion present without `prefers-reduced-motion` fallback
timer_tabata_ativo/code.html:1 - missing `touch-action: manipulation` for tap-heavy mobile UI
timer_tabata_ativo/code.html:132 - `<img>` missing explicit `width` and `height`
timer_tabata_ativo/code.html:135 - button lacks explicit visible focus styling
timer_tabata_ativo/code.html:135 - icon-only button missing `aria-label`
timer_tabata_ativo/code.html:160 - `transition: all`/`transition-all` used; list explicit properties
