# Henrico Agent OS

Biblioteca pessoal de skills, agents, MCPs, workflows e padrões operacionais para projetos de Henrico Amaral.

Este repositório não pertence a nenhum projeto específico. Ele é a base operacional reutilizável para:

- Portfolio
- LavaPro
- SaaS
- projetos futuros
- rotinas de pesquisa
- design system
- UX research
- frontend
- acessibilidade
- carreira
- conteúdo
- automação

## Princípio central

Projetos não devem armazenar bibliotecas completas de agentes ou skills.

Projetos devem consumir skills por referência, cópia controlada ou instalação seletiva.

## Estrutura

```txt
skills/
  core/
  design/
  product/
  research/
  frontend/
  accessibility/
  content/
  career/
  mcp/
  repo-hygiene/

agents/
  design/
  product/
  engineering/
  research/
  content/
  governance/

mcps/
  registry/
  candidates/
  installed/
  security-review/

workflows/
  portfolio/
  saas/
  lava-pro/
  research/
  content/
  repository-maintenance/

templates/
  skill-template/
  agent-template/
  mcp-template/
  audit-template/

registry/
  skills-index.md
  agents-index.md
  mcps-index.md
  external-sources.md

external/
  README.md

adapted/
  README.md

archive/
  README.md
```

## Regra de uso

- `external/` guarda materiais originais clonados ou copiados de terceiros.
- `adapted/` guarda versões adaptadas para o fluxo de Henrico.
- `skills/` guarda somente skills oficiais e limpas.
- `agents/` guarda agentes com papéis claros.
- `mcps/` guarda inventário, avaliação e configuração de MCPs.
- `workflows/` guarda processos aplicáveis por projeto.
- `archive/` guarda material antigo ou em quarentena.

## Segurança

Nunca instalar ou executar skill, script, MCP ou agente externo sem revisão.

Toda skill externa deve passar por:

1. leitura manual
2. checagem de permissões
3. remoção de instruções perigosas
4. adaptação ao padrão Henrico
5. registro no índice
6. teste controlado
