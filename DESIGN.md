---
version: 0.1
name: henrico-agent-os-design
status: draft
---

# DESIGN.md — Henrico Agent OS

Este arquivo define a direção visual e estrutural para interfaces, dashboards, documentação visual ou páginas geradas a partir deste repositório.

## Direção

A estética deve ser:

- técnica
- editorial
- madura
- precisa
- sóbria
- operacional
- orientada a sistemas

## Evitar

- visual SaaS genérico
- excesso de glow
- gradiente decorativo
- cards sem função
- tipografia fraca
- contraste baixo
- UI infantil
- complexidade visual desnecessária

## Preferir

- hierarquia clara
- layout editorial
- superfícies discretas
- densidade controlada
- tipografia legível
- padrões reutilizáveis
- acessibilidade básica
- motion sutil

## Tokens iniciais

```yaml
colors:
  background: "#0B0D10"
  surface: "#12161B"
  surfaceElevated: "#171C22"
  textPrimary: "#F4F6F8"
  textSecondary: "#A7B0BA"
  borderSubtle: "#28313A"
  accent: "#ABC5CF"
  danger: "#A60311"

typography:
  sans: "Inter, system-ui, sans-serif"
  mono: "JetBrains Mono, ui-monospace, monospace"

spacing:
  base: "4px"
  scale: [4, 8, 12, 16, 24, 32, 48, 64, 96]

radius:
  sm: "6px"
  md: "12px"
  lg: "20px"
```
