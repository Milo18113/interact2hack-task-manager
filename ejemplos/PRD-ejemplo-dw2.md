# PRD · PrestaLab

**Versión:** 1.0 · **Fecha:** 23 de noviembre de 2026 · **Equipo:** Ana Torres y Diego Mena
**Fuente:** respuestas del cliente del 11 de noviembre (`docs/cliente/preguntas.md`)

Este documento describe **qué** debe hacer PrestaLab y **qué no**. No describe cómo se construye: tecnologías, datos y pantallas se deciden en las specs.

## 1. Problema y contexto

El laboratorio de robótica presta kits de robótica, sensores y herramientas sueltas (multímetros, soldadores) a los estudiantes. Hoy el control se lleva en una hoja de cálculo que se actualiza tarde o nunca. Por eso:

- Los coordinadores no saben con certeza qué equipo está fuera ni quién lo tiene.
- Los préstamos vencidos se descubren cuando otro estudiante pide el mismo equipo.
- Los estudiantes tienen que buscar al coordinador en persona para saber si algo está disponible.

PrestaLab se usa durante todo el semestre: los estudiantes reservan desde el celular y retiran en el laboratorio; los coordinadores y ayudantes registran entregas y devoluciones desde la computadora del laboratorio.

## 2. Usuarios y perfiles

| Perfil | Puede | No puede |
| --- | --- | --- |
| **Coordinador** | Crear, editar y desactivar usuarios. Crear, editar y retirar equipos del catálogo. Todo lo que puede un ayudante. | — |
| **Ayudante de laboratorio** | Ver el tablero. Registrar la entrega de una reserva y la devolución de un préstamo. | Crear usuarios ni modificar el catálogo. |
| **Estudiante** | Ver el catálogo y la disponibilidad. Reservar equipo. Ver sus préstamos y su estado. Cancelar una reserva propia que aún no retiró. | Ver los préstamos de otros estudiantes. Registrar entregas o devoluciones. |

Todos entran con usuario y contraseña. No hay registro: los usuarios los crea un coordinador (R10).

## 3. Objetivos y cómo se mide el éxito

| Objetivo | Cómo sabrá el cliente que se cumplió |
| --- | --- |
| Saber en todo momento qué equipo está fuera | En el tablero, el coordinador ve cada préstamo activo con quién lo tiene y cuándo vence, sin abrir otra herramienta. |
| Reducir los préstamos vencidos | Al terminar el semestre hay menos préstamos vencidos que el semestre anterior (el cliente traerá la cifra de la hoja de cálculo). |
| Que los estudiantes no dependan del coordinador para saber qué hay | Un estudiante puede reservar un equipo disponible desde el celular sin hablar con nadie. |

## 4. Alcance (MoSCoW)

| Prioridad | Funcionalidad |
| --- | --- |
| **Must** | Inicio de sesión con los tres perfiles. Gestión de usuarios por el coordinador. Catálogo de equipos con su disponibilidad. Reservar, entregar y devolver con las reglas de la sección 6. Tablero de préstamos para coordinadores y ayudantes. "Mis préstamos" para el estudiante. |
| **Should** | Filtrar el catálogo por tipo (kit, sensor, herramienta). Historial de préstamos de un equipo. |
| **Could** | Extender un préstamo una vez, si nadie más reservó el equipo. |
| **Won't (esta versión)** | Notificaciones por correo (P-12). Multas o sanciones económicas. |

## 5. No-alcance

- Notificaciones por correo o mensajería (P-12).
- Multas, sanciones o calificaciones de los estudiantes.
- Préstamos a personas externas a la universidad.
- Inventario de consumibles (cables, tornillos, filamento): no se prestan, se entregan.
- Registro de usuarios por su cuenta.

## 6. Reglas de negocio

