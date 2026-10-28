# AGENTS.md — regras para qualquer agente neste repositório

Leia este arquivo inteiro antes de qualquer tarefa. Ele vale para Claude Code, Codex, Antigravity e Cursor.

## Como trabalhar
1. **Nunca comece pelo código.** Procure a spec em `docs/specs/`. Sem spec, crie uma a partir de `docs/spec-template.md` e pare para aprovação.
2. **Proponha o plano** (arquivos tocados, migrações, testes) e espere "ok" humano antes de editar.
3. **Mudança mínima.** Não refatore o que a spec não pede. Não renomeie sem motivo.
4. **Prove.** Toda regra de negócio nova ganha teste. Rode `npm run lint` e `npm test` antes de dizer que terminou.
5. **Registre.** Atualize `TASKS.md` (Feat / Fix / Implementação) e, se escolheu entre alternativas, crie um ADR em `docs/decisions/`.
6. **Na dúvida, pergunte.** Requisito ambíguo é pergunta, não suposição. Nunca invente regra de negócio, número ou endpoint.

## Stack e convenções (preencha por projeto)
- Next.js (App Router) + TypeScript estrito · Prisma + PostgreSQL · NextAuth · Tailwind + shadcn/ui
- Rotas com Prisma declaram `export const runtime = 'nodejs'`
- No App Router, `params` é uma Promise: sempre `await params`
- Banco evolui **somente por migrations versionadas**; nunca edite o banco à mão
- Auditoria passa por um serviço central (ex.: `registrarAuditoria()`); rotas não gravam log por conta própria
- Regras de ciclo de vida ficam explícitas (máquina de estados), não espalhadas em `if`
- Integrações externas são disparadas por regra de negócio e não bloqueiam o fluxo principal
- Tema escuro: use `resolvedTheme`, não `theme`
- Textos de interface em português; código e commits em inglês

## Proibido
- Ler, imprimir ou commitar `.env`, chaves ou credenciais
- Dados reais de pessoas em seeds, testes, prints ou exemplos — use dados fictícios
- Escrever em sistemas que a spec define como somente leitura (ex.: bases legadas acessadas só por `SELECT`)
- Desativar testes ou lint para "passar"

## Definição de pronto
- [ ] Critérios Dado/Quando/Então da spec atendidos
- [ ] Lint e testes verdes
- [ ] Migração versionada, se houve mudança de schema
- [ ] `TASKS.md` atualizado
- [ ] Nenhum dado real ou segredo no diff
