# 🗜️ Módulo 5: Compresión de Tokens de IA

En este módulo aprenderás cómo funciona el sistema de compresión de tokens de OmniRoute, capaz de reducir entre un **15% y un 95%** de los tokens consumidos en cada interacción sin perder precisión técnica ni corromper tu código.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar este módulo serás capaz de:
1. Comprender por qué la compresión de tokens ahorra dinero y amplía la ventana de contexto.
2. Identificar los componentes de la pila de **12 motores de compresión**.
3. Reconocer los motores insignia **RTK** y **Caveman**.
4. Activar y ajustar modos de compresión en tus consultas o mediante encabezados.

---

## 5.1 ¿Por qué comprimir tokens?

Los modelos de lenguaje cobran por el volumen de texto enviado en la solicitud (*Input Tokens*) y generado en la respuesta (*Output Tokens*). Además, cuando utilizas herramientas CLI como Claude Code o Aider, los comandos de consola, diferencias de código (*git diffs*) y rastreos de errores añaden miles de tokens redundantes a la conversación.

### Beneficios de la compresión:
- **Reducción de costos directa**: Hasta 90% menos de gasto en solicitudes pesadas.
- **Respuesta más rápida**: Menos tokens implican menor tiempo de procesamiento.
- **Mayor espacio en la ventana de contexto**: Evita llegar al límite máximo del modelo en conversaciones largas.

---

## 5.2 La Pila de 12 Motores de Compresión

OmniRoute cuenta con una canalización (*pipeline*) de 12 motores independientes que pueden combinarse o activarse según las necesidades del flujo:

```
 Prompt Original (ej. 10,000 tokens)
                  │
                  ▼
 1. Session-Dedup  ──► (Elimina bloques repetidos en la conversación)
 2. CCR            ──► (Sustituye grandes bloques por marcas de recuperación)
 3. Lite           ──► (Limpia espacios en blanco y formato innecesario)
 4. RTK            ──► (Filtra y condensa salidas de consola y herramientas CLI)
 5. Tool Output    ──► (Compactación JSON de salidas de herramientas)
 6. Headroom       ──► (Compresión tabular de arreglos JSON)
 7. Relevance      ──► (Alineación con la última pregunta del usuario)
 8. Caveman        ──► (Condensa la prosa quitando relleno gramatical)
 9. Aggressive     ──► (Resumen y envejecimiento de turnos antiguos)
 10. LLMLingua-2   ──► (Poda semántica mediante aprendizaje automático)
 11. Ultra         ──► (Poda heurística avanzada)
 12. OmniGlyph     ──► (Codificación de contexto)
                  │
                  ▼
 Contexto Comprimido Final (ej. ~1,080 tokens - Ahorro del ~89%)
```

---

## 5.3 Motores Destacados: RTK y Caveman

### 🧰 RTK (Rust Token Killer)
Diseñado específicamente para logs de consola, salidas de tests, resultados de builds y salidas de git. RTK elimina líneas repetitivas, encabezados irrelevantes e información superflua manteniendo los mensajes de error clave.

### 🪨 Caveman (Prosa Condensada)
Inspirado en el principio de *"¿Por qué usar muchas palabras si pocas palabras bastan?"*, Caveman condensa la prosa explicativa eliminando rodeos, artículos prescindibles y lenguaje de relleno.

#### Ejemplo de condensación con Caveman:

- **Prosa original (42 tokens)**:
  > *"El problema principal por el cual tu componente de React se está volviendo a renderizar es que estás creando un nuevo objeto en cada ciclo de renderizado. Te recomendaría usar el hook useMemo."*

- **Texto comprimido (12 tokens)**:
  > *"Re-render: objeto nuevo cada ciclo. Usar hook `useMemo`."*

**Ganas el mismo significado técnico con un 70% menos de tokens.**

---

## 5.4 Preservación Inteligente e Inviolable

Muchos desarrolladores temen que al comprimir se altere el código. **OmniRoute incluye un motor de preservación estricto**:

- ❌ **Lo que SÍ se comprime**: Salidas de terminal, textos de relleno, conversaciones antiguas, explicaciones largas.
- ✅ **Lo que NUNCA se altera**: Bloques de código (sintaxis exacta), URLs, cadenas de formato JSON y datos estructurados.

---

## 5.5 Modos y Modificadores de Compresión

Puedes solicitar un nivel de compresión enviando el encabezado HTTP `x-omniroute-compression`:

| Modo | Ahorro estimado | Recomendado para |
| :--- | :--- | :--- |
| `lite` | ~15% | Uso general seguro siempre activo |
| `standard` | ~30% | Desarrollo de código diario |
| `aggressive` | ~50% | Sesiones largas con muchas herramientas |
| `ultra` | ~75% | Máximo ahorro en grandes proyectos |
| `rtk` | 60% – 90% | Logs de consola, ejecuciones de test y git |
| `stacked` | **78% – 95%** | Combinación de RTK y Caveman |

---

## 5.6 Ejercicio Práctico del Módulo 5

Enviaremos una solicitud solicitando el modo de compresión `stacked` para observar cómo responde OmniRoute.

### 📝 Instrucciones:

Ejecuta el siguiente comando en tu terminal:

#### 🐧 Linux / 🍎 macOS (Bash):
```bash
curl http://localhost:20128/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "x-omniroute-compression: stacked" \
  -d '{
    "model": "auto",
    "messages": [
      {"role": "user", "content": "Explícame de forma detallada qué es el patrón Singleton en programación orientada a objetos."}
    ]
  }'
```

#### 🪟 Windows (PowerShell):
```powershell
Invoke-RestMethod -Uri "http://localhost:20128/v1/chat/completions" `
  -Method Post `
  -Headers @{
    "Content-Type"="application/json"
    "x-omniroute-compression"="stacked"
  } `
  -Body '{
    "model": "auto",
    "messages": [
      {"role": "user", "content": "Explícame de forma detallada qué es el patrón Singleton en programación orientada a objetos."}
    ]
  }'
```

#### 🪟 Windows (CMD):
```cmd
curl http://localhost:20128/v1/chat/completions -H "Content-Type: application/json" -H "x-omniroute-compression: stacked" -d "{\"model\": \"auto\", \"messages\": [{\"role\": \"user\", \"content\": \"Explícame de forma detallada qué es el patrón Singleton en programación orientada a objetos.\"}]}"
```

---

### ❓ Preguntas de Autoevaluación

**1. ¿Qué elementos están estrictamente protegidos durante la compresión para evitar que sufran modificaciones?**
- A) Explicaciones teóricas largo formato.
- B) Bloques de código sintáctico, URLs y estructuras JSON.
- C) Los saltos de línea de la consola.
- *Respuesta correcta: B*

**2. ¿Qué motor de la pila está especializado en la compresión de salidas de herramientas CLI y logs de consola?**
- A) Caveman
- B) RTK (Rust Token Killer)
- C) Session-Dedup
- *Respuesta correcta: B*

**3. ¿Qué porcentaje aproximado de ahorro se logra al combinar RTK y Caveman en modo `stacked`?**
- A) Entre 5% y 10%.
- B) Entre 78% y 95%.
- C) Exactamente 0%.
- *Respuesta correcta: B*

---

¡Excelente! Has completado el **Módulo 5**. Avanza al [🤖 Módulo 6: Integración con CLIs, IDEs y Agentes](./modulo-6-integracion-con-clis-y-agentes.md).
