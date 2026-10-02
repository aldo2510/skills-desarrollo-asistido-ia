# Step 4 — Diseña pruebas y depura con evidencia

## Objetivo
Distinguir entre una hipótesis generada por IA y un problema realmente reproducible.

## 1. Prompt para diseñar pruebas
~~~text
Revisa la implementación actual de priority.
No modifiques archivos.
Identifica casos normales, inválidos, ausentes y límites.
Para cada caso indica entrada, endpoint, resultado HTTP esperado y riesgo de regresión.
~~~

## 2. Crea docs/test-strategy.md

~~~markdown
# Test Strategy

## Objetivo
Validar el contrato de priority y preservar el comportamiento existente.

## Matriz
| Caso | Entrada | Esperado |
|---|---|---|
| low | priority=low | 201 |
| medium | priority=medium | 201 |
| high | priority=high | 201 |
| inválida | priority=urgent | 422 |
| ausente | sin priority | 422 |
| listado | GET /tasks | priority presente |
| regresión | suite existente | todo pasa |
| colección vacía | POST /tasks sin tareas | creación correcta |

## Ejecución
~~~bash
pytest -q
~~~

## Criterio de salida
No continuar mientras exista una prueba fallida.
~~~

## 3. Analiza el caso de colección vacía
~~~text
Analiza app/main.py.
No modifiques archivos.
Determina si la generación del ID funciona cuando tasks está vacía.
Explica si existe una excepción posible, cómo reproducirla y cuál es la causa exacta.
No escribas código.
~~~

## 4. Crea tests/test_empty_tasks.py

~~~python
from fastapi.testclient import TestClient
from app.main import app, tasks

client = TestClient(app)

def test_create_task_when_collection_is_empty():
    original_tasks = list(tasks)
    tasks.clear()
    try:
        response = client.post(
            "/tasks",
            json={"title": "First task", "priority": "medium"},
        )
        assert response.status_code == 201
        assert response.json()["id"] == 1
    finally:
        tasks.extend(original_tasks)
~~~

## 5. Corrige con Copilot
~~~text
Ahora implementa la corrección mínima para que crear una tarea funcione cuando tasks está vacía.
No cambies otros comportamientos.
Mantén la prueba que reproduce el problema.
Ejecuta pytest -q y explica causa, corrección y evidencia.
~~~

## 6. Crea docs/debugging-notes.md

~~~markdown
# Debugging Notes

## Problema
Generación del primer ID cuando no existen tareas.

## Síntoma
La creación puede fallar si se calcula el máximo de una colección vacía.

## Causa
La lógica de generación del ID debe contemplar explícitamente el caso sin elementos.

## Reproducción
tests/test_empty_tasks.py vacía temporalmente la colección y ejecuta POST /tasks.

## Corrección
Se aplicó únicamente el cambio necesario para soportar la colección vacía.

## Evidencia
~~~bash
pytest -q
~~~

## Decisión
No se modificaron otros comportamientos de la API.
~~~

## 7. Verificación
~~~bash
test -f docs/debugging-notes.md
test -f tests/test_empty_tasks.py
pytest -q
~~~

## 8. Commit
~~~bash
git add app tests docs
git commit -m "test: cover empty task collection"
git push
~~