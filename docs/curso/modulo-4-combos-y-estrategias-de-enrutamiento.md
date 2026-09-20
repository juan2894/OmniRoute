# 🎯 Módulo 4: Combos y Estrategias de Enrutamiento

En este módulo aprenderás cómo funciona el motor de enrutamiento de OmniRoute, qué son los **Combos**, cómo aprovechar el canal inteligente `auto` y cómo funcionan las **19 estrategias de enrutamiento** y las 3 capas de resiliencia automáticas.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar este módulo serás capaz de:
1. Definir qué es un **Combo** de modelos en OmniRoute.
2. Entender y utilizar las diferentes variantes del canal virtual `auto` (`auto/coding`, `auto/fast`, `auto/cheap`, etc.).
3. Conocer las 19 estrategias de enrutamiento disponibles.
4. Explicar cómo el sistema de resiliencia de 3 capas previene interrupciones (*circuit breaker*, *cooldown* y *lockout*).

---

## 4.1 ¿Qué es un Combo?

Un **Combo** es una secuencia ordenable o agrupada de modelos y proveedores a los que OmniRoute recurre de manera automática.

Si el primer modelo del combo agota su límite de cuota (*Rate Limit / 429*), experimenta un fallo de red o un error del servidor (*500/503*), OmniRoute conmuta al siguiente modelo de la lista en milisegundos sin interrumpir la respuesta al cliente.

```
Petición del Cliente
       │
       ▼
 ┌───────────┐      ¿Responde bien? ──(Sí)──► Retorna Respuesta al Cliente
 │ Modelo A  │ ──┐
 └───────────┘   │ (Error 429 / 5xx / Cooldown)
                 ▼
 ┌───────────┐      ¿Responde bien? ──(Sí)──► Retorna Respuesta al Cliente
 │ Modelo B  │ ──┐
 └───────────┘   │ (Error o Límite alcanzado)
                 ▼
 ┌───────────┐
 │ Modelo C  │ ──────────────────────(Sí)──► Retorna Respuesta al Cliente
 └───────────┘
```

---

## 4.2 El Canal Inteligente Zero-Config: `auto`

No necesitas crear combos manualmente para empezar. OmniRoute incluye un algoritmo de evaluación en tiempo real que calcula **16 factores** (latencia, costo, calidad, historial de fallos, cuota restante) para enrutar tus peticiones.

Puedes usar las siguientes variantes predefinidas según tu objetivo:

| Identificador de Modelo | ¿Para qué sirve? |
| :--- | :--- |
| `auto` | 🎯 Equilibrio general óptimo (mantiene adherencia al último proveedor que funcionó bien - LKGP). |
| `auto/coding` | 🧑‍💻 Ponderación orientada a máxima calidad para generación y refactorización de código. |
| `auto/fast` | ⚡ Prioriza los proveedores con menor latencia p95. |
| `auto/cheap` | 💰 Prioriza los modelos de menor costo o totalmente gratuitos. |
| `auto/smart` | 🔭 Máxima inteligencia + 10% de exploración para descubrir mejores modelos. |
| `auto/offline` | 🔋 Prioriza los proveedores con mayor margen de cuotas y límites holgados. |

---

## 4.3 Las 19 Estrategias de Enrutamiento

Cuando creas tu propio Combo personalizado en el Dashboard (**Combos → Create Combo**), puedes asignar una de las **19 estrategias disponibles**:

