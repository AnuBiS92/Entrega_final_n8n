# 🛒 Análisis Automatizado de Reseñas de Clientes con n8n + LLMs

## 📌 Descripción general

Este proyecto implementa un workflow automatizado en **n8n** que permite analizar reseñas de clientes utilizando **Modelos de Lenguaje (LLMs)** para clasificar su sentimiento y actuar en consecuencia.

El objetivo principal es:

- Detectar reseñas **negativas**
- Generar un **resumen claro** y extraer hasta **3 razones principales**
- Notificar automáticamente al equipo de **Customer Experience (CX)**
- Responder automáticamente a clientes con reseñas **positivas o neutras**

---

## ⚙️ Funcionamiento del Workflow

El flujo se ejecuta de forma automática a partir de un **Webhook**, que recibe la reseña del cliente.

### 🔄 Flujo completo

1. **Webhook (Trigger)**
   - Recibe los datos de la reseña (cliente, email, texto, etc.)

2. **LLM 1 — Clasificación de sentimiento**
   - Analiza la reseña y la clasifica como:
     - `POSITIVO`
     - `NEGATIVO`
     - `NEUTRAL`

3. **Nodo Set — Parseo**
   - Convierte la salida del LLM en un JSON estructurado para su evaluación

4. **Nodo IF — Condicional**
   - Evalúa el resultado del LLM:
     - Si es `NEGATIVO` → rama crítica
     - Si es `POSITIVO` o `NEUTRAL` → rama de agradecimiento

---

## 🔴 Rama: Reseña Negativa

5. **LLM 2 — Análisis de reseña**
   - Genera:
     - Un **resumen breve (1 oración)**
     - Hasta **3 razones principales**

6. **Nodo Set — Parseo**
   - Estructura la respuesta del LLM en:
     - `resumen`
     - `razones`

7. **Nodo Gmail — Notificación a CX**
   - Envía un email al equipo de Customer Experience con:
     - Datos del cliente
     - Resumen de la reseña
     - Motivos detectados

👉 Objetivo: permitir una intervención rápida del equipo ante problemas.

---

## 🟢 Rama: Reseña Positiva / Neutral

5. **Nodo Gmail — Respuesta automática**
   - Envía un email al cliente:
     - Agradeciendo su feedback
     - Reforzando la relación con la marca

👉 Objetivo: mejorar la experiencia del cliente y fidelización.
