# Decisiones y escalamientos — Frente 2

**Regla que gobierna este archivo.** `README.md` de Célula 3: *«Si se detecta una contradicción, **no se resuelve silenciosamente**: se aplica la jerarquía indicada en el Maestro y se registra el conflicto en `DECISIONES_Y_ESCALAMIENTOS.md`.»* Y `00_MAESTRO`, §1, que a su vez remite a `FEP01, Art. 5.1–5.4`: **la precedencia contractual la encabezan las Bases Administrativas y sus anexos**, seguidas de las Bases Técnicas del caso y sus anexos y de las aclaraciones y modificaciones formales, en el orden que ese artículo indica. Los PDF oficiales prevalecen sobre el material propio de trabajo, pero **entre sí no se ordenan como `FEP03 > FEP02 > FEP01`**: `FEP02 §1.3` establece que las Transversales desarrollan las Administrativas sin rebajarlas, y que el caso puede endurecer el piso transversal, no bajarlo. Dentro de un mismo documento rige la disposición más exigente (`Art. 5.3`) y la ambigüedad real se consulta (`Art. 5.4`).

> *Corrección `F2-COR-008` (2026-09-06).* Esta cabecera decía «prevalecen los PDF oficiales (`FEP03` > `FEP02` > `FEP01`)» **atribuyéndoselo al Maestro §1, que dice lo contrario**. Era una jerarquía inventada, y del lado equivocado: habría permitido descartar una obligación administrativa o transversal por una lectura técnica. Detectado por la auditoría global pre-D3 como `AGC3-001` y verificado contra el texto del Maestro y del `FEP01, Art. 5`.

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
| `F2-ESC-011` | 2026-09-05 | C4 | EXTERNO | tamaño real de imagen de los lectores de patente y contenedor | el supuesto propio de 500 KB gobierna el **91 % del buffer de 72 h**, el ancho de banda de reposición y el 100 % del almacenamiento documental. A 1 MB el buffer sube a 40 GB y la reposición a 58 Mbps | solicitar el tamaño real que producen los lectores actuales; entretanto el margen del 30 % absorbe hasta ≈650 KB | C2, C3, C4, T-11 | BLOQUEADO EXTERNO |
| `F2-ESC-012` | 2026-09-05 | C3/C4 | EXTERNO | capacidad real de la fibra y del radioenlace de respaldo | la sincronización en ≤90 min exige **32,5 Mbps sostenidos** a peak estacional; el caso describe el respaldo como «de menor capacidad» | solicitar la capacidad contratada de ambos enlaces; si el respaldo no la sostiene, el compromiso de `RNF-DIS-04` se cumple sobre el principal restablecido o sobre el segundo camino de `RT-03.17` | C3, C4, `RNF-DIS-04` | BLOQUEADO EXTERNO |
| `F2-INT-001` | 2026-09-05 | C1..C4 | INTERCAMBIO CUMPLIDO | cruce con `SEC-PHYS-v0.1` del Frente 3 | 17 grupos emplazados en C1 §6.bis, con producto en C2 §8.bis, zonas y flujos en C3 §5.bis y clasificación T-11 en C4 §9.bis | cerrar `F3-DEP-003` contra este material; `B7-F05` quedó superado | D1, D2, D3 | **APLICADO** |
| `F2-ESC-013` | 2026-09-05 · **acotado 2026-09-06** | C4 | EXTERNO | ingesta del registro de seguridad | **la política ya existe:** D1 `B5.2.1` admite al 100 % seguridad, auditoría y alertas obligatorias, y deja la telemetría operacional cruda en su dominio — confirma el método de C4 §9.ter. Lo que falta ahora es **medición**, no política: los registros de plataforma, red y borde siguen sin cuantificar y suelen dominar | medir fuentes, EPS, tamaño y peaks; la clasificación campo→sensibilidad sigue en `F3-DEP-004` (Subdocumento 5 y CLIENTE). Destino: `T11-C2-19` | C4, D1, T-11 | BLOQUEADO EXTERNO, **alcance reducido** |
| `F2-ESC-014` | 2026-09-06 | C1 | COLISIÓN DE IDs + BRECHA | los códigos `SPOF-01` a `SPOF-10` significan materias distintas en C1 y en el `B4` de D2 | ninguno de los diez coincide; D2 es el dueño del registro consolidado, que es su producto obligatorio | C1 renumera a `F2-SPOF-*`; D2 conserva la numeración global. **Cuatro puntos de falla de C1 no están en el registro de D2** y deben incorporarse | D2, D3, consolidado §4.3 | **APLICADO** en C1; traspaso a D2 pendiente |
| `F2-INT-002` | 2026-09-06 | C1, C3, C4 | INTEGRACIÓN CUMPLIDA | consumo de A2, A3 y D2 §B5 | A3 §7 corrigió la columna de fallback manual de C3; A3 §3 aportó la autoridad por bloque; A2 confirmó que ninguna contraparte altera el ancho de banda; D2 §B5 amarró `ADR-005` y `ADR-007` a SPOF y amenazas | avisar a F1 y F3 que su material quedó consumido | F1, F3 | **APLICADO** |
| `F2-ESC-015` | 2026-09-06 | — | CITA PROPAGADA | el rango truncado `RT-06.01 a RT-06.24` reaparece en la fila de `ADR-005` de D2 §B5 | es el tercer documento donde se propaga, tras el Maestro §10.3 y el contrato original de C2. El BTT exige hasta `RT-06.34` | corregir en el Maestro cierra la fuente; avisar a D2 | Maestro, D2, C2 | PARA REVISIÓN DEL INTEGRADOR |
| `F2-ESC-016` | 2026-09-06 | — | DIAGNÓSTICO DESFASADO | D2 §B5 afirma que «`ADR-001` a `ADR-007` están en `CANDIDATO` y todavía no tienen contenido: sus autores son A1, A2, A3 y C1–C4, que siguen en plantilla» | era cierto para `main`; hoy A3 tiene `ADR-002` y `ADR-004` redactados, C1 §7 desarrolla las tres alternativas de `ADR-005`, y C2/C4 alimentan `ADR-007` | avisar a D2 para que B6 no parta de un inventario vacío | D2, D3 | PARA REVISIÓN |
| `F2-DEC-002` | 2026-09-05 | C2 | TENSIÓN A DECLARAR | `RT-06.20` exige biometría facial para el recinto técnico | la restricción no negociable 8 registra la objeción a la biometría obligatoria | declarar que son poblaciones distintas; no silenciar | C2, D1 | PENDIENTE |
| `F2-DEC-003` | 2026-09-05 | C2 | TENSIÓN A DECLARAR | `RT-06.24` exige videovigilancia propia del recinto, 30 días en línea | la regla negativa 6 prohíbe crear un portal de video y conserva el VMS | declarar que el CCTV del recinto no es el VMS del terminal | C2, C3, D1 | PENDIENTE |
| `F2-COR-001` | 2026-09-05 | C1 | CORRECCIÓN PROPIA | cumplimientos decían `RT-03.01..15` | el capítulo llega a `RT-03.24` | corregido en C1 | C1, C3, C4 | APLICADO |
| `F2-COR-002` | 2026-09-05 | C2 | CORRECCIÓN PROPIA | cumplimientos decían `RT-06.01..24` y omitían el Cap. 7 | rango real `.01..34`, más `RT-07.01..14` | corregido en C2 | C2 | APLICADO |
| `F2-COR-003` | 2026-09-05 | C3 | CORRECCIÓN PROPIA | cumplimientos omitían el Cap. 7 y `RT-10.03` | DR, respaldos y plan de continuidad ISO 22301 | corregido en C3 | C3 | APLICADO |
| `F2-COR-004` | 2026-09-05 | C4 | CORRECCIÓN PROPIA | cumplimientos citaban `RT-09.02` y no `RT-09.01` | `RT-09.01` es el que exige el cálculo de capacidad | corregido en C4 | C4 | APLICADO |
| `F2-COR-005` | 2026-09-06 | C1 | CORRECCIÓN PROPIA | `CTX-VESSEL` estaba solo en nube pese a ser `Crítica` en A1 | contradecía a A1 §3.1, a A3 y a la propia matriz de continuidad de C3 §7: con esa asignación el corte de enlace habría detenido la atención de nave, contra `CP, Cap. 15, RT-03.10` | `PHY-OPS-01` incorpora `CTX-VESSEL`; la mensajería EDIFACT sigue en cola en `INT-HUB`. Hallazgo `B6-F03` de D2 | C1, C3, C4, `ADR-002` | APLICADO |
| `F2-COR-006` | 2026-09-06 | C1 | CORRECCIÓN PROPIA | seis diferencias de criticidad con A1 y ubicación de `CH-CAB` | la criticidad es atributo del catálogo lógico de A1, no de C1; y `CH-CAB` es canal de cabina **y de terreno**, no solo de muelle | C1 §5 adopta los valores de A1 y §5.1 declara el criterio; `CH-CAB` pasa a `PHY-EDG-04` + `PHY-EDG-02` + `PHY-EDG-01`. Hallazgo `B6-F04` de D2 | C1, D1, D2 | APLICADO |
| `F2-COR-008` | 2026-09-06 | trazabilidad | CORRECCIÓN PROPIA | **jerarquía contractual invertida y mal atribuida** | la cabecera de este archivo decía «prevalecen los PDF oficiales (`FEP03` > `FEP02` > `FEP01`)» **citándolo como del Maestro §1, que dice lo contrario**: `FEP01, Art. 5.1–5.4` pone primero las Bases Administrativas | corregida la cabecera con la regla real; ninguna decisión de este registro se había tomado usando la fórmula errónea, verificado una por una | todos | APLICADO |
| `F2-COR-009` | 2026-09-06 | C2 | CORRECCIÓN PROPIA | el rango truncado `RT-06.01..24` seguía **vigente en las reglas normativas** de C2 | `F2-COR-002` agregó la nota de corrección pero dejó en pie la regla equivocada de la línea 58. Cuarta aparición del rango truncado, tras el Maestro §10.3, el contrato de C2 y D2 §B5 | corregido a `RT-06.01` a `RT-06.34` en la propia regla | C2, C4, `ADR-005` | APLICADO |
| `F2-COR-010` | 2026-09-06 | C1..C4, trazas | CORRECCIÓN PROPIA | citas ambiguas de códigos colisionados y una familia RNF inexistente | contra la regla del Maestro §1.1 —*documento + capítulo + código + materia*—: `RT-05.10` y `RT-09.01` citados sin documento en cuerpo sustantivo, `RT-06.01` en la tabla de alternativas de sala, y «RNF-ARQ» en `TRZ-C1-001`, familia que Célula 2 no tiene | desambiguadas las cuatro; retirada «RNF-ARQ» y citado `BTT, Cap. 2, RT-02.01` | C1, C4, trazas | APLICADO |
| `F2-COR-011` | 2026-09-06 | C1..C4 | CORRECCIÓN PROPIA | dos «Definición de terminado» por documento, ambas legibles como estado | el contrato deja casillas sin marcar y la sección final las marca; un lector concluía pendiente y cumplido a la vez (`AGC3-019`) | la del contrato queda rotulada como **lista normativa, no estado**, remitiendo a la sección de estado vigente | C1..C4 | APLICADO |
| `F2-COR-007` | 2026-09-06 | C2/C4 | CORRECCIÓN PROPIA | doble conteo de la plataforma de observabilidad y SIEM | `T11-C2-19` y `T11-SEC-04` eran la misma plataforma vista dos veces; `RT-03.16` exige una sola para nube y on-premise | fusionadas en `T11-C2-19`; `T11-SEC-04` se conserva como ancla de trazabilidad sin fila propia. Hallazgo `B6-F05` de D2 | C2, C4, T-11, integrador | APLICADO |
| `F2-ESC-017` | 2026-09-06 | C1 | PROPUESTA DE CAMBIO A OTRO FRENTE | criticidad de `SRV-IAM` | A1 la declara `Alta`; C1 la había puesto `crítica`. Por la escala de A1, «debe sobrevivir 72 h e ir en `EDGE-RUN`» **es** la definición de crítica, y sin autenticación local las cinco funciones críticas no se operan durante el corte | C1 adopta el valor de A1 en la tabla y propone a Frente 1 elevar `SRV-IAM` a `Crítica`. El dimensionamiento no cambia: la capacidad local ya está especificada | A1, D1, `ADR-008` | PARA REVISIÓN DE FRENTE 1 |
| `F2-INT-003` | 2026-09-06 | C1 | RESPUESTA A OTRO FRENTE | brecha `ACT-TI` / consola de administración (`F1-OBS-002`) | la brecha es de A1 y no se cierra aquí, pero su resolución podría reabrir emplazamiento y T-11 a última hora | C1 §5.2 responde el lado físico por anticipado: la administración vive en `PHY-OPS-06` sobre `Z-MGMT` vía `PHY-CLD-02`/`PHY-OPS-04`; **no aparece nodo nuevo ni fila nueva de T-11** | A1, D1, D3 | **APLICADO** |

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

