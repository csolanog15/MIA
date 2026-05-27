# 🤖 Inventario Funcional & Estado del Arte: MIA Agente IA

**Asistente Inmobiliaria Inteligente | Python + LangGraph + Gemini 2.0 | Langfuse + Datadog**

---

## 📊 Vista Ejecutiva y Salud del Sistema

| Indicador | Valor |
|-----------|-------|
| **Prompts** | 46 |
| **Agentes Core** | 4 |
| **Agentes Outbound** | 5+ |
| **Integraciones** | 7 |
| **Tools** | 12 |
| **Repos** | 4 |
| **Canales** | 4 |
| **Issues Jira** | 2,848+ |
| **Equipo** | 5 personas |
| **Sesiones** | 928K+ |

### Semáforo de Estado

| Nivel | Cantidad | Detalle |
|-------|----------|---------|
| 🔴 Críticos | 5 | Safety settings, PII logging, monitores incorrectos, sin circuit breaker Langfuse, etiquetas expuestas |
| 🟠 Advertencias | 7 | Latencia, Single AZ, image tag, error handling, print(), Flask, insistencia crédito |
| 🟢 Tests E2E | 8/12 OK | Router, Search, get_property_info, paginate, substitutes, VIS, POI, FAQ/RAG |

### Indicadores de Satisfacción

| Métrica | Valor Acumulado 2026 | Abril 2026 | Estado |
|---------|---------------------|------------|--------|
| **INS** | -5 | -82 | 🔴🚨 CATASTRÓFICO |
| **NPS** | -7 | -90 | 🔴🚨 CATASTRÓFICO |

### Métricas Datadog (últimos 7 días)

| Métrica | Valor |
|---------|-------|
| Requests/día | 1,420 |
| Errores (7d) | 158 (95% Langfuse 502) |
| Latencia máxima | 30.8s |

---

## 💼 Track de Producto y Procesos de Negocio

### Flujos Core

**Inbound:**
```
Usuario ──> Router ──> Search Agent ──> [Muestra inmuebles] ──> Profiler ──> save_lead_to_zoho
```

**Outbound Davivienda:**
```
Sistema contacta preaprobado ──> Sales Agent ──> Propósito ──> Urgencia ──> Validación financiera ──> Agendar ──> Sustitutos
```

**Aliados Venta:**
```
Lead aliado ──> Sales Allies Agent ──> search_sales_allies_properties ──> save_lead_to_zoho
```

**Aliados Arriendo:**
```
Lead aliado ──> Rent Allies Agent ──> search_rent_allies_properties ──> save_lead_to_zoho
```

**FAQ/RAG:**
```
Usuario pregunta ──> Router ──> FAQ Agent ──> search_faqs (RedisVL) ──> search_rag (DuckDuckGo)
```

**Campañas IAValida:**
```
Trigger ──> Validación (7 reglas) ──> Selección template ──> Envío Infobip ──> Respuesta ──> Conversación MIA
```

### Canales

| Canal | Detalle |
|-------|---------|
| **Web** | ciencuadras.com/mia-asistente-inmobiliaria |
| **WhatsApp** | Formato optimizado sin Markdown. Sender 573153277577 (Quality HIGH, UNLIMITED) |
| **Outbound** | Contacto proactivo Davivienda |
| **Voz** | Canal telefónico vía Dapta |

### Análisis UX de Producción (Web vs WhatsApp)

Resultado de **12 pruebas E2E** en producción:

| Estado | Cantidad | Funcionalidades |
|--------|----------|-----------------|
| 🟢 Coinciden | 8/12 | Router, Search, get_property_info, paginate_search, search_substitutes, Filtro VIS, POI, FAQ/RAG |
| 🟠 Parcial | 2/12 | Response Question (nueva búsqueda en vez de filtrar), Guardrail off-topic (responde fuera del dominio) |
| 🔴 Bloqueados | 2/12 | Profiler y save_lead_to_zoho (intencional en web, solo WhatsApp) |

### Impacto en la Experiencia del Cliente (Hallazgos Críticos)

