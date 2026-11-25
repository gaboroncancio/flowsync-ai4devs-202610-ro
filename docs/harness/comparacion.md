# Comparación: con harness vs sin harness

**Ticket:** Registro de usuarios desde la web · **Modelo:** Opus 5.5 (`claude-opus-5-5`) en los dos lados · **Herramienta:** Claude Code v2.1.329
**Harness (solo copia A):** `CLAUDE.md` + hook `PostToolUse` (oxlint) + hook `Stop` (tsc) + subagente `revisor`

| Casilla | Sin harness (B) | Con harness (A) |
|---|---|---|
| **Archivos tocados** | 7: modifica `App.tsx`, `App.css`, `index.html`, `vite.config.ts`; crea `api/auth.ts`, `features/signup/SignupForm.tsx`, `features/signup/validation.ts` | 5: modifica `App.tsx`, `App.css`; crea `lib/api.ts`, `components/SignupForm.tsx`, `components/SignupForm.css` |
| **Convenciones respetadas** | No había ninguna escrita. Por su cuenta: no tocó backend, sin dependencias nuevas, sin `any` ni `console.log`, textos en español | Componentes en `components/` en PascalCase ✅ · HTTP solo en `lib/api.ts` ✅ · URL desde `VITE_API_URL` ✅ · sin `any` ni `console.log` ✅ · backend intacto ✅ · reglas leídas del validador ✅ · preguntó ante la ambigüedad ✅ · tres estados (cargando/error/éxito) ✅ |
| **Convenciones no respetadas** | No aplica (no había) | Modificó `App.css` (la regla decía CSS del componente o `index.css`) · no usó el subagente `revisor` |
| **Intervenciones** | 0 sobre el ticket: decidió sola `passwordConfirmation` (envía la contraseña dos veces) y el sentido de "alfanumérica" | 2: me preguntó por `passwordConfirmation` (elegí añadir "Confirmar contraseña") y por "alfanumérica" (elegí "al menos 1 letra y 1 número") |
| **Qué arreglaría a mano** | Confirmar el campo de confirmación: tal como está, anula la comprobación del backend. Revisar si el cambio en `vite.config.ts`/`index.html` debía entrar en el ticket. Probar en navegador | Borrar el usuario de prueba `test-ui-check@example.com` que creó en la BD local. Probar en navegador |
| **Coste / tokens** | $0.62 · 9 requests · 8.8k output | $0.60 · 11 requests · 10.3k output |

> En los dos lados el primer prompt fue un error mío (pegué un bloque de shell en vez del ticket), seguido de `/clear`. Fue simétrico y no cuenta como intervención sobre el ticket. Detalle en `prompts.md`.

## Parte B: tres líneas

1. **Piezas montadas y cuál costó más:** `CLAUDE.md` (orienta), hook `PostToolUse` con oxlint y hook `Stop` con `tsc -b` (comprueban) y subagente `revisor`. Lo que más costó fue el `CLAUDE.md`: el frontend era la plantilla vacía de Vite, así que no había convenciones que copiar y tuve que decidir cuáles poner.
2. **Primera diferencia y dónde miraba:** en la terminal, antes de que se escribiera código. La A leyó `backend/app/validators/user.ts` y me lanzó un cuestionario porque el backend exige `passwordConfirmation` y el ticket no; la B resolvió lo mismo sola, enviando la contraseña dos veces. Lo vi en el cuestionario de la A y luego en el resumen final de la B, sin abrir archivos.
3. **Algo escrito en el harness que no cumplió:** el `CLAUDE.md` dice que los estilos van en el CSS propio del componente o en `index.css`, y aun así la A modificó `App.css`. Además, el `revisor` dice "úsalo al terminar una tarea" y no lo invocó: haberlo escrito en la descripción no bastó para que lo usara.
