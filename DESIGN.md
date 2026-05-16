# Design Principles — Henrico Agent OS

Este documento define os princípios de design que regem o **Harness Operacional**, garantindo que tanto o sistema quanto as UIs geradas por ele mantenham o padrão de excelência de Henrico.

## Design de Componentes do Harness

1. **Atômico**: Cada skill deve resolver um problema técnico específico sem efeitos colaterais ocultos.
2. **Context-Driven**: Toda ação deve ser precedida por uma auditoria de memória do projeto alvo.
3. **Auditável**: O sistema deve deixar rastros claros de por que uma decisão foi tomada (logs, commits semânticos).
4. **Resiliente**: Falhas de subagentes ou builds devem ser tratadas via `build-failure-resolver`.

## Padrão Estético (Anti-Generic)

O harness impõe uma estética "Premium Editorial" em todos os projetos de produto:

- **Tokens Semânticos**: Uso rigoroso de variáveis de cor (HSL) e tipografia (Inter/Outfit).
- **Grid de Elite**: Priorizar layouts baseados em bento grids, grids editoriais e proporção áurea.
- **Micro-Interações**: Animações suaves (GSAP) que conferem vida e feedback à interface.
- **Bloqueio de Clichês**: Rejeição automática de:
  - Cores CSS nomeadas (`blue`, `red`).
  - Fontes default do sistema (`Arial`, `Times`).
  - Layouts "Bootstrap-style" (Navbar + Hero + 3 Cards).

## Documentação North Star

O `DESIGN.md` de cada projeto de produto é o "Contrato Visual" que os agentes de design devem seguir. Ele deve ser gerado pelo `design-md-generator` e auditado pelo `anti-generic-ui-reviewer`.
