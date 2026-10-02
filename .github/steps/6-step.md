# Step 6 — Haz code review asistido por IA

## Objetivo
Usar IA para buscar defectos en el PR sin convertir la respuesta de IA en una aprobación automática.

## 1. Prompt exacto
~~~text
Actúa como reviewer senior del Pull Request actual.
Revisa el diff contra main.
No modifiques archivos.
Busca errores funcionales, regresiones, validaciones incompletas, pruebas faltantes, cambios fuera de alcance, mantenibilidad y compatibilidad.
Para cada hallazgo indica archivo, problema, evidencia y severidad.
Si no encuentras problemas, explica qué verificaste.
~~~

## 2. Crea docs/code-review.md

~~~markdown
# Code Review

## Alcance
Se revisó el diff del Pull Request contra main.

## Checklist
- [x] Requerimiento de priority revisado.
- [x] Validación de entrada revisada.
- [x] POST /tasks revisado.
- [x] GET /tasks revisado.
- [x] Pruebas revisadas.
- [x] Caso de colección vacía revisado.
- [x] Cambios fuera de alcance revisados.
- [x] Suite completa ejecutada.

## Hallazgos
Los hallazgos de Copilot deben contrastarse con el código real antes de aceptarse.

## Evidencia
~~~bash
git diff main...HEAD
pytest -q
~~~

## Decisión
Un hallazgo solo se considera válido cuando existe evidencia reproducible.
~~~

## 3. Verificación y commit
~~~bash
test -f docs/code-review.md
pytest -q
git add docs/code-review.md
git commit -m "docs: record ai code review"
git push
~~