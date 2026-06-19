# Inventario Completo de Prompts MIA - Langfuse

**Total de prompts:** 47
**Modelo principal:** Gemini (prod)

## Tabla Resumen

| # | Nombre | Categoria |
|---|--------|----------|
| 1 | mia_router_agent_prod_gemini_1 | Core - Router |
| 2 | mia_search_agent_prod_gemini_1 | Core - Search |
| 3 | mia_profiler_agent_prod_gemini_1 | Core - Profiler |
| 4 | mia_faq_rag_agent_prod_gemini_1 | Core - FAQ/RAG |
| 5 | mia_evaluation_agent_prod_gemini_1 | Core - Evaluation |
| 6 | mia_vendedora_conversacion_prod_gemini_1 | Outbound - Vendedora |
| 7 | mia_sales_agent_prod_gemini_1 | Outbound - Sales |
| 8 | mia_sales_allies_agent_prod_gemini_1 | Outbound - Sales Allies |
| 9 | mia_rent_allies_agent_prod_gemini_1 | Outbound - Rent Allies |
| 10 | mia_perfiladora_conversacion_prod_gemini_1 | Core - Profiler (v2) |
| 11 | mia_vendedora_extraer_datos_prod_gemini_1 | Extractor - Vendedora |
| 12 | mia_extract_sales_agent_prod_gemini_1 | Extractor - Sales |
| 13 | mia_extract_sales_allies_agent_prod_gemini_1 | Extractor - Sales Allies |
| 14 | mia_extract_rent_allies_agent_prod_gemini_1 | Extractor - Rent Allies |
| 15 | mia_extract_allies_data_prod_gemini_1 | Extractor - Allies Data |
| 16 | mia_sales_allies_router_prod_gemini_1 | Router - Sales Allies |
| 17 | mia_search_allies_router_prod_gemini_1 | Router - Search Allies |
| 18 | mia_rent_allies_router_prod_gemini_1 | Router - Rent Allies |
| 19 | mia_sales_faq_router_prod_gemini_1 | Router - Sales/FAQ |
| 20 | mia_search_allies_agent_prod_gemini_1 | Search - Allies (Venta) |
| 21 | mia_search_sales_allies_agent_prod_gemini_1 | Search - Sales Allies |
| 22 | mia_search_rent_allies_agent_prod_gemini_1 | Search - Rent Allies |
| 23 | MIA 3.0 | Core - Conversacional |
| 24 | mia_reactivation_advisor_dev_gemini_1 | Outbound - Reactivacion |
| 25 | extract_features_from_description_001_prod_gemini_1 | Utilidad |
| 26 | response_question_property_001_prod_gemini_1 | Utilidad |
| 27-47 | mia_1_* y mia_2_* | Legacy (v1/v2) |

## Cobertura de Canales

| Canal | Router | Search | Conversacion | Extractor |
|-------|--------|--------|-------------|----------|
| Inbound general | mia_router_agent | mia_search_agent | mia_profiler_agent | mia_perfiladora |
| Outbound vendedora | mia_sales_faq_router | - | mia_vendedora | mia_vendedora_extraer |
| Ventas directas | mia_sales_faq_router | - | mia_sales_agent | mia_extract_sales |
| Aliados venta | mia_sales_allies_router | mia_search_sales_allies | mia_sales_allies | mia_extract_sales_allies |
| Aliados arriendo | mia_rent_allies_router | mia_search_rent_allies | mia_rent_allies | mia_extract_rent_allies |
| FAQ/RAG | - | - | mia_faq_rag_agent | - |

## Herramientas compartidas

| Tool | Agentes que la usan |
|------|-------------------|
| search_properties | search_agent |
| search_sales_allies_properties | search_sales_allies, search_allies |
| search_rent_allies_properties | search_rent_allies |
| search_substitutes_properties | vendedora, sales_agent |
| paginate_search | Todos los search + vendedora |
| get_property_info | profiler, sales, allies, rent |
| get_appointment | profiler, sales_allies, rent_allies |
| validate_appointment_date | profiler, sales_allies, rent_allies |
| validate_financial_capacity | vendedora, sales, sales_allies |
| save_lead_to_zoho | Todos los agentes de cierre |
| search_faqs | faq_rag |
| search_rag | faq_rag |

## Reglas de Negocio Transversales

### CRM (Zoho)
- **Lead statuses:** Contactado, Interesado en asesoria, Descartado, Volver a llamar
- **origin_lead valores:** MIA - Vendedora, MIA - Vendedora Aliados, Outbound - MIA, MIA - Credito

### Financiacion
- Credito hipotecario: 30% cuota inicial, 70% financiado
- Leasing habitacional: 20% cuota inicial, 80% financiado
- VIS tope: $213,525,000

### Formato WhatsApp
- URLs en texto plano (NO markdown)
- Un asterisco para negritas: *texto*
- Emojis moderados
- Respuestas concisas (2-3 oraciones)

## Versiones

| Version | Prefijo | Estado |
|---------|---------|--------|
| v1 | mia_1_* | Legacy |
| v2 | mia_2_* | Legacy |
| v3 | agentes actuales | **Produccion** |
