## Step 2: Convierte el requerimiento en un plan

> **Idea clave:** una buena interacción con IA no empieza con "hazlo". Empieza con contexto, restricciones, criterios de aceptación y una decisión explícita sobre qué se quiere construir.

### Requerimiento

> Las tareas deben tener una prioridad: `low`, `medium` o `high`. La prioridad debe ser obligatoria al crear una tarea y debe aparecer al consultar tareas.

### ¿Qué problema estamos resolviendo?

Parece un cambio pequeño, pero afecta varias capas:

```
Requerimiento
    ↓
Modelo de datos
    ↓
Entrada HTTP / validación
    ↓
Lógica de aplicación
    ↓
Respuesta API
    ↓
Pruebas
    ↓
Clientes existentes
```

Tu objetivo es aprender a **mapear el impacto antes de escribir código**.

### 1. No implementes todavía

Pide a Copilot que analice el requerimiento:

> Analiza este requerimiento, inspecciona el código y crea un plan detallado de implementación. No implementes todavía. Identifica cambios en modelos, endpoints, validaciones, pruebas y posibles efectos sobre compatibilidad.

Después pide una segunda opinión:

> Revisa el plan anterior como arquitecto de software. Busca supuestos ocultos, cambios innecesarios, riesgos de compatibilidad y casos de prueba que falten.

Guarda el resultado en `docs/implementation-plan.md`.

### 2. Haz que el plan sea accionable

El documento debe incluir:

- modelo `Task`;
- modelo de creación;
- POST /tasks;
- GET /tasks;
- validación de `low`, `medium`, `high`;
- estrategia de pruebas;
- impacto en clientes existentes;
- criterios de aceptación;
- riesgos y rollback;
- archivos que probablemente deberán modificarse;
- orden recomendado de implementación.

### 3. Diseña los criterios de aceptación

No te limites a decir "debe funcionar".

Escribe criterios verificables, por ejemplo:

- una tarea con `priority=low` se crea correctamente;
- una tarea con `priority=medium` se crea correctamente;
- una tarea con `priority=high` se crea correctamente;
- un valor distinto de los tres permitidos es rechazado;
- una petición sin prioridad es rechazada;
- `GET /tasks` devuelve la prioridad.

Luego pregunta a Copilot:

> ¿Puedes encontrar algún caso de aceptación ambiguo o que no sea comprobable automáticamente?

### 4. Compara alternativas

Pide:

> Propón dos formas de representar y validar priority en FastAPI/Pydantic. Compara claridad, mantenibilidad, validación automática, extensibilidad y riesgo de errores. No cambies el código.

Documenta brevemente las dos alternativas y cuál prefieres.

### 5. Revisión humana

Agrega una sección **Decisiones humanas** explicando:

1. qué sugerencia de Copilot aceptaste;
2. qué sugerencia cambiaste o rechazaste;
3. por qué;
4. qué decisión consideras demasiado importante para delegarla completamente a la IA.

### 6. Pregunta de cierre

Antes del commit, responde:

> Si Copilot implementara exactamente su primera propuesta, ¿qué parte revisarías primero y por qué?

Haz commit y push.

**Tiempo sugerido: 15-17 min.**
