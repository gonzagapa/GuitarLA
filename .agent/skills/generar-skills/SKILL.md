---
name: generar-skills
description: Genera una nueva skill en el workspace actual siguiendo la estructura y convenciones de Antigravity. Úsala cuando el usuario pida crear, añadir o definir una nueva skill para el proyecto.
---

# Skill: Generar Skills

Cuando el usuario te pida crear una nueva skill para el workspace, sigue estos pasos de forma precisa.

## ¿Qué es una Skill?

Una skill es un paquete reutilizable de conocimiento e instrucciones que extiende las capacidades del agente para tareas específicas. Consiste en una carpeta con un archivo `SKILL.md` obligatorio y, opcionalmente, subcarpetas de soporte.

## Estructura de una Skill

```
.agent/skills/<nombre-de-la-skill>/
├── SKILL.md           ← Obligatorio
├── scripts/           ← Opcional: scripts de ayuda
├── examples/          ← Opcional: implementaciones de referencia
└── resources/         ← Opcional: plantillas y otros recursos
```

### Ubicaciones válidas

- **Local (específica del proyecto):** `<raíz-del-workspace>/.agent/skills/<carpeta-de-la-skill>/`
- **Global (todos los proyectos):** `~/.gemini/antigravity/skills/<carpeta-de-la-skill>/`

Salvo que el usuario indique lo contrario, crea las skills **localmente** dentro del workspace actual.

## Formato del archivo SKILL.md

El `SKILL.md` debe comenzar siempre con un bloque de frontmatter YAML:

```markdown
---
name: nombre-de-la-skill
description: Descripción clara en tercera persona. Incluye palabras clave que ayuden al agente a decidir cuándo usar esta skill.
---

# Título de la Skill

Instrucciones detalladas en markdown que el agente seguirá cuando esta skill esté activa.
```

### Reglas del frontmatter

| Campo         | Descripción                                                                                     | Obligatorio |
| ------------- | ----------------------------------------------------------------------------------------------- | ----------- |
| `name`        | Identificador único en minúsculas con guiones. Si se omite, se usará el nombre de la carpeta.   | No          |
| `description` | **Crítico para el descubrimiento.** Escríbela en tercera persona con palabras clave relevantes. | Sí          |

## Pasos para crear una nueva Skill

1. **Identifica el propósito** de la skill: ¿qué tarea específica realizará?
2. **Elige el nombre** en kebab-case (minúsculas y guiones), descriptivo y conciso.
3. **Crea la carpeta** en `.agent/skills/<nombre-de-la-skill>/`.
4. **Crea el archivo `SKILL.md`** con:
   - Frontmatter YAML con `name` y `description`.
   - Instrucciones claras en markdown.
   - Árbol de decisión si hay múltiples enfoques posibles.
   - Referencias a scripts/recursos si corresponde.
5. **Agrega carpetas opcionales** (`scripts/`, `examples/`, `resources/`) solo si aportan valor real.
6. **Verifica** que el `SKILL.md` sea legible y accionable por sí solo.

## Buenas Prácticas

- **Enfoque único:** Cada skill debe hacer una sola cosa bien. Evita skills genéricas o demasiado amplias.
- **Descripción precisa:** Usa palabras clave específicas para que el agente sepa exactamente cuándo aplicar la skill.
- **Divulgación progresiva:** Si incluyes scripts, dile al agente que los ejecute (con `--help`) en lugar de leer el código fuente.
- **Árbol de decisión:** Incluye guía sobre qué enfoque tomar en escenarios específicos.
- **Idioma consistente:** Escribe las instrucciones en el mismo idioma que el equipo usa cotidianamente.

## Ejemplo de Skill bien formada

```markdown
---
name: revision-de-codigo
description: Revisa cambios de código en busca de errores, problemas de estilo y buenas prácticas. Úsala al revisar Pull Requests o al hacer code review de cualquier archivo.
---

# Revisión de Código

Al revisar código, sigue estos pasos:

## Lista de verificación

1. **Corrección:** ¿El código hace lo que se supone que debe hacer?
2. **Casos borde:** ¿Se manejan las condiciones de error?
3. **Legibilidad:** ¿El código es fácil de entender?
4. **Rendimiento:** ¿Hay operaciones innecesariamente costosas?
5. **Seguridad:** ¿Se validan entradas del usuario?
```

## Árbol de Decisión para esta Skill

```
¿El usuario quiere crear una skill?
├── ¿Local (solo este proyecto)?  → .agent/skills/<nombre>/
└── ¿Global (todos los proyectos)? → ~/.gemini/antigravity/skills/<nombre>/

¿Necesita scripts de ayuda?
├── Sí → Crear carpeta scripts/ con los scripts correspondientes
└── No → Solo SKILL.md es suficiente
```
