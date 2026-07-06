# Doc Model - Anthony Arango (v1.3)

Mi método estándar para documentar y ejecutar cualquier proyecto, personal o de un empleador/cliente. Se aplica en el proyecto activo y se replica en los que vengan.

**Regla cero:** esta es la versión vigente. No se pule. Cualquier duda o mejora imaginada se anota y se sigue; no se rediseña el modelo por leerlo. **Solo se cambia cuando usarlo en un frente real lo rompe** (algo se contradice, bloquea, o no se puede cumplir): eso se registra en el log de correcciones del modelo (sección 8) y sube de versión. Leerlo para buscarle fallas es el reflejo de pulir; resístelo. El modelo sirve para *terminar* proyectos, no para quedar bonito.

---

## 1. Las dos naturalezas de documento

- **Documentos de proyecto** - el *qué*. Oficiales, suben a Git, lenguaje técnico de ejecución. Para quien use u opere el proyecto.
- **Documentos de construcción** - el *cómo lo hice*. Míos, no suben, para apoyarme. Para mí.

Se retroalimentan, pero **no se mezclan**. Nunca subo material de construcción a lo oficial.

---

## 2. Estructura estándar (esqueleto de todo proyecto)

```
proyecto/
|- README.md                # indice publico, punto de entrada        (SUBE)
|- <carpetas-de-contenido>/ # lo especifico del proyecto              (SUBE)
|- building/                # mi capa de construccion    (NO SUBE - .gitignore)
   |- sealed_state.md       # lo decidido firme. se LEE primero, siempre.
   |- personal_index.md     # tablero de posicion: en que parte voy
   |- roadmap.md            # hacia donde, en que orden
   |- decision_log.md       # por que decidi X
   |- correction_log.md     # donde me equivoque y que aprendi
```

La capa de construcción (`building/`) es la de la sección 1: mía, personal, fuera de Git.

**Proyectos sin Git:** el esqueleto y las dos naturalezas se mantienen, pero la separación oficial/construcción deja de ser división de almacenamiento (sube/no sube) y pasa a ser solo división de visibilidad dentro de la misma carpeta: lo oficial es lo que podría compartir; `building/` sigue siendo mío. El respaldo cambia de alcance (sección 7).

---

## 3. La pieza central: `sealed_state.md`

- Es **corto**. Lista de decisiones firmes por frente: "esto ya está cerrado, no reabrir".
- No es la bitácora larga. Es el resumen vivo de lo que no se toca.
- **Se LEE al empezar cualquier frente, antes de ejecutar.** El documento no sirve por existir, sirve por consultarse antes. Ese es el paso que se me olvida y el que rompe el ciclo de reabrir lo cerrado.

---

## 4. Cómo trabajo cada frente (método de ejecución)

**El primer frente de todo proyecto es el alcance.** Antes de cualquier otro frente, respondo por escrito y corto:

1. ¿Qué estoy construyendo? (una frase, sin tecnicismos)
2. ¿Para qué y para quién? (el problema real que resuelve)
3. ¿Quiénes están involucrados o afectados?
4. ¿Qué NO es este proyecto? (el límite - la pregunta que evita desviarse)
5. ¿Cómo se ve terminado? (criterio concreto de "ya cumplió")

**Visión no es alcance de la iteración.** Las 5 preguntas pueden responderse en grande - eso es la **visión**: el norte del proyecto. Da dirección pero **no se testea ni se mide**. Lo que se sella y se mide es el **alcance de la iteración actual**: qué se prueba ahora, con quiénes concretos, y cómo sé que esta iteración terminó. En `sealed_state.md` van como dos campos separados: `vision` (cambia rara vez) y `alcance de la iteracion` (se resella al abrir cada iteración). Test rápido: si una respuesta no cabe en una iteración medible ("cualquier persona", "cambiar X"), es visión - se anota como visión y se vuelve a acotar hasta que sea medible.

