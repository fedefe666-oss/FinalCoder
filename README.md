# 🤖 Slack Bot - Pagos y Soporte (Make + Slack + Gemini + Airtable)

Automatización desarrollada en **Make.com** para gestionar consultas recibidas desde **Slack**, utilizando **Gemini AI** para interpretar el lenguaje natural, **Airtable** como base de datos y **Data Store** para mantener el contexto de la conversación.

Este proyecto demuestra una arquitectura de automatización basada en IA, incluyendo memoria conversacional, clasificación inteligente de consultas y soporte para flujos Human-in-the-Loop.

---

# 📌 Características

- ✅ Recepción de mensajes desde Slack
- ✅ Memoria conversacional mediante Data Store
- ✅ Detección automática de patentes argentinas
- ✅ Consulta de información en Airtable
- ✅ Respuestas generadas con Gemini AI
- ✅ Escalamiento de consultas urgentes
- ✅ Notificaciones internas mediante Slack
- ✅ Envío de correos electrónicos
- ✅ Arquitectura modular y escalable

---

# 🏗 Arquitectura

```text
Slack

│

▼

Watch Messages

│

▼

Leer Estado (Data Store)

│

▼

Detectar Patente (Regex)

│

▼

Router

├──────────────┐
│              │
▼              ▼
Pagos       Soporte
│              │
▼              ▼
Airtable    Slack Alert
│              │
▼              ▼
Gemini      Gmail
│              │
▼              ▼
Slack Reply Actualizar Estado
```

---

# ⚙ Tecnologías utilizadas

| Tecnología | Uso |
|------------|-----|
| Make.com | Orquestación |
| Slack | Entrada y salida |
| Gemini AI | Comprensión del lenguaje natural |
| Airtable | Base de datos |
| Data Store | Memoria conversacional |
| Gmail | Alertas |

---

# 📂 Flujo del escenario

## 1. Recepción del mensaje

El escenario escucha permanentemente un canal de Slack.

Se procesan únicamente:

- mensajes enviados por usuarios
- mensajes con contenido
- mensajes nuevos

Se ignoran:

- bots
- mensajes automáticos
- eventos internos

---

## 2. Recuperación del contexto

Antes de procesar el mensaje, se consulta un **Data Store** utilizando el **Slack User ID**.

El objetivo es recuperar información previa del usuario.

Ejemplo:

- estado
- intención
- patente
- hilo de conversación
- última pregunta

---

## 3. Detección de patente

Se utiliza una expresión regular para detectar automáticamente patentes argentinas.

Formatos soportados:

ABC123

AA123BB

---

## 4. Consulta de pagos

Cuando se detecta una patente:

1. Se consulta Airtable.
2. Se obtiene la información correspondiente.
3. Gemini genera una respuesta natural.
4. Slack responde al usuario.

---

## 5. Consultas urgentes

Cuando el mensaje contiene palabras relacionadas con urgencias:

- se notifica al equipo de soporte
- se envía un correo electrónico
- se informa al usuario que su caso fue derivado

---

# 🧠 Inteligencia Artificial

Gemini es utilizado para:

- comprender el mensaje
- interpretar el contexto
- generar respuestas naturales
- evitar respuestas rígidas

La IA únicamente utiliza la información disponible en Airtable para evitar alucinaciones.

---

# 🗄 Base de Datos

El escenario utiliza Airtable como fuente principal de información.

Se recomienda utilizar las siguientes tablas:

## Consultas

- ID
- Fecha
- Usuario
- Mensaje
- Estado
- Respuesta IA
- Thread ID

---

## Usuarios

- Nombre
- Slack ID
- Email
- Empresa

---

## Categorías

- Pagos
- Comercial
- Reclamos
- Soporte
- Otros

---

# 💾 Memoria Conversacional

El Data Store mantiene el contexto de cada usuario.

Información almacenada:

- Estado
- Intención
- Patente
- Prioridad
- Thread ID
- Última interacción

Esto permite mantener conversaciones continuas sin perder contexto.

---

# 📊 Estados del flujo

```text
Nuevo

↓

Procesando

↓

Consulta Airtable

↓

Generar Respuesta

↓

Respondido

↓

Fin
```

En caso de error:

```text
Error

↓

Registrar incidente

↓

Notificar soporte

↓

Continuar flujo
```

---

# 📁 Estructura recomendada del repositorio

```text
.
├── Blueprint/
│   └── Slack Bot Pagos y Soporte.json
│
├── docs/
│   ├── Arquitectura.md
│   ├── ManualTecnico.md
│   └── README.md
│
├── prompts/
│   └── Gemini.md
│
└── images/
    └── arquitectura.png
```

---

# 🚀 Cómo utilizar

1. Importar el Blueprint en Make.
2. Configurar las conexiones de Slack.
3. Configurar Airtable.
4. Configurar Gemini.
5. Configurar Gmail.
6. Crear el Data Store.
7. Ejecutar el escenario.

---

# 🔐 Requisitos

- Cuenta de Make
- Workspace de Slack
- Base de Airtable
- API Key de Gemini
- Cuenta Gmail
- Data Store configurado

---

# 📈 Mejoras futuras

- Human-in-the-Loop
- Dashboard de métricas
- Clasificación automática mediante IA
- Integración con HubSpot
- WhatsApp Business
- API REST
- Sistema de Tickets
- Auditoría completa
- Historial IA
- Configuración dinámica

---

# 👨‍💻 Autor

**Federico Ferreyra**

Arquitecto de Automatizaciones | IA Aplicada | Customer Experience | Process Automation

---

# 📄 Licencia

Este proyecto fue desarrollado con fines educativos y de demostración de arquitectura de automatización basada en Inteligencia Artificial.
