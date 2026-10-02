## Step 3: Implementa y prueba

### Objetivo
Implementar el plan sin escribir el código manualmente.

### 1. Implementación con Copilot Agent

Copia y pega:

```text
Implementa el requerimiento descrito en docs/implementation-plan.md.

Antes de modificar:
1. inspecciona el código existente;
2. identifica los archivos necesarios;
3. respeta la estructura actual;
4. no modifiques funcionalidades fuera del requerimiento.

Implementa:
- Task con priority;
- valores permitidos low, medium y high;
- priority obligatoria al crear;
- priority visible en GET /tasks.

Agrega las pruebas necesarias.

Ejecuta pytest -q.

Al terminar:
- muestra los archivos modificados;
- explica cada cambio;
- indica el resultado de las pruebas;
- no hagas cambios que no estén relacionados con el requerimiento.
```

Revisa el diff y ejecuta:

```bash
pytest -q
```

### 2. Comparación de alternativas

Copia y pega:

```text
Analiza la implementación actual de priority.

No modifiques archivos.

Propón una alternativa para modelar y validar priority y compárala con la implementación actual usando:
- claridad;
- mantenibilidad;
- validación;
- extensibilidad;
- riesgo de errores.

Indica cuál implementación está actualmente en el código y qué ventajas tiene.
```

Crea `docs/implementation-review.md`:

```markdown
# Implementation Review

## Opción implementada
...

## Alternativa
...

## Comparación
| Criterio | Implementada | Alternativa |
|---|---|---|
| Claridad | ... | ... |
| Mantenibilidad | ... | ... |
| Validación | ... | ... |
| Extensibilidad | ... | ... |
| Riesgo | ... | ... |

## Decisión humana
- Opción seleccionada:
- Motivo:
- Qué recomendación de Copilot acepté:
- Qué recomendación modifiqué o rechacé:
```

### 3. Generación de pruebas

Copia y pega:

```text
Diseña e implementa tests/test_priority.py.

Cubre obligatoriamente:
1. low;
2. medium;
3. high;
4. prioridad inválida;
5. prioridad ausente;
6. prioridad devuelta por GET /tasks;
7. creación correcta de una tarea con priority.

Después ejecuta pytest -q.
No modifiques pruebas existentes salvo que sea necesario para mantenerlas correctas.
```

Crea `docs/test-strategy.md`:

```markdown
# Test Strategy

## Escenarios
| Escenario | Qué valida | Resultado |
|---|---|---|
| low | ... | ... |
| medium | ... | ... |
| high | ... | ... |
| inválida | ... | ... |
| ausente | ... | ... |
| GET /tasks | ... | ... |

## Revisión QA

Copia y pega:

"Revisa tests/test_priority.py como QA senior. Busca assertions débiles, falsos positivos y escenarios que podrían pasar aunque la implementación estuviera incorrecta. No modifiques el archivo. Devuelve los hallazgos."

Hallazgos:
- ...

## Verificación humana
- ...
```

### 4. Salida

```bash
pytest -q
```

Deben existir:
- docs/implementation-review.md
- docs/test-strategy.md
- tests/test_priority.py

Haz commit y push.

**Tiempo: 22-24 min.**
