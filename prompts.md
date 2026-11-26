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

Borra el ejemplo de abajo cuando escribas el primero.

---

## Prompt 1

**Modelo:** Opus 5.5
**Herramienta:** Claude Code v2.1.329 (copia con harness: `CLAUDE.md` + hook de lint)

```
Implementa este ticket de Jira en el proyecto:

Título: Registro de nuevos usuarios

Descripción:
Como visitante de FlowSync quiero crear una cuenta con mis datos para poder
usar la plataforma.

Criterios de aceptación:
1. Al abrir la página principal veo un formulario de registro.
2. Puedo registrarme indicando mi nombre, mi correo y una contraseña.
3. Si algún dato no es válido, veo un mensaje claro junto al campo que debo corregir.
4. Si el correo ya está registrado, la pantalla me lo indica.
5. Mientras se procesa mi registro no puedo enviar el formulario de nuevo.
6. Cuando el registro es exitoso, veo un mensaje de bienvenida con mi nombre y quedo dentro de la plataforma.
```

**Qué salió:** Implementó el ticket en 1 min 38 s; lint y build pasan.

## Prompt 2

**Modelo:** Opus 5.5
**Herramienta:** Claude Code v2.1.329 (copia con harness: `CLAUDE.md` + hook de lint)

```
Implementa este ticket de Jira en el proyecto:

Título: Registro de nuevos usuarios

Descripción:
Como visitante de FlowSync quiero crear una cuenta con mis datos para poder
usar la plataforma.

Criterios de aceptación:
1. Al abrir la página principal veo un formulario de registro.
2. Puedo registrarme indicando mi nombre, mi correo y una contraseña.
3. Si algún dato no es válido, veo un mensaje claro junto al campo que debo corregir.
4. Si el correo ya está registrado, la pantalla me lo indica.
5. Mientras se procesa mi registro no puedo enviar el formulario de nuevo.
6. Cuando el registro es exitoso, veo un mensaje de bienvenida con mi nombre y quedo dentro de la plataforma.
```

**Qué salió:** Repetición accidental del encargo en la misma sesión; el agente dijo que ya estaba implementado y no rehízo nada.

## Prompt 3

**Modelo:** Opus 5.5
**Herramienta:** Claude Code v2.1.329 (copia sin harness)

```
Implementa este ticket de Jira en el proyecto:

Título: Registro de nuevos usuarios

Descripción:
Como visitante de FlowSync quiero crear una cuenta con mis datos para poder
usar la plataforma.

Criterios de aceptación:
1. Al abrir la página principal veo un formulario de registro.
2. Puedo registrarme indicando mi nombre, mi correo y una contraseña.
3. Si algún dato no es válido, veo un mensaje claro junto al campo que debo corregir.
4. Si el correo ya está registrado, la pantalla me lo indica.
5. Mientras se procesa mi registro no puedo enviar el formulario de nuevo.
6. Cuando el registro es exitoso, veo un mensaje de bienvenida con mi nombre y quedo dentro de la plataforma.
```

**Qué salió:** Implementó el ticket en 1 min 54 s; probó el registro contra el backend real.

