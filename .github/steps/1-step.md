## Step 1: Conoce el código con Copilot

Abre el repositorio en Codespaces:

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{full_repo_name}}?quickstart=1)

Ejecuta:

```bash
pip install -r requirements.txt
pytest -q
```

Usa Copilot Chat en modo Agent con un prompt similar a:

> Analiza este proyecto como un developer senior. Explica la arquitectura, los archivos principales, los endpoints y cómo ejecutar las pruebas. No cambies ningún archivo.

Crea `docs/project-analysis.md` con:
- mención de FastAPI;
- endpoints principales;
- cómo ejecutar las pruebas;
- explicación breve de `app/main.py`.

Haz commit y push. GitHub validará el resultado.
