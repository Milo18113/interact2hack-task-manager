# Hallazgos aceptados y rechazados

**Equipo:** Juan Burgos Landazuri y Emilio Puga · **Fecha:** 25 de noviembre de 2026
**Fuentes:** `02-critique.md` (`/impeccable critique`, 26/40) y `03-audit.md` (`/impeccable audit`, 14/20) sobre la dirección 2 «Señal».

Impeccable recomienda; el `DESIGN.md` decide. Solo los hallazgos **aceptados** pasan al `DESIGN.md` y al brand board. El tile de la dirección 2 no se retoca: queda como evidencia de lo que se criticó.

## Hallazgos

| Id | Hallazgo | Origen | Decisión | Razón y cómo entra al DESIGN.md |
| --- | --- | --- | --- | --- |
| H-01 | El momento de confirmar no está diseñado (sin confirmación, sin éxito, sin «a tu nombre»). | Crítica P1 | **Aceptado** | Es la promesa central (R11). El DESIGN.md define el detalle de tarea con barra inferior fija, el diálogo de R12 («¿Confirmar la ejecución? Se marcará completada para…») y un aviso de éxito con quién y cuándo (S-05). Se **rechaza** quitar «Guardar avance»: R12 y S-04 lo mantienen como acción aparte. |
| H-02 | El lugar y la hora son lo más pequeño y tenue; la hora no lleva día. | Crítica P1 | **Aceptado en parte** | Se **rechaza** cambiar el tamaño del lugar y de la hora: el equipo los considera correctos. Se **acepta** que falta el día: la fecha va en palabras a la izquierda («Hoy», «Mañana», «En 3 días», «Venció») y la hora a la derecha. En el tablero, la fecha lleva el avance: «Mañana (2 de 5)». |
| H-03 | Metadatos de 13–15 px por debajo de los 16 px del brief. | Crítica P1 | **Rechazado** | Los 16 px del brief aplican al texto de lectura y a los campos. Lugar, responsables y avance son etiquetas secundarias; se quedan en 14 px con contraste de 8:1. |
| H-04 | Insignias: el lima se usa en varias a la vez y «Completada» parece deshabilitada; propuesta de cuatro niveles. | Crítica P2 | **Rechazado** | Las insignias se quedan como están. El lima en «En ejecución» sigue la regla del brandboard «Lima = ahora» (estado en curso), y es el color que el equipo eligió. |
| H-05 | «Próxima» y «Próxima a vencer» se usan con dos textos distintos. | Crítica (heurística 4) | **Aceptado** | La insignia sólida ámbar lleva el dato en dos partes: «Próxima:» y «25 min». Si no caben en una línea, «25 min» baja entero a la siguiente; nunca se corta dentro de una parte. |
| H-06 | La tarjeta señal corona una tarea que vence pronto mientras hay una Vencida debajo (contra R18 y R19), y la duplica. | Crítica P2 | **Aceptado, con otra solución** | La tarjeta señal pasa a ser **Novedades** (R25): resume lo que cambió desde la última vez que se abrió la app. La lista mantiene el orden del PRD sin duplicados. |
| H-07 | El checklist resalta los pasos hechos y apaga los pendientes. | Crítica P3 | **Aceptado** | Borde morado para los pasos pendientes y gris para los completados: lo que falta destaca (brief). |
| H-08 | Contraste del kicker de la tarjeta señal: 4.03:1. | Crítica + Audit P1 | **Aceptado** | Sobre morado, todo texto va en tinta pura (5.83:1), sin opacidad. |
| H-09 | Anillo de foco lima sobre morado: 2.28:1. | Crítica + Audit P2 | **Aceptado** | Dentro de superficies moradas el anillo de foco va en tinta (5.83:1). |
| H-10 | Scroll lateral a 390 px y 360 px. | Crítica + Audit P1 | **Aceptado** | Es del marco del tile, pero el DESIGN.md fija el layout por ancho (indicador del tablero y cuadrícula colapsan en celular) y un criterio verificable: sin scroll horizontal a 390 px. |
| H-11 | Las franjas que se abren son `div` con `role="link"`, sin `href`. | Audit P2 | **Aceptado** | Regla para el agente: cada franja es un enlace real (`<a href>`) y su nombre accesible es el título de la tarea. |
| H-12 | La ayuda del botón deshabilitado no está asociada. | Audit P2 | **Aceptado** | El motivo («Faltan 3 pasos por marcar») se asocia con `aria-describedby`. |
| H-13 | Los tokens de estado se nombran por color, no por rol. | Audit P2 | **Aceptado** | El DESIGN.md define un token por estado (`--color-vencida`, `--color-proxima`, `--color-ejecucion`, `--color-pendiente`, `--color-no-asignada`, `--color-completada`), como pide la guía. |
| H-14 | Los datos de ejemplo contradicen el PRD (umbral de 1 h 20 min, conteos del tablero, falta la sección Vencidas). | Crítica + Audit P2 | **Aceptado** | Umbral unificado en 30 minutos (R16, S-09). El brand board usa datos que cumplen R16, R19 y R21. |
| H-15 | Iconos sin `aria-hidden`; avisos sin `role`. | Audit P3 | **Aceptado** | Iconos decorativos con `aria-hidden="true"`; avisos con `role="status"`, y `role="alert"` para «Vencida». |
| H-16 | Se carga Big Shoulders 700 sin usarse; degradado escrito en hex. | Audit P3 | **Aceptado** | Solo se carga el peso 900. El degradado de progreso usa los tokens de marca. |
| H-17 | No hay estados de carga, vacío ni error (guardado fallido). | Crítica (heurística 9) | **Aceptado** | El DESIGN.md define cargando, vacío («No tienes tareas pendientes») y error con «Reintentar». El uso sin conexión queda fuera de alcance (S-18). |
| H-18 | Títulos largos sin regla de truncado. | Crítica (persona Riley) | **Aceptado** | En la lista, el título se corta a 3 líneas; en el detalle se muestra completo. |
| H-19 | El botón principal queda arriba y con ancho natural en el celular. | Crítica (persona Casey) | **Aceptado** | En el celular, la acción principal del detalle va a ancho completo en la barra inferior fija (zona del pulgar). |
| H-20 | El «›» de la franja es diminuto. | Crítica (menor) | **Aceptado** | El «›» se centra verticalmente y crece a 28 px. |
| H-21 | La barra de progreso es lo más brillante de una tarea completada. | Crítica (menor) | **Aceptado** | En Completada la barra va en gris atenuado. |
| H-22 | Los indicadores del tablero no funcionan como filtros y no hay forma de saltar a Vencidas. | Crítica (heurística 7) | **Rechazado** | Filtrar no está en el PRD; el tablero ya muestra Vencidas primero (R19). Queda como idea para después. |
| H-23 | No hay ayuda que explique el checklist ni los estados. | Crítica (heurística 10) | **Rechazado** | Los estados llevan texto e icono y las ayudas van en línea. Una sección de ayuda está fuera del alcance de esta versión. |
| H-24 | `kicker-above-heading` / `hero-eyebrow-chip` (rótulo sobre el título). | Detector | **Rechazado** | Falso positivo: marcó el rótulo del marco del tile. Además, «kicker + título» es el encabezado del brandboard. |
| H-25 | `line-length` y `straggler`. | Detector | **Rechazado** | Cosmético y casi todo del marco del tile, no del producto. |
| H-26 | «pedí» usa voseo; el resto usa tuteo. | Crítica (menor) | **Aceptado** | Todo el texto de la app va en «tú» (voz del brandboard). |

