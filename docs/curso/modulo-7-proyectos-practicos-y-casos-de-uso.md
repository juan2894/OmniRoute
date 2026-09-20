# 💡 Módulo 7: Proyectos Prácticos y Solución de Problemas

¡Bienvenido al módulo final del **Curso de OmniRoute**! En este módulo pondremos en práctica todo lo aprendido mediante **dos proyectos integradores reales** y revisaremos una guía detallada de **solución de problemas (*Troubleshooting*)** para superar cualquier inconveniente técnico.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar este módulo serás capaz de:
1. Diseñar e implementar un flujo de trabajo completo de desarrollo asistido por IA con coste $0.
2. Configurar una arquitectura de alta disponibilidad con resiliencia multi-proveedor.
3. Diagnosticar y resolver errores comunes de red, puertos bloqueados, problemas de CORS o permisos en Windows, macOS y Linux.

---

## 7.1 Proyecto Integrador 1: Entorno de Desarrollo a Coste $0

### 📋 Objetivo:
Configurar un entorno de desarrollo de código asistido por agente CLI (Claude Code o OpenCode) utilizando exclusivamente la cuota de proveedores del *Free Tier*, aplicando compresión de tokens y conmutación automática de respaldo.

### 🛠️ Pasos de Implementación:

1. **Iniciar OmniRoute**:
   Asegúrate de que tu servidor OmniRoute está activo.

2. **Verificar el canal libre**:
   Confirma que el canal `auto` tiene proveedores activos ejecutando en tu terminal:

   #### 🐧 Linux / 🍎 macOS (Bash):
   ```bash
   curl http://localhost:20128/v1/models
   ```

   #### 🪟 Windows (PowerShell):
   ```powershell
   Invoke-RestMethod -Uri "http://localhost:20128/v1/models"
   ```

   #### 🪟 Windows (CMD):
   ```cmd
   curl http://localhost:20128/v1/models
   ```

3. **Ejecutar el agente de código con compresión `stacked`**:
   Ejecuta el agente utilizando el canal optimizado de código y la compresión activada:

   ```bash
   omniroute run opencode --model auto/coding
   ```

4. **Resultado**:
   Habrás configurado un agente capaz de generar, refactorizar y probar código sin haber ingresado ninguna tarjeta de crédito ni haber gastado un solo dólar.

---

## 7.2 Proyecto Integrador 2: Enrutador Resiliente Multi-Proveedor

### 📋 Objetivo:
Crear un Combo personalizado que combine un modelo principal de alta calidad (ej. `openai/gpt-4o`), un modelo secundario rápido de bajo costo (ej. `gemini/gemini-2.0-flash`) y un modelo gratuito de respaldo (ej. `oc/opencode-free`) con la estrategia `priority`.

### 🛠️ Pasos de Implementación:

1. Abre el Dashboard en `http://localhost:20128`.
2. Dirígete a **Combos** -> **Create Combo**.
3. Asigna el nombre `mi-combo-resiliente`.
4. Selecciona la estrategia `priority`.
5. Agrega los objetivos en orden:
   - Posición 1: `openai/gpt-4o` (si tienes API Key configurada)
   - Posición 2: `gemini/gemini-2.0-flash`
   - Posición 3: `oc/opencode-free`
6. Guarda el combo.
7. Realiza una prueba desde tu código o cURL enviando `"model": "mi-combo-resiliente"`.

Si la clave de OpenAI se agota o falla, la solicitud pasará instantáneamente a Gemini; y si Gemini falla, atenderá OpenCode Free. **Disponibilidad del 99.99%.**

---

## 7.3 Solución de Problemas Frecuentes (*Troubleshooting*)

### 🔴 Problema 1: "Port 20128 already in use" (El puerto 20128 está ocupado)
Ocurre cuando ya hay otra instancia de OmniRoute u otra aplicación escuchando en ese puerto.

#### 💡 Solución:
- **En Linux / macOS (Bash)**:
  ```bash
  lsof -ti:20128 | xargs kill -9
  ```
- **En Windows (PowerShell)**:
  ```powershell
  Get-Process -Id (Get-NetTCPConnection -LocalPort 20128).OwningProcess | Stop-Process -Force
  ```
- **En Windows (CMD)**:
  ```cmd
  for /f "tokens=5" %a in ('netstat -aon ^| findstr :20128') do taskkill /F /PID %a
  ```

---

### 🔴 Problema 2: Error `429 Too Many Requests` constante
Ocurre cuando un proveedor ha agotado su cuota o límite de frecuencia de peticiones.

#### 💡 Solución:
1. No te preocupes: OmniRoute activará automáticamente la capa de *Cooldown* para esa clave.
2. Si usas un modelo directo (ej. `groq/...`), cambia tu solicitud al canal `auto` para que OmniRoute elija un proveedor alternativo saludable.
3. Revisa la pestaña **Free Tiers** en el Dashboard para ver qué cuotas se han reestablecido.

---

### 🔴 Problema 3: `ECONNREFUSED` o error de conexión en Cursor / VS Code

#### 💡 Solución:
1. Verifica que el servidor de OmniRoute está en ejecución (`omniroute`).
2. Asegúrate de incluir el sufijo `/v1` al final de la URL base en la configuración de la herramienta:
   - Correcto: `http://localhost:20128/v1`
   - Incorrecto: `http://localhost:20128`

---

## 7.4 Examen Final de Autoevaluación

¡Ponte a prueba para certificar tus conocimientos adquiridos en el curso!

**1. ¿Cuál es la ruta HTTP correcta para hacer solicitudes Chat Completions en OmniRoute?**
- A) `http://localhost:20128/chat`
- B) `http://localhost:20128/v1/chat/completions`
- C) `http://localhost:20128/api/v2/generate`
- *Respuesta correcta: B*

**2. ¿Qué ocurre si la primera opción de un combo configurado con estrategia `priority` falla?**
- A) Se detiene el sistema y arroja un error 500 fatal.
- B) OmniRoute pasa de inmediato a la siguiente opción definida en el combo sin interrumpir al cliente.
- C) Se borra la base de datos local.
- *Respuesta correcta: B*

**3. ¿Cuál es el beneficio de usar `omniroute run <cli>` en lugar de configurar variables de entorno globales?**
- A) Inyecta credenciales y endpoints en un proceso aislado sin contaminar la configuración global de tu sistema operativo.
- B) Es más lento pero más seguro.
- C) No ofrece ningún beneficio.
- *Respuesta correcta: A*

---

## 🏆 ¡Felicitaciones!

Has completado con éxito todo el **Curso Práctico de OmniRoute**. Ahora tienes el control total para enrutar, optimizar y comprimir tus solicitudes de Inteligencia Artificial en tus proyectos de desarrollo de software.

Regresa al [Índice General del Curso](./README.md) para repasar cualquier lección o consultar la documentación. ¡A programar! 🚀
