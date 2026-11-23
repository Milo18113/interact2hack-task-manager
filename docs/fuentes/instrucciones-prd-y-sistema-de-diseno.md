Proyecto final: avance #2: PRD, brand board y sistema de diseño

Ocultar información del deber
Instrucciones
1. Descripción general
En el Avance 1 encontraron las dudas y, en la sesión con el cliente, obtuvieron respuestas. En este avance las convierten en los dos documentos que van a guiar la construcción de la herramienta de organización de staff del Interact2Hack:

El PRD, que define qué debe hacer el producto y qué no.
El sistema de diseño (DESIGN.md y su brand board), que define cómo debe verse y comportarse la interfaz.
Todavía no se escribe código. Estos documentos son el contexto que el agente leerá en el Avance 3: si son ambiguos, el agente va a inventar.

1.1 Objetivo
Producir un PRD fiel a lo que dijo el cliente y un sistema de diseño propio, verificable y coherente con el producto, con el mismo proceso que practicamos en clase con Hangar Orbital y con el reto del sistema de diseño propio.

1.2 Modalidad y fechas
Equipos

Los mismos del Avance 1, de hasta 2 integrantes.

Insumos

La descripción del proyecto final y su documento del Avance 1 con las respuestas del cliente.

Entrega

Lunes 23 de noviembre, hasta las 23:59.

Dónde

En el repositorio de GitHub del proyecto final, con el enlace subido a D2L.

1.3 Lo que viene después
Avance 3 — 2 de diciembre: avance funcional para el cliente, construido con harness y specs a partir de este PRD y este DESIGN.md.
Presentación final — 16/17 de diciembre (fecha por definir).
2. Qué deben entregar
Tres documentos en el repositorio, más el documento del Avance 1 actualizado con las respuestas del cliente.

2.1 PRD — docs/prd/PRD.md
Describe el producto completo desde el punto de vista del cliente. Sin detalle técnico: ni tablas, ni componentes, ni librerías, ni frameworks. Debe tener estas secciones:

Sección

Qué contiene

Problema y contexto

Qué problema resuelve, para quién y en qué momento del hackathon se usa.

Usuarios y perfiles

Qué puede hacer cada perfil y qué no.

Objetivos y éxito

Cómo sabrá el cliente que la herramienta funcionó.

Alcance

Las funcionalidades, priorizadas con MoSCoW (Must, Should, Could, Won't).

No-alcance

Lo que explícitamente queda fuera de esta versión.

Reglas de negocio

Las reglas que el producto debe respetar, numeradas (R1, R2…): estados de una tarea, cuándo se considera completada, qué significa "próxima a vencer", qué pasa con varios responsables, etc.

Épicas

Las épicas del producto, cada una con una descripción de un párrafo y su prioridad.

Supuestos y puntos abiertos

Lo que el cliente no definió, marcado como [SUPUESTO], con la decisión que tomó el equipo. Y lo que sigue sin resolver.

Trazabilidad

Una tabla que relaciona cada regla de negocio con la pregunta del Avance 1 (P-01, P-02…) que la originó, o con el supuesto que la sostiene.

2.2 Sistema de diseño — DESIGN.md
En la raíz del repositorio, con la misma estructura que trabajamos en clase:

Nombre y propósito del sistema.
Brief: tres palabras de personalidad, un referente y quién usa la herramienta (administradores en un escritorio, estudiantes en el celular, en medio de un hackathon).
Decisiones de diseño y su porqué.
Tokens: colores con roles semánticos (incluidos los estados de una tarea que definieron en el PRD), tipografía, escala de espaciado, radios y movimiento.
Componentes del producto, con sus estados. Como mínimo: tarjeta de tarea, ítem de checklist, insignia de estado, formulario, botón, aviso, y el indicador del tablero de cumplimiento.
Accesibilidad: contraste de 4.5:1 para texto y 3:1 para bordes de control, con el valor calculado de cada par; foco visible; áreas táctiles; estados que no dependen solo del color.
Reglas para el agente: qué debe y qué no debe hacer al construir la interfaz.
Criterios verificables numerados (D-01, D-02…), cada uno con cómo se comprueba.
Si el cliente indicó una identidad visual del Interact2Hack que deban respetar, el sistema la sigue. Si no, la decisión del equipo queda documentada como supuesto.

2.3 Brand board — docs/diseno/brand-board.html
Una página HTML autocontenida que se abre en el navegador y se genera a partir del DESIGN.md: si algo no coincide, manda el DESIGN.md. Muestra la paleta, la tipografía y cada componente con datos realistas del producto: una tarea pendiente, una próxima a vencer, una completada, un checklist a medio completar.

3. Proceso recomendado
El orden importa: primero el qué, después cómo se ve.

3.1 Del cliente al PRD
Consoliden las respuestas. Completen el documento del Avance 1 con lo que dijo el cliente, y marquen cada supuesto como confirmado, descartado o pendiente.
Escriban el PRD a partir de las respuestas, no de la descripción original. Cada regla de negocio debe poder rastrearse hasta una respuesta o un supuesto.
Busquen los huecos con la IA. Pidan al agente que revise el PRD buscando reglas ambiguas, casos borde y contradicciones, igual que en el refinamiento de criterios. Registren lo aceptado y lo rechazado.
Revisen que no haya detalle técnico. Si aparece una tabla, un endpoint o una librería, sobra.
3.2 Del PRD al sistema de diseño
Es el proceso del reto de la sesión que cubrimos en clase:

Brief. Tres palabras de personalidad, un referente y el contexto de uso. Lo escribe el equipo, no la IA.
Tres direcciones. Pidan tres style tiles claramente distintos, con datos reales del producto (tareas, checklists, estados).
Elegir y criticar. Elijan una dirección, justifiquen por qué, y revísenla con /impeccable critique y /impeccable audit. Clasifiquen cada hallazgo: aceptado o rechazado, con su razón.
DESIGN.md. Escríbanlo con las decisiones y los hallazgos aceptados. Calculen y anoten el contraste de cada par.
Brand board. Genérenlo desde el DESIGN.md. Si algo no les convence, corrijan primero el DESIGN.md y vuelvan a generarlo.
Recuerden: Impeccable recomienda; el DESIGN.md decide. No ejecuten /impeccable init ni /impeccable document en el repositorio, porque escriben un DESIGN.md propio.

3.3 Coherencia entre los dos documentos
Los estados de una tarea del PRD son los mismos que tienen color y texto en el DESIGN.md.
Los componentes del DESIGN.md cubren lo que necesita cada perfil del PRD.
El contexto de uso del PRD (celular, escritorio, conectividad del evento) se refleja en las decisiones de diseño.
3.4 Uso de IA
Se espera que usen IA en todo el avance. El equipo es responsable de lo que entrega: cada regla del PRD y cada decisión del DESIGN.md debe poder explicarse y defenderse.

4. Formato de entrega
Todo vive en el repositorio de GitHub del proyecto final. El equipo sube a D2L un solo enlace al commit de la entrega, con los nombres de ambos integrantes.
Estructura esperada:
DESIGN.md
docs/
├── prd/PRD.md
├── diseno/
│   ├── brand-board.html
│   └── criticas/
└── backlog/            (opcional)
El historial de commits debe mostrar el orden del proceso: respuestas del cliente, PRD, brief y direcciones, DESIGN.md, brand board.
Si el repositorio es privado, agreguen al docente como colaborador.
Vence el 25 de noviembre de 2026 23:59