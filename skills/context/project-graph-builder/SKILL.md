---
name: project-graph-builder
description: Builds a conceptual knowledge graph of the project to reduce redundant raw reading.
version: 1.0.0
---

# Project Graph Builder

## Propósito
Criar e manter um grafo de conhecimento (Knowledge Graph) do projeto, mapeando dependências, fluxos de dados e decisões arquiteturais de forma semântica. Inspirado no conceito de Graphify.

## Quando usar
- Ao iniciar um novo projeto ou assumir um legado.
- Quando o contexto do projeto se torna complexo demais para leitura sequencial.
- Para identificar redundâncias e pontos de falha sistêmicos.

## Quando não usar
- Em scripts triviais de arquivo único.
- Quando já existe uma documentação de grafo atualizada e confiável.

## Entradas esperadas
- Estrutura de diretórios do projeto.
- Arquivos de configuração (`package.json`, `go.mod`, etc.).
- Documentação existente (`README.md`, `DESIGN.md`).
- Histórico de commits (opcional).

## Processo
1. Escanear a raiz do projeto para identificar tecnologias e padrões.
2. Mapear os principais módulos e suas interconexões.
3. Extrair entidades principais (Serviços, Modelos, UI Components).
4. Gerar um arquivo `PROJECT_GRAPH.md` ou `KNOWLEDGE_BASE.md`.
5. Validar o grafo contra o código real para evitar alucinações.

## Saída esperada
- Um mapa visual ou textual (Markdown/Mermaid) das conexões do projeto.
- Lista de "Hotspots" (áreas de alta complexidade).

## Critérios de sucesso
- Redução no tempo de descoberta de contexto por novos agentes.
- Ausência de redundâncias óbvias no mapeamento.

## Limites de segurança
- Não deve expor segredos ou chaves de API encontradas no código.
- O grafo deve residir apenas no ambiente local do projeto.
