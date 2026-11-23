# DESIGN.md · PrestaLab

Sistema de diseño **«Mesa de Taller»**, versión 1.0 (noviembre 2026).

Este archivo es la fuente de verdad de cómo se **ve** y se **siente** PrestaLab. No define funcionalidad: qué hace la app lo dicen el PRD (`docs/prd/PRD.md`), las historias y las specs. Cuando una tarea toque la interfaz, el agente lee este archivo antes de escribir código.

## 1. Cómo se usa este archivo

| Pregunta | Respuesta |
| --- | --- |
| ¿Quién lo lee? | Todo el equipo y el agente. `AGENTS.md` lo referenciará para cualquier tarea visual. |
| ¿Qué decide? | Tokens (color, tipografía, espaciado), componentes, layout, accesibilidad y reglas de estilo. |
| ¿Qué no decide? | Reglas de negocio, textos de la app ni comportamiento. Esos viven en el PRD y en las specs. |
| ¿Cómo se relaciona con una spec? | La spec de interfaz cita tokens y componentes **por su nombre** (`--color-vencido`, «Tarjeta de préstamo»). No copia valores. |
| ¿Cómo se cambia? | Se edita este archivo y el archivo de tokens en el mismo commit, con un mensaje `docs(diseño): …`. El brand board se vuelve a generar desde aquí. |
| ¿Qué pasa si choca con una spec? | Gana la spec en lo que hace la app; gana este archivo en cómo se ve. Si la duda persiste, se pregunta antes de implementar. |

## 2. Brief

- **Personalidad:** ordenado, cercano, confiable.
- **Referente:** las etiquetas de inventario y las cajas organizadoras de un taller bien cuidado.
- **Quién lo usa:** estudiantes desde el celular, entre clases; coordinadores y ayudantes desde la computadora del laboratorio, con el equipo en la mano (PRD §1, P-10).
- **Restricción del cliente:** "algo claro y fácil de leer" (P-11). El laboratorio no tiene identidad visual propia; la paleta es decisión del equipo.

El proceso que llevó a estas decisiones está en `docs/diseno/criticas/`.

## 3. Principios

1. **Estado y fecha primero.** En cada préstamo, lo primero que se lee es su estado y su fecha de devolución. El resto viene después.
2. **Nunca solo color.** Todo estado lleva texto e icono («Por vencer», «Vencido»…). El color refuerza; no informa por sí solo.
3. **Cada equipo tiene su etiqueta.** El código de inventario se muestra siempre igual, como una etiqueta física, para que el ayudante lo encuentre con el equipo en la mano.
4. **Un solo acento.** El azul marca lo que se puede hacer (botones, enlaces, foco). Los demás colores se reservan para los estados de los préstamos.
5. **Plano y en calma.** Sin degradados ni animaciones decorativas. La jerarquía sale del tamaño, el peso y el espacio.

## 4. Decisiones de diseño

| Decisión | Por qué |
| --- | --- |
| Tema claro, fondo de papel cálido | El cliente pidió algo claro (P-11). Los estudiantes lo usan en el celular, a veces a pleno sol; el fondo cálido cansa menos que el blanco puro. |
| Atkinson Hyperlegible para todo el texto | Diseñada para distinguir caracteres parecidos (1, l, I; 0, O). Importa en nombres de equipos y en pantallas pequeñas. |
| JetBrains Mono para códigos y fechas | Los códigos de inventario y las fechas se comparan en columna en el tablero; la mono los alinea. Refuerza la metáfora de etiqueta. |
| Tarjetas en móvil, filas en escritorio | El estudiante ve pocos préstamos (máximo 2, R5) y necesita leerlos grandes. El coordinador ve muchos y necesita compararlos. Mismo componente, dos densidades. |
| Insignia con icono y texto | La crítica C-1 mostró que "por vencer" y "vencido" se confundían por color. El icono y el texto los separan aunque el color no se perciba. |
| Bootstrap no se usa | El sistema es pequeño; las variables CSS bastan y el estilo no hereda la apariencia genérica de un framework. |