Las respuestas son las **primeras decisiones selladas** de `sealed_state.md` y la base de `roadmap.md`. Si más adelante un frente propone algo que contradice el alcance sellado, no se persigue en caliente: se anota y sigue, o si es real, entra por el log de correcciones. Releer el alcance al abrir cada frente es lo que detecta el punto ciego de irse desviando sin notarlo.

Para el resto de frentes:

- **Una conversación = un frente.** No mezclar temas.
- **Al abrir:** pego el `sealed_state` del frente + subo los documentos que *ese* frente edita.
- **Documentos de otros frentes:** NO los subo enteros. Pego su decisión sellada (3 líneas). El estado sellado es la **interfaz entre frentes**.
- **Si surge otro frente en medio** (y va a surgir): lo anoto en una línea y sigo. No lo persigo. Perseguirlo es rodar.
- **Al cerrar:** pido los documentos actualizados y actualizo `sealed_state` si hubo decisión nueva.

---

## 5. El log de correcciones (lo que rompe el ciclo)

- Uno **por proyecto** (`correction_log.md`), no global. Cada proyecto corrige lo suyo.
- **Disparador concreto:** cada vez que digo "me toca volver atrás" o deshago algo ya decidido -> una entrada. Sin disparador, se queda vacía.
- **Formato corto:** fecha | qué decidí mal | qué me obligó a cambiarlo | qué aprendo.
- Se lee junto al `sealed_state` al empezar.

---

## 6. Convención de nombres y escritura

**Principio de precedencia:** mi convención gobierna todo lo que es decisión mía. Donde una plataforma, lenguaje o herramienta tiene disposición propia (nombres que exige, palabras clave que parsea, estilo oficial del lenguaje), esa disposición gana - ignorarla rompe funcionalidad o va contra el estándar del ecosistema. Test rápido en la duda: ¿quién lee este nombre? Si solo humanos -> mi convención. Si algo automático lo parsea o el lenguaje tiene estándar oficial -> lo externo.

**Identificadores** (nombres de carpetas, archivos y código) - **inglés**, ASCII, minúsculas. Misma regla de idioma que `git_method.md`: la estructura es protocolo y va en inglés, sin excepciones.

- **Carpetas:** `NN-kebab-case`.
- **Archivos:** `snake_case`. Prefijo que nombra el **tipo** de documento + número que **reinicia por carpeta**. Ej.: `arch_01_...`, `log_01_...`, `rep_01_...`, `proc_01_...`.
- La **regla** (prefijo = tipo, numeración por carpeta) es universal; la **tabla de prefijos** se declara al inicio de cada proyecto según sus tipos de documento (un proyecto de código usaría `adr_`, `spec_`, `test_`, etc.).
- **Mayúsculas solo cuando algo externo lo impone** (aplicación directa del principio de precedencia): `README.md` (estándar universal de entrada, aplica con o sin Git) y los nombres que una plataforma exige literalmente (ej. `LICENSE`, `ISSUE_TEMPLATE/` en GitHub). Todo archivo cuyo nombre decido yo va en minúsculas - incluidos los documentos de método (`git_method.md`, `doc_model.md`).

**Contenido que se lee** (el texto dentro de los documentos, salidas de consola para personas) - español correcto y natural, **con** tildes, ñ y puntuación. La regla de inglés/ASCII es solo para identificadores, **nunca** para la prosa que alguien va a leer.

**Caracteres tecleables:** todo contenido que mantengo (documentos oficiales y `building/`) usa solo caracteres de mi teclado (layout latinoamericano). Reemplazos fijos: rayas largas -> `-`, flechas unicode -> `->`, comillas tipográficas -> rectas, puntos suspensivos unicode -> `...`, dibujo de árboles -> `|-`. Separador de campos en logs: `|`. Los signos estructurales (`#`, `*`, listas, tablas) los gobierna markdown - formato externo, principio de precedencia. Lo generado por herramientas se ajusta a este alfabeto antes de integrarse.

