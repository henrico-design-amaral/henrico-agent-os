# DECISIONS — Henrico Agent OS

Registro de decisões arquiteturais do harness operacional.

Formato: cada decisão registra contexto, alternativas consideradas, motivo da escolha e impacto.

---

## DEC-001 — henrico-agent-os é a autoridade única para regras, skills, workflows e templates de agentes

**Data:** 2026-05-15 (implantação inicial) / revisada em 2026-06-22

**Contexto:**
Antes deste sistema, regras de agentes estavam espalhadas entre diferentes projetos, arquivos de chat e documentos sem versionamento. Cada projeto de produto criava suas próprias convenções de forma independente.

**Alternativas consideradas:**
1. Manter regras dentro de cada projeto individualmente
2. Usar um repositório de configuração central com CI/CD que propaga arquivos
3. Centralizar no henrico-agent-os com adoção manual controlada por sprint

**Decisão:** Opção 3 — centralização no henrico-agent-os com adoção manual controlada.

**Motivo:**
- Opção 1 leva a divergência e retrabalho
- Opção 2 é overhead técnico desnecessário para o volume atual de projetos
- Opção 3 mantém controle humano sobre o que vai para cada projeto

**Impacto:** Projetos de produto recebem recursos do OS apenas via sessão controlada. Nenhum arquivo é copiado automaticamente.

---

## DEC-002 — Projetos de produto não recebem arquivos automaticamente

**Data:** 2026-06-22

**Contexto:**
Durante a análise de adoção do OS, identificamos o risco de scripts ou agentes copiando arquivos de governança automaticamente para projetos de produto, causando conflitos de versão e perda de contexto específico do projeto.

**Alternativas consideradas:**
1. Propagação automática via script ou workflow
2. Adoção manual por sessão controlada
3. Submodule Git apontando para henrico-agent-os

**Decisão:** Opção 2 — adoção manual por sessão controlada.

**Motivo:**
- Opção 1 remove controle humano e pode sobrescrever customizações de projeto
- Opção 3 cria dependência técnica frágil e acoplamento desnecessário
- Opção 2 garante que cada adoção é deliberada, validada e documentada

**Impacto:** Todo sprint de adoção requer sessão própria com escopo declarado.

---

## DEC-003 — Adoção do OS por projetos será em sprints controlados

**Data:** 2026-06-22

**Contexto:**
O henrico-agent-os tem 5 projetos de produto para atender: Portfolio, henrico.works, CondoLogPro, PersonalOps e HenricoOPS. Tentar adotar tudo de uma vez cria risco de erros difíceis de rastrear.

**Decisão:** Adoção em 5 sprints sequenciais, começando pelos recursos de fundação do próprio OS.

**Ordem:**
1. Sprint 1: Fundação do OS (este sprint)
2. Sprint 2: Portfolio
3. Sprint 3: henrico.works (prioridade alta — zero governança)
4. Sprint 4: CondoLogPro
5. Sprint 5: PersonalOps + limpeza do OS

**Impacto:** Projetos de produto sem governança assumem risco até seus sprints.

---

## DEC-004 — Arquivos autoritativos vazios são bloqueadores de adoção

**Data:** 2026-06-22

**Contexto:**
Foram encontrados 3 arquivos com nomes críticos completamente vazios: `QUALITY_GATES.md`, `PROMPT_BOOTSTRAP.md` e `TOOL_MAP.md`. Citar arquivos vazios como referência de governança cria falsa sensação de segurança — pior do que não ter o arquivo.

**Decisão:** Nenhum arquivo de governança pode ser citado como referência sem ter conteúdo real, validável e aplicável.

**Critério de validação:** Um agente deve conseguir responder a uma pergunta sobre escopo, segurança ou ferramenta usando o arquivo como única referência.

**Impacto:** Sprint 1 foi exclusivamente dedicado a preencher estes 3 arquivos antes de qualquer adoção nos projetos de produto.

---

## DEC-005 — Skills legadas não serão apagadas sem sessão própria

**Data:** 2026-06-22

**Contexto:**
Foram identificadas 6 skills com nomenclatura fora do padrão oficial (`skill.md` minúsculo em vez de `SKILL.md`) e fora da taxonomia de diretórios: `anti-puxadinho-scope`, `astro-visual-qa`, `motion-design-clean`, `project-intake`, `memory-closeout`, `release-governance`.

