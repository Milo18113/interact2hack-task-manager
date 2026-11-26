# DESIGN.md · Organización del staff del Interact2Hack

Sistema de diseño **«Señal de staff»**, versión 1.0 (noviembre 2026).

Este archivo es la fuente de verdad de cómo se **ve** y se **comporta** la interfaz de la herramienta de organización del staff. No define funcionalidad: qué hace la herramienta lo dice el PRD (`docs/prd/PRD.md`). Cuando una tarea toque la interfaz, el agente lee este archivo antes de escribir código.

El sistema extiende la identidad oficial **Señal Neón v1.0** del Interact2Hack (`docs/fuentes/Interact2Hack-Brandboard.html`) a una herramienta de trabajo. Donde el brandboard decide, este archivo lo sigue; donde no decide (estados de una tarea, componentes de la herramienta), la decisión es del equipo y queda marcada como **[SUPUESTO]**.

## 1. Cómo se usa este archivo

| Pregunta | Respuesta |
| --- | --- |
| ¿Quién lo lee? | El equipo y el agente que construye la interfaz en el Avance 3. |
| ¿Qué decide? | Tokens (color, tipografía, espaciado, radios, movimiento), layout, componentes con sus estados, accesibilidad y reglas de estilo. |
| ¿Qué no decide? | Reglas de negocio, flujos ni datos. Eso vive en el PRD y en las specs. |
| ¿Cómo se relaciona con una spec? | La spec cita tokens y componentes **por su nombre** (`--color-vencida`, «Franja de tarea»). No copia valores. |
| ¿Cómo se cambia? | Se edita este archivo y el archivo de tokens en el mismo commit. El brand board (`docs/diseno/brand-board.html`) se vuelve a generar desde aquí; si no coinciden, manda este archivo. |
| ¿Qué pasa si choca con una spec? | Gana la spec en lo que hace la herramienta; gana este archivo en cómo se ve. Si la duda persiste, se pregunta antes de implementar. |

El proceso que llevó a estas decisiones está en `docs/diseno/`: brief (`brief.md`), tres direcciones (`direcciones/`), elección (`criticas/01-eleccion.md`), crítica y auditoría de Impeccable (`criticas/02-critique.md`, `criticas/03-audit.md`) y hallazgos aceptados y rechazados (`criticas/04-hallazgos.md`, citados aquí como H-xx).

## 2. Brief

- **Personalidad:** bold, calls-to-action, understandable (digerible y legible).
- **Referente:** un pizarrón con una lista de pendientes, al estilo de Google Tasks. Como metáfora, no como estilo esqueumorfista: superficie oscura, texto claro de alto contraste, y cada tarea como un **renglón** que se abre.
- **Quién lo usa:** administradores desde una computadora, creando tareas y siguiendo el tablero; estudiantes del staff desde el celular, moviéndose por el campus durante los tres días del hackathon, con conexión a internet (PRD §1, S-18).
- **Restricción del cliente:** «Se debe mantener la identidad visual del Interact2Hack» (Avance 1, Extras).

## 3. Principios

1. **El negro manda.** Toda pantalla parte de `--color-fondo`. No hay modo claro: la identidad es oscura por diseño (brandboard §13).
2. **Una sola señal morada por pantalla.** Como máximo un bloque sólido morado: la tarjeta de Novedades o la acción principal. Si hay dos, ninguna destaca (brandboard, principio 2).
3. **Lima = ahora.** El lima marca lo que está en curso: la insignia «En ejecución», el contador de avisos sin leer y el anillo de foco. Nunca como fondo de áreas grandes.
4. **Nunca solo color.** Todo estado lleva texto e icono. El color refuerza; no informa por sí solo.
5. **Lo que falta destaca, lo hecho se apaga.** Pendiente en morado o blanco; completado en gris (H-07, H-21).
6. **Lo que se abre parece contenedor.** Cada tarea de una lista es una franja con borde arriba y abajo y un «›» (brief).
7. **Esquinas rectas, sin sombras.** Radio 0 en todo. Las únicas formas curvas son los círculos de indicadores (brandboard §5).

## 4. Decisiones de diseño

