## Step 5: Revisión final y reflexión humana

> **Idea clave:** terminar el código no significa terminar el trabajo. La última etapa consiste en demostrar qué decidiste, qué verificaste y dónde mantuviste control humano.

### 1. Revisa toda la evidencia

Comprueba que existan:
- docs/project-analysis.md
- docs/implementation-plan.md
- docs/implementation-review.md
- tests/test_priority.py
- docs/test-strategy.md
- docs/debugging-notes.md
- docs/pr-description.md
- Pull Request abierto contra main

Ejecuta una última vez:

    pytest -q

### 2. Revisa el Pull Request como reviewer

Lee el diff completo y responde:
- ¿el cambio implementa exactamente el requerimiento?
- ¿hay código innecesario?
- ¿las pruebas realmente demuestran el comportamiento?
- ¿el bug de robustez quedó cubierto por una regresión?
- ¿la documentación coincide con lo que realmente se hizo?

Si encuentras un problema, corrígelo y vuelve a ejecutar las pruebas.

### 3. Completa x-review.md

Usa esta estructura:

    # Revisión humana final

    ## 1. Sugerencia de IA que acepté
    - ...

    ## 2. Sugerencia de IA que modifiqué o rechacé
    - ...
    - Motivo:

    ## 3. Defecto que descubrí personalmente
    - ...

    ## 4. Validación que nunca delegaría completamente a la IA
    - ...

    ## 5. Evidencia que me convenció
    - ...

    ## 6. Reflexión
    ### ¿Dónde aportó más valor la IA?
    ...

    ### ¿Dónde fue necesario mi criterio?
    ...

    ### ¿Qué habría ocurrido si aceptaba todos los cambios sin revisar?
    ...

    ### ¿Qué volvería a delegar a Copilot?
    ...

    ### ¿Qué mantendría bajo control humano?
    ...

Haz commit y push.

### 4. Cierre

El objetivo no es demostrar que Copilot puede escribir código.

El objetivo es demostrar que puedes utilizar IA dentro de un ciclo de ingeniería manteniendo:

**contexto → criterio → implementación → pruebas → debugging → revisión humana.**

**Tiempo sugerido: 10-12 min.**
