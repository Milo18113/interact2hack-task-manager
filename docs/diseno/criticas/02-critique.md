# Crítica · Dirección 2 «Señal»

Method: dual-agent (A: revisión de diseño · B: detector + evidencia de navegador, ejecutados aislados)

**Herramienta:** Impeccable 0.1.30, `/impeccable critique` · **Objetivo:** `docs/diseno/direcciones/direccion-2-senal.html` (+ `base.css`) · **Fecha:** 25 de noviembre de 2026
**Modo de superficie:** Operate (interfaz de una app), dentro de una marca fija (brandboard Señal Neón v1.0).
**Contexto usado:** no existe PRODUCT.md (no se ejecutó `init`, porque la guía del curso lo prohíbe). Se dio a los agentes `brief.md`, el PRD y las reglas del brandboard como restricciones fijas.
**Persistencia:** no se guardó snapshot en `.impeccable/critique/`, para no crear esa carpeta dentro del repositorio de la entrega. Este archivo es el registro.

## Puntaje de salud del diseño

| # | Heurística | Puntaje | Problema clave |
| --- | --- | --- | --- |
| 1 | Visibilidad del estado del sistema | 3 | Insignia, «2 de 5 pasos» y tiempo restante son claros. No hay feedback de guardado ni de éxito al confirmar, ni señal de que otro responsable marcó un paso (R10). |
| 2 | Lenguaje del mundo real | 3 | Español claro. «Confirmar ejecución» es lenguaje del PRD, no del estudiante. «Próxima» choca con «Tu próxima tarea». |
| 3 | Control y libertad del usuario | 2 | Confirmar es definitivo para todos los responsables (R11, R15) y no hay paso de confirmación ni deshacer. «Guardar avance» explícito puede perder marcas al salir. |
| 4 | Consistencia y estándares | 3 | Tokens disciplinados. El tablero dice «En ejecución · 3» sobre 2 tarjetas En ejecución y 1 Completada; la insignia dice «Próxima» en tarjetas y «Próxima a vencer» en la paleta. |
| 5 | Prevención de errores | 3 | El botón deshabilitado con «Faltan 3 pasos» es bueno; la ayuda queda separada, debajo de la fila de botones. |
| 6 | Reconocer en vez de recordar | 3 | Cada estado tiene icono y texto, pero hay seis tratamientos distintos de insignia. El «›» es diminuto. |
| 7 | Flexibilidad y eficiencia | 2 | La tarjeta señal es un buen atajo. Los indicadores del tablero no parecen filtros y no hay orden ni salto a Vencidas. |
| 8 | Diseño estético y minimalista | 3 | Hay contención real. Las insignias lima y ámbar y los 7 datos por tarjeta del tablero añaden ruido. |
| 9 | Recuperación de errores | 2 | «Todavía puedes completarla» es ejemplar. No hay estado de guardado fallido, sin conexión (S-18) ni validación. |
| 10 | Ayuda y documentación | 2 | Hay ayudas en línea. Nada explica el checklist ni los estados. |
| **Total** | | **26/40** | **Aceptable (20–27)** |

El lenguaje visual vale más que el 26: lo que baja el puntaje son los momentos que el tile no diseña (confirmar, éxito, fallo).

## Veredicto de especificidad

**Revisión de diseño:** es específico de la marca, pero solo a medias del producto. Negro, neón, Big Shoulders en mayúsculas y el bloque morado son del evento; cualquier herramienta del Interact2Hack (agenda de mentores, jurado) podría reutilizarlos sin cambios. Lo propio de un gestor de tareas es solo esto: la hora de vencimiento como numeral grande, el checklist numerado 01–05 y la «tarjeta señal». El degradado morado → lima de la barra de progreso es la parte más genérica y la menos fiel a la marca.

**Escaneo determinista (detector):** 1 hallazgo en el archivo y 3 más al renderizar; detalle en la sección «Evidencia del detector».

## Impresión general

La dirección acierta en jerarquía y en «una señal por pantalla». La mayor oportunidad no está en los componentes sueltos sino en el **momento de confirmar la tarea**, que es la promesa central del producto (R11) y no está diseñado. Después, que «dónde» y «cuándo» (lo que el cliente quiere que el estudiante sepa sin preguntar) son lo más pequeño y tenue de la tarjeta.

## Qué funciona

1. **La tarjeta señal.** Un solo bloque morado, un verbo y una fecha con conteo de pasos responden «¿qué hago ahora?» en dos segundos.
2. **El estado nunca depende solo del color.** Icono, texto y relleno siempre van juntos; los avisos y la ayuda del botón deshabilitado están bien redactados.
3. **La hora como numeral protagonista** (32 px, roja si está vencida) es el instinto correcto para un staff que trabaja contra reloj.

