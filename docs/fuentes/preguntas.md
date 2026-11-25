2# Proyecto final: avance #1 - Preguntas para el cliente

**Juan Burgos Landazuri, 00335157**  
**Emilio Puga, 00336640**

## 1. Lo que entendimos

Este va a ser una app web para ayudar a gestionar las tareas del staff para el Interact2Hack 2027. Los administradores pueden crear, eliminar, editar, ver y asignar tareas al personal del staff, mientras que el personal del staff puede ver su lista de tareas, añadir observaciones y completar cada una. Todas estas acciones se reflejan en la base de datos para tener constancia de las tareas pendientes, las tareas completadas, los responsables y los detalles que implique cada una.


## 2. Preguntas

| ID | Tema | Pregunta | Importancia | Supuestos | Prioridad | Respuesta |
|---|---|---|---|---|---|
| P-01 | Tareas y Checklist | ¿Las observaciones son necesarias para que se pueda completar una tarea? | Define el flujo de estados de la tarea y si las observaciones son opcionales u obligatorias para cerrarla. | Las observaciones son opcionales y no bloquean que el staff marque la tarea como completada. | Media | Es opcional |
| P-02 | Usuarios y Perfiles | ¿Quién gestiona los usuarios administrativos? | Determina quién tiene permisos para crear cuentas administrativas y cómo se controla el acceso al sistema. | Existe una lista previa de usuarios administrativos que se crean directamente en la aplicación mediante un administrador principal. | Alta | Crear un usuario master que tiene todos los permisos. Opción de restablecer contraseña que te reinicie por correo |
| P-03 | Tareas y Checklist | ¿Un miembro del staff puede ver sus tareas completadas? | Define qué información se muestra al staff y si se necesita un historial de tareas completadas en su vista. | El staff puede visualizar tanto sus tareas pendientes como las completadas, mientras que los administradores pueden consultar las tareas de todos los usuarios. | Baja | Si puede ver sus tareas completadas |
| P-04 | Tablero | ¿Cuál es el criterio para que una tarea se muestre en el tablero? | Aclara qué tareas deben aparecer en el tablero y permite definir los criterios de filtrado y visualización. | El tablero muestra las tareas del día actual. | Alta | Se muestran las n tareas, ordenadas por: vencidas, ordenadas por orden de vencimiento, en ejecución, sin asignar, completadas |
| P-05 | Usuarios y Perfiles | ¿Un usuario puede tener múltiples roles (staff y admin)? | Define la estructura de roles, permisos y restricciones de acceso para cada usuario. | Cada usuario tiene un único rol asignado: administrador o staff. | Media | No |
| P-06 | Tareas y Checklist | ¿Todos los elementos de un checklist deben ser obligatorios? | Determina las validaciones del formulario y las condiciones necesarias para permitir completar una tarea. | Todos los elementos del checklist son obligatorios y deben marcarse antes de confirmar la finalización. | Alta | Sí. Si no se han completado, no se puede completar la tarea. |
| P-07 | Tareas y Checklist | Cuando una tarea tiene varios responsables, ¿cada estudiante tiene su propio checklist o todos comparten uno? | Define cómo se almacena el progreso de cada responsable y cómo se calcula el cumplimiento de una tarea compartida. | Cada estudiante tiene su propio progreso individual en el checklist y la tarea se considera completada cuando todos sus responsables la finalizan. | Alta | Todos comparten un solo checklist |
| P-08 | Tareas y Checklist | ¿El estudiante confirma directamente la finalización de una tarea o el administrador debe aprobar primero? | Define el flujo de finalización de las tareas y si se requiere un proceso adicional de revisión por parte del administrador. | El estudiante confirma directamente la finalización y el administrador puede visualizar el resultado. | Alta | El estudiante confirma directamente la finalización y el administrador puede visualizar el resultado. |
| P-09 | Tablero | ¿Qué información e indicadores específicos debe mostrar el tablero y el resumen? | Permite definir los indicadores necesarios para monitorear el cumplimiento general y facilitar la toma de decisiones de los administradores. | El tablero muestra el total de tareas, tareas pendientes, en progreso, completadas y vencidas. | Alta | Muestra, en orden de vencimiento, título, responsables, ubicación y fecha de vencimiento |
| P-10 | Acceso | ¿Qué sucede si un usuario olvida su contraseña? | Define el mecanismo de recuperación de acceso y las responsabilidades del administrador sobre las credenciales. | El administrador puede restablecer la contraseña de un usuario desde la gestión de usuarios. | Media | La debe poder cambiar. Inicialmente el admin asigna una contraseña y el usuario la podrá cambiar. |
| P-11 | Contexto de uso | ¿Cuántos usuarios y administradores utilizarán aproximadamente el sistema? | Permite estimar la cantidad de cuentas, dimensionar infraestructura y considerar la concurrencia de usuarios. | Se espera que la plataforma sea utilizada por un grupo limitado de estudiantes y administradores pertenecientes al staff del evento. | Media | *(Sin respuesta)* |
| P-12 | Usuarios y Perfiles | ¿Qué información debe contener el perfil de cada usuario? | Define los campos necesarios para el registro, identificación y administración de los usuarios. | El perfil contiene nombres, apellidos, correo electrónico, contraseña, rol y estado de la cuenta. | Alta | nombre, correo, teléfono |
| P-13 | Alcance | ¿Se necesitan notificaciones para nuevas asignaciones, recordatorios y tareas completadas? | Determina si se necesita un sistema adicional de notificaciones y qué eventos deben generar alertas. | No se implementan notificaciones externas en la primera versión; los usuarios consultan las actualizaciones directamente en la plataforma. | Media | Dentro de la aplicación, para vencimiento o nuevas tareas |
| P-14 | Tareas y Checklist | ¿Qué ocurre con una tarea que venció sin ser completada? | Define cómo se gestionan los incumplimientos y cómo se refleja el vencimiento en el tablero. | La tarea cambia automáticamente al estado de vencida, pero sigue disponible para que el estudiante pueda completarla. | Alta | Se muestra con alta prioridad, no desaparece. |
| P-15 | Tareas y Checklist | ¿Cuáles son los estados que una tarea puede tener? | Define el ciclo de vida de una tarea y las transiciones permitidas entre sus diferentes estados. | Las tareas tienen cuatro estados principales: pendiente, en progreso, completada y vencida. | Alta | No Asignado, Pendiente, En Ejecución, Completado, Vencida |
| P-16 | Alcance | ¿Se necesita un historial con los cambios y fechas de ejecución? | Determina si es necesario almacenar información histórica para realizar seguimiento y auditoría de las actividades. | Se registra la fecha de creación, última actualización y finalización de cada tarea, así como el usuario responsable. | Media | Extra si se puede |
| P-17 | Tareas y Checklist | ¿Las tareas se eliminan definitivamente o se archivan? | Define cómo se gestionan los registros históricos y evita la pérdida de información sobre tareas ejecutadas. | Las tareas se archivan en lugar de eliminarse definitivamente, conservando su información e historial. | Media | Que se archive nomás, no sea visible |
| P-18 | Alcance | ¿Se debe implementar un sistema de evidencia para la finalización de tareas? | Determina si se necesitan funcionalidades adicionales para adjuntar archivos, fotografías u otras evidencias. | No se requiere adjuntar evidencias en la primera versión; basta con completar el checklist y agregar observaciones opcionales. | Baja | No es necesario, pero es un buen extra si las condiciones de Supabase lo permiten. |


## 3. Preguntas Clave

### P-07

Cuando una tarea tiene varios responsables, ¿cada estudiante tiene su propio checklist o todos comparten uno? Todos comparten la misma tarea, si uno la completa, se completa para todos.


### P-08

¿El estudiante confirma directamente la finalización de una tarea o el administrador debe aprobar primero? Staff


### P-04

¿Cuál es el criterio para que una tarea se muestre en el tablero? En admin, una grid con tarjetas de tarea. Cada tarjeta muestra su estado, detalles, color coding/separación por secciones. Orden: fecha de vencimiento: más reciente a antiguo


## Extras

- Se debe mantener la identidad visual del Interact2Hack
- Campos de tarea: categorías no son relevantes