## Cambios del equipo (no vienen de Impeccable)

| Cambio | Origen | Cómo entra al DESIGN.md |
| --- | --- | --- |
| Cada tarea de una lista es una **franja**: borde solo arriba y abajo, «›» a la derecha, se abre para ver el detalle. | Brief (referente: renglón del pizarrón) | Componente «Franja de tarea». |
| **Novedades**: la tarjeta señal morada resume tareas nuevas, tareas compartidas completadas por otro, tareas vencidas, cambios de hora o lugar, y tareas de las que lo retiraron; se queda hasta tocar «Entendido». Solo estudiantes. | Equipo; PRD R25, S-20 | Componente «Tarjeta de Novedades» (el único bloque morado de la pantalla). |
| **Campana** arriba a la derecha con contador de no leídas en círculo lima; abre un panel con todos los avisos del evento, el más reciente primero y con su hora. Solo estudiantes. | Juan; PRD R26, S-21 | Componentes «Campana» y «Panel de avisos», que reusa el componente Aviso. |
| **Aviso ámbar** para «próxima a vencer». | Equipo; PRD R23 | Variante del componente Aviso. |
| El **icono de cada aviso** va en el mismo color que su borde (lima, ámbar o rojo). | Juan | Regla del componente Aviso. |

## Resumen

- **Aceptados:** 20 (incluye 3 aceptados en parte o con otra solución: H-01, H-02 y H-06).
- **Rechazados:** 6, cada uno con su razón.
- Siguiente paso: escribir el `DESIGN.md` con los aceptados y los cambios del equipo, y generar el brand board desde él.