| Decisión | Por qué |
| --- | --- |
| Dirección «Señal»: lenguaje de cartel del evento, con títulos en Big Shoulders y cifras grandes | Se distingue de otras herramientas de tareas, es fiel a la marca, muestra la información de forma jerárquica y se siente como el hub del Interact2Hack (`01-eleccion.md`). |
| Tema oscuro único | Lo exige el brandboard («Modo claro: no se ofrece»). El contraste alto del blanco sobre negro (20.54:1) también resiste el uso en exteriores. |
| La tarjeta morada es **Novedades**, no «tu próxima tarea» | La versión anterior coronaba una tarea mientras otra vencida quedaba debajo, contra R18 y R19 (H-06). Novedades resume lo que cambió desde la última visita (R25) y la lista conserva el orden del PRD. |
| Franjas en lugar de tarjetas con borde completo | Cada tarea se entiende como un renglón propio que se abre para ver el detalle y el checklist (descripción: «ingresar al detalle de la tarea»). |
| Fecha en palabras a la izquierda, hora a la derecha | «Hoy», «Mañana», «En 3 días», «Venció» se leen más rápido que una fecha durante un evento de tres días; la hora queda grande y alineada para comparar (H-02). |
| Insignias sólidas para lo que pide atención, contorno para lo que espera | Vencida y próxima a vencer en relleno; Pendiente y No asignada en contorno. El lima de «En ejecución» sigue «Lima = ahora» (H-04, rechazado el cambio). |
| Rojo `#FF6B6B` y ámbar `#FFC857` para vencida y próxima a vencer `[SUPUESTO]` | El brandboard no define estados de tarea. Son los mismos tonos que el brandboard usa para marcar lo incorrecto y las advertencias, y cumplen contraste sobre negro (7.40:1 y 13.35:1). |
| Borde de control al 40 % de blanco `[SUPUESTO]` | El borde de marca al 14 % da 1.37:1 y no cumple el 3:1 para controles. El 14 % queda solo para bordes decorativos. |
| Sobre morado, todo va en tinta pura | El texto atenuado y el foco lima no cumplen contraste sobre morado (H-08, H-09). |
| Sin librería de estilos ni de componentes | El sistema es pequeño; las variables CSS bastan y la interfaz no hereda la apariencia genérica de un framework. |

## 5. Tokens

Todos los tokens viven en un único archivo de tokens (por ejemplo `src/styles/tokens.css`, o el que fije la spec), dentro de `:root`. Ningún otro archivo escribe un color, una fuente o un tamaño literal.

### 5.1 Color: base

| Token | Valor | Uso |
| --- | --- | --- |
| `--color-fondo` | `#050307` | Fondo de toda pantalla (negro de marca) |
| `--color-superficie` | `#0E0A14` | Franjas, avisos, campos, panel de avisos |
| `--color-superficie-hover` | `rgba(164, 108, 251, 0.08)` | Fondo de una franja al pasar el cursor |
| `--color-texto` | `#FFFFFF` | Texto principal |
| `--color-texto-suave` | `rgba(255, 255, 255, 0.64)` | Texto secundario, metadatos, ayudas |
| `--color-borde` | `rgba(255, 255, 255, 0.14)` | Bordes decorativos, separadores, pasos completados |
| `--color-borde-control` | `rgba(255, 255, 255, 0.40)` | Borde de campos, casillas y franjas (elementos que se tocan) |
| `--color-accion` | `#A46CFB` | Botón primario, tarjeta de Novedades, enlaces, pasos pendientes |
| `--color-sobre-accion` | `#0B0612` | Texto e iconos sobre `--color-accion` y sobre los rellenos de estado (tinta de marca) |
| `--color-ahora` | `#5CF000` | Contador de avisos sin leer, hover del botón primario |
| `--color-foco` | `#5CF000` | Anillo de foco sobre fondo y superficie |
| `--color-foco-sobre-accion` | `#0B0612` | Anillo de foco dentro de superficies moradas (H-09) |
| `--degradado-progreso` | `linear-gradient(90deg, var(--color-accion), var(--color-ahora))` | Barra de avance del checklist (el brandboard lo reserva para progreso) |

### 5.2 Color: estados de una tarea (PRD R8 y R16)

Cada estado tiene su token de rol. Los rellenos llevan texto `--color-sobre-accion` (tinta).

| Estado | Token | Valor | Cómo se usa en la insignia | Icono |
| --- | --- | --- | --- | --- |
| No asignada | `--color-no-asignada` | `rgba(255, 255, 255, 0.64)` | Contorno punteado `--color-borde-control`, texto en este color | Persona tachada |
| Pendiente | `--color-pendiente` | `#FFFFFF` | Contorno de 2 px y texto en este color | Reloj |
| En ejecución | `--color-ejecucion` | `#5CF000` | Relleno; texto tinta | Reproducir |
| Completada | `--color-completada` | `rgba(255, 255, 255, 0.14)` | Relleno; texto `--color-texto` | Marca de verificación |
| Vencida | `--color-vencida` | `#FF6B6B` `[SUPUESTO]` | Relleno; texto tinta | Triángulo de alerta |
| Próxima a vencer (marca, no estado) | `--color-proxima` | `#FFC857` `[SUPUESTO]` | Relleno; texto tinta; lleva el tiempo restante | Reloj de arena |