**Alternativas:**
1. Apagar imediatamente
2. Mover para `archive/` agora
3. Manter no lugar e arquivar em sprint dedicado

**Decisão:** Opção 3 — arquivar em sprint dedicado (Sprint 5).

**Motivo:** Risco de perda de conteúdo útil sem avaliação. Algumas podem ter valor que justifica migração para a taxonomia oficial.

**Impacto:** Skills legadas permanecem no lugar sem ser referenciadas como ativas até Sprint 5.

---

## DEC-006 — Instincts e rules devem ser referenciados, não duplicados

**Data:** 2026-06-22

**Contexto:**
Durante o planejamento de adoção, surgiu a questão de se os conteúdos de `instincts/` e `rules/` devem ser copiados para os AGENTS.md de cada projeto ou apenas referenciados.

**Decisão:** Referenciar por caminho relativo ao OS. Não copiar.

**Motivo:**
- Duplicação cria divergência: projetos ficam com versões diferentes das regras sem saber
- Referência por path garante que a atualização do OS propaga para todos os projetos automaticamente (quando o agente lê o contexto)

**Exceção:** Instincts podem ser expandidos localmente se o projeto tiver necessidades específicas — mas o texto do OS é a base.

---

## DEC-007 — henrico.works é prioridade alta de adoção por ausência total de governança

**Data:** 2026-06-22

**Contexto:**
Auditoria revelou que henrico.works é o único projeto ativo sem nenhum arquivo de governança (zero AGENTS.md, zero HANDOFF.md, zero DESIGN.md). É o site de posicionamento público de Henrico — qualquer agente atuando nele hoje toma decisões de design e tom arbitrariamente.

**Decisão:** henrico.works é o Sprint 3 (não o 4 ou 5). Portfolio, apesar de ter mais conteúdo, já tem AGENTS.md robusto — o risco de henrico.works sem governança é mais urgente.

**Impacto:** Sprint 3 focado exclusivamente em criar AGENTS.md, HANDOFF.md e DESIGN.md para henrico.works.

---

## DEC-008 — Subagent orchestration e context compression permanecem bloqueados

**Data:** 2026-06-22

**Contexto:**
As skills `subagent-orchestrator` e `context-compression-auditor` estão presentes no OS mas não podem ser usadas com segurança sem infraestrutura de rollback e backup de memória.

**Risco do subagent-orchestrator:** Pode delegar ações a subagentes que cometem alterações fora de escopo sem revisão humana.

**Risco do context-compression-auditor:** Pode apagar contexto legítimo de projetos sem protocolo de backup definido.

**Decisão:** Ambas permanecem no Tier 3 (bloqueadas). Desbloqueio requer:
1. Definição de critérios claros de rollback para subagentes
2. Protocolo de backup de memória antes de compressão
3. Sessão dedicada de avaliação de risco

---

## DEC-009 — OFFICIAL_SESSION_PROMPTS.md é referência primária de prompts de sessão

**Data:** 2026-06-22

**Contexto:**
O documento `docs/orchestration/OFFICIAL_SESSION_PROMPTS.md` continha os prompts mais completos do repositório. O novo `PROMPT_BOOTSTRAP.md` foi criado como porta de entrada mais acessível, mas referencia os mesmos princípios.

**Decisão:** `PROMPT_BOOTSTRAP.md` é o documento de uso cotidiano. `OFFICIAL_SESSION_PROMPTS.md` é o documento de referência técnica completa (inclui prompts por ferramenta com mais detalhes contextuais).

**Impacto:** Ambos são mantidos. Não há duplicação — são níveis diferentes de detalhe.

---

## DEC-010 — registry.md foi substituído pela pasta registry/ com arquivos por categoria

**Data:** 2026-05-15 (implantação da estrutura v2)

**Contexto:**
O `registry.md` original era um arquivo único de índice. A estrutura evoluiu para uma pasta `registry/` com arquivos por categoria (agents, skills, rules, workflows, etc.).

**Decisão:** O arquivo `registry.md` na raiz está obsoleto e será removido ou atualizado para apontar para `registry/` em sprint de limpeza.

**Impacto:** Qualquer referência ao `registry.md` deve ser redirecionada para `registry/skills-index.md`, `registry/workflows-index.md`, etc., conforme a categoria buscada.
