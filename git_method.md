# Git Method - Anthony Arango (v2)

Mi método personal para trabajar con Git y GitHub.
Aplica a todos mis proyectos. Las reglas FIJAS son innegociables.
Las reglas ADAPTABLES se deciden por proyecto usando el framework de decisiones.

---

## 1. Reglas FIJAS (aplican siempre, sin excepción)

### Commits
- Formato: **Conventional Commits** (feat:, fix:, docs:, refactor:, chore:, test:)
- Un commit = un cambio lógico. No mezclar cosas sin relación
- Nunca commitear secretos (.env, API keys, credenciales)

### Idioma

Aplica a todo el repo, no solo a commits:

- Estructura (protocolo, no contenido) - SIEMPRE inglés:
  tipo y scope de commit, descripción corta del commit (header),
  nombres de rama, labels, nombres de archivo, encabezados de templates
  de issues/PRs, palabras clave de footer (`Closes`, `Fixes`, `BREAKING CHANGE`)
- Contenido (texto libre) - español:
  cuerpo del commit cuando hace falta contexto, lo que se llena adentro
  de un issue o PR, README, documentación, comentarios de código

Motivo: la estructura es lo que cualquier colaborador o herramienta
(commitlint, changelog generators) espera en inglés por convención global.
El contenido es donde se explica algo de verdad, y ahí conviene la fluidez
del idioma nativo. Como beneficio adicional, escribir tipo+descripción en
inglés todos los días es práctica de inglés técnico de bajo esfuerzo y
alta frecuencia.

### Push
- Push lo hago YO siempre. Ningún agente ni automatización pushea sin mi orden explícita
- No se pushea código que no compila o que rompe el proyecto

### Trabajo con agente/IA
- El agente NO hace push ni commits automáticos sin mi aprobación
- Si el agente genera código, yo reviso antes de commitear
- Sin trailer de Co-Author en commits. El uso de IA se reconoce a nivel de proyecto (README o documentación), no commit por commit
- La IA funciona como un stackoverflow avanzado: genera, yo verifico y decido
- Esto NO limita: si entiendo lo que hizo y está correcto, commiteo sin problema

### Config global de Git
- `pull.rebase = true`
- `fetch.prune = true`
- `rerere.enabled = true`
- `init.defaultBranch = main`
- `branch.sort = -committerdate`

### Archivos obligatorios en todo repo
- `.gitignore` (apropiado al stack)
- `README.md` (mínimo: qué es, cómo correr, stack usado)
- `LICENSE` - si el repo es público
- `.github/ISSUE_TEMPLATE/` y `.github/PULL_REQUEST_TEMPLATE.md` - si el proyecto usa issues/PRs (heredados de este repo .github como default; sobreescribir en el repo específico solo si hace falta algo distinto)

Nunca commitear (además de secretos):
- `node_modules/`, `dist/`, `build/`, `__pycache__/`, `venv/`, `.venv/`
- Archivos de IDE, salvo que se compartan a propósito
- Dumps de base de datos, backups, datos de clientes o información laboral confidencial
- `building/` - capa de construcción personal de cada proyecto
  (definida en doc_method.md); se respalda aparte, nunca en el repo

### Gists

Gists: snippets sueltos o notas rápidas de código, nunca proyectos completos (para eso es un repo). Público si es para compartir o mostrar en el portafolio, secreto si es solo para mí - pero secreto no es privado real, cualquiera con el link lo puede ver. No poner secretos ni credenciales ahí tampoco, misma regla que en cualquier repo.

---

## 2. Reglas ADAPTABLES (se deciden por proyecto)

Estas reglas tienen un valor por defecto, pero se ajustan según el contexto del proyecto.
Cada proyecto documenta sus decisiones en su propia bitácora, usando el formato de la sección 4.

### Estrategia de ramas

**Pregunta clave:** ¿Trabajo solo o con otros? ¿Hay chance de colaboración futura?

| Contexto | Estrategia |
|----------|-----------|
| Solo, repo privado, sin colaboradores | Directo a `main` para cambios menores. Rama local para features grandes o experimentales |
| Solo, pero con posibilidad de colaboración | Ramas con merge local. PRs opcionales para documentar decisiones |
| Colaborativo | Siempre rama + PR. Nunca push directo a `main` |

