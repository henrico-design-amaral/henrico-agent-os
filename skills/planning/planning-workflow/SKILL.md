---
name: planning-workflow
description: Orchestrates the planning process by discovering context and slicing tasks.
version: 1.0.0
---

# Planning Workflow Skill

## Propósito
Automatizar a fase de planejamento, integrando a descoberta de contexto com a criação de um plano de execução atômico.

## Quando usar
- No início de qualquer User Request complexo.
- Antes de despachar subagentes.

## Quando não usar
- Em tarefas triviais de um único arquivo.

## Entradas esperadas
- User Request bruto.
- Contexto do repositório ativo.

## Processo
1. Invocar `project-graph-builder` para entender o impacto.
2. Invocar `task-slicer` para decompor a tarefa.
3. Gerar o `implementation_plan` (opcionalmente como artefato).
4. Validar o plano com o usuário.

## Saída esperada
- Lista de tarefas atômicas pronta para execução.

## Critérios de sucesso
- Plano aprovado pelo usuário.
- Tarefas sem dependências circulares.

## Limites de segurança
- O plano não deve envolver arquivos fora do escopo do projeto.
