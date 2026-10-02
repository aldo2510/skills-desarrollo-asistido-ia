# Step 2 — Convierte el requerimiento en un plan

## Objetivo
Transformar el requerimiento en cambios, pruebas y criterios verificables sin inventar trabajo.

## Requerimiento
Agregar `priority` a las tareas. Solo se permiten `low`, `medium` y `high`. El campo es obligatorio al crear y debe aparecer al consultar tareas.

## Prompt opcional para Copilot
~~~text
Analiza el requerimiento de priority y el código actual.
No modifiques archivos ni escribas código.
Propón archivos a modificar, archivos a crear, impacto en modelos y endpoints, pruebas, criterios de aceptación, riesgos y rollback.
~~~

## 1. Crea docs/implementation-plan.md

~~~markdown
# Implementation Plan

## 1. Requerimiento
Agregar priority a las tareas con valores permitidos low, medium y high. El campo es obligatorio al crear y debe devolverse en las respuestas.

## 2. Estado actual
La API tiene Task, TaskCreate, POST /tasks y GET /tasks. Las tareas se almacenan en memoria.

## 3. Impacto técnico
| Componente | Cambio | Motivo |
|---|---|---|
| Task | Agregar priority | Exponer prioridad |
| TaskCreate | Agregar priority obligatoria | Validar entrada |
| POST /tasks | Persistir priority | Conservar el dato |
| GET /tasks | Devolver priority | Exponer el dato |
| Tareas iniciales | Asignar priority válida | Mantener contrato |
| Tests | Cubrir valores y obligatoriedad | Evitar regresiones |

## 4. Archivos a modificar
- app/main.py
- tests/test_api.py

## 5. Archivos a crear
- tests/test_priority.py
- docs/test-strategy.md
- docs/implementation-review.md

## 6. Alternativas
### Alternativa A
Validar priority en el modelo de entrada.

### Alternativa B
Validar manualmente dentro del endpoint.

## 7. Criterios de aceptación
- low, medium y high son válidos.
- Un valor fuera del conjunto es rechazado.
- Omitir priority al crear es rechazado.
- POST conserva priority.
- GET devuelve priority.
- Las pruebas existentes siguen pasando.

## 8. Riesgos
- Romper clientes que no envíen priority.
- Introducir validación inconsistente.
- Modificar comportamiento fuera de alcance.

## 9. Rollback
Revertir el commit que introduce priority y ejecutar nuevamente pytest.

## 10. Evidencia
El plan debe contrastarse con app/main.py y tests/test_api.py antes de implementar.
~~~

## 2. Verificación
~~~bash
test -f docs/implementation-plan.md
grep -Eiq 'low|medium|high' docs/implementation-plan.md
grep -Eiq 'criterios|aceptaci' docs/implementation-plan.md
grep -Eiq 'riesgo|rollback' docs/implementation-plan.md
~~~

## 3. Commit
~~~bash
git add docs/implementation-plan.md
git commit -m "docs: create implementation plan"
git push
~~