---
name: agent-security-auditor
description: Audits agent actions and tool usage to prevent malicious patterns or accidental data exposure.
version: 1.0.0
---

# Agent Security Auditor

## Propósito
Garantir que as ações dos agentes sejam seguras, bloqueando comandos destrutivos não autorizados e prevenindo vazamentos de dados.

## Quando usar
- Antes de cada execução de comando sensível.
- Durante a revisão de código (`review` workflow).

## Quando não usar
- Em ambientes de teste locais sem acesso a dados reais.

## Entradas esperadas
- Plano de comandos do agente.
- Diff de código.

## Processo
1. Validar comandos contra a lista negra de segurança.
2. Escanear diffs por segredos (API keys, passwords).
3. Verificar se o agente está tentando acessar arquivos fora do escopo.

## Saída esperada
- Veredito de segurança (Approved/Blocked).

## Critérios de sucesso
- Bloqueio de 100% de tentativas de comitar segredos conhecidos.

## Limites de segurança
- O auditor não deve ter permissão de desativar a si mesmo.
