---
name: context-compression-auditor
description: Audits project context to identify and prune redundant or obsolete information, keeping tokens focused on what matters.
version: 1.0.0
---

# Context Compression Auditor

## Propósito
Otimizar o uso de tokens e a carga cognitiva dos agentes através da compressão e poda de contexto irrelevante, mantendo apenas a "verdade operacional" necessária.

## Quando usar
- Quando o contexto enviado para o LLM está próximo do limite de tokens.
- Após grandes refatorações onde documentos de design antigos podem estar obsoletos.
- Periodicamente para manter a `ia-memory` limpa.

## Quando não usar
- Durante a fase de pesquisa inicial, onde o ruído pode conter pistas importantes.
- Em auditorias de segurança (onde detalhes granulares são críticos).

## Entradas esperadas
- Conteúdo da pasta `ai-memory/`.
- Logs de conversas recentes.
- Arquivos de especificação (`DESIGN.md`).

## Processo
1. Analisar arquivos de memória e identificar duplicatas.
2. Cruzar especificações com o código atual para marcar obsolescência.
3. Resumir decisões históricas em "lições aprendidas" curtas.
4. Propor a deleção ou arquivamento de arquivos de contexto "sujos".

## Saída esperada
- Relatório de compressão (tokens economizados).
- Lista de arquivos propostos para limpeza/arquivamento.

## Critérios de sucesso
- Redução de pelo menos 20% no volume de contexto sem perda de precisão operacional.

## Limites de segurança
- Nunca deletar arquivos sem aprovação explícita do usuário.
- Manter backups em `archive/` antes de qualquer remoção definitiva.
