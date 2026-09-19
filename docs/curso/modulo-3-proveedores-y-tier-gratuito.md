# 🌐 Módulo 3: Proveedores y Catálogo del Tier Gratuito

En este módulo aprenderás a conectar diferentes proveedores de Inteligencia Artificial a OmniRoute, tanto los que requieren una clave de API (*API Key*) como los que funcionan de manera totalmente gratuita y sin contraseña o registro (*Zero-Config / Keyless*).

---

## 🎯 Objetivos de Aprendizaje

Al finalizar este módulo serás capaz de:
1. Comprender cómo funciona el catálogo del **Tier Gratuito (*Free Tier*)** que acumula ~1.62 mil millones de tokens al mes.
2. Distinguir entre proveedores **con clave de API** (OpenAI, Anthropic, Gemini, Kimi, etc.) y **sin clave de API** (OpenCode Free, Pollinations, etc.).
3. Conectar y gestionar proveedores desde la interfaz web (Dashboard) o mediante comandos.
4. Realizar consultas directas especificando proveedores concretos.

---

## 3.1 El Catálogo del Tier Gratuito (~1.62B Tokens / Mes)

OmniRoute incluye un catálogo auditado periódicamente con **489 entradas gratuitas organizadas en 35 bolsas (*pools*) recurrentes**.

### ¿Cómo es posible tener tantos tokens gratis?
Muchos proveedores de IA ofrecen capas de uso gratuito para atraer desarrolladores o probar sus infraestructuras:
- **Groq**: Ofrece límites por minuto/día muy altos en modelos Llama y Mixtral.
- **Google Gemini**: Ofrece un tier gratuito con límites holgados para Gemini 1.5 Flash / Pro y Gemini 2.0.
- **Kimi (Moonshot AI)** / **OpenCode Free**: Proveedores integrados para consultas directas y sin coste inicial.
- **Pollinations.ai**: Servicio público que enruta hacia múltiples modelos sin necesidad de API Key.

OmniRoute consolida y suma todas estas cuotas de forma transparente para que nunca te quedes sin capacidad de cómputo.

---

## 3.2 Tipos de Proveedores en OmniRoute

```
                       ┌─────────────────────────────────────────┐
                       │  Tipos de Proveedores en OmniRoute      │
                       └────────────────────┬────────────────────┘
                                            │
                  ┌─────────────────────────┴─────────────────────────┐
                  ▼                                                   ▼
   🔑 Proveedores con API Key                           🆓 Proveedores Sin Clave (Keyless)
   • OpenAI (GPT-4o, O3-Mini)                           • OpenCode Free (`oc/...`)
   • Anthropic (Claude 3.5 / 3.7)                       • Pollinations (`pollinations/...`)
   • Google Gemini (Gemini 2.0 Flash)                   • Z.AI GLM (`glm/...`)
   • Kimi (Kimi K3)                                     • Qoder AI (`qoder/...`)
   • DeepSeek, Mistral, Groq, etc.                      • Kilo Code (`kilo/...`)
```

---

## 3.3 Conectando Proveedores desde el Dashboard

1. Inicia OmniRoute ejecutando `omniroute` en tu consola.
2. Abre tu navegador y dirígete a `http://localhost:20128`.
3. En el menú lateral izquierdo, haz clic en **Providers** (Proveedores).
4. Aquí verás el listado completo de proveedores disponibles (+350):
   - **Para conectar un proveedor con clave** (ej. Gemini o Groq): Haz clic en el proveedor, pega tu API Key y presiona **Save** (Guardar).
   - **Para proveedores de acceso libre** (ej. OpenCode Free): Ya aparecen conectados automáticamente.

---

## 3.4 Invocación Directa de Modelos vs. Canal `auto`

Cuando realizas una petición a OmniRoute en `http://localhost:20128/v1/chat/completions`, puedes especificar el modelo de dos formas:

1. **Uso del enrutador automático**:
   - `"model": "auto"` → OmniRoute selecciona el mejor modelo disponible entre tus proveedores conectados.
2. **Uso de prefijo de proveedor específico**:
   - `"model": "gemini/gemini-2.0-flash"` → Fuerza el uso directo de Gemini 2.0 Flash.
   - `"model": "oc/opencode-free"` → Fuerza el uso de OpenCode Free.
   - `"model": "groq/llama-3.3-70b-versatile"` → Fuerza el uso de Groq.

---

## 3.5 Ejercicio Práctico del Módulo 3

Probaremos realizar dos consultas: una utilizando el proveedor libre integrado `oc/...` y otra usando la sintaxis general.

### 📝 Pasos a realizar:

Abre tu terminal (segunda ventana con OmniRoute en ejecución) y prueba las llamadas según tu sistema operativo:

#### 🐧 Linux / 🍎 macOS (Bash):
```bash
# Consulta forzando el proveedor OpenCode Free:
curl http://localhost:20128/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "oc/opencode-free",
    "messages": [{"role": "user", "content": "Escribe una frase motivadora para un programador."}]
  }'
```

#### 🪟 Windows (PowerShell):
```powershell
Invoke-RestMethod -Uri "http://localhost:20128/v1/chat/completions" `
  -Method Post `
  -Headers @{"Content-Type"="application/json"} `
  -Body '{
    "model": "oc/opencode-free",
    "messages": [{"role": "user", "content": "Escribe una frase motivadora para un programador."}]
  }'
```

#### 🪟 Windows (CMD):
```cmd
curl http://localhost:20128/v1/chat/completions -H "Content-Type: application/json" -d "{\"model\": \"oc/opencode-free\", \"messages\": [{\"role\": \"user\", \"content\": \"Escribe una frase motivadora para un programador.\"}]}"
```

---

### ❓ Preguntas de Autoevaluación

**1. Aproximadamente, ¿cuántos tokens mensuales gratuitos calcula el catálogo auditado de OmniRoute?**
- A) 100,000 tokens.
- B) ~1.62 mil millones de tokens (1.62B).
- C) Exactamente 10 millones de tokens.
- *Respuesta correcta: B*

**2. Si deseas forzar el uso de un modelo específico de un proveedor, ¿cómo debes nombrarlo en el parámetro `"model"`?**
- A) Solo el nombre del modelo (ej. `gpt-4o`).
- B) `prefijo_proveedor/nombre_modelo` (ej. `gemini/gemini-2.0-flash`).
- C) No es posible forzar un modelo.
- *Respuesta correcta: B*

---

¡Excelente! Has completado el **Módulo 3**. Continúa con el [🎯 Módulo 4: Combos y Estrategias de Enrutamiento](./modulo-4-combos-y-estrategias-de-enrutamiento.md).