### 5.3 Tipografía

| Token | Valor |
| --- | --- |
| `--fuente-display` | `"Big Shoulders Display", "Arial Narrow", sans-serif` (solo peso 900) |
| `--fuente-texto` | `"Sora", "Segoe UI", sans-serif` (pesos 400 y 600) |

Big Shoulders va siempre en mayúsculas y **nunca por debajo de 24 px** ni en párrafos (brandboard §4).

| Nivel | Fuente · tamaño / alto de línea · peso | Uso |
| --- | --- | --- |
| `--texto-cifra` | Display · 64 / 0.85 · 900 (44 en celular) | Números del Indicador del tablero |
| `--texto-pantalla` | Display · 40 / 0.9 · 900 | Título de la pantalla («Mis tareas», título en el detalle) |
| `--texto-senal` | Display · 36 / 0.92 · 900 | Titular de la tarjeta de Novedades |
| `--texto-hora` | Display · 32 / 1 · 900 | Hora de vencimiento en la franja |
| `--texto-tarea` | Display · 28 / 0.95 · 900 | Título de la tarea en la franja; numeral del checklist |
| `--texto-aviso` | Display · 24 / 1 · 900 | Título de un aviso; título de sección del panel |
| `--texto-base` | Texto · 16 / 1.6 · 400 | Texto de lectura, pasos del checklist, campos (nunca menos de 16 px en campos) |
| `--texto-boton` | Texto · 15 / 1 · 600, mayúsculas, +0.08 em | Botones |
| `--texto-meta` | Texto · 14 / 1.4 · 400 | Lugar, responsables, ayudas, texto de avisos (H-03) |
| `--texto-kicker` | Texto · 12 / 1.2 · 600, mayúsculas, +0.2 em | Rótulos: «Novedades», títulos de grupo, etiquetas de campo |
| `--texto-insignia` | Texto · 12 / 1 · 600, mayúsculas, +0.14 em | Insignias de estado |

### 5.4 Espaciado, radios y bordes

| Token | Valor |
| --- | --- |
| `--espacio-1` … `--espacio-8` | 4, 8, 12, 16, 24, 32, 48, 64 px (base 4, brandboard §5) |
| `--radio` | 0 en todo |
| `--radio-circulo` | 50 %, solo para el contador de avisos y el punto de estado |
| `--borde-componente` | 2 px |
| `--borde-fino` | 1 px (separadores) |
| `--borde-paso` | 3 px (borde superior de cada paso del checklist) |
| `--borde-aviso` | 6 px (borde izquierdo del aviso) |
| `--alto-progreso` | 4 px |
| `--alto-tactil` | 44 px mínimo; botones a 52 px |
| `--sombra-flotante` | `0 18px 60px rgba(0, 0, 0, 0.6)`, solo para el diálogo de confirmación y el panel de avisos en escritorio |

### 5.5 Movimiento

| Token | Valor | Uso |
| --- | --- | --- |
| `--duracion-ui` | 200 ms | Hover, foco, marcar un paso |
| `--curva` | `cubic-bezier(0.16, 1, 0.3, 1)` | Todas las transiciones |

Sin animaciones de entrada ni barridos dentro de la herramienta: es una pantalla de trabajo. Con `prefers-reduced-motion: reduce`, todas las duraciones pasan a 0.

## 6. Layout

| Ancho | Comportamiento |
| --- | --- |
| Hasta 640 px (celular del estudiante) | Una columna, márgenes laterales `--espacio-4`. Encabezado con el título de la pantalla y la Campana a la derecha. Lista de franjas agrupadas por estado. La acción principal del detalle va a ancho completo en una barra inferior fija (H-19). El Indicador del tablero pasa a 2 columnas. |
| 641 a 1024 px | Cuadrícula del tablero a 2 columnas; Indicador a 3 columnas. |
| Más de 1024 px (escritorio del administrador) | Contenedor de 1200 px máximo, márgenes `--espacio-6`. Indicador a 5 columnas sobre el tablero; franjas en cuadrícula de 3 columnas por sección. |

Ninguna pantalla hace scroll horizontal a 390 px ni a 360 px (H-10). Las columnas usan `minmax(0, 1fr)` para que el contenido no las ensanche.

**Orden de las listas.** El tablero agrupa por estado en el orden de R19: Vencidas, En ejecución, Pendientes, No asignadas, Completadas. La lista del estudiante usa el mismo orden (R18). Dentro de cada grupo, primero lo más cercano al momento actual (R20). Cada grupo lleva un título en `--texto-kicker` y `--color-accion` con su conteo: «VENCIDAS · 1».

