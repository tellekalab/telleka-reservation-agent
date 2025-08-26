
---

## 2) `README_EN.md` (completo en inglés)

```markdown
# Telleka Reservation Agent

Agent for **restaurant table reservations** built on **n8n**, optionally voice-enabled with **ElevenLabs**/**Vapi**.  
This starter focuses on **normalized data**, **strict validation**, and **consistent responses**.

## ✨ Features
- HTTP Webhook (POST) to receive reservation requests.
- Validation & normalization (name, party size, date, time, phone).
- Consistent JSON response (`ok`, `message`, `data`).
- Clean project layout ready for demos or production.
- Optional voice layer (ElevenLabs/Vapi).

## 📁 Project Structure
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

## ✅ Requirements
- **n8n** (self-hosted or cloud)
- **Node.js** 18+ (as recommended by n8n)
- (Optional) **ElevenLabs** / **Vapi** account for voice

## 🚀 Quick Start
1. Open n8n → **Import** → select `workflows/workflow-reservation-agent.json`.
2. Activate/publish the **Webhook** node.
3. Send a test request:

**Example payload**
```json
{
  "Nombre": "María Pérez",
  "Personas": 4,
  "Fecha": "2025-08-28",
  "Hora": "20:30",
  "Telefono": "+1-512-555-1234"
}

curl -X POST "https://YOUR_SUBDOMAIN.app.n8n.cloud/webhook-test/reservas" \
  -H "Content-Type: application/json" \
  -d '{ "Nombre":"María Pérez", "Personas":4, "Fecha":"2025-08-28", "Hora":"20:30", "Telefono":"+1-512-555-1234" }'

Invoke-RestMethod -Method POST "https://YOUR_SUBDOMAIN.app.n8n.cloud/webhook-test/reservas" `
  -Headers @{ "Content-Type" = "application/json" } `
  -Body '{ "Nombre":"María Pérez", "Personas":4, "Fecha":"2025-08-28", "Hora":"20:30", "Telefono":"+1-512-555-1234" }'

{
  "ok": true,
  "message": "✅ Reservation confirmed for 4 people on 08/28 at 20:30. Thank you María!",
  "data": {
    "Nombre": "María Pérez",
    "Personas": 4,
    "FechaISO": "2025-08-28",
    "HoraISO": "20:30:00",
    "Telefono": "+1-512-555-1234",
    "_meta": { "version": "1.0.0", "receivedAt": "..." }
  }
}

🧱 Sample CSV

data/reservations-sample.csv

Nombre,Personas,Fecha,Hora,Telefono
Carlos Gómez,2,2025-08-28,19:00,+1-512-111-2222
María Pérez,4,2025-08-28,20:30,+1-512-333-4444

🗣️ Voice (optional)

Define tools/tool-elevenlabs.json with your voice provider schema.

Map speech-to-text results to required fields: Nombre, Personas, Fecha, Hora, Telefono.

🧪 Good Practices

Validate types before processing (numbers, dates).

Return a fixed response shape (ok, message, data).

Version changes in _meta.version.

🗺️ Roadmap

 Availability checks per time slot

 SMS/WhatsApp confirmations

 Admin dashboard

 Conflict detection (overbooking)

📄 License

MIT