| Id | Regla |
| --- | --- |
| R1 | El catálogo tiene tres tipos de equipo: **kit**, **sensor** y **herramienta**. Cada unidad se identifica con su código de inventario. |
| R2 | Una unidad de equipo está en uno de cuatro estados: **disponible**, **reservada**, **prestada** o **en mantenimiento**. Solo una unidad disponible se puede reservar. |
| R3 | El plazo de un préstamo empieza al entregar el equipo: **5 días** para kits y **2 días** para sensores y herramientas. Si la fecha de devolución cae en sábado o domingo, se adelanta al viernes anterior `[SUPUESTO S-02]`. |
| R4 | Un préstamo está en uno de cinco estados: **reservado** (aún no retirado), **prestado**, **por vencer** (faltan 24 horas o menos para la fecha de devolución), **vencido** (pasó la fecha sin devolución) y **devuelto**. |
| R5 | Un estudiante tiene como máximo **2 préstamos activos** (reservados, prestados, por vencer o vencidos). |
| R6 | Un estudiante con un préstamo **vencido** no puede reservar hasta devolverlo. |
| R7 | Una reserva que no se retira en **24 horas** se cancela y la unidad vuelve a estar disponible `[SUPUESTO S-01]`. |
| R8 | Al registrar una devolución se indica si la unidad está **completa y funcionando**, **incompleta** o **dañada**, con observaciones opcionales. Una unidad incompleta o dañada pasa a **en mantenimiento**. |
| R9 | Hay tres perfiles: coordinador, ayudante y estudiante, con los permisos de la sección 2. |
| R10 | No hay registro. Solo un coordinador crea usuarios, con el correo institucional. |
| R11 | El tablero muestra primero los préstamos **vencidos**, después los **por vencer**, y la cantidad de unidades disponibles por tipo. |
| R12 | Un estudiante solo ve sus propios préstamos. |

## 7. Épicas

| Id | Épica | Descripción | Prioridad |
| --- | --- | --- | --- |
| E1 | Acceso y usuarios | Inicio de sesión con tres perfiles y gestión de usuarios por el coordinador (R9, R10, R12). | Must |
| E2 | Reservas y préstamos | El estudiante reserva una unidad disponible; un ayudante registra la entrega y la devolución, con los plazos, límites y estados de las reglas R2 a R8. | Must |
| E3 | Catálogo | El coordinador mantiene los equipos y sus unidades; todos ven la disponibilidad (R1, R2). | Must |
| E4 | Tablero | Coordinadores y ayudantes ven de un vistazo lo vencido, lo que vence y lo disponible (R11). | Must |

## 8. Supuestos y puntos abiertos

| Id | Supuesto | Por qué lo decidimos así | Estado |
| --- | --- | --- | --- |
| S-01 | Una reserva no retirada en 24 horas se cancela (R7). | El cliente dejó la decisión al equipo (P-07). Sin un límite, un equipo podría quedar bloqueado por una reserva olvidada. | `[SUPUESTO]` · validar en el Avance 3 |
| S-02 | Si la devolución cae en fin de semana, se adelanta al viernes (R3). | El cliente dijo "nunca sobre fin de semana sin permiso", pero no qué hacer. Adelantar evita que el laboratorio cerrado reciba devoluciones. | `[SUPUESTO]` · validar en el Avance 3 |

**Puntos abiertos:**

- ¿Cómo se da el "permiso" para que un préstamo pase el fin de semana? Por ahora no existe en el producto.
- ¿Qué pasa con los préstamos activos al terminar el semestre?

## 9. Trazabilidad

| Regla | Origen |
| --- | --- |
| R1 | Corrección del cliente al resumen ("también herramientas sueltas") |
| R2 | P-08 (estado en mantenimiento) |
| R3 | P-03 y S-02 |
| R4 | P-05 |
| R5 | P-04 |
| R6 | P-06 |
| R7 | P-07 y S-01 |
| R8 | P-08 |
| R9 | P-01 |
| R10 | P-02 |
| R11 | P-09 |
| R12 | P-01 (los estudiantes no ven lo de otros) |