### `F2-ESC-011` — El tamaño de imagen es el supuesto más sensible de todo el dimensionamiento

**De dónde viene.** La plantilla de volumetría de Célula 2 declara, como supuesto propio y marcado, **500 KB por imagen** de reconocimiento de patente y de contenedor, junto con una cobertura óptica del 20 % de los movimientos de patio.

**Qué gobierna.** Al recalcular el buffer de 72 horas a peak estacional, las imágenes resultan ser **19,9 de los 21,9 GB**, es decir el 91 %. Y como el ancho de banda de reposición se deriva de ese volumen, gobierna también los 32,5 Mbps de la sincronización, además del 100 % del almacenamiento documental en nube.

**Sensibilidad.** Si el tamaño real fuera 1 MB, el buffer sube a ≈40 GB, la sincronización en 90 minutos exige ≈58 Mbps y el almacenamiento documental pasa de 1,43 a 2,9 TB anuales. Es el único supuesto del modelo cuyo error cambia el diseño y no solo la cifra.

**Cómo se trata mientras tanto.** El margen del 30 % declarado en `RT-08.05` absorbe hasta unos 650 KB por imagen sin rehacer nada. Por sobre eso hay que revisar el enlace y el buffer. Se solicita al CLIENTE el tamaño que producen sus lectores actuales, que es un dato que tiene.

