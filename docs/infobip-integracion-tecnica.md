# Integracion Tecnica: Infobip - n8n - MIA Agente IA

## Resumen

MIA usa Infobip como plataforma WhatsApp y n8n como orquestador de flujos.

## Diagrama de Integracion

```
[WhatsApp User]
       |
       v
[Infobip - Chatbot Answers 4207]
       |
       +-- Intencion simple -> Respuesta directa del chatbot
       |
       +-- Intencion compleja -> Webhook a n8n
                                      |
                                      v
                              [n8n Workflow]
                                      |
                                      +-- Contexto (DB/Cache)
                                      +-- LLM (MIA - Agente IA)
                                      +-- Respuesta -> Infobip API
                                                          |
                                                          v
                                                  [Usuario WhatsApp]
```

## Endpoints Clave de Infobip

| Endpoint | Metodo | Proposito |
|----------|--------|----------|
| `POST /whatsapp/1/message/text` | POST | Enviar mensaje de texto simple |
| `POST /whatsapp/1/message/template` | POST | Enviar template message (pre-aprobado) |
| `POST /whatsapp/1/message/interactive/buttons` | POST | Mensaje con botones interactivos |
| `POST /whatsapp/1/message/interactive/list` | POST | Mensaje con lista interactiva |
| `POST /messages/1/send` | POST | Messages API unificada (multi-canal) |
| `GET /whatsapp/2/senders/{sender}/templates` | GET | Listar templates disponibles |

## Autenticacion

- **Header:** `Authorization: App {API_KEY}`
- **Base URL:** Personal por cuenta
- **Scope:** `whatsapp:message:send`

## Ventana de 24 Horas

- Mensajes de sesion (texto libre, botones, listas) solo dentro de 24h desde ultimo mensaje del usuario.
- Fuera de ventana: solo template messages pre-aprobados por Meta.

## Mensajes Interactivos

- Reply Buttons: maximo 3 botones por mensaje
- Listas: maximo 10 secciones con 10 opciones cada una
- WhatsApp Flows: formularios estructurados
- Carousel Templates: hasta 10 tarjetas con imagen/video + botones

## Transferencia Bot -> MIA

- Webhook directo: inbound del numero apunta a n8n
- Elemento API en Answers: chatbot llama a n8n via HTTP
- External CCaaS integration: Answers transfiere conversacion completa
- `conversationId` es clave para mantener contexto

## Sender WhatsApp

- **Numero:** 573153277577 (Ciencuadras)
- **Quality:** HIGH
- **Limite:** UNLIMITED

## Referencias

- WhatsApp API: https://www.infobip.com/docs/api/channels/whatsapp
- Inbound Messages: https://www.infobip.com/docs/api/channels/whatsapp/whatsapp-inbound-messages
- Template Messages: https://infobip.com/docs/tutorials/send-whatsapp-template-messages
