## Step 4: Depura y prepara el Pull Request

### Teoría: debugging asistido por IA

Debugging no significa pedirle a la IA que "arregle el error" inmediatamente.

Un proceso reproducible es:

```
Síntoma → reproducción → evidencia → causa raíz → alternativas → corrección → regresión
```

La prueba de regresión es especialmente importante: evita que un bug corregido vuelva a aparecer.

En este ejercicio existe deliberadamente un bug en el cálculo del ID cuando la colección de tareas está vacía.

### 1. Reproduce el bug

Copia y pega:

```text
Analiza create_task en app/main.py.

No corrijas el código todavía.

Explícame exactamente qué ocurre si tasks está vacía.
Genera una prueba de regresión que reproduzca el problema, pero no la implementes todavía.
Explica la causa probable.
```

### 2. Crea la prueba de regresión

Copia y pega:

```text
Implementa una prueba de regresión para el caso en que tasks esté vacía y create_task deba generar correctamente el siguiente ID.

No corrijas todavía la implementación.
Ejecuta únicamente esa prueba y muestra el fallo.
```

### 3. Investiga la causa raíz

Copia y pega:

```text
Analiza el fallo de la prueba de regresión.

No modifiques el código.

Explica:
1. síntoma;
2. reproducción;
3. causa raíz;
4. dos alternativas de corrección;
5. ventajas y riesgos de cada alternativa.

Después indica qué evidencia respalda la causa raíz.
```

### 4. Corrige

Copia y pega:

```text
Corrige únicamente el bug de create_task identificado en la prueba de regresión.

Conserva el comportamiento existente.
Ejecuta primero la prueba de regresión y después pytest -q.

Muestra el diff y explica la corrección.
```

### 5. Documenta

Crea `docs/debugging-notes.md`:

```markdown
# Debugging Notes

## Síntoma
...

## Reproducción
...

## Causa raíz
...

## Hipótesis descartadas
- ...

## Alternativas consideradas
### Alternativa 1
...
### Alternativa 2
...

## Corrección elegida
...

## Evidencia
- Prueba de regresión:
- Suite completa:

## Verificación humana
...
```

### 6. Prepara el PR

Copia y pega:

```text
Genera una descripción de Pull Request usando únicamente evidencia del repositorio.

Incluye:
- problema;
- solución;
- archivos modificados;
- pruebas ejecutadas;
- riesgos;
- rollback;
- decisiones humanas;
- limitaciones.

No inventes resultados.
```

Crea `docs/pr-description.md` con:

```markdown
# Pull Request

## Problema
...

## Solución
...

## Archivos modificados
- ...

## Pruebas ejecutadas
- ...

## Riesgos
- ...

## Rollback
...

## Decisiones humanas
...

## Limitaciones
...
```

Crea una rama, haz commit y push, y abre un Pull Request contra `main`.

**No hagas merge.**

### 7. Revisión del PR

Copia y pega:

```text
Revisa el Pull Request actual como un reviewer senior.

Busca:
- cambios no relacionados;
- tests débiles;
- validaciones faltantes;
- comportamiento inesperado;
- documentación que no tenga evidencia.

No modifiques archivos. Devuelve los hallazgos ordenados por prioridad.
```

Corrige cualquier hallazgo y ejecuta:

```bash
pytest -q
```

**Tiempo: 18-20 min.**