## 7. Componentes

### 7.1 Botón

| Variante | Fondo | Texto | Borde | Hover |
| --- | --- | --- | --- | --- |
| Primario | `--color-accion` | `--color-sobre-accion` | — | Fondo `--color-ahora` |
| Secundario | transparente | `--color-accion` | 2 px `--color-accion` | Fondo `--color-accion`, texto tinta |
| Sobre morado | `--color-sobre-accion` | `--color-texto` | — | Texto `--color-ahora` |
| Peligro | transparente | `--color-vencida` | 2 px `--color-vencida` | Fondo `--color-vencida`, texto tinta |
| Deshabilitado | transparente | `--color-texto-suave` | 2 px punteado `--color-borde-control` | — |

- Alto 52 px, `--texto-boton`, un verbo claro («Confirmar ejecución», «Guardar avance», «Asignar», «Entendido»).
- Un solo botón primario por pantalla, y cuenta como el bloque morado de esa pantalla (principio 2).
- Deshabilitado: usa `aria-disabled="true"`, sigue siendo enfocable y muestra el motivo en texto cerca, asociado con `aria-describedby` («Faltan 3 pasos por marcar», R11; H-12).

### 7.2 Campo de formulario

- Etiqueta arriba, en `--texto-kicker` y `--color-accion`; si es opcional lo dice: «Observaciones · opcional» (R13).
- Campo con fondo `--color-superficie`, borde 2 px `--color-borde-control`, texto `--texto-base` (16 px), alto mínimo `--alto-tactil`. El área de observaciones mide al menos 96 px.
- Ayuda debajo en `--texto-meta` y `--color-texto-suave` («Las ven todos los responsables de la tarea»).
- Error: borde y mensaje en `--color-vencida`, mensaje debajo del campo y enlazado con `aria-describedby`.
- Foco: anillo de 3 px `--color-foco` con 2 px de separación.
- El formulario del administrador para crear o editar una tarea usa estos mismos campos: título, fecha y hora, lugar o aula, más el Editor de pasos (§7.12) y el Selector de responsables (§7.13) (R6).

### 7.3 Insignia de estado

Bloque rectangular (radio 0) con icono + texto en `--texto-insignia`, relleno y contorno según §5.2. El texto es siempre visible; el icono es decorativo (`aria-hidden="true"`).

- **Próxima a vencer** se suma a la insignia del estado y lleva el tiempo restante en dos partes: «Próxima:» y «25 min». Cada parte no se corta por dentro (`white-space: nowrap`); si las dos no caben en una línea, «25 min» baja **entera** a la línea siguiente (H-05). Aparece solo cuando faltan 30 minutos o menos (R16).
- Sobre la tarjeta morada, las insignias se invierten: relleno tinta con texto del color del estado.

### 7.4 Franja de tarea

Es el renglón de una lista: la lista del estudiante y el tablero del administrador usan el mismo componente.

- **Contenedor:** fondo `--color-superficie`, borde de 2 px `--color-borde-control` **solo arriba y abajo**, sin bordes laterales. Separación de `--espacio-3` entre franjas.
- **Enlace:** toda la franja es un `<a href>` al detalle de la tarea; su nombre accesible es el título (H-11).
- **Indicador de apertura:** «›» de 28 px en `--color-texto-suave`, centrado verticalmente a la derecha (H-20).
- **Contenido, de arriba abajo:**
  1. Insignias: estado y, si aplica, «Próxima: 25 min».
  2. Título en `--texto-tarea`, cortado a 3 líneas en la lista (H-18).
  3. Lugar (icono de ubicación) y responsables (icono de personas) en `--texto-meta` y `--color-texto-suave`.
  4. Barra de avance de 4 px con `--degradado-progreso`.
  5. Fila de vencimiento: **a la izquierda la fecha en palabras**, a la derecha la hora en `--texto-hora` (H-02).

**Fecha en palabras:** «Hoy», «Mañana», «En 3 días» (n ≥ 2) o «Venció». En el tablero del administrador lleva el avance entre paréntesis: «Mañana (2 de 5)». En la lista del estudiante el avance va en la barra y en el detalle.

| Estado de la franja | Qué cambia |
| --- | --- |
| Normal | Como arriba |
| Hover | Fondo `--color-superficie-hover`; «›» en `--color-accion` |
| Foco | Anillo `--color-foco` alrededor de toda la franja |
| Vencida | Bordes superior e inferior en `--color-vencida`; la hora en `--color-vencida`; la fecha dice «Venció» |
| Completada | Fondo transparente; título y hora en `--color-texto-suave`; barra en `--color-borde` (H-21) |

