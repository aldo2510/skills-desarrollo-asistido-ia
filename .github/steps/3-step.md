## Step 3: Implementa, prueba, depura y prepara el cambio

Esta es la parte principal del laboratorio.

> **Idea clave:** desarrollo asistido por IA no significa "generar código y aceptar". Vas a recorrer un ciclo completo: implementar → comparar → probar → romper → depurar → preparar PR → revisar como humano.

---

### Fase A — Implementación con Copilot Agent

Pide a Copilot Agent:

> Implementa el requerimiento de prioridad descrito en docs/implementation-plan.md. Inspecciona el código existente, modifica los modelos y endpoints necesarios, valida los valores permitidos y agrega las pruebas necesarias. Ejecuta pytest y explícame qué cambiaste. No modifiques archivos que no sean necesarios.

Antes de aceptar los cambios:

1. revisa el diff;
2. identifica qué archivos cambió;
3. verifica que cada cambio tenga relación con el requerimiento;
4. pregunta a Copilot por cualquier línea que no entiendas.

Debes conseguir:
- `Task` contiene `priority`;
- solo se aceptan `low`, `medium` o `high`;
- crear una tarea exige prioridad;
- GET /tasks devuelve prioridad.

### Fase B — Contrasta soluciones

No asumas que la primera solución es la única.

Pide una segunda propuesta:

> Propón otra forma de modelar y validar priority. Compara mantenibilidad, claridad, validación automática, extensibilidad y riesgo con la implementación actual. No cambies el código.

Documenta en `docs/implementation-review.md`:

- opción elegida;
- alternativa considerada;
- ventajas y riesgos;
- qué cambiaste de la propuesta de Copilot;
- por qué la solución final es adecuada para este ejercicio.

### Fase C — Pruebas como actividad de ingeniería

Pide a Copilot:

> Diseña una estrategia de pruebas para priority. Primero enumera los escenarios y explica qué riesgo cubre cada uno. Después implementa tests/test_priority.py.

Cubre como mínimo:
- `low`;
- `medium`;
- `high`;
- prioridad inválida;
- prioridad ausente;
- prioridad visible en GET /tasks;
- creación de una tarea con prioridad.

Ejecuta:

```bash
pytest -q
```

Después pide:

> Revisa estas pruebas como QA senior. Busca falsos positivos, assertions débiles y escenarios que podrían pasar aunque la implementación estuviera incorrecta.

Corrige cualquier prueba débil.

### Fase D — Debugging intencional

Ahora vas a investigar un problema diferente al requerimiento principal.

La función `create_task` contiene una debilidad: si la colección de tareas queda vacía, el cálculo del siguiente ID puede fallar.

La idea es experimentar con IA como herramienta de diagnóstico.

Pide a Copilot:

> Analiza create_task. ¿Qué ocurre si tasks está vacío? Antes de proponer una corrección, explícame cómo reproducir el problema y qué prueba de regresión debería existir.

Después:

1. reproduce el fallo;
2. crea una prueba de regresión;
3. ejecuta únicamente esa prueba y observa el fallo;
4. pide a Copilot que explique la causa raíz;
5. pide al menos dos posibles correcciones;
6. elige una;
7. revisa el diff;
8. ejecuta toda la suite.

Documenta en `docs/debugging-notes.md`:

- síntoma;
- reproducción;
- causa raíz;
- hipótesis descartadas;
- alternativas consideradas;
- corrección elegida;
- evidencia de pruebas.

> **Pregunta importante:** ¿la IA encontró la causa raíz o simplemente reconoció un patrón conocido? Explica cómo lo comprobaste.

### Fase E — Pull Request

Usa Copilot para preparar `docs/pr-description.md`.

Pide:

> Genera una descripción de Pull Request para este cambio. Resume problema, solución, archivos modificados, pruebas ejecutadas, riesgos, rollback y decisiones humanas. No inventes evidencia: usa solo lo que realmente existe en el repositorio.

Incluye:
- problema;
- solución;
- archivos modificados;
- pruebas;
- riesgos;
- rollback;
- decisiones humanas;
- limitaciones conocidas.

Crea una rama y abre un Pull Request contra `main`.

**No hagas merge todavía.**

### Fase F — Revisión humana del PR

Lee el diff completo del PR como si fueras reviewer.

Busca:

- cambios no relacionados;
- validaciones faltantes;
- tests que podrían dar falsos positivos;
- nombres poco claros;
- comportamiento inesperado;
- documentación que afirma algo que no está demostrado.

Completa `x-review.md` con:

- una sugerencia de IA que aceptaste;
- una que modificaste o rechazaste;
- una validación que nunca delegarías a la IA;
- un defecto que descubriste tú;
- qué evidencia te convenció de que el cambio funciona.

Haz commit y push.

### Fase G — Reflexión

Antes de terminar, responde:

1. ¿En qué fase la IA aportó más valor?
2. ¿En qué fase necesitaste más criterio humano?
3. ¿Qué habría pasado si hubieras aceptado todos los cambios sin revisar el diff?
4. ¿Qué tarea le volverías a delegar a Copilot en un proyecto real?
5. ¿Qué tarea mantendrías bajo control humano?

**Tiempo sugerido: 50-60 min.**

**Tiempo total acumulado del ejercicio: aproximadamente 80-90 min.**
