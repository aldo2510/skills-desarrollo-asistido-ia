## Step 5: Depura con IA

Ahora trabaja como si hubieras recibido un incidente.

### Bug deliberado

La función de creación de tareas contiene una debilidad: si la colección está vacía, calcular el siguiente ID puede producir un error.

Reproduce el problema de forma controlada.

Pide a Copilot:

> Analiza create_task. ¿Qué ocurre si la colección de tareas está vacía? Propón una prueba de regresión antes de corregir el código.

### Objetivo

1. crea una prueba que reproduzca el fallo;
2. ejecuta la prueba y captura la evidencia;
3. pide a Copilot que explique la causa raíz;
4. corrige el código;
5. vuelve a ejecutar todas las pruebas;
6. confirma que la prueba de regresión queda permanentemente en el proyecto.

Documenta en `docs/debugging-notes.md`:

- síntoma;
- reproducción;
- causa raíz;
- hipótesis descartadas;
- cambio realizado;
- evidencia de pruebas.

**No aceptes la primera solución de Copilot sin revisar el diff.**

Haz commit y push.

**Tiempo sugerido: 12-15 min.**
