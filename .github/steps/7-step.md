# Step 7 — Documenta decisiones técnicas

## Objetivo
Registrar por qué se eligió una solución y qué consecuencias tiene.

## 1. Prompt exacto
~~~text
Analiza los cambios realizados en este ejercicio.
No modifiques archivos.
Identifica las decisiones técnicas más importantes sobre priority, validación, pruebas, generación de ID y compatibilidad.
Para cada decisión indica problema, alternativas, decisión, evidencia y consecuencia.
~~~

## 2. Crea docs/technical-decisions.md

~~~markdown
# Technical Decisions

## Decisión 1 — Validación de priority
**Decisión:** Validar priority como parte del contrato de entrada.

**Motivo:** low, medium y high son valores permitidos por el requerimiento.

**Alternativa:** Validación manual dentro del endpoint.

**Consecuencia:** La regla queda centralizada y es más reutilizable.

## Decisión 2 — Cobertura de pruebas
**Decisión:** Cubrir valores válidos, inválidos, ausencia del campo y regresiones.

**Motivo:** El nuevo campo cambia el contrato.

**Consecuencia:** Se detectan cambios incompatibles con pruebas automatizadas.

## Decisión 3 — Generación de ID
**Decisión:** Manejar explícitamente una colección vacía.

**Motivo:** La primera creación debe funcionar sin tareas existentes.

**Consecuencia:** El caso límite queda protegido por una prueba.

## Decisión 4 — Control humano
**Decisión:** No aceptar automáticamente sugerencias de Copilot.

**Motivo:** La IA puede interpretar incorrectamente el código o el requerimiento.

**Consecuencia:** Cada cambio se contrasta con diff y pruebas.

## Evidencia
~~~bash
git diff
pytest -q
~~~
~~~

## 3. Revisión con Copilot
~~~text
Revisa docs/technical-decisions.md contra el código actual.
No modifiques archivos.
Indica cualquier decisión que no tenga evidencia suficiente o que describa un comportamiento inexistente.
~~~

## 4. Verificación
~~~bash
test -f docs/technical-decisions.md
pytest -q
~~~

## 5. Commit
~~~bash
git add docs/technical-decisions.md
git commit -m "docs: record technical decisions"
git push
~~