**Nombres de ramas (cuando se usen):** `tipo/descripcion-corta`
- `feature/login-form`, `fix/api-timeout`, `docs/update-readme`

### Estrategia de merge

| Contexto | Estrategia |
|----------|-----------|
| PR con muchos commits tipo "wip" | Squash merge |
| PR donde cada commit ya cuenta su propia historia | Merge normal |
| Rebase de una rama compartida después de que otros ya hicieron pull | Nunca |

### Versionado y releases

**Pregunta clave:** ¿El proyecto tiene usuarios? ¿Necesita versiones estables?

| Contexto | Estrategia |
|----------|-----------|
| Proyecto en desarrollo activo, sin usuarios | No necesita tags aún |
| Proyecto con hitos claros o despliegue | Tags semánticos: `v1.0.0`, `v0.1.0-beta` |
| Librería o herramienta reutilizable | Versionado semántico obligatorio |

### CI/CD

**Pregunta clave:** ¿Qué tan crítico es que cada push esté validado automáticamente?

| Contexto | Estrategia |
|----------|-----------|
| Proyecto personal en desarrollo temprano | CI opcional. Validar manualmente |
| Proyecto con deploy automático | CI obligatorio antes de merge/deploy |
| Colaborativo | CI + checks obligatorios en PRs |

Workflow templates disponibles en este repo (`workflow-templates/`). Son punto de partida, no rígidos.

### Testing

**Pregunta clave:** ¿Qué nivel de testing necesita el proyecto HOY?

| Contexto | Estrategia |
|----------|-----------|
| MVP/prototipo | Tests manuales. Tests unitarios para lógica crítica |
| Proyecto estable con usuarios | Suite de tests, CI los corre |
| API pública o librería | Coverage alto, tests de integración |

### Issues y PRs

**Pregunta clave:** ¿Necesito registro formal de decisiones y bugs?

| Contexto | Estrategia |
|----------|-----------|
| Solo, proyecto personal | Issues opcionales para decisiones grandes |
| Solo, proyecto profesional | Issues para bugs y features. Registro de decisiones |
| Colaborativo | Issues + PRs obligatorios. Usar templates |

Cuando un proyecto usa issues (según la tabla ya existente), agrupar por tipo con el mismo criterio que los commits:

- Tipo: `type:feature`, `type:bug`, `type:docs`, `type:refactor`, `type:chore`
- Prioridad: `priority:high`, `priority:medium`, `priority:low`
- Estado: `status:in-progress`, `status:blocked`, `status:review`

Un issue se cierra solo al mergear el PR que lo resuelve, usando `Closes #N` en la descripción del PR.

### Visibilidad del repo

**Pregunta clave:** ¿Es información de un empleador o cliente, o tiene datos sensibles? ¿Es una tarea de curso activa? ¿Es portafolio?

| Contexto | Visibilidad | README |
|----------|-----------|--------|
| Repo de un empleador o cliente | Privado, siempre, sin excepción | Español |
| Tarea de curso en grupo, curso activo | Privado (revisar política de integridad académica de la UPB) | Español (equipo y profesores leen en español) |
| Proyecto personal o portafolio, sin datos sensibles | Público | Inglés |
| Repo de método/templates (.github) | Público | Inglés |

Nota GitHub Pages: el sitio publicado siempre es visible aunque el repo fuente sea privado (salvo GitHub Enterprise). No poner secretos en lo que se renderiza.

---

## 3. Framework de decisiones

### Cómo decidir las reglas adaptables para un proyecto nuevo

Al iniciar un proyecto, responder estas preguntas:

1. **¿Trabajo solo o hay/habrá colaboradores?**
2. **¿El proyecto tiene o tendrá usuarios reales?**
3. **¿Hay deploy automático o manual?**
4. **¿Qué tan crítico es un bug en producción?**
5. **¿El stack requiere build/compilación?**

Las respuestas determinan qué columna de la sección 2 aplica a cada regla.

### Regla de promoción

