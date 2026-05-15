# AGENTS.md — Henrico Agent OS

Este repositório é a fonte central de skills, agentes, MCPs e workflows de Henrico Amaral.

## Regras para agentes

Antes de criar ou alterar qualquer skill, agente ou MCP:

1. Ler este AGENTS.md.
2. Ler `registry/skills-index.md`, `registry/agents-index.md` e `registry/mcps-index.md`.
3. Confirmar se já existe algo semelhante.
4. Evitar duplicidade.
5. Criar artefatos pequenos, claros e reutilizáveis.
6. Registrar qualquer novo artefato no índice correspondente.
7. Nunca inserir segredos, tokens ou credenciais.
8. Nunca colocar código executável não revisado em skills oficiais.
9. Separar material externo bruto de material adaptado.
10. Manter compatibilidade com agentes que leem SKILL.md.

## Hierarquia

1. Instrução explícita de Henrico.
2. Este AGENTS.md.
3. Índices em `registry/`.
4. Templates em `templates/`.
5. Skills, agents e MCPs oficiais.
6. Materiais em `adapted/`.
7. Materiais em `external/`.
8. Inferência.

Inferência nunca deve virar regra sem registro.

## Padrão de qualidade

Todo artefato precisa ter:

- propósito claro
- gatilhos de uso
- entradas esperadas
- processo passo a passo
- critérios de sucesso
- limites
- riscos
- exemplos
- registro no índice

## Regra final

Este repositório deve reduzir confusão, não aumentar.
Não criar 50 skills pequenas se 5 skills fortes resolvem melhor.