### `F2-ESC-012` — No sabemos si el enlace de respaldo sostiene la sincronización

**El compromiso.** `RNF-DIS-04` y el `CP, Cap. 15, RT-03.13` obligan a sincronizar en **≤90 minutos** tras 72 horas de desconexión. A peak estacional eso exige **32,5 Mbps sostenidos**, además del tráfico de la operación en curso, porque el terminal no se detiene mientras sincroniza.

**El problema.** El `CP, Cap. 6` describe el respaldo como *«radioenlace de menor capacidad»* y advierte que *«no se ha probado en conmutación real desde 2022»*. Si el corte de 72 horas fue causado por la caída de la fibra y la reconexión ocurre estando aún sobre el radioenlace, el compromiso de 90 minutos **puede no ser alcanzable**.

**Cómo se trata.** El compromiso se declara sobre el enlace principal restablecido o sobre el segundo camino que `RT-03.17` obliga a proveer, dimensionado a esta cifra. No se promete sobre un respaldo cuya capacidad no conocemos. Se solicita al CLIENTE la capacidad contratada de ambos enlaces.

### `F2-INT-001` — Cruce con `SEC-PHYS-v0.1` y respuesta a `B7-F05`

**Qué se hizo.** Los 17 grupos del paquete temprano del Frente 3 quedaron emplazados, con producto de referencia, zona, conducto y clasificación T-11, en los cuatro paquetes de este frente.

