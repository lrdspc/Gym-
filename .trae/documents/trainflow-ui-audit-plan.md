# TrainFlow UI Audit Plan

## Summary

Create a whole-suite UI audit plan for the TrainFlow design archive, focused strictly on web-interface-guideline compliance and usability/accessibility/performance issues. Do not redesign the visual language, brand direction, palette, or layout system beyond documenting targeted fixes needed to make the existing design implementation production-ready.

## Current State Analysis

- Workspace contents:
  - `/workspace/README.md` contains only a placeholder title.
  - `/workspace/stitch_modern_application_suite (1).zip` is the only meaningful project artifact.
- Archive contents discovered from the zip listing:
  - Product/master spec: `stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md`
  - Multiple standalone HTML screens under `stitch_modern_application_suite/**/code.html`
  - Matching preview images under `stitch_modern_application_suite/**/screen.png`
  - One design-system reference: `stitch_modern_application_suite/high_performance_athletic/DESIGN.md`
- Product direction confirmed from the explored spec:
  - App name: TrainFlow
  - Target form factor: mobile-first PWA
  - Recommended stack: React + Vite + Tailwind + shadcn/ui + Motion
  - Dual experience: student-facing and trainer-facing flows
- Visual system confirmed from the explored design docs:
  - Pure-black / deep-charcoal surfaces
  - Electric-lime primary action color
  - Bebas Neue + Inter pairing
  - High-contrast, glassmorphism-influenced fitness UI
- Representative HTML screen inspected:
  - `stitch_modern_application_suite/dashboard_do_aluno/code.html`
  - Observed implementation style: standalone HTML + Tailwind CDN + Google Fonts + Material Symbols + dark-mode shell + many interactive controls
- Constraints confirmed from user decisions:
  - Deliverable is an audit plan, not a redesign plan
  - Scope covers the whole suite
  - Audit must preserve the current design direction; no visual redesign work

## Proposed Changes

### 1. Prepare the audit target set

- Target files:
  - `stitch_modern_application_suite/**/code.html`
  - `stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md`
  - `stitch_modern_application_suite/high_performance_athletic/DESIGN.md`
- What:
  - Extract the zip to a working directory and treat every `code.html` file as an auditable screen artifact.
- Why:
  - The current workspace has no extracted frontend codebase; the archive is the source of truth.
- How:
  - Unpack the archive into a stable workspace folder.
  - Build an inventory table of all screens.
  - Group screens into `student`, `trainer`, `shared`, and `reference-only` buckets using folder names and content.

### 2. Audit all screens against the web-interface guidelines

- Target files:
  - Entire pattern: `stitch_modern_application_suite/**/code.html`
  - Representative high-priority screens to inspect first:
    - `stitch_modern_application_suite/login_do_aluno/code.html`
    - `stitch_modern_application_suite/dashboard_do_aluno/code.html`
    - `stitch_modern_application_suite/player_de_treino/code.html`
    - `stitch_modern_application_suite/player_de_treino_dark_mode_1/code.html`
    - `stitch_modern_application_suite/dashboard_do_personal/code.html`
    - `stitch_modern_application_suite/gest_o_de_alunos_trainer/code.html`
    - `stitch_modern_application_suite/builder_de_plano_de_treino/code.html`
    - `stitch_modern_application_suite/mensagens_do_personal_conversa/code.html`
    - `stitch_modern_application_suite/formul_rio_de_avalia_o_f_sica_profissional/code.html`
- What:
  - Review each screen for guideline compliance in accessibility, semantics, focus, forms, copy, interaction, image handling, motion, and performance-risk categories.
- Why:
  - These standalone HTML mocks are likely to carry over into implementation decisions; catching issues now reduces repeated defects later.
- How:
  - Use the fetched Vercel Web Interface Guidelines as the audit rubric.
  - Record findings in terse `file:line` format.
  - Prioritize issues that affect keyboard access, screen-reader use, semantic correctness, form usability, and production robustness.

### 3. Produce issue categories that preserve the existing design

- Target files:
  - All audited `code.html` screens
- What:
  - Classify findings into “must fix before implementation” and “safe follow-up” without proposing visual redesign.
- Why:
  - The user explicitly wants audit-only output, so the executor needs implementation-safe fixes rather than style exploration.
- How:
  - Use these issue buckets:
    - Accessibility blockers
    - Semantic/interaction correctness
    - Focus/keyboard states
    - Form labeling and input metadata
    - Motion/performance risks
    - Content/copy consistency
    - Image/loading/layout stability issues
  - For each finding, describe the smallest compliant fix that preserves the existing look and layout intent.

### 4. Cross-check design intent vs. implementation artifacts

- Target files:
  - `stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md`
  - `stitch_modern_application_suite/high_performance_athletic/DESIGN.md`
  - All `stitch_modern_application_suite/**/code.html`
- What:
  - Validate that implementation details support the documented TrainFlow design and product constraints.
- Why:
  - Some issues may not be visible from a single screen alone; they emerge when the spec, design tokens, and HTML implementation are compared together.
- How:
  - Check whether HTML screens consistently apply:
    - documented typography pairings
    - action-color semantics
    - dark-theme expectations
    - touch-target minimums
    - mobile-first spacing rhythm
  - Flag mismatches only when they cause guideline or product-alignment problems, not when they merely differ stylistically.

### 5. Deliver a final audit artifact the executor can act on

- Target files:
  - New audit report to be created during execution, alongside the extracted archive
- What:
  - Produce a suite-level audit report organized by file with concise findings and a short rollout order.
- Why:
  - The executor needs a single actionable artifact to fix issues efficiently across dozens of screens.
- How:
  - Structure the report as:
    - scope and screen inventory
    - findings by file in clickable `file:line` format
    - recurring patterns across many screens
    - recommended fix order by severity
  - Keep recommendations implementation-oriented and non-redesign.

## Assumptions & Decisions

- The zip archive is the only reliable source of current UI work in this workspace.
- `screen.png` files are visual references only; the audit source of truth is each `code.html`.
- The audit reviews static HTML implementations, not a running React app.
- The audit should not propose a new aesthetic direction, component library migration, or layout overhaul.
- The audit may recommend semantic, accessibility, focus, form, copy, and performance fixes even if they require small markup/CSS changes.
- The fetched Vercel Web Interface Guidelines are the compliance rubric for the review.
- The strongest early focus should be on login, dashboard, workout player, messaging, trainer-management, and form-heavy screens because they carry the highest interaction and accessibility risk.

## Verification Steps

1. Extract the archive into a stable workspace folder and confirm all `code.html` files are present.
2. Build a complete inventory of auditable screens and group them by flow.
3. Run a full guideline audit across all `code.html` files.
4. Spot-check representative screens from each flow to confirm recurring issues are not being over-generalized.
5. Ensure every reported issue is tied to an actual file and line number.
6. Verify that recommendations preserve the TrainFlow visual direction and avoid redesign suggestions.
7. Deliver the final audit report and confirm it covers the whole suite, not only the representative sample.
