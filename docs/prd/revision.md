# Revisión del PRD

**Equipo:** Juan Burgos Landazuri y Emilio Puga · **Fecha:** 23 de noviembre de 2026
**Fuentes:** docs/fuentes/descripcion-proyecto.md y docs/cliente/preguntas.md (incluye las aclaraciones del profesor, A-xx)

## Huecos

| # | Sección | Frase exacta del PRD | Tipo (1–8) | Gravedad | Origen | Qué dicen las fuentes | Corrección |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 2 |Hay dos perfiles: administrador y estudiante (staff). Cada usuario tiene un solo perfil (R1). Uno de los administradores es el usuario master (R2). | 6 | media | Equipo | La descripción define dos perfiles (administradores y estudiantes) y P-05 confirma un solo rol por usuario. P-02 pide «crear un usuario master que tiene todos los permisos», pero ninguna fuente dice qué puede hacer el master que no pueda otro administrador. A-01 (aclaración del profesor) corrige P-02: no hay usuario master. | No va a haber super administrador, solamente existirán los 2 roles (admin y staff). Preferiblemente, los usuarios administradores ya deben estar predefinidos y creados de antemano. **Aplicado (A-01):** se elimina el master de R1, R2 y la sección 2; S-01 pasa a cubrir solo si un administrador gestiona a otros administradores. |
| 2 | 2 |Cada usuario tiene nombre, correo, teléfono y perfil. Entra con su correo y su contraseña. Dos usuarios no pueden tener el mismo correo. | 1 | media | IA | P-12 confirma nombre, correo y teléfono; P-02 confirma el acceso y la recuperación, pero ninguna fuente exige que el correo sea único. | Pasa a supuestos y se pregunta al cliente: ¿Debe ser obligatorio que no se repita el correo entre usuarios? **Aplicado:** R4 lleva `[SUPUESTO S-19]` y S-19 está en la sección 8. |
| 3 | 6 |Solo un estudiante puede ser responsable de una tarea. Una tarea puede tener varios responsables. | 4 | alta | IA | La descripción dice «uno o varios estudiantes»; P-05 confirma la separación entre administrador y staff, pero no una restricción de un solo responsable. | Corregir la contradicción según la fuente y preguntar al cliente: ¿Confirmamos que una tarea puede tener uno o varios estudiantes responsables? **Aplicado:** R7 dice ahora «Solo los estudiantes pueden ser responsables de una tarea, y una tarea puede tener uno o varios responsables». |
| 4 | 6 |Una tarea completada no se puede desmarcar, editar ni reabrir; solo se puede archivar `[SUPUESTO S-08]`. | 6 | alta | IA | P-08 confirma que el estudiante confirma directamente; P-16 deja el historial como extra, pero ninguna fuente establece que una tarea completada sea inmutable o no pueda reabrirse. La sección 2 tampoco dice qué puede hacer un administrador con una tarea completada. | El equipo definió el permiso del administrador: puede reagendar una tarea completada o vencida, conservando el avance y la confirmación. **Aplicado:** R14 reescrita y S-08 actualizado; se pregunta al cliente si basta con reagendar o necesita reabrirla. |
| 5 | 6 |Una tarea No asignada, Pendiente o En ejecución a la que le faltan 2 horas o menos para vencer se marca como «próxima a vencer». Es una marca, no un estado `[SUPUESTO S-09]`. | 2 | media | IA | La descripción solo menciona «tareas próximas a vencer» y P-13 habla de avisos por vencimiento o nuevas tareas; ninguna fuente fija el umbral de dos horas. | Se mantiene como supuesto S-09 y el equipo ajustó la cifra a 30 minutos. **Aplicado:** R16 y S-09 dicen 30 minutos; se pregunta al cliente si confirma ese umbral. |
| 6 | 6 |Un estudiante recibe un aviso dentro de la herramienta cuando se le asigna una tarea, cuando una de sus tareas pasa a «próxima a vencer» y cuando una de sus tareas vence. Los administradores no reciben avisos `[SUPUESTO S-15]`. | 6 | media | IA | P-13 solo dice «Dentro de la aplicación, para vencimiento o nuevas tareas»; no define destinatarios ni si el vencimiento incluye un recordatorio previo. | Se mantiene como supuesto S-15 y se pregunta al cliente: ¿Quién recibe cada aviso y en qué momentos: al asignar, antes de vencer, al vencer, o varios? **Aplicado:** R23 reescrita por el equipo; vuelve a citar S-15 en la regla y en la trazabilidad. |
| 7 | 6 |Si se elimina a un estudiante, deja de ser responsable de sus tareas no completadas; una tarea que se queda sin responsables pasa a No asignada. En las tareas completadas se conserva su nombre como quien la confirmó `[SUPUESTO S-16]`. | 6 | alta | IA | La descripción y P-12 hablan de gestionar/eliminar usuarios, y P-15 define «No asignado», pero ninguna fuente dice qué pasa con las tareas al eliminar un estudiante. La sección 2 le permite al administrador eliminar estudiantes sin decir si puede hacerlo cuando tienen tareas activas. | El equipo definió la baja: se deshabilita la cuenta y se retira al estudiante de todas sus tareas, conservando quién confirmó cada una. **Aplicado:** R24 reescrita y S-16 actualizado; se pregunta al cliente si prefiere bloquear la baja o reasignar las tareas. |

