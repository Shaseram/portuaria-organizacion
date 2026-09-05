# Decisiones y escalamientos — Frente 2

**Regla que gobierna este archivo.** `README.md` de Célula 3: *«Si se detecta una contradicción, **no se resuelve silenciosamente**: se aplica la jerarquía indicada en el Maestro y se registra el conflicto en `DECISIONES_Y_ESCALAMIENTOS.md`.»* Y `00_MAESTRO`, §1: ante contradicción prevalecen los PDF oficiales (`FEP03` > `FEP02` > `FEP01`) por sobre el material propio.

**Cómo leer los estados.** `PENDIENTE` es trabajo propio no iniciado; `BLOQUEADO EXTERNO` requiere dato o autorización de un tercero; `PARA REVISIÓN DEL INTEGRADOR` es un asunto de `00_Gobierno/`, que este frente no edita por regla de autoridad; `APLICADO` es una corrección ya hecha dentro de los archivos propios del frente.

## 1. Tabla de control

| ID | Fecha | Entregable | Tipo | Tema | Alternativas/impacto | Recomendación o pregunta | Afecta a | Estado |
|---|---|---|---|---|---|---|---|---|
| `F2-DEC-001` | — | C1/C2 | CANDIDATO ADR | sala técnica | actual/nueva/edge mínimo | desarrollar ADR-005 | todos | PENDIENTE |
| `F2-ESC-001` | — | C3 | EXTERNO | site survey | cantidad/ubicación radio | mantener rango y levantar | C4/T-11 | BLOQUEADO EXTERNO |
| `F2-ESC-002` | — | C3 | EXTERNO | plan protección | autoridad aprueba segregación | no intervenir sin aprobación | D1 | BLOQUEADO EXTERNO |
| `F2-ESC-003` | 2026-09-05 | C2/C3 | OMISIÓN DE ALCANCE | Capítulo 7 del BTT ausente en toda la célula | 14 requisitos no citados; `T21-4.2-E` es elemento evaluado | incorporar al Maestro §9.2 y a los cumplimientos de C2/C3 | C2, C3, C4, D1, matriz global | PARA REVISIÓN DEL INTEGRADOR |
| `F2-ESC-004` | 2026-09-05 | C2 | CITA INCOMPLETA | rango `RT-06` truncado en `.24`; el BTT exige hasta `.34` | se pierden custodia de medios, espacio de operación y rutas de comunicaciones | corregir el rango en el Maestro §10.3 | C2, C4, T-11, `ADR-005` | PARA REVISIÓN DEL INTEGRADOR |
| `F2-ESC-005` | 2026-09-05 | todos | OMISIÓN DE ALCANCE | checklist del Capítulo C del BTT no incorporado | 28 entregables exigibles con su artículo y su Sobre; 6 son del Frente 2 | agregarlo como control en la matriz global §2 | los tres frentes | PARA REVISIÓN DEL INTEGRADOR |
| `F2-ESC-006` | 2026-09-05 | C1/C3/C4 | COLISIÓN DE CÓDIGOS | 4 códigos `RT` de los capítulos del Frente 2 designan materias distintas en BTT y caso | el Supuesto M de Célula 2 solo documenta 5 colisiones, ninguna de estas | ampliar el listado del Maestro §1.1 con estos códigos | C1, C3, C4, T-12 | PARA REVISIÓN DEL INTEGRADOR |
| `F2-ESC-007` | 2026-09-05 | todos | LÍNEA BASE DESFASADA | Maestro §2.2 y `MC-19` citan 138 RF / 84 RNF / 10 reglas | hoy son 139 / 91 / 11 y el reparto es 82 / 57 | actualizar §2.2 y registrar el commit `c4756df` según la regla de lectura 5 | los tres frentes | PARA REVISIÓN DEL INTEGRADOR |
| `F2-ESC-008` | 2026-09-05 | C1/C2 | EXTERNO | ingresos físicos de comunicaciones del edificio administrativo | `RT-06.32` exige rutas físicas distintas con ingreso al edificio por puntos separados; el caso no dice si el edificio lo admite | levantar antes de cerrar `ADR-005`; puede descartar por norma la alternativa de endurecer la sala actual | C1, C2, C3, `ADR-005` | BLOQUEADO EXTERNO |
| `F2-ESC-009` | 2026-09-05 | C2 | DECISIÓN SIN ADR | proveedor y región de nube | `RT-03.01` exige declarar proveedor y regiones primaria y secundaria; `RT-15.04`/`.05` exigen intensidad de carbono y análisis comparativo. La lista `ADR-001` a `ADR-010` no cubre esta decisión | abrir `ADR-011`; afecta a los tres frentes, no se resuelve en el Frente 2 | todos | PARA REVISIÓN DEL INTEGRADOR |
| `F2-ESC-010` | 2026-09-05 | C3 | INTERPRETACIÓN CON EFECTO DE PLAZO | el ambiente de DR debe estar operativo en el **mes 6** | `RT-04.01` condiciona el hito H3 a los **cinco** ambientes; el E-25 describe H3 nombrando cuatro. Art. 5.2 y 5.4 de las BA obligan a la lectura más exigente | planificar región secundaria, replicación y conmutación para el mes 6, no para el paso a producción. Afecta el cronograma del Subdocumento 7 | C2, C3, C4, Frente 1, planificación | PARA REVISIÓN DEL INTEGRADOR |
| `F2-DEC-002` | 2026-09-05 | C2 | TENSIÓN A DECLARAR | `RT-06.20` exige biometría facial para el recinto técnico | la restricción no negociable 8 registra la objeción a la biometría obligatoria | declarar que son poblaciones distintas; no silenciar | C2, D1 | PENDIENTE |
| `F2-DEC-003` | 2026-09-05 | C2 | TENSIÓN A DECLARAR | `RT-06.24` exige videovigilancia propia del recinto, 30 días en línea | la regla negativa 6 prohíbe crear un portal de video y conserva el VMS | declarar que el CCTV del recinto no es el VMS del terminal | C2, C3, D1 | PENDIENTE |
| `F2-COR-001` | 2026-09-05 | C1 | CORRECCIÓN PROPIA | cumplimientos decían `RT-03.01..15` | el capítulo llega a `RT-03.24` | corregido en C1 | C1, C3, C4 | APLICADO |
| `F2-COR-002` | 2026-09-05 | C2 | CORRECCIÓN PROPIA | cumplimientos decían `RT-06.01..24` y omitían el Cap. 7 | rango real `.01..34`, más `RT-07.01..14` | corregido en C2 | C2 | APLICADO |
| `F2-COR-003` | 2026-09-05 | C3 | CORRECCIÓN PROPIA | cumplimientos omitían el Cap. 7 y `RT-10.03` | DR, respaldos y plan de continuidad ISO 22301 | corregido en C3 | C3 | APLICADO |
| `F2-COR-004` | 2026-09-05 | C4 | CORRECCIÓN PROPIA | cumplimientos citaban `RT-09.02` y no `RT-09.01` | `RT-09.01` es el que exige el cálculo de capacidad | corregido en C4 | C4 | APLICADO |

