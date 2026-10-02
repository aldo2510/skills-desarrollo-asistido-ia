# Step 3 — Implementa con IA y compara alternativas

## Objetivo
Usar Copilot Agent para implementar, pero conservar el control humano mediante diff, pruebas y una decisión documentada.

## 1. Prompt exacto para Copilot Agent
~~~text
Implementa el requerimiento descrito en docs/implementation-plan.md.

Agrega priority a Task y TaskCreate.
Solo permite low, medium y high.
Haz priority obligatoria al crear.
POST /tasks debe conservarla.
GET /tasks debe devolverla.
Las tareas iniciales deben tener un valor válido.
Agrega pruebas para valores válidos, inválidos, ausencia del campo y persistencia en POST.
Mantén las funcionalidades existentes.
Antes de modificar archivos revisa app/main.py, tests/test_api.py y docs/implementation-plan.md.
Después ejecuta pytest -q y muestra los archivos modificados.
No agregues dependencias nuevas.
~~~

## 2. Verifica el cambio
~~~bash
git diff
pytest -q
~~~

## 3. Crea tests/test_priority.py

Copia exactamente:

~~~python
from fastapi.testclient import TestClient
from app.main import app

client = TestClient(app)

def test_priority_is_returned_by_get_tasks():
    response = client.get("/tasks")
    assert response.status_code == 200
    assert all(task["priority"] in {"low", "medium", "high"} for task in response.json())

def test_create_task_with_priority():
    response = client.post("/tasks", json={"title": "Priority test", "priority": "high"})
    assert response.status_code == 201
    assert response.json()["priority"] == "high"

def test_create_task_rejects_invalid_priority():
    response = client.post("/tasks", json={"title": "Invalid", "priority": "urgent"})
    assert response.status_code == 422

def test_create_task_requires_priority():
    response = client.post("/tasks", json={"title": "Missing priority"})
    assert response.status_code == 422
~~~

## 4. Crea docs/implementation-review.md

Copia exactamente:

~~~markdown
# Implementation Review

## Implementación elegida
La solución incorpora priority al contrato de entrada y al modelo de salida, conserva el valor en POST /tasks y lo devuelve mediante GET /tasks.

## Alternativa considerada
Validar manualmente priority dentro de POST /tasks.

## Comparación
| Criterio | Modelo | Endpoint |
|---|---|---|
| Claridad | Regla centralizada | Regla mezclada con lógica |
| Mantenibilidad | Menor duplicación | Mayor riesgo de duplicación |
| Validación | Automática | Manual |
| Reutilización | Alta | Menor |
| Acoplamiento | Menor | Mayor |

## Decisión humana
Se mantiene la validación en el modelo porque priority forma parte del contrato de entrada.

## Evidencia
- Se revisó el diff.
- Se ejecutó pytest -q.
- Se revisaron tests/test_priority.py.
- Se verificaron los endpoints afectados.

## Control humano
La implementación de Copilot no se acepta automáticamente. El participante revisa el diff y decide si el cambio cumple el alcance.
~~~

## 5. Verificación
~~~bash
test -f tests/test_priority.py
test -f docs/implementation-review.md
pytest -q
~~~

## 6. Commit
~~~bash
git add app tests docs
git commit -m "feat: add task priority"
git push
~~