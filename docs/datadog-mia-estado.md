# Estado de Observabilidad - MIA Agente IA (Datadog)

**Servicio principal:** `ciencuadras-agentes-2-0-ia-ms`
**Servicio legacy:** `ciencuadras-agentes-ia-ms`
**Team:** ciencuadras

## Monitores (10 total)

### Servicio: `ciencuadras-agentes-2-0-ia-ms`

| Monitor | Estado | Metrica | Prioridad |
|---------|--------|---------|----------|
| Alta tasa de error | OK | error rate > 50% (10m) | P2 |
| Nuevo error (Error Tracking) | OK | Nuevos errores > 1 (5m) | P2 |
| Latencia alta (p90) | OK | p90 >= 60s (10m) | P2 |
| Ausencia de trafico | No Data | hits < 1 (10m) | P1 |
| Cambio anormal rendimiento | OK | Anomalias (4h, agile, weekly) | P1 |

## Dependencias Downstream

| Dependencia | Tipo |
|-------------|------|
| `us.cloud.langfuse.com` | Externo - Observabilidad LLM |
| `ciencuadras-zona-privada-ms` | Interno |
| `ciencuadras-java-descripciones-ms` | Interno |
| `ciencuadras-modelos-ia-ms` | Interno |
| `google.cloud.aiplatform.v1beta1.predictionservice` | Externo - Vertex AI |

## Recomendaciones

1. Crear dashboard dedicado para MIA
2. Agregar monitor de latencia a Vertex AI
3. Revisar estado No Data en monitores de trafico
4. Consolidar servicios duplicados
5. Agregar SLOs formales