## 2. Detalle de los escalamientos

### `F2-ESC-003` — El Capítulo 7 del BTT no está citado en ninguna parte de Célula 3

**Verificación.** `grep -rn "RT-07" Celula3/` no devuelve ninguna línea. Tampoco aparece «Capítulo 7» ni «site secundario».

**Qué es lo que falta.** `FEP02`, Cap. 7 — *Site secundario y recuperación ante desastres*, `RT-07.01` a `RT-07.14`, catorce requisitos, once de ellos obligatorios.

**Por qué importa aquí.** `T21-4.2-E` «Data center secundario» es un elemento formal evaluado dentro del 16 % de arquitectura física, y la matriz global lo asigna a C2/C3. Además, el checklist del Capítulo C del BTT lo exige dos veces: entregable N° 8 *«Especificación del site principal y del site secundario, con planos»* (Caps. 6 y 7) y entregable N° 9 *«Plan de recuperación ante desastres y política de respaldo»* (Cap. 7).

**Qué se perdió.** El Maestro §9.2 absorbió cuatro de los catorce en su tabla de umbrales —RTO ≤4 h, RPO ≤15 min, prueba semestral con conmutación real, respaldo 3-2-1-1-0— pero sin citar el capítulo de origen, de modo que el resto quedó invisible. Entre lo omitido, lo que en este caso es argumento y no trámite:

