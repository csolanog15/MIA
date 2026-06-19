# Flujo de Campanas WhatsApp - MIA Agente IA

**Sender principal:** 573153277577 (Ciencuadras)
**Total templates MIA:** 128 de 786 (16.3%)

## Resumen del Flujo

```
[TRIGGER] -> [VALIDACION IAValida] -> [SELECCION TEMPLATE] -> [ENVIO Infobip] -> [RESPUESTA USUARIO] -> [CONVERSACION MIA]
```

## Triggers

| Trigger | Tipo | Descripcion |
|---------|------|-------------|
| Lead guardado en Zoho CRM | Post-Lead | Usuario dejo datos via save_lead_to_zoho |
| Preaprobado Davivienda | Proactiva | Datos financieros del cliente disponibles |
| Lead sin respuesta (2, 7, 30, 60 dias) | Post-Lead | Seguimiento temporal automatico |
| Campana masiva programada | Proactiva | Impulso comercial |
| Usuario desde buscadores (Google/Meta Ads) | Proactiva | Contactabilidad de leads captados por ads |

## Validacion de Campana (IAValida)

| Validacion | Criterio |
|-----------|----------|
| Ventana 24h | Solo templates fuera de ventana |
| Template aprobado | Status APPROVED en Meta |
| Opt-in del usuario | Habeas Data Colombia |
| Datos del lead completos | nombre, telefono, email validos |
| Segmentacion correcta | Template corresponde al perfil |
| Frecuencia de contacto | No contactar en ultimas 48h |
| Quality score del sender | Mantener HIGH |

## Categorias de Templates (128 total)

| Categoria | Cant. | Proposito |
|-----------|-------|----------|
| Carruseles inmuebles | ~40 | Envio de opciones con imagenes |
| Leads rescatados | ~15 | Reactivacion de leads inactivos |
| Credito/Colocacion | ~10 | Comunicaciones financieras |
| Auditoria/Remates | ~8 | Seguimiento temporal |
| Campanas/Impulso | ~8 | Activacion masiva |
| Owner contact | ~6 | Datos de contacto propietario |
| Vendedora | ~5 | Venta activa |
| Arrendadora | ~5 | Flujo arriendo |
| Reactivadora | ~5 | Conversaciones inactivas |
| Buscadores | ~4 | Leads desde ads |
| Perfilamiento | ~3 | Perfilamiento inicial |
| Otros/Experimentos | ~19 | Aliados, juntas, experimentos |

## Agentes que atienden campanas

| Campana | Agente que responde |
|---------|---------------------|
| Vendedora (preaprobados) | mia_sales_agent |
| Arriendo aliados | mia_rent_allies_agent |
| Venta aliados | mia_sales_allies_agent |
| Reactivacion | mia_outbound |
| Leads rescatados | mia_outbound |
| Campanas impulso | mia_outbound |

## Reglas de envio

- **Horarios:** Lun-Vie 8am-7pm, Sab 8am-1pm. No domingos ni festivos.
- **Maximo 1 campana por usuario cada 48h** (salvo respuesta activa)
- **Carruseles:** Solo si hay 3+ inmuebles que coincidan con perfil
- **Leads rescatados:** Maximo 3 intentos (2d, 7d, 30d). Despues -> descarte.
