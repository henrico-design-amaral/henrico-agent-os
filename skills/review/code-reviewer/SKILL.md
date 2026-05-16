---
name: code-reviewer
description: Expert code review focused on performance, readability, and adherence to project patterns.
version: 1.0.0
---

# Code Reviewer

## Propósito
Realizar revisões técnicas profundas em diffs de código, focando em dívida técnica, bugs latentes e padrões de arquitetura.

## Quando usar
- Antes de commitar qualquer mudança significativa.
- Após a conclusão de uma tarefa por um subagente.

## Quando não usar
- Para revisões estéticas (usar `anti-generic-ui-reviewer`).

## Entradas esperadas
- Diff das alterações.
- Contexto do arquivo afetado.

## Processo
1. Analisar complexidade ciclomática.
2. Verificar tratamento de erros e casos de borda.
3. Checar contra os `instincts` e `rules` do projeto.
4. Sugerir melhorias específicas com snippets.

## Saída esperada
- Relatório de revisão com sugestões de fix.

## Critérios de sucesso
- Identificação de pelo menos um ponto de melhoria ou bug em 80% das revisões.

## Limites de segurança
- Não deve aprovar código que viole as `rules/security/`.
