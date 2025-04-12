
# Asistente de IA para Laboratorios 2.0

Este proyecto integra:
- **Dialogflow**: para interpretar el lenguaje del paciente
- **Flask**: para ejecutar acciones como agendar turnos
- **OCR (Tesseract)**: para leer órdenes médicas desde imágenes
- **Google Sheets**: para registrar los turnos
- **Railway**: para alojar el webhook sin necesidad de un VPS

---

## ¿Qué hace?

1. El paciente envía un mensaje o una imagen de orden médica
2. Dialogflow detecta la intención
3. Flask recibe la intención y:
   - Agenda turnos
   - Usa OCR si se envía una receta médica
4. Responde al paciente automáticamente

---

## Requisitos

- Cuenta en [Dialogflow](https://dialogflow.cloud.google.com/)
- Cuenta en [Railway](https://railway.app/)
- Cuenta de [Google Cloud](https://console.cloud.google.com/) con acceso a Google Sheets API
- Tesseract OCR instalado si vas a correr localmente
- Python 3.8 o superior

---

## Estructura

```
asistente-ocr-dialogflow/
├── app.py                      # Webhook principal
├── requirements.txt            # Dependencias
├── railway.json                # Configuración para Railway
├── service_account.json        # Credenciales de Google Sheets (no subir a GitHub)
└── README.md                   # Esta guía
```

---

## Cómo usar este proyecto

### 1. Subilo a GitHub

```bash
git init
git remote add origin https://github.com/usuario/asistente-ocr-dialogflow.git
git add .
git commit -m "Primer commit"
git push -u origin master
```

### 2. Desplegalo en Railway

1. Ingresá a [Railway](https://railway.app/)
2. Conectá tu cuenta de GitHub
3. Seleccioná el repositorio
4. Railway detectará automáticamente `app.py`
5. En **Variables**, agregá `service_account.json` con el contenido completo del archivo JSON

### 3. Configurá Dialogflow

- En tu agente, activá el webhook:
  - Fulfillment URL: `https://tu-proyecto.up.railway.app/`
- En cada intent (Saludo, PedirTurno, EnviarImagenOrden):
  - Activá "Enable webhook call for this intent"
  - En `EnviarImagenOrden`, asegurate de enviar la imagen codificada en base64 como `imagen_b64`

---

## 4. Conexión con WhatsApp (Opcional)

### Opción A: **Twilio Sandbox**
1. Crear cuenta en Twilio
2. Activar sandbox de WhatsApp
3. Conectarlo con Dialogflow o reenviar mensajes a Railway

### Opción B: **Meta Cloud API**
1. Crear una app en [Meta for Developers](https://developers.facebook.com/)
2. Configurar Webhook con URL de Railway
3. Recibir y reenviar mensajes a Dialogflow o a `app.py`

---

## Créditos
Desarrollado con propósito de atención automatizada en laboratorios de análisis clínicos.