Si una regla ADAPTABLE se repite idéntica en todos los proyectos durante un tiempo,
se promueve a FIJA. Esto se revisa periódicamente.

### Regla de excepción

Si un proyecto necesita algo diferente a lo que dice este método, se documenta
en el README del proyecto explicando el PORQUÉ. No basta con "porque sí".

---

## 4. Decisiones por proyecto

Cada proyecto registra sus decisiones en su propia capa de construcción o en su README, usando este formato:

### <nombre-del-proyecto> (<stack>)
- **Ramas:** <estrategia y por qué>
- **Versionado:** <estrategia y por qué>
- **CI/CD:** <estrategia y por qué>
- **Testing:** <estrategia y por qué>
- **Issues:** <estrategia y por qué>

Este documento no acumula registros: define el formato.
La regla de promoción (sección 3) se evalúa revisando las bitácoras
de los proyectos activos, no una lista central.

---

## 5. Flujo de trabajo diario

```
1. git st              ver estado actual
2. (trabajar en cambios)
3. git add <archivos>  stage solo lo relevante (nunca git add . a ciegas)
4. git ci              commit con mensaje descriptivo
5. git push            cuando el cambio esté completo y verificado
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

Uso fork solo cuando el repo es de otra persona/organización y no tengo permiso de push directo. Para mis propios repos (o los de un empleador/cliente) nunca hace falta fork, trabajo con rama normal.

```
1. Fork del repo original (botón Fork en GitHub)
2. Clonar mi fork, no el original
3. Agregar el original como remote upstream:
   git remote add upstream <url-del-original>
4. Rama para el cambio: git co -b fix/nombre-corto
5. Commitear, push a mi fork
6. Abrir PR desde mi fork hacia el repo original
```

Mantener el fork al día antes de empezar algo nuevo:
```
git fetch upstream
git checkout main
git merge upstream/main
git push
```

---

## 6. Qué NO hacer

- `git add .` sin revisar qué se está incluyendo
- Commits tipo "fix", "update", "changes" sin contexto
- Push de código que no compila
- Force push a main
- Commitear archivos generados (node_modules, dist, build, __pycache__)
- Ignorar el .gitignore
- Dejar que un agente pushee o commitee sin mi revisión

---

## 7. Relación con otras capas y log de cambios del método

Este documento es SOLO Git y GitHub.

- **Modelo documental** (cómo se documenta y ejecuta cada proyecto) -> `doc_method.md` (este repo)
- **Stack y herramientas** -> se decide por proyecto, no globalmente. Cada proyecto elige su stack
- **Organización digital** -> proyecto aparte (estructura de carpetas, cuentas, PC)

Git se acopla al método general porque:
- El método define fases (pensar -> verificar -> construir)
- Git entra en la fase de construir: cuando ya se decidió QUÉ hacer, Git registra el CÓMO se hizo
- Los commits reflejan cambios concretos del código, no fases del plan

**Precedencia entre capas:** este documento hereda de `doc_method.md` las reglas transversales (idioma, alfabeto tecleable, `building/`, respaldo) y no las redefine - solo agrega lo propio de Git y GitHub. En caso de conflicto, gana `doc_method.md`.

### Log de cambios del método

- **2026-07 | v1 -> v2 |** Decidí mal: no darle a este documento número de versión ni log de cambios propio, a diferencia de `doc_method.md`, que sí versiona y registra sus correcciones. Qué me obligó a cambiarlo: `sealed_state.md` ya citaba "git_method.md v2" sin que el archivo tuviera ese número en ningún lado, y la declaración explícita de jerarquía entre capas (ver arriba) exigía dejar constancia de cuándo y por qué cambia esta capa. Qué aprendo: si una capa del método se corrige y se vuelve a sellar, necesita el mismo tratamiento que `doc_method.md` - versión en el título y log de cambios propio, no solo el sellado externo en `sealed_state.md`.

---

## 8. Filosofía

- Consistencia > perfección
- Estructura > rigidez (las reglas sirven para ordenar, no para limitar)
- Si algo no funciona, se cambia con razón documentada
- El método se actualiza con la experiencia
- Lo que es FIJO da confianza. Lo que es ADAPTABLE da flexibilidad. Ambos son necesarios