**Comentarios en código:** MAYÚSCULA SOSTENIDA para títulos de sección; oración normal para funciones o elementos concretos. En español (son contenido, no protocolo).

---

## 7. Reglas contra los puntos ciegos

- `building/` no sube a Git -> está en el `.gitignore` estándar de todo proyecto (regla en `git_method.md`) y se **respalda aparte**. Es lo más valioso y sería lo único sin copia. Respaldo por defecto: **Google Drive, cuenta personal** - nunca cuentas que puedo perder (la universitaria se pierde al graduarme). En proyectos con Git, lo oficial ya tiene copia en el remoto: se respalda solo `building/`. En proyectos sin Git se respalda la **carpeta completa** del proyecto. En ambos casos el respaldo es **obligatorio y manual** (sincronización de la carpeta), no opcional. Proyectos de un empleador/cliente: por ahora se respaldan igual en mi Drive personal; queda pendiente transferir ese material a infraestructura del empleador cuando exista - la responsabilidad de que tenga copia es mía mientras tanto.
- Todo en `building/` se escribe **corto**: fecha + verbo + resultado. Si da pereza mantenerlo, está mal escrito.
- El modelo se prueba **terminando** algo con él. Si me descubro puliendo el modelo en vez de usarlo, ese es el síntoma: parar y ejecutar.

---

## 8. Relación con otras capas y log de correcciones del modelo

Este documento es SOLO documentación y ejecución de proyectos. Git y GitHub -> `git_method.md` (este mismo repo). Las dos capas comparten la regla de idioma: identificadores en inglés, contenido en español.

### Log de correcciones del modelo

- **2026-07 | v1.2 -> v1.3 |** Decidí mal: la convención de escritura regulaba idioma y tildes pero no la tipografía del contenido; los documentos generados con IA llegaron con rayas largas, flechas unicode y símbolos que mi teclado no produce. Qué me obligó a cambiarlo: mantener a mano archivos con caracteres que no puedo teclear rompe la mantenibilidad que exige la sección 7. Qué aprendo: lo generado hereda la tipografía de la herramienta; la convención debe fijar el alfabeto de trabajo explícito, y el punto de aplicación es la herramienta que genera, no la corrección manual después.
- **2026-07 | v1.1 -> v1.2 |** (1) Decidí mal: dejar el respaldo de `building/` como "aparte (OneDrive o repo privado)", sin destino por defecto, sin regla para proyectos sin Git y sin obligatoriedad. Qué me obligó a cambiarlo: un proyecto real sin Git dejó la carpeta completa sin copia y sin criterio de dónde respaldarla. Qué aprendo: una regla de respaldo sin destino concreto no es regla, es intención. (2) Decidí mal: el frente de alcance no separaba visión de iteración; respondí las 5 preguntas mezclando el norte del proyecto con la prueba concreta, y el piloto quedó inmedible. Qué me obligó a cambiarlo: sellar un alcance que no se podía medir. Qué aprendo: la visión orienta pero no se testea; solo se sella lo que una iteración puede medir.
- **2026-07 | v1 -> v1.1 |** Decidí mal: prefijos de archivo en español (`arq_`, `bit_`, `inf_`, `pro_`) y nombres de la capa de construcción en español. Qué me obligó a cambiarlo: al usar el modelo junto a `git_method.md`, su regla fija de idioma (identificadores siempre en inglés) chocó de frente con los prefijos - dos reglas fijas contradiciéndose. Qué aprendo: una regla transversal (idioma) debe definirse en una sola capa y las demás la heredan; las excepciones por capa son deuda. También en esta versión: se eliminaron menciones de empleador y proyectos específicos (el modelo es mío y aplica a cualquier contexto laboral), se agregó el principio de precedencia (sección 6), y se incorporó el frente de alcance como primer frente obligatorio (sección 4) - la v1 ejecutaba bien pero no definía qué se está construyendo antes de construir, que era el punto ciego de arrancar proyectos desviados.
