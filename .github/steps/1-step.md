# Step 1 — Analiza el proyecto

## Objetivo
Comprender el sistema antes de modificarlo. Copilot es apoyo; la evidencia definitiva está en el repositorio.

## Prompt opcional para Copilot
~~~text
Analiza este proyecto FastAPI como un ingeniero senior.
No modifiques ningún archivo ni escribas código.
Explica arquitectura, endpoints, modelos, persistencia, pruebas, flujo de POST /tasks, flujo de PATCH /tasks/{task_id} y dos riesgos técnicos.
Termina con 3 afirmaciones que yo deba verificar directamente en el repositorio.
~~~

## 1. Crea docs/project-analysis.md

Copia y pega exactamente:

~~~markdown
# Project Analysis

## 1. Arquitectura
| Archivo | Responsabilidad |
|---|---|
| app/main.py | Aplicación FastAPI, modelos, estado y endpoints |
| tests/test_api.py | Pruebas de la API |
| requirements.txt | Dependencias Python |

## 2. Endpoints
| Método | Endpoint | Entrada | Respuesta |
|---|---|---|---|
| GET | /health | Ninguna | Estado |
| GET | /tasks | Ninguna | Lista de tareas |
| POST | /tasks | TaskCreate | Nueva tarea |
| PATCH | /tasks/{task_id} | ID | Tarea actualizada |

## 3. Modelos
### Task
- id
- title
- completed

### TaskCreate
- title

## 4. Persistencia actual
Las tareas se almacenan en memoria mediante la lista global tasks. No existe una base de datos y los datos se pierden al reiniciar el proceso.

## 5. Ejecución de pruebas
El proyecto utiliza pytest y FastAPI TestClient. La suite se ejecuta con pytest -q.

## 6. Flujo de POST /tasks
1. Recibe TaskCreate.
2. Valida la entrada.
3. Calcula el nuevo ID.
4. Crea Task.
5. Agrega la tarea a tasks.
6. Devuelve la tarea.

## 7. Flujo de PATCH /tasks/{task_id}
1. Recibe el ID.
2. Busca la tarea.
3. Marca completed como true.
4. Devuelve la tarea.
5. Si no existe, devuelve 404.

## 8. Riesgos técnicos
1. La información se pierde al reiniciar.
2. El ID depende del estado actual de la colección.
3. La lista global representa estado compartido durante la ejecución.
4. Las pruebas dependen del estado inicial del módulo.

## 9. Lo que verifiqué
| Afirmación | Verificación | Resultado |
|---|---|---|
| La aplicación utiliza FastAPI | Revisé app/main.py | Confirmado |
| Las tareas están en memoria | Revisé la variable tasks | Confirmado |
| Existen cuatro endpoints | Revisé las rutas | Confirmado |

## 10. Conclusión
La aplicación es una API FastAPI pequeña, con almacenamiento en memoria y pruebas automatizadas. La IA se utiliza como apoyo y el código real del repositorio es la fuente de verificación.
~~~

## 2. Verificación
~~~bash
test -f docs/project-analysis.md
pytest -q
~~~

## 3. Commit
~~~bash
git add docs/project-analysis.md
git commit -m "docs: analyze project"
git push
~~