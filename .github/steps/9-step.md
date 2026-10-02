# Step 9 — Ejecuta la validación final

## Objetivo
Reunir evidencia antes de cerrar el cambio.

## 1. Prompt exacto
~~~text
Actúa como reviewer final.
No modifiques archivos.
Revisa el requerimiento original, el diff, las pruebas y la documentación.
Indica:
- requisitos cubiertos;
- pruebas ejecutadas;
- riesgos pendientes;
- cambios fuera de alcance;
- evidencia faltante.
No escribas código.
~~~

## 2. Crea docs/final-validation.md

~~~markdown
# Final Validation

## Requisitos
| Requisito | Evidencia | Resultado |
|---|---|---|
| priority acepta low | tests/test_priority.py | Cumple |
| priority acepta medium | tests/test_priority.py | Cumple |
| priority acepta high | tests/test_priority.py | Cumple |
| priority es obligatoria | tests/test_priority.py | Cumple |
| priority inválida es rechazada | tests/test_priority.py | Cumple |
| GET devuelve priority | tests/test_priority.py | Cumple |
| colección vacía funciona | tests/test_empty_tasks.py | Cumple |
| regresión | pytest -q | Cumple |

## Validación ejecutada
~~~bash
pytest -q
git diff main...HEAD
~~~

## Riesgos pendientes
La aplicación continúa usando almacenamiento en memoria; no se introdujo una base de datos porque está fuera del alcance.

## Decisión
El cambio puede pasar a revisión final si todos los comandos anteriores terminan correctamente.
~~~

## 3. Verificación
~~~bash
test -f docs/final-validation.md
pytest -q
git diff --check
~~~

## 4. Commit
~~~bash
git add docs/final-validation.md
git commit -m "docs: record final validation"
git push
~~