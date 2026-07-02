# Git Method - Anthony Arango

Mi metodo personal para trabajar con Git y GitHub.
Aplica a todos mis proyectos. Las reglas FIJAS son innegociables.
Las reglas ADAPTABLES se deciden por proyecto usando el framework de decisiones.

---

## 1. Reglas FIJAS (aplican siempre, sin excepcion)

### Commits
- Formato: **Conventional Commits** (feat:, fix:, docs:, refactor:, chore:, test:)
- Un commit = un cambio logico. No mezclar cosas sin relacion
- Nunca commitear secretos (.env, API keys, credenciales)

### Idioma

Aplica a todo el repo, no solo a commits:

- Estructura (protocolo, no contenido) — SIEMPRE ingles:
  tipo y scope de commit, descripcion corta del commit (header),
  nombres de rama, labels, nombres de archivo, encabezados de templates
  de issues/PRs, palabras clave de footer (`Closes`, `Fixes`, `BREAKING CHANGE`)
- Contenido (texto libre) — espanol:
  cuerpo del commit cuando hace falta contexto, lo que se llena adentro
  de un issue o PR, README, documentacion, comentarios de codigo

Motivo: la estructura es lo que cualquier colaborador o herramienta
(commitlint, changelog generators) espera en ingles por convencion global.
El contenido es donde se explica algo de verdad, y ahi conviene la fluidez
del idioma nativo. Como beneficio adicional, escribir tipo+descripcion en
ingles todos los dias es practica de ingles tecnico de bajo esfuerzo y
alta frecuencia.

### Push
- Push lo hago YO siempre. Ningun agente ni automatizacion pushea sin mi orden explicita
- No se pushea codigo que no compila o que rompe el proyecto

### Trabajo con agente/IA
- El agente NO hace push ni commits automaticos sin mi aprobacion
- Si el agente genera codigo, yo reviso antes de commitear
- Sin trailer de Co-Author en commits. El uso de IA se reconoce a nivel de proyecto (README o documentacion), no commit por commit
- La IA funciona como un stackoverflow avanzado: genera, yo verifico y decido
- Esto NO limita: si entiendo lo que hizo y esta correcto, commiteo sin problema

### Config global de Git
- `pull.rebase = true`
- `fetch.prune = true`
- `rerere.enabled = true`
- `init.defaultBranch = main`
- `branch.sort = -committerdate`

### Archivos obligatorios en todo repo
- `.gitignore` (apropiado al stack)
- `README.md` (minimo: que es, como correr, stack usado)
- `LICENSE` — si el repo es publico
- `.github/ISSUE_TEMPLATE/` y `.github/PULL_REQUEST_TEMPLATE.md` — si el proyecto usa issues/PRs (heredados de este repo .github como default; sobreescribir en el repo especifico solo si hace falta algo distinto)

Nunca commitear (ademas de secretos):
- `node_modules/`, `dist/`, `build/`, `__pycache__/`, `venv/`, `.venv/`
- Archivos de IDE, salvo que se compartan a proposito
- Dumps de base de datos, backups, datos de clientes o informacion laboral confidencial
- `building/` — capa de construccion personal de cada proyecto
  (definida en doc_model.md); se respalda aparte, nunca en el repo

### Gists

Gists: snippets sueltos o notas rapidas de codigo, nunca proyectos completos (para eso es un repo). Publico si es para compartir o mostrar en el portafolio, secreto si es solo para mi — pero secreto no es privado real, cualquiera con el link lo puede ver. No poner secretos ni credenciales ahi tampoco, misma regla que en cualquier repo.

---

## 2. Reglas ADAPTABLES (se deciden por proyecto)

Estas reglas tienen un valor por defecto, pero se ajustan segun el contexto del proyecto.
Cada proyecto documenta sus decisiones en su propia bitacora, usando el formato de la seccion 4.

### Estrategia de ramas

