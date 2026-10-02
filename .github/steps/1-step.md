## Step 1: Conoce el código con Copilot

> **Idea clave:** antes de pedirle a una IA que cambie código, necesitas construir tu propio modelo mental del sistema. Copilot puede acelerar la exploración, pero no sustituye la lectura del código ni la verificación de sus respuestas.

### ¿Qué vas a practicar?

En este paso aprenderás a usar IA para **comprender**, no para implementar.

El objetivo no es obtener una respuesta bonita de Copilot. El objetivo es comprobar si la IA puede ayudarte a responder preguntas concretas sobre un repositorio que realmente has inspeccionado.

### 1. Línea base

Abre el repositorio en Codespaces:

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{full_repo_name}}?quickstart=1)

Ejecuta:

```bash
pip install -r requirements.txt
pytest -q
```

**¿Por qué empezar por aquí?**

Porque una modificación asistida por IA necesita una referencia. Si las pruebas no pasan antes del cambio, después no podrás distinguir entre un problema preexistente y uno introducido por tu trabajo.

Anota mentalmente:
- cuántas pruebas existen;
- cuánto tarda aproximadamente la suite;
- qué comportamiento está cubierto.

### 2. Exploración asistida

Usa Copilot Chat en modo Agent con prompts como:

> Analiza este proyecto como un developer senior. Explica la arquitectura, los archivos principales, los endpoints, el modelo de datos y cómo se ejecutan las pruebas. No cambies ningún archivo.

Después pregunta:

> Sigue el flujo de una petición POST /tasks desde la entrada HTTP hasta la respuesta. Indica qué modelos y funciones participan y qué supuestos haces.

Y finalmente:

> ¿Qué riesgos técnicos ves si agregamos un nuevo atributo obligatorio al recurso Task? Considera compatibilidad, validación, pruebas y clientes existentes.

### 3. Verificación humana

Ahora compara las respuestas de Copilot con el código real.

Busca específicamente:
- una afirmación correcta;
- una afirmación incompleta;
- una afirmación que necesite matices;
- una parte del código que Copilot no haya mencionado.

> **Regla del laboratorio:** una explicación de IA no se considera evidencia hasta que puedas señalar dónde se demuestra en el código.

### 4. Documentación

Crea `docs/project-analysis.md` con:

- arquitectura y responsabilidad de cada archivo;
- endpoints existentes;
- modelos `Task` y `TaskCreate`;
- estrategia actual de persistencia;
- cómo ejecutar las pruebas;
- al menos **2 riesgos o decisiones técnicas** detectadas con ayuda de IA;
- una sección **"Lo que Copilot dijo vs. lo que verifiqué"** con al menos 3 observaciones;
- qué información de Copilot verificaste manualmente;
- una pregunta técnica que todavía quede abierta.

### 5. Mini reflexión

Antes de hacer commit, responde en el documento:

1. ¿Qué parte de la exploración fue más rápida con IA?
2. ¿Qué parte fue más fácil entender leyendo directamente el código?
3. ¿Qué error podría haber ocurrido si hubieras confiado ciegamente en Copilot?

Haz commit y push.

**Tiempo sugerido: 15-18 min.**
