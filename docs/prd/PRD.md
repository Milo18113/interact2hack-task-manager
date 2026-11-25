# PRD · Organización del staff del Interact2Hack

**Versión:** 0.1 (borrador) · **Fecha:** 23 de noviembre de 2026 · **Equipo:** Juan Burgos Landazuri y Emilio Puga
**Fuentes:** descripción del proyecto final (`docs/fuentes/descripcion-proyecto.md`) y respuestas del cliente del 11 de noviembre y aclaraciones del profesor (A-xx) (`docs/cliente/preguntas.md`).

Este documento describe **qué** debe hacer la herramienta y **qué no**. No describe cómo se construye: las tecnologías, los datos y las pantallas se deciden en las specs, y cómo se ve se define en `DESIGN.md`.

## 1. Problema y contexto

Durante el evento Interact2Hack 2027, el staff tiene que saber qué hacer, dónde y hasta cuándo. Los administradores, por su parte, tienen que saber en cualquier momento qué tareas ya se cumplieron, cuáles están en curso y cuáles se atrasaron.

La herramienta convierte cada tarea en un checklist paso a paso, con fecha y hora de vencimiento, lugar y uno o varios responsables. Una tarea queda ejecutada cuando todos sus pasos están marcados y un responsable confirma su ejecución.

Los administradores crean y asignan las tareas y siguen su cumplimiento en el tablero, desde una computadora. Los estudiantes del staff consultan sus tareas y las completan desde el celular, donde estén en ese momento `[SUPUESTO S-18]`.


## 2. Usuarios y perfiles

Hay dos perfiles: **administrador** y **estudiante (staff)**. Cada usuario tiene un solo perfil (R1). No hay usuario master: los administradores vienen creados de antemano (R2).

| Perfil | Puede | No puede |
| --- | --- | --- |
| **Administrador** | Crear, ver, editar y eliminar estudiantes. Crear, ver, editar, archivar y asignar tareas. Ver el detalle de cualquier tarea, con su checklist y sus observaciones. Ver el tablero de cumplimiento. Cambiar su propia contraseña. | Crear, editar ni eliminar administradores `[SUPUESTO S-01]`. Ser responsable de una tarea, marcar pasos o confirmar una tarea. |
| **Estudiante (staff)** | Ver la lista de sus tareas, pendientes y completadas. Entrar al detalle de una tarea suya. Marcar los pasos del checklist, escribir observaciones, guardar su avance y confirmar la ejecución. Ver sus avisos. Cambiar su propia contraseña. | Ver tareas en las que no es responsable. Ver el tablero. Crear, editar, asignar ni archivar tareas. Gestionar usuarios. Editar su nombre, correo o teléfono `[SUPUESTO S-17]`. |

Todos entran con su correo y su contraseña. No hay registro: los administradores vienen creados de antemano y a los estudiantes los crea un administrador (R2, R3).

## 3. Objetivos y éxito

| Objetivo | Cómo sabrá el cliente que se cumplió |
| --- | --- |
| Que cada miembro del staff sepa qué hacer, dónde y hasta cuándo | Un estudiante abre la herramienta y ve sus tareas con el lugar y la fecha y hora de vencimiento, sin preguntarle a nadie. |
| Que los administradores conozcan el estado de todas las tareas sin preguntar | En el tablero ven primero lo vencido y lo que está en ejecución, con los responsables, el lugar y el vencimiento de cada tarea. |
| Que una tarea solo cuente como hecha si se hizo completa | Ninguna tarea aparece como completada con pasos sin marcar (R11). |
| Que las tareas se cumplan a tiempo | Al cerrar el evento, el tablero muestra cuántas tareas se completaron y cuántas siguen vencidas. El cliente no definió una meta numérica (ver puntos abiertos). |

## 4. Alcance (MoSCoW)

