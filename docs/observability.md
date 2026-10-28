# Observabilidade do agente

O Claude Code exporta métricas e eventos via **OpenTelemetry**. Com isso dá para medir custo,
tokens, sessões e uso de ferramentas por pessoa e por projeto.

```bash
export CLAUDE_CODE_ENABLE_TELEMETRY=1
export OTEL_METRICS_EXPORTER=otlp
export OTEL_LOGS_EXPORTER=otlp
export OTEL_EXPORTER_OTLP_PROTOCOL=grpc
export OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4317
```

Use um coletor OTLP (Grafana, Honeycomb, Datadog ou o seu próprio) e acompanhe:

| Métrica | Pergunta que responde |
|---|---|
| Custo e tokens por sessão | Quanto custa cada feature? |
| Linhas alteradas e commits | O agente está entregando ou só conversando? |
| Decisões de permissão | Onde os guardrails estão segurando o agente? |

Um relatório semanal consolida esses números para o time (ver `rag-captacao-demo`).