## Problemas prioritarios

**[P1] El momento de confirmar no está diseñado**
- **Por qué importa:** confirmar es irreversible para todos los responsables y es el núcleo del producto. Hoy no hay confirmación, éxito, ni garantía de a nombre de quién queda (S-05).
- **Arreglo:** pantalla de detalle con barra inferior fija que lleva el único bloque morado, «Confirmar ejecución», con «5 de 5 · quedará a tu nombre» arriba. Al tocar, una hoja a ancho completo, solo borde y radio 0: «¿Confirmar? Se marcará completada para Ana y Luis» con [Confirmar] [Aún no]. El éxito es un bloque lima de 200 ms, «HECHO · 14:02», y la tarjeta señal pasa a «Siguiente: …». Si el checklist se autoguarda, se elimina «Guardar avance».
- **Comando sugerido:** `/impeccable shape`

**[P1] «Dónde» y «cuándo» están poco servidos**
- **Por qué importa:** el objetivo del PRD es «qué hacer, dónde y hasta cuándo». El lugar es el texto más tenue (14 px, 64 %) mientras el título y la hora son enormes. `.card-meta` (14), `.card-due span` (13), `.signal p` (15) y `.hint` (14) incumplen el «≥ 16 px en celular» del brief. La hora no lleva día (el evento dura tres) ni la etiqueta «Vence» en el tablero.
- **Arreglo:** lugar a 16 px en blanco ~87 % justo bajo el título; etiqueta «Vence hoy 21:00» o «Vence mié 10:00» en celular y tablero. Los 12–13 px quedan solo para insignias y kickers.
- **Comando sugerido:** `/impeccable typeset`

**[P2] Accesibilidad medida: contraste y foco sobre el morado, y desborde horizontal**
- **Por qué importa:** ambos agentes lo encontraron por separado. `.signal small` (tinta al 72 % sobre morado, 12 px) da **4.03:1**, bajo el 4.5:1. El anillo de foco lima sobre la tarjeta señal morada da **2.28:1**, bajo el 3:1. En 390 px la página mide 486 px y hace scroll lateral porque `.meter` conserva 3 columnas y `.phone` desborda.
- **Arreglo:** quitar la opacidad (tinta pura sobre morado da 5.83:1); anillo de foco blanco o tinta dentro de la tarjeta señal (blanco sobre morado da 3.43:1); colapsar `.meter` a una columna bajo 640 px y dejar `.phone` con `max-width: 100%`. El desborde es del marco del tile, no del producto.
- **Comando sugerido:** `/impeccable adapt` (desborde) y `/impeccable polish` (contraste y foco)

**[P2] El sistema de insignias de estado (problema ya conocido por el equipo)**
- **Por qué importa:** hay cinco usos del lima o del degradado, lo que rompe «el lima es escaso». Lima junto a ámbar en una fila es lo más ruidoso de la tarjeta, y «En ejecución» (sano) grita tanto como Vencida. «Completada» se lee como deshabilitada y se parece a «No asignada».
- **Arreglo (cuatro niveles):** relleno sólido = pide atención (Vencida, vence pronto); tinte morado al 22 % con borde morado de 2 px y icono de reproducir = En ejecución, con la barra de pasos en 5 celdas moradas, sin degradado; contorno blanco = Pendiente; **Completada sin insignia**: una franja de una línea con ✓ en el mismo cuadro blanco del checklist, título atenuado y «Sofía · 09:42». «Próxima» pasa a insignia ámbar con el dato: «⏳ 1 H 20 MIN».
- **Comando sugerido:** `/impeccable colorize`

**[P2] La tarjeta señal contradice la lista, y «próxima» se usa con dos sentidos**
- **Por qué importa:** corona una tarea que vence en 1 h 20 min mientras debajo hay una Vencida, aunque R18 y R19 ordenan Vencidas primero. Además duplica una franja. «Tu próxima tarea» y «Próxima» significan cosas distintas.
- **Arreglo:** la tarjeta señal muestra la primera tarea en el orden de R9 y R20 y esa tarea sale de la lista; el kicker pasa a «Lo más urgente». Dentro de la tarjeta, invertir las insignias a relleno tinta con texto de color, porque el rojo sobre el relleno morado casi no se separa.
- **Comando sugerido:** `/impeccable clarify`

## Evidencia del detector

