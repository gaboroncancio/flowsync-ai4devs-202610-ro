# Prompts

Encargo FLOW-1 lanzado una sola vez en cada copia, con el mismo texto (leído de `ticket.txt` con `claude "$(cat ../ticket.txt)"`). No hubo intervenciones posteriores en ninguna de las dos.

---

## Prompt 1 — copia CON harness (8:57)

**Modelo:** Opus 5.5
**Herramienta:** Claude Code v2.1.329

```
Registro de nuevos usuarios

Como visitante de FlowSync quiero crear una cuenta con mis datos para poder usar la plataforma.

Criterios de aceptación
1. Al abrir la página principal veo un formulario de registro.
2. Puedo registrarme indicando mi nombre, mi correo y una contraseña.
3. Si algún dato no es válido, veo un mensaje claro junto al campo que debo corregir.
4. Si el correo ya está registrado, la pantalla me lo indica.
5. Mientras se procesa mi registro no puedo enviar el formulario de nuevo.
6. Cuando el registro es exitoso, veo un mensaje de bienvenida con mi nombre y quedo dentro de la plataforma.
```

**Qué salió:** funcionó a la primera (~3 min); lint y build OK; hizo el nombre obligatorio y arrancó el backend pese a declararlo de solo lectura.

---

## Prompt 2 — copia SIN harness (8:58)

**Modelo:** Opus 5.5
**Herramienta:** Claude Code v2.1.332

```
Registro de nuevos usuarios

Como visitante de FlowSync quiero crear una cuenta con mis datos para poder usar la plataforma.

Criterios de aceptación
1. Al abrir la página principal veo un formulario de registro.
2. Puedo registrarme indicando mi nombre, mi correo y una contraseña.
3. Si algún dato no es válido, veo un mensaje claro junto al campo que debo corregir.
4. Si el correo ya está registrado, la pantalla me lo indica.
5. Mientras se procesa mi registro no puedo enviar el formulario de nuevo.
6. Cuando el registro es exitoso, veo un mensaje de bienvenida con mi nombre y quedo dentro de la plataforma.
```

**Qué salió:** funcionó a la primera (~1 min); lint y build OK; menos archivos, dejó restos de la plantilla Vite y el cierre de sesión no invalida el token.

---

## Nota sobre el harness

El `CLAUDE.md` y el hook se redactaron con apoyo de Claude (chat en claude.ai, Opus 5.5) antes de lanzar el encargo; no se lanzaron como prompts a Claude Code.
