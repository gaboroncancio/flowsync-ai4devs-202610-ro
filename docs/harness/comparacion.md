# Comparación: con harness vs. sin harness

**Ticket:** "Registro de nuevas personas usuarias" (el mismo texto, palabra por palabra, en las dos copias).
**Modelo:** Opus 5.5 · effort medium · auto mode.
**Herramienta:** Claude Code en la terminal (WSL Ubuntu). La copia A usó la v2.1.329 y la copia B la v2.1.332, porque se actualizó entre las dos corridas.
**Backend:** el mismo para las dos copias (`localhost:3333`, levantado desde la copia con harness).

## El harness (copia B)

| Pieza | Familia | Qué hace |
|---|---|---|
| `CLAUDE.md` en la raíz | Orienta **antes** | Reglas: trabajar solo en `frontend/`, leer el validador y el controlador reales, no inventar endpoints, no instalar dependencias, un componente por archivo en `src/components/` con PascalCase, sin `console.log`, textos en español, `<label>` visible, errores debajo del campo, tres estados (cargando, error y éxito), espaciados en múltiplos de 8px, y ejecutar lint y build al terminar. |
| Hook `PostToolUse` en `.claude/settings.json` | Verifica **después** | Después de cada `Edit`, `Write` o `MultiEdit`, ejecuta `npx oxlint src` en `frontend/`. Si falla, devuelve el error al agente (exit 2). |

## Tabla comparativa

| | A — sin harness | B — con harness |
|---|---|---|
| **Duración** | 1 min 28 s | ~4 min 15 s |
| **Intervenciones** | 0 | 0 |
| **Archivos tocados** | **7**: 3 nuevos (`src/pages/SignupPage.tsx`, `src/pages/SignupPage.css`, `src/api/auth.ts`), 3 modificados (`src/App.tsx`, `vite.config.ts`, `index.html`) y 1 borrado (`src/App.css`) | **6**: 3 nuevos (`src/components/SignupForm.tsx`, `src/components/SignupSuccess.tsx`, `src/api/auth.ts`), 3 modificados (`src/App.tsx`, `src/App.css`, `src/index.css`) y 0 borrados |
| **Fuera del ticket** | Cambió `index.html` (idioma y título), añadió un proxy en `vite.config.ts` y borró `App.css` | Nada fuera de `frontend/src` |
| **Efectos secundarios** | Creó el usuario de prueba `probe-dup@example.com` en la base de datos **de la otra copia** y no lo borró | No creó usuarios: lo justificó con "para no escribir en tu base de datos" |
| **Lint y build** | Pasan | Pasan, y lo reportó como pide el `CLAUDE.md` |
| **Pruebas en el navegador** (vacío, contraseña corta, no coinciden, correo repetido, éxito) | 5/5 OK | 5/5 OK |
| **¿Lo probó en el navegador?** | No | No |

### Convenciones, una por una

| Convención (del `CLAUDE.md`) | A — sin harness | B — con harness |
|---|---|---|
| Componentes en `src/components/` con PascalCase | ❌ Los puso en `src/pages/` | ✅ |
| Espaciados en múltiplos de 8px | ❌ `gap: 6px` | ✅ 8 / 16 / 24 / 32 / 64 |
| Leer el validador real (8–32 caracteres, correo de 254 como máximo) | ✅ Por iniciativa propia | ✅ |
| No inventar endpoints (`POST /api/v1/auth/signup`) | ✅ | ✅ |
| No instalar dependencias | ✅ | ✅ |
| Trabajar solo en `frontend/` | ⚠️ No tocó código del backend, pero escribió en su base de datos | ✅ |
| Sin `console.log` | ✅ | ✅ |
| Textos en español, `<label>` visible, errores debajo del campo | ✅ | ✅ |
| Tres estados (cargando, error y éxito) | ✅ | ✅ El botón cambia a "Creando cuenta…" |

### Lo que arreglaría a mano

| A — sin harness | B — con harness |
|---|---|
| La tarjeta de éxito queda mal ubicada, con mucho espacio vacío arriba | El texto de ayuda ("Entre 8 y 32 caracteres") y el error se amontonan debajo de la contraseña. El error debería reemplazar a la ayuda, como hace la A |
| Inventó un texto de marketing que nadie pidió: "Empieza a usar FlowSync en un minuto" | El interlineado de los errores es muy alto cuando ocupan dos líneas |
| Mover el componente a `src/components/` y cambiar `gap: 6px` por 8px | En la pantalla de éxito, el correo se parte por el guion ("ana-" / "b@prueba.com") |
| — | La pestaña del navegador sigue diciendo "frontend" |
| **En las dos:** el nombre sale en minúscula al inicio de la frase ("ana, tu cuenta…"); en la pantalla de éxito no hay botón ni enlace para seguir; quedan restos de la plantilla de Vite (el morado `#aa3bff` y los bordes laterales); falta el enlace "¿Ya tienes cuenta? Inicia sesión" | |

### Lectura

Las dos copias cumplen los cuatro criterios del ticket, y la copia sin harness lo hizo sorprendentemente bien: fue a leer el validador sin que nadie se lo dijera.

La diferencia no está en *si funciona*, sino en **cómo se comporta el agente**:

- Con el harness respetó las convenciones de código y no se salió del área que le tocaba.
- Sin el harness se tomó libertades: borró archivos, cambió configuración y ensució la base de datos de otra copia.

Por otro lado, **el harness no le dio mejor criterio visual**. En el manejo de errores, la A tomó una decisión de UX mejor que la B. El `CLAUDE.md` garantiza lo que está escrito, no lo que falta: igual que un design system, lo que no está documentado queda a criterio de quien lo hace.

## Parte B

1. **Piezas que armé:** un `CLAUDE.md`, que orienta antes, y un hook `PostToolUse` con oxlint, que verifica después. Con la guía paso a paso ninguna de las dos me costó mucho. Lo que costó más de lo esperado fue preparar el entorno: tener dos copias, varias pestañas de Ubuntu (no PowerShell) y entender que el backend que estaba corriendo era el de una sola copia.
2. **Primera diferencia:** mientras los agentes trabajaban no noté ninguna, porque los dos dieron un resumen parecido y pasaban lint y build. La primera diferencia la vi al revisar, en la terminal, la lista de archivos de cada resumen final: la copia sin harness creó `src/pages/SignupPage.tsx` y la copia con harness `src/components/SignupForm.tsx`. Era la regla de carpetas del `CLAUDE.md`, a la vista solo en las rutas.
3. **Algo escrito en el harness que el agente igual esquivó:** el hook vigila `Edit|Write|MultiEdit`, pero para modificar `src/index.css` el agente no usó esas herramientas. Ejecutó un script de Python desde Bash, así que esa edición pasó sin que el hook la revisara. Además, el `CLAUDE.md` pide un `<label>` y errores claros, pero no dice que el error debe reemplazar al texto de ayuda, y el agente los dejó amontonados.

> **Nota:** en la copia con harness abrí sin querer una segunda sesión con el mismo ticket (a las 8:07 PM). Esa sesión encontró el código hecho, no cambió ningún archivo, pero sí creó un usuario de prueba (`prueba1795828063@ejemplo.com`) en la base de datos. Para la comparación uso solo la primera sesión (4:56 PM).