| Código | Exigencia | Por qué pesa en el Caso 06 |
|---|---|---|
| `RT-07.01` | declarar activo-activo o activo-pasivo **y justificarlo** frente a costo, RTO y complejidad operacional | la complejidad operacional se paga con un área TI de 5 personas |
| `RT-07.02` | declarar la **distancia al sitio principal** y el **análisis de amenazas comunes** | la sala actual está a menos de 300 m del mar, en ambiente salino; un secundario cercano comparte el evento |
| `RT-07.03` | replicación continua **con medición y alertamiento del retraso** | sin esto, el RPO de 15 min es una promesa sin instrumento |
| `RT-07.05` | conmutación **ejecutable por el personal del CLIENTE** tras la transferencia de conocimiento | restricción no negociable 11: TI del CLIENTE son 5 personas |
| `RT-07.06` | procedimiento de **retorno al principal**, probado, con reconciliación de lo generado en contingencia | el Maestro §12 exige retorno de intervenciones, no de una conmutación DR |
| `RT-07.10` `RT-07.11` | respaldos cifrados con clave gestionada aparte, y copias inmutables protegidas **incluso frente a credenciales administrativas comprometidas** | el Maestro solo dice «3-2-1-1-0» |
| `RT-07.13` | por **cada dominio de dato**: frecuencia, retención y tiempo estimado de restauración completa | engancha con las siete retenciones del Maestro §16.1, hoy sin plan de respaldo asociado |
| §7.2 | disponibilidad **99,95 % por componente** —energía, climatización, red, cómputo, motor de BD, portal— | el Maestro lo comprimió a un único «99,95 % infraestructura aplicable» |

**Recomendación.** Incorporar el capítulo completo al Maestro §9.2, y agregarlo a los cumplimientos asignados de C2 y C3. Este frente ya lo aplicó a sus propios contratos (`F2-COR-002` y `F2-COR-003`), pero el Maestro es la autoridad contextual de los tres frentes y el Frente 3 escribe 4.2.12 sobre la misma base.

### `F2-ESC-004` — El rango del site principal está truncado

**Verificación.** `FEP02`, numeral 3.2, dice literalmente: *«Sala técnica principal | El caso requiere cómputo, almacenamiento y procesamiento sustantivos en las instalaciones del CLIENTE. | Se aplican íntegramente los requisitos **RT-06.01 a RT-06.34**.»* El índice del Capítulo A confirma 34 requisitos. El Maestro §10.3 y el contrato de C2 dicen `RT-06.01 a RT-06.24`, reproduciendo la fórmula «se aplican íntegramente», lo que hace que se lea como cita textual.

**Qué queda fuera.** Tres subcapítulos completos, todos del Frente 2:

- **6.7 Respaldo y custodia de medios** (`RT-06.26` a `RT-06.28`): servicio de custodia para el sitio primario en medio físico transportable, recinto de custodia con exigencias de luminosidad, humedad y ventilación, e inventario de medios con rotación, verificación periódica de legibilidad y registro de movimientos. Es una fila de T-11 que hoy nadie tiene, y es el soporte físico del «una fuera de sitio, una inmutable» del 3-2-1-1-0.
- **6.8 Espacio de operación del personal** (`RT-06.29` a `RT-06.31`): espacio habilitado con estaciones de trabajo, telefonía y conexión, **separado de la sala de equipos**, que no obligue a entrar al recinto técnico para las labores habituales. `RT-06.31` permite reutilizar instalaciones sanitarias y zonas de emergencia existentes, con declaración expresa.
- **6.9 Rutas de comunicaciones** (`RT-06.32` y `RT-06.33`): acceso a las redes por **rutas físicas distintas, con ingreso al edificio por puntos separados**, y provisión de toda la canalización necesaria.

