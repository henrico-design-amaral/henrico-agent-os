# Official Session Prompts

Última atualização: 28/05/2026

## Objetivo

Este documento define prompts oficiais para iniciar, conduzir e encerrar sessões de trabalho usando ChatGPT, Antigravity, Codex, Claude Code e Cowork.

A função destes prompts é reduzir erro operacional, evitar alterações fora de escopo, preservar Git limpo e garantir que o caminho oficial seja respeitado.

## Raiz operacional oficial

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO

O caminho antigo está obsoleto:

C:\Users\henri\Documents\!PROJETOS

## Repositórios principais

### henrico-agent-os

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO\00_SYSTEM\henrico-agent-os

Remote:

https://github.com/henrico-design-amaral/henrico-agent-os.git

### Portfolio

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO\01_ACTIVE\Portfolio

Remote:

https://github.com/henrico-design-amaral/portfolio.git

## Regras obrigatórias

Nunca rodar na raiz 04_PROJETOS_CONTEÚDO:

- git init
- uv init
- npm init
- npm install

A raiz 04_PROJETOS_CONTEÚDO não é um repositório Git.

Comandos técnicos devem ser executados apenas dentro dos repositórios específicos ou em áreas temporárias controladas.

Antes de qualquer edição em projeto Git:

- git status -sb
- git branch --show-current
- git remote -v
- git pull --ff-only

Se houver mudança inesperada, parar e reportar.

## Prompt universal de início de sessão

Read the project governance files first.

Official root:

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO

Before doing anything:

1. Confirm the current working directory.
2. Run git status -sb.
3. Run git branch --show-current.
4. Run git remote -v.
5. Run git pull --ff-only only if the working tree is clean.
6. Identify whether the current folder is a Git repository.
7. If the current folder is the root 04_PROJETOS_CONTEÚDO, do not run project initialization commands.
8. Do not edit files yet.
9. Do not commit yet.

Report:

- current directory;
- whether this is a Git repo;
- current branch;
- working tree status;
- remote;
- risks;
- whether it is safe to proceed.

## Prompt para Antigravity

You are operating inside the official project root:

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO

Respect the root governance:

- ROOT_RULES.md
- WORKFLOW.md
- PROJECT_INDEX.md
- LOCAL_SETUP.md

Task:

Start a controlled Antigravity work session.

Rules:

1. Do not edit files before reporting the current state.
2. Do not run git init, uv init, npm init or npm install in the root.
3. If working on Portfolio, use C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO\01_ACTIVE\Portfolio.
4. If working on agent governance, use C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO\00_SYSTEM\henrico-agent-os.
5. One branch per objective.
6. One pull request per relevant change.
7. Do not touch files outside the declared scope.

First report:

- current directory;
- repo status;
- branch;
- untracked files;
- recommended branch name;
- safe next action.

## Prompt para Codex

Read the governance files before acting.

Official root:

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO

Task:

Execute a controlled technical task.

Before editing:

1. Run pwd or equivalent.
2. Run git status -sb.
3. Run git branch --show-current.
4. Run git remote -v.
5. Confirm the target repository.
6. Confirm the files that may be changed.
7. Stop if unrelated changes exist.

Execution rules:

- Do not edit files outside scope.
- Do not initialize projects in the root.
- Do not copy raw assets into Git.
- Do not version node_modules, .venv, dist, build, .next, caches or large raw files.
- Prefer small commits.
- Explain every changed file.

Closeout:

- run git status -sb;
- summarize changed files;
- propose commit message;
- do not push unless explicitly instructed.

## Prompt para Claude Code

Read the governance files first:

- ROOT_RULES.md
- WORKFLOW.md
- PROJECT_INDEX.md
- LOCAL_SETUP.md

Official root:

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO

Task:

Start a long-form Claude Code session with strict operational control.

Before action:

1. Identify repository.
2. Validate Git status.
3. Validate current branch.
4. Identify project-specific instructions.
5. Identify allowed files.
6. Identify forbidden files.
7. Stop if the worktree is not clean or if scope is ambiguous.

Rules:

- Work in one branch only.
- Keep changes scoped.
- Do not migrate raw assets into Git.
- Do not touch snapshots in 99_ARCHIVE unless explicitly requested.
- Do not alter root governance files unless task is governance-related.
- Prefer documentation of decisions when behavior changes.

Closeout:

- run git status -sb;
- summarize what changed;
- summarize what did not change;
- list risks;
- list next recommended action.

## Prompt para Cowork

Use the official root:

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO

Task:

Organize or synthesize project materials without changing code.

Rules:

1. Treat Google Drive as continuity and source of raw materials.
2. Treat GitHub as technical version history.
3. Do not move or delete snapshots.
4. Do not copy raw files into Git repositories.
5. Keep raw case materials in C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO\04_SHARED_ASSETS.
6. Produce summaries, indexes or lightweight documents only.
7. Clearly state source paths and destination paths.

Report:

- what was read;
- what was created;
- what was moved, if anything;
- what should remain untouched.

## Prompt de encerramento de sessão

Close this work session.

Before closing:

1. Run git status -sb in every repository touched.
2. Confirm current branch.
3. Confirm whether changes were committed.
4. Confirm whether changes were pushed.
5. Confirm whether a PR exists.
6. Confirm whether any files remain untracked.
7. Confirm whether root files were changed.
8. Confirm whether raw assets were moved or copied.

Report:

- repositories touched;
- final status;
- commits created;
- PRs created or merged;
- files intentionally changed;
- files intentionally not changed;
- risks;
- next recommended action.

## Regra para raw assets do Portfolio

Os materiais brutos do Portfolio ficam em:

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO\04_SHARED_ASSETS\Portfolio

O repo ativo do Portfolio fica em:

C:\Users\henri\Documents\04_PROJETOS_CONTEÚDO\01_ACTIVE\Portfolio

O repo ativo não deve receber:

- case-references
- data
- busca-metricas-linkedin.csv
- dumps
- exports pesados
- PDFs grandes sem necessidade técnica
- planilhas brutas
- screenshots em massa

O repo ativo pode receber apenas índices leves, documentação consolidada e assets finais intencionais.
