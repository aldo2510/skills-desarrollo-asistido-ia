# Step 8 — Documenta el aprendizaje técnico

## Objetivo
Explicar qué aportó la IA y qué responsabilidades permanecieron en manos de la persona desarrolladora.

## 1. Prompt exacto
~~~text
Analiza todo el ejercicio.
No modifiques archivos.
Resume:
1. dónde ayudó la IA;
2. dónde fue necesario verificar manualmente;
3. qué cambio requirió pruebas;
4. qué riesgo habría existido aceptando la salida de IA sin revisar;
5. qué decisión permaneció humana.
No escribas código.
~~~

## 2. Crea docs/ai-learning.md

~~~markdown
# AI Learning

## Dónde ayudó la IA
- Análisis inicial del repositorio.
- Propuesta de plan.
- Implementación del cambio.
- Diseño de pruebas.
- Revisión del diff.
- Identificación de posibles riesgos.

## Qué verifiqué manualmente
- Archivos realmente modificados.
- Contrato de los endpoints.
- Resultados de pytest.
- Caso de colección vacía.
- Compatibilidad con las pruebas existentes.

## Riesgo de aceptar IA sin revisión
Una respuesta puede ser técnicamente plausible y no corresponder al código real. Por eso la evidencia del repositorio y las pruebas tienen prioridad.

## Decisión humana
La persona participante decide qué propuesta de IA aceptar, modificar o rechazar.

## Evidencia
~~~bash
git diff main...HEAD
pytest -q
~~~
~~~

## 3. Verificación y commit
~~~bash
test -f docs/ai-learning.md
grep -Eiq 'IA|verifi|humana' docs/ai-learning.md
git add docs/ai-learning.md
git commit -m "docs: record ai learning"
git push
~~