**Lo que este frente le devuelve al Frente 3.** La auditoría B7 de D1 registró en `B7-F05` que *«A1–A3 y C1–C4 visibles siguen en estructura/plantilla, sin catálogos, contratos, nodos, productos ni cantidades utilizables para validar D1»*, y mantuvo `F3-DEP-003` abierta. Ese diagnóstico era correcto **para el estado de `main` al 2026-09-05**: los cuatro paquetes del Frente 2 estaban en la rama `frente_2`, sin integrar. Con la consolidación existen los nodos `PHY-*`, los productos por clase, las zonas y redes, y el dimensionamiento. **`F3-DEP-003` puede cerrarse contra este material.**

**Tres cosas que el cruce cambió en este frente, y que no venían de nosotros.**

`SEC-KEY-01` obliga a **material de clave protegido en el sitio**. Es la consecuencia física de `ADR-009` de D1 y de la regla negativa 8 del Maestro: un cifrado cuya clave viva solo en nube impide que las cinco funciones críticas lean y escriban durante las 72 h de corte. C2 §8.bis lo incorpora como requisito excluyente.

`FL-10` de D1 destapó un hueco real: *«tiempo, nombres y registros locales no pueden depender solo de nube»*. C3 había dimensionado cómputo, almacenamiento y enlace para el corte, pero no la resolución de nombres, la hora, la validación de certificados ni la caché de identidad. Sin esos cinco, las funciones críticas fallan por una causa ajena a su lógica. Es la nueva §5.ter de C3.

