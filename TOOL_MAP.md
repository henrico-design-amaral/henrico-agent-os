# TOOL MAP — Henrico Agent OS

Última atualização: 2026-06-22

Mapa de ferramentas do ecossistema operacional de Henrico Amaral. Define quando usar cada ferramenta, quando não usar, riscos conhecidos, comandos permitidos e evidências exigidas.

Regra central: ferramentas são meios, não fins. A qualidade da decisão é de Henrico. A ferramenta executa.

---

## 1. Git

**Finalidade:** Controle de versão, histórico semântico, rastreabilidade de decisões e colaboração segura com remotes.

**Quando usar:**
- Para qualquer alteração em arquivo de projeto versionado
- Para criar branches de trabalho isoladas
- Para commitar e publicar alterações

**Quando não usar:**
- Na raiz `04_PROJETOS_CONTEÚDO` (não é um repositório Git)
- Para versionar `node_modules`, `dist`, `build`, `.next`, `.venv`, caches
- Para versionar assets brutos pesados (PDFs, planilhas, images não processadas)

**Riscos:**
- `git add .` sem revisão pode incluir arquivos sensíveis
- `git reset --hard` é destrutivo — exige confirmação
- Push direto para `main` em mudanças estruturais sem PR é risco de rollback difícil
- Histórico com commits misturados ("wip", "fix", "update") reduz rastreabilidade

**Comandos permitidos por contexto:**

```bash
# Inspeção (sempre seguro)
git status -sb
git branch --show-current
git remote -v
git log --oneline -10
git diff
git diff --stat
git diff --cached --stat

# Staging controlado (revisar antes)
git add <arquivo-específico>     # nunca git add .
git diff --cached                # revisar o que vai no commit

# Commit
git commit -m "type(scope): descrição"   # mensagem semântica obrigatória

# Branch
git checkout -b feature/nome-descritivo
git checkout main

# Sync
git pull --ff-only               # preferência a --rebase para histórico linear
git push origin <branch>

# Inspeção avançada
git log --oneline --graph --all -15
git show <hash> --stat
git merge-base HEAD origin/main
```

**Comandos que exigem confirmação humana:**
```bash
git reset --hard <hash>          # destrutivo
git push --force                 # nunca sem aprovação explícita
git rebase                       # risco de conflito
git merge --allow-unrelated-histories  # cria história artificial
```

**Evidências exigidas antes de push:**
- `git diff origin/main --stat` revisado
- `git log origin/main..HEAD` revisado
- Gate 7 (Pré-push) aprovado

---

## 2. GitHub CLI (`gh`)

**Finalidade:** Gerenciar repositórios, PRs, issues e releases no GitHub sem abrir o browser.

**Quando usar:**
- Para criar e verificar repositórios remotos
- Para criar e listar PRs
- Para verificar status de repositório antes de push

**Quando não usar:**
- Para criar repositórios em nome de organização sem confirmação
- Para fazer merge de PRs sem revisão
- Como substituto de `git` para controle de versão local

**Riscos:**
- A variável `GITHUB_TOKEN` pode conflitar com a autenticação do keyring — usar `$env:GITHUB_TOKEN=""` para forçar keyring quando necessário
- Operações destrutivas via `gh` (delete repo, delete branch) são irreversíveis

**Comandos permitidos:**
```bash
# Autenticação
gh auth status                   # verificar conta ativa

# Repositórios
gh repo view <owner>/<repo> --json name,url,defaultBranchRef
gh repo list <owner>

# PRs
gh pr list
gh pr create --title "..." --body "..." --base main
gh pr view <número>

# Releases
gh release list
gh release create v0.1 --notes "..."
```

**Comandos que exigem confirmação:**
```bash
gh repo delete <repo>            # irreversível
gh pr merge <número>             # merge sem revisão adicional
```

**Nota sobre autenticação:**
Em ambiente Windows com GITHUB_TOKEN inválido no env, usar:
```powershell
$env:GITHUB_TOKEN=""; gh <comando>
```

---

## 3. ChatGPT

**Finalidade:** Planejamento estratégico, análise de alternativas, síntese de informações, revisão de copy, geração de ideias e consultas pontuais sem execução de código.

