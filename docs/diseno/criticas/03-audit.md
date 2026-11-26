# Auditoría técnica · Dirección 2 «Señal»

**Herramienta:** Impeccable 0.1.30, `/impeccable audit` · **Objetivo:** `docs/diseno/direcciones/direccion-2-senal.html` (+ `base.css`) · **Fecha:** 25 de noviembre de 2026
**Método:** auditoría de código del archivo, reutilizando la evidencia medida en la crítica (`02-critique.md`, Assessment B) sobre el mismo archivo sin cambios: `impeccable detect` (archivo y navegador a 320, 360, 390 y 1280 px en Chrome headless), contrastes calculados con la fórmula WCAG 2.x y recorrido real con Tab.
**Persistencia:** no se guardó en `.impeccable/`, para no crear esa carpeta dentro del repositorio de la entrega. Este archivo es el registro.

## Puntaje de salud técnica

| # | Dimensión | Puntaje | Hallazgo clave |
| --- | --- | --- | --- |
| 1 | Accesibilidad | 3 | `.signal small` a 4.03:1 y foco lima sobre morado a 2.28:1 |
| 2 | Rendimiento | 3 | Se carga Big Shoulders 700, que no se usa |
| 3 | Theming | 3 | Tokens de estado nombrados por color (`--estado-rojo`), no por rol; degradado en hex literal |
| 4 | Responsive | 2 | Scroll lateral: 486 px de ancho a 390 px; no cumple reflow a 320 px |
| 5 | Integridad | 3 | Datos de ejemplo que contradicen el PRD (umbral R16, conteos del tablero) |
| **Total** | | **14/20** | **Bueno (14–17)** |

## Veredicto de integridad: pasa

El sistema es coherente y propio: todos los componentes toman tokens de `base.css`, los estados siempre llevan icono y texto, y no hay radios, sombras ni fuentes fuera del brandboard. El detector dio 1 hallazgo real (contraste); `kicker-above-heading` es en parte falso positivo (marcó el rótulo del marco del tile) y `line-length` viene del texto del marco. Lo que falla son los datos de ejemplo, no el sistema.

## Resumen

- Hallazgos: **P0: 0 · P1: 2 · P2: 5 · P3: 3**.
- Lo más importante: contraste del kicker de la señal, desborde horizontal, foco sobre el morado, tokens sin rol semántico y datos que contradicen el PRD.

## Hallazgos por gravedad

### [P1] Contraste insuficiente en el kicker de la tarjeta señal
- **Dónde:** `.signal small`, línea 52 (tinta con `opacity: 0.72` sobre morado, 12 px).
- **Categoría:** Accesibilidad.
- **Impacto:** el rótulo de la tarjeta más importante queda a 4.03:1.
- **Norma:** WCAG 1.4.3 (mínimo 4.5:1).
- **Arreglo:** quitar la opacidad; tinta pura sobre morado da 5.83:1. Aplica también a la tarjeta de Novedades.
- **Comando:** `/impeccable polish`

### [P1] Desborde horizontal en celular
- **Dónde:** `.screens` en `base.css` (la columna `1fr` crece a 470 px); `.meter` mantiene 3 columnas bajo 640 px; `.phone` más ancho que el contenedor.
- **Categoría:** Responsive.
- **Impacto:** 96 px de más a 390 px y 126 px a 360 px; scroll lateral. Es el marco del tile, no una pantalla real del producto.
- **Norma:** WCAG 1.4.10 Reflow.
- **Arreglo:** `minmax(0, 1fr)` en `.screens`, `.meter` a 1–2 columnas bajo 640 px y `.phone { max-width: 100% }`.
- **Comando:** `/impeccable adapt`

### [P2] Anillo de foco invisible sobre el morado
- **Dónde:** el `:focus-visible` global (lima) dentro de `.signal`.
- **Categoría:** Accesibilidad.
- **Impacto:** 2.28:1 sobre el morado; quien navega con teclado pierde el foco en el botón de la señal.
- **Norma:** WCAG 1.4.11 (no textual, 3:1).
- **Arreglo:** anillo tinta (5.83:1) o blanco (3.43:1) dentro de superficies moradas.
- **Comando:** `/impeccable polish`

### [P2] Las tarjetas que se abren no son enlaces reales
- **Dónde:** líneas 200, 209, 235, 241 y 247 (`div role="link" tabindex="0"` sin `href` ni manejo de Enter).
- **Categoría:** Accesibilidad / Integridad.
- **Impacto:** aceptable en un tile; si el agente lo copia, la tarjeta recibe foco y no hace nada.
- **Norma:** WCAG 2.1.1 Teclado.
- **Arreglo:** el DESIGN.md exige `<a href>` envolviendo la franja, con el título como nombre accesible.
- **Comando:** `/impeccable harden`

