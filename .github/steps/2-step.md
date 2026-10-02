## Step 2: Convierte el requerimiento en un plan

### Requerimiento

Agregar prioridad a las tareas.

Reglas:
- valores permitidos: `low`, `medium`, `high`;
- la prioridad es obligatoria al crear una tarea;
- `GET /tasks` debe devolverla;
- las pruebas deben cubrir los nuevos escenarios;
- no cambiar funcionalidades que no estén relacionadas.

### 1. Copia y pega este prompt en Copilot

```text
Analiza el requerimiento de agregar priority a Task.

Requerimiento:
- priority debe aceptar únicamente low, medium o high;
- priority es obligatoria al crear una tarea;
- GET /tasks debe devolver priority;
- debemos agregar pruebas;
- no debemos cambiar funcionalidades no relacionadas.

No modifiques archivos.

Genera un plan de implementación que incluya:
1. archivos que habría que modificar;
2. archivos que habría que crear;
3. cambios en modelos;
4. cambios en endpoints;
5. estrategia de validación;
6. pruebas necesarias;
7. riesgos;
8. criterios de aceptación;
9. una alternativa de implementación y sus ventajas y riesgos.

Termina con una lista de decisiones que requieren revisión humana.
```

### 2. Crea el documento

Crea `docs/implementation-plan.md` con:

```markdown
# Implementation Plan

## 1. Requerimiento
...

## 2. Archivos a modificar
- ...

## 3. Archivos a crear
- ...

## 4. Cambios de modelo
- ...

## 5. Cambios de API
- ...

## 6. Estrategia de validación
- ...

## 7. Pruebas necesarias
- ...

## 8. Criterios de aceptación
- [ ] ...
- [ ] ...
- [ ] ...

## 9. Riesgos
| Riesgo | Impacto | Mitigación |
|---|---|---|
| ... | ... | ... |

## 10. Alternativa de implementación
### Alternativa
...

### Ventajas
...

### Riesgos
...

## 11. Decisiones humanas
- ...
```

### 3. Revisión del plan

Copia y pega:

```text
Revisa docs/implementation-plan.md contra el requerimiento original.

No modifiques ningún archivo.

Devuelve una tabla con:
- requisito;
- dónde está cubierto en el plan;
- evidencia;
- qué falta, si falta.

Después indica si el plan contiene cambios innecesarios o riesgos no considerados.
```

Aplica las correcciones necesarias al documento.

### 4. Verificación

```bash
test -f docs/implementation-plan.md
```

Haz commit y push.

**Tiempo: 15-17 min.**
