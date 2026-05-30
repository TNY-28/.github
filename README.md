# .github

Templates globales y metodo de trabajo para todos mis repos.

## Contenido

### Templates

- **Issue Templates** — Bug reports y feature requests (`ISSUE_TEMPLATE/`)
- **PR Template** — Checklist para pull requests (`PULL_REQUEST_TEMPLATE/`)

### Workflow Templates

Workflows de CI listos para copiar a cualquier proyecto:

- **ci-react.yml** — CI para proyectos React/Vite (install, build)
- **ci-django.yml** — CI para proyectos Django/Python (install, check, test)

#### Como usar

Copiar el workflow al proyecto destino:

```bash
# Desde la raiz del proyecto
mkdir -p .github/workflows
cp ruta/al/template .github/workflows/ci.yml
```

Ajustar segun el proyecto (variables de entorno, version de Node/Python, etc).

### Git Method

**GIT_METHOD.md** — Mi metodo personal de Git. Reglas fijas, reglas adaptables, flujo diario.

## Notas

- Estos templates son un punto de partida, no reglas rigidas
- Cada proyecto puede ajustar lo que necesite en su propio repo
- Commits siguen Conventional Commits (ver GIT_METHOD.md)