| Prioridad | Funcionalidad |
| --- | --- |
| **Must** | Inicio de sesión con los dos perfiles, con los administradores creados de antemano. Gestión de estudiantes por los administradores. Cambio de contraseña por el propio usuario y recuperación por correo. Crear, editar, archivar y asignar tareas con fecha y hora de vencimiento, lugar, checklist y responsables. Lista de tareas del estudiante, con pendientes y completadas. Detalle de la tarea con el checklist compartido, observaciones, guardar avance y confirmar la ejecución. Estados y vencimiento de las tareas según las reglas R8 a R16. Tablero de cumplimiento para administradores (R19 a R22). Identidad visual del Interact2Hack. |
| **Should** | Avisos dentro de la herramienta: tarea nueva asignada, tarea próxima a vencer y tarea vencida (R23). |
| **Could** | Historial de cambios de cada tarea con sus fechas (P-16: «Extra si se puede»). Adjuntar evidencias al completar una tarea (P-18: «buen extra»). |
| **Won't (esta versión)** | Categorías de tareas. Aprobación del administrador para cerrar una tarea. Un checklist por responsable. Notificaciones por correo, mensajería o push. Usuarios con más de un perfil. Usuario master o super administrador. |

Los avisos los pidió el cliente (P-13). Van en Should porque la herramienta cumple su objetivo sin ellos: el estudiante ve sus tareas y sus estados en su lista. Se construyen después del flujo principal.

## 5. No-alcance

- Categorías de tareas («categorías no son relevantes»).
- Aprobación de un administrador para cerrar una tarea (P-08).
- Un checklist por responsable: todos comparten uno (P-07).
- Notificaciones fuera de la herramienta: correo, mensajería o push (P-13). El único correo que envía la herramienta es el de recuperación de contraseña (P-02).
- Borrar tareas para siempre: se archivan (P-17).
- Ver o restaurar tareas archivadas `[SUPUESTO S-10]`.
- Reabrir una tarea completada `[SUPUESTO S-08]`.
- Registro de usuarios por su cuenta.
- Usuarios con más de un perfil (P-05).
- Usuario master o super administrador (A-01).
- Uso sin conexión a internet `[SUPUESTO S-18]`.

## 6. Reglas de negocio

| Id | Regla |
| --- | --- |
| R1 | Hay dos perfiles: **administrador** y **estudiante (staff)**. Cada usuario tiene un solo perfil. |
| R2 | **No hay usuario master.** Los administradores vienen **creados de antemano**. Desde la herramienta, un administrador no crea, edita ni elimina a otros administradores `[SUPUESTO S-01]`. |
| R3 | No hay registro. Solo un administrador crea estudiantes y, al crearlos, les asigna una contraseña inicial. |
| R4 | Cada usuario tiene **nombre, correo, teléfono** y perfil. Entra con su correo y su contraseña. Dos usuarios no pueden tener el mismo correo `[SUPUESTO S-19]`. |
| R5 | Cada usuario puede cambiar su contraseña cuando quiera. Si la olvida, la restablece con un enlace que recibe en su correo. |
| R6 | Una tarea tiene **título, fecha y hora de vencimiento, lugar o aula, checklist** y **cero, uno o varios responsables**. Son obligatorios el título, la fecha y hora, el lugar y al menos un paso en el checklist `[SUPUESTO S-02]`. Las tareas no tienen categorías. |
| R7 | Solo los **estudiantes** pueden ser responsables de una tarea, y una tarea puede tener **uno o varios** responsables. |
| R8 | Una tarea está en uno de cinco estados: **No asignada**, **Pendiente**, **En ejecución**, **Completada** o **Vencida**. |
| R9 | El estado se decide con la primera condición que se cumpla, en este orden `[SUPUESTO S-03]`: 1) **Completada**: un responsable confirmó su ejecución. 2) **Vencida**: pasó su fecha y hora de vencimiento sin confirmarse. 3) **No asignada**: no tiene responsables. 4) **En ejecución**: tiene al menos un paso marcado y guardado. 5) **Pendiente**: tiene responsables y ningún paso marcado. |
| R10 | Todos los responsables de una tarea trabajan sobre **el mismo checklist**: un paso que marca uno queda marcado para todos. |
| R11 | Una tarea solo se puede confirmar con **todos sus pasos marcados**. La confirma cualquiera de sus responsables, sin aprobación de un administrador, y queda completada para todos. Se registra quién la confirmó y cuándo `[SUPUESTO S-05]`. |
| R12 | Un responsable puede **guardar** los pasos marcados y las observaciones sin confirmar la tarea. Si guarda con todos los pasos marcados, la herramienta le pregunta si quiere confirmar la ejecución `[SUPUESTO S-04]`. |
| R13 | Las **observaciones son opcionales** y no impiden confirmar una tarea. Hay un solo campo de observaciones por tarea, compartido por sus responsables `[SUPUESTO S-06]`. |
| R14 | Una tarea completada no se puede desmarcar, editar ni reabrir; solo se puede archivar `[SUPUESTO S-08]`. |
| R15 | Una tarea **vencida no desaparece**: se muestra con prioridad alta y sus responsables todavía la pueden completar `[SUPUESTO S-07]`. Al confirmarla pasa a Completada. |
| R16 | El tablero muestra la marca **«próxima a vencer»** en las tareas No asignadas, Pendientes o En ejecución que estén dentro del umbral previo al vencimiento. El umbral queda por confirmar (S-09). |
| R17 | **Eliminar una tarea la archiva**: deja de verse en el tablero y en las listas de los estudiantes, y su información se conserva. Una tarea archivada no se puede restaurar en esta versión `[SUPUESTO S-10]`. |
| R18 | Un estudiante solo ve las tareas no archivadas en las que es responsable, pendientes y completadas, separadas por estado y en el mismo orden que el tablero `[SUPUESTO S-13]`. En cada tarea suya ve también a los demás responsables. |
| R19 | **Solo los administradores ven el tablero.** Muestra todas las tareas no archivadas como tarjetas, separadas por estado en este orden: **Vencidas, En ejecución, Pendientes, No asignadas, Completadas** `[SUPUESTO S-11]`. |
| R20 | Dentro de cada sección del tablero va primero la tarea cuya fecha y hora de vencimiento está **más cerca del momento actual** `[SUPUESTO S-12]`. |
| R21 | Cada tarjeta del tablero muestra el **estado, título, responsables, lugar y fecha y hora de vencimiento**, la marca «próxima a vencer» cuando aplica y el avance del checklist, por ejemplo «2 de 5 pasos» `[SUPUESTO S-14]`. |
| R22 | Sobre las tarjetas, el tablero muestra un resumen con **cuántas tareas hay en cada estado** `[SUPUESTO S-14]`. |
| R23 | Cada estudiante recibe un **aviso dentro de la aplicación** cuando se le asigna una nueva tarea, cuando una tarea a su cargo pasa a **«próxima a vencer»** (R16) y cuando una tarea a su cargo vence. |
| R24 | Al dar de baja a un estudiante, el administrador deshabilita su cuenta y el estudiante pierde el acceso a la herramienta. Se lo retira de la lista de responsables de todas sus tareas, incluidas las completadas y archivadas. Se aplican las condiciones de estado de R9 y se conserva el registro de confirmación de R11. |

