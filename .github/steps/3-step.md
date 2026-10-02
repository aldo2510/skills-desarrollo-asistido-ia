## Step 3: Implementa con Copilot Agent

Ahora sí: implementa el plan.

Pide a Copilot Agent:

> Implementa el requerimiento de prioridad descrito en docs/implementation-plan.md. Inspecciona el código existente, modifica los modelos y endpoints necesarios, valida los valores permitidos y agrega las pruebas necesarias. Ejecuta pytest y explícame qué cambiaste.

### Criterios funcionales

Debes conseguir:

- `Task` contiene `priority`;
- la prioridad acepta únicamente `low`, `medium` o `high`;
- crear una tarea exige prioridad;
- GET /tasks devuelve la prioridad;
- existe cobertura de pruebas para los casos válidos e inválidos.

### Trabajo con IA

Antes de aceptar los cambios:

- pide a Copilot que explique el diff;
- pide una segunda alternativa de implementación;
- compara ambas alternativas;
- revisa manualmente el diff;
- ejecuta `pytest -q`.

Documenta en `docs/implementation-review.md` qué solución elegiste y por qué.

Haz commit y push.

**Tiempo sugerido: 15-20 min.**