| ID | Severidad | Problema | Impacto |
|----|-----------|----------|---------|
| P1 | 🔴 | **Etiquetas internas expuestas:** mia_generic_agent responde "buscar_inmueble", "ninguna" al usuario | Confusión total, abandono |
| P2 | 🔴 | **Respuesta "ninguna" sin fallback:** Router no clasifica, sin escalamiento a humano | Frustración, pérdida de leads |
| P3 | 🟠 | **Perfilamiento ignora preguntas:** Script rígido, ignora preguntas fuera del flujo | Experiencia robótica |
| P4 | 🟠 | **Insistencia en crédito tras rechazo:** MIA insiste cuando el usuario dice NO | Irritación, NPS negativo |
| P5 | 🟠 | **JSON/PII expuestos al usuario:** Muestra JSON con nombre, cédula, teléfono, email | Riesgo regulatorio (Habeas Data) |

### Top Problemas Reportados por Usuarios (Encuestas)

| Frecuencia | Problema |
|-----------|----------|
| 864 | No me ayudó a avanzar, requiero asesor |
| 657 | Resultados que no coincidían |
| 487 | No entendió lo que le pedí |
| 313 | Tardó mucho en responder |
| 177 | Me pidió repetir información |
| 163 | Se desconectó o no siguió la conversación |

### INS/NPS Tendencia 2026

| Mes | Respuestas | INS | NPS | Estado |
|-----|-----------|-----|-----|--------|
| Enero | 1,476 | -9 | 8 | 🔴 |
| Febrero | 1,098 | 17 | -2 | 🟢 |
| Marzo | 860 | -4 | -12 | 🔴 |
| Abril | 765 | -82 | -90 | 🔴🚨 CRÍTICO |
| Mayo (parcial) | 311 | -10 | — | 🔴 |

---

## 💻 Track de Ingeniería, Arquitectura y DevOps

### Arquitectura del Sistema

| Capa | Tecnología | Versión |
|------|-----------|---------|
| Orquestación agentes | LangGraph (Supervisor + Swarm) | 0.6.4 |
| Framework LLM | LangChain + langchain-community | 0.2.14 / 0.3.27 |
| Modelo LLM | Google Gemini 2.0 (via LangChain) | — |
| Observabilidad LLM | Langfuse | 2.60.8 |
| APM | Datadog (ddtrace) | 3.10.2 |
| Web Framework | Flask (async) | 2.3.3 |
| Persistencia estado | MongoDB (langgraph-checkpoint) | — |
| Cache/Vectores | Redis + RedisVL | 6.2 / 0.7 |
| Búsqueda web (RAG) | DuckDuckGo Search | 5.0+ |
| AWS | boto3 | 1.37 |
| Lib interna | ia-transversal-langchain-python-lib | 2.6.3 |
| Testing | pytest + pytest-cov + pytest-mock | 8.0.1 |
| CI/CD | GitHub Actions | — |
| Contenedores | Docker + docker-compose | — |

### Repositorios

| Repo | Lenguaje | Framework | Creado | Descripción |
|------|----------|-----------|--------|-------------|
| ciencuadras-agentes-2-0-ia-ms | Python 3.11+ | Flask + LangGraph | May 2025 | Cerebro de MIA: orquestación multi-agente |
| ciencuadras-mcp-inmuebles-ia-ms | Python | Flask | May 2025 | Tools MCP: búsqueda de inmuebles |
| ciencuadras-modelos-ia-ms | Java (Gradle) | Spring Boot | Sep 2023 | Modelos IA v1 (legacy, aún activo) |
| ciencuadras-admin-prompts-ia-ms | Python | Flask | Oct 2023 | Administración de prompts (Langfuse) |

### Gobierno de Prompts (Langfuse) — 47 prompts

**Agentes Core:**

| Agente | Prompt ID | Función |
|--------|-----------|---------|
| Router Principal | `mia_router_agent_prod_gemini_1` | Clasifica intención → search, profiler, faq_rag |
| Search | `mia_search_agent_prod_gemini_1` | Búsqueda de inmuebles |
| Profiler | `mia_profiler_agent_prod_gemini_1` | Captura datos, agendamiento, save_lead_to_zoho |
| FAQ/RAG | `mia_faq_rag_agent_prod_gemini_1` | Preguntas frecuentes con search_faqs + search_rag |
| Evaluation | `mia_evaluation_agent_prod_gemini_1` | Evalúa calidad (JSON: feedback, sentiment, lead_sent, error) |
| MIA 3.0 | `MIA 3.0` | Conversacional completo con enfoque emocional |
| Perfiladora | `mia_perfiladora_conversacion_prod_gemini_1` | Perfilamiento detallado v2 |

