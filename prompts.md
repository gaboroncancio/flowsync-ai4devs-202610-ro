# Prompts

Todos los prompts lanzados en el ejercicio, en orden y tal cual, extraídos del historial de sesiones de Claude Code (`~/.claude/projects/`).

**Modelo:** Opus 5.5 (`claude-opus-5-5`) en las dos copias · **Herramienta:** Claude Code v2.1.329 en WSL

---

## Copia A: con harness (`flowsync-ai4devs-202610-ro`)

### Prompt 1: ERRÓNEO (16:23 UTC)

**Modelo:** Opus 5.5 · **Herramienta:** Claude Code

Pegué en Claude el bloque de shell que preparaba el ticket, en vez del texto del ticket.

```
cd /home/vivianag/curso/mod-1 && cat > prompt-ticket.txt <<'EOF'
Implementa este ticket:

Registro de usuarios desde la web

Como visitante de FlowSync quiero poder crear una cuenta desde la web para empezar a usar la aplicación.

Criterios de aceptación:
- Al abrir la aplicación hay una pantalla de registro.
- La pantalla de registro contiene los campos "Correo electrónico", "Contraseña"
- El correo electrónico debe tener la estructura correcta y se debe validar que no se encuentre ya registrado en el sistema
- La contraseña debe ser igual o mayor a 8 dígitos y debe ser alfanumérica
- El usuario introduce sus datos y pulsa "Crear cuenta".
- Si algún dato no es válido, el usuario ve qué tiene que corregir antes de enviarlo.
- Si el registro funciona, ve un mensaje de confirmación.
- Si el servidor rechaza el registro (por ejemplo, el email ya existe), ve un mensaje claro de qué pasó.
EOF
for d in flowsync-ai4devs-202610-ro flowsync-sin-harness; do (cd $d && git status --short > /tmp/antes-$d.txt); done && echo "=== foto inicial guardada ===" && cat /tmp/antes-*.txt && echo "=== prompt ===" && cat prompt-ticket.txt
```

**Qué salió:** ejecutó los comandos y no implementó nada. Después hice `/clear` para empezar con el contexto limpio.

### Prompt 2: el ticket (16:26 UTC, después de `/clear`)

**Modelo:** Opus 5.5 · **Herramienta:** Claude Code

```
Implementa este ticket:

Registro de usuarios desde la web

Como visitante de FlowSync quiero poder crear una cuenta desde la web para empezar a usar la aplicación.

Criterios de aceptación:
- Al abrir la aplicación hay una pantalla de registro.
- La pantalla de registro contiene los campos "Correo electrónico", "Contraseña"
- El correo electrónico debe tener la estructura correcta y se debe validar que no se encuentre ya registrado en el sistema
- La contraseña debe ser igual o mayor a 8 dígitos y debe ser alfanumérica
- El usuario introduce sus datos y pulsa "Crear cuenta".
- Si algún dato no es válido, el usuario ve qué tiene que corregir antes de enviarlo.
- Si el registro funciona, ve un mensaje de confirmación.
- Si el servidor rechaza el registro (por ejemplo, el email ya existe), ve un mensaje claro de qué pasó.
```

**Qué salió:** leyó `backend/app/validators/user.ts` y, antes de implementar, me hizo dos preguntas con opciones.

### Prompt 3: respuestas al cuestionario del agente

**Modelo:** Opus 5.5 · **Herramienta:** Claude Code

```
P: El backend exige un campo `passwordConfirmation` que debe ser igual a `password`, pero el ticket solo pide "Correo electrónico" y "Contraseña". ¿Cómo lo resuelvo?
R: 1. Añadir campo "Confirmar contraseña" (Recomendado)

P: El ticket dice que la contraseña debe ser "alfanumérica", pero el backend no tiene esa regla (solo mínimo 8 y máximo 32 caracteres). ¿Qué significa "alfanumérica" aquí?
R: 1. Al menos 1 letra y 1 número (Recomendado)
```

**Qué salió:** implementó el ticket. Lint y tsc limpios. Probado con curl, no en el navegador.

---

## Copia B: sin harness (`flowsync-sin-harness`)

### Prompt 1: ERRÓNEO (16:23 UTC)

**Modelo:** Opus 5.5 · **Herramienta:** Claude Code

El mismo error que en la A: pegué el bloque de shell en vez del ticket.

```
cd /home/vivianag/curso/mod-1 && cat > prompt-ticket.txt <<'EOF'
Implementa este ticket:

Registro de usuarios desde la web

Como visitante de FlowSync quiero poder crear una cuenta desde la web para empezar a usar la aplicación.

Criterios de aceptación:
- Al abrir la aplicación hay una pantalla de registro.
- La pantalla de registro contiene los campos "Correo electrónico", "Contraseña"
- El correo electrónico debe tener la estructura correcta y se debe validar que no se encuentre ya registrado en el sistema
- La contraseña debe ser igual o mayor a 8 dígitos y debe ser alfanumérica
- El usuario introduce sus datos y pulsa "Crear cuenta".
- Si algún dato no es válido, el usuario ve qué tiene que corregir antes de enviarlo.
- Si el registro funciona, ve un mensaje de confirmación.
- Si el servidor rechaza el registro (por ejemplo, el email ya existe), ve un mensaje claro de qué pasó.
EOF
for d in flowsync-ai4devs-202610-ro flowsync-sin-harness; do (cd $d && git status --short > /tmp/antes-$d.txt); done && echo "=== foto inicial guardada ===" && cat /tmp/antes-*.txt && echo "=== prompt ===" && cat prompt-ticket.txt
```

**Qué salió:** ejecutó los comandos y no implementó nada. Después hice `/clear`.

### Prompt 2: el ticket (16:26 UTC, después de `/clear`)

**Modelo:** Opus 5.5 · **Herramienta:** Claude Code

```
Implementa este ticket:

Registro de usuarios desde la web

Como visitante de FlowSync quiero poder crear una cuenta desde la web para empezar a usar la aplicación.

Criterios de aceptación:
- Al abrir la aplicación hay una pantalla de registro.
- La pantalla de registro contiene los campos "Correo electrónico", "Contraseña"
- El correo electrónico debe tener la estructura correcta y se debe validar que no se encuentre ya registrado en el sistema
- La contraseña debe ser igual o mayor a 8 dígitos y debe ser alfanumérica
- El usuario introduce sus datos y pulsa "Crear cuenta".
- Si algún dato no es válido, el usuario ve qué tiene que corregir antes de enviarlo.
- Si el registro funciona, ve un mensaje de confirmación.
- Si el servidor rechaza el registro (por ejemplo, el email ya existe), ve un mensaje claro de qué pasó.
```

**Qué salió:** implementó sin hacer ninguna pregunta. Resolvió `passwordConfirmation` enviando la contraseña dos veces e interpretó "alfanumérica" por su cuenta.
