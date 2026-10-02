# Step 4 — Diseña la estrategia de pruebas

## Objetivo

Definir y ejecutar pruebas que demuestren que `priority` forma parte del contrato de la API y que las funcionalidades existentes continúan funcionando.

La documentación de este Step ya está preparada. No necesitas pedirle a Copilot que genere el Markdown.

## 1. Revisión opcional con Copilot

Puedes usar Copilot para revisar la estrategia, pero no es obligatorio para completar el Step.

Copia y pega este prompt:

~~~text
Revisa la implementación actual de priority y la estrategia de pruebas descrita en docs/test-strategy.md.

No modifiques ningún archivo.

Indica:
1. Qué casos normales están cubiertos.
2. Qué casos inválidos están cubiertos.
3. Qué casos de regresión están cubiertos.
4. Si falta algún caso importante.
5. Si algún resultado HTTP documentado no coincide con el código actual.

No escribas código.
~~~

La respuesta de Copilot es una referencia. La fuente definitiva es el código y las pruebas del repositorio.

## 2. Crea docs/test-strategy.md

Crea exactamente este archivo:

`docs/test-strategy.md`

Copia y pega todo el contenido siguiente:

~~~markdown
# Test Strategy

## Objetivo

Comprobar que `priority` forma parte del contrato de la API sin romper las funcionalidades existentes.

## Casos de prueba

| Caso | Entrada | Resultado esperado |
|---|---|---|
| Prioridad baja | `priority=low` | 201 Created |
| Prioridad media | `priority=medium` | 201 Created |
| Prioridad alta | `priority=high` | 201 Created |
| Prioridad inválida | `priority=urgent` | 422 Unprocessable Entity |
| Prioridad ausente | Sin `priority` | 422 Unprocessable Entity |
| Listado de tareas | `GET /tasks` | Cada tarea contiene `priority` |
| Regresión | Suite existente | Todas las pruebas pasan |

## Validaciones

La estrategia debe comprobar:

- `priority` es obligatorio al crear una tarea.
- Solo se aceptan los valores `low`, `medium` y `high`.
- Una prioridad inválida es rechazada.
- Una petición sin prioridad es rechazada.
- `GET /tasks` devuelve la prioridad de cada tarea.
- Las funcionalidades existentes continúan funcionando.
- Las pruebas existentes no presentan regresiones.

## Ejecución

~~~bash
pytest -q
~~~

## Criterio de salida

No continuar mientras exista una prueba fallida.
~~~

## 3. Prueba el caso de colección vacía

Este caso sirve para practicar una idea importante de desarrollo asistido por IA: una implementación puede parecer correcta con datos normales y fallar con un caso límite.

Usa Copilot opcionalmente con este prompt:

~~~text
Analiza app/main.py.

No modifiques ningún archivo.

Determina si la generación del ID funciona cuando la lista tasks está vacía.

Explica:
1. Qué ocurre actualmente.
2. Si existe una excepción posible.
3. Cómo reproducirla.
4. Cuál es la causa exacta.

No escribas código.
~~~

## 4. Crea la prueba del caso límite

Crea:

`tests/test_empty_tasks.py`

Copia y pega:

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

## 5. Ejecuta la prueba

~~~bash
pytest -q
~~~

Si la prueba falla, **no continúes como si fuera un resultado esperado sin analizarlo**.

El objetivo es identificar:

- qué condición provoca el fallo;
- qué línea del código lo provoca;
- por qué el caso normal puede ocultar el problema.

## 6. Corrección asistida por Copilot

Ahora sí puedes utilizar Copilot para proponer la corrección.

Copia y pega:

~~~text
La prueba tests/test_empty_tasks.py reproduce un fallo al crear la primera tarea cuando tasks está vacía.

Analiza primero el fallo.

Después implementa la corrección mínima necesaria para que POST /tasks funcione cuando no existen tareas.

Restricciones:
- No cambies el contrato de los endpoints.
- No cambies el comportamiento de las tareas existentes.
- No elimines la prueba que reproduce el problema.
- No agregues funcionalidades no solicitadas.

Después ejecuta:

pytest -q

Explica:
1. Causa raíz.
2. Cambio realizado.
3. Prueba que demuestra la corrección.
~~~

Revisa el cambio propuesto antes de aceptarlo.

## 7. Crea docs/debugging-notes.md

Crea:

`docs/debugging-notes.md`

Copia y pega:

~~~markdown
# Debugging Notes

## Problema

Generación del primer ID cuando no existen tareas.

## Síntoma

La creación de una tarea puede fallar cuando la colección `tasks` está vacía.

## Causa

La lógica de generación del ID debe contemplar explícitamente el caso en el que no existen elementos.

## Reproducción

La prueba `tests/test_empty_tasks.py` vacía temporalmente la colección y ejecuta `POST /tasks`.

## Corrección

Se aplicó únicamente el cambio necesario para soportar la colección vacía.

## Evidencia

~~~bash
pytest -q
~~~

## Decisión

No se modificaron otros comportamientos de la API.
~~~

## 8. Verificación final

Ejecuta:

~~~bash
test -f docs/test-strategy.md
test -f docs/debugging-notes.md
test -f tests/test_empty_tasks.py
pytest -q
~~~

Todos los comandos deben finalizar correctamente.

## Criterio de salida

Puedes continuar al siguiente Step únicamente cuando:

- existe `docs/test-strategy.md`;
- existe `docs/debugging-notes.md`;
- existe `tests/test_empty_tasks.py`;
- `pytest -q` termina correctamente;
- revisaste manualmente el cambio realizado por Copilot;
- puedes explicar por qué el caso de colección vacía podía fallar.

## 9. Commit y push

Cuando todo esté correcto:

~~~bash
git add app tests docs
git commit -m "test: add priority strategy and empty collection coverage"
git push
~~~
