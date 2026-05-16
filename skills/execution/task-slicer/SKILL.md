---
name: task-slicer
description: Slices complex features into small, atomic, and independent tasks following the GSD (Get Shit Done) philosophy.
version: 1.0.0
---

# Task Slicer

## Propósito
Decompor requisitos de alto nível em tarefas técnicas atômicas que podem ser executadas de forma independente por subagentes, minimizando conflitos e maximizando a velocidade de entrega.

## Quando usar
- Ao receber um User Request complexo.
- Antes de iniciar qualquer fase de implementação.
- Para planejar um novo track de trabalho.

## Quando não usar
- Para correções de bugs simples (one-liner).
- Em tarefas puramente exploratórias sem entrega de código.

## Entradas esperadas
- Descrição da feature ou problema.
- Contexto técnico do repositório.

## Processo
1. Identificar o "caminho crítico" da implementação.
2. Quebrar a feature em sub-tarefas de no máximo 20-30 linhas de código (idealmente).
3. Definir critérios de aceitação claros para cada fatia (slice).
4. Sequenciar as tarefas para evitar bloqueios de dependência.

## Saída esperada
- Checklist de tarefas atômicas no `README.md` ou em um arquivo de track.

## Critérios de sucesso
- Cada tarefa pode ser concluída em um único turno de subagente.
- Nenhuma tarefa depende de outra tarefa sendo executada simultaneamente no mesmo arquivo.

## Limites de segurança
- Não deve planejar alterações em arquivos fora do escopo definido.