**Quando usar:**
- Para raciocinar sobre arquitetura antes de implementar
- Para revisar copy e posicionamento (Portfolio, henrico.works)
- Para sintetizar pesquisas e referências visuais
- Para elaborar prompts e checklists
- Para conversas exploratórias sem risco de alteração

**Quando não usar:**
- Para execução de código real (sem acesso ao filesystem)
- Para commitar ou fazer push (sem acesso ao Git)
- Como fonte de verdade de fatos técnicos recentes (sem acesso à internet por padrão)
- Para geração de código que vai direto para produção sem revisão

**Riscos:**
- Contexto longo pode fazer o modelo "esquecer" restrições de escopo declaradas no início
- Respostas de código podem estar desatualizadas em relação a versões recentes de frameworks
- Sem acesso ao filesystem real — pode planejar baseado em premissas erradas

**Comandos/prompt esperados:**
- Usar prompt do `PROMPT_BOOTSTRAP.md` seção ChatGPT
- Sempre fornecer AGENTS.md ou HANDOFF.md como contexto colado
- Terminar sessão com lista explícita de decisões e pendências

**Evidências exigidas ao encerrar:**
- Lista de decisões tomadas
- Lista de pendências em aberto
- Próximo passo concreto identificado

---

## 4. Codex (OpenAI)

**Finalidade:** Execução técnica de tarefas bem definidas com acesso ao terminal e filesystem. Adequado para tarefas de implementação dentro de um escopo claro.

**Quando usar:**
- Para implementar features com especificação clara
- Para refatorações com escopo definido
- Para rodar scripts e inspecionar resultados
- Para tarefas que requerem execução de comandos e leitura de output

**Quando não usar:**
- Para tarefas de planejamento estratégico (usar ChatGPT)
- Para sessões longas sem checkpoint (risco de drift de contexto)
- Para mudanças estruturais sem plano aprovado
- Em projetos sem `AGENTS.md` (criar antes)

**Riscos:**
- Pode executar `npm install`, `git init` ou comandos perigosos na raiz se não orientado
- Sem instrução explícita, pode commitar automaticamente
- Tende a resolver problemas imediatamente sem perguntar — pode agir fora de escopo

**Protocolo obrigatório:**
- Usar prompt do `PROMPT_BOOTSTRAP.md` seção Codex
- Declarar escopo permitido e bloqueado explicitamente
- Revisar `git diff` antes de aprovar commit
- Nunca autorizar push sem inspecionar os commits gerados

---

## 5. Claude Code (Anthropic)

**Finalidade:** Sessões longas de implementação estrutural, debugging complexo, refatorações de múltiplos arquivos e tarefas que exigem raciocínio progressivo com contexto acumulado.

**Quando usar:**
- Para implementações que envolvem 5+ arquivos relacionados
- Para debugging com stack trace complexo
- Para refatoração com dependências cruzadas
- Para sessões de trabalho com múltiplos checkpoints

**Quando não usar:**
- Para tarefas simples (overhead de contexto desnecessário)
- Para decisões de posicionamento ou copy (usar ChatGPT)
- Para projetos sem governança mínima (`AGENTS.md`, `HANDOFF.md`)

**Riscos:**
- Contexto muito longo pode causar alucinações sobre estado do código
- Pode sugerir mudanças fora de escopo se o prompt não for restritivo
- Risco de commits automáticos se não bloqueado explicitamente no prompt

**Protocolo obrigatório:**
- Usar prompt do `PROMPT_BOOTSTRAP.md` seção Claude Code
- Usar `/goal` para sessões de projeto
- Verificar working tree ao início e ao fim
- Usar Prompt de Encerramento ao final

---

## 6. Antigravity (IDE Antigravity / Google DeepMind)

**Finalidade:** IDE com agente integrado. Acesso direto ao filesystem, terminal, browser e Git. Principal ferramenta de execução técnica do ecossistema.

**Quando usar:**
- Para qualquer tarefa de implementação com acesso ao filesystem local
- Para inspeções de repositório e execução de comandos
- Para sessões de trabalho documentadas com histórico de transcript

**Quando não usar:**
- Para planejamento puro sem execução (usar ChatGPT)
- Para tarefas que não requerem acesso ao código (usar ChatGPT ou Cowork)

