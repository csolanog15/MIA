# Arquitectura de MIA — Agente IA Inmobiliario de Ciencuadras

## Resumen Ejecutivo

MIA es un sistema multi-agente conversacional que funciona como asesora inmobiliaria de Ciencuadras. Utiliza un patrón de **Router + Agentes Especializados** orquestado a través de Langfuse para gestión de prompts y observabilidad. El modelo principal es **Gemini** (Google).

---

## Arquitectura de Alto Nivel

```
USUARIO (WhatsApp / Web)
       |
       v
mia_router_agent (Enrutador)
  Clasifica intencion -> Deriva al agente especializado
       |
   +---+---+---+
   |       |       |
   v       v       v
mia_search  mia_profiler  mia_faq_rag
_agent      _agent        _agent
```

## Inventario de Agentes (46 prompts en Langfuse)

### Agentes Core (Inbound)

| Agente | Prompt en Langfuse | Funcion |
|--------|-------------------|--------|
| **Router** | `mia_router_agent_prod_gemini_1` | Clasifica intencion y deriva al agente correcto |
| **Search** | `mia_search_agent_prod_gemini_1` | Busqueda de inmuebles en catalogo |
| **Profiler** | `mia_profiler_agent_prod_gemini_1` | Captura datos personales, crea lead en Zoho CRM |
| **FAQ/RAG** | `mia_faq_rag_agent_prod_gemini_1` | Responde preguntas frecuentes con RAG |

### Agentes de Venta Directa (Outbound)

| Agente | Prompt en Langfuse | Funcion |
|--------|-------------------|--------|
| **Sales Agent** | `mia_sales_agent_prod_gemini_1` | Venta directa con validacion financiera |
| **Vendedora** | `mia_vendedora_conversacion_prod_gemini_1` | Conversacion de venta (Davivienda preaprobados) |
| **Sales Allies** | `mia_sales_allies_agent_prod_gemini_1` | Venta a traves de aliados inmobiliarios |
| **Rent Allies** | `mia_rent_allies_agent_prod_gemini_1` | Arriendo a traves de aliados |
| **Outbound** | `mia_2_outbound_conv_001_prod_gemini_1` | Contacto saliente / reactivacion |

## Herramientas (Tools) del Sistema

| Tool | Funcion |
|------|---------|
| `search_properties` | Busqueda en catalogo con criterios |
| `paginate_search` | Paginacion de resultados |
| `get_property_info` | Info detallada de un inmueble |
| `get_appointment` | Consulta disponibilidad de horarios |
| `validate_appointment_date` | Valida fecha/hora especifica |
| `save_lead_to_zoho` | Guarda lead en Zoho CRM |
| `validate_financial_capacity` | Validacion financiera |
| `search_substitutes_properties` | Busca inmuebles similares |
| `search_faqs` | Busqueda semantica en FAQs |
| `search_rag` | Busqueda complementaria web |

## Integraciones

| Sistema | Proposito |
|---------|-----------|
| **Zoho CRM** | Gestion de leads |
| **Davivienda** | Creditos preaprobados |
| **Catalogo Ciencuadras** | Busqueda de inmuebles |
| **Vector Store** | RAG para FAQs |
| **Redis** | Cache de sesiones |
| **Langfuse** | Prompt management + observabilidad |
| **Infobip** | Canal WhatsApp |
| **n8n** | Orquestacion de flujos |

## Modelo LLM

- **Principal:** Google Gemini 2.0
- **Legacy:** GPT-3.5 (algunos prompts v1)

## Reglas de Negocio Clave

1. **Arriendo vs Compra:** Si presupuesto < $100M o rango mensual -> Arriendo
2. **VIS:** proyecto=true, transaccion=venta, precio maximo $213.525.000
3. **Cuota inicial:** Leasing 20%, Hipotecario 30%
4. **Horarios visita:** Lun-Vie 8am-5pm, Sab 8am-12pm
5. **Datos obligatorios lead:** nombre, identificacion, tipo doc, telefono, email
6. **Politica privacidad:** Siempre mencionar antes de capturar datos
7. **Contactos inmobiliaria:** Solo DESPUES de save_lead_to_zoho exitoso

## Canales

- **Web:** https://www.ciencuadras.com/mia-asistente-inmobiliaria
- **WhatsApp:** Formato optimizado (sin Markdown, un asterisco para negritas)
- **Outbound:** Contacto proactivo a usuarios con preaprobado Davivienda
