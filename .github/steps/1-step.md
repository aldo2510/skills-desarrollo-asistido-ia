## Step 1: Conoce el código con Copilot

> **Idea clave:** antes de pedirle a una IA que cambie código, necesitas construir tu propio modelo mental del sistema. Copilot puede acelerar la exploración, pero no sustituye la lectura del código ni la verificación de sus respuestas.

### ¿Qué vas a practicar?

En este paso aprenderás a usar IA para **comprender un proyecto existente**. No vas a implementar funcionalidades todavía.

Vas a practicar este ciclo:

```text
Preguntar a Copilot
      ↓
Observar su explicación
      ↓
Comprobarla contra el código
      ↓
Detectar diferencias
      ↓
Documentar lo aprendido
```

### 1. Abre el entorno

Abre el repositorio en Codespaces:

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{full_repo_name}}?quickstart=1)

Ejecuta:

```bash
pip install -r requirements.txt
pytest -q
```

**Antes de continuar**, confirma que las pruebas pasan.

Anota:
- cuántas pruebas pasan;
- qué endpoints ya están cubiertos;
- qué comportamiento parece no estar cubierto.

### 2. Explora el proyecto con Copilot

Usa Copilot Chat en modo Agent con los siguientes prompts.

#### Prompt 1 — Arquitectura

> Analiza este proyecto como un developer senior. Explica la arquitectura, los archivos principales, la responsabilidad de cada archivo, los endpoints disponibles, los modelos de datos y cómo se ejecutan las pruebas. No cambies ningún archivo.

#### Prompt 2 — Flujo de una petición

> Sigue paso a paso qué ocurre cuando un cliente realiza POST /tasks. Identifica el modelo de entrada, la función que procesa la petición, cómo se genera el ID, cómo se almacena la tarea y qué respuesta recibe el cliente. No cambies ningún archivo.

#### Prompt 3 — Persistencia

> Analiza cómo se almacenan actualmente las tareas. ¿Existe una base de datos? ¿Qué ocurre cuando la aplicación se reinicia? ¿Qué ventajas y limitaciones tiene esta estrategia para un entorno real?

#### Prompt 4 — Riesgos

> ¿Qué riesgos técnicos ves si agregamos un nuevo atributo obligatorio al recurso Task? Considera compatibilidad, validación, pruebas y clientes existentes.

### 3. Verifica las respuestas de Copilot

Ahora **no copies directamente las respuestas de Copilot**.

Abre `app/main.py` y comprueba cada afirmación importante.

Busca deliberadamente:

- una afirmación de Copilot que sea correcta;
- una explicación que sea incompleta;
- una afirmación que necesite un matiz;
- algún detalle que Copilot no haya mencionado.

> **Regla del laboratorio:** una explicación de IA no se considera evidencia hasta que puedas señalar dónde se demuestra en el código.

### 4. Documenta el análisis

Ahora sí debes crear el archivo:

```text
docs/project-analysis.md
```

**El archivo NO existe inicialmente. Tú debes crearlo.**

No necesitas inventar información. Debes completar el documento a partir de lo que encontraste en el código y de las conversaciones con Copilot.

#### Usa esta estructura obligatoria

Copia esta plantilla y completa cada sección:

```markdown
# Análisis del proyecto

## 1. Resumen del proyecto

Explica en 3-5 líneas qué hace la aplicación y cuál es su propósito.

## 2. Arquitectura y archivos principales

Describe qué responsabilidad tiene cada archivo relevante.

Ejemplo de tabla:

| Archivo | Responsabilidad |
|---|---|
| app/main.py | ... |
| requirements.txt | ... |
| tests/... | ... |

## 3. Endpoints existentes

Documenta cada endpoint actual.

| Método | Endpoint | Propósito | Respuesta |
|---|---|---|---|
| GET | /health | ... | ... |
| GET | /tasks | ... | ... |
| POST | /tasks | ... | ... |
| PATCH | /tasks/{task_id} | ... | ... |

## 4. Modelos de datos

Explica:

### Task

- campos;
- tipos;
- valores por defecto;
- propósito.

### TaskCreate

- campos;
- tipos;
- validaciones;
- propósito.

## 5. Persistencia actual

Explica:

- dónde se almacenan las tareas;
- durante cuánto tiempo permanecen;
- qué ocurre al reiniciar la aplicación;
- ventajas;
- limitaciones.

## 6. Estrategia actual de pruebas

Explica:

- qué framework se utiliza;
- cómo se ejecutan las pruebas;
- qué endpoints están cubiertos;
- qué escenarios importantes están cubiertos;
- qué escenarios parecen faltar.

## 7. Riesgos o decisiones técnicas detectadas con ayuda de IA

Documenta **al menos 2**.

Para cada uno:

### Riesgo/decisión 1

- Qué identificó Copilot:
- Evidencia encontrada en el código:
- Por qué importa:
- Mi conclusión:

### Riesgo/decisión 2

- Qué identificó Copilot:
- Evidencia encontrada en el código:
- Por qué importa:
- Mi conclusión:

## 8. Lo que Copilot dijo vs. lo que verifiqué

Incluye **al menos 3 observaciones**.

| # | Copilot dijo | Lo que verifiqué en el código | Resultado |
|---|---|---|---|
| 1 | ... | ... | Correcto / Incompleto / Incorrecto |
| 2 | ... | ... | Correcto / Incompleto / Incorrecto |
| 3 | ... | ... | Correcto / Incompleto / Incorrecto |

## 9. Información de Copilot que verifiqué manualmente

Explica qué partes de las respuestas decidiste comprobar directamente en el código y cómo las comprobaste.

## 10. Pregunta técnica abierta

Escribe al menos una pregunta que haya quedado sin resolver y que investigarías antes de evolucionar el proyecto.

## 11. Reflexión

Responde:

1. ¿Qué parte de la exploración fue más rápida con IA?
2. ¿Qué parte fue más fácil entender leyendo directamente el código?
3. ¿Qué error podría haber ocurrido si hubieras confiado ciegamente en Copilot?
```

**Importante:** las respuestas deben estar basadas en este repositorio. No copies respuestas genéricas de Internet ni inventes componentes que no existen.

### 5. Revisión final antes del commit

Antes de hacer commit, comprueba:

- [ ] `docs/project-analysis.md` existe.
- [ ] Describe los archivos reales del proyecto.
- [ ] Documenta los 4 endpoints actuales.
- [ ] Explica `Task` y `TaskCreate`.
- [ ] Explica cómo funciona la persistencia.
- [ ] Explica cómo se ejecutan las pruebas.
- [ ] Incluye al menos 2 riesgos o decisiones técnicas.
- [ ] Incluye 3 comparaciones entre Copilot y el código real.
- [ ] Incluye una pregunta técnica abierta.
- [ ] Incluye la reflexión final.

Haz commit y push.

**Tiempo sugerido: 15-17 min.**