## 5. Tokens

Todos los tokens vivirán en `src/styles/tokens.css`, dentro de `:root`. Ningún otro archivo escribe un color, una fuente o un tamaño literal.

### 5.1 Color

**Base**

| Token | Valor | Uso |
| --- | --- | --- |
| `--color-fondo` | `#F6F4EE` | Fondo de la página |
| `--color-superficie` | `#FFFFFF` | Tarjetas, paneles, campos |
| `--color-superficie-alta` | `#EFECE3` | Fondo de la etiqueta de inventario, filas al pasar el cursor |
| `--color-borde` | `#DDD8CC` | Bordes decorativos de tarjetas y separadores |
| `--color-borde-control` | `#8A8577` | Borde de campos y controles (A-2) |
| `--color-texto` | `#1E2328` | Texto principal |
| `--color-texto-suave` | `#5A6068` | Texto secundario, etiquetas de campo |
| `--color-acento` | `#1F5FBF` | Botón primario, enlaces, anillo de foco |
| `--color-sobre-acento` | `#FFFFFF` | Texto sobre el acento |

**Estados de un préstamo (PRD, R4)**

| Estado | Texto e icono | Fondo |
| --- | --- | --- |
| Reservado | `--color-reservado` `#5B4BB7` | `--color-reservado-fondo` `#ECE9FA` |
| Prestado | `--color-prestado` `#1F6F8B` | `--color-prestado-fondo` `#E3F1F6` |
| Por vencer | `--color-por-vencer` `#8A5A00` | `--color-por-vencer-fondo` `#FCF0D6` |
| Vencido | `--color-vencido` `#B42318` | `--color-vencido-fondo` `#FDE7E5` |
| Devuelto | `--color-devuelto` `#276B43` | `--color-devuelto-fondo` `#E4F3EA` |

El estado «en mantenimiento» de una unidad (R2, R8) usa `--color-por-vencer` con el texto «En mantenimiento»: comparten el significado de "requiere atención".

### 5.2 Tipografía

| Token | Valor |
| --- | --- |
| `--fuente-texto` | `"Atkinson Hyperlegible", system-ui, sans-serif` |
| `--fuente-mono` | `"JetBrains Mono", ui-monospace, monospace` |

| Nivel | Tamaño / alto de línea | Peso | Uso |
| --- | --- | --- | --- |
| `--texto-titulo` | 28 / 34 px | 700 | Título de la página |
| `--texto-seccion` | 20 / 26 px | 700 | Título de sección y de tarjeta |
| `--texto-base` | 16 / 24 px | 400 | Texto general (nunca menos de 16 px en campos, para evitar el zoom del celular) |
| `--texto-pequeno` | 14 / 20 px | 400 | Etiquetas, ayudas |
| `--texto-codigo` | 14 / 20 px | 500 | Código de inventario y fechas, siempre en `--fuente-mono` |

### 5.3 Espaciado, radios y bordes

| Token | Valor |
| --- | --- |
| `--espacio-1` … `--espacio-8` | 4, 8, 12, 16, 24, 32, 48, 64 px |
| `--radio-control` | 6 px (botones, campos) |
| `--radio-tarjeta` | 10 px |
| `--radio-etiqueta` | 4 px |
| `--borde` | 1 px sólido |
| `--alto-tactil` | 44 px (A-3) |

### 5.4 Movimiento

| Token | Valor | Uso |
| --- | --- | --- |
| `--duracion-rapida` | 120 ms | Cambios de color al pasar el cursor o al enfocar |
| `--duracion-media` | 200 ms | Aparición de avisos |

Con `prefers-reduced-motion: reduce`, todas las duraciones pasan a 0.

## 6. Layout

