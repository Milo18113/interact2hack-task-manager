# Revisión del PRD

**Equipo:** Juan Burgos Landazuri y Emilio Puga · **Fecha:** 23 de noviembre de 2026
**Fuentes:** docs/fuentes/descripcion-proyecto.md y docs/cliente/preguntas.md

## Huecos

| # | Sección | Frase exacta del PRD | Tipo (1–8) | Gravedad | Origen | Qué dicen las fuentes | Corrección |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 2 |Hay dos perfiles: administrador y estudiante (staff). Cada usuario tiene un solo perfil (R1). Uno de los administradores es el usuario master (R2). | 1 | media | Equipo | | No va a haber super administrador, solamente existirán los 2 roles (admin y staff). Preferiblemente, los usuarios administradores ya deben estar predefinidos y creados de antemano. |
| 1 | 2 |Hay dos perfiles: administrador y estudiante (staff). Cada usuario tiene un solo perfil (R1). Uno de los administradores es el usuario master (R2). | 1 | media | Equipo | | |
| 2 | 2 |Cada usuario tiene nombre, correo, teléfono y perfil. Entra con su correo y su contraseña. Dos usuarios no pueden tener el mismo correo. | 1 | media | IA | P-12 confirma nombre, correo y teléfono; P-02 confirma el acceso y la recuperación, pero ninguna fuente exige que el correo sea único. | Pasa a supuestos y se pregunta al cliente: ¿Debe ser obligatorio que no se repita el correo entre usuarios? |
| 3 | 6 |Solo un estudiante puede ser responsable de una tarea. Una tarea puede tener varios responsables. | 4 | alta | IA | La descripción dice «uno o varios estudiantes»; P-05 confirma la separación entre administrador y staff, pero no una restricción de un solo responsable. | Corregir la contradicción según la fuente y preguntar al cliente: ¿Confirmamos que una tarea puede tener uno o varios estudiantes responsables? |
| 4 | 6 |Una tarea completada no se puede desmarcar, editar ni reabrir; solo se puede archivar. | 1 | alta | IA | P-08 confirma que el estudiante confirma directamente; P-16 deja el historial como extra, pero ninguna fuente establece que una tarea completada sea inmutable o no pueda reabrirse. | Pasa a supuestos y se pregunta al cliente: si se completa por error, ¿un administrador puede editarla o reabrirla? |
| 5 | 6 |Una tarea No asignada, Pendiente o En ejecución a la que le faltan 2 horas o menos para vencer se marca como «próxima a vencer». | 2 | media | IA | La descripción solo menciona «tareas próximas a vencer» y P-13 habla de avisos por vencimiento o nuevas tareas; ninguna fuente fija el umbral de dos horas. | Pasa a supuestos y se pregunta al cliente: ¿Con cuánta anticipación exacta debe marcarse una tarea como próxima a vencer? |
| 6 | 6 |Un estudiante recibe un aviso dentro de la herramienta cuando se le asigna una tarea, cuando una de sus tareas pasa a «próxima a vencer» y cuando una de sus tareas vence. Los administradores no reciben avisos. | 6 | media | IA | P-13 solo dice «Dentro de la aplicación, para vencimiento o nuevas tareas»; no define destinatarios ni si el vencimiento incluye un recordatorio previo. | Pasa a supuestos y se pregunta al cliente: ¿Quién recibe cada aviso y en qué momentos: al asignar, antes de vencer, al vencer, o varios? |
| 7 | 6 |Si se elimina a un estudiante, deja de ser responsable de sus tareas no completadas; una tarea que se queda sin responsables pasa a No asignada. | 8 | alta | IA | La descripción y P-12 hablan de gestionar/eliminar usuarios, y P-15 define «No asignado», pero ninguna fuente dice qué pasa con las tareas al eliminar un estudiante. | Pasa a supuestos y se pregunta al cliente: al eliminar un estudiante, ¿se lo quita de las tareas, se bloquea la eliminación o se reasignan sus tareas? |

## Para presentar

### 1. Responsables contradictorios — gravedad alta — encontrado por IA

- **Qué decía el PRD:** «Solo un estudiante puede ser responsable de una tarea. Una tarea puede tener varios responsables.»
- **Por qué era un problema:** Las dos oraciones se contradicen y no permiten saber si una tarea puede asignarse a uno o a varios estudiantes. Esto afecta la creación, asignación y ejecución de tareas.
- **Cómo quedó:** Se identificó la contradicción y se decidió corregirla según la fuente: una tarea puede tener uno o varios estudiantes responsables. La decisión queda pendiente de confirmación del cliente.

### 2. Tarea completada inmutable — gravedad alta — encontrado por IA

- **Qué decía el PRD:** «Una tarea completada no se puede desmarcar, editar ni reabrir; solo se puede archivar.»
- **Por qué era un problema:** Ninguna fuente establece qué debe ocurrir si una tarea se completa por error. La regla puede impedir corregir información o reabrir trabajo sin terminar.
- **Cómo quedó:** Se pasó a supuesto y se llevará al cliente: debe definirse si un administrador puede editar o reabrir una tarea completada.

### 3. Eliminación de estudiantes y tareas — gravedad alta — encontrado por IA

- **Qué decía el PRD:** «Si se elimina a un estudiante, deja de ser responsable de sus tareas no completadas; una tarea que se queda sin responsables pasa a No asignada.»
- **Por qué era un problema:** Las fuentes no definen el efecto de eliminar un estudiante sobre sus tareas. La decisión puede dejar tareas sin responsable o provocar pérdida de asignaciones.
- **Cómo quedó:** Se pasó a supuesto y se llevará al cliente: debe definirse si se quita al estudiante de las tareas, se bloquea su eliminación o se reasignan sus tareas.

## Preguntas para el cliente

### Prioridad alta

1. Una tarea puede tener uno o varios estudiantes responsables, ¿confirmamos que se debe eliminar la frase «Solo un estudiante puede ser responsable de una tarea»?
2. Si una tarea se completa por error, ¿un administrador puede editarla o reabrirla? ¿Qué permisos tendría?
3. Al eliminar un estudiante, ¿se lo quita de sus tareas, se bloquea la eliminación o se reasignan sus tareas?

### Prioridad media

4. ¿Quién recibe cada aviso y en qué momentos: al asignar una tarea, antes de vencer, al vencer, o varios?
5. ¿Con cuánta anticipación exacta debe marcarse una tarea como «próxima a vencer»?
6. ¿Debe ser obligatorio que no se repita el correo entre usuarios?
7. ¿Qué puede hacer el usuario master que no pueda un administrador normal?

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
