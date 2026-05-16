---
name: subagent-orchestrator
description: Orchestrates multiple subagents to execute sliced tasks in parallel or sequence, maintaining global state consistency.
version: 1.0.0
---

# Subagent Orchestrator

## Propósito
Gerenciar a execução de tarefas por subagentes, garantindo que cada um tenha o contexto necessário, cumpra sua tarefa e reporte o status corretamente ao agente principal.

## Quando usar
- Quando uma implementação foi fatiada em múltiplas tarefas.
- Para rodar testes, lint e build em paralelo à codificação.

## Quando não usar
- Em tarefas sequenciais simples onde o overhead de orquestração não se justifica.

## Entradas esperadas
- Lista de tarefas gerada pelo `task-slicer`.
- Definição de limites de recursos (threads, tokens).

## Processo
1. Despachar subagentes para tarefas específicas.
2. Monitorar o progresso e logs de cada subagente.
3. Resolver conflitos de mesclagem se dois subagentes tocarem no mesmo arquivo (raro se o fatiamento for bom).
4. Validar a entrega final contra os critérios de aceitação.

## Saída esperada
- Status consolidado de execução das tarefas.
- Código integrado e testado.

## Critérios de sucesso
- Execução sem erros de concorrência.
- Todas as fatias de código integradas perfeitamente.

## Limites de segurança
- Limitar o número de subagentes simultâneos para evitar estouro de limite de taxa (rate limit).
- Isolar subagentes em diretórios ou branches se necessário.
