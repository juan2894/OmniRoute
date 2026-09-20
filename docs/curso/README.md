# 🎓 Curso Completo de OmniRoute: De Cero a Experto

Bienvenido al **Curso Práctico de OmniRoute**, el pasarela de IA (*AI Gateway*) de código abierto, local y gratuita. Este curso está diseñado especialmente para principiantes y desarrolladores que desean aprender desde cero a unificar, optimizar, enrutar y comprimir sus consultas de Inteligencia Artificial para todas sus herramientas de desarrollo.

---

## 🎯 ¿Qué aprenderás en este curso?

Al finalizar este curso serás capaz de:
1. **Comprender la arquitectura** y el funcionamiento interno de un AI Gateway local.
2. **Instalar y configurar OmniRoute** en cualquier entorno (Windows con PowerShell/CMD, macOS o Linux, y Docker).
3. **Aprovechar más de 1.62 mil millones de tokens gratuitos al mes** combinando más de 150 proveedores del tier gratuito sin pagar suscripciones costosas.
4. **Configurar combos de modelos y estrategias avanzadas de enrutamiento** para tener resiliencia total y tolerancia a fallos.
5. **Reducir tu consumo de tokens entre un 15% y un 95%** utilizando la pila de 12 motores de compresión (como RTK y Caveman).
6. **Integrar OmniRoute con tus herramientas diarias**: Claude Code, Cursor, Codex CLI, Aider, Cline, OpenCode, VS Code, así como agentes MCP y A2A.
7. **Resolver problemas habituales** y desplegar soluciones prácticas en tus proyectos reales.

---

## 📌 Requisitos Previos

- **Conocimientos informáticos básicos**: Manejo de la consola/terminal de comandos (PowerShell, CMD o Bash).
- **Node.js**: Versión 22 o superior (recomendado para ejecución con `npm` o `npx`).
- **Ganas de aprender y ahorrar dinero** en uso de modelos de lenguaje (LLMs).

---

## 📚 Estructura del Curso

El curso está organizado en **7 módulos progresivos**. Cada módulo incluye explicación teórica, ejemplos prácticos paso a paso (con comandos adaptados para Bash, Windows PowerShell y CMD) y ejercicios prácticos de autoevaluación al final.

### [🚀 Módulo 1: Introducción a OmniRoute](./modulo-1-introduccion.md)
- ¿Qué es un AI Gateway y por qué lo necesitas?
- Arquitectura general y funcionamiento de un proxy local.
- Beneficios clave: Resiliencia, ahorro de costes, privacidad y unificación de APIs.
- Ejercicio práctico de autoevaluación.

### [📦 Módulo 2: Instalación y Configuración Paso a Paso](./modulo-2-instalacion-y-configuracion.md)
- Instalación mediante `npm`, Docker, Bun y desde código fuente.
- Comandos específicos para Linux/macOS (Bash) y Windows (PowerShell / CMD).
- Configuración de variables de entorno (`.env`) y puerto de servicio (`20128`).
- Exploración de la interfaz web (Dashboard) y comprobación del estado del sistema.
- Ejercicio práctico de instalación y diagnóstico (`omniroute doctor`).

### [🌐 Módulo 3: Proveedores y Catálogo del Tier Gratuito](./modulo-3-proveedores-y-tier-gratuito.md)
- Conexión de proveedores con API Key (OpenAI, Anthropic, Gemini, Kimi, etc.).
- Conexión de proveedores sin autenticación ni clave (OpenCode Free, Pollinations, etc.).
- Entendiendo el catálogo del *Free Tier* (~1.62B tokens/mes).
- Ejercicio práctico: Tu primera llamada API sin pagar un solo centavo.

### [🎯 Módulo 4: Combos y Estrategias de Enrutamiento](./modulo-4-combos-y-estrategias-de-enrutamiento.md)
- El concepto de **Combo** y el modelo inteligente `auto`.
- Las 19 estrategias de enrutamiento (`priority`, `cost-optimized`, `headroom`, `lkgp`, `fusion`, etc.).
- Sistema de resiliencia de 3 capas: *Circuit Breaker*, *Cooldown* de llaves y *Lockout* de modelos.
- Ejercicio práctico: Crear un combo con conmutación por error (*fallback*) automática.

### [🗜️ Módulo 5: Compresión de Tokens de IA](./modulo-5-compresion-de-tokens.md)
- ¿Por qué comprimir tokens? Economía, velocidad y límites de contexto.
- La pila de 12 motores de compresión: RTK, Caveman, Session-Dedup, Lite, Ultra, etc.
- Preservación inteligente de código, JSON y URLs.
- Ejercicio práctico: Reducción de prompt en vivo y comparación antes/después.

### [🤖 Módulo 6: Integración con CLIs, IDEs y Agentes](./modulo-6-integracion-con-clis-y-agentes.md)
- Configuración en una línea con `omniroute run` y `omniroute configure`.
- Integración con **Claude Code**, **Cursor**, **Codex CLI**, **Aider**, **Cline** y **VS Code**.
- Conexión con agentes usando **MCP** (Model Context Protocol) y **A2A** (Agent-to-Agent).
- Ejercicio práctico: Utilizar Claude Code conectado a OmniRoute con un modelo gratuito.

### [💡 Módulo 7: Proyectos Prácticos y Solución de Problemas](./modulo-7-proyectos-practicos-y-casos-de-uso.md)
- **Proyecto Integrador 1**: Flujo de desarrollo continuo de software a coste $0.
- **Proyecto Integrador 2**: Enrutador resiliente para producción multi-proveedor.
- Guía completa de solución de problemas (*Troubleshooting*) comunes en Windows, macOS y Linux.
- Examen final y recomendaciones para continuar.

---

¡Empieza ahora mismo abriendo el [Módulo 1: Introducción a OmniRoute](./modulo-1-introduccion.md)! 🚀
