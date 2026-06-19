# Analisis de Repositorios - MIA Agente IA

## Resumen

| Repo | Rol | Tecnologia |
|------|-----|----------|
| `ciencuadras-agentes-2-0-ia-ms` | **PRINCIPAL** | Python 3.10+ / Flask / LangGraph / Gemini 2.0 |
| `ciencuadras-mcp-inmuebles-ia-ms` | Auxiliar - Servidor MCP | Python 3.12+ / Starlette / MCP Protocol |
| `ciencuadras-modelos-ia-ms` | Legacy (v1) | Java 11 / Spring Boot 2.4 |

## Repo Principal: `ciencuadras-agentes-2-0-ia-ms`

### Tecnologia

| Componente | Tecnologia |
|-----------|----------|
| Lenguaje | Python 3.10+ |
| Framework Web | Flask |
| Framework IA | LangGraph + LangChain |
| Modelo LLM | Gemini 2.0 (Google) |
| Observabilidad LLM | Langfuse |
| Observabilidad Infra | Datadog |
| Cache/Sesiones | Redis |
| Checkpointing | MongoDB |
| Almacenamiento | AWS S3 |
| Autenticacion | AWS Cognito (JWT) |
| CRM | Zoho |
| Vector DB | Pinecone |

### Endpoints de la API

| Endpoint | Agente |
|----------|--------|
| `POST /ia-assistant/mia-search/chat` | Search Agent |
| `POST /ia-assistant/mia-sales/chat` | Sales Agent |
| `POST /ia-assistant/mia-sales/extract_data` | Extract Agent |
| `POST /ia-assistant/mia-faq-rag/chat` | FAQ RAG Agent |
| `POST /ia-assistant/mia-profiler/chat` | Profiler Agent |
| `POST /ia-assistant/mia-supervisor/chat` | Supervisor Agent |
| `POST /ia-assistant/mia-swarm/chat` | Swarm Agent |

### Grafos LangGraph

| Grafo | Entry Point |
|-------|-------------|
| `sales_agent` | `sales_agent_graph` |
| `extract_data_agent` | `extract_data_agent_graph` |
| `profiler_agent` | `profiler_agent_graph` |
| `search_agent` | `search_agent_graph` |
| `supervisor_agent` | `supervisor_agent_graph` |
| `faq_rag_agent` | `faq_rag_agent_graph` |

## Repo Auxiliar: MCP Inmuebles

### Herramientas MCP Expuestas

| Herramienta | Descripcion |
|-------------|------------|
| `buscar_inmuebles` | Busqueda avanzada con 30+ filtros |
| `buscar_por_ubicacion` | Busqueda rapida por ciudad/zona |
| `obtener_inmueble` | Detalle de inmueble por ID |
