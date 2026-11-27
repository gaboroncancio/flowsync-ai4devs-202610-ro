# Comparación: mismo encargo con y sin harness

**Encargo:** FLOW-1 "Registro de nuevos usuarios" (Jira), mismo texto en ambas copias vía `ticket.txt`.
**Modelo:** Opus 5.5 en ambas · **Herramienta:** Claude Code (v2.1.329 con harness, v2.1.332 sin harness).
**Harness:** `CLAUDE.md` (orienta antes) + hook `PostToolUse` con `oxlint` en `.claude/settings.json` (comprueba después).

| Casilla | Sin harness | Con harness |
|---|---|---|
| Tiempo | 8:58 → 8:59 (~1 min) | 8:57 → 9:00 (~3 min) |
| Archivos tocados | **5**: 2 modificados, 3 nuevos | **15**: 4 modificados, 7 nuevos, 4 borrados |
| Convenciones respetadas | No había ninguna escrita. Por iniciativa propia: llamadas en `src/api/`, textos en español, leyó el backend y detectó `passwordConfirmation`. | Llamadas a la API en `src/api/`; URL en un único lugar (`config.ts` + `VITE_API_URL`); un componente por archivo (`SignupForm`, `Welcome`); textos en español; borró restos de la plantilla Vite; sin dependencias nuevas; pasó lint y build; leyó el validador y replicó longitudes y confirmación. |
| Convenciones no respetadas | (Medidas contra el CLAUDE.md del otro lado) URL definida dentro de `auth.ts`; bienvenida embebida en `App.tsx`; dejó assets e `index.html` de la plantilla (`lang="en"`, título "frontend"). | Hizo `fullName` obligatorio aunque el validador lo marca opcional. Arrancó el backend y escribió en su base de datos pese a "SOLO LECTURA". |
| Intervenciones mías | 0 | 0 |
| Qué arreglaría a mano | Limpiar assets de la plantilla; centralizar la URL; "Cerrar sesión" no invalida el token en el backend; decidir si el nombre es obligatorio; probar en navegador. | Decidir si el nombre es obligatorio; borrar el usuario de prueba de la BD; probar en navegador. |

**Nota:** ambas copias usaron el mismo backend en `localhost:3333` (el de la carpeta con harness), así que compartieron base de datos. Ninguna se probó en el navegador.

## Parte B

1. **Piezas que monté y cuál me costó más:** `CLAUDE.md` y un hook `PostToolUse` que ejecuta `oxlint`. Lo que más tiempo me llevó fue el `CLAUDE.md`: para escribir reglas concretas tuve que leer antes el validador, las rutas y los scripts del `package.json`.
2. **Primera diferencia que vi y dónde estaba mirando:** en la lista de `Write(...)` de cada terminal, antes de abrir archivos. La copia con harness creó primero `src/api/config.ts` para la URL; la pelada escribió la URL directamente dentro de `src/api/auth.ts`.
3. **Algo que dejé escrito en el harness y el agente no cumplió:** el `CLAUDE.md` pedía replicar las reglas del validador "(longitudes, formatos, campos opcionales, confirmaciones)", y el agente hizo `fullName` obligatorio aunque el backend lo acepta vacío (lo justificó por el ticket). Además, declaré el backend "SOLO LECTURA" y aun así lo arrancó y escribió un usuario de prueba en su base de datos.