`SEC-END-01` obligó a declarar que **el EDR no cubre los dispositivos de terreno**. Los equipos de las cinco clases marinas son de fabricantes industriales cuyo soporte de agente no está confirmado, y el `CP, Cap. 11` prohíbe imponer software al fabricante. Se cubren por segmentación y por la gestión de flota de `RT-03.18`. Contar una licencia por dispositivo habría inflado el T-11 con algo no instalable.

**Lo que sigue abierto.** El dimensionamiento de la ingesta del registro de seguridad. *Actualizado el 2026-09-06:* la **política** ya la entregó D1 en `B5.2.1` y confirma el método de C4 §9.ter; lo que falta es **medir** los registros de plataforma, red y borde, y la clasificación campo→sensibilidad que D1 mantiene como `F3-DEP-004`. Su destino es `T11-C2-19`, no una fila propia (`F2-COR-007`). La **unidad** está declarada; el **valor** no se inventa.

### `F2-ESC-006 bis` — La lista verificada de colisiones `RT` son once, no cinco ni diez

**Cómo se obtuvo.** Se extrajeron mecánicamente los **374 códigos `RT` del BTT** y los **27 del Capítulo 15 del Caso 06**, y se comparó materia contra materia. Los 27 del caso reutilizan códigos del BTT; en **once** la materia es distinta. Además se verificaron las **970 citas de código `RT`** que hacen los tres frentes en Célula 3: **ninguna cita un código inexistente**.

| Código | Materia en el BTT | Materia en el `CP, Cap. 15` | ¿Estaba documentada? |
|---|---|---|---|
| `RT-03.13` | declarar qué funciones **no** están disponibles offline | sincronización tras reconexión ≤90 min | `F2-ESC-006` |
| `RT-03.24` | calidad de servicio y priorización de tráfico | rediseño de la red del patio | `F2-ESC-006` |
| `RT-05.10` | catálogo de datos con linaje | retención de históricos y auditoría | Supuesto M |
| `RT-05.15` | históricos **no** migrados en repositorio de consulta | históricos **a** migrar | **no, es nueva** |
| `RT-06.01` | encabezado de rango del numeral 6 | tipología del emplazamiento on-premise | `F2-ESC-006` |
| `RT-09.01` | cálculo de capacidad con supuestos | transacción operacional crítica ≤1 s | `F2-ESC-006` |
| `RT-15.02` | apagar ambientes no productivos fuera de horario | certificaciones sectoriales ISPS | `F2-ESC-006` |
| `RT-16.14` | motor de reglas sin recompilación | firma electrónica | Supuesto M |
| `RT-16.21` | plantillas de notificación administrables | canales de notificación y escalamiento | Supuesto M |
| `RT-16.30` | registro de exportación de información sensible | portal público | Supuesto M |
| `RT-21.06` | SLA del centro de atención: 80/20, FCR 70 %, abandono ≤5 % | horario del centro de atención | Supuesto M |

