## Step 2: Convierte el requerimiento en un plan

> **Idea clave:** una buena interacción con IA no empieza con “hazlo”. Empieza con contexto, restricciones, criterios de aceptación y una decisión explícita sobre qué se quiere construir.

### Requerimiento

> Las tareas deben tener una prioridad: `low`, `medium` o `high`. La prioridad debe ser obligatoria al crear una tarea y debe aparecer al consultar tareas.

### ¿Qué vas a practicar?

En este paso todavía **no vas a implementar código**. Vas a usar Copilot para transformar un requerimiento funcional en un plan técnico verificable.

El flujo es:

```text
Requerimiento
    ↓
Impacto técnico
    ↓
Alternativas
    ↓
Criterios de aceptación
    ↓
Plan de implementación
    ↓
Revisión humana
```

### 1. Pide un primer plan a Copilot

Usa:

> Analiza este requerimiento, inspecciona el código y crea un plan detallado de implementación. No implementes todavía. Identifica cambios en modelos, endpoints, validaciones, pruebas y posibles efectos sobre compatibilidad.

Después pide una segunda revisión:

> Revisa el plan anterior como arquitecto de software. Busca supuestos ocultos, cambios innecesarios, riesgos de compatibilidad y casos de prueba que falten. No cambies ningún archivo.

### 2. Compara alternativas antes de decidir

Pregunta:

> Propón dos formas de representar y validar priority en FastAPI/Pydantic. Compara claridad, mantenibilidad, validación automática, extensibilidad y riesgo de errores. No cambies el código.

No necesitas elegir lo que Copilot recomiende. Debes justificar tu decisión.

### 3. Crea `docs/implementation-plan.md`

**El archivo no existe inicialmente. Debes crearlo.**

Copia esta plantilla y complétala con información de este proyecto:

```markdown
# Plan de implementación: prioridad de tareas

## 1. Requerimiento

Resume el cambio solicitado en tus propias palabras.

## 2. Estado actual

Explica cómo funciona hoy:
- Task;
- TaskCreate;
- POST /tasks;
- GET /tasks;
- validaciones actuales;
- pruebas relacionadas.

## 3. Impacto técnico

| Componente | Cambio esperado | Motivo |
|---|---|---|
| Task | ... | ... |
| TaskCreate | ... | ... |
| POST /tasks | ... | ... |
| GET /tasks | ... | ... |
| Pruebas | ... | ... |

## 4. Archivos que probablemente cambiarán

| Archivo | Cambio previsto |
|---|---|
| app/main.py | ... |
| tests/... | ... |

Agrega otros archivos solo si realmente son necesarios.

## 5. Alternativas consideradas

### Alternativa A
- Descripción:
- Ventajas:
- Riesgos:

### Alternativa B
- Descripción:
- Ventajas:
- Riesgos:

## 6. Decisión de diseño

- Alternativa elegida:
- Motivo:
- Qué recomendó Copilot:
- Qué decidí yo:

## 7. Criterios de aceptación

Incluye como mínimo:

- [ ] Una tarea con priority=low se crea correctamente.
- [ ] Una tarea con priority=medium se crea correctamente.
- [ ] Una tarea con priority=high se crea correctamente.
- [ ] Un valor distinto de low/medium/high es rechazado.
- [ ] Una petición sin priority es rechazada.
- [ ] GET /tasks devuelve priority.

Agrega cualquier otro criterio que consideres necesario.

## 8. Estrategia de pruebas

| Escenario | Tipo de prueba | Resultado esperado |
|---|---|---|
| low | ... | ... |
| medium | ... | ... |
| high | ... | ... |
| valor inválido | ... | ... |
| campo ausente | ... | ... |
| consulta GET | ... | ... |

## 9. Compatibilidad

Explica:
- qué podría ocurrir con clientes que hoy crean tareas sin priority;
- si el cambio es backward compatible;
- qué decisión tomarías en un sistema real.

## 10. Riesgos

| Riesgo | Impacto | Mitigación |
|---|---|---|
| ... | ... | ... |
| ... | ... | ... |

## 11. Rollback

Explica cómo revertirías el cambio si genera problemas.

## 12. Orden de implementación

1. ...
2. ...
3. ...
4. ...

## 13. Decisiones humanas

### Sugerencia de Copilot que acepté
...

### Sugerencia que modifiqué o rechacé
...

### Motivo
...

### Decisión que no delegaría completamente a la IA
...

## 14. Pregunta de revisión

Si Copilot implementara exactamente su primera propuesta, ¿qué parte revisarías primero y por qué?
```

### 4. Revisa la calidad del plan

Antes de hacer commit, comprueba:

- [ ] El plan describe el estado actual antes del cambio.
- [ ] Identifica los componentes afectados.
- [ ] Incluye al menos dos alternativas.
- [ ] Define criterios de aceptación verificables.
- [ ] Define una estrategia de pruebas.
- [ ] Considera compatibilidad.
- [ ] Incluye riesgos y mitigaciones.
- [ ] Incluye rollback.
- [ ] Explica decisiones humanas.
- [ ] Todavía no modificaste la implementación.

Haz commit y push.

**Tiempo sugerido: 15-17 min.**