**Consecuencia sobre `ADR-005`.** `RT-06.32` es un criterio de descarte citable para la alternativa «remediar la sala actual»: si el edificio no admite dos entradas físicas separadas, la alternativa cae por una obligación del BTT y no por preferencia del proponente. Lo mismo `RT-06.29`/`RT-06.30` frente a una sala de 34 m².

### `F2-ESC-005` — El checklist del Capítulo C del BTT no está incorporado

**Verificación.** El Capítulo C del BTT es una *Checklist de entregables de la oferta técnica*: 28 filas con entregable, el código o capítulo que lo exige y el Sobre en que se presenta. En Célula 3 no hay ninguna referencia a él.

**Seis de esas filas son del Frente 2**, y dos no tienen hoy producto asignado en ningún contrato:

| N° | Entregable exigido | Exigido en | Estado en el Frente 2 |
|---:|---|---|---|
| 3 | tabla de emplazamiento nube/on-premise justificada | Cap. 3 | cubierto por C1 |
| 8 | especificación del site principal y del secundario, **con planos** | Caps. 6 y 7 | C2 ofrece «plano conceptual»; el secundario no estaba |
| 9 | **plan de recuperación ante desastres y política de respaldo** | Cap. 7 | **sin producto asignado**; C3 solo tiene el plan de pruebas |
| 10 | especificación del hardware y de los dispositivos de terreno | Cap. 8 | cubierto por C2 |
| 11 | cálculo de capacidad y dimensionamiento | `RT-09.01` | cubierto por C4; el código no estaba citado |
| 12 | **plan de continuidad del negocio conforme a ISO 22301** | `RT-10.03` | **sin producto asignado**; `STD-07` lo asigna a C3/D1 sin entregable |

**Recomendación.** Incorporarlo como columna o bloque de control en la matriz global §2. Es la lista contra la cual el evaluador puede verificar mecánicamente si falta algo, y hoy nuestra matriz no la reproduce.

### `F2-ESC-006` — Cuatro colisiones de código `RT` en los capítulos del Frente 2

**Contexto.** El Maestro §1.1 ya establece la regla correcta —*«Nunca citar solo `RT-xx.xx`. La referencia mínima es documento + capítulo/numeral + código + materia»*—, pero no enumera qué códigos colisionan en los capítulos de este frente. El Supuesto M de Célula 2 documenta cinco colisiones (`RT-05.10`, `RT-16.14`, `RT-16.21`, `RT-16.30`, `RT-21.06`), ninguna de ellas de infraestructura.

**Contraste código por código.** Se revisaron los ocho códigos de los capítulos 3, 6, 9 y 10 que el Cap. 15 del caso reutiliza:

| Código | `FEP02` (BTT) | `FEP03`, Cap. 15 (caso) | Lectura |
|---|---|---|---|
| `RT-03.10` | autonomía on-premise ≥24 h **«o el mayor que fije el caso»** | 72 h continuas | **coincide** — el caso fija el valor; uso correcto de «según caso» |
| `RT-03.13` | declarar qué funciones **no** estarán disponibles en modo desconectado | sincronización tras la reconexión ≤90 min | **colisión** |
| `RT-03.24` | calidad de servicio y priorización de tráfico *(Deseable)* | red de los sitios operacionales: rediseño del patio y radiopropagación con patio cargado | **colisión** — esa materia es `RT-03.23` en el BTT |
| `RT-06.01` | espacio de uso exclusivo, aislado, con acceso independiente | tipología del emplazamiento: sala de 34 m² de 2012 que debe habilitarse o reemplazarse | **colisión parcial** — materias vecinas, no iguales |
| `RT-09.01` | presentar el **cálculo de capacidad** con sus supuestos | transacción operacional crítica: confirmación de movimiento ≤1 s | **colisión** |
| `RT-09.02` | soportar la concurrencia y el volumen que fije el caso | se deriva de la volumetría del numeral 14.1 | **coincide** |
| `RT-10.05` | mantenimientos fuera de la ventana crítica, aviso ≥10 días hábiles | 24x7x365; congelamiento 15-dic a 30-abr | **coincide** |

