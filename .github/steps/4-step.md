## Step 4: Depura y prepara el Pull Request

> **Idea clave:** una IA puede encontrar un bug rápidamente, pero el aprendizaje está en demostrar cómo se reproduce, cómo se identifica la causa raíz y cómo se comprueba la corrección.

### 1. Investiga el bug deliberado

La función create_task tiene una debilidad: si la colección de tareas queda vacía, el cálculo del siguiente ID puede fallar.

Pide a Copilot:

> Analiza create_task. ¿Qué ocurre si tasks está vacío? No corrijas todavía. Explícame cómo reproducir el problema y qué prueba de regresión debería existir.

### 2. Reproduce antes de corregir

Primero crea una prueba que reproduzca el problema.

Ejecuta únicamente esa prueba y observa el fallo.

Después pide:

> Explica la causa raíz basándote en el código y en el fallo observado. Propón al menos dos correcciones posibles y compara sus riesgos.

Elige una solución y revisa el diff antes de aceptarla.

Vuelve a ejecutar:

    pytest -q

### 3. Documenta el debugging

Crea docs/debugging-notes.md con esta estructura:

    # Debugging notes

    ## Síntoma
    ¿Qué fallaba?

    ## Reproducción
    ¿Qué pasos o prueba reproducían el fallo?

    ## Causa raíz
    ¿Qué línea o lógica provocaba el problema?

    ## Hipótesis descartadas
    - ...

    ## Alternativas consideradas
    ### Alternativa 1
    - ...
    ### Alternativa 2
    - ...

    ## Corrección elegida
    - ...

    ## Evidencia
    - Prueba de regresión:
    - Suite completa:
    - Resultado:

    ## Verificación humana
    ¿Cómo comprobaste que la corrección realmente resuelve el problema?

### 4. Prepara el Pull Request

Pide a Copilot:

> Genera una descripción de Pull Request para este cambio usando únicamente evidencia existente en el repositorio. Incluye problema, solución, archivos modificados, pruebas ejecutadas, riesgos, rollback, decisiones humanas y limitaciones. No inventes resultados.

Crea docs/pr-description.md con:

    # Pull Request: Task Priority

    ## Problema
    ...

    ## Solución
    ...

    ## Archivos modificados
    - ...

    ## Pruebas ejecutadas
    - ...

    ## Riesgos
    - ...

    ## Rollback
    ...

    ## Decisiones humanas
    ...

    ## Limitaciones o pendientes
    ...

### 5. Abre el Pull Request

Crea una rama y abre un Pull Request contra main.

**No hagas merge.**

Lee el diff completo como reviewer y comprueba:
- cambios no relacionados;
- validaciones faltantes;
- tests débiles;
- comportamiento inesperado;
- documentación que afirme algo no demostrado.

Completa x-review.md solo en el siguiente paso.

### 6. Criterios de salida

- [ ] El bug fue reproducido antes de corregirlo.
- [ ] Existe una prueba de regresión.
- [ ] Existe docs/debugging-notes.md.
- [ ] La suite completa pasa.
- [ ] Existe docs/pr-description.md.
- [ ] Existe un Pull Request abierto contra main.
- [ ] Revisaste el diff del PR.

Haz commit y push.

**Tiempo sugerido: 18-22 min.**
