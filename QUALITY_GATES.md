# QUALITY GATES — Henrico Agent OS

Última atualização: 2026-06-22

Este documento define os gates operacionais obrigatórios para qualquer sessão de trabalho com agentes de IA nos projetos de Henrico Amaral.

Gates não são sugestões. São pontos de parada com critério binário: passa ou bloqueia.

---

## Gate 0 — Abertura de sessão

**Objetivo:** Confirmar que o agente está operando no repositório correto, com estado limpo e contexto carregado antes de qualquer ação.

**Quando roda:** No início de toda sessão, sem exceção.

**Comandos obrigatórios:**
```bash
pwd                         # confirmar diretório
git status -sb              # estado do working tree
git branch --show-current   # branch ativa
git remote -v               # remote configurado
git log --oneline -5        # histórico recente
```

**Evidências esperadas:**
- Diretório dentro de `04_PROJETOS_CONTEÚDO`
- Branch declarada explicitamente (ex: `main`, `feature/X`)
- Remote `origin` apontando para o GitHub correto
- Working tree sem alterações não intencionais

**Critério de aprovação:**
- Todos os 5 comandos executados e reportados
- Diretório, branch e remote confirmados como esperados
- Nenhuma alteração pendente não prevista no escopo

**Critério de bloqueio:**
- Diretório incorreto (ex: raiz `04_PROJETOS_CONTEÚDO` diretamente)
- Branch errada para o tipo de tarefa
- Remote ausente ou apontando para repositório diferente
- Working tree sujo com arquivos não relacionados ao escopo

**Em caso de falha:**
1. Parar imediatamente.
2. Reportar o problema ao usuário.
3. Não editar nenhum arquivo até que o estado seja corrigido.

---

## Gate 1 — Escopo

**Objetivo:** Confirmar que o escopo da sessão está declarado, entendido e delimitado antes de qualquer execução.

**Quando roda:** Após Gate 0, antes de qualquer edição.

**Evidências esperadas:**
- Escopo permitido listado explicitamente (quais arquivos, qual diretório, qual objetivo)
- Escopo bloqueado listado explicitamente (o que não pode ser tocado)
- Referência ao `HANDOFF.md` ou `AGENTS.md` do projeto como fonte de escopo

**Critério de aprovação:**
- Agente consegue responder: "quais arquivos posso alterar nesta sessão?" sem perguntar ao usuário
- Agente consegue responder: "o que está fora do escopo?" sem perguntar ao usuário
- Nenhuma tarefa do tipo "melhore tudo" ou "resolva o projeto"

**Critério de bloqueio:**
- Escopo vago ou ambíguo (ex: "fazer deploy", "melhorar o site")
- Ausência de `AGENTS.md` ou `HANDOFF.md` no projeto-alvo quando a tarefa é não trivial
- Usuário não declarou o que pode e o que não pode ser tocado

**Em caso de falha:**
1. Solicitar clarificação de escopo ao usuário.
2. Não editar arquivos.
3. Propor uma lista de escopo para aprovação antes de prosseguir.

---

## Gate 2 — Segurança

**Objetivo:** Garantir que nenhum dado sensível seja exposto, commitado ou processado de forma insegura.

**Quando roda:** Antes de qualquer commit. Obrigatório em projetos com PII (CondoLogPro, PersonalOps).

**Comandos:**
```bash
git diff --cached --stat        # revisar o que está no staging
git diff HEAD -- .env           # nunca deve existir em staging
grep -r "sk-" --include="*.js" . 2>/dev/null   # chaves OpenAI
grep -r "ghp_" --include="*.md" . 2>/dev/null  # tokens GitHub
```

**Evidências esperadas:**
- Nenhum arquivo `.env`, `.pem`, `.key`, `*.secret` no staging
- Nenhuma chave de API hardcoded em arquivos modificados
- Nenhum dado de cliente (CPF, e-mail, endereço) em arquivos de código ou doc

**Critério de aprovação:**
- `git diff --cached` não contém arquivos sensíveis
- Skill `private-data-scanner` executada e sem alertas
- `.gitignore` do projeto cobre os padrões críticos

**Critério de bloqueio:**
- Qualquer arquivo `.env` ou equivalente detectado no staging
- Qualquer token, senha ou chave hardcoded no diff
- Dados de clientes ou moradores em arquivos de código ou documentação

