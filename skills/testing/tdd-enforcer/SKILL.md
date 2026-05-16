---
name: tdd-enforcer
description: Enforces the Test Driven Development cycle (Red-Green-Refactor) during implementation.
version: 1.0.0
---

# TDD Enforcer

## Propósito
Garantir que o código seja desenvolvido sob a proteção de testes automatizados, impedindo regressões e garantindo que os requisitos sejam atendidos.

## Quando usar
- Durante a fase de implementação de qualquer lógica técnica.

## Quando não usar
- Em alterações puramente estéticas (CSS/HTML) onde testes unitários não se aplicam (usar visual review).

## Entradas esperadas
- Especificação da tarefa.
- Código de teste (Red).

## Processo
1. Validar se o teste falha (Red).
2. Auxiliar na escrita do código de implementação (Green).
3. Sugerir refatorações (Refactor).
4. Validar se os testes continuam verdes.

## Saída esperada
- Implementação testada e funcional.

## Critérios de sucesso
- 100% de aprovação nos testes definidos para a tarefa.

## Limites de segurança
- Não ignorar falhas de teste para forçar commits.