## 7. Épicas

| Id | Épica | Descripción | Prioridad |
| --- | --- | --- | --- |
| E1 | Acceso y usuarios | Inicio de sesión con correo y contraseña, sin registro. Los administradores vienen creados de antemano y gestionan a los estudiantes; cada usuario puede cambiar y recuperar su contraseña (R1 a R5, R24). | Must |
| E2 | Gestión de tareas | El administrador crea, edita, asigna y archiva tareas con su fecha y hora de vencimiento, lugar, checklist y responsables (R6, R7, R17). | Must |
| E3 | Ejecución de tareas | El estudiante ve sus tareas, entra al detalle, marca los pasos del checklist compartido, escribe observaciones, guarda su avance y confirma la ejecución. Los estados y el vencimiento se actualizan solos (R8 a R16, R18). | Must |
| E4 | Tablero de cumplimiento | Los administradores ven todas las tareas separadas por estado, con lo vencido primero, y un resumen de cuántas hay en cada estado (R19 a R22). | Must |
| E5 | Avisos | El staff recibe avisos dentro de la aplicación por nuevas asignaciones, tareas próximas a vencer y tareas vencidas (R23). | Should |
| E6 | Historial y evidencias | Registro de los cambios de cada tarea con sus fechas, y adjuntos como evidencia al completarla (P-16, P-18). | Could |

## 8. Supuestos y puntos abiertos

