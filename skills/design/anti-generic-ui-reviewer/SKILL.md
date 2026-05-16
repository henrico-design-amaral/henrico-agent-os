---
name: anti-generic-ui-reviewer
description: Reviews UI code to block visual clichés and ensure compliance with premium design standards.
version: 1.0.0
---

# Anti-Generic UI Reviewer

## Propósito
Agir como um gatekeeper de design, revisando código de frontend para detectar e corrigir padrões genéricos, cores "default" e falta de polimento visual.

## Quando usar
- Antes de cada commit que altere a UI.
- Após um subagente gerar um protótipo inicial.
- Como parte do workflow de CI de design.

## Quando não usar
- Em ambientes de admin interno onde o design é secundário à função (embora Henrico prefira design bom em tudo).

## Entradas esperadas
- Arquivos `.html`, `.css`, `.tsx`, `.jsx`.
- O `DESIGN.md` do projeto.

## Processo
1. Comparar as cores do código com os tokens definidos no `DESIGN.md`.
2. Verificar o uso de sombras, bordas e espaçamentos (bloquear valores "crus" como `blue`, `10px`).
3. Sugerir melhorias de micro-animação.
4. Rejeitar o código se ele parecer um "template gratuito de 2015".

## Saída esperada
- Lista de correções estéticas necessárias.
- Refatoração direta dos estilos se autorizado.

## Critérios de sucesso
- Zero uso de cores CSS nomeadas (ex: `red`, `green`).
- Interface com aspecto premium e personalizado.

## Limites de segurança
- Não alterar lógica de negócio durante a revisão estética.
