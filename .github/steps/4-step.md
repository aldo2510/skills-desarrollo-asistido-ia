## Step 4: Genera pruebas con IA

Pide a Copilot que cree `tests/test_priority.py`.

Debe cubrir como mínimo:

- prioridad `low`;
- prioridad `medium`;
- prioridad `high`;
- prioridad inválida;
- ausencia de prioridad;
- prioridad visible en GET /tasks;
- creación de una tarea con prioridad.

Después pide a Copilot:

> Revisa estas pruebas como QA senior. Busca casos que puedan dar falsos positivos o que no comprueben realmente el requerimiento.

Corrige las pruebas si es necesario.

Ejecuta:

```bash
pytest -q
```

Guarda en `docs/test-strategy.md`:

- qué escenarios cubriste;
- qué escenarios no cubriste;
- qué recomendó Copilot;
- qué verificaste manualmente.

Haz commit y push.

**Tiempo sugerido: 10-12 min.**
