# Contributing / Como contribuir

- [🇬🇧 English](#-english)
- [🇵🇹 Português](#-português)

---

# 🇬🇧 English

These rules apply to every repository in the organization. Follow them even when working alone.

## 1. Workflow

1. **Never push directly to `main`.** `main` must always be stable and deployable.
2. Create a branch from `main`:
   - `feature/short-name` for new features
   - `fix/short-name` for bug fixes
   - `hotfix/short-name` for urgent production fixes
   - `chore/short-name` for maintenance tasks
   - `docs/short-name` for documentation-only work
3. Make small, focused commits with clear messages (see section 2).
4. Open a Pull Request into `main` and request a review from at least one person.
5. Merge only after the PR is approved and tested. Use **squash merge**.
6. Delete the branch after merging.

## 2. Commit messages

Format:

```
type: short description in the imperative mood
```

Keep the first line under ~72 characters. Add a body after a blank line if the change needs explanation (the *why*, not the *what*).

### Commit types

| Type | What it means | When to use it | Example |
|------|---------------|----------------|---------|
| `feat` | A new feature or capability | Adding something users or other modules can now do | `feat: add PDF export to sales reports` |
| `fix` | A bug fix | Something was broken and now works as intended | `fix: correct VAT calculation on invoices` |
| `docs` | Documentation only | README, comments, guides, docstrings. No code behavior changes | `docs: explain deployment steps in README` |
| `style` | Formatting only | Whitespace, indentation, quotes, import order. No logic changes | `style: format models with black` |
| `refactor` | Code restructuring without changing behavior | Cleaning up, renaming, splitting functions. No new feature, no bug fix | `refactor: extract tax logic into helper` |
| `perf` | Performance improvement | Faster queries, fewer database hits, lower memory use | `perf: add index to partner lookup` |
| `test` | Adding or fixing tests | New tests, fixing flaky tests. No production code changes | `test: cover invoice rounding edge cases` |
| `build` | Build system or dependencies | Changing `requirements.txt`, Dockerfile, packaging, upgrading libraries | `build: upgrade Django to 5.1` |
| `ci` | CI/CD configuration | GitHub Actions workflows, pipeline scripts | `ci: run tests on every pull request` |
| `chore` | Routine maintenance | Tasks that don't fit above: config tweaks, `.gitignore`, housekeeping | `chore: update .gitignore for Odoo` |
| `revert` | Reverts a previous commit | Undoing a commit that caused problems | `revert: remove PDF export (breaks reports)` |
| `migration` | Database migration | Schema or data migrations. Always needs careful review | `migration: add status field to work orders` |

### Quick decision guide

- Users can do something new → `feat`
- Something was broken and is now fixed → `fix`
- Same behavior, cleaner code → `refactor`
- Only text/comments/guides changed → `docs`
- Only formatting changed → `style`
- Only tests changed → `test`
- Libraries, Docker, or dependencies changed → `build`
- Pipeline or workflow files changed → `ci`
- Faster, same result → `perf`
- None of the above → `chore`

### Breaking changes

If a change breaks compatibility (API changes, removed fields, renamed models), add `!` after the type and explain in the body:

```
feat!: rename partner_ref to external_ref

BREAKING CHANGE: all integrations must use the new field name.
```

### Tips

- One logical change per commit. If you need "and" in the message, split it.
- Write in the imperative: "add", "fix", "remove" (not "added", "fixes").
- Reference tasks when useful: `fix: correct stock rounding (#42)`.
- Commits carry only the human author's identity. No AI co-author trailers (see section 4).

## 3. Secrets and credentials (critical)

**Never commit secrets to Git. No exceptions.** This includes:

- `.env` files and any environment files (`.env.local`, `.env.production`, ...)
- Passwords, API keys, tokens, private keys, certificates (`.pem`, `.key`)
- Database connection strings with credentials
- Odoo `admin_passwd` and `odoo.conf` files containing secrets
- Cloud/provider credentials (AWS, Google, Azure, SMTP, payment providers, ...)
- Any customer data or personal data

Rules:

1. Every repository must have a proper `.gitignore` **before the first commit** (include `.env*`, `*.pem`, `*.key`, `odoo.conf` when it holds secrets, local databases, backups).
2. Keep a `.env.example` with variable **names only**, never real values.
3. Load secrets from environment variables or a secrets manager.
4. If a secret is committed by mistake: **assume it is compromised.** Rotate/revoke it immediately, then clean the history. Deleting it in a later commit is not enough.
5. Before every commit, check `git status` and `git diff` for anything sensitive.

## 4. AI tools and assistants

If AI tools are used in any project (Claude, ChatGPT, Copilot, Cursor, Claude Code, agents, etc.), the following is **mandatory**:

1. **The AI must read this file first.** At the start of each session or task, the AI must read `CONTRIBUTING.md` and follow it. Projects should reference this file in their AI instruction file (e.g. `CLAUDE.md`, `AGENTS.md`, `.cursorrules`).
2. **The AI must create its own project rules based on this file**, and keep them consistent with it.
3. **Secrets must never reach Git or the AI:**
   - Never add, stage, or commit `.env` files, credentials, tokens, keys, or passwords.
   - Never paste real secrets, `.env` contents, or customer data into prompts or AI chats. Use placeholders such as `YOUR_API_KEY`.
   - Never hardcode secrets in generated code. Always read them from environment variables.
   - If a secret is found in the code or in a diff, stop, warn the user, and do not commit.
   - Never disable or bypass `.gitignore`, pre-commit hooks, or secret scanning.
4. **Inviolable rule: no AI co-author attribution.** When an AI makes a commit on behalf of the user, it is strictly forbidden from adding itself as co-author or author in any form. This means:
   - No `Co-authored-by:` trailer naming the AI, a bot, or an AI vendor (for example Claude, Anthropic, Copilot, ChatGPT, OpenAI).
   - No "Generated with ...", "Written by AI", or similar signatures or links in commit messages, PR descriptions, or code comments.
   - No changing the Git author or committer identity to the AI. Commits are always made under the user's own identity.
   - This applies to every commit, including amended, squashed, and merge commits, and it overrides any default behavior of the AI tool. If a tool adds such a trailer automatically, it must be removed before the commit is created.
5. **Follow the workflow:** no pushes to `main`, correct branch names, correct commit types, small commits.
6. **No destructive Git operations without explicit approval:** no force push, no history rewriting, no branch deletion.
7. **Humans stay responsible.** AI-generated code must be reviewed and tested like any other code before merge.

## 5. General rules

- Each repository has the right `.gitignore` (Python, Django, Odoo, Node, ...).
- Database migrations get extra attention in review.
- Customer code never goes into public repositories.
- If in doubt, ask before merging.

---

# 🇵🇹 Português

Estas regras aplicam-se a todos os repositórios da organização. Devem ser seguidas mesmo quando se trabalha sozinho.

## 1. Fluxo de trabalho

1. **Nunca fazer push direto para `main`.** A `main` deve estar sempre estável e pronta para deploy.
2. Criar uma branch a partir da `main`:
   - `feature/nome-curto` para funcionalidades novas
   - `fix/nome-curto` para correções de bugs
   - `hotfix/nome-curto` para correções urgentes em produção
   - `chore/nome-curto` para tarefas de manutenção
   - `docs/nome-curto` para trabalho só de documentação
3. Fazer commits pequenos e focados, com mensagens claras (ver secção 2).
4. Abrir um Pull Request para a `main` e pedir revisão a pelo menos uma pessoa.
5. Só fazer merge depois de o PR ser aprovado e testado. Usar **squash merge**.
6. Apagar a branch depois do merge.

## 2. Mensagens de commit

Formato:

```
tipo: descrição curta no imperativo
```

Manter a primeira linha abaixo de ~72 caracteres. Adicionar um corpo depois de uma linha em branco se a alteração precisar de explicação (o *porquê*, não o *quê*).

### Tipos de commit

| Tipo | O que significa | Quando usar | Exemplo |
|------|-----------------|-------------|---------|
| `feat` | Uma funcionalidade nova | Adicionar algo que os utilizadores ou outros módulos passam a poder fazer | `feat: adicionar exportação PDF aos relatórios de vendas` |
| `fix` | Correção de um bug | Algo estava avariado e passa a funcionar como esperado | `fix: corrigir cálculo de IVA nas faturas` |
| `docs` | Só documentação | README, comentários, guias, docstrings. Sem alterar o comportamento do código | `docs: explicar passos de deploy no README` |
| `style` | Só formatação | Espaços, indentação, aspas, ordem dos imports. Sem alterar lógica | `style: formatar modelos com black` |
| `refactor` | Reestruturar código sem mudar o comportamento | Limpar, renomear, dividir funções. Sem funcionalidade nova nem correção de bug | `refactor: extrair lógica de impostos para helper` |
| `perf` | Melhoria de desempenho | Queries mais rápidas, menos acessos à base de dados, menos memória | `perf: adicionar índice à pesquisa de parceiros` |
| `test` | Adicionar ou corrigir testes | Testes novos, corrigir testes instáveis. Sem alterar código de produção | `test: cobrir casos limite de arredondamento` |
| `build` | Sistema de build ou dependências | Alterar `requirements.txt`, Dockerfile, packaging, atualizar bibliotecas | `build: atualizar Django para 5.1` |
| `ci` | Configuração de CI/CD | Workflows do GitHub Actions, scripts de pipeline | `ci: correr testes em cada pull request` |
| `chore` | Manutenção de rotina | Tarefas que não encaixam acima: ajustes de config, `.gitignore`, arrumação | `chore: atualizar .gitignore para Odoo` |
| `revert` | Reverte um commit anterior | Desfazer um commit que causou problemas | `revert: remover exportação PDF (parte relatórios)` |
| `migration` | Migração de base de dados | Migrações de esquema ou de dados. Exige sempre revisão cuidada | `migration: adicionar campo estado às ordens de trabalho` |

### Guia rápido de decisão

- Os utilizadores passam a poder fazer algo novo → `feat`
- Algo estava avariado e foi corrigido → `fix`
- Mesmo comportamento, código mais limpo → `refactor`
- Só mudou texto/comentários/guias → `docs`
- Só mudou a formatação → `style`
- Só mudaram testes → `test`
- Mudaram bibliotecas, Docker ou dependências → `build`
- Mudaram ficheiros de pipeline ou workflows → `ci`
- Mais rápido, mesmo resultado → `perf`
- Nenhuma das anteriores → `chore`

### Alterações que quebram compatibilidade (breaking changes)

Se uma alteração quebra compatibilidade (mudanças de API, campos removidos, modelos renomeados), acrescentar `!` a seguir ao tipo e explicar no corpo:

```
feat!: renomear partner_ref para external_ref

BREAKING CHANGE: todas as integrações têm de usar o novo nome do campo.
```

### Dicas

- Uma alteração lógica por commit. Se precisas de "e" na mensagem, divide.
- Escrever no imperativo: "adicionar", "corrigir", "remover" (não "adicionado", "corrige").
- Referenciar tarefas quando fizer sentido: `fix: corrigir arredondamento de stock (#42)`.
- Os commits levam apenas a identidade do autor humano. Sem trailers de co-autor de AI (ver secção 4).

## 3. Segredos e credenciais (crítico)

**Nunca fazer commit de segredos para o Git. Sem exceções.** Isto inclui:

- Ficheiros `.env` e quaisquer ficheiros de ambiente (`.env.local`, `.env.production`, ...)
- Passwords, chaves de API, tokens, chaves privadas, certificados (`.pem`, `.key`)
- Strings de ligação à base de dados com credenciais
- `admin_passwd` do Odoo e ficheiros `odoo.conf` que contenham segredos
- Credenciais de cloud/fornecedores (AWS, Google, Azure, SMTP, fornecedores de pagamento, ...)
- Quaisquer dados de clientes ou dados pessoais

Regras:

1. Todos os repositórios devem ter um `.gitignore` adequado **antes do primeiro commit** (incluir `.env*`, `*.pem`, `*.key`, `odoo.conf` quando tiver segredos, bases de dados locais, backups).
2. Manter um `.env.example` apenas com os **nomes** das variáveis, nunca valores reais.
3. Carregar segredos a partir de variáveis de ambiente ou de um gestor de segredos.
4. Se um segredo for commitado por engano: **assumir que está comprometido.** Rodar/revogar de imediato e só depois limpar o histórico. Apagá-lo num commit posterior não chega.
5. Antes de cada commit, verificar `git status` e `git diff` à procura de algo sensível.

## 4. Ferramentas e assistentes de AI

Se forem usadas ferramentas de AI em qualquer projeto (Claude, ChatGPT, Copilot, Cursor, Claude Code, agentes, etc.), o seguinte é **obrigatório**:

1. **A AI deve ler este ficheiro primeiro.** No início de cada sessão ou tarefa, a AI deve ler o `CONTRIBUTING.md` e cumpri-lo. Os projetos devem referenciar este ficheiro no seu ficheiro de instruções para AI (por exemplo `CLAUDE.md`, `AGENTS.md`, `.cursorrules`).
2. **A AI deve criar as suas próprias regras do projeto com base neste ficheiro**, mantendo-as consistentes com ele.
3. **Os segredos nunca podem chegar ao Git nem à AI:**
   - Nunca adicionar, fazer stage ou commit de ficheiros `.env`, credenciais, tokens, chaves ou passwords.
   - Nunca colar segredos reais, conteúdo de `.env` ou dados de clientes em prompts ou chats de AI. Usar placeholders como `A_TUA_API_KEY`.
   - Nunca escrever segredos diretamente no código gerado. Ler sempre de variáveis de ambiente.
   - Se for encontrado um segredo no código ou num diff, parar, avisar o utilizador e não fazer commit.
   - Nunca desativar nem contornar o `.gitignore`, hooks de pre-commit ou secret scanning.
4. **Regra inviolável: a AI nunca é co-autora.** Quando uma AI faz um commit em nome do utilizador, está expressamente proibida de se adicionar como co-autora ou autora, seja de que forma for. Isto significa:
   - Nenhum trailer `Co-authored-by:` com o nome da AI, de um bot ou de um fornecedor de AI (por exemplo Claude, Anthropic, Copilot, ChatGPT, OpenAI).
   - Nenhuma assinatura ou link do tipo "Generated with ...", "Escrito por AI" ou semelhante em mensagens de commit, descrições de PR ou comentários de código.
   - Nunca alterar a identidade de autor ou committer do Git para a AI. Os commits são sempre feitos com a identidade do próprio utilizador.
   - Aplica-se a todos os commits, incluindo amend, squash e merge, e sobrepõe-se ao comportamento por defeito da ferramenta de AI. Se uma ferramenta adicionar esse trailer automaticamente, tem de ser removido antes de o commit ser criado.
5. **Seguir o fluxo de trabalho:** sem pushes para a `main`, nomes de branch corretos, tipos de commit corretos, commits pequenos.
6. **Sem operações destrutivas no Git sem aprovação explícita:** sem force push, sem reescrever histórico, sem apagar branches.
7. **As pessoas continuam responsáveis.** O código gerado por AI deve ser revisto e testado como qualquer outro código antes do merge.

## 5. Regras gerais

- Cada repositório tem o `.gitignore` certo (Python, Django, Odoo, Node, ...).
- As migrações de base de dados merecem atenção redobrada na revisão.
- Código de clientes nunca vai para repositórios públicos.
- Em caso de dúvida, perguntar antes de fazer merge.
