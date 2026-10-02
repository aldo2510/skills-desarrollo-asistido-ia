## Step 3: Implementa, prueba, depura y prepara el cambio

Esta es la parte principal del laboratorio. Trabaja como si estuvieras atendiendo un cambio real de producto.

### Fase A — Implementación con Copilot Agent

Pide a Copilot Agent:

> Implementa el requerimiento de prioridad descrito en docs/implementation-plan.md. Inspecciona el código existente, modifica los modelos y endpoints necesarios, valida los valores permitidos y agrega las pruebas necesarias. Ejecuta pytest y explícame qué cambiaste.

Debes conseguir:
- Task contiene priority.
- Solo se aceptan low, medium o high.
- Crear una tarea exige prioridad.
- GET /tasks devuelve prioridad.

### Fase B — Contrasta soluciones

Pide una segunda propuesta:

> Propón otra forma de modelar y validar priority. Compara mantenibilidad, claridad y riesgo con la implementación actual.

Documenta en docs/implementation-review.md:
- opción elegida;
- alternativa considerada;
- ventajas y riesgos;
- qué cambiaste de la propuesta de Copilot.

### Fase C — Pruebas

Pide a Copilot que genere tests/test_priority.py.

Cubre low, medium, high, prioridad inválida, prioridad ausente y prioridad visible en GET /tasks.

Ejecuta:

    pytest -q

Pide a Copilot una revisión tipo QA y corrige cualquier prueba que no compruebe realmente el requerimiento.

### Fase D — Debugging

Investiga un bug deliberado en create_task: si la colección de tareas está vacía, el cálculo del siguiente ID puede fallar.

Pide a Copilot que:
1. explique cómo reproducirlo;
2. proponga una prueba de regresión;
3. identifique la causa raíz;
4. proponga una corrección.

Reproduce el fallo, corrige el código y vuelve a ejecutar toda la suite.

Documenta en docs/debugging-notes.md:
- síntoma;
- reproducción;
- causa raíz;
- hipótesis descartadas;
- corrección;
- evidencia de pruebas.

### Fase E — Pull Request

Usa Copilot para preparar docs/pr-description.md.

Incluye problema, solución, archivos modificados, pruebas, riesgos, rollback y decisiones humanas.

Crea una rama y abre un Pull Request contra main. No hagas merge todavía.

### Fase F — Revisión humana

Completa x-review.md con:
- una sugerencia de IA que aceptaste;
- una que modificaste o rechazaste;
- una validación que nunca delegarías a la IA.

Haz commit y push.

**Tiempo sugerido: 45-55 min.**