### 7.5 Ítem de checklist

- Fila completa tocable (la etiqueta envuelve la casilla), alto mínimo 60 px.
- Numeral del paso («01», «02»…) en `--texto-tarea` a la izquierda; texto del paso en `--texto-base`; casilla de 28 × 28 px a la derecha, borde 2 px `--color-borde-control`.
- **Pendiente:** borde superior de 3 px en `--color-accion` y numeral en `--color-accion` (H-07).
- **Completado:** borde superior en `--color-borde`, numeral y texto en `--color-texto-suave`, texto tachado, casilla rellena de `--color-texto` con la marca en tinta.
- Foco: el anillo se dibuja en la casilla.
- Arriba de la lista, el avance en texto: «2 de 5 pasos».

### 7.6 Detalle de tarea y confirmación

Pantalla del estudiante al abrir una franja.

- **Encabezado:** insignias, título en `--texto-pantalla`, y debajo lugar, fecha en palabras con la hora («Hoy · 10:00») y responsables.
- **Cuerpo:** Ítems de checklist y el campo de Observaciones.
- **Barra inferior fija:** botón a ancho completo con su ayuda arriba. Mientras falten pasos, el primario es «Guardar avance» y la ayuda dice «Con los 5 pasos marcados podrás confirmar la ejecución».
- **Confirmar (R11, R12):** al guardar con todos los pasos marcados aparece un diálogo (radio 0, borde superior 2 px `--color-accion`, `--sombra-flotante` en escritorio): «¿Confirmar la ejecución? Se marcará como completada para Ana Torres y Luis Mena. Quedará registrada a tu nombre.» Botones: «Confirmar ejecución» (primario) y «Aún no» (secundario). El foco entra al diálogo y `Esc` lo cierra (H-01).
- **Éxito:** Aviso de tipo «hecho» con quién confirmó y a qué hora («Completaste «Check-in de participantes» · 14:02»; S-05).

### 7.7 Aviso

Bloque con fondo `--color-superficie`, borde izquierdo de 6 px en el color del tipo, icono de 20 px **en el mismo color que el borde**, título en `--texto-aviso` y texto en `--texto-meta` y `--color-texto-suave`.

| Tipo | Color del borde y del icono | Icono | Ejemplo |
| --- | --- | --- | --- |
| Tarea nueva | `--color-ejecucion` (lima) | Reproducir | «Nueva tarea para ti · «Check-in de participantes» · Hall principal · Hoy 10:00» |
| Próxima a vencer | `--color-proxima` (ámbar) | Reloj de arena | «Próxima a vencer · «Check-in de participantes» vence en 25 min · faltan 3 pasos» |
| Vencida | `--color-vencida` (rojo) | Triángulo de alerta | «Tarea vencida · «Preparar sala de mentorías» venció a las 08:30. Todavía puedes completarla.» |
| Cambio de hora o lugar | `--color-accion` (morado) | Reloj | «Cambió la hora · «Check-in de participantes» ahora vence a las 10:30» |
| Te retiraron de una tarea | `--color-accion` (morado) | Persona tachada | «Ya no eres responsable de «Montar audio del teatro»» |
| Completada por otro | `--color-borde-control` (gris) | Marca de verificación | «Luis Mena completó «Repartir kits de bienvenida» · 09:42» |
| Hecho (confirmaste tú) | `--color-ejecucion` (lima) | Marca de verificación | «Completaste «Check-in de participantes» · 14:02» |

Se anuncian con `role="status"`; el de tarea vencida con `role="alert"`.

### 7.8 Tarjeta de Novedades

El único bloque morado de «Mis tareas». Resume lo ocurrido desde la última vez que el estudiante abrió la herramienta (R25). Solo para estudiantes.

- Fondo `--color-accion`, todo el texto en `--color-sobre-accion` puro, sin opacidad (H-08).
- Rótulo «NOVEDADES» en `--texto-kicker`; titular en `--texto-senal` con el total: «3 novedades».
- Una línea por tipo de cambio, en Sora 600 de 15 px, solo los tipos que tengan al menos uno: «2 tareas nuevas», «1 completada por Luis Mena», «1 venció», «1 cambió de hora o lugar», «1 ya no es tuya».
- Botón «Entendido» con la variante «Sobre morado». Al tocarlo la tarjeta desaparece hasta que haya novedades nuevas. Si no hay novedades, la tarjeta no se muestra.
- El anillo de foco dentro de la tarjeta usa `--color-foco-sobre-accion` (H-09).

### 7.9 Campana y contador

