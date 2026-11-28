# Prompts

Aquí van **todos los prompts que lanzaste** para hacer el ejercicio, en el orden en que los
lanzaste, con el modelo y la herramienta de cada uno.

Esto no es papeleo. Lo que se revisa es **cómo pediste las cosas**, no solo lo que salió: un
resultado flojo con un prompt bueno y un resultado flojo con un prompt vago necesitan feedback
distinto, y sin este archivo no se distinguen.

## Cómo rellenarlo

- Un apartado `## Prompt N` por cada prompt.
- **Pega el prompt tal cual lo lanzaste**, dentro del bloque de código, aunque ocupe diez líneas
  y aunque tenga faltas. No lo reescribas para que quede bien: el que arreglaste mentalmente
  después no es el que lanzaste.
- Incluye también los que **no funcionaron**. Suelen ser los más útiles de leer.
- `Modelo` y `Herramienta` en todos. Si cambiaste de una a otra a mitad, se nota aquí.

---

## Prompt 1 — Pedir guía para montar el harness

**Modelo:** Opus 5.5
**Herramienta:** Claude (app de escritorio, pestaña Code), fuera del repo

```
Ahora continuamos con las lecturas, por ahora quiero que me ayudes a hacer la actividad paso a paso, y me vayas indicando lo que debo hacer: en caso de dudas haz me saber, nosotros en la empresa adelantamos algo.
```

**Qué salió:** junto al prompt pegué el enunciado del ejercicio y las indicaciones del líder. A partir de ahí fue una conversación de varios mensajes: Claude me guió para preparar el entorno, escribir el `CLAUDE.md` con nano y crear el hook en `.claude/settings.json`. Los mensajes de seguimiento fueron cortos, del tipo "listo, me quedó así" con pantallazos.

## Prompt 2 — Corrida A (sin harness)

**Modelo:** Opus 5.5 · effort medium · auto mode
**Herramienta:** Claude Code v2.1.329, terminal WSL Ubuntu, en `flowsync-sin-harness`

```
Título: Registro de nuevas personas usuarias

Como persona que quiere empezar a usar FlowSync,
quiero crear mi cuenta desde la web,
para poder acceder a la aplicación.

Criterios de aceptación:
- Hay una pantalla de registro donde la persona escribe sus datos para crear la cuenta.
- Si algún dato no es válido, se le indica qué está mal y cómo corregirlo.
- Si el correo ya tiene una cuenta, se le informa.
- Cuando la cuenta se crea correctamente, ve una confirmación clara.
```

**Qué salió:** funcionó a la primera, sin intervenciones (1 min 28 s). Puso los componentes en `src/pages/`, usó un `gap: 6px` y creó un usuario de prueba en la base de datos de la otra copia.

## Prompt 3 — Corrida B (con harness)

**Modelo:** Opus 5.5 · effort medium · auto mode
**Herramienta:** Claude Code v2.1.332, terminal WSL Ubuntu, en `flowsync-ai4devs-202610-ro` (con `CLAUDE.md` y hook)

```
Título: Registro de nuevas personas usuarias

Como persona que quiere empezar a usar FlowSync,
quiero crear mi cuenta desde la web,
para poder acceder a la aplicación.

Criterios de aceptación:
- Hay una pantalla de registro donde la persona escribe sus datos para crear la cuenta.
- Si algún dato no es válido, se le indica qué está mal y cómo corregirlo.
- Si el correo ya tiene una cuenta, se le informa.
- Cuando la cuenta se crea correctamente, ve una confirmación clara.
```

**Qué salió:** funcionó a la primera, sin intervenciones (~4 min 15 s). Siguió el `CLAUDE.md`: componentes en `src/components/` y espaciados en múltiplos de 8. No creó usuarios de prueba.

## Prompt 4 — Corrida B repetida por error

**Modelo:** Opus 5.5 · effort medium · auto mode
**Herramienta:** Claude Code v2.1.332, terminal WSL Ubuntu, en `flowsync-ai4devs-202610-ro`

```
Título: Registro de nuevas personas usuarias

Como persona que quiere empezar a usar FlowSync,
quiero crear mi cuenta desde la web,
para poder acceder a la aplicación.

Criterios de aceptación:
- Hay una pantalla de registro donde la persona escribe sus datos para crear la cuenta.
- Si algún dato no es válido, se le indica qué está mal y cómo corregirlo.
- Si el correo ya tiene una cuenta, se le informa.
- Cuando la cuenta se crea correctamente, ve una confirmación clara.
```

**Qué salió:** abrí sin querer una segunda sesión en la misma copia. Encontró el código del Prompt 3, lo verificó contra el backend y no cambió ningún archivo, pero sí creó el usuario de prueba `prueba1795828063@ejemplo.com`. No cuenta para la comparación.