**Em caso de falha:**
1. Executar `git reset HEAD <arquivo>` para remover do staging.
2. Adicionar o arquivo ao `.gitignore`.
3. Se dados já foram commitados anteriormente: parar, notificar o usuário, avaliar revoke de credenciais.

---

## Gate 3 — Alteração

**Objetivo:** Garantir que cada alteração é intencional, mínima e coerente com o escopo declarado.

**Quando roda:** Antes de commitar. Após cada bloco de alterações.

**Comandos:**
```bash
git diff --stat             # resumo de arquivos alterados
git diff                    # conteúdo das alterações
```

**Evidências esperadas:**
- Cada arquivo alterado tem justificativa explícita no escopo
- Nenhum arquivo alterado que não foi declarado no Gate 1
- Alterações agrupadas por tipo (não misturar docs + código + config no mesmo commit)

**Critério de aprovação:**
- Todos os arquivos no diff estão dentro do escopo declarado
- O agente consegue justificar cada arquivo alterado em uma frase
- Não há alterações colaterais não intencionais

**Critério de bloqueio:**
- Arquivo fora do escopo aparece no diff
- Múltiplos tipos de alteração misturados sem justificativa
- Qualquer arquivo de outro projeto aparece no diff

**Em caso de falha:**
1. Executar `git checkout -- <arquivo>` para reverter alteração não intencional.
2. Separar as alterações em commits distintos por tipo.
3. Reportar ao usuário antes de prosseguir.

---

## Gate 4 — Visual/Design

**Objetivo:** Garantir que alterações de UI não violam o padrão estético definido no `DESIGN.md` do projeto.

**Quando roda:** Sempre que o diff inclui arquivos de UI (`.html`, `.css`, `.astro`, `.tsx`, `.jsx`, componentes).

**Evidências esperadas:**
- `DESIGN.md` do projeto existe e foi lido antes da alteração
- Skill `anti-generic-ui-reviewer` foi consultada
- Nenhuma cor CSS nomeada básica (`red`, `blue`, `green`) usada diretamente
- Tipografia usa fontes declaradas no design system (Inter, Outfit ou equivalente definido)
- Nenhum layout "bootstrap-style" (Navbar + Hero + 3 Cards sem variação)

**Critério de aprovação:**
- Preview visual confirmado localmente
- Contraste de texto aprovado (regra: texto difícil de ler = falha estética)
- Animações têm propósito funcional (guiam o olhar ou confirmam ação)

**Critério de bloqueio:**
- Projeto sem `DESIGN.md` → gerar `DESIGN.md` antes de qualquer alteração visual
- Cores hardcoded fora do design system
- Layout genérico sem diferenciação

**Em caso de falha:**
1. Reverter alteração visual.
2. Ativar `design-md-generator` para criar o North Star visual.
3. Só retomar implementação após `DESIGN.md` aprovado.

---

## Gate 5 — Build/Teste

**Objetivo:** Confirmar que o código funciona no ambiente local antes de qualquer push.

**Quando roda:** Antes de commitar em projetos com build (Next.js, Astro, Vite).

**Comandos por projeto:**

```bash
# Portfolio (HTML/CSS/JS puro)
# abrir index.html no browser e validar manualmente

# henrico-works (Astro)
npm run build       # deve completar sem erros
npm run preview     # validar resultado localmente

# CondoLogPro (Next.js + Prisma)
npx prisma validate
npm run build
# testar fluxo crítico: cadastro de encomenda, consulta de morador

# PersonalOps
# dependente da stack atual do projeto
```

**Evidências esperadas:**
- Build completa sem erros fatais
- Fluxo crítico funciona no ambiente local
- Nenhum erro de TypeScript ou Prisma schema em projetos tipados

**Critério de aprovação:**
- Build passou sem `error` (warnings aceitos com justificativa)
- Fluxo principal testado manualmente e funcionando

**Critério de bloqueio:**
- Build falhando com erro fatal
- Fluxo crítico quebrado
- Erro de tipagem ou schema não resolvido

**Em caso de falha:**
1. Ativar skill `build-failure-resolver`.
2. Diagnosticar e corrigir antes do commit.
3. Nunca commitar código com build quebrado, exceto em branch de diagnóstico explícita.

---

## Gate 6 — Git