- Icono de campana de 24 px en `--color-texto`, arriba a la derecha del encabezado, con área tocable de 44 × 44 px. Solo para estudiantes (R26).
- Contador de no leídos: círculo de 20 px mínimo en `--color-ahora`, número en `--color-sobre-accion` (Sora 600, 12 px), sobre la esquina superior derecha de la campana. Más de 9 se muestra como «9+». Con 0 no se muestra.
- Nombre accesible con el conteo: `aria-label="Avisos, 3 sin leer"`.

### 7.10 Panel de avisos

- Se abre desde la Campana. En celular ocupa toda la pantalla; en escritorio es un panel lateral de 400 px con `--sombra-flotante`.
- Encabezado «AVISOS» en `--texto-aviso` y botón de cerrar (×) de 44 × 44 px.
- Lista de Avisos (§7.7) del evento completo, **del más reciente al más antiguo**, cada uno con su hora arriba en `--texto-meta` («Hoy · 09:42»). Al abrir el panel los avisos quedan leídos y el contador vuelve a 0.
- Vacío: «Todavía no tienes avisos.»
- Al abrir, el foco va al título del panel; `Esc` lo cierra y el foco vuelve a la Campana.

### 7.11 Indicador del tablero de cumplimiento

Fila de celdas sobre el tablero, una por estado y en el orden de R19 (R22).

- Cada celda: borde 2 px `--color-borde`, número en `--texto-cifra`, nombre del estado en `--texto-insignia` y `--color-texto-suave`.
- **Vencidas con 1 o más:** la celda va rellena de `--color-vencida` con número y texto en tinta. Con 0, celda normal con «0».
- Columnas según el ancho (§6): 5, 3 o 2.

### 7.12 Editor de pasos del checklist

En el formulario de tarea del administrador.

- Lista de pasos numerados («01», «02»…, numeral en `--texto-tarea` y `--color-accion`), cada uno con un campo de texto de una línea en `--texto-base`.
- Cada paso tiene un botón «Quitar» con icono ×, área de 44 × 44 px y nombre accesible con su número: `aria-label="Quitar paso 3"`.
- Debajo, botón secundario «Agregar paso». El foco pasa al campo del paso nuevo.
- Se exige al menos un paso (R6, S-02): con un solo paso, «Quitar» queda deshabilitado con su motivo («La tarea necesita al menos un paso»); al guardar sin pasos, error en `--color-vencida` bajo la lista.

### 7.13 Selector de responsables

En el formulario de tarea del administrador.

- Campo de búsqueda por nombre y, debajo, la lista de estudiantes con la misma casilla del Ítem de checklist (§7.5): nombre en `--texto-base`, correo en `--texto-meta`. Fila completa tocable, alto mínimo 52 px.
- Solo aparecen estudiantes con cuenta activa (R7, R24); nunca administradores.
- Los elegidos se muestran arriba como chips (radio 0, borde 2 px `--color-borde`, Sora 600 de 13 px, alto 44 px) con su × para quitarlos.
- Se puede guardar sin responsables; la ayuda lo dice: «Sin responsables, la tarea queda No asignada» (R6, R9).

### 7.14 Fila de estudiante

En la gestión de usuarios del administrador (PRD §2).

- Fila con fondo `--color-superficie` y borde inferior `--borde-fino` `--color-borde`: nombre en Sora 600 de 16 px, y debajo correo y teléfono en `--texto-meta` y `--color-texto-suave` (R4).
- A la derecha, «Editar» (secundario) y «Dar de baja» (peligro). En celular, los botones bajan debajo de los datos a ancho completo.
- «Dar de baja» abre el mismo diálogo de §7.6, con el botón de peligro como acción: «¿Dar de baja a Ana Torres? Perderá el acceso y se retirará de sus 3 tareas. Se conserva quién confirmó cada una.» (R24).
- Sobre la lista, el botón primario «Crear estudiante» (el bloque morado de la pantalla).

### 7.15 Estados de pantalla

| Estado | Qué se muestra |
| --- | --- |
| Cargando | Esqueletos del tamaño de las franjas en `--color-superficie`, sin animación de brillo. |
| Vacío (estudiante) | «No tienes tareas asignadas. Cuando un administrador te asigne una, aparecerá aquí.» |
| Vacío (grupo del tablero) | El grupo no se muestra; su celda del Indicador dice «0». |
| Error al guardar | Aviso rojo con `role="alert"`: «No se pudo guardar tu avance» y el botón «Reintentar». Los pasos marcados se mantienen en pantalla (H-17). |

## 8. Accesibilidad

Contraste calculado con la fórmula de WCAG 2.x (los colores con transparencia, compuestos sobre su fondo real).

