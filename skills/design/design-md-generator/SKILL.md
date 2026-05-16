---
name: design-md-generator
description: Generates high-fidelity visual specifications in Markdown (DESIGN.md) to guide agents towards premium UI.
version: 1.0.0
---

# Design MD Generator

## Propósito
Transformar intenções de design e referências visuais em um arquivo `DESIGN.md` estruturado, que serve como o "North Star" visual para qualquer agente que mexa na UI.

## Quando usar
- No início da criação de uma nova interface ou componente.
- Quando a UI atual começa a divergir da visão original.
- Para documentar um Design System local.

## Quando não usar
- Em ferramentas CLI que não possuem interface visual.
- Quando já existe um `DESIGN.md` completo e atualizado.

## Entradas esperadas
- Prints de referência (opcional).
- Descrição de cores, tipografia e "vibe".
- Framework de UI utilizado.

## Processo
1. Definir a paleta de cores (Tokens).
2. Estabelecer regras de espaçamento e grid.
3. Descrever micro-interações e animações esperadas.
4. Listar componentes proibidos (bloqueio de clichês).
5. Gerar o arquivo `DESIGN.md`.

## Saída esperada
- Arquivo `DESIGN.md` com especificações semânticas.

## Critérios de sucesso
- Agentes subsequentes conseguem implementar a UI sem pedir clarificações visuais.
- A UI resultante foge do padrão "bootstrap genérico".

## Limites de segurança
- Não deve sobrescrever arquivos existentes sem backup.
- Deve respeitar as regras locais de `ai-memory`.