**Objetivo:** Garantir que o histórico Git permanece semântico, limpo e rastreável.

**Quando roda:** No momento do commit.

**Evidências esperadas:**
- Mensagem de commit no padrão: `type(scope): descrição curta`
  - Types válidos: `feat`, `fix`, `docs`, `chore`, `style`, `refactor`, `test`, `perf`
  - Scope: nome do arquivo ou módulo principal alterado
  - Ex: `docs(QUALITY_GATES): add pre-commit and pre-push gates`
- Um commit por tipo de alteração (não misturar)
- Branch adequada ao tipo de tarefa (não trabalhar direto na `main` em mudanças estruturais)

**Comandos:**
```bash
git add <arquivos-específicos>   # nunca git add .
git diff --cached --stat         # revisar staging final
git commit -m "type(scope): descrição"
git log --oneline -3             # confirmar commit criado corretamente
```

**Critério de aprovação:**
- Commit criado com mensagem semântica
- Staging contém apenas o que foi revisado no Gate 3
- Histórico linear sem merges desnecessários

**Critério de bloqueio:**
- Mensagem de commit vaga ("update", "fix stuff", "wip")
- `git add .` sem revisão prévia do `git diff`
- Commit com arquivos de múltiplos escopos sem justificativa

**Em caso de falha:**
1. Usar `git commit --amend` se o commit ainda não foi publicado.
2. Usar `git reset HEAD~1` para desfazer o último commit e recriar com escopo correto.

---

## Gate 7 — Pré-push

**Objetivo:** Última revisão antes de publicar no remote.

**Quando roda:** Imediatamente antes de `git push`.

**Comandos:**
```bash
git log --oneline origin/main..HEAD    # commits que serão publicados
git diff origin/main --stat            # arquivos que serão publicados
git status -sb                         # confirmar working tree limpo
```

**Evidências esperadas:**
- Apenas commits esperados na fila de push
- Nenhum arquivo sensível nos commits
- Working tree limpo (sem alterações pendentes não commitadas)
- Branch correta para o remote destino

**Critério de aprovação:**
- Lista de commits publicados revisada e aprovada
- Gate 2 (segurança) já passou
- Usuário autorizou o push (ou push faz parte do escopo declarado)

**Critério de bloqueio:**
- Commits inesperados na fila
- Dados sensíveis identificados
- Push para `main` de mudança estrutural sem PR

**Em caso de falha:**
1. Não executar `git push`.
2. Usar `git reset HEAD~N` para remover commits problemáticos.
3. Reportar ao usuário antes de qualquer ação destrutiva.

---

## Gate 8 — Fechamento/Memória

**Objetivo:** Garantir que toda sessão termina com estado documentado e rastreável.

**Quando roda:** No encerramento de toda sessão.

**Evidências esperadas:**
- `memory/operational-log.md` atualizado com:
  - Arquivos alterados e motivo
  - Decisões tomadas
  - Validações executadas
  - Commit e hash final
  - Pendências para próxima sessão
- `git status -sb` limpo (`## main...origin/main`)
- Nenhum arquivo untracked relevante esquecido

**Comandos:**
```bash
git status -sb                  # estado final
git log --oneline -3            # confirmar commits publicados
```

**Critério de aprovação:**
- Log atualizado com conteúdo factual (não "sessão concluída")
- Working tree limpo
- Pendências documentadas, não apenas mencionadas verbalmente

**Critério de bloqueio:**
- Sessão encerrada sem log
- Decisões tomadas sem registro
- Arquivos alterados não documentados

**Em caso de falha:**
1. Criar log retroativo antes de encerrar.
2. Documentar o que foi feito, mesmo que parcialmente.
3. Nunca encerrar sessão com memória vazia após execução real.

---

## Resumo dos gates

| Gate | Nome | Quando |
|---|---|---|
| 0 | Abertura de sessão | Início de toda sessão |
| 1 | Escopo | Antes de qualquer edição |
| 2 | Segurança | Antes de todo commit |
| 3 | Alteração | Antes de commitar, após edições |
| 4 | Visual/Design | Quando diff inclui UI |
| 5 | Build/Teste | Antes de commitar em projetos com build |
| 6 | Git | No momento do commit |
| 7 | Pré-push | Antes de `git push` |
| 8 | Fechamento/Memória | Encerramento de toda sessão |
