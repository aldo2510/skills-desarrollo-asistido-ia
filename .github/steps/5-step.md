## Step 5: Revisión final

### 1. Ejecuta la validación completa

```bash
pytest -q
test -f docs/project-analysis.md
test -f docs/implementation-plan.md
test -f docs/implementation-review.md
test -f docs/test-strategy.md
test -f docs/debugging-notes.md
test -f docs/pr-description.md
test -f x-review.md
```

### 2. Revisión final con Copilot

Copia y pega:

```text
Revisa el cambio completo del ejercicio contra el requerimiento original.

No modifiques archivos.

Comprueba:
- priority low/medium/high;
- priority obligatoria;
- GET /tasks;
- pruebas;
- corrección del bug de tasks vacía;
- documentación;
- coherencia entre código, tests y PR.

Devuelve:
1. requisitos cumplidos;
2. requisitos no cumplidos;
3. riesgos;
4. inconsistencias;
5. recomendaciones.

No inventes evidencia.
```

### 3. Revisión humana

Abre el Pull Request y revisa el diff.

Si encuentras un problema, corrígelo y vuelve a ejecutar `pytest -q`.

### 4. Crea x-review.md

**Copia esta estructura:**

```markdown
# Revisión humana final

## 1. Sugerencia de IA que acepté
- ...

## 2. Sugerencia de IA que modifiqué o rechacé
- ...
- Motivo: ...

## 3. Defecto que detecté
- ...

## 4. Validación que no delegaría completamente a la IA
- ...

## 5. Evidencia revisada
- ...

## 6. ¿Dónde aportó más valor la IA?
...

## 7. ¿Dónde fue necesario criterio humano?
...

## 8. ¿Qué habría ocurrido si aceptaba todos los cambios sin revisar?
...

## 9. ¿Qué volvería a delegar?
...

## 10. ¿Qué mantendría bajo control humano?
...
```

Haz commit y push.

### Resultado esperado

El ejercicio demuestra:

**analizar → planificar → implementar → probar → depurar → PR → revisión humana**

**Tiempo: 10-12 min.**
