## Step 2: Convierte el requerimiento en un plan

### Requerimiento

> Las tareas deben tener una prioridad: low, medium o high. La prioridad debe ser obligatoria al crear una tarea y debe aparecer al consultar tareas.

### 1. No implementes todavía

Pide a Copilot que analice el requerimiento y proponga una estrategia:

> Analiza este requerimiento, inspecciona el código y crea un plan detallado de implementación. No implementes todavía. Identifica cambios en modelos, endpoints, validaciones, pruebas y posibles efectos sobre compatibilidad.

Guarda el resultado en `docs/implementation-plan.md`.

### 2. Haz que el plan sea accionable

Debe incluir:

- modelo `Task`;
- modelo de creación;
- POST /tasks;
- GET /tasks;
- validación de `low`, `medium`, `high`;
- estrategia de pruebas;
- impacto en clientes existentes;
- criterios de aceptación;
- riesgos y rollback.

### 3. Revisión humana

Agrega una sección **Decisiones humanas** explicando:

1. qué sugerencia de Copilot aceptaste;
2. qué sugerencia cambiaste o rechazaste;
3. por qué.

Haz commit y push.

**Tiempo sugerido: 10-12 min.**