**Agentes Outbound:**

| Agente | Prompt ID | Función |
|--------|-----------|---------|
| Vendedora | `mia_vendedora_conversacion_prod_gemini_1` | Venta a preaprobados Davivienda |
| Sales Agent | `mia_sales_agent_prod_gemini_1` | Ventas directas con property_code |
| Sales Allies | `mia_sales_allies_agent_prod_gemini_1` | Ventas aliados |
| Rent Allies | `mia_rent_allies_agent_prod_gemini_1` | Arriendo aliados |
| Outbound v2 | `mia_2_outbound_conv_001_prod_gemini_1` | Contacto saliente crédito (legacy activo) |
| Search Sales Allies | `mia_search_sales_allies_agent_prod_gemini_1` | Búsqueda para aliados venta |
| Search Rent Allies | `mia_search_rent_allies_agent_prod_gemini_1` | Búsqueda para aliados arriendo |

**Routers especializados (5):** sales_faq_router, sales_allies_router, rent_allies_router, search_allies_router, router_general

**Extractores (5):** extract_sales, extract_sales_allies, extract_rent_allies, extract_allies_data, vendedora_extraer_datos

**Utilidades (2):** extract_features_from_description, response_question_property

**Legacy v1 (8 prompts):** mia_1_* — chains con clasificación + extracción, modelo dual Gemini/GPT-3.5

**Legacy v2 (10 prompts):** mia_2_* — routers sofisticados, outbound, perfil con validación

### Tools (12 confirmadas)

| Tool | Agente(s) | Función |
|------|-----------|---------|
| search_properties | Search Agent | Búsqueda catálogo general |
| search_sales_allies_properties | Search Sales Allies | Inventarios aliados (venta) |
| search_rent_allies_properties | Search Rent Allies | Inventarios aliados (arriendo) |
| search_substitutes_properties | Vendedora, Sales Agent | Inmuebles sustitutos |
| paginate_search | Todos los Search + Vendedora | Siguiente página |
| get_property_info | Profiler, Sales, Allies, Rent | Info detallada por código |
| get_appointment | Profiler, Sales Allies, Rent Allies | Disponibilidad horarios |
| validate_appointment_date | Profiler, Sales Allies, Rent Allies | Valida fecha/hora |
| validate_financial_capacity | Vendedora, Sales, Sales Allies | Compara preaprobado vs valor |
| save_lead_to_zoho | Todos los agentes de cierre | Guarda lead en Zoho CRM |
| search_faqs | FAQ/RAG Agent | Búsqueda semántica RedisVL |
| search_rag | FAQ/RAG Agent | Búsqueda web DuckDuckGo |

### Integraciones

| Sistema | Propósito | Tipo |
|---------|-----------|------|
| n8n | Orquestador de flujos | Orquestación |
| Zoho CRM | Gestión de leads | CRM |
| Salesforce Data Cloud | Plataforma de datos | Data Platform |
| Davivienda | Créditos preaprobados | Financiero |
| Catálogo Ciencuadras | Búsqueda de inmuebles | Core |
| Redis + RedisVL | Cache + Vector Store RAG | Infraestructura |
| Dapta | Canal de voz | Canal |
| Langfuse | Prompt management + observabilidad | Plataforma IA |
| Google Gemini | Modelo LLM principal | IA/ML |
| Datadog | APM, métricas, trazas | Observabilidad |

### Infraestructura AWS (ECS Fargate)

| Componente | Valor |
|-----------|-------|
| Cluster | ms-internal-prod-ecs-cluster |
| Service | ciencuadras-prod-python-asistente-2-0-ia-ms |
| Task Definition | v9 |
| Región | us-east-1 (single AZ: us-east-1b) |
| Runtime | Python (Flask 2.3.3 + httpx 0.28.1) |
| Image | ECR `:latest` (no inmutable) |
| Auth | AWS Cognito (JWT) para APIs internas |

