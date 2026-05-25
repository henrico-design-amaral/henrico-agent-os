# Henrico Agent OS — Phase 1 Orchestrator

## Objetivo

Criar uma camada mínima de orquestração para manter ChatGPT, Codex local, Codex no Antigravity e o próprio usuário trabalhando com o mesmo contexto operacional.

A Fase 1 não é multiagente avançado.
A Fase 1 não é automação completa.
A Fase 1 é governança, memória mínima, fluxo de decisão e qualidade.

## Princípio central

Nenhuma IA é fonte de verdade.

A fonte de verdade é o conjunto de arquivos Markdown do projeto, atualizado de forma explícita e versionável.

## Ordem obrigatória de leitura

Antes de qualquer tarefa em um projeto, o agente deve procurar e ler, quando existirem:

1. `PROJECT_CONTROL.md`
2. `AGENTS.md`
3. `GEMINI.md`
4. `HANDOFF.md`
5. `TASKS.md`
6. `DECISIONS.md`
7. `QUALITY_GATES.md`
8. `docs/audits/`
9. `docs/orchestrator/`

## Fluxo obrigatório

Toda tarefa deve seguir:

1. Entender o contexto
2. Identificar branch atual
3. Verificar `git status`
4. Separar escopo permitido e proibido
5. Planejar antes de executar
6. Aguardar aprovação quando a mudança for estrutural
7. Alterar o mínimo necessário
8. Testar
9. Registrar decisão ou log factual
10. Sugerir commit pequeno

## Regras de execução

- Não trabalhar direto na `main`.
- Não misturar escopos diferentes no mesmo PR.
- Não alterar arquivos durante auditoria.
- Não executar pedidos vagos como “melhore tudo”.
- Não corrigir tudo de uma vez.
- Não aplicar mudanças visuais, técnicas e textuais no mesmo commit sem justificativa.
- Não commitar secrets, API keys ou arquivos de ambiente.
- Não versionar `node_modules`, `dist`, `build` ou caches.

## Quality gates mínimos

Antes de commit:

- `git status` revisado
- `git diff --stat` revisado
- `git diff` revisado quando necessário
- arquivos modificados coerentes com o escopo
- nada sensível incluído
- teste manual ou técnico realizado
- mensagem de commit clara

Antes de PR:

- 1 PR = 1 tipo de mudança
- descrição objetiva
- fora de escopo declarado
- riscos conhecidos declarados
- próximos passos separados

## Relação com o Portfolio

O Portfolio é o projeto piloto da Fase 1.

Toda evolução do orquestrador deve primeiro provar valor no Portfolio antes de virar regra global permanente.

## Regra final

A IA executa e organiza.
Henrico pensa, decide e assina.
