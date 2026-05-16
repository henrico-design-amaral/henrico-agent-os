---
name: private-data-scanner
description: Scans the codebase for sensitive information, credentials, and PII (Personally Identifiable Information).
version: 1.0.0
---

# Private Data Scanner

## Propósito
Detectar e prevenir o commit de dados privados, arquivos de configuração sensíveis e informações de clientes.

## Quando usar
- Antes de cada commit.
- Durante o workflow de `secure`.

## Quando não usar
- Em arquivos marcados explicitamente como públicos/open-source.

## Entradas esperadas
- Arquivos modificados ou todo o diretório de trabalho.

## Processo
1. Rodar regex de detecção de segredos (Secrets, API Keys).
2. Verificar a existência de arquivos proibidos (ex: `.env`, `*.pem`).
3. Alertar sobre dados de clientes em logs ou documentação.

## Saída esperada
- Lista de arquivos/linhas com dados sensíveis encontrados.

## Critérios de sucesso
- Zero vazamentos de dados detectados no histórico de Git.

## Limites de segurança
- Não deve armazenar os segredos encontrados em logs de auditoria.
