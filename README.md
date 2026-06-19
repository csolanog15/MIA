# MIA — Agente IA Inmobiliario de Ciencuadras

## Contexto General

**MIA** es la asistente inmobiliaria con IA de [Ciencuadras](https://www.ciencuadras.com), la plataforma digital de Servicios Bolívar S.A. (NIT: 900.311.092-7) para arriendo, venta y alquiler de inmuebles en Colombia.

- **URL pública:** https://www.ciencuadras.com/mia-asistente-inmobiliaria
- **Presentación en producción:** "¡Hola de nuevo! Soy MIA, tu asesora inmobiliaria de Ciencuadras 😊 ¿En qué puedo ayudarte hoy para encontrar tu lugar ideal?"
- **Integración en Home:** Visible en el buscador principal de ciencuadras.com con CTA "Habla con MIA"
- **Plataforma de orquestación:** Langfuse (Prompt Management + Observabilidad)

---

## Proyectos en Langfuse

| Proyecto | Propósito |
|----------|----------|
| `MIA_PROD` | Producción — prompts y trazas del agente en vivo |
| `MIA_TEST` | Testing — prompts experimentales y validación pre-deploy |

---

## Sobre Ciencuadras (Plataforma)

| Atributo | Valor |
|----------|-------|
| Empresa | Servicios Bolívar S.A. |
| NIT | 900.311.092-7 |
| Dirección | Av. Cl 26 # 69 76, Bogotá D.C. |
| Línea de soporte | #923 / 601 3905331 |
| Email soporte | lineadesoporte923@serviciosbolivar.com |
| Redes | Instagram, TikTok, Facebook, LinkedIn, Spotify |

### Servicios principales de la plataforma

- **Arriendo** de apartamentos, casas, fincas, locales
- **Venta** de inmuebles usados
- **Proyectos de vivienda nueva** (constructoras aliadas)
- **Crédito de vivienda** (alianza con Davivienda)
- **Comercialización** inmobiliaria
- **Avalúos en línea**
- **Simulador de gastos notariales**
- **Publicación de inmuebles** (para propietarios e inmobiliarias)

### Cobertura geográfica

Bogotá, Medellín, Cali, Barranquilla, Bucaramanga, Cartagena, Pereira, Manizales, Ibagué, Neiva, Villavicencio, Cúcuta, Pasto, Santa Marta, Valledupar, Popayán, y municipios aledaños.

---

## Rol de MIA en la Plataforma

MIA funciona como **asesora inmobiliaria conversacional** integrada directamente en el flujo de búsqueda del usuario:

1. **Ayudar a encontrar inmuebles** según las necesidades del usuario
2. **Guiar en el proceso** de arriendo/venta/compra
3. **Responder preguntas** sobre la plataforma y sus servicios

---

## Estructura de este Repositorio

```
MIA/
├── README.md                          ← Este archivo
├── docs/
│   ├── arquitectura-mia.md           ← Arquitectura multi-agente
│   ├── langfuse-prompts-inventario.md ← Inventario completo de 47 prompts
│   ├── infobip-integracion-tecnica.md ← Integración WhatsApp/Infobip/n8n
│   ├── flujo-campanas-whatsapp-mia.md ← Flujo de campañas y templates
│   ├── clarity-mia-comportamiento.md  ← Comportamiento de usuarios (Clarity)
│   ├── datadog-apm-profundo-mia.md    ← Observabilidad APM
│   ├── repos-mia-analisis.md          ← Análisis de repositorios
│   └── ...                            ← Más documentación
├── reports/                           ← Reportes HTML
└── inventario-funcional-mia-v2.md     ← Inventario funcional
```

---

*Última actualización: Junio 2026*
