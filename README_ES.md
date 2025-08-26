
---

## 3) `README_ES.md` (completo en español)

```markdown
# Telleka Reservation Agent

Agente de **reservas de mesas** para restaurantes sobre **n8n**, con opción de voz usando **ElevenLabs**/**Vapi**.  
Este starter prioriza **datos normalizados**, **validación estricta** y **respuestas consistentes**.

## ✨ Características
- Webhook (POST) para recibir solicitudes de reserva.
- Validación y normalización (nombre, personas, fecha, hora, teléfono).
- Respuesta JSON consistente (`ok`, `mensaje`, `data`).
- Estructura limpia lista para demos o producción.
- Capa de voz opcional (ElevenLabs/Vapi).

## 📁 Estructura
telleka-reservation-agent/
├── workflows/
│ └── workflow-reservation-agent.json
├── tools/
│ └── tool-elevenlabs.json
├── data/
│ └── reservations-sample.csv
├── README.md
├── README_EN.md
├── README_ES.md
└── .gitignore


## ✅ Requisitos
- **n8n** (self-hosted o cloud)
- **Node.js** 18+ (recomendado por n8n)
- (Opcional) **ElevenLabs** / **Vapi** para voz

## 🚀 Uso rápido
1. Abre n8n → **Import** → selecciona `workflows/workflow-reservation-agent.json`.
2. Activa/publica el nodo **Webhook**.
3. Envía una prueba:

**Payload ejemplo**
```json
{
  "Nombre": "María Pérez",
  "Personas": 4,
  "Fecha": "2025-08-28",
  "Hora": "20:30",
  "Telefono": "+1-512-555-1234"
}


cURL

curl -X POST "https://TU_SUBDOMINIO.app.n8n.cloud/webhook-test/reservas" \
  -H "Content-Type: application/json" \
  -d '{ "Nombre":"María Pérez", "Personas":4, "Fecha":"2025-08-28", "Hora":"20:30", "Telefono":"+1-512-555-1234" }'


PowerShell

Invoke-RestMethod -Method POST "https://TU_SUBDOMINIO.app.n8n.cloud/webhook-test/reservas" `
  -Headers @{ "Content-Type" = "application/json" } `
  -Body '{ "Nombre":"María Pérez", "Personas":4, "Fecha":"2025-08-28", "Hora":"20:30", "Telefono":"+1-512-555-1234" }'


Respuesta esperada

{
  "ok": true,
  "mensaje": "✅ Reserva confirmada para 4 personas el 28/08 a las 20:30. ¡Gracias María!",
  "data": {
    "Nombre": "María Pérez",
    "Personas": 4,
    "FechaISO": "2025-08-28",
    "HoraISO": "20:30:00",
    "Telefono": "+1-512-555-1234",
    "_meta": { "version": "1.0.0", "recibidoEn": "..." }
  }
}

🧱 CSV de ejemplo

data/reservations-sample.csv

Nombre,Personas,Fecha,Hora,Telefono
Carlos Gómez,2,2025-08-28,19:00,+1-512-111-2222
María Pérez,4,2025-08-28,20:30,+1-512-333-4444

🗣️ Voz (opcional)

Define tools/tool-elevenlabs.json con el esquema de tu proveedor de voz.

Mapea la transcripción a: Nombre, Personas, Fecha, Hora, Telefono.

🧪 Buenas prácticas

Validar tipos antes de procesar (números, fechas).

Mantener una forma de respuesta fija (ok, mensaje, data).

Versionar cambios en _meta.version.

🗺️ Roadmap

 Verificación de disponibilidad por horario

 Confirmaciones por SMS/WhatsApp

 Panel de administración de reservas

 Detección de conflictos (overbooking)

📄 Licencia

MIT