**Topología:**

```
[Usuario] ──> [WhatsApp / Web / Voz (Dapta)]
                    │
            [Infobip Webhook] ──> [n8n Orquestador]
                    │
            [Flask API - 11 Blueprints]
                    │
    ┌───────────────┼───────────────┐
    ▼               ▼               ▼
[Supervisor]    [Swarm]        [Agentes directos]
    │               │
    ▼               ▼
[Gemini 2.0]    [Gemini 2.5 + thinking]
    │               │
    └───────┬───────┘
            ▼
[Tools: Zoho, MCP Inmuebles, Appointments]
            │
[MongoDB checkpoints] + [Redis cache/vectores]
            │
[Langfuse prompts] + [Datadog APM]
```

### Métricas Operativas (Datadog APM — últimos 7 días)

| Endpoint | Requests/día | Tipo |
|----------|-------------|------|
| POST /ia-assistant/mia-generic/chat | 1,420 | Principal |
| POST /ia-assistant/mia-router/chat | 630 | Router |
| GET /ia-assistant/actuator/health | 304 | Health check |
| POST /ia-assistant/mia-rent-allies/extract_data | 37 | Extractor |
| POST /ia-assistant/mia-sales/extract_data | 4 | Extractor |

### Auditoría de Código y Seguridad (Deuda Técnica)

**🔴 Críticos:**

| # | Hallazgo | Riesgo |
|---|----------|--------|
| 1 | **Safety settings BLOCK_NONE:** Gemini sin filtros de seguridad | Contenido inapropiado |
| 2 | **Logging de PII:** zoho_server_tool loguea payload completo del lead | Violación Habeas Data |
| 3 | **Monitores métrica incorrecta:** trace.servlet.request.hits (Java) en servicio Python | "No Data" permanente |
| 4 | **Sin circuit breaker Langfuse:** 158 errores 502 en 7 días | Disponibilidad cero |
| 5 | **Etiquetas internas expuestas al usuario** (P1) | Abandono inmediato |

**🟠 Advertencias:**

| # | Hallazgo | Impacto |
|---|----------|---------|
| 1 | Umbral latencia 60s (debería ser 15s) | Alertas no detectan degradación |
| 2 | Single AZ (us-east-1b) | Single point of failure |
| 3 | Image tag :latest (no inmutable) | Rollbacks difíciles |
| 4 | Sin circuit breaker general | Cascada de fallos |
| 5 | Error handling inconsistente | Comportamiento impredecible |
| 6 | print() en vez de logger | Sin observabilidad |
| 7 | Flask (no FastAPI) | Deuda técnica |

---

## 🚀 Plan de Acción y Roadmap de Optimización

| # | Acción | Impacto | Esfuerzo | Quick Win | Problema que resuelve |
|---|--------|---------|----------|-----------|----------------------|
| 1 | Ocultar etiquetas internas del router | ⭐⭐⭐⭐⭐ | Medio | ✅ | P1, P2 — Usuarios ven "buscar_inmueble" o "ninguna" |
| 2 | Escalamiento a humano | ⭐⭐⭐⭐ | Medio | ✅ | P2 — Sin fallback cuando router no clasifica |
| 3 | JSON como system message (no output) | ⭐⭐⭐ | Bajo | ✅ | P2, P5 — PII expuestos al usuario |
| 4 | Flexibilizar perfilamiento | ⭐⭐⭐⭐ | Alto | ❌ | P3, P4 — Script rígido, insistencia |
| 5 | Habilitar safety settings Gemini | ⭐⭐⭐⭐⭐ | Bajo | ✅ | Contenido inapropiado |
| 6 | Eliminar logging de PII | ⭐⭐⭐⭐ | Bajo | ✅ | Violación Habeas Data |
| 7 | Circuit breaker para Langfuse | ⭐⭐⭐⭐ | Medio | ❌ | 158 errores 502/semana |
| 8 | Corregir monitores Datadog | ⭐⭐⭐ | Bajo | ✅ | Monitores en "No Data" |
| 9 | Reducir umbral latencia a 15s | ⭐⭐⭐ | Bajo | ✅ | Alertas no detectan degradación |
| 10 | Multi-AZ | ⭐⭐⭐ | Alto | ❌ | Single point of failure |
| 11 | Image tag inmutable (commit SHA) | ⭐⭐ | Bajo | ✅ | Rollbacks difíciles |
| 12 | Guardrail off-topic | ⭐⭐⭐ | Medio | ❌ | Riesgo de marca |
| 13 | Investigar caída abril 2026 | ⭐⭐⭐⭐⭐ | Medio | ❌ | INS -82, NPS -90 |
| 14 | Implementar IAValida en n8n | ⭐⭐⭐ | Alto | ❌ | Campañas sin validación |