**Riesgo concreto.** El Maestro §4.6 lleva a su tabla de umbrales «desconexión 72 h» y «sincronización ≤90 min» sin código. Si alguien los cita como `RT-03.10` y `RT-03.13` a secas, un lector del BTT encontrará «autonomía de 24 h» y «declaración de funciones no disponibles». El T-12 exige responder los 374 códigos uno por uno: una cita cruzada se detecta ahí de inmediato.

**Recomendación.** Ampliar el listado del Maestro §1.1 con estos cuatro, y anotar los tres que sí coinciden, porque saber cuáles **no** colisionan también evita duplicar trabajo.

### `F2-ESC-007` — La línea base de Célula 2 quedó desfasada

**Verificación.** Maestro §2.2 declara 138 RF (82 Etapa 1 + 56 Etapa 2), 84 RNF, 10 reglas de negocio; `MC-19` en §18.1 dice «138 RF normalizados». Tras la segunda y tercera ronda de corrección de Célula 2, el estado vigente es **139 RF (82 + 57)**, **91 RNF**, **11 reglas**, 21 decisiones y 25 supuestos.

**Origen de la diferencia.** `B1` agregó `RNF-DES-09..12` y `RNF-DIS-13..15` (84 → 91); `B2` creó `RF-POR-09` (138 → 139, Etapa 2, de ahí 56 → 57); `B4` creó `RN-11` (10 → 11).

**Además.** La regla de lectura 5 del propio Maestro dice: *«Si el proyecto pasa a un repositorio Git, se debe registrar en este encabezado el commit que congela Célula 2.»* El repositorio ya existe y ese commit es **`c4756df`**. Mientras no se registre, el Maestro sigue declarando como corte «la versión auditada del 2026-09-04», que ya no es la vigente.

**Nota para el Frente 2.** Ninguna de las cifras de dimensionamiento cambia: los siete RNF nuevos son de desempeño y disponibilidad, y `RF-POR-09` es un canal de presentación documental sin volumen propio declarado. El impacto es de cita y de conteo, no de capacidad.

### `F2-ESC-008` — Ingresos físicos de comunicaciones del edificio administrativo

**Qué falta.** `RT-06.32` del BTT exige que *«el acceso a las redes de comunicaciones estará provisto a través de rutas físicas distintas, con ingreso al edificio por puntos separados»*. El CP, Cap. 6 declara que hoy existe fibra de un solo proveedor con respaldo por radioenlace, pero no dice si el edificio administrativo admite dos ingresos físicos separados de canalización.

**Por qué bloquea.** Es un posible criterio de descarte **por norma** para la alternativa A de `ADR-005` —endurecer la sala actual—, anterior a cualquier comparación de costo u operabilidad. Sin el dato, el ADR debe cerrarse por criterios secundarios, que es una decisión más débil y más objetable.

**Cómo se levanta.** Inspección del edificio administrativo o consulta al CLIENTE sobre canalizaciones existentes y puntos de acometida disponibles. Mientras tanto, C1 lo declara abierto y no presume la respuesta en ninguna dirección.

### `F2-ESC-009` — La elección de proveedor y región de nube no tiene ADR asignado

**Qué exigen las bases.** `RT-03.01` del BTT obliga a declarar el proveedor de nube pública y las regiones primaria y secundaria, con presencia de región o zona en Chile o Sudamérica. `RT-15.04` obliga a declarar la **intensidad de carbono de la región escogida**, y `RT-15.05` valora escoger la de menor intensidad cuando latencia y regulación lo permitan, *«con el análisis comparativo correspondiente»*.

**Por qué es un ADR.** Tiene alternativas reales, criterios vinculados al caso, consecuencias sobre las otras vistas y riesgo residual: es exactamente la definición del Registro ADR Global. El índice `ADR-001` a `ADR-010` no la contempla, de modo que hoy la decisión se tomaría de hecho, sin registro, al escribir el primer nombre de proveedor en un documento.

**Criterios propuestos para `ADR-011`.** Presencia de región en Chile o Sudamérica y número de zonas de disponibilidad; latencia medida al terminal; intensidad de carbono declarada de la región; cobertura del catálogo de servicios gestionados frente a la pila de C2 §3; certificaciones y residencia de datos frente a la condición de operador de importancia vital del `CP, Cap. 10`, restricción 7; y esfuerzo de reversibilidad conforme a `RT-03.07`.