1. `priority`: Lista ordenada por prioridad estricta. Agota un proveedor antes de pasar al siguiente.
2. `fill-first`: Llenia la cuota del primer proveedor por completo antes de pasar al segundo.
3. `weighted`: Distribución aleatoria ponderada por pesos definidos.
4. `round-robin`: Turno rotatorio equitativo entre todos los objetivos.
5. `p2c` (*Power of Two Choices*): Elige el mejor de dos candidatos al azar para balanceo de carga eficiente.
6. `least-used`: Selecciona el proveedor con la menor carga de trabajo en ese instante.
7. `random`: Selección aleatoria uniforme.
8. `strict-random`: Aleatorio puro sin deduplicación.
9. `cost-optimized`: Minimiza el costo en dólares utilizando la tabla de precios en vivo.
10. `headroom`: Selecciona el objetivo con mayor cuota restante.
11. `reset-window`: Prefiere el objetivo cuyo reinicio de cuota esté más cercano.
12. `reset-aware`: Ordena por tiempo de reinicio de ventana.
13. `context-relay`: Transfiere contexto en conversaciones largas entre diferentes modelos.
14. `context-optimized`: Elige el modelo con la ventana de contexto idónea para el tamaño del prompt.
15. `cache-optimized`: Fijación de prefijos reutilizables para maximizar aciertos de memoria caché.
16. `lkgp` (*Last-Known-Good Provider*): Mantiene al último proveedor exitoso hasta que presente un fallo.
17. `auto`: Algoritmo inteligente completo de 16 factores.
18. `fusion`: Panel de modelos donde un juez sintetiza la mejor respuesta final.
19. `pipeline`: Encadenamiento de pasos donde la salida de un modelo alimenta al siguiente.

---

## 4.4 Resiliencia en 3 Capas Independientes

OmniRoute previene que tus solicitudes fallen utilizando 3 capas de auto-recuperación:

1. **Capa 1: Circuit Breaker de Proveedor**:
   - Si un proveedor completo falla repetidamente (errores 508, 5xx), el circuito se abre y OmniRoute desvía el tráfico hacia otros proveedores durante un tiempo de enfriamiento (ej. 60 segundos).
2. **Capa 2: Cooldown de Llave/Cuenta**:
   - Si una API Key específica recibe un error `429 Too Many Requests`, esa clave entra en *cooldown* temporal mientras las demás llaves del mismo proveedor siguen atendiendo peticiones.
3. **Capa 3: Lockout de Modelo**:
   - Si un modelo concreto dentro de un proveedor no está disponible (error 404 o denegación de permisos), solo se bloquea ese modelo específico sin afectar al resto de capacidades de la cuenta.

---

## 4.5 Ejercicio Práctico del Módulo 4

Probaremos enviar una petición utilizando la variante orientada a código `auto/coding` y la variante ultrarrápida `auto/fast`.

### 📝 Instrucciones:

Ejecuta los siguientes comandos en tu terminal de pruebas:

#### 🐧 Linux / 🍎 macOS (Bash):
```bash
# Probar variante para código:
curl http://localhost:20128/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "auto/coding",
    "messages": [{"role": "user", "content": "Escribe una función en JS para revertir un string."}]
  }'
```

#### 🪟 Windows (PowerShell):
```powershell
Invoke-RestMethod -Uri "http://localhost:20128/v1/chat/completions" `
  -Method Post `
  -Headers @{"Content-Type"="application/json"} `
  -Body '{
    "model": "auto/coding",
    "messages": [{"role": "user", "content": "Escribe una función en JS para revertir un string."}]
  }'
```

#### 🪟 Windows (CMD):
```cmd
curl http://localhost:20128/v1/chat/completions -H "Content-Type: application/json" -d "{\"model\": \"auto/coding\", \"messages\": [{\"role\": \"user\", \"content\": \"Escribe una función en JS para revertir un string.\"}]}"
```

---

### ❓ Preguntas de Autoevaluación

**1. ¿Qué es un Combo en OmniRoute?**
- A) Un paquete de descuento para comprar más tokens.
- B) Una secuencia o grupo de modelos que OmniRoute enruta con conmutación por error automática.
- C) Una extensión de VS Code.
- *Respuesta correcta: B*

**2. ¿Qué variante del canal `auto` debes utilizar si deseas priorizar la menor latencia de respuesta posible?**
- A) `auto/cheap`
- B) `auto/fast`
- C) `auto/coding`
- *Respuesta correcta: B*

**3. ¿Qué hace la estrategia `cost-optimized`?**
- A) Elimina todas las respuestas del servidor.
- B) Minimiza el costo económico seleccionando la opción de menor precio por token entre los modelos saludables.
- C) Desconecta Internet.
- *Respuesta correcta: B*

---

¡Excelente! Has completado el **Módulo 4**. Avanza al [🗜️ Módulo 5: Compresión de Tokens de IA](./modulo-5-compresion-de-tokens.md).