### [P2] La ayuda del botón deshabilitado no está asociada
- **Dónde:** botón `disabled` de la línea 171 y el `.hint` debajo.
- **Categoría:** Accesibilidad.
- **Impacto:** un lector de pantalla anuncia «Confirmar ejecución, no disponible» sin decir que faltan 3 pasos.
- **Arreglo:** `aria-describedby` al hint; mejor `aria-disabled` en vez de `disabled`, para que siga siendo enfocable.
- **Comando:** `/impeccable clarify`

### [P2] Los tokens de estado no tienen rol semántico
- **Dónde:** `base.css`: `--estado-rojo`, `--estado-ambar`, y el lima de marca reusado como estado.
- **Categoría:** Theming.
- **Impacto:** la guía pide «colores con roles semánticos (incluidos los estados de una tarea)»; con nombres de color el agente no sabe qué token usar para cada estado.
- **Arreglo:** el DESIGN.md define `--color-vencida`, `--color-proxima`, `--color-ejecucion`, `--color-pendiente`, `--color-no-asignada` y `--color-completada` (más sus fondos), que apuntan a los valores de marca.
- **Comando:** `/impeccable extract`

### [P2] Los datos de ejemplo contradicen el PRD
- **Dónde:** tablero y avisos del tile.
- **Categoría:** Integridad.
- **Impacto:** «Próxima a vencer» con 1 h 20 min, pero R16 dice 30 min (y S-09 sigue diciendo 2 h); «En ejecución · 3» agrupa una tarea Completada; el indicador dice 1 vencida y el tablero no muestra la sección Vencidas.
- **Arreglo:** unificar el umbral en el PRD y usar en el brand board datos que cumplan R16, R19 y R21.
- **Comando:** `/impeccable clarify`

### [P3] Iconos sin ocultar a lectores de pantalla
- **Dónde:** cada `<svg class="ico">` en insignias y metadatos (solo el sprite lleva `aria-hidden`).
- **Arreglo:** `aria-hidden="true"` en cada icono decorativo; el texto ya nombra el estado.

### [P3] Peso de fuente cargado y sin uso
- **Dónde:** línea 9, Big Shoulders `wght@700;900`; solo se usa 900.
- **Arreglo:** cargar `wght@900` (una descarga menos).
- **Comando:** `/impeccable optimize`

### [P3] Degradado y avisos con valores literales
- **Dónde:** `.bar i` (línea 48) usa hex en vez de `var(--i2h-purple)`/`var(--i2h-lime)`; los `.notice` no llevan `role="status"`.
- **Arreglo:** usar los tokens; el DESIGN.md exige `role="status"` (o `alert` para «Vencida»).

## Patrones sistémicos

- **La accesibilidad falla en un solo contexto: las superficies moradas.** El texto atenuado y el foco lima pierden contraste ahí. El DESIGN.md necesita una regla: «sobre morado, todo va en tinta pura».
- **El tile documenta los estilos pero no la semántica** (enlaces, roles, descripciones de ayuda). El DESIGN.md debe especificarla para que el agente no la invente.

## Lo que está bien

- Todos los pares de contraste base pasan: texto 20.54:1, morado 5.70:1, tinta sobre rojo 7.21:1, borde de control 3.78:1.
- Áreas táctiles: botones de 52 px, pasos de 60 px y franjas de más de 200 px de alto.
- Foco visible en todos los tipos de elemento (probado con Tab real); no hay `outline: none` en ningún lado.
- `prefers-reduced-motion` respetado; solo cambian colores, así que no se pierde información.
- Ligero: sin imágenes, iconos en sprite SVG, fuentes con `preconnect` y `display=swap`.

## Acciones recomendadas

1. **[P1] `/impeccable polish`:** tinta pura en `.signal small` y foco tinta dentro de superficies moradas.
2. **[P1] `/impeccable adapt`:** `minmax(0,1fr)` en `.screens`, `.meter` colapsable y `.phone` al 100 %.
3. **[P2] `/impeccable extract`:** tokens de estado con nombre de rol.
4. **[P2] `/impeccable harden`:** franjas como `<a href>` y avisos con `role`.
5. **[P2] `/impeccable clarify`:** `aria-describedby` en el botón deshabilitado y datos de ejemplo alineados con R16, R19 y R21.
6. **`/impeccable polish`:** pasada final.
