# 🤖 Módulo 6: Integración con CLIs, IDEs y Agentes

En este módulo aprenderás cómo conectar OmniRoute a tus herramientas de desarrollo favoritas: **Claude Code**, **Cursor**, **Codex CLI**, **Aider**, **Cline**, **OpenCode**, **VS Code** y protocolos de agentes como **MCP** y **A2A**.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar este módulo serás capaz de:
1. Usar los comandos de un solo toque `omniroute run` y `omniroute configure`.
2. Configurar la URL base y la clave de API en asistentes CLI e IDEs de desarrollo.
3. Exponer OmniRoute como servidor **MCP** (Model Context Protocol).
4. Conectar agentes mediante el protocolo **A2A** (Agent-to-Agent).

---

## 6.1 Lanzamiento Directo con `omniroute run`

OmniRoute permite ejecutar directamente tus CLIs favoritas inyectando las credenciales necesarias de forma aislada sin modificar tus archivos de configuración globales.

### Ejemplos de uso con `omniroute run`:

#### 🐧 Linux / 🍎 macOS (Bash):
```bash
# Lanzar Claude Code apuntando a GPT-4o a través de OmniRoute:
omniroute run claude --model openai/gpt-4o

# Lanzar Codex CLI con GLM:
omniroute run codex --model glm/glm-4.5

# Lanzar Aider:
omniroute run aider --model auto/coding

# Lanzar OpenCode:
omniroute run opencode --model auto
```

#### 🪟 Windows (PowerShell):
```powershell
omniroute run claude --model openai/gpt-4o
omniroute run codex --model glm/glm-4.5
omniroute run aider --model auto/coding
omniroute run opencode --model auto
```

#### 🪟 Windows (CMD):
```cmd
omniroute run claude --model openai/gpt-4o
omniroute run codex --model glm/glm-4.5
omniroute run aider --model auto/coding
omniroute run opencode --model auto
```

---

## 6.2 Configuración Guiada con `omniroute configure`

Si deseas escribir de forma permanente los archivos de configuración de tu CLI favorita para que apunte siempre a tu servidor local de OmniRoute:

### Comando interactivo:
```bash
omniroute configure codex
# También disponible para: claude, opencode, qwen, aider, goose, gemini, cline, continue, kilo
```

---

## 6.3 Configuración Manual en IDEs (Cursor, VS Code, Cline)

Para conectar entornos de desarrollo gráfico a OmniRoute:

### 1. Cursor IDE
1. Abre **Cursor Settings** -> **Models** -> **OpenAI API Key**.
2. Ingresa cualquier texto ficticio como API Key (ej. `omniroute-key`).
3. Activa la opción **Override OpenAI Base URL** e ingresa:
   `http://localhost:20128/v1`
4. En la lista de modelos, agrega `auto` o el modelo de tu preferencia (ej. `gemini/gemini-2.0-flash`).

### 2. VS Code con Extensión OmniCopilot
1. Instala la extensión **OmniCopilot** desde el Marketplace de VS Code.
2. Abre Copilot Chat -> Selector de modelos -> **Manage Models...** -> Selecciona **OmniRoute**.
3. ¡Todos los modelos expuestos por OmniRoute aparecerán directamente en tu chat nativo!

---

## 6.4 Integración con Protocolos de Agentes (MCP y A2A)

 OmniRoute expone interfaces estandarizadas para que otros agentes de Inteligencia Artificial puedan controlarlo e interactuar con sus más de 110 herramientas.

### 🧰 Servidor MCP (Model Context Protocol)

Puedes agregar OmniRoute como un servidor MCP HTTP en **Claude Desktop** o **Cursor**:

- **URL de transporte HTTP**: `http://localhost:20128/api/mcp/stream`
- **Comando CLI para Claude Code**:
  ```bash
  claude mcp add-server omniroute --type http --url http://localhost:20128/api/mcp/stream
  ```

### 🤝 Protocolo Agent-to-Agent (A2A)

OmniRoute publica su tarjeta de capacidades (*Agent Card*) bajo el estándar A2A:
- **Punto de enlace Agent.json**: `http://localhost:20128/.well-known/agent.json`

---

## 6.5 Ejercicio Práctico del Módulo 6

En este ejercicio práctico ejecutaremos el diagnóstico de integración de herramientas con el comando interactivo o de ayuda.

### 📝 Instrucciones:

Ejecuta el siguiente comando para ver la lista de herramientas compatibles soportadas por OmniRoute:

#### 🐧 Linux / 🍎 macOS / 🪟 Windows (Cualquier terminal):
```bash
omniroute run --help
```

---

### ❓ Preguntas de Autoevaluación

**1. ¿Qué comando te permite lanzar una CLI (como Claude Code) inyectándole automáticamente el punto de enlace de OmniRoute?**
- A) `omniroute launch-all`
- B) `omniroute run <herramienta> --model <modelo>`
- C) `npm start`
- *Respuesta correcta: B*

**2. ¿Cuál es la URL Base estándar que debes configurar en Cursor o VS Code para usar OmniRoute?**
- A) `http://localhost:20128/v1`
- B) `https://api.openai.com/v1`
- C) `http://127.0.0.1:8080/api`
- *Respuesta correcta: A*

**3. ¿Qué protocolo te permite exponer las más de 110 herramientas de OmniRoute hacia Claude Desktop o Cursor?**
- A) FTP
- B) MCP (Model Context Protocol)
- C) SMTP
- *Respuesta correcta: B*

---

¡Excelente! Has completado el **Módulo 6**. Avanza al módulo final: [💡 Módulo 7: Proyectos Prácticos y Solución de Problemas](./modulo-7-proyectos-practicos-y-casos-de-uso.md).
