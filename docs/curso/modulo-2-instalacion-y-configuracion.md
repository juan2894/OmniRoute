# 📦 Módulo 2: Instalación y Configuración Paso a Paso

En este módulo aprenderás a instalar y configurar **OmniRoute** en cualquier sistema operativo (Windows, macOS o Linux) utilizando diferentes métodos de instalación. Veremos comandos detallados para **Bash (Linux/macOS)**, **Windows PowerShell** y **Windows CMD**.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar este módulo serás capaz de:
1. Verificar y preparar el entorno (Node.js, versiones y dependencias).
2. Instalar OmniRoute mediante `npm`, Docker o desde el código fuente.
3. Configurar las variables de entorno (`.env`) e iniciar el servidor en el puerto 20128.
4. Ejecutar diagnósticos con `omniroute doctor` para verificar el correcto funcionamiento.

---

## 2.1 Requisitos del Sistema

Antes de comenzar, asegúrate de contar con **Node.js 22.x** o superior instalado en tu sistema.

Para verificar la versión instalada, ejecuta en tu terminal:

### 🐧 Linux / 🍎 macOS (Bash):
```bash
node -v
npm -v
```

### 🪟 Windows (PowerShell):
```powershell
node -v
npm -v
```

### 🪟 Windows (Símbolo del sistema / CMD):
```cmd
node -v
npm -v
```

> **Nota para principiantes**: Si no tienes Node.js instalado, descárgalo desde [nodejs.org](https://nodejs.org) seleccionando la versión LTS.

---

## 2.2 Método 1: Instalación Global con `npm` (Recomendado)

Es la forma más rápida y sencilla de instalar OmniRoute en cualquier ordenador.

### 🐧 Linux / 🍎 macOS (Bash):
```bash
npm install -g omniroute
```

### 🪟 Windows (PowerShell - Ejecutar como usuario o Administrador):
```powershell
npm install -g omniroute
```

### 🪟 Windows (CMD):
```cmd
npm install -g omniroute
```

---

## 2.3 Método 2: Ejecución mediante Docker

Si prefieres aislar OmniRoute en un contenedor Docker, puedes utilizar la imagen oficial.

### 🐧 Linux / 🍎 macOS (Bash) / 🪟 Windows (PowerShell / CMD):
```bash
docker run -d --name omniroute --restart unless-stopped \
  -p 127.0.0.1:20128:20128 \
  -v omniroute-data:/app/data \
  diegosouzapw/omniroute:latest
```

---

## 2.4 Método 3: Instalación desde el Código Fuente (Para desarrolladores)

Si deseas modificar el código de OmniRoute o colaborar en su desarrollo:

### 🐧 Linux / 🍎 macOS (Bash):
```bash
git clone https://github.com/diegosouzapw/OmniRoute.git
cd OmniRoute
cp .env.example .env
npm install
npm run dev
```

### 🪟 Windows (PowerShell):
```powershell
git clone https://github.com/diegosouzapw/OmniRoute.git
cd OmniRoute
Copy-Item .env.example .env
npm install
npm run dev
```

### 🪟 Windows (CMD):
```cmd
git clone https://github.com/diegosouzapw/OmniRoute.git
cd OmniRoute
copy .env.example .env
npm install
npm run dev
```

---

## 2.5 Iniciar el Servidor y la Interfaz Web (Dashboard)

Una vez instalado de forma global con `npm`, puedes iniciar OmniRoute simplemente escribiendo:

### 🐧 Linux / 🍎 macOS / 🪟 Windows (Cualquier terminal):
```bash
omniroute
```

Al ejecutar este comando, verás en la consola mensajes indicando que el servidor está listo:

```txt
🚀 OmniRoute gateway running on http://localhost:20128
📊 Dashboard accessible at http://localhost:20128
```

Abre tu navegador web e ingresa a: **`http://localhost:20128`** para ver el panel de control.

---

## 2.6 Diagnóstico y Verificación del Sistema

OmniRoute cuenta con una herramienta integrada de diagnóstico llamada `doctor` que revisa dependencias, puertos ocupados y estado de la base de datos.

Ejecuta el siguiente comando en tu terminal para verificar tu instalación:

### 🐧 Linux / 🍎 macOS (Bash):
```bash
omniroute doctor
```

### 🪟 Windows (PowerShell):
```powershell
omniroute doctor
```

### 🪟 Windows (CMD):
```cmd
omniroute doctor
```

---

## 2.7 Ejercicio Práctico del Módulo 2

Realizaremos un ejercicio práctico paso a paso para comprobar que tu servidor está funcionando correctamente mediante una consulta con `curl`.

### 📝 Instrucciones:

1. Asegúrate de tener OmniRoute corriendo en una ventana de terminal (`omniroute`).
2. Abre una **segunda ventana de terminal**.
3. Ejecuta la consulta de prueba según tu sistema operativo:

#### 🐧 Linux / 🍎 macOS (Bash):
```bash
curl http://localhost:20128/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"auto","messages":[{"role":"user","content":"¡Hola OmniRoute!"}]}'
```

#### 🪟 Windows (PowerShell):
```powershell
Invoke-RestMethod -Uri "http://localhost:20128/v1/chat/completions" `
  -Method Post `
  -Headers @{"Content-Type"="application/json"} `
  -Body '{"model":"auto","messages":[{"role":"user","content":"¡Hola OmniRoute!"}]}'
```

#### 🪟 Windows (CMD):
```cmd
curl http://localhost:20128/v1/chat/completions -H "Content-Type: application/json" -d "{\"model\":\"auto\",\"messages\":[{\"role\":\"user\",\"content\":\"¡Hola OmniRoute!\"}]}"
```

### 🎯 Resultado esperado:
Recibirás una respuesta JSON con un texto generado de forma instantánea por el proveedor gratuito integrado (`OpenCode Free`), confirmando que la instalación fue un éxito total. ¡Sin haber ingresado ninguna clave API!

---

¡Excelente trabajo! Has completado el **Módulo 2**. Avanza al [🌐 Módulo 3: Proveedores y Catálogo del Tier Gratuito](./modulo-3-proveedores-y-tier-gratuito.md).