---

## 📎 Anexos

### Reglas de Negocio

| # | Regla | Detalle |
|---|-------|---------|
| 1 | Arriendo vs Compra | Presupuesto menor a 100M o rango mensual → Arriendo |
| 2 | VIS | proyecto=true, venta, máx $213.525.000 |
| 3 | Cuota inicial | Leasing 20%, Hipotecario 30% |
| 4 | Horarios visita | Lun-Vie 8am-5pm, Sáb 8am-12pm |
| 5 | Datos obligatorios | nombre, identificación, tipo doc, teléfono, email |
| 6 | Política privacidad | Mencionar antes de capturar datos |
| 7 | Contactos inmobiliaria | Solo DESPUÉS de save_lead_to_zoho |
| 8 | Formato WhatsApp | Asterisco para negritas, URLs texto plano |
| 9 | Sitios de interés | Salud, Educación, Transporte, Parque, CC, Supermercado |
| 10 | Validación financiera | Comparar preaprobado vs valor inmueble |
| 11 | Urgencia | Plazo mayor a 3 meses → proyectos vivienda nueva |
| 12 | Co-deudor | Crédito insuficiente → sugerir co-deudor |

### Equipo MIA

**Área:** Inteligencia Artificial - MIALAB | **Metodología:** Scrum (sprints 2 semanas) | **Jira:** MIA (2,848+ issues)

| Persona | Rol | Responsabilidades |
|---------|-----|-------------------|
| Daniela Lopera Hernández | IA Engineer | n8n, integraciones, prompts, tools, flujos |
| Julián Eduardo Rivera Cristancho | Backend / IA | Gemini, evaluaciones Langfuse, Lambda |
| Hernán Darío Castaño Ruiz | Dev / Scrum Master | Acompañamiento técnico, dailies |
| Daniel Sebastián Chavarría | Desarrollador | Ceremonias, soporte técnico |
| Carlos Andrés Patiño Vélez | PO / Líder técnico | Producto, priorización |

### Cobertura Geográfica

Bogotá, Medellín, Cali, Barranquilla, Bucaramanga, Cartagena, Pereira, Manizales, Ibagué, Neiva, Villavicencio, Cúcuta, Pasto, Santa Marta, Valledupar, Popayán y municipios aledaños.

### Infobip WhatsApp

| Parámetro | Valor |
|-----------|-------|
| Cuenta | G. BOLIVAR - Ciencuadras |
| API Base | 6jexvz.api.infobip.com |
| Balance | COP -40.4M (postpago) |
| Productos | Conversations (15/15 seats) + Answers (13,707/30,000 sessions) |
| Sender MIA | 573153277577 (Quality HIGH, UNLIMITED, WABA RICHNESTT SAS) |
| Templates MIA | 128 (121 approved, 7 rejected) |
| Templates totales | 786 (764 approved, 21 rejected, 1 pending) |

### LangGraph Graphs

| Graph | Descripción |
|-------|-------------|
| sales_agent_graph | Grafo de ventas directas |
| extract_data_agent_graph | Grafo de extracción de datos |
| profiler_agent_graph | Grafo de perfilamiento |
| search_agent_graph | Grafo de búsqueda |
| supervisor_agent_graph | Grafo supervisor (orquestador) |
| faq_rag_agent_graph | Grafo de FAQ con RAG |

---

*Actualizado: Mayo 2026 | Plataforma: Langfuse + LangGraph | Modelo: Google Gemini | Jira: MIA (2,848+ issues)*

*URL: https://www.ciencuadras.com/mia-asistente-inmobiliaria | Repo: segurosbolivar/ciencuadras-agentes-2-0-ia-ms*