- **Archivo (HTML + `base.css`):** 1 hallazgo, `low-contrast` en la línea 195, `.signal small`, 4.0:1 sobre 4.5:1. **Real**, no depende de la marca.
- **Navegador a 390 px:** el mismo contraste, `kicker-above-heading` y `body-text-viewport-edge` (scroll lateral, 96 px de más). A 360 px, 126 px de más. A 1280 px: `hero-eyebrow-chip` y 2 `line-length` (~90 y ~105 caracteres).
- **Falsos positivos o marco del tile:** `kicker-above-heading` es en parte falso, porque el rótulo «Dirección 2 de 3» pertenece al marco; el detector omitió los casos reales dentro del producto (`.signal small` sobre `b`, `.group-h`, `.field label`) porque `b` no es un encabezado. `line-length` y los 3 `straggler` son cosméticos y casi todos del marco.
- **Ninguno de los elementos fijados por la marca** (tema oscuro, mayúsculas, radio 0, morado, lima) fue marcado.
- Un resultado vacío en las demás reglas significa «el detector no lo encontró», no «está limpio»: no juzga el diseño de la maqueta.
- **Contrastes que pasan:** blanco sobre negro 20.54:1, texto atenuado 8.18:1, morado sobre superficie 5.70:1, tinta sobre lima 13.27:1, sobre rojo 7.21:1, sobre ámbar 13.01:1, tinta sobre morado 5.83:1, borde de control 3.78:1.
- **Áreas táctiles:** `.btn` 52 px, `.step` 60 px, tarjetas > 200 px de alto. Las casillas visuales de 28 px quedan bajo 44 px, pero el área real es la fila completa.
- **Foco:** `:focus-visible` global de 3 px lima y se probó con Tab en cada tipo de elemento; la única falla es el contraste del anillo sobre el morado (arriba).

## Personas

- **Alex, administrador que busca lo atrasado.** El indicador rojo «1 Vencidas» se lee en 2 segundos, pero no parece clicable y el cuadro del tablero no incluye tarjetas Vencidas. En la cuadrícula de 3 columnas, las insignias de la tarjeta 1 se envuelven y empujan su título más abajo que el de las vecinas, lo que rompe el escaneo por filas. Las horas no llevan fecha y no hay filtro por persona ni lugar.
- **Sam, accesibilidad.** Casi todo bien: texto más icono, borde de control a 3.7:1, movimiento reducido respetado. Fallan `.signal small` (4.0:1 a 12 px) y el foco lima sobre morado (2.3:1). El texto atenuado de 13–14 px incomoda al ampliar.
- **Casey, estudiante bajo el sol, caminando.** Los bloques sólidos y los títulos blancos resisten el reflejo; los metadatos grises al 64 % y las líneas del 9–14 % se pierden. «Continuar» queda en la mitad superior y los botones están alineados a la izquierda con ancho natural, no a ancho completo en la zona del pulgar. Una interrupción a mitad del checklist, más un guardado explícito, arriesga perder marcas, y los compañeros no las ven.
- **Riley, casos borde.** Un título de 60 caracteres se vuelve 4 líneas de 28 px en mayúsculas sin regla de truncado. No hay estado para Vencidas = 0 ni para «todo hecho». Las listas largas de responsables no están probadas.

## Observaciones menores

- **[P3] El checklist invierte «lo que falta destaca»:** los pasos hechos (01–02) llevan regla morada de 3 px y numeral morado pleno, mientras los pendientes llevan reglas tenues. Arreglo: hecho = regla al 14 % y numeral atenuado; pendiente = regla al 40 %; el primer paso sin marcar lleva numeral y regla moradas.
- **Errores en la maqueta del tablero:** «En ejecución · 3» sobre 2 En ejecución más 1 Completada, y falta la sección Vencidas pese al «1» del indicador.
- **Conflicto en el PRD (fuera del diseño):** R16 ahora dice **30 minutos**, pero S-09 dice **2 horas**, y el tile muestra «próxima a vencer» con 1 h 20 min. Hay que unificar el umbral antes de que la marca ámbar signifique algo.
- El «›» es diminuto y está arriba a la derecha: centrarlo o llevarlo a 32 px.
- La barra de la tarjeta Completada es lo más brillante de una tarjeta «atenuada».
- «pedí» usa voseo; el resto del texto usa tuteo.

## Preguntas para considerar

1. Si la señal es «lo único», ¿por qué un 08:30 rojo vencido grita más que el bloque morado de arriba? ¿Debería una tarea vencida ser la señal?
2. ¿El tablero del admin tiene que ser de tarjetas? Una pila densa de franjas de una línea ordenadas por estado, como en el referente Google Tasks, se escanearía más rápido para «qué está atrasado». ¿«Bold» tiene que costar densidad de lectura en escritorio?
3. Un estudiante que termina la última tarea de la noche recibe el componente más silencioso del sistema. ¿Se aprovecha mejor el lima en ese momento que en tres insignias En ejecución?
4. Si el checklist es compartido y se autoguarda, ¿el estudiante necesita «Guardar avance»?
