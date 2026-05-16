---
name: tdd-coverage-planner
description: Plans and enforces TDD (Test Driven Development) coverage for new features to ensure reliability from the start.
version: 1.0.0
---

# TDD Coverage Planner

## Propósito
Garantir que cada nova funcionalidade nasça acompanhada de testes automatizados, seguindo o ciclo Red-Green-Refactor.

## Quando usar
- Na fase de planejamento de uma feature (integrado ao `task-slicer`).
- Antes de escrever qualquer código de implementação.

## Quando não usar
- Em protótipos de "descarte rápido" (embora desencorajado).

## Entradas esperadas
- Especificação da feature.
- Framework de testes do projeto.

## Processo
1. Definir os cenários de teste (sucesso e falha).
2. Gerar os arquivos de teste com falhas intencionais (Red).
3. Orientar o agente a escrever o código mínimo para passar nos testes (Green).
4. Revisar e refatorar (Refactor).

## Saída esperada
- Suite de testes robusta.
- Relatório de cobertura.

## Critérios de sucesso
- 100% de cobertura nos "happy paths" e casos de borda críticos da nova feature.

## Limites de segurança
- Não mockar comportamentos de segurança críticos sem validação real.