| Id | Supuesto | Por qué lo decidimos así | Pregunta para el cliente | Estado |
| --- | --- | --- | --- | --- |
| S-01 | Un administrador no crea, edita ni elimina a otros administradores desde la herramienta (R2). | A-01 elimina el usuario master que pedía P-02 y dice que los administradores vienen creados de antemano, pero no si un administrador puede gestionar a otros. Lo limitamos para que ningún administrador pueda dejar al sistema sin administradores. | ¿Un administrador puede crear, editar o eliminar a otros administradores desde la herramienta, o esa lista es fija? | `[SUPUESTO]` · validar en el Avance 3 |
| S-02 | Título, fecha y hora, lugar y al menos un paso son obligatorios; los responsables no (R6). | Una tarea sin pasos no se puede completar (P-06), y existe el estado «No asignado» (P-15), así que se puede crear sin responsables. | ¿Hay algún dato de la tarea que pueda quedar vacío? | `[SUPUESTO]` · validar en el Avance 3 |
| S-03 | El orden de condiciones que decide el estado (R9). | El cliente nombró los cinco estados (P-15) pero no cuándo se pasa de uno a otro. | ¿Una tarea pasa a «En ejecución» cuando se marca el primer paso, o cuando el estudiante indica que empezó? | `[SUPUESTO]` · validar en el Avance 3 |
| S-04 | Guardar con todos los pasos marcados pregunta si se confirma la ejecución (R12). | La descripción tiene un solo botón de guardar, y la confirmación no se puede deshacer (S-08). | ¿Guardar con todo marcado debe completar la tarea, o completar es una acción aparte? | `[SUPUESTO]` · validar en el Avance 3 |
| S-05 | Se registra quién confirmó la tarea y cuándo (R11). | Con un checklist compartido (P-07), el administrador necesita saber quién la cerró. El historial completo de cambios es un extra (P-16). | ¿Necesitan ver quién completó cada tarea? | `[SUPUESTO]` · validar en el Avance 3 |
| S-06 | Un solo campo de observaciones por tarea, compartido (R13). | El checklist es uno solo para todos (P-07); seguimos la misma lógica. | ¿Cada responsable escribe sus propias observaciones o son unas solas para la tarea? | `[SUPUESTO]` · validar en el Avance 3 |
| S-07 | Una tarea vencida se puede seguir completando (R15). | El cliente dijo que «no desaparece» (P-14), pero no si se puede completar. Bloquearla impediría terminar trabajo atrasado. | ¿Una tarea vencida se puede completar? ¿Debe quedar marcada como completada con retraso? | `[SUPUESTO]` · validar en el Avance 3 |
| S-08 | Una tarea completada no se edita ni se reabre (R14). | El cliente no lo dijo. Sin esta regla, un cambio después de completarla cambiaría lo que el estudiante confirmó. | Si una tarea se completa por error, ¿un administrador puede editarla o reabrirla? | `[SUPUESTO]` · validar en el Avance 3 |
| S-09 | «Próxima a vencer» = faltan 2 horas o menos (R16). | La descripción habla de «tareas próximas a vencer» sin una cifra. El evento dura tres días y las tareas se miden en horas. | ¿Con cuánta anticipación una tarea debe considerarse próxima a vencer? | `[SUPUESTO]` · validar en el Avance 3 |
| S-10 | Las tareas archivadas no las ve nadie y no se restauran (R17). | El cliente dijo «Que se archive nomas, no sea visible» (P-17), sin decir si alguien las consulta después. | ¿Un administrador necesita ver o recuperar las tareas archivadas? | `[SUPUESTO]` · validar en el Avance 3 |
| S-11 | El tablero muestra todas las tareas no archivadas, y las Pendientes van después de En ejecución (R19). | El cliente dijo «las n tareas» y el orden «vencidas, … en ejecución, sin asignar, completadas» (P-04), sin mencionar las pendientes ni el valor de «n». | ¿El tablero muestra todas las tareas o un número fijo? ¿Dónde van las pendientes? | `[SUPUESTO]` · validar en el Avance 3 |
| S-12 | Dentro de cada sección va primero lo más cercano al momento actual (R20). | El cliente dijo «más reciente a antiguo» (P-04, clave). Para una vencida, la más reciente es la que venció hace menos; para una futura, la que vence antes. | ¿Las tareas que vencen antes van primero? | `[SUPUESTO]` · validar en el Avance 3 |
| S-13 | La lista del estudiante usa las mismas secciones y el mismo orden que el tablero (R18). | El cliente solo describió el orden del tablero. Usar el mismo evita dos lógicas distintas. | ¿La lista del estudiante debe ordenarse igual que el tablero? | `[SUPUESTO]` · validar en el Avance 3 |
| S-14 | El tablero muestra el avance del checklist en cada tarjeta y un resumen con la cantidad de tareas por estado (R21, R22). | La descripción dice que el tablero «es un resumen general del estado de las tareas», pero el cliente no dijo qué cifras lleva (P-09). | ¿Qué cifras quieren ver en el resumen del tablero? | `[SUPUESTO]` · validar en el Avance 3 |
| S-15 | Los avisos son para los responsables: tarea asignada, próxima a vencer y vencida. Los administradores no reciben avisos (R23). | El cliente dijo «para vencimiento o nuevas tareas» (P-13), sin decir para quién ni en qué momento del vencimiento. | ¿Los administradores también deben recibir avisos? ¿El aviso de vencimiento es antes, al vencer o ambos? | `[SUPUESTO]` · validar en el Avance 3 |
| S-16 | Al eliminar a un estudiante se lo quita de sus tareas no completadas (R24). | La descripción permite eliminar usuarios, pero no dice qué pasa con sus tareas. | Al eliminar un estudiante, ¿se lo quita de sus tareas, se bloquea la eliminación o se reasignan sus tareas? | `[SUPUESTO]` · validar en el Avance 3 |
| S-17 | El estudiante no edita su nombre, correo ni teléfono; solo su contraseña (sección 2). | El cliente solo habló de que el usuario cambie su contraseña (P-10). | ¿El estudiante puede editar sus propios datos? | `[SUPUESTO]` · validar en el Avance 3 |
| S-18 | Los administradores usan una computadora y los estudiantes el celular, con conexión a internet durante el evento (sección 1). | Así lo plantean las instrucciones del Avance 2; el cliente no habló del contexto de uso ni de la conectividad. | ¿Habrá internet estable para el staff en todo el campus? ¿Los administradores también la usarán desde el celular? | `[SUPUESTO]` · validar en el Avance 3 |
| S-19 | Dos usuarios no pueden tener el mismo correo (R4). | El correo es el dato con el que se entra y al que llega la recuperación de contraseña (P-02); si se repite, no se sabría a qué cuenta entrar. Ninguna fuente lo exige. | ¿Debe ser obligatorio que no se repita el correo entre usuarios? | `[SUPUESTO]` · validar en el Avance 3 |

