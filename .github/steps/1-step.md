## Step 1: Conoce el código con Copilot

Abre el repositorio en Codespaces:

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{full_repo_name}}?quickstart=1)

### 1. Línea base

Ejecuta:

```bash
pip install -r requirements.txt
pytest -q
```

Confirma que la línea base pasa antes de modificar el producto.

### 2. Exploración asistida

Usa Copilot Chat en modo Agent con prompts como:

> Analiza este proyecto como un developer senior. Explica la arquitectura, los archivos principales, los endpoints, el modelo de datos y cómo se ejecutan las pruebas. No cambies ningún archivo.

> ¿Qué riesgos técnicos ves si agregamos un nuevo atributo obligatorio al recurso Task?

No aceptes cambios todavía. Compara las respuestas de Copilot con el código real.

### 3. Documentación

Crea `docs/project-analysis.md` con:

- arquitectura y responsabilidad de cada archivo;
- endpoints existentes;
- modelos `Task` y `TaskCreate`;
- estrategia actual de persistencia;
- cómo ejecutar las pruebas;
- al menos **2 riesgos o decisiones técnicas** detectadas con ayuda de IA;
- qué información de Copilot verificaste manualmente.

Haz commit y push.

**Tiempo sugerido: 12-15 min.**