| Ancho | Comportamiento |
| --- | --- |
| Hasta 640 px (celular) | Una columna. Préstamos como Tarjetas de préstamo. Navegación inferior con tres destinos: Catálogo, Mis préstamos, Cuenta. |
| 641 a 1024 px | Dos columnas en el catálogo. |
| Más de 1024 px (escritorio del laboratorio) | Contenedor de 1200 px máximo. El tablero muestra los préstamos como filas y los Indicadores de disponibilidad arriba. |

Márgenes laterales: `--espacio-4` en celular, `--espacio-6` en escritorio. Sin desplazamiento horizontal a 390 px.

## 7. Componentes

### 7.1 Botón

| Variante | Fondo | Texto | Borde |
| --- | --- | --- | --- |
| Primario | `--color-acento` | `--color-sobre-acento` | — |
| Secundario | `--color-superficie` | `--color-acento` | `--color-borde-control` |
| Peligro | `--color-superficie` | `--color-vencido` | `--color-vencido` |

Alto mínimo `--alto-tactil`. Estado deshabilitado: opacidad 0.5 y cursor `not-allowed`, con el motivo en texto cerca del botón («Tienes un préstamo vencido», R6). Un solo botón primario por pantalla.

### 7.2 Campo de formulario

Etiqueta arriba en `--texto-pequeno` y `--color-texto-suave`. Campo con borde `--color-borde-control`, `--radio-control` y alto `--alto-tactil`. Error: borde y mensaje en `--color-vencido`, con el mensaje debajo del campo y enlazado con `aria-describedby`.

### 7.3 Insignia de estado

Píldora con icono + texto, en el color de texto y el fondo del estado (§5.1). Iconos: reloj (reservado), caja (prestado), reloj de arena (por vencer), triángulo de alerta (vencido), marca de verificación (devuelto), llave (en mantenimiento). El texto es siempre visible; el icono es decorativo (`aria-hidden`).

### 7.4 Etiqueta de inventario

El código de inventario (`KIT-014`, `HER-203`) en `--fuente-mono` y `--texto-codigo`, sobre `--color-superficie-alta`, con `--radio-etiqueta`. Aparece siempre antes del nombre del equipo.

### 7.5 Tarjeta de préstamo

En celular. Fila superior: Etiqueta de inventario a la izquierda, Insignia de estado a la derecha. Debajo, el nombre del equipo en `--texto-seccion`. Al final, «Devolver hasta» y la fecha en `--fuente-mono`. Si el estado es vencido, la fecha va en `--color-vencido`. La fecha nunca se oculta (C-4).

### 7.6 Fila de préstamo

En el tablero de escritorio. Columnas: Etiqueta de inventario, equipo, estudiante, fecha de devolución, Insignia de estado, acción. Orden fijo: vencidos, por vencer, el resto (R11).

### 7.7 Indicador de disponibilidad

Para el tablero (R11). Un panel por tipo de equipo: el número de unidades disponibles en `--texto-titulo`, el total en `--texto-pequeno` («6 de 10 kits disponibles»). Si quedan 0, el número va en `--color-vencido` y el texto dice «Sin kits disponibles».

### 7.8 Avisos

Bloque con borde izquierdo de 4 px en el color del estado relacionado, icono y texto. Éxito en `--color-devuelto`, advertencia en `--color-por-vencer`, error en `--color-vencido`, información en `--color-acento`. Se anuncian con `role="status"` (o `role="alert"` para errores).

### 7.9 Estados de pantalla

| Estado | Qué se muestra |
| --- | --- |
| Cargando | Esqueletos del tamaño de las tarjetas o filas, sin animación de brillo si hay movimiento reducido. |
| Vacío | Texto que explica qué falta y qué hacer: «No tienes préstamos. Busca algo en el Catálogo.» |
| Error | Aviso de error con la acción «Reintentar». |

## 8. Accesibilidad

