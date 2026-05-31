# TrainFlow Design Archive

Este repositório nao contem uma aplicacao executavel. Ele funciona como um arquivo de produto e design do **TrainFlow**, reunindo especificacao funcional, sistema visual e prototipos HTML para uma PWA mobile-first de fitness com jornadas separadas para aluno e personal trainer.

## O que existe aqui

- Especificacao principal do produto em `stitch_modern_application_suite/trainflow_especifica_o_mestre_do_produto_1.md`
- Sistema de design em `stitch_modern_application_suite/high_performance_athletic/DESIGN.md`
- 42 telas prototipo em HTML standalone dentro de `stitch_modern_application_suite/*/code.html`
- Wiki gerada em `wiki/` com visao de arquitetura, modelo de dados, APIs planejadas e instrucoes de uso

## O que nao existe aqui

- `package.json`, `src/`, backend, migrations ou testes automatizados
- Comandos de `npm install`, `npm run dev` ou build
- Implementacao real da aplicacao descrita na especificacao

## Estrutura principal

```text
.
|-- README.md
|-- CODE_WIKI.md
|-- wiki/
|-- stitch_modern_application_suite/
|   |-- trainflow_especifica_o_mestre_do_produto_1.md
|   |-- high_performance_athletic/DESIGN.md
|   `-- */code.html
`-- .trae/documents/
```

## Como visualizar os prototipos

Voce pode abrir qualquer tela diretamente no navegador, por exemplo:

- `stitch_modern_application_suite/login_do_aluno/code.html`
- `stitch_modern_application_suite/dashboard_do_aluno/code.html`
- `stitch_modern_application_suite/player_de_treino/code.html`

Se preferir servir os arquivos localmente:

```bash
cd stitch_modern_application_suite
python3 -m http.server 8000
```

Depois abra URLs como:

- `http://localhost:8000/login_do_aluno/code.html`
- `http://localhost:8000/dashboard_do_aluno/code.html`
- `http://localhost:8000/player_de_treino/code.html`

## Documentacao

- Wiki principal: `wiki/README.md`
- Indice rapido: `CODE_WIKI.md`

Paginas da wiki:

- `wiki/01-Repository-Overview.md`
- `wiki/02-Intended-Architecture.md`
- `wiki/03-Data-Model-and-Security.md`
- `wiki/04-UI-Prototypes-and-Design-System.md`
- `wiki/05-Key-APIs-and-Functions.md`
- `wiki/06-Running-and-Viewing.md`

## Stack planejada

A especificacao descreve uma implementacao futura baseada em:

- React + Vite
- TanStack Router
- Tailwind + shadcn/ui
- Supabase
- PWA com Service Worker
- Realtime chat, push notifications e suporte offline

## Objetivo deste repositorio

Este material serve como base para:

- alinhamento de produto e UX
- referencia visual das telas
- documentacao da arquitetura pretendida
- futura implementacao da aplicacao real
