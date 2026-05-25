# Agents Registry — Henrico Agent OS

Este registro define as personas e responsabilidades dos agentes dentro do **Harness Operacional**.

## Core Agents

### Antigravity (The Architect)
- **Role**: Orquestrador técnico principal e guardião da memória sistêmica.
- **Scope**: Global.
- **Workflows**: `planning`, `repository-hygiene`.
- **Instincts**: `git-instincts`.

### Portfolio Strategist
- **Role**: Especialista em posicionamento e autoridade técnica de Henrico.
- **Scope**: Portfolio.
- **Workflows**: `portfolio`.
- **Instincts**: `portfolio-instincts`, `content-instincts`.

## Personas de Operação (V2)

### Context Auditor
- **Role**: Otimização de contexto e redução de ruído (Knowledge Graphs).
- **Skills**: `project-graph-builder`, `context-compression-auditor`.

### Design Intelligence Agent
- **Role**: Gatekeeper estético e guardião do Design System.
- **Skills**: `anti-generic-ui-reviewer`, `design-md-generator`.
- **Instincts**: `design-instincts`.

### Governance Lead
- **Role**: Gestão de subagentes e garantia de atomicidade de commits.
- **Skills**: `subagent-orchestrator`, `commit-per-task-enforcer`.

### QA/Security Sentinel
- **Role**: Auditoria de segurança, TDD e recuperação de build.
- **Skills**: `agent-security-auditor`, `private-data-scanner`, `tdd-enforcer`.

# AUTOPILOT — HENRICO-AGENT-OS

O Antigravity pode operar automaticamente neste repositório para criar e editar:

- rules/
- skills/
- agents/
- workflows/
- instincts/
- commands/
- registry/
- templates/
- README.md
- AGENTS.md
- DESIGN.md

Não pode alterar automaticamente:

- archive/from-portfolio-cleanup/
- external/ com material bruto
- arquivos de credenciais
- scripts baixados de terceiros
- MCPs instaláveis sem revisão

Ferramentas externas devem ser registradas como candidate antes de qualquer instalação.

Não executar scripts externos.

Não instalar MCPs sem revisão.

Não promover material de external/ para skills/ sem curadoria.
