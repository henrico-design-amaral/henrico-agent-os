---
name: commit-per-task-enforcer
description: Ensures that every atomic task results in a clean, descriptive commit, following the GSD workflow.
version: 1.0.0
---

# Commit Per Task Enforcer

## Propósito
Garantir a rastreabilidade e a facilidade de rollback através da imposição de um commit para cada tarefa atômica concluída.

## Quando usar
- Durante todo o processo de implementação de uma feature.
- Ao final de cada tarefa do `task-slicer`.

## Quando não usar
- Em commits de "WIP" (Work In Progress) que não devem ir para o histórico principal.

## Entradas esperadas
- Tarefa concluída.
- Mudanças no staging area (git).

## Processo
1. Verificar se as mudanças correspondem exatamente à tarefa concluída.
2. Gerar uma mensagem de commit semântica (ex: `feat(ui): add honey-toned buttons`).
3. Executar o commit.

## Saída esperada
- Um novo commit limpo no histórico do Git.

## Critérios de sucesso
- Histórico de Git legível, onde cada commit representa uma unidade lógica de trabalho.

## Limites de segurança
- Não commitar arquivos sensíveis ou não relacionados.
- Validar build antes de commitar.
