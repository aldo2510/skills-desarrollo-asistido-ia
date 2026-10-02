# Step 5 — Prepara el Pull Request

## Objetivo
Convertir el trabajo técnico en un cambio revisable y trazable.

## 1. Prompt exacto
~~~text
Revisa git diff y el requerimiento original.
Genera una descripción de Pull Request en español con objetivo, cambios, pruebas, riesgos, validación y rollback.
No modifiques archivos.
~~~

## 2. Crea docs/pr-description.md

~~~markdown
# Pull Request

## Objetivo
Agregar priority a las tareas y corregir la generación del primer ID sin romper la API existente.

## Cambios
- Se incorporó priority al modelo de tarea.
- Se incorporó priority al modelo de creación.
- Se actualizaron los endpoints necesarios.
- Se agregaron pruebas de prioridad.
- Se agregó una prueba para colección vacía.
- Se corrigió la generación del primer ID.
- Se documentaron decisiones y pruebas.

## Pruebas
~~~bash
pytest -q
~~~

## Riesgos
- Clientes antiguos que no envíen priority.
- Cambio del contrato de entrada.
- Estado en memoria durante la ejecución.

## Validación
Revisar git diff y ejecutar toda la suite.

## Rollback
Revertir el commit del cambio y ejecutar pytest nuevamente.
~~~

## 3. Crea la rama
~~~bash
git checkout -b feat/task-priority
git status
~~~

Si ya tienes los cambios en main, no los pierdas: conserva los cambios, crea la rama y verifica que el PR se origine desde ella.

## 4. Commit y push
~~~bash
git add .
git commit -m "feat: task priority and validation"
git push -u origin feat/task-priority
~~~

## 5. Abre el PR
Crea un Pull Request hacia main usando docs/pr-description.md como descripción. No hagas merge.

## 6. Verificación
~~~bash
test -f docs/pr-description.md
test -f docs/debugging-notes.md
test -f tests/test_empty_tasks.py
pytest -q
~~