**Pregunta clave:** Trabajo solo o con otros? Hay chance de colaboracion futura?

| Contexto | Estrategia |
|----------|-----------|
| Solo, repo privado, sin colaboradores | Directo a `main` para cambios menores. Rama local para features grandes o experimentales |
| Solo, pero con posibilidad de colaboracion | Ramas con merge local. PRs opcionales para documentar decisiones |
| Colaborativo | Siempre rama + PR. Nunca push directo a `main` |

**Nombres de ramas (cuando se usen):** `tipo/descripcion-corta`
- `feature/login-form`, `fix/api-timeout`, `docs/update-readme`

### Estrategia de merge

| Contexto | Estrategia |
|----------|-----------|
| PR con muchos commits tipo "wip" | Squash merge |
| PR donde cada commit ya cuenta su propia historia | Merge normal |
| Rebase de una rama compartida despues de que otros ya hicieron pull | Nunca |

### Versionado y releases

**Pregunta clave:** El proyecto tiene usuarios? Necesita versiones estables?

| Contexto | Estrategia |
|----------|-----------|
| Proyecto en desarrollo activo, sin usuarios | No necesita tags aun |
| Proyecto con hitos claros o despliegue | Tags semanticos: `v1.0.0`, `v0.1.0-beta` |
| Libreria o herramienta reutilizable | Versionado semantico obligatorio |

### CI/CD

**Pregunta clave:** Que tan critico es que cada push este validado automaticamente?

| Contexto | Estrategia |
|----------|-----------|
| Proyecto personal en desarrollo temprano | CI opcional. Validar manualmente |
| Proyecto con deploy automatico | CI obligatorio antes de merge/deploy |
| Colaborativo | CI + checks obligatorios en PRs |

Workflow templates disponibles en este repo (`workflow-templates/`). Son punto de partida, no rigidos.

### Testing

**Pregunta clave:** Que nivel de testing necesita el proyecto HOY?

| Contexto | Estrategia |
|----------|-----------|
| MVP/prototipo | Tests manuales. Tests unitarios para logica critica |
| Proyecto estable con usuarios | Suite de tests, CI los corre |
| API publica o libreria | Coverage alto, tests de integracion |

### Issues y PRs

**Pregunta clave:** Necesito registro formal de decisiones y bugs?

| Contexto | Estrategia |
|----------|-----------|
| Solo, proyecto personal | Issues opcionales para decisiones grandes |
| Solo, proyecto profesional | Issues para bugs y features. Registro de decisiones |
| Colaborativo | Issues + PRs obligatorios. Usar templates |

Cuando un proyecto usa issues (segun la tabla ya existente), agrupar por tipo con el mismo criterio que los commits:

- Tipo: `type:feature`, `type:bug`, `type:docs`, `type:refactor`, `type:chore`
- Prioridad: `priority:high`, `priority:medium`, `priority:low`
- Estado: `status:in-progress`, `status:blocked`, `status:review`

Un issue se cierra solo al mergear el PR que lo resuelve, usando `Closes #N` en la descripcion del PR.

### Visibilidad del repo

**Pregunta clave:** Es informacion de un empleador o cliente, o tiene datos sensibles? Es una tarea de curso activa? Es portafolio?

| Contexto | Visibilidad | README |
|----------|-----------|--------|
| Repo de un empleador o cliente | Privado, siempre, sin excepcion | Espanol |
| Tarea de curso en grupo, curso activo | Privado (revisar politica de integridad academica de la UPB) | Espanol (equipo y profesores leen en espanol) |
| Proyecto personal o portafolio, sin datos sensibles | Publico | Ingles |
| Repo de metodo/templates (.github) | Publico | Ingles |

Nota GitHub Pages: el sitio publicado siempre es visible aunque el repo fuente sea privado (salvo GitHub Enterprise). No poner secretos en lo que se renderiza.

---

## 3. Framework de decisiones

### Como decidir las reglas adaptables para un proyecto nuevo

