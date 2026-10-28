# ai-harness-template

Template de repositório para desenvolver **com agentes de código sem cair em vibe coding**.
É o harness que uso no dia a dia com Claude Code, Codex, Antigravity e Cursor nos sistemas
que construo (gestão de ativos, agendamento de laboratórios, ERP, Pró-Bem).

> A IA entrega velocidade. O harness garante que ela entregue **dentro do padrão, uma vez só**.

## A ideia em 30 segundos

O agente nunca recebe "faz isso pra mim". Ele recebe **contexto, regras e um jeito de provar que acertou**:

| Camada | Arquivo | O que resolve |
|---|---|---|
| Regras do projeto | `AGENTS.md` (lido por Codex, Antigravity, Cursor) · `CLAUDE.md` (importa o AGENTS.md) | Stack, convenções e proibições valem para qualquer agente |
| Contexto da tarefa | `docs/specs/<feature>.md` a partir de `docs/spec-template.md` | Problema, regras de negócio, modelo de dados e critérios de aceite **antes** do código |
| Decisões | `docs/decisions/ADR-*.md` | Por que escolhemos A e não B — o agente não "redecide" a cada sessão |
| Habilidades | `.claude/skills/*` | Procedimentos repetíveis: spec primeiro, portão de revisão, changelog |
| Guardrails | `.claude/settings.json` | Bloqueia leitura de `.env`, roda lint e testes depois de cada edição |
| Observabilidade | `docs/observability.md` | Telemetria do agente via OpenTelemetry: custo, tokens e uso por sessão |
| Memória do projeto | `TASKS.md` | Changelog por data (Feat / Fix / Implementação) que o agente lê e atualiza |

## O ciclo

```
Dor de negócio ─► Spec (docs/specs) ─► Plano revisado por humano ─► Implementação pelo agente
      ▲                                                                     │
      └──── TASKS.md + ADR ◄── Revisão humana ◄── Lint + testes (hooks) ◄───┘
```

1. **Spec primeiro** — `/spec-first` transforma a demanda em spec com regras de negócio e critérios Dado/Quando/Então.
2. **Plano antes do código** — o agente propõe arquivos e passos; um humano aprova.
3. **Implementação guiada** — o agente só pode seguir as regras do `AGENTS.md` e da spec.
4. **Prova automática** — hooks rodam lint e testes depois de cada edição.
5. **Portão de revisão** — `/review-gate` confere a entrega contra a spec antes do PR.
6. **Memória** — `/changelog` registra o que mudou em `TASKS.md`.

## Como usar num projeto

```bash
npx degit felipesobrinho/ai-harness-template meu-projeto   # ou copie as pastas
```

1. Preencha a seção **Stack e convenções** do `AGENTS.md`.
2. Para cada feature, copie `docs/spec-template.md` para `docs/specs/<feature>.md`.
3. Peça ao agente: "leia a spec X, proponha o plano e espere minha aprovação".

## Resultados onde já foi aplicado

- Módulo de cálculo financeiro com previsão de **6 meses a 1 ano** entregue em **1 semana**.
- **300+ queries** otimizadas e 5+ módulos refatorados num ERP legado com revisão humana em cada PR.
- Plataforma de ativos de TI em produção com **361 ativos e 152 colaboradores**.