**Puntos abiertos:**

- ¿Cuántos administradores y estudiantes usarán la herramienta? (P-11 quedó sin respuesta.)
- ¿Qué cifra de cumplimiento considerarían un éxito al cerrar el evento?
- ¿Qué pasa con las tareas y los usuarios cuando termina el evento?

## 9. Trazabilidad

| Regla | Origen |
| --- | --- |
| R1 | Descripción («perfiles»), P-05 y A-01 |
| R2 | A-01 y S-01. A-01 corrige P-02: no hay usuario master. |
| R3 | Descripción («no es necesario un proceso de registro»), P-10 y A-01 |
| R4 | P-12 (nombre, correo, teléfono), P-02 (recuperación por correo) y S-19 |
| R5 | P-10 y P-02 |
| R6 | Descripción («Como crear las tareas»), P-09 (título), Extras («categorías no son relevantes») y S-02 |
| R7 | Descripción («uno o varios estudiantes») y P-05 |
| R8 | P-15 |
| R9 | P-15, P-14 y S-03 |
| R10 | P-07 |
| R11 | P-06, P-07 (clave), P-08 y S-05 |
| R12 | Descripción («el botón de guardar») y S-04 |
| R13 | P-01 y S-06 |
| R14 | S-08 |
| R15 | P-14 y S-07 |
| R16 | Descripción («tareas próximas a vencer») y S-09 |
| R17 | P-17 y S-10. La descripción dice «eliminar tareas»; manda la respuesta del cliente: se archivan. |
| R18 | Descripción («ver lista de tareas asignadas»), P-03 y S-13 |
| R19 | P-04, P-04 (clave) y S-11 |
| R20 | P-04 (clave) y S-12 |
| R21 | P-09, P-04 (clave) y S-14 |
| R22 | Descripción («resumen general del estado de las tareas») y S-14 |
| R23 | P-13 y decisión del equipo sobre destinatarios y momentos de aviso |
| R24 | Descripción («eliminar usuarios») y decisión del equipo sobre deshabilitación y retiro de asignaciones |
