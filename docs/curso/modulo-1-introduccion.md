# 🚀 Módulo 1: Introducción a OmniRoute

Bienvenido al primer módulo del curso de **OmniRoute**. En este módulo aprenderás los conceptos fundamentales detrás de una pasarela de Inteligencia Artificial (*AI Gateway*), comprenderás cómo funciona OmniRoute por dentro y descubrirás por qué es la solución definitiva para optimizar el desarrollo de software asistido por IA.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar este módulo serás capaz de:
1. Explicar qué es un **AI Gateway** y qué problemas resuelve en el desarrollo diario.
2. Identificar los componentes principales de la arquitectura de OmniRoute.
3. Comprender las ventajas de ejecutar un servidor local (*local-first*) frente a servicios en la nube.
4. Diferenciar entre modelos directos, combos de modelos y proveedores gratuitos.

---

## 1.1 ¿Qué es un AI Gateway y por qué lo necesitas?

Cuando utilizas herramientas modernas de desarrollo con IA (como Claude Code, Cursor, Codex CLI, Aider o Cline), cada una de ellas suele conectarse directamente a un proveedor de IA específico (por ejemplo, OpenAI o Anthropic).

Esto genera varios problemas comunes:
- **Fragmentación de llaves y presupuestos**: Tienes que configurar API Keys en múltiples aplicaciones.
- **Interrupciones por límites de frecuencia (*Rate Limits*)**: Si agotas la cuota de un proveedor, tu trabajo se detiene por completo.
- **Costes elevados**: Pagas el precio estándar por cada token enviado y recibido, incluso cuando se envían grandes contextos repetitivos o registros de consola interminables.
- **Falta de visibilidad**: No sabes exactamente cuántos tokens gasta cada herramienta ni cuánto estás pagando al mes en total.

### 💡 La solución: OmniRoute

**OmniRoute** actúa como un punto único de entrada (**un punto de enlace OpenAI-compatible en `http://localhost:20128/v1`**) que se interpone entre tus herramientas de desarrollo y más de 350 proveedores de Inteligencia Artificial.

```
┌─────────────────────────────────────────┐
│ Tus Herramientas de Desarrollo         │
│ (Claude Code, Cursor, Codex, Aider...) │
└────────────────────┬────────────────────┘
                     │ (Solicitudes API OpenAI / Anthropic)
                     ▼
┌─────────────────────────────────────────┐
│        🚀 OmniRoute AI Gateway          │
│       (http://localhost:20128/v1)       │
│                                         │
│  • Compresión de Tokens (RTK/Caveman)   │
│  • Enrutamiento Inteligente (19 tipos)  │
│  • Resiliencia y Fallback Automático    │
└────────────────────┬────────────────────┘
                     │
     ┌───────────────┼───────────────┐
     ▼               ▼               ▼
┌──────────┐   ┌──────────┐   ┌─────────────┐
│ OpenAI / │   │ Anthropic│   │ Proveedores │
│ Gemini   │   │ / Kimi   │   │ Gratis ($0) │
└──────────┘   └──────────┘   └─────────────┘
```

---

## 1.2 Características Principales de OmniRoute

1. **🆓 Gratis desde el primer segundo (Zero-Config)**:
   - Recién instalado, OmniRoute incluye proveedores sin autenticación (como *OpenCode Free*) preconfigurados bajo el modelo virtual `auto`. ¡Puedes hacer preguntas de inmediato sin ingresar tarjetas de crédito ni llaves API!

2. **💰 Acceso a ~1.62 mil millones de tokens gratuitos al mes**:
   - OmniRoute cataloga más de 150 proveedores y niveles gratuitos (*free tiers*), permitiéndote encadenar cuentas y capas gratuitas para programar sin costes.

3. **🔀 19 Estrategias de Enrutamiento y Combos**:
   - Si un proveedor falla, responde con error o agota su cuota, OmniRoute conmuta automáticamente al siguiente proveedor saludable sin interrumpir tu sesión de código.

4. **🗜️ Compresión Inteligente de Tokens (15% - 95%)**:
   - Mediante motores como **RTK** y **Caveman**, OmniRoute limpia y condensa el texto enviado sin perder precisión técnica ni alterar los bloques de código.

5. **🔒 Privado y Local-First**:
   - El servidor corre localmente en tu ordenador. Tus claves de API se guardan cifradas con **AES-256-GCM** y no se envían a servidores intermediarios de terceros.

---

## 1.3 Ejercicios Prácticos de Autoevaluación

Para fijar los conocimientos de esta lección, responde a las siguientes preguntas y realiza el ejercicio reflexivo:

### ❓ Preguntas de Opción Múltiple

**1. ¿Cuál es la función principal de OmniRoute?**
- A) Reemplazar a Node.js en tu sistema operativo.
- B) Actuar como un AI Gateway local que enruta, comprime y gestiona llamadas a modelos de IA.
- C) Crear modelos de lenguaje desde cero en tu GPU.
- *Respuesta correcta: B*

**2. ¿A través de qué puerto por defecto escucha OmniRoute?**
- A) 8080
- B) 3000
- C) 20128
- *Respuesta correcta: C*

**3. ¿Qué sucede si la API Key de un proveedor falla o agota su límite de velocidad cuando usas un Combo en OmniRoute?**
- A) Tu programa se cierra inmediatamente.
- B) OmniRoute conmuta automáticamente al siguiente proveedor o modelo disponible en la cadena (*Fallback*).
- C) Tienes que reiniciar tu ordenador.
- *Respuesta correcta: B*

---

### 📝 Reto Reflexivo Práctico

1. Abre un bloc de notas o terminal en tu equipo.
2. Identifica qué herramientas con IA utilizas actualmente (ej. VS Code, Cursor, scripts de Python, etc.).
3. Anota cuántas claves API distintas estás gestionando en cada una de ellas.
4. Imagina cómo cambiaría tu flujo de trabajo si todas esas herramientas apuntaran a una sola dirección local: `http://localhost:20128/v1`.

---

¡Felicitaciones! Has completado el **Módulo 1**. Estás listo para avanzar al [📦 Módulo 2: Instalación y Configuración Paso a Paso](./modulo-2-instalacion-y-configuracion.md).
