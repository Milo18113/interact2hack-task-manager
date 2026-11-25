# Brief del sistema de diseño

**Equipo:** Juan Burgos Landazuri y Emilio Puga · **Fecha:** 25 de noviembre de 2026

## Personalidad

**Bold, calls-to-action, understandable** (digestible and readable).

| Palabra | Cómo la leemos en la interfaz |
| --- | --- |
| Bold | Títulos y cifras grandes en Big Shoulders, contraste alto, nada tímido. El estado de una tarea se ve desde lejos. |
| Calls-to-action | Cada pantalla deja claro qué hacer ahora: una sola acción principal, visible y con un verbo («Confirmar ejecución», «Asignar»). |
| Understandable | Texto de lectura en Sora, nunca menor a 16 px en el celular; cada estado se nombra con texto, no solo con color; poca información por tarea. Lo que se puede abrir se ve como un contenedor: cada tarea de la lista es una franja que lleva a su detalle. |

## Referente

**Un pizarrón con una lista de pendientes, al estilo de Google Tasks.**

Lo tomamos como metáfora, no como estilo esqueumorfista: no hay textura de tiza, marco de madera ni letra a mano. Lo que tomamos es:

- La superficie oscura con texto claro de alto contraste, que coincide con el negro de la identidad del Interact2Hack.
- La lista que se lee de arriba abajo, como Google Tasks.
- Cada tarea es un **renglón del pizarrón**: una franja con borde arriba y abajo, sin bordes laterales, que se toca para abrir su detalle. El checklist, las observaciones y la confirmación viven en ese detalle, no en la lista (descripción: «ingresar al detalle de la tarea y completar el checklist»; PRD §2).
- Dentro del detalle, una casilla por paso, como Google Tasks.
- Lo que está hecho se apaga; lo que falta destaca.

## Quién lo usa y dónde

- **Administradores**, desde una computadora: crean y asignan tareas y siguen el tablero de cumplimiento (PRD §1).
- **Estudiantes del staff**, desde el celular, moviéndose por el campus durante los tres días del hackathon, con conexión a internet (PRD §1, `[SUPUESTO S-18]`).

## Restricción del cliente

«Se debe mantener la identidad visual del Interact2Hack» (Avance 1, Extras). El sistema parte del brandboard oficial **Señal Neón v1.0** (`docs/fuentes/Interact2Hack-Brandboard.html`): fondo negro, morado para la acción, lima escaso para lo activo, Big Shoulders Display y Sora, esquinas rectas y sin sombras.

Lo que el brandboard no cubre (colores para los estados de una tarea, en especial «Vencida» y «próxima a vencer») lo decide el equipo y queda documentado como supuesto en el `DESIGN.md`.

## Direcciones

Las tres direcciones exploradas están en `docs/diseno/direcciones/`.