**Dos casos que no son colisión pero se registran para que nadie los lea como una.** `RT-13.12`: el caso conserva la materia (multiidioma) pero **cambia la clasificación**, y lo dice literalmente — «Obligatorio, y no deseable como en el documento transversal». Es el único código que reclasifica al BTT de forma explícita. `RT-21.16`: el caso declara «no exigible en los términos del documento transversal» el traslado a sitios alejados, **porque toda la operación ocurre en un emplazamiento** — es una constatación fáctica, no un rebaje del piso de `FEP02 §1.3`, y conviene decirlo así.

**Qué hay que hacer con esto.** El Supuesto M de Célula 2 documenta cinco; el Maestro §1.1 fija la regla de cita pero no lista los códigos. Esta tabla los reemplaza a ambos como lista de referencia. Corresponde al integrador llevarla al Maestro §1.1 y a Célula 2 actualizar el Supuesto M. Se suma a `F2-ESC-006`, no lo sustituye.

### `F2-ESC-014` — Colisión de identificadores `SPOF` entre C1 y D2, y cuatro puntos de falla que faltan

**Cómo apareció.** Al integrar `frente_3` con el `B4` de D2 recién completado, se comparó su registro consolidado de 21 puntos únicos de falla contra los diez de C1 §8. **Los códigos `SPOF-01` a `SPOF-10` existen en ambos y ninguno significa lo mismo.** Ejemplo: `SPOF-01` es «`EDGE-RUN` y su almacenamiento» en D2 y «fibra de un solo proveedor» en C1.

**Por qué importa.** La sección 4.3 del consolidado reúne ambos registros. Con la numeración cruzada, veintiún identificadores tendrían diez con doble significado, y `RT-02.11` del BTT —que exige declarar los puntos únicos de falla **y justificar por qué son aceptables**— quedaría sin traza seguible.

**Resolución aplicada.** D2 es el propietario formal del registro consolidado: su contrato lo nombra como producto obligatorio. Su numeración queda como la global. Los diez de C1 pasan a `F2-SPOF-01` a `F2-SPOF-10`, con la tabla de correspondencia en C1 §8.1. No se tocó ningún archivo de D2.

**Lo que falta y hay que traspasar a D2.** Cuatro puntos de falla de C1 **no tienen equivalente** en el registro consolidado, y los cuatro son condiciones preexistentes que el `CP, Cap. 6` describe de forma explícita:

| Falta en D2 | Texto del caso que lo respalda |
|---|---|
| operación, administración y CCTV sobre la misma conmutación | *«comparten infraestructura de conmutación […] en eventos de alta actividad se ha observado degradación del acceso al sistema de operación»* |
| 26 tableros del patio refrigerado sin instrumentación remota | *«la falla de un tablero solo se conoce cuando alguien pasa caminando»* |
| generación de respaldo del patio refrigerado nunca verificada a carga total de temporada | *«la autonomía del respaldo del patio refrigerado no está verificada bajo carga total de temporada»* |
| proveedor de nube único | consecuencia del Art. 16; `RT-03.07` obliga a declarar la estrategia de reversibilidad. El `SPOF-20` de D2 es el proveedor de SOC, que es otra cosa |

**Lo que C1 incorporó de D2.** Tres de sus 21 no estaban en este frente y sí le tocan: `SPOF-04` referencia temporal —consecuencia de `FL-10`, tratada en C3 §5.ter pero no declarada como punto de falla—, `SPOF-15` aprobador único de break-glass, y `SPOF-16` dotación de turno con habilitación ISPS. Quedan referenciados en C1 §8.1.

### `F2-INT-002` — Integración de A2, A3 y D2 §B5

**Lo más importante que salió: A3 corrigió un error de este frente.** La matriz de continuidad de C3 §7 proponía procedimientos de papel como respaldo de las cinco funciones críticas —planilla de turno para movimientos, acta en papel para la evidencia—. El `§7` de A3 muestra que eso **contradice el propio diseño**: si el núcleo local sostiene esas funciones durante 72 horas, no hay nada que reemplazar a mano. Lo que se degrada no es la función, es su contraparte externa: la mensajería queda en cola, la conciliación con el TOS se posterga, la verificación contra autoridades usa el carril de excepción que **ya existe hoy**, el reporte agregado se difiere y la entrega al ERP espera. Corregidas las cinco filas.

