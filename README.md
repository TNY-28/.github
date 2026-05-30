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

**GIT_METHOD.md** — Metodo personal de Git y GitHub.

Estructura:
- Reglas FIJAS (commits, push, config, IA policy) — no cambian
- Reglas ADAPTABLES (ramas, CI, testing, versiones) — se deciden por proyecto
- Framework de decisiones — preguntas para definir que aplica a cada proyecto
- Decisiones por proyecto — registro de que se decidio y por que

## Filosofia

- Lo FIJO da confianza. Lo ADAPTABLE da flexibilidad
- Templates y workflows son punto de partida, no reglas rigidas
- Cada proyecto ajusta lo que necesite, documentando el por que
- Si una regla adaptable se repite en todos los proyectos, se promueve a fija
