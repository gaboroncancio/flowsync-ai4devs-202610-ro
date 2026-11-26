# Comparación con y sin harness

Encargo: ticket FLOW-1 "Registro de nuevos usuarios" (mismo texto en ambas copias, ver prompts.md).
Herramienta y modelo: Claude Code v2.1.329, Opus 5.5, auto mode en ambas.

| | Con harness | Sin harness |
|---|---|---|
| Archivos tocados | 8 (3 modificados, 5 nuevos) | 9 (5 modificados, 4 nuevos) |
| Líneas en archivos nuevos | 370 (5 archivos) | 305 (4 archivos) |
| Intervenciones | 1 (repetí el encargo por error a las 6:12; no cambió el código) | 0 |
| Lo que habría que arreglar a mano | Restaurar la sesión al recargar la página (el token se guarda pero vuelve a salir el formulario; el agente lo advirtió), probar el flujo contra el backend real (no se hizo) y sacar la URL de la API de `src/api/auth.ts` | Decidir si queda el botón «Cerrar sesión», que el ticket no pedía; borrar el usuario de prueba que dejó en la BD de desarrollo (`probe23581@example.com`); y revisar el cambio en `vite.config.ts`, que el ticket no mencionaba |

## Convenciones del proyecto

| Convención (CLAUDE.md) | Con harness | Sin harness (no había reglas escritas) |
|---|---|---|
| No tocar `backend/` | Sin cambios en git | Sin cambios en git; el agente reportó un usuario de prueba en la BD de desarrollo |
| No añadir dependencias | Sin cambios en `package.json` | Sin cambios en `package.json` |
| Leer validadores antes de asumir reglas | Sí, según el agente | Sí, según el agente |
| Un componente por archivo en `src/components/` | Sí (1 por archivo) | Sí (1 componente por archivo) |
| TypeScript sin `any` | Sin usos | Sin usos |
| Textos en español | Sí, en los textos de los componentes que revisé | Sí, en los textos de los componentes que revisé |
| Lint y build antes de terminar | Hoy pasan (lo verifiqué); el agente dice haberlos corrido | Hoy pasan (lo verifiqué); el agente dice haberlos corrido |
| Listar archivos creados o modificados | Sí | Sí |

## Parte B
1. Piezas que monté y cuál me costó más: Monté dos piezas: un `CLAUDE.md` en la raíz (alcance, qué leer antes de implementar, reglas del frontend y de cierre) y un hook `PostToolUse` que corre `npm run lint` tras cada edición. Lo que más me costó no fue una pieza sino arrancar: autenticar Claude Code en WSL (el login por URL y código me tomó varios intentos).
2. Primera diferencia que vi entre las dos salidas, y dónde estaba mirando: Lo primero que noté fue en el resumen final de cada agente en la terminal, sin abrir archivos: la copia sin harness levantó el backend y probó el registro contra la API real (y dejó un usuario de prueba), mientras que la copia con harness dijo que no pudo probarlo porque el backend no estaba encendido. Después, con `git status` y `wc -l`, vi que la copia con harness repartió el código en más archivos (8 contra 9 en total, pero con `FormField` y `validation/signup.ts` por separado).
3. Algo que dejé escrito en el harness y el agente no cumplió: Con lo que pude comprobar no encontré ninguna regla escrita que el agente incumpliera: `backend/` y dependencias sin cambios, sin `any`, un componente por archivo, textos en español, lint y build pasan. No pude comprobar si el hook de lint se disparó ni si leyó el controlador y el transformer antes de escribir (de su resumen solo consta el validador). Además, la regla «TypeScript estricto» la escribí sin comprobarla contra el `tsconfig`, y al comprobarlo después ningún `tsconfig` del frontend contiene `strict`, así que esa regla no describía la configuración real del proyecto (es un fallo de mi harness, no del agente).