| Par | Contraste | Mínimo |
| --- | --- | --- |
| `--color-texto` sobre `--color-fondo` | 20.54:1 | 4.5:1 |
| `--color-texto` sobre `--color-superficie` | 19.59:1 | 4.5:1 |
| `--color-texto` sobre `--color-superficie-hover` | 19.28:1 | 4.5:1 |
| `--color-texto-suave` sobre `--color-fondo` | 8.27:1 | 4.5:1 |
| `--color-texto-suave` sobre `--color-superficie` | 8.18:1 | 4.5:1 |
| `--color-accion` sobre `--color-fondo` (rótulos, enlaces) | 5.98:1 | 4.5:1 |
| `--color-accion` sobre `--color-superficie` | 5.70:1 | 4.5:1 |
| `--color-sobre-accion` sobre `--color-accion` (botón, Novedades) | 5.83:1 | 4.5:1 |
| `--color-texto` sobre `--color-sobre-accion` (botón sobre morado) | 20.02:1 | 4.5:1 |
| Tinta sobre `--color-ejecucion` (insignia, contador) | 13.27:1 | 4.5:1 |
| Tinta sobre `--color-vencida` (insignia, indicador) | 7.21:1 | 4.5:1 |
| Tinta sobre `--color-proxima` (insignia) | 13.01:1 | 4.5:1 |
| `--color-texto` sobre `--color-completada` (insignia sobre superficie) | 13.66:1 | 4.5:1 |
| `--color-vencida` sobre `--color-fondo` (hora vencida) | 7.40:1 | 4.5:1 |
| `--color-vencida` sobre `--color-superficie` (botón de peligro, errores) | 7.06:1 | 4.5:1 |
| `--color-borde-control` sobre `--color-fondo` | 3.71:1 | 3:1 |
| `--color-borde-control` sobre `--color-superficie` | 3.78:1 | 3:1 |
| `--color-foco` sobre `--color-fondo` | 13.61:1 | 3:1 |
| `--color-foco` sobre `--color-superficie` | 12.98:1 | 3:1 |
| `--color-foco-sobre-accion` sobre `--color-accion` | 5.83:1 | 3:1 |

**Pares prohibidos:** texto blanco sobre morado (3.43:1, solo para títulos de 24 px o más, y este sistema no lo usa); texto con opacidad sobre morado; foco lima sobre morado (2.28:1); `--color-borde` (1.37:1) como borde de un control.

Además:

- **Foco visible** en todo elemento interactivo: anillo de 3 px con 2 px de separación, en `--color-foco` o `--color-foco-sobre-accion` dentro del morado. Nunca `outline: none`.
- **Áreas táctiles** de al menos 44 × 44 px; botones de 52 px; pasos del checklist de 60 px.
- **Ningún estado depende solo del color:** toda insignia lleva texto e icono (principio 4).
- **Semántica:** franjas como `<a href>`; casillas como `<input type="checkbox">` dentro de su `<label>`; iconos decorativos con `aria-hidden="true"`; avisos con `role="status"` o `role="alert"`; diálogos y panel con foco atrapado y `Esc`.
- **Texto:** todo campo tiene etiqueta visible; errores y motivos de deshabilitado se asocian con `aria-describedby`.
- **Movimiento reducido** respetado (§5.5).

## 9. Reglas para el agente

**DEBE:**

- Leer este archivo antes de cualquier tarea que toque la interfaz.
- Usar solo los tokens de §5, por su nombre.
- Mostrar cada estado de tarea con la Insignia de estado (icono + texto), con los colores de §5.2.
- Usar la Franja de tarea para toda lista de tareas, como `<a href>` al detalle.
- Mostrar la fecha en palabras a la izquierda y la hora a la derecha, y en el tablero «Mañana (2 de 5)».
- Mostrar «Próxima: n min» solo cuando falten 30 minutos o menos (R16), con el salto de línea solo entre sus dos partes.
- Ordenar listas y tablero según R18, R19 y R20.
- Mantener un solo bloque sólido morado por pantalla.
- Pintar el icono de cada Aviso del mismo color que su borde.
- Respetar los anchos de §6 y probar a 390 px y a 360 px.

**NO DEBE:**

- Escribir colores, fuentes o tamaños literales fuera del archivo de tokens.
- Ofrecer modo claro, redondear esquinas, añadir sombras (salvo `--sombra-flotante` donde §7 lo dice) o degradados que no estén en §5.
- Usar Big Shoulders por debajo de 24 px, en minúsculas o en párrafos.
- Poner texto atenuado o foco lima sobre morado.
- Usar el lima como fondo de áreas grandes.
- Mostrar la tarjeta de Novedades, la Campana o el Panel de avisos a un administrador (S-15).
- Instalar librerías de estilos o de componentes.
- Cambiar textos de la herramienta definidos en las specs; el tono es directo y en «tú» (brandboard §11; H-26).