**Avance:** los huecos 1, 2, 3, 4 y 7 cambiaron reglas del PRD (R1, R2, R4, R7, R14 y R24); en 5 el equipo fijó el umbral en 30 minutos; en 6 se reescribió R23 y se mantiene S-15. Quedan pendientes de confirmación del cliente los huecos 2 a 7 (preguntas abajo); el 1 ya está resuelto por A-01.

## Para presentar

### 1. Responsables contradictorios — gravedad alta — encontrado por IA

- **Qué decía el PRD:** «Solo un estudiante puede ser responsable de una tarea. Una tarea puede tener varios responsables.»
- **Por qué era un problema:** Las dos oraciones se contradicen y no permiten saber si una tarea puede asignarse a uno o a varios estudiantes. Esto afecta la creación, asignación y ejecución de tareas.
- **Cómo quedó:** Se corrigió R7 según la fuente: «Solo los estudiantes pueden ser responsables de una tarea, y una tarea puede tener uno o varios responsables». Se mantiene que un administrador no puede ser responsable. Queda pendiente de confirmación del cliente.

### 2. Permisos sobre una tarea completada — gravedad alta — encontrado por IA

- **Qué decía el PRD:** «Una tarea completada no se puede desmarcar, editar ni reabrir; solo se puede archivar `[SUPUESTO S-08]`.»
- **Por qué era un problema:** Estaba marcado como supuesto, pero deja incompleto el perfil del administrador: ninguna fuente ni la sección 2 dicen qué puede hacer con una tarea completada por error. La regla puede impedir corregir información o reabrir trabajo sin terminar.
- **Cómo quedó:** El equipo reescribió R14: un administrador puede reagendar una tarea completada o vencida con una nueva fecha y hora, sin perder el avance ni la confirmación. S-08 se actualizó y se lleva al cliente: ¿basta con reagendar o necesita reabrirla?

### 3. Eliminación de estudiantes y tareas — gravedad alta — encontrado por IA

- **Qué decía el PRD:** «Si se elimina a un estudiante, deja de ser responsable de sus tareas no completadas; una tarea que se queda sin responsables pasa a No asignada. […] `[SUPUESTO S-16]`.»
- **Por qué era un problema:** Estaba marcado como supuesto, pero deja incompleto el permiso del administrador para eliminar estudiantes: las fuentes no dicen si puede eliminar a uno con tareas activas ni qué pasa con ellas. La decisión puede dejar tareas sin responsable o provocar pérdida de asignaciones.
- **Cómo quedó:** El equipo reescribió R24: dar de baja a un estudiante deshabilita su cuenta y lo retira de todas sus tareas, conservando quién confirmó cada una. S-16 se actualizó y se lleva al cliente: ¿prefiere bloquear la baja o reasignar las tareas?

## Preguntas para el cliente

### Prioridad alta

1. ¿Confirmamos que una tarea puede tener uno o varios estudiantes responsables, y que un administrador no puede ser responsable?
2. Si una tarea se completa por error o vence, ¿basta con que un administrador la reagende con una nueva fecha y hora, o necesita reabrirla?
3. Al dar de baja a un estudiante lo retiramos de todas sus tareas y deshabilitamos su cuenta. ¿Está bien, o prefieren bloquear la baja o reasignar sus tareas?

### Prioridad media

4. ¿Quién recibe cada aviso y en qué momentos: al asignar una tarea, antes de vencer, al vencer, o varios?
5. ¿Confirmamos que una tarea se marca como «próxima a vencer» cuando faltan 30 minutos o menos?
6. ¿Debe ser obligatorio que no se repita el correo entre usuarios?
7. Los administradores vienen creados de antemano (A-01). ¿Un administrador puede crear, editar o eliminar a otros administradores desde la herramienta, o esa lista es fija?

---

## Lista de control (referencia, de la guía)

| # | Tipo de hueco | Pregunta para encontrarlo |
| --- | --- | --- |
| 1 | Supuesto escrito como hecho | ¿En qué respuesta del cliente o en qué parte de la descripción lo dice? Si no lo encuentras, es un supuesto. |
| 2 | Regla vaga o sin cifra | ¿Dice «rápido», «pronto», «próximas a vencer» o «fácil» sin un número o un criterio comprobable? |
| 3 | Alcance inflado | ¿Esto cabe en el avance funcional del 2 de diciembre, o es un «sería lindo»? |
| 4 | Contradicción resuelta en silencio | ¿La descripción y las respuestas del cliente dicen cosas distintas, y el PRD eligió una sin decirlo? |
| 5 | Pregunta abierta desaparecida | ¿Una pregunta que quedó sin respuesta en el avance 1 dejó de aparecer en el PRD? |
| 6 | Perfil o permiso incompleto | ¿Está claro qué puede y qué no puede hacer cada perfil, administrador y estudiante? |
| 7 | Detalle técnico | ¿Habla de tablas, endpoints, componentes o librerías? En un PRD sobra. |
| 8 | Regla sin trazabilidad | ¿La regla aparece en la tabla de trazabilidad con su pregunta P-xx o su supuesto? |