**De A3 §3, la autoridad por bloque.** El núcleo de registro se sustituye como un solo contexto acotado pero **se despliega bloque por bloque del patio**. Consecuencia física: `PHY-OPS-03` debe sostener autoridad diferenciada por bloque de forma simultánea —pre-cutover, validación y post-cutover conviviendo—, y post-cutover hay escritura dual hacia el TOS para conservar el retorno, que se ejecuta por redirección de enrutamiento en la fachada y no por restauración de datos.

**De A2, la confirmación de que el ancho de banda no cambia.** Ninguna contraparte introduce un término que altere el cálculo de C4 §5.1: el `EXT-TOS12` cursa todo el tráfico transaccional a ~0,27 TPS de peak —coherente con `DIM-02`— pero es flujo **local** y no consume el enlace exterior. El resto son cargas de mensajería. El término dominante sigue siendo el de las imágenes. Los peaks por naviera son cualitativos porque los contratos no están levantados (`F1-ESC-002`).

### `F2-INT-004` — Consumo de la auditoría de cierre de Frente 3

**Qué llegó.** Frente 3 cerró D1 y D2 y publicó su `AUDITORIA_CIERRE.md` con cinco observaciones dirigidas a los Frentes 1 y 2, más dos observaciones de auditoría (`B7-O01`, `B7-O02`). Las que tocan a este frente se resolvieron todas, ninguna en silencio:

| Observación de D2 | Qué era | Cómo se cerró |
|---|---|---|
| `B6-F03` | `CTX-VESSEL` crítico y local en A1/A3, solo en nube en C1 | corregido: `F2-COR-005`, C1 §4, §5 y §5.1 |
| `B6-F04` | seis diferencias de criticidad y ubicación de `CH-CAB` | corregido: `F2-COR-006`, C1 §5 y §5.1 |
| `B6-F05` | posible doble conteo `T11-C2-19` / `T11-SEC-04` | corregido por fusión: `F2-COR-007`, C2 §9 y C4 §9.bis |
| `B7-O01` | `SPOF-13` y `SPOF-22` no deben consolidarse | confirmado y declarado: C2 §4.1 |
| `B7-O02` | la cobertura de 21 nodos es sobre el catálogo declarado, no sobre la instalación real | **se acepta la observación tal cual.** C1 §9 ya condiciona el catálogo al levantamiento de sitio (`F2-ESC-001`, `F2-ESC-008`); no se declara cobertura de la instalación real y no se convertirá en afirmación de cierre |
| `B7.2 #8` | `ADR-011` sin alternativas concretas ni selección | atendido hasta donde el Informe 1 permite: C2 §4.1 acota el espacio de decisión con seis alternativas nombradas, declara los tres datos que faltan y deja una recomendación condicionada. La selección sigue siendo del integrador con el CLIENTE (`F2-ESC-009`) |
| `ACT-TI` | brecha de canal de A1, con posible consecuencia física | respondida por anticipado: `F2-INT-003`, C1 §5.2 |

**Lo que se devuelve a Frente 3.** `F2-ESC-017` (propuesta de elevar `SRV-IAM`) es de Frente 1, pero afecta a `ADR-008`. `F2-ESC-015` y `F2-ESC-016` siguen abiertos hacia D2. Y el traspaso de los cuatro puntos de falla de `F2-ESC-014` al registro consolidado sigue pendiente en D2.

**De D2 §B5, los anclajes de los ADR propios.** `ADR-005` queda amarrado a `SPOF-06` y `SPOF-01`, amenazas `THR-052` y `THR-054`, disparador `ESC-09`, con residual `ESCALADO`. `ADR-007` recibe la consecuencia negativa que no puede omitir: *«respaldo alcanzable por la misma autoridad que puede borrarlo; restauración no probada»*, cubierta por `RT-07.10`, `.11` y `.12` en C2 §6.1.

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
