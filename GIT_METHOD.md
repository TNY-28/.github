# Git Method - Anthony Arango

Mi metodo personal para trabajar con Git y GitHub.
Aplica a todos mis proyectos salvo que se indique lo contrario.

---

## 1. Reglas fijas (no cambian)

### Commits
- Formato: **Conventional Commits** (feat:, fix:, docs:, refactor:, chore:, test:)
- Idioma: ingles para el mensaje, espanol en el cuerpo si hace falta contexto
- Un commit = un cambio logico. No mezclar cosas sin relacion
- Nunca commitear secretos (.env, API keys, credenciales)

### Ramas
- `main` es la rama estable. Siempre debe compilar/funcionar
- Nombres de ramas: `tipo/descripcion-corta`
  - `feature/login-form`
  - `fix/api-timeout`
  - `docs/update-readme`
  - `refactor/clean-utils`

### Archivos obligatorios en todo repo
- `.gitignore` (apropiado al stack)
- `README.md` (minimo: que es, como correr, stack usado)

---

## 2. Reglas adaptables (dependen del proyecto)

### Modo solo (repos donde trabajo yo solo)
- Puedo commitear directo a `main` para cambios menores
- Para features grandes o experimentales: usar rama y merge local
- PRs no son obligatorios, pero si quiero documentar una decision grande, puedo crear uno
- Push cuando el cambio este listo, no por cada commit

### Modo colaborativo (repos con mas personas)
- Nunca push directo a `main`
- Siempre rama + PR
- PR necesita descripcion clara de que cambia y como probarlo
- Usar las plantillas de issue/PR del repo `.github`

### Modo con agente/IA
- Las mismas reglas aplican sin importar quien escribe el codigo
- El agente NO hace push sin mi orden explicita
- El agente NO hace commits automaticos sin mi aprobacion
- Si el agente genera codigo, yo reviso antes de commitear
- Co-Author en commits generados con IA (transparencia)

---

## 3. Flujo de trabajo diario

```
1. git st            → ver estado actual
2. (trabajar en cambios)
3. git add <archivos> → stage solo lo relevante (no git add .)
4. git ci            → commit con mensaje descriptivo
5. git push          → cuando el cambio este completo
```

### Para features grandes:
```
1. git co -b feature/nombre
2. (trabajar, commitear)
3. git co main
4. git merge feature/nombre
5. git push
6. git br -d feature/nombre  → limpiar rama local
```

---

## 4. Que NO hacer

- `git add .` sin revisar que se esta incluyendo
- Commits tipo "fix", "update", "changes" sin contexto
- Push de codigo que no compila
- Force push a main
- Commitear archivos generados (node_modules, dist, build)
- Ignorar el .gitignore

---

## 5. GitHub

### Issues
- Usar para trackear bugs y features, incluso trabajando solo
- Ayuda a mantener registro de decisiones y prioridades
- Templates disponibles en el repo `.github`

### Releases/Tags
- Usar tags semanticos cuando un proyecto llegue a un hito estable
- Formato: `v1.0.0`, `v0.1.0-beta`

---

## 6. Notas

- Este metodo es un punto de partida. Se actualiza con la experiencia.
- Lo importante es consistencia, no perfeccion.
- Si algo no aplica a un proyecto especifico, se documenta en el README de ese proyecto.