| Par | Contraste | Mínimo |
| --- | --- | --- |
| `--color-texto` sobre `--color-fondo` | 14.40:1 | 4.5:1 |
| `--color-texto` sobre `--color-superficie` | 15.83:1 | 4.5:1 |
| `--color-texto` sobre `--color-superficie-alta` | 13.40:1 | 4.5:1 |
| `--color-texto-suave` sobre `--color-superficie` | 6.35:1 | 4.5:1 |
| `--color-texto-suave` sobre `--color-fondo` | 5.77:1 | 4.5:1 |
| `--color-acento` sobre `--color-superficie` | 6.09:1 | 4.5:1 |
| `--color-sobre-acento` sobre `--color-acento` | 6.09:1 | 4.5:1 |
| `--color-borde-control` sobre `--color-superficie` | 3.68:1 | 3:1 |
| `--color-borde-control` sobre `--color-fondo` | 3.35:1 | 3:1 |
| Reservado (texto sobre su fondo) | 5.61:1 | 4.5:1 |
| Prestado (texto sobre su fondo) | 4.91:1 | 4.5:1 |
| Por vencer (texto sobre su fondo) | 5.24:1 | 4.5:1 |
| Vencido (texto sobre su fondo) | 5.55:1 | 4.5:1 |
| Devuelto (texto sobre su fondo) | 5.60:1 | 4.5:1 |
| `--color-vencido` sobre `--color-superficie` | 6.57:1 | 4.5:1 |

Además:

- Foco visible en todo elemento interactivo: anillo de 3 px en `--color-acento` con 2 px de separación (A-4).
- Áreas táctiles de al menos 44 × 44 px (A-3).
- Ningún estado depende solo del color (§3, principio 2).
- Todo campo tiene etiqueta visible; los errores se asocian con `aria-describedby`.

## 9. Reglas para el agente

**DEBE:**

- Leer este archivo antes de cualquier tarea que toque la interfaz.
- Usar solo los tokens de §5, por su nombre.
- Mostrar cada estado de préstamo con la Insignia de estado (icono + texto).
- Mostrar el código de inventario con la Etiqueta de inventario, antes del nombre.
- Respetar los anchos de §6 y probar a 390 px.

**NO DEBE:**

- Escribir colores, fuentes o tamaños literales fuera del archivo de tokens.
- Añadir degradados, sombras decorativas o animaciones que no estén en §5.4.
- Ocultar la fecha de devolución en ningún ancho.
- Instalar librerías de estilos o de componentes.
- Cambiar textos de la app: vienen de las specs.

## 10. Criterios verificables de diseño

| Id | Criterio | Cómo se verifica |
| --- | --- | --- |
| D-01 | No hay colores hexadecimales fuera del archivo de tokens. | `grep -rnE "#[0-9a-fA-F]{3,8}\b" src --include=*.css --include=*.tsx \| grep -v tokens.css` no devuelve nada. |
| D-02 | No hay `font-family` fuera del archivo de tokens. | `grep -rn "font-family" src \| grep -v tokens.css` no devuelve nada. |
| D-03 | Todo préstamo muestra su estado con texto. | En el navegador, cada Tarjeta y Fila de préstamo tiene una Insignia con texto visible. |
| D-04 | La fecha de devolución es visible a 390 px. | Vista de celular de «Mis préstamos»: cada tarjeta muestra «Devolver hasta» y la fecha. |
| D-05 | El tablero ordena vencidos, por vencer y el resto. | Con datos de prueba de los tres grupos, el orden en pantalla es ese. |
| D-06 | Todo elemento interactivo tiene foco visible. | Recorrer la pantalla con Tab: cada elemento muestra el anillo de foco. |
| D-07 | Las áreas táctiles miden al menos 44 px. | En las herramientas del navegador, botones y campos miden 44 px o más de alto. |
| D-08 | No hay desplazamiento horizontal a 390 px. | `document.documentElement.scrollWidth` es 390 en una ventana de 390 px. |
| D-09 | Los códigos de inventario y las fechas usan la fuente mono. | En las herramientas del navegador, su fuente calculada es JetBrains Mono. |
| D-10 | Con 0 unidades disponibles, el Indicador lo dice con texto. | Con un tipo sin unidades disponibles, el indicador muestra «Sin … disponibles». |