## 10. Criterios verificables de diseño

| Id | Criterio | Cómo se verifica |
| --- | --- | --- |
| D-01 | No hay colores literales fuera del archivo de tokens. | `grep -rnE "#[0-9a-fA-F]{3,8}\b\|rgba?\(" src` excluyendo el archivo de tokens no devuelve nada. |
| D-02 | No hay `font-family` fuera del archivo de tokens. | `grep -rn "font-family" src` excluyendo el archivo de tokens no devuelve nada. |
| D-03 | No hay esquinas redondeadas salvo los círculos permitidos. | `grep -rn "border-radius" src` solo devuelve `var(--radio)` o `var(--radio-circulo)`. |
| D-04 | Toda tarea muestra su estado con texto. | En el navegador, cada Franja tiene una Insignia con texto visible. |
| D-05 | El tablero y la lista siguen el orden del PRD. | Con datos de prueba de los cinco estados, los grupos aparecen como Vencidas, En ejecución, Pendientes, No asignadas, Completadas (R19), y dentro de cada grupo lo más cercano al momento actual primero (R20). |
| D-06 | «Próxima a vencer» respeta el umbral. | Con una tarea a 25 min y otra a 45 min, solo la primera muestra «Próxima: 25 min». |
| D-07 | El tiempo de «Próxima» nunca se corta por dentro. | A 320 px de ancho, «25 min» aparece entero en una línea, junto a «Próxima:» o debajo. |
| D-08 | Hay como máximo un bloque sólido morado por pantalla. | En cada pantalla, contar elementos con fondo calculado `rgb(164, 108, 251)`: el resultado es 0 o 1. |
| D-09 | No hay scroll horizontal en celular. | En ventanas de 390 px y 360 px, `document.documentElement.scrollWidth` es igual al ancho de la ventana. |
| D-10 | Todo elemento interactivo tiene foco visible con contraste. | Recorrer cada pantalla con Tab: cada elemento muestra el anillo; dentro de Novedades el anillo es tinta. |
| D-11 | Las áreas táctiles miden al menos 44 px. | En las herramientas del navegador, botones, Campana, cerrar del panel, pasos y franjas miden 44 px o más de alto. |
| D-12 | No hay pares de texto con contraste insuficiente. | `impeccable detect` sobre las pantallas no devuelve `low-contrast`. |
| D-13 | Las franjas son enlaces reales. | Cada Franja es un `<a>` con `href`; con Enter abre el detalle; su nombre accesible es el título de la tarea. |
| D-14 | El botón deshabilitado explica por qué. | El botón «Confirmar ejecución» con pasos sin marcar tiene `aria-describedby` apuntando al texto «Faltan n pasos por marcar». |
| D-15 | Confirmar pide confirmación y muestra el resultado. | Al guardar con todos los pasos marcados aparece el diálogo con los nombres de los responsables; al confirmar aparece el Aviso «Completaste… · hh:mm». |
| D-16 | El icono de cada aviso coincide con su borde. | En cada Aviso, el color calculado del icono es igual al `border-left-color`. |
| D-17 | El contador de la Campana refleja los no leídos. | Con 3 avisos nuevos el contador dice «3» y la Campana se anuncia «Avisos, 3 sin leer»; al abrir el panel el contador desaparece. |
| D-18 | Novedades aparece solo cuando hay algo nuevo. | Sin cambios desde la última apertura, «Mis tareas» no muestra la tarjeta; tras «Entendido» no vuelve a aparecer al recargar hasta que haya un cambio nuevo. |
| D-19 | La fecha va en palabras. | Con tareas de hoy, mañana, en 3 días y vencida, las franjas dicen «Hoy», «Mañana», «En 3 días» y «Venció», con la hora a la derecha; en el tablero, «Mañana (2 de 5)». |
| D-20 | Big Shoulders nunca baja de 24 px. | En las herramientas del navegador, todo elemento con `--fuente-display` tiene un tamaño calculado de 24 px o más. |
| D-21 | Se respeta el movimiento reducido. | Con `prefers-reduced-motion: reduce` emulado, ninguna transición dura más de 0 ms. |
| D-22 | Una tarea no se guarda sin pasos. | En el formulario de tarea, quitar todos los pasos y guardar muestra el error bajo el Editor de pasos y no crea la tarea. |
| D-23 | El Selector de responsables solo ofrece estudiantes activos. | Con un administrador y un estudiante dado de baja en los datos de prueba, ninguno de los dos aparece en la lista. |