Al iniciar un proyecto, responder estas preguntas:

1. **Trabajo solo o hay/habra colaboradores?**
2. **El proyecto tiene o tendra usuarios reales?**
3. **Hay deploy automatico o manual?**
4. **Que tan critico es un bug en produccion?**
5. **El stack requiere build/compilacion?**

Las respuestas determinan que columna de la seccion 2 aplica a cada regla.

### Regla de promocion

Si una regla ADAPTABLE se repite identica en todos los proyectos durante un tiempo,
se promueve a FIJA. Esto se revisa periodicamente.

### Regla de excepcion

Si un proyecto necesita algo diferente a lo que dice este metodo, se documenta
en el README del proyecto explicando el POR QUE. No basta con "porque si".

---

## 4. Decisiones por proyecto

Cada proyecto registra sus decisiones en su propia capa de construccion o en su README, usando este formato:

### <nombre-del-proyecto> (<stack>)
- **Ramas:** <estrategia y por que>
- **Versionado:** <estrategia y por que>
- **CI/CD:** <estrategia y por que>
- **Testing:** <estrategia y por que>
- **Issues:** <estrategia y por que>

Este documento no acumula registros: define el formato.
La regla de promocion (seccion 3) se evalua revisando las bitacoras
de los proyectos activos, no una lista central.

---

## 5. Flujo de trabajo diario

```
1. git st              ver estado actual
2. (trabajar en cambios)
3. git add <archivos>  stage solo lo relevante (nunca git add . a ciegas)
4. git ci              commit con mensaje descriptivo
5. git push            cuando el cambio este completo y verificado
```

### Para features grandes:
```
1. git co -b feature/nombre
2. (trabajar, commitear incrementalmente)
3. git co main
4. git merge feature/nombre
5. git push
6. git br -d feature/nombre  limpiar rama local
```

### Contribuir a proyectos externos (fork)

Uso fork solo cuando el repo es de otra persona/organizacion y no tengo permiso de push directo. Para mis propios repos (o los de un empleador/cliente) nunca hace falta fork, trabajo con rama normal.

```
1. Fork del repo original (boton Fork en GitHub)
2. Clonar mi fork, no el original
3. Agregar el original como remote upstream:
   git remote add upstream <url-del-original>
4. Rama para el cambio: git co -b fix/nombre-corto
5. Commitear, push a mi fork
6. Abrir PR desde mi fork hacia el repo original
```

Mantener el fork al dia antes de empezar algo nuevo:
```
git fetch upstream
git checkout main
git merge upstream/main
git push
```

---

## 6. Que NO hacer

- `git add .` sin revisar que se esta incluyendo
- Commits tipo "fix", "update", "changes" sin contexto
- Push de codigo que no compila
- Force push a main
- Commitear archivos generados (node_modules, dist, build, __pycache__)
- Ignorar el .gitignore
- Dejar que un agente pushee o commitee sin mi revision

---

## 7. Relacion con otras capas

Este documento es SOLO Git y GitHub.

- **Modelo documental** (como se documenta y ejecuta cada proyecto) → `doc_model.md` (este repo)
- **Stack y herramientas** → se decide por proyecto, no globalmente. Cada proyecto elige su stack
- **Organizacion digital** → proyecto aparte (estructura de carpetas, cuentas, PC)

Git se acopla al metodo general porque:
- El metodo define fases (pensar → verificar → construir)
- Git entra en la fase de construir: cuando ya se decidio QUE hacer, Git registra el COMO se hizo
- Los commits reflejan cambios concretos del codigo, no fases del plan

---

## 8. Filosofia

- Consistencia > perfeccion
- Estructura > rigidez (las reglas sirven para ordenar, no para limitar)
- Si algo no funciona, se cambia con razon documentada
- El metodo se actualiza con la experiencia
- Lo que es FIJO da confianza. Lo que es ADAPTABLE da flexibilidad. Ambos son necesarios
