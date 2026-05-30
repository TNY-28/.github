# Git Method - Anthony Arango

Mi metodo personal para trabajar con Git y GitHub.
Aplica a todos mis proyectos. Las reglas FIJAS son innegociables.
Las reglas ADAPTABLES se deciden por proyecto usando el framework de decisiones.

---

## 1. Reglas FIJAS (aplican siempre, sin excepcion)

### Commits
- Formato: **Conventional Commits** (feat:, fix:, docs:, refactor:, chore:, test:)
- Idioma: ingles para el tipo y mensaje, espanol en el cuerpo si hace falta contexto
- Un commit = un cambio logico. No mezclar cosas sin relacion
- Nunca commitear secretos (.env, API keys, credenciales)

### Push
- Push lo hago YO siempre. Ningun agente ni automatizacion pushea sin mi orden explicita
- No se pushea codigo que no compila o que rompe el proyecto

### Trabajo con agente/IA
- El agente NO hace push ni commits automaticos sin mi aprobacion
- Si el agente genera codigo, yo reviso antes de commitear
- Co-Author en commits donde la IA genero codigo (transparencia)
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

---

## 2. Reglas ADAPTABLES (se deciden por proyecto)

Estas reglas tienen un valor por defecto, pero se ajustan segun el contexto del proyecto.
Cada proyecto documenta sus decisiones en la seccion 4.

### Estrategia de ramas

**Pregunta clave:** Trabajo solo o con otros? Hay chance de colaboracion futura?

| Contexto | Estrategia |
|----------|-----------|
| Solo, repo privado, sin colaboradores | Directo a `main` para cambios menores. Rama local para features grandes o experimentales |
| Solo, pero con posibilidad de colaboracion | Ramas con merge local. PRs opcionales para documentar decisiones |
| Colaborativo | Siempre rama + PR. Nunca push directo a `main` |

**Nombres de ramas (cuando se usen):** `tipo/descripcion-corta`
- `feature/login-form`, `fix/api-timeout`, `docs/update-readme`

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

### proyecto-frontend (React/Vite - frontend)
- **Ramas:** directo a main (trabajo solo, repo privado, sin colaboradores futuros)
- **Versionado:** sin tags por ahora (en desarrollo activo)
- **CI/CD:** pendiente (cuando haya deploy)
- **Testing:** manual por ahora, tests unitarios para logica critica
- **Issues:** no por ahora

### proyecto-backend (Django/Python - backend)
- **Ramas:** directo a main (mismo contexto que PWA)
- **Versionado:** sin tags por ahora
- **CI/CD:** pendiente
- **Testing:** manual + tests Django para endpoints criticos
- **Issues:** no por ahora

### .github (este repo - templates globales)
- **Ramas:** directo a main (es config, no codigo)
- **Versionado:** no aplica
- **CI/CD:** no aplica
- **Testing:** no aplica

### Thony-arango (perfil README)
- **Ramas:** directo a main
- **Versionado:** no aplica

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

---

## 6. Que NO hacer

- `git add .` sin revisar que se esta incluyendo
- Commits tipo "fix", "update", "changes" sin contexto
- Push de codigo que no compila
- Force push a main
- Commitear archivos generados (node_modules, dist, build, __pycache__)
- Ignorar el .gitignore
- Dejar que un agente pushee o commitee sin tu revision

---

## 7. Relacion con otras capas

Este documento es SOLO Git y GitHub.

- **Metodo general de desarrollo** (como analizar, disenar, construir) → `Manual-de-Metodo-Analisis-y-Diseno.md` (carpeta personal)
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
