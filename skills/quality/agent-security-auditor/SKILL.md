---
name: agent-security-auditor
description: Audits agent actions and tool usage to prevent malicious patterns, accidental data exposure, or insecure dependency installation.
version: 1.0.0
---

# Agent Security Auditor

## Propósito
Monitorar e validar as ações de outros agentes no repositório, garantindo conformidade com regras de segurança e evitando a introdução de vulnerabilidades.

## Quando usar
- Após a conclusão de tarefas por subagentes externos.
- Antes de fazer push de código para repositórios públicos.
- Ao instalar novas dependências (watchlist).

## Quando não usar
- Em ambientes de sandbox totalmente isolados (embora boa prática).

## Entradas esperadas
- Diff do código alterado.
- Lista de comandos executados pelo agente.

## Processo
1. Verificar vazamento de segredos (secrets scanning).
2. Analisar mudanças em permissões de arquivos ou configurações de rede.
3. Checar contra a `registry/tools-watchlist.md`.
4. Bloquear commits que violem políticas de segurança.

## Saída esperada
- Relatório de segurança "Pass/Fail".
- Sugestões de mitigação.

## Critérios de sucesso
- Zero segredos commitados.
- Zero vulnerabilidades conhecidas introduzidas por agentes.

## Limites de segurança
- O auditor deve ter permissões de leitura superiores às de escrita do agente auditado.
