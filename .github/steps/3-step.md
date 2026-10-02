## Step 3: Implementa y prueba

> **Idea clave:** ahora vas a pasar del plan al código, pero manteniendo control sobre cada cambio que propone la IA.

### 1. Implementa con Copilot Agent

Pide a Copilot Agent:

> Implementa el requerimiento de prioridad descrito en docs/implementation-plan.md. Inspecciona el código existente, modifica solo los archivos necesarios, valida low/medium/high, haz que priority sea obligatoria al crear una tarea y agrega las pruebas necesarias. Ejecuta pytest y explícame los cambios.

Antes de aceptar el resultado:
- revisa el diff;
- identifica cada archivo modificado;
- comprueba que cada cambio responde al plan;
- pregunta por cualquier cambio que no entiendas.

Debes conseguir:
- Task contiene priority;
- solo se aceptan low, medium y high;
- crear una tarea exige prioridad;
- GET /tasks devuelve prioridad.

### 2. Comprueba la funcionalidad

Ejecuta:

    pytest -q

Además, prueba manualmente al menos una petición válida y una inválida.

### 3. Compara dos soluciones

Pide a Copilot:

> Propón otra forma de modelar y validar priority. Compara la implementación actual con la alternativa en claridad, mantenibilidad, validación automática y extensibilidad. No cambies el código.

Crea docs/implementation-review.md con esta estructura:

    # Revisión de implementación

    ## Opción implementada
    - Descripción:
    - Cómo funciona:
    - Ventajas:
    - Riesgos:

    ## Alternativa propuesta por Copilot
    - Descripción:
    - Ventajas:
    - Riesgos:

    ## Comparación
    | Criterio | Actual | Alternativa |
    |---|---|---|
    | Claridad | ... | ... |
    | Mantenibilidad | ... | ... |
    | Validación | ... | ... |
    | Extensibilidad | ... | ... |

    ## Decisión humana
    - Qué elegí:
    - Por qué:
    - Qué cambié o rechacé de la propuesta de IA:

### 4. Diseña las pruebas con IA

Pide:

> Diseña una estrategia de pruebas para priority. Enumera primero los escenarios y el riesgo que cubre cada uno. Después implementa tests/test_priority.py.

Cubre:
- low;
- medium;
- high;
- prioridad inválida;
- prioridad ausente;
- prioridad visible en GET /tasks;
- creación de una tarea con prioridad.

Después pide:

> Revisa estas pruebas como QA senior. Busca assertions débiles, falsos positivos y escenarios que podrían pasar aunque la implementación estuviera incorrecta.

Crea docs/test-strategy.md con esta estructura:

    # Estrategia de pruebas

    ## Escenarios cubiertos
    | Escenario | Qué valida | Resultado |
    |---|---|---|
    | ... | ... | ... |

    ## Escenarios no cubiertos
    - ...

    ## Recomendaciones de Copilot
    - ...

    ## Verificación humana
    - Qué revisé:
    - Qué prueba corregí:
    - Por qué:

### 5. Criterios de salida

- [ ] La funcionalidad está implementada.
- [ ] tests/test_priority.py existe.
- [ ] La suite pasa.
- [ ] Existe docs/implementation-review.md.
- [ ] Existe docs/test-strategy.md.
- [ ] Revisaste el diff.
- [ ] Comparaste una alternativa.

Haz commit y push.

**Tiempo sugerido: 22-24 min.**
