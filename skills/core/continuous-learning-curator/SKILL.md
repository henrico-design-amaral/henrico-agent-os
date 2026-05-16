---
name: continuous-learning-curator
description: Curates lessons learned from project executions and updates the project's memory.
version: 1.0.0
---

# Continuous Learning Curator

## Propósito
Garantir que o conhecimento gerado durante uma tarefa seja persistido, evitando a repetição de erros e solidificando decisões técnicas na `ia-memory`.

## Quando usar
- Ao final de cada tarefa ou milestone importante.
- Após resolver um bug complexo.

## Quando não usar
- Em tarefas triviais de manutenção.

## Entradas esperadas
- Logs de execução da tarefa.
- Feedback do usuário.
- Mudanças no código.

## Processo
1. Extrair "Lessons Learned" (O que funcionou, o que falhou).
2. Resumir decisões arquiteturais tomadas.
3. Atualizar a `ia-memory` do projeto ou as `instincts` globais.

## Saída esperada
- Atualização em arquivos de memória ou instincts.

## Critérios de sucesso
- Agentes futuros não repetem erros documentados pelo curador.

## Limites de segurança
- Não persistir dados sensíveis ou temporários.