**Riscos:**
- Acesso direto ao filesystem: pode alterar arquivos fora do escopo se o prompt for vago
- Pode executar comandos no terminal sem confirmação adicional
- Variável `GITHUB_TOKEN` inválida no ambiente pode bloquear `gh` — usar `$env:GITHUB_TOKEN=""` antes de comandos gh

**Protocolo obrigatório:**
- Usar prompt do `PROMPT_BOOTSTRAP.md` seção Antigravity
- Declarar escopo explicitamente no início
- Executar Gate 0 e Gate 8 de QUALITY_GATES.md
- Todo push requer Gate 7

**Evidências exigidas ao encerrar:**
- `git status -sb` reportado
- `memory/operational-log.md` atualizado

---

## 7. Browser / Preview local

**Finalidade:** Validação visual de interfaces antes de commit e push. Único meio confiável de confirmar que a UI está correta.

**Quando usar:**
- Antes de qualquer commit que altere CSS, HTML, componentes Astro, React ou Next.js
- Para confirmar responsividade em mobile e desktop
- Para validar animações e micro-interações

**Quando não usar:**
- Como substituto de testes automatizados em lógica de negócio
- Como aprovação final de acessibilidade (requer ferramentas específicas)

**Riscos:**
- Cache do browser pode mostrar versão desatualizada — sempre forçar hard reload (`Ctrl+Shift+R`)
- Preview local e produção podem diferir (ex: variáveis de ambiente)

**Comandos por projeto:**
```bash
# Portfolio (HTML/JS puro)
# Abrir index.html direto no browser ou via live server

# henrico-works (Astro)
npm run dev        # dev server
npm run build && npm run preview   # validar build de produção

# CondoLogPro (Next.js)
npm run dev        # dev server em http://localhost:3000

# PersonalOps
# conforme stack atual do projeto
```

---

## 8. Netlify

**Finalidade:** Deploy e hospedagem de sites estáticos e Astro (henrico.works). Integrado ao GitHub para deploy automático.

**Quando usar:**
- Para publicar henrico.works
- Para criar previews de PR antes de merge

**Quando não usar:**
- Para projetos com backend complexo (CondoLogPro usa modelo diferente)
- Para commits de teste sem aprovação visual local prévia

**Riscos:**
- Deploy automático em push para `main` — qualquer push quebrado vai para produção
- Variáveis de ambiente de produção não são versionadas no repositório

**Protocolo:**
- Sempre validar `npm run build` localmente antes de push para `main`
- Usar branch de PR para preview antes de merge
- Verificar painel Netlify após deploy para confirmar sucesso

---

## 9. GitHub Pages

**Finalidade:** Hospedagem de sites estáticos (Portfolio). Deploy via branch específica ou pasta `/docs`.

**Quando usar:**
- Para publicar Portfolio
- Para hospedar documentação estática de projetos

**Quando não usar:**
- Para projetos com build complexo (preferir Netlify ou Vercel)
- Para sites com autenticação ou backend

**Riscos:**
- Latência de deploy pode atrasar até 10 minutos
- Apenas sites estáticos — sem suporte a server-side rendering

---

## 10. Vercel

**Candidata — não integrada ao ecossistema como padrão ainda.**

Avaliação pendente via skill `mcp-evaluator` antes de uso oficial.

---

## Resumo de uso por projeto

| Projeto | Git | gh | ChatGPT | Codex | Claude Code | Antigravity | Browser | Netlify | GitHub Pages |
|---|---|---|---|---|---|---|---|---|---|
| henrico-agent-os | ✅ | ✅ | ✅ planejamento | ✅ | ✅ | ✅ principal | ❌ | ❌ | ❌ |
| Portfolio | ✅ | ✅ | ✅ copy/pos. | ✅ | ✅ | ✅ principal | ✅ obrigatório | ❌ | ✅ |
| henrico.works | ✅ | ✅ | ✅ copy/pos. | ✅ | ✅ | ✅ principal | ✅ obrigatório | ✅ | ❌ |
| CondoLogPro | ✅ | ✅ | ✅ produto | ✅ | ✅ | ✅ principal | ✅ obrigatório | ❌ | ❌ |
| PersonalOps | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ principal | 🔲 depende | 🔲 depende | 🔲 depende |