**Por qué no la resuelve este frente.** Afecta a la arquitectura lógica del Frente 1, a los controles y la residencia de datos del Frente 3, y a la estructura de costos que el Art. 16 exige que sea coherente con la arquitectura. Se propone, no se decide.

### `F2-ESC-010` — El ambiente de recuperación ante desastres vence en el mes 6, no al pasar a producción

**Las tres piezas.** El BTT, numeral 4.1, define **cinco** ambientes, incluido Recuperación ante desastres. `RT-04.01` dice: *«Los cinco ambientes del numeral 4.1 estarán habilitados y operativos **como condición del hito H3** del Formulario E-25.»* El Formulario E-25 de las BA describe H3 como *«Entrega de la infraestructura híbrida y habilitación de los ambientes de Desarrollo, QA, Preproducción y Producción, con observabilidad operativa»*, en el **mes 6**, con el 10 % de la estructura de pagos. El Art. 24 de las BA, por su parte, habla de *«cuatro ambientes obligatorios»*.

**Por qué no es una contradicción.** El Art. 5.2 de las BA establece que los documentos *«conforman un todo integrado y se complementan recíprocamente. Toda obligación que aparezca en cualquiera de ellos se entenderá parte del Contrato, aunque no se repita en los demás»*. El DR no falta en las BA: tiene artículo propio, el 20°. Y el Art. 5.4 da por aceptada la interpretación más exigente una vez presentada la oferta, sin posibilidad de invocar la contradicción después.

**Qué significa en la práctica.** La región secundaria, la replicación continua y el procedimiento de conmutación de `RT-07.05` deben existir y funcionar en el **mes 6**, es decir **diez meses antes** de que la Etapa 1 entre en producción en el mes 16. Una planificación que deje el DR para el final del desarrollo no cumple H3, que es un hito de pago con criterio de aceptación.

**Por qué se escala.** Excede al Frente 2: cambia el cronograma y la Carta Gantt del Subdocumento 7, la curva de consumo de infraestructura y la secuencia de pruebas. Este frente lo asume en su calendario y en C2 §6, pero la decisión de planificación no es suya.

## 3. Tensiones declaradas, no resueltas

### `F2-DEC-002` — Biometría

`RT-06.20` exige que el ingreso al recinto técnico se controle *«mediante seguridad física y control de acceso biométrico basado principalmente en biometría facial, con AFIS como respaldo»*. La restricción no negociable 8 del Maestro registra que **la biometría obligatoria fue objetada**, y el Maestro §11.2 pide credencial temporal para eventuales *«sin biometría obligatoria»*.

No son la misma cosa: una es el acceso de un puñado de personas a un recinto técnico cerrado; la otra es el control de hasta 380 eventuales por turno en el recinto portuario. La arquitectura las trata por separado y **lo dice**, en lugar de dejar que el evaluador encuentre la palabra «biometría» en los dos lados y saque su propia conclusión.

### `F2-DEC-003` — Videovigilancia del recinto

`RT-06.24` exige videovigilancia y monitoreo IP del recinto técnico, con al menos 30 días en línea y respaldo posterior. La regla negativa 6 del Maestro prohíbe *«crear un portal de video»* y conserva el VMS existente como interfaz de video del terminal; la regla 7 prohíbe llevar video completo por la red operacional sin necesidad demostrada.

Tampoco son la misma cosa: el CCTV del recinto técnico es un control de seguridad física de nuestra propia instalación, con su propio almacenamiento y su propia red, y no se integra al VMS de las 142 cámaras del terminal ni a su tráfico. Se declara así en C2 y se coordina con D1.

## 4. Acciones pendientes de otro

| Quién | Qué |
|---|---|
| Integrador | resolver `F2-ESC-003` a `F2-ESC-007` en la puerta de integración |
| Líder de proyecto | asignar responsables y revisores cruzados en la tabla de control del Plan, hoy en `POR ASIGNAR` |
| Frente 3 | `F2-DEC-002` y `F2-DEC-003` afectan D1; confirmar el tratamiento antes de la Puerta 2 |
