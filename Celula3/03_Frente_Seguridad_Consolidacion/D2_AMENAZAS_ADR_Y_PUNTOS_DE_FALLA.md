# D2 — Amenazas, ADR y puntos de falla

## Contrato del entregable

### Objetivo y destino

Modelar amenazas y fallos del caso, y consolidar decisiones con alternativas reales. Alimenta la sección 4.3.

### Cumplimientos asignados

- `SD4-04`, `SD4-07`, `SD4-08`.
- BTT RT-02.04/08/09/11; modelado STRIDE por componente e integración.
- Decisiones 1, 9, 19 y 20; riesgos derivados de MC-02/07/08/09/10/11/12/30.

### Entradas obligatorias

- Maestro §§6–19.
- Registro ADR global.
- Inicialmente clases genéricas; luego catálogos A1, A2, C1 y C3 `v0.1`.

### Trabajo requerido

- [x] Identificar activos y fronteras de confianza en versión provisional B1; A1/A2/C1/C3 deben refinar la correspondencia.
- [x] Aplicar STRIDE a canal, gateway, servicio, broker, datos, edge y tercero. B2 dejó `CLS-DAT`/S abierta y **B6 la cerró con `THR-072`**: las siete clases tienen las seis categorías. Cobertura de modelo, no control probado.
- [x] Refinar por componente e integración real en B6, conservando como observación las diferencias que deben corregir sus autores.
- [x] Cubrir TOS, gate/OCR, reefer, app offline, VMS, radio, ERP/autoridades y sincronización en versión provisional B3 (`SCN-01..12`); la lista de funciones no disponibles durante la desconexión sigue abierta por dependencia de A3 y C1–C4.
- [x] Definir amenaza, condición, impacto, control preventivo/detectivo/correctivo y evidencia (`THR-001..073`, incluidas dos agregadas por el cruce B6); toda evidencia es prevista, ninguna ejecutada.
- [x] Consolidar todos los SPOF y su aceptabilidad (`SPOF-01..22`, incluido uno agregado por B6); ninguno aceptado, 11 escalados fuera del alcance de los frentes.
- [x] Revisar ADR de estilo, runtime, integración, TOS, sala, red, datos e identidad en versión provisional B5; `ADR-001..007` en revisión de suficiencia porque aún no tienen contenido.
- [x] Registrar consecuencias negativas y disparadores de revisión para los diez ADR en B5.2/B5.3; D2 no promovió ni aprobó ninguno en su corte. El ajuste posterior del autor deja `ADR-008` `PROPUESTO` condicionado.

### Matriz STRIDE obligatoria

La fila siguiente es ilustrativa del formato exigido. La matriz efectiva se desarrolla en `B2.3`–`B2.4`, donde cada amenaza se presenta en dos tablas unidas por el identificador `THR-*`.

| ID | Activo/componente | Frontera | S/T/R/I/D/E | Escenario portuario | Prob. | Impacto | Control preventivo | Detección | Respuesta/evidencia | Riesgo residual | Estado |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `THR-xxx` | app offline | dispositivo↔plataforma | POR CLASIFICAR | pérdida/robo + cola local | — | — | cifrado/sesión | telemetría | revocación/auditoría | — | ILUSTRATIVA |

### Registro SPOF obligatorio

| SPOF | Vista/componente | Escenario | Impacto | Mitigación | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| ver `B4.2`–`B4.6` | — | — | — | — | — | — | — | DESARROLLADO EN B4 |

### Productos obligatorios

1. Modelo de amenazas por componente/integración.
2. Registro de SPOF.
3. ADR revisados y registro global actualizado.
4. Vista de fronteras de confianza.
5. Resumen de riesgo residual listo para consolidar.

### Aporte T-11/ADR

Valida que los controles físicos/licencias tengan respaldo en riesgo real y que ningún ADR omita impacto en T-11.

### Salidas hacia otros frentes

- Observaciones accionables por componente, no recomendaciones genéricas.
- Requisitos de redundancia, aislamiento, logging o retorno que deban incorporarse.

### Definición de terminado

- [ ] Todo componente/integración relevante tiene amenazas y controles.
- [ ] Todos los SPOF subsistentes están declarados.
- [ ] Cada ADR compara al menos dos alternativas y consecuencias.
- [ ] Riesgos residuales tienen aceptación o escalamiento.
- [ ] No se presentan controles sin evidencia verificable.
- [ ] `TRZ_D2.md` completo.

## Plan de desarrollo acordado

**Estado:** desarrollo técnico `EN CURSO` desde 2026-09-05. Los bloques B1 a B6 están redactados; B5 fue revalidado y B6 cruzó los paquetes reales de A1–A3 y C1–C4 sin corregir silenciosamente sus diferencias. B7 es el siguiente bloque y debe auditar la cobertura y las observaciones de ese cruce. Por decisión de secuencia, **B8 completo —diagramas y resumen residual— queda diferido hasta integrar y auditar la cobertura**; no se producirá una versión parcial. Desde B4 el desarrollo usa **modo registro**. Ningún riesgo queda aceptado por el solo hecho de estar descrito.

### Uso de los archivos

- **Este D2:** contrato, plan, activos, fronteras, amenazas, SPOF, revisión de ADR y resumen de riesgo. Solo contenido aprobado pasa a «Contenido listo para integrar».
- **TRZ_D2:** cadena fuente → activo/frontera → amenaza o fallo → control/decisión → evidencia. No duplica la narrativa ni convierte una prueba prevista en prueba ejecutada.
- **DECISIONES_Y_ESCALAMIENTOS:** dependencias, decisiones abiertas y asuntos que requieren autoridad externa. La aceptación de riesgo exige responsable y no se infiere documentalmente.
- **Registro ADR global:** índice y estado común de ADR-001..011. D2 revisa; no aprueba decisiones cuyo autor, insumo o riesgo residual aún esté pendiente.
- **Índice y auditoría del frente:** muestran avance y control de cierre. La matriz global se modifica solo cuando exista cobertura material enlazada.

### Método y reglas de estado

1. Partir del inventario provisional del Maestro §6.1 y de las integraciones de §7, sin inventar productos, protocolos o nodos.
2. Mantener separados **activo**, **componente**, **frontera**, **amenaza**, **control**, **evidencia** y **aceptación**.
3. Aplicar STRIDE a cada clase y escenario; una misma amenaza puede afectar varios componentes, pero cada fila debe permitir una acción verificable.
4. Distinguir control preventivo, detectivo y correctivo. Citar controles `SEC-*` de D1 cuando existan; una referencia no prueba implementación.
5. Registrar todos los SPOF subsistentes aunque tengan mitigación. `ACEPTADO` requiere aprobador, fundamento, plazo/revisión y evidencia; mientras falte, usar `POR ACEPTAR` o `ESCALADO`.
6. Asignar probabilidad e impacto recién en B2 sobre escenarios concretos. La escala y umbrales serán explícitos y no sustituirán la aceptación del CLIENTE.
7. Refinar IDs y flujos en B6 con catálogos reales. **Regla de actualización del modelo (`RT-11.02`), obligatoria y permanente:** cualquiera de estos cinco cambios obliga a revisar y versionar las amenazas, los SPOF y las trazas afectadas antes de dar el modelo por vigente —
   (a) alta, baja o cambio de responsabilidad de un **componente lógico** `A1`;
   (b) alta, baja o cambio de contrato, versión, iniciador o campos de una **integración** `A2/A3`, incluidas las contrapartes externas;
   (c) alta, baja o cambio de emplazamiento, criticidad o dominio de fallo de un **nodo físico** `C1–C4`;
   (d) alta, baja o cambio de alcance de un **control `SEC-*`** de D1;
   (e) cambio de estado, alternativa seleccionada o condición de revisión de un **ADR**.
   El cambio se registra en `TRZ_D2.md` con su corte fechado; no se corrige el historial de un bloque ya cerrado, se emite un corte nuevo.
8. Elaborar el diagrama final en B8, después de estabilizar contenido, relaciones y revisión cruzada.

### Plan de bloques y punto de continuación

**Última actualización: 2026-09-06.** Actualizar esta tabla y el punto de continuación al cerrar cada bloque.

| Bloque | Contenido y resultado esperado | Avance actual / condición de cierre |
|---|---|---|
| P0 — Preparación y cobertura | Confirmar rama/corte, fuentes, contrato, clases, estados e IDs; revisar índice y trazas | **COMPLETADO.** Rama `frente_3`, base `2ce77d3`, Maestro v1.1 y Célula 2 `c4756df`; D2 identificado como siguiente entregable. No se tocó material local ajeno |
| B1 — Activos y fronteras | Inventario `AST-*`, clases, flujos y fronteras `TB-*`; alcance provisional verificable | **BORRADOR REDACTADO**, no aprobado: B1.1–B1.7. A1/A2/C1/C3 y Subdocumento 5 refinan correspondencia, contratos, nodos y campos |
| B2 — STRIDE por clases | Amenazas para canal, gateway, servicio, broker, dato, edge y tercero; probabilidad, impacto, controles y evidencia | **BORRADOR REDACTADO**, no aprobado: B2.1–B2.8. Escala `P1..P4`/`I1..I4`, 66 amenazas `THR-001..066`, fronteras `TB-04`/`TB-06`/`TB-05` y las siete clases `CLS-*`. `CLS-DAT`/S queda declarada abierta; ningún riesgo aceptado |
| B3 — Escenarios portuarios | TOS, gate/OCR, reefer, app offline, VMS, radio, ERP/autoridades y sincronización | **BORRADOR REDACTADO**, no aprobado: B3.1–B3.18. 12 escenarios `SCN-01..12` cubren las 8 materias del contrato y los 9 recorridos de `B1.5`; `THR-067..070` agregadas; 16 `SPOF-CAND-*` entregados a B4 |
| B4 — SPOF | Registro consolidado de fallos, mitigación, prueba, aceptabilidad, dueño y escalamiento | **BORRADOR REDACTADO**, no aprobado: B4.1–B4.8. Cifra de corte de B4: `SPOF-01..21`; **vigente tras B6: `SPOF-01..22`**, 0 aceptados, 11 `POR ACEPTAR` y 11 `ESCALADO`; `THR-071` agregada |
| B5 — ADR | Revisar ADR-001..011, alternativas, criterios, consecuencias negativas, riesgo residual y efecto T-11 | **REVALIDADO CON INSUMOS REALES**, no aprobado: B5.1–B5.5. `ADR-001..004` tienen decisión propuesta por sus autores; `ADR-005..007` conservan desarrollo parcial/candidato; `ADR-008..010` mantienen revisión completa y `ADR-011` se registra como candidato transversal |
| B6 — Cruce y refinamiento | Sustituir clases por IDs reales A1/A2/C1/C3; cruzar D1, capacidad, retorno y Subdocumento 5 | **BORRADOR REDACTADO**, no aprobado: B6.1–B6.8. Cobertura 24/24 componentes, 11/11 sistemas canónicos, 21/21 nodos y dos amenazas nuevas `THR-072/073`; diferencias A1↔C1 conservadas como hallazgos |
| B7 — Auditoría v0.5 | Cobertura 100 % inventario/integraciones, trazabilidad, contradicciones, vacíos y salidas accionables | **EJECUTADA: `CONFORME PARA v0.5 CON PENDIENTE ADR`.** B7.1–B7.7. Doce comprobaciones: 9 conformes —2 con observación—, 2 no conformes corregidas dentro de D2 (`B7-F01..F06`) y 1 pendiente de autor (`ADR-011`). `RT-11.02` cubierto a nivel de diseño documental; sigue `EN CURSO` por pruebas, revisión cruzada y aprobación. Cifras vigentes en `B7.3` |
| B8 — Vista y cierre | Diagrama de fronteras estable, resumen de riesgo residual y contenido aprobado para §4.3 | **DIFERIDO POR SECUENCIA.** Se ejecutará completo después de B6/B7, con catálogos integrados y cobertura auditada; no producir versión parcial |

**Retomar exactamente aquí:** B7, la integración B7-R y la revisión conjunta B7-C están ejecutadas. El modelo D2 conserva el veredicto `CONFORME PARA v0.5 CON PENDIENTE ADR`; `ADR-011` mantiene alternativas/selección pendientes. El siguiente paso es la auditoría independiente/general del paquete D1–D2, no B8 ni D3. Las cifras vigentes son las de `B7.3`; no se producen diagramas todavía.

### Dependencias de cierre, no de inicio

| ID | Entrada requerida | Estado de la entrada | Qué no puede darse por cerrado |
|---|---|---|---|
| `D2-DEP-001` | A1: catálogo lógico, criticidad y responsables `v0.1` | **RESUELTA A NIVEL DOCUMENTAL EN B6.** A1 declara 16 actores y 24 componentes; todos quedaron asociados a amenazas y nodos | Aprobación de propietarios y corrección de `ACT-TI` siguen fuera de D2; no impiden el cruce documental |
| `D2-DEP-002` | A2/A3: interfaces, contratos, autoridad TOS y degradación real | **RESUELTA A NIVEL DE DISEÑO EN B6.** Los 11 sistemas canónicos y la contraparte `EXT-CON` quedaron cruzados; A3 aporta autoridad, degradación y respaldo manual | Protocolos/campos efectivos, validación del CLIENTE y pruebas por interfaz continúan en `D2-DEP-005` |
| `D2-DEP-003` | C1/C2/C3/C4: nodos, red, sala, productos, HA/DR y capacidad | **CRUZADA CON OBSERVACIONES EN B6.** Los 21 nodos tienen amenazas aplicables; se registran diferencias de criticidad, continuidad y ubicación sin alterarlas | Corrección por Frente 2, independencia real, site survey, compatibilidad y pruebas |
| `D2-DEP-004` | D1/Subdocumento 5: controles y catálogo campo→sensibilidad→retención | **PARCIAL.** D1 aporta controles `SEC-*` y política de eventos; falta el catálogo de campos del Subdocumento 5 | Cobertura campo→sensibilidad→retención→custodia y riesgo residual de privacidad |
| `D2-DEP-005` | CLIENTE/terceros: contratos, SLA, directorio, site survey y aceptadores | **BLOQUEADO EXTERNO.** No depende de integrar ramas | Probabilidad basada en historia, viabilidad demostrada y aceptación formal de riesgo |

### B0-R. Reapertura de integración — línea base recibida

**Estado: COMPLETADO.** Esta reapertura no modifica los entregables de Frente 1 o Frente 2; los consume como evidencia y registra sus diferencias para que las resuelva su propietario.

| Entrada | Evidencia disponible | Resultado para D2 |
|---|---|---|
| A1 | 16 actores, 24 componentes lógicos, criticidad, propietarios y continuidad | habilita mapeo de `CLS-*`/`AST-*` en B6 |
| A2/A3 | 21 contrapartes, 7 familias técnicas, contratos lógicos, secuencias críticas, autoridad TOS y tabla de degradación/respaldo manual | habilita refinamiento de `TB-*`; los protocolos y contratos efectivos siguen externos |
| C1–C4 | 21 nodos físicos, matriz lógica→física 24/24, zonas, red, HA/DR, tecnologías y cálculos de capacidad/T-11 | habilita cruce físico; no demuestra pruebas ni resuelve site survey |
| D1 | controles `SEC-*`, ADR-008..010 y política de admisión de eventos | habilita amenaza→control; Subdocumento 5 aún debe entregar campo→sensibilidad→retención |

**Observaciones que B6 debe conservar:** `CTX-VESSEL` es crítico y local en A1/A3, pero C1 lo ubica solo en nube; existen otras diferencias de criticidad entre A1 y C1; C2/C4 pueden duplicar observabilidad/SIEM entre `T11-C2-19` y `T11-SEC-04`. Son entradas recibidas con observación, no motivos para volver a declarar ausentes los catálogos.

## Contenido técnico en elaboración

### B1. Activos y fronteras de confianza — borrador inicial

**Estado del bloque: BORRADOR REDACTADO; no aprobado.** Esta línea base permite iniciar STRIDE sin esperar los catálogos de los otros frentes. Los IDs son estables dentro de D2; B6 debe mapearlos contra componentes, interfaces y nodos reales sin borrar el historial.

#### B1.1 Alcance y unidad de análisis

D2 analiza la solución TERABYTE, sus canales, servicios, datos, runtime local, cadena de entrega y relaciones con sistemas conservados o externos. Una «frontera de confianza» es un cruce donde cambia al menos una de estas condiciones: identidad o autoridad, administración, red/zona, custodia de datos, disponibilidad, organización responsable o nivel de exposición. Estar dentro de la red del puerto no elimina la frontera ni concede confianza implícita.

La unidad mínima de amenaza será:

`activo + componente/clase + frontera + actor o condición adversa + efecto + controles + evidencia + riesgo residual`.

Los fallos accidentales y de dependencia se registran junto a STRIDE cuando cambian la seguridad o continuidad; los puntos únicos se consolidan en B4, no se ocultan dentro de una amenaza.

#### B1.2 Clases provisionales para STRIDE

| Clase | Alcance inicial | IDs del Maestro incluidos | Fronteras típicas | Refinamiento pendiente |
|---|---|---|---|---|
| `CLS-CAN` — canal | Portal, app y cabina/terminal compartido; dispositivo y sesión asociados | `CH-PORTAL`, `CH-APP`, `CH-CAB` | TB-01, TB-03, TB-05 | A1 confirma canales, perfiles y responsabilidad; C1/C2 dispositivos |
| `CLS-GWY` — gateway | Borde expuesto y puerta de enlace de servicios | `GW-EDGE`, `GW-API` | TB-01, TB-02, TB-03 | A2 confirma rutas, iniciadores, contratos y dominios |
| `CLS-SVC` — servicio | Contextos de negocio y servicios comunes | `CTX-*`, `SRV-IAM`, `SRV-NOTIF`, `SRV-EVID` | TB-02, TB-03, TB-11 | A1 confirma límites/criticidad; A2 interfaces |
| `CLS-BRK` — broker/integración | Bus, colas, adaptadores y anticorrupción del TOS | `INT-HUB`, `INT-TOS` | TB-04, TB-06..09, TB-11 | A2/A3 confirman contratos, autoridad, orden y conciliación |
| `CLS-DAT` — dato | Datos operacionales, series, documentos, analítica, logs, claves y respaldos | `DATA-CORE`, `DATA-TS`, `DATA-DOC`, `DATA-AN`; activos AST-001..016 | TB-11, TB-14 | Subdocumento 5/C2 confirman campos, stores, custodios y retención |
| `CLS-EDG` — edge | Runtime y buffer locales, administración y sincronización | `EDGE-RUN` | TB-04, TB-05, TB-10, TB-14 | C1/C3 confirman nodos, enlaces, HA y energía |
| `CLS-EXT` — tercero/conservado | TOS, ERP, VMS, navieras, autoridades, ferrocarril, concedente y periféricos | `EXT-*` del Maestro §5.2 y grupos §7 | TB-05..09 | A2/CLIENTE levantan contrato, SLA, versión y responsable |

La clase no reemplaza el inventario final. Por ejemplo, una amenaza de `CLS-EXT` contra TOS y otra contra una autoridad pueden compartir patrón, pero conservan frontera, autoridad, fallback y evidencia distintos.

#### B1.3 Inventario provisional de activos

| ID | Activo que debe protegerse | Valor/consecuencia en el caso | Componentes o clases iniciales | Propiedades prioritarias | Fuente principal | Validación pendiente |
|---|---|---|---|---|---|---|
| `AST-001` | Autoridad operacional por dominio × zona × fase | Evita dos fuentes de verdad y movimientos contradictorios durante convivencia TOS | `CTX-OPS`, `INT-TOS`, `DATA-CORE`, `CLS-BRK` | integridad, autenticidad, consistencia, disponibilidad | Maestro §8; MC-07/08; Decisión 1 | A2/A3 definen matriz, traspaso y contrato real |
| `AST-002` | Posición, inventario y cruce de zonas | Una posición falsa o desconocida compromete seguridad, productividad, gate y facturación | `CTX-OPS`, `CTX-YARD`, `EDGE-RUN`, `DATA-CORE` | integridad, frescura, trazabilidad, disponibilidad | Maestro §§6.1/9; Decisiones 2/15 | A1/A3 y periferia confirman fuentes y excepción |
| `AST-003` | Gate, citas y tiempos de entrada/salida | Controla acceso, cola y el indicador que no puede reconstruirse después | `CTX-GATE`, `CH-PORTAL`, `EDGE-RUN`, `DATA-CORE` | autenticidad, integridad, disponibilidad, no repudio | Maestro §§6.1/9; MC-10/16 | A2/A3 levantan barreras/OCR y autoridad offline |
| `AST-004` | Telemetría, estado y alarmas reefer | Protege carga refrigerada; ausencia o parametrización inválida puede impedir alarma ≤5 min | `CTX-REEFER`, `DATA-TS`, `SRV-NOTIF`, `EDGE-RUN` | disponibilidad, integridad, frescura, trazabilidad | Maestro §§9/15/18.1; RN-11; RF-REF-04/07 | Parámetros, fuentes, responsables y capacidad por validar |
| `AST-005` | Hechos y evidencia facturable | Sustenta evento→evidencia→ERP y objeciones; no puede reconstruirse posteriormente | `CTX-BILL`, `SRV-EVID`, `DATA-DOC`, `DATA-CORE` | integridad, autenticidad, no repudio, retención | Maestro §§7/9/16; Decisión 11 | A2/A3/Subdoc. 5 confirman esquema y relación 1:1 |
| `AST-006` | Identidades, roles, sesiones y acreditaciones | Determina quién puede operar, representar a una empresa o elevar privilegios | `SRV-IAM`, `CLS-CAN`, `CLS-SVC` | autenticidad, mínimo privilegio, revocación, auditoría | Maestro §11.2; D1 B1/B2; MC-04/18 | F3-ESC-001/002, A1 y CLIENTE |
| `AST-007` | Mensajes, contratos, colas y estado de conciliación | Preserva orden, idempotencia, deduplicación y recuperación entre 21 contrapartes y 7 familias | `INT-HUB`, `INT-TOS`, `CLS-EXT` | integridad, orden, disponibilidad, trazabilidad | Maestro §§6.2/7/8 | A2 aporta contrato, versión, iniciador y campos |
| `AST-008` | Registros de auditoría y evidencia de seguridad | Permite detectar, investigar y demostrar acciones durante operación conectada/desconectada | `SRV-EVID`, repositorio de logs, `EDGE-RUN` | integridad, inmutabilidad, disponibilidad, retención | Maestro §§11.3/16.1; D1 B5 | C2/C4 dimensionan; D1/CLIENTE definen custodia y acceso |
| `AST-009` | Claves, secretos, certificados y material de recuperación | Un compromiso permite suplantar servicios o descifrar datos; una pérdida puede detener operación | capacidades `SEC-KEY-01`, `SEC-SECRET-01`; híbrido | confidencialidad, integridad, disponibilidad, separación de funciones | Maestro §11.1; D1 B4; ADR-009 | Producto, ubicación, HA, custodios y rotación pendientes |
| `AST-010` | Datos personales, comerciales y de carga/ruta | Su exposición afecta privacidad, competencia y seguridad de carga | `DATA-CORE`, `DATA-DOC`, `DATA-AN` | confidencialidad, integridad, minimización, trazabilidad | Maestro §§11/16; RNF-SEG-05/09; D1 B4 | Subdocumento 5 entrega catálogo de campos y licitud |
| `AST-011` | Software, dependencias, imágenes, SBOM, firma, procedencia e IaC | Una alteración de suministro puede introducir código o infraestructura no autorizados | pipeline/registro; `CLS-SVC`, `CLS-EDG` | integridad, autenticidad, reproducibilidad, trazabilidad | Maestro §§10.1/11.3/12; D1 B6 | C3 define plataforma, responsables y flujo real |
| `AST-012` | Configuración, reglas y parámetros operacionales | Cambios en reglas de patio, reefer, seguridad o integración alteran decisiones sin cambiar código | `CTX-*`, `GW-*`, `EDGE-RUN`, `INT-*` | integridad, autorización, versionado, retorno | Maestro §§8/12/18.1; Decisiones 3–5/8 | A1–A3/C3 definen repositorio, aprobadores y despliegue |
| `AST-013` | Disponibilidad de cinco funciones críticas locales y buffer 72 h | La pérdida de enlace exterior no puede detener nave, posición, gate, reefer ni evidencia | `EDGE-RUN`, servicios/datos críticos | disponibilidad, capacidad, integridad, recuperabilidad | Maestro §9; RNF-DIS-02/03/04 | A3/C1–C4 demuestran alcance, nodos y peak |
| `AST-014` | Sincronización y reconciliación posterior | Debe recuperar el estado automáticamente, sin duplicar ni perder, en ≤90 min | `EDGE-RUN`, `INT-HUB`, `INT-TOS`, `DATA-CORE` | integridad, determinismo, orden, trazabilidad | Maestro §§6.2/8/9/15.1 | A2/A3/C3/C4 validan volumen, conflicto, enlace y holgura |
| `AST-015` | Continuidad de VMS/ISPS y separación de protección | La modernización no puede degradar protección ni convertir video en una nueva carga operacional | sistema VMS conservado, metadatos/eventos, red de protección | disponibilidad, aislamiento, integridad, confidencialidad | Maestro §§7/10.2/19; MC-02; Decisión 19 | C3/CLIENTE confirman conducto permitido y prueba de continuidad |
| `AST-016` | Mensajería de nave, ventanas y evidencia del programa 2029 | La manipulación, pérdida o redigitación impide los cuatro resultados indivisibles | `CTX-VESSEL`, `INT-HUB`, navieras, `DATA-DOC` | autenticidad, integridad, disponibilidad, no repudio | Maestro §§7/14; MC-20/23/24/25 | A2/A3 levantan versión, línea, plazo y evidencia E2E |

#### B1.4 Catálogo provisional de fronteras de confianza

| ID | Cruce | Cambio de confianza o autoridad | Activos principales | Controles D1 de partida | Evidencia futura mínima | Pendiente de refinamiento |
|---|---|---|---|---|---|---|
| `TB-01` | Internet/actor externo ↔ `GW-EDGE` | exposición pública y organización/dispositivo no administrado | AST-003/006/010/016 | `SEC-EDGE-01/02`, `SEC-EXP-01` | inventario externo, reglas WAF/DDoS/bots, TLS y pruebas | Dominios, rutas, proveedor y capacidad A1/A2/C1/C3 |
| `TB-02` | `GW-EDGE` ↔ `GW-API`/servicios privados | borde administrado a plano privado; cambia terminación y política | AST-001/003/006/010 | `SEC-API-01`, `SEC-NET-01` | política origen-destino, esquema, identidad, rechazo y trazas | Rutas/contratos/segmentos reales A2/C3 |
| `TB-03` | Canal/servicio ↔ `SRV-IAM` | autenticación, representación, sesión y elevación de privilegio | AST-006/009 | `SEC-IAM-01`, `SEC-ADM-01` | casos de acceso/revocación/relevo/PAM y auditoría | Directorio, roles, parámetros y corte F3-ESC-001/002 |
| `TB-04` | Nube ↔ terminal/`EDGE-RUN` | dominio administrativo, disponibilidad de enlace y posible autoridad de escritura | AST-001/007/008/009/013/014 | `SEC-NET-01`, `SEC-LOG-01`, `SEC-KEY-01` | aislamiento 72 h, buffer, reconexión, conflicto y pérdida de enlace | Topología, iniciador, enlaces, HA y capacidad C1/C3/C4 |
| `TB-05` | Zona operacional/edge ↔ periferia de terreno | dispositivo/firmware/fabricante, ambiente físico y red operacional | AST-002/003/004/012/013/015 | `SEC-NET-01`, `SEC-HARD-01`, `SEC-END-01` | inventario, identidad de dispositivo, comandos permitidos, failover y registros | Contratos, protocolos, protección marina y site survey |
| `TB-06` | Plataforma nueva/`INT-TOS` ↔ TOS 2012 | fuente de verdad variable, legado y traspaso dominio×zona×fase | AST-001/002/003/005/007/014 | `SEC-API-01`, `SEC-LOG-01` | pruebas de lectura/escritura parcial, orden, conciliación y retorno | Contrato/capacidad/soporte reales ESC-04/06; A2/A3 |
| `TB-07` | Plataforma ↔ ERP | organización/sistema conservado y autoridad tributaria externa al alcance | AST-005/007/010 | `SEC-API-01`, `SEC-DATA-01`, `SEC-LOG-01` | conciliación 1:1, autenticidad, rechazo, objeción y reenvío | Contrato, campos, SLA y fallback A2/CLIENTE |
| `TB-08` | Plataforma ↔ navieras/autoridades/ferrocarril/concedente | contraparte, versión, disponibilidad y responsabilidad distintas | AST-007/010/016 | `SEC-EDGE-02`, `SEC-API-01`, `SEC-LOG-01` | pruebas por contrato/versión, cola, reintento, no repudio y fallback | Interfaces/plazos/SLA ESC-01/06/14; A2 |
| `TB-09` | Plataforma operacional ↔ VMS/red de protección | separación IEC 62443/ISPS y sistema conservado | AST-007/015 | `SEC-NET-01`, `SEC-API-01` | rutas denegadas/permitidas, metadatos mínimos y continuidad VMS | Conducto y responsabilidades C3/CLIENTE; no transportar video por defecto |
| `TB-10` | Administración/soporte/SOC ↔ planos de gestión | privilegio elevado y organización de soporte posiblemente externa | AST-006/008/009/011/012 | `SEC-ADM-01`, `SEC-PROD-01`, `SEC-SOC-01` | MFA/PAM, aprobación, sesión grabada, segregación y respuesta | RACI, bastión, proveedor y accesos reales D1/C3/CLIENTE |
| `TB-11` | Servicio/broker ↔ repositorio de datos | cambia proceso a persistencia y custodia; consultas directas son riesgo separado | AST-001..005/007/008/010/012/014 | `SEC-DATA-01`, `SEC-KEY-01`, `SEC-LOG-01` | autorización por servicio, cifrado, consulta sensible, integridad y retención | Stores/esquemas/campos/propietarios A1/A2/Subdoc. 5 |
| `TB-12` | Desarrollo/terceros ↔ pipeline/registro ↔ runtime | confianza de persona/dependencia a artefacto ejecutable y despliegue | AST-009/011/012 | `SEC-PIPE-01`, `SEC-SUPPLY-01`, `SEC-ART-01` | revisión, bloqueo, SBOM, firma, procedencia y verificación al desplegar | Plataforma, identidades, registro y política C3 |
| `TB-13` | Desarrollo/QA/Preproducción ↔ Producción/DR | cambia sensibilidad de datos, privilegio y autoridad operacional | AST-006/009/010/011/012 | `SEC-NPDATA-01`, `SEC-PROD-01`, `SEC-ADM-01` | aislamiento, promoción de artefacto único, no uso de datos reales y retorno | Diseño de ambientes/despliegue C3 |
| `TB-14` | Producción/edge ↔ respaldo, archivo y DR | custodia, inmutabilidad, región/sitio y modo de recuperación | AST-005/008/009/013/014 | `SEC-BKP-01`, `SEC-KEY-01`, `SEC-LOG-01` | 3-2-1-1-0, restauración mensual, conmutación semestral e integridad | Ubicación, producto, separación, RPO/RTO y capacidad C1–C4 |

#### B1.5 Recorridos críticos que B2/B3 deben desafiar

| Recorrido | Fronteras | Resultado que no debe perderse | Condición de falla/ataque inicial |
|---|---|---|---|
| Solicitud externa de cita/documentación → operación de gate | TB-01→02→03→11; TB-04 si terminal aislado | recibir no equivale a confirmar; autoridad y frescura visibles | suplantación, abuso automatizado, dato manipulado o confirmación con estado obsoleto |
| OCR/barrera/camión → hecho de gate | TB-05→11; TB-04/06 según autoridad | cero diferencias no explicadas y evento no reconstruido | sensor/imagen repetida, comando falso, pérdida de enlace o doble escritura |
| Reefer → alarma → escalamiento | TB-05→11→04/03 | alarma operacional dentro del límite y evidencia de recepción | silencio de sensor, parámetro alterado, cola saturada o notificación suplantada |
| Movimiento/posición → TOS/plataforma nueva | TB-05→11→06 | una autoridad por dominio×zona×fase y posición verificable | evento fuera de orden, replay, escritura parcial o traspaso incompleto |
| Hecho facturable → ERP | TB-11→07 | relación 1:1, objeción y reenvío sin duplicidad | evidencia alterada, pérdida, repudio o duplicación en reintento |
| Operación local 72 h → reconexión ≤90 min | TB-04→11→06/07/08 | cinco funciones sin pérdida y conciliación determinista | partición, buffer agotado, reloj divergente, conflicto o saturación al retorno |
| Naviera → mensajería de nave → confirmación | TB-08→11 | versión por naviera, orden, exclusividad 2029 y no repudio | emisor falso, mensaje alterado/repetido, versión incompatible o tercero caído |
| Cambio de software/configuración → Producción/edge | TB-12→13→04/05 | artefacto firmado, configuración autorizada y retorno | dependencia comprometida, firma eludida, secreto filtrado o cambio fuera de ventana |
| Administración/SOC → componente/dato sensible | TB-10→03/11 | privilegio temporal, trazable y mínimo | credencial privilegiada robada, sesión no registrada o acceso directo a datos |

#### B1.6 Supuestos, exclusiones y preguntas de refinamiento

- Los IDs del Maestro son una base de trabajo, no evidencia de que A1 haya cerrado el catálogo. No se afirma cobertura 100 % de RT-11.02 en B1.
- `TB-*` expresa cruces lógicos. No presume VLAN, firewall, región, rack, enlace, puerto ni producto; C1/C3 deben materializar la topología.
- Los sistemas conservados siguen fuera del límite de reemplazo, pero su integración está dentro del análisis. D2 no propone reemplazar TOS, ERP, VMS, control de grúas, barreras o báscula.
- No se modela video completo como flujo operacional. Para VMS se limita inicialmente a eventos, metadatos o evidencia confirmada, sujeto a contrato.
- La nube y el terminal son dominios distintos incluso si comparten proveedor de identidad o herramientas. Una pérdida de enlace exterior no equivale a falla de energía, LAN, edge o sala.
- La lista debe ampliarse si A1/A2/C1/C3 incorporan un componente, integración, plano de gestión o almacén no representado. Toda incorporación relevante dispara revisión STRIDE y trazabilidad.
- Innovaciones del Subdocumento 5 se incorporan solo cuando exista flujo, activo, dato e interfaz definidos y cuando modifiquen la arquitectura de seguridad; no se inventa su diseño desde D2.

#### B1.7 Auditoría del bloque y salida

| Comprobación | Resultado B1 | Estado correcto |
|---|---|---|
| siete clases mínimas del contrato | 7/7 definidas como `CLS-*` y enlazadas al Maestro | CONFORME PARA INICIAR B2 |
| activos | 16 activos con valor, propiedades, fuente y refinamiento | BORRADOR; inventario final depende de A1/A2/Subdoc. 5 |
| fronteras | 14 fronteras con cambio de confianza, activos, controles y evidencia | BORRADOR; topología depende de C1/C3 |
| escenarios de recorrido | 9 recorridos críticos preparados para STRIDE | EN CURSO; amenazas/severidad se desarrollan en B2/B3 |
| amenazas STRIDE completas | todavía no | PENDIENTE — no cerrar RT-11.02 |
| SPOF/aceptaciones | todavía no | PENDIENTE — B4 |
| productos, cantidades o precios inventados | no detectados | CONFORME |

**Salida B1:** existe un inventario inicial que permite modelar amenazas sin fingir que los otros frentes ya entregaron sus catálogos. `TRZ_D2.md` enlaza las fuentes y mantiene las dependencias visibles. Próximo bloque: **B2 — STRIDE por clases**, con controles preventivos/detectivos/correctivos y evidencia futura; ningún riesgo se marcará aceptado.

### B2. STRIDE por clases — borrador inicial

**Estado del bloque: BORRADOR REDACTADO; propuesta no aprobada.** B2 convierte el inventario de B1 en amenazas verificables. Ninguna fila declara un control implementado, una prueba ejecutada, un riesgo aceptado ni una decisión del CLIENTE. Los identificadores `THR-*` son estables dentro de D2: B3 los reutiliza con contexto operacional, B4 consolida los puntos únicos de falla y B6 los reasigna a componentes e interfaces reales sin borrarlos ni renumerarlos.

#### B2.1 Escala cualitativa de probabilidad, impacto y riesgo

La escala existe para **priorizar el trabajo de B3–B8**. No expresa tolerancia del CLIENTE, no sustituye la aceptación formal de riesgo y no proviene de un historial de incidentes: el terminal no ha entregado estadística de incidentes y `D2-DEP-005` permanece abierta. Cada valor se justifica por condiciones ya declaradas en el Maestro, el Caso 06 o las Bases, no por frecuencia observada.

**Probabilidad — condición que la sustenta**

| Nivel | Lectura | Criterio de asignación |
|---|---|---|
| `P1` | Baja | requiere acceso privilegiado, presencia física controlada o una cadena de condiciones simultáneas poco habituales |
| `P2` | Media-baja | plausible durante operación normal por error humano, configuración incompleta, contrato no cerrado o falla de un componente |
| `P3` | Media-alta | favorecida por una condición estructural ya declarada del caso: exposición pública, legado 2012, terreno compartido e intemperie, 72 h sin enlace, terceros sin contrato levantado o peak coincidente |
| `P4` | Alta | se espera al menos una ocurrencia durante marcha blanca u operación si no existe un control específico y verificado |

En B2 no se usa `P4` salvo que la condición esté escrita en una fuente vigente. Un escenario sin fuente se mantiene en `P2` y se marca para revisión, en lugar de inflar la prioridad.

**Impacto — anclado a umbrales y criterios de aceptación del caso**

| Nivel | Lectura | Criterio de asignación |
|---|---|---|
| `I1` | Menor | molestia local corregible dentro del turno; no afecta umbrales, evidencia, protección ni continuidad |
| `I2` | Moderado | degrada un umbral no crítico (portal ≤60 s, consulta ≤1 s) o genera retrabajo, sin pérdida de evidencia ni detención |
| `I3` | Mayor | incumple un umbral crítico o un criterio de aceptación —gate ≤120 s, OCR ≤3 s, posición ≤30 s, sincronización ≤90 min, ventana ≥72 h, KPI del concedente ≤1 h— o compromete datos de `AST-005`/`AST-008`/`AST-010` de forma recuperable |
| `I4` | Crítico | detiene nave, muelle o gate; impide la alarma reefer ≤5 min; pierde o corrompe de forma irreversible evidencia facturable, indicadores del concedente o registros de auditoría; degrada protección ISPS/VMS; compromete identidades, claves o secretos; o deja dos fuentes de verdad no reconciliables |

**Matriz de riesgo**

| | `I1` | `I2` | `I3` | `I4` |
|---|---|---|---|---|
| `P4` | MEDIO | ALTO | CRÍTICO | CRÍTICO |
| `P3` | BAJO | MEDIO | ALTO | CRÍTICO |
| `P2` | BAJO | MEDIO | ALTO | ALTO |
| `P1` | BAJO | BAJO | MEDIO | ALTO |

**Riesgo residual proyectado.** Es el nivel estimado **suponiendo que el control propuesto quedara correctamente implementado y probado**. Es una proyección de diseño, no una medición: mientras la evidencia sea futura, el residual real no puede ser inferior al inherente. Por eso B2 no baja ningún residual a `BAJO` cuando el control depende de un producto, un nodo, un contrato o un responsable todavía inexistente, y ninguna fila usa el estado `ACEPTADO`. Los estados admitidos en B2 son:

- `PROPUESTA` — amenaza y controles redactados por D2, sin validación externa;
- `POR VALIDAR` — depende de un insumo identificado de otro frente, del Subdocumento 5 o del CLIENTE;
- `ESCALADO` — requiere una autoridad externa registrada en `DECISIONES_Y_ESCALAMIENTOS.md` o en los `ESC-*` del Maestro.

`ACEPTADO` solo puede aparecer en B4/B8, y exige aprobador nominado, fundamento, evidencia y condición de revisión.

#### B2.2 Método, numeración y forma de leer las tablas

1. Cada amenaza recibe un identificador estable `THR-xxx`, correlativo y no reutilizable. La fila del contrato es ilustrativa del formato y no ocupa identificador; B2 asigna la numeración definitiva desde `THR-001` y cubre el escenario de la app instalable perdida o robada en `THR-026`.
2. Cada bloque presenta **dos tablas unidas por el identificador**: la **Tabla A** aporta activo, componente o clase, frontera, categoría STRIDE, condición y escenario, probabilidad, impacto y riesgo inherente; la **Tabla B** aporta control preventivo, control detectivo, respuesta correctiva con evidencia esperada, riesgo residual proyectado, estado y validación pendiente. Ambas juntas materializan la matriz STRIDE obligatoria del contrato; se separan para que cada celda siga siendo legible y accionable en lugar de reducirse a una palabra.
3. Los controles se citan con los identificadores `SEC-*` de D1. **Citar un control no acredita implementación, producto, ubicación, capacidad ni prueba**; D1 declara explícitamente que su evidencia es prevista y que `SEC-PHYS-v0.1` aún no fue intercambiado.
4. Se distingue **diseño propuesto** (lo que D2 recomienda), **evidencia futura** (la prueba que deberá existir) y **evidencia ejecutada** (inexistente en este bloque). Ninguna celda de B2 contiene evidencia ejecutada.
5. Los fallos accidentales y de dependencia se registran junto a STRIDE cuando alteran seguridad o continuidad, conforme B1.1. Su consolidación como puntos únicos ocurre en B4, no dentro de la amenaza.
6. No se inventan APIs, protocolos, puertos, versiones, productos, topología, historial de incidentes, cantidades, precios ni decisiones del CLIENTE. Donde la fuente no alcanza, la celda dice qué falta y quién debe aportarlo.
7. El orden de desarrollo es el de mayor consecuencia operacional: primero `TB-04`, `TB-06` y `TB-05`; después la cobertura inicial de las siete clases `CLS-*`.

#### B2.3 Fronteras prioritarias

Se desarrollan primero porque concentran la consecuencia operacional del caso: la continuidad de 72 h, la convivencia con el TOS 2012 y el terreno donde ocurren gate, posición y frío.

##### B2.3.1 `TB-04` — nube ↔ terminal y `EDGE-RUN`

Cruce de dominio administrativo, disponibilidad de enlace y posible autoridad de escritura. Activos principales `AST-001`, `AST-007`, `AST-008`, `AST-009`, `AST-013` y `AST-014`. Clases involucradas `CLS-EDG`, `CLS-BRK` y `CLS-DAT`.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-001` | AST-001/014 | `EDGE-RUN`, `INT-HUB` / `CLS-EDG`, `CLS-BRK` | TB-04 | S | Un extremo no autorizado se presenta como el lado nube (o como el runtime local) al restablecerse el enlace y entrega estado o instrucciones de escritura que el otro extremo aplica como legítimas | P2 | I4 | ALTO |
| `THR-002` | AST-002/005/014 | `EDGE-RUN`, `INT-HUB`, `DATA-CORE` / `CLS-EDG`, `CLS-DAT` | TB-04 | T | El lote acumulado durante el aislamiento se altera antes o durante la reconciliación: posiciones, movimientos o hechos facturables llegan modificados y se aplican como si vinieran del terreno | P2 | I4 | ALTO |
| `THR-003` | AST-006/008 | `EDGE-RUN`, repositorio de logs / `CLS-EDG`, `CLS-DAT` | TB-04 | R | Una operación ejecutada localmente durante las 72 h no puede atribuirse después, porque el registro local no se conserva íntegro ni se correlaciona con el central al reconectar | P3 | I3 | ALTO |
| `THR-004` | AST-010/013 | `EDGE-RUN`, buffer local / `CLS-EDG`, `CLS-DAT` | TB-04 | I | El buffer local retiene datos personales, comerciales o que permiten inferir contenido y ruta; quien alcanza el nodo o su almacenamiento los lee sin pasar por el servicio propietario | P2 | I3 | ALTO |
| `THR-005` | AST-013 | `EDGE-RUN`, servicios y datos críticos locales / `CLS-EDG` | TB-04 | D | El buffer se agota antes de las 72 h porque el aislamiento coincide con dos naves y gate saturado; se pierden eventos de una o más de las cinco funciones críticas y no hay reconstrucción posterior | P3 | I4 | CRÍTICO |
| `THR-006` | AST-013/014 | enlace exterior, `INT-HUB` / `CLS-EDG`, `CLS-BRK` | TB-04 | D | Al reconectar, la descarga del buffer consume el enlace y desplaza el tráfico operacional en curso; la sincronización excede los 90 min y la operación queda con datos divergentes más tiempo del previsto | P3 | I3 | ALTO |
| `THR-007` | AST-006/009/011/012 | canal de administración y actualización del runtime local / `CLS-EDG` | TB-04 + TB-10 | E | El camino de administración remota o de actualización del nodo local se usa para obtener privilegio dentro de la zona operacional, alcanzando datos y periferia que el canal funcional no expone | P2 | I4 | ALTO |
| `THR-008` | AST-002/007/014 | `EDGE-RUN`, `INT-HUB`, `DATA-CORE` / `CLS-EDG`, `CLS-BRK` | TB-04 | T | La referencia temporal del terminal y la de la nube divergen durante el aislamiento; al reconciliar, el orden de los eventos, la ventana de deduplicación y la resolución de conflictos dejan de ser deterministas | P3 | I3 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-001` | `SEC-SYNC-01` conducto autenticado con identidad técnica acotada por extremo; `SEC-KEY-01` material de identidad no exportable y separado por ámbito nube/local | `SEC-LOG-01` / `SEC-SIEM-01` registro de cada establecimiento del conducto, con alerta ante identidad desconocida, renegociación anómala o extremo duplicado | Revocar la identidad técnica, aislar el conducto y revalidar el lote ya aplicado; **evidencia esperada:** prueba documentada de rechazo de un extremo no autorizado y de revocación efectiva sin detener la operación local | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-003`: A2/A3 definen iniciador y contrato del conducto; C1/C3 la topología y los enlaces reales |
| `THR-002` | `SEC-SYNC-01` integridad extremo a extremo del lote; `SEC-ENC-01`/`SEC-FIELD-01` protección en tránsito y por campo sensible; escritura idempotente con clave y ventana de deduplicación (Maestro §6.2) | `SEC-LOG-01` conciliación por turno con detección temprana y no solo tardía; contraste de totales por dominio antes de aplicar | Detener la aplicación del lote, aislar el conjunto sospechoso y reconciliar contra el origen; **evidencia esperada:** prueba de reconciliación con lote alterado deliberadamente y traza del rechazo | ALTO | POR VALIDAR | `D2-DEP-002`: A2/A3 definen campos, orden, conflicto y conciliación por integración real |
| `THR-003` | `SEC-LOG-01` registro local inalterable con continuidad durante el aislamiento; `SEC-IAM-01` identidad individual también en operación local | `SEC-SIEM-01` verificación de continuidad de la serie de registros y de su ingesta posterior; alerta por vacío de secuencia | Reconstruir la cadena desde el registro local, marcar el período no atribuible y escalarlo; **evidencia esperada:** prueba de 72 h aisladas con atribución completa tras la reingesta | ALTO | POR VALIDAR | `D2-DEP-003`/`D2-DEP-004`: C1–C4 dimensionan el buffer de registro; D1/CLIENTE definen custodia y acceso |
| `THR-004` | `SEC-DATA-01` acceso por clasificación; `SEC-ENC-01` cifrado en reposo del buffer; `SEC-FIELD-01` cifrado adicional de campo sensible; `SEC-HARD-01` endurecimiento del nodo | `SEC-END-01` detección en el nodo local; `SEC-LOG-01` registro de consultas y de acceso al almacenamiento local | Aislar el nodo, rotar el material afectado y evaluar notificación; **evidencia esperada:** verificación de que el buffer en reposo no es legible fuera del servicio propietario | ALTO | POR VALIDAR | `D2-DEP-004`: el Subdocumento 5 debe entregar el catálogo campo→sensibilidad→retención antes de afirmar cobertura |
| `THR-005` | Dimensionamiento del buffer al peak coincidente declarado (Maestro §10.2 y §15.1); degradación elegante con funciones no disponibles declaradas; priorización de las cinco funciones críticas frente a tráfico diferible | `SEC-SIEM-01` y telemetría de ocupación del buffer con umbral de aviso anticipado; alerta antes del agotamiento, no en el agotamiento | Activar el procedimiento manual declarado para las funciones no sostenibles y preservar la evidencia mínima; **evidencia esperada:** prueba de 72 h con peak coincidente y demostración de que ningún evento crítico se descarta silenciosamente | CRÍTICO | POR VALIDAR | `D2-DEP-003`: C1–C4 deben demostrar capacidad, holgura y comportamiento en el límite. La cifra de dimensionamiento no se fija en D2 |
| `THR-006` | Control de tasa y prioridad en la descarga; `SEC-SYNC-01` reconciliación por lotes ordenados; separación entre tráfico de recuperación y tráfico operacional | `SEC-SIEM-01` medición del avance de sincronización contra el objetivo de 90 min; alerta por proyección de incumplimiento | Reducir la tasa de recuperación, priorizar dominios críticos y declarar el estado degradado a la operación; **evidencia esperada:** prueba de reconexión tras 72 h con medición del tiempo real y del efecto sobre la operación | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-003`: A2/A3 aportan volumen y conflicto; C3/C4 el enlace y su holgura |
| `THR-007` | `SEC-ADM-01` administración con MFA, elevación temporal y sesión registrada; `SEC-NET-01` conducto de gestión separado del funcional; `SEC-SUPPLY-01`/`SEC-ART-01` solo artefactos firmados con procedencia verificada en el nodo | `SEC-SIEM-01`/`SEC-END-01` detección de sesión administrativa fuera de ventana, de cambio no aprobado y de ejecución no firmada | Cortar el acceso, revocar credenciales, revisar el nodo y aplicar el retorno registrado; **evidencia esperada:** grabación de sesión, aprobación asociada y verificación de firma en el despliegue | ALTO | POR VALIDAR | `D2-DEP-003`/`D2-DEP-005`: C3 define bastión y plataforma; el CLIENTE define RACI y proveedor de soporte |
| `THR-008` | Sincronización de referencia temporal en ambos dominios y sello de origen en el evento; orden por secuencia propia además de por marca de tiempo | `SEC-SIEM-01` alerta por desviación de referencia temporal y por eventos fuera de ventana esperada | Reprocesar el lote con la secuencia de origen y marcar los conflictos para resolución determinista; **evidencia esperada:** prueba de reconciliación con desviación temporal inducida | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-003`: no se presume una fuente de tiempo ni un mecanismo concreto; A2/A3 y C3 deben definirlo |

##### B2.3.2 `TB-06` — plataforma nueva/`INT-TOS` ↔ TOS 2012

Cruce donde la fuente de verdad varía por `dominio × zona × fase` y donde el legado impone su contrato. Activos principales `AST-001`, `AST-002`, `AST-003`, `AST-005`, `AST-007` y `AST-014`. Clases `CLS-BRK` y `CLS-EXT`. El contrato real del TOS, sus fechas de soporte y su capacidad de escritura permanecen abiertos (`ESC-04`, `ESC-06`); B2 no supone ninguna de las tres cosas.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-009` | AST-001/002/007 | `INT-TOS` / `CLS-BRK`, `CLS-EXT` | TB-06 | S | Un cliente no autorizado escribe contra el TOS —o contra la plataforma— presentándose como la capa anticorrupción, e introduce movimientos o estados que ningún operador ejecutó | P2 | I4 | ALTO |
| `THR-010` | AST-002/003/007 | `INT-TOS` / `CLS-BRK` | TB-06 | T | La traducción legado↔nuevo se altera y cambia contenedor, zona o posición; el destino acepta el mensaje porque es sintácticamente válido y no hay verificación cruzada con el origen | P2 | I4 | ALTO |
| `THR-011` | AST-001/005 | `INT-TOS`, `CTX-OPS`, `CTX-BILL` / `CLS-BRK`, `CLS-SVC` | TB-06 | R | Una escritura se aplica en un solo lado y después nadie puede demostrar qué sistema tenía autoridad sobre ese dominio, zona y fase en ese instante; la diferencia se descubre fuera de las ventanas de investigación de 48 h y 24 h | P3 | I4 | CRÍTICO |
| `THR-012` | AST-002/007 | `INT-TOS`, `INT-HUB` / `CLS-BRK` | TB-06 | T | Un mensaje de movimiento se reprocesa o se repite durante los reintentos y produce un segundo movimiento; el inventario y el cruce de zona quedan incorrectos sin que nadie declare un error | P3 | I3 | ALTO |
| `THR-013` | AST-002/003/007 | TOS 2012, `INT-TOS` / `CLS-EXT`, `CLS-BRK` | TB-06 | D | El legado degrada o rechaza escrituras durante nave o gate; la cola crece, la conciliación por turno se retrasa y las diferencias se detectan cuando ya no pueden investigarse dentro de la ventana | P3 | I3 | ALTO |
| `THR-014` | AST-010 | `INT-TOS`, `DATA-AN` / `CLS-BRK`, `CLS-DAT` | TB-06 | I | La lectura hacia el legado se define más amplia de lo necesario para funcionar y arrastra datos comerciales o tarifarios que después se propagan a analítica y reportes | P2 | I3 | ALTO |
| `THR-015` | AST-006/009 | credencial técnica de integración con el TOS / `CLS-BRK`, `CLS-EXT` | TB-06 + TB-10 | E | La cuenta usada por la capa anticorrupción tiene privilegios amplios en el legado y permite operaciones fuera del contrato de coexistencia, incluidas las que el diseño reservó a la puerta de retiro | P3 | I4 | CRÍTICO |
| `THR-016` | AST-001/005 | `INT-TOS`, `CTX-OPS` / `CLS-BRK` | TB-06 | T | El retorno de autoridad o el mecanismo de emergencia se ejecuta sin doble control ni registro suficiente; la fase queda con dos fuentes de verdad activas y las escrituras posteriores no son reconciliables | P2 | I4 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-009` | `SEC-API-01` autenticación y autorización por operación en el adaptador; `SEC-NET-01` conducto restringido entre la plataforma y el legado; identidad técnica única y acotada por dirección | `SEC-LOG-01`/`SEC-SIEM-01` registro de cada escritura con origen, y contraste con el volumen esperado por turno | Suspender el conducto, revocar la credencial técnica y conciliar el período afectado; **evidencia esperada:** prueba con contrato, stub o versión acordada que demuestre el rechazo de un cliente no autorizado, sin modificar el esquema del TOS | ALTO | POR VALIDAR | `ESC-04`/`ESC-06` y `D2-DEP-002`: contrato, capacidad de escritura y soporte del TOS siguen sin confirmar |
| `THR-010` | Verificación de contrato y versión en la traducción; validación cruzada del identificador de contenedor y de la zona antes de aplicar; `SEC-API-01` validación de esquema y payload | Conciliación por turno con detección temprana; contraste posición registrada contra verificación física o telemétrica (`AST-002`, Decisión 2) | Revertir el estado aplicado, reconciliar y abrir investigación dentro de la ventana de 48 h; **evidencia esperada:** prueba con mensajes deliberadamente alterados y traza del rechazo | ALTO | POR VALIDAR | `D2-DEP-002`: A2/A3 deben entregar contrato, campos, versión y regla de conciliación por integración real |
| `THR-011` | Autoridad única por `dominio × zona × fase` declarada y aplicada en el adaptador; traspaso transaccional al cruzar zona; escritura idempotente con clave | Conciliación por turno; alerta por escritura parcial y por diferencia de gate no explicada al cierre diario | Restituir la autoridad declarada, marcar el período y escalar; **evidencia esperada:** matriz de autoridad probada, con demostración de traspaso y de detección→operación restituida ≤30 min en marcha blanca crítica | CRÍTICO | POR VALIDAR | `D2-DEP-002`: la matriz de autoridad es un producto de A3. D2 la exige, no la inventa |
| `THR-012` | Idempotencia con clave y ventana de deduplicación; secuencia por origen; reintento con backoff exponencial y jitter en lugar de reenvío inmediato | Detección de duplicados por clave; contraste de inventario y de cruces de zona por turno | Anular el movimiento duplicado con traza y recalcular el inventario afectado; **evidencia esperada:** prueba de reenvío masivo sin duplicación de movimiento | ALTO | POR VALIDAR | `D2-DEP-002`: ventana de deduplicación y clave dependen del contrato real |
| `THR-013` | Cola durable con DLQ; timeout explícito, circuit breaker y bulkhead por integración (Maestro §6.2); modo degradado visible para la operación | Medición de profundidad de cola y de antigüedad del mensaje más viejo; alerta antes de agotar la ventana de investigación | Activar el fallback declarado, preservar el orden y conciliar al restablecer; **evidencia esperada:** prueba de degradación del legado con contrato o stub acordado y medición del efecto sobre gate y nave | ALTO | POR VALIDAR | `ESC-04`/`D2-DEP-002`: no se presume disponibilidad, capacidad ni comportamiento del TOS bajo carga |
| `THR-014` | Mínimo privilegio y mínimo conjunto de datos en el contrato de lectura; `SEC-DATA-01` clasificación aplicada también al dato proveniente del legado | `SEC-LOG-01` registro de consulta sensible; revisión periódica del conjunto efectivamente leído contra el declarado | Reducir el alcance del contrato, purgar lo propagado indebidamente y revisar los destinos analíticos; **evidencia esperada:** inventario de campos leídos y justificación por finalidad | ALTO | POR VALIDAR | `D2-DEP-004`: sin el catálogo del Subdocumento 5 no puede afirmarse minimización efectiva |
| `THR-015` | Credencial técnica dedicada, con privilegios limitados a las operaciones del contrato; `SEC-SECRET-01` custodia y rotación; `SEC-ADM-01` cualquier uso ampliado pasa por elevación temporal registrada | `SEC-SIEM-01` alerta por operación fuera del catálogo permitido y por uso de la credencial desde origen no esperado | Revocar y reemitir el material, revisar el histórico de uso y conciliar; **evidencia esperada:** catálogo de operaciones autorizadas y prueba de rechazo fuera de él | CRÍTICO | ESCALADO | `ESC-04`/`ESC-06` y `D2-DEP-005`: el modelo de privilegios del TOS 2012 lo determina el fabricante o el contrato vigente, no D2 |
| `THR-016` | Doble control para el retorno normal y procedimiento de emergencia tipo break-glass explícitamente auditado (Maestro §8.8); registro obligatorio de los ocho campos de retorno (Maestro §12) | Alerta inmediata al activarse el mecanismo de emergencia; verificación de que solo una autoridad queda activa por dominio, zona y fase | Cerrar la autoridad duplicada, conciliar el período y revisar la activación con el responsable; **evidencia esperada:** ejercicio de retorno con doble control y expediente completo de los ocho campos | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-005`: A3 define el procedimiento; el CLIENTE nomina a quien autoriza el break-glass |

##### B2.3.3 `TB-05` — zona operacional/edge ↔ periferia de terreno

Cruce donde cambian el dispositivo, el firmware, el fabricante, el ambiente físico y la red operacional. Activos principales `AST-002`, `AST-003`, `AST-004`, `AST-012`, `AST-013` y `AST-015`. Clases `CLS-EDG` y `CLS-EXT`. D2 no propone intervenir el control de grúas, las barreras, la báscula ni el VMS: modela el conducto y el evento, conforme a la regla negativa 5 del Maestro.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-017` | AST-002/003/013 | periferia de posición, lectura óptica y acceso / `CLS-EXT`, `CLS-EDG` | TB-05 | S | Un equipo no inventariado se presenta como sensor de posición, lectura de contenedor o toma reefer, y sus eventos se aceptan porque el conducto confía en la red operacional en lugar de en la identidad del dispositivo | P3 | I3 | ALTO |
| `THR-018` | AST-003/005 | `CTX-GATE`, periferia de gate, `EDGE-RUN` / `CLS-EDG`, `CLS-EXT` | TB-05 | T | Una lectura o imagen de gate se repite o se altera y produce una entrada o salida que no ocurrió; el hecho no puede reconstruirse después y el cierre diario deja una diferencia sin explicación | P2 | I4 | ALTO |
| `THR-019` | AST-004/013 | `CTX-REEFER`, tomas y tableros, radioenlace de patio / `CLS-EDG`, `CLS-EXT` | TB-05 | D | La señal de una o varias tomas deja de llegar por silencio del equipo o por pérdida de cobertura con el patio cargado; la desviación de temperatura existe pero no se alarma dentro de los 5 minutos | P3 | I4 | CRÍTICO |
| `THR-020` | AST-004/012 | parámetros de alarma reefer en `CTX-REEFER` y `EDGE-RUN` / `CLS-EDG`, `CLS-SVC` | TB-05 + TB-11 | T | La banda o la duración de desviación se modifica localmente sin aprobación ni versionado y queda en un valor que hace imposible alarmar a tiempo; el sistema informa normalidad mientras la carga se degrada | P2 | I4 | ALTO |
| `THR-021` | AST-003/012/013 | conducto hacia periferia de acceso y tableros / `CLS-EDG`, `CLS-EXT` | TB-05 | E | Desde la zona operacional se alcanza un conducto no controlado hacia periferia y se emite un comando que el diseño nunca previó como operación remota | P2 | I4 | ALTO |
| `THR-022` | AST-015 | VMS conservado y red de protección / `CLS-EXT` | TB-05 + TB-09 | I | La integración de eventos o metadatos abre un camino por el que circula video completo o por el que la red de protección queda alcanzable desde la red operacional, degradando la separación aprobada | P2 | I4 | ALTO |
| `THR-023` | AST-011/012 | firmware y configuración de periferia / `CLS-EXT`, `CLS-EDG` | TB-05 + TB-12 | T | Una actualización de firmware o de configuración de terreno se instala sin verificación de procedencia ni retorno registrado, y altera el comportamiento del equipo durante una ventana en que no se puede intervenir | P2 | I3 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-017` | Identidad por dispositivo y no por pertenencia a la red; `SEC-NET-01` segregación de la zona operacional con conductos controlados; `SEC-HARD-01` endurecimiento y `SEC-EXP-01` inventario de lo que expone | `SEC-SIEM-01` alerta por dispositivo no inventariado y por evento cuyo emisor no corresponde a la zona; contraste de posición contra la verificación cruzada de la Decisión 2 | Aislar el equipo, invalidar sus eventos y reconciliar la posición afectada; **evidencia esperada:** inventario vigente de periferia con identidad por equipo y prueba de rechazo de un emisor desconocido | ALTO | POR VALIDAR | `ESC-06`/`ESC-10` y `D2-DEP-003`: contratos, protocolos y site survey no están levantados. No se presume identidad por dispositivo disponible en todas las familias |
| `THR-018` | Vinculación del evento de gate a la identidad de quien opera y a la evidencia asociada; deduplicación por clave de la lectura; sello de integridad del hecho en `SRV-EVID` conforme `SEC-LOG-01` | Conciliación de gate por turno con objetivo de cero diferencias no explicadas al cierre diario; alerta por lectura repetida o por secuencia imposible | Invalidar el hecho con traza, reabrir el expediente y conciliar antes de que venza la ventana de 24 h; **evidencia esperada:** prueba con lectura repetida y demostración de que el hecho no se duplica | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-003`: A2/A3 levantan barreras y lectura óptica; C1–C4 confirman equipamiento y capacidad |
| `THR-019` | Continuidad local de la función reefer sin dependencia de la nube; failover real del radioenlace y segregación de la red de patio; canal redundante de notificación con escalamiento | Supervisión de vivacidad por toma y tablero: la ausencia de dato se trata como condición alarmable y no como silencio normal; medición del tiempo dato→alarma | Escalar por el canal alternativo con confirmación identificada y activar la revisión física de la toma; **evidencia esperada:** prueba con patio cargado que mida la alarma extremo a extremo dentro de los 5 min y prueba de pérdida de cobertura | CRÍTICO | POR VALIDAR | `D2-DEP-003`/`ESC-10`: cobertura, radioenlace y capacidad dependen de C1–C4 y del site survey. La cantidad de tomas y tableros la fija Célula 2, no D2 |
| `THR-020` | Parámetro operacional versionado, con aprobador declarado y retorno; rechazo de valores incompatibles con la alarma ≤5 min conforme a la restricción vigente de `RN-11`; `SEC-ADM-01` para el cambio | `SEC-LOG-01` registro de cada cambio de parámetro con autor, valor anterior y posterior; alerta por parámetro fuera de la banda autorizada | Restituir el valor aprobado, revisar el período con el parámetro alterado y notificar a operación; **evidencia esperada:** historial de parámetros y prueba de rechazo de un valor que impida alarmar | ALTO | POR VALIDAR | `D2-DEP-001`/`D2-DEP-005`: la banda y la duración quedan sujetas a parametrización y validación del CLIENTE (Maestro §18.1). D2 no fija tolerancias |
| `THR-021` | `SEC-NET-01` conductos explícitos y denegación por defecto entre zona operacional y periferia; catálogo cerrado de comandos permitidos por familia; `SEC-ADM-01` para toda operación remota sobre equipamiento | `SEC-SIEM-01` alerta por comando fuera del catálogo y por operación remota fuera de ventana; registro correlacionado con la acción física observada | Cortar el conducto, revisar el estado físico del equipo y aplicar el retorno; **evidencia esperada:** matriz de conductos permitidos y denegados, y prueba de rechazo de un comando fuera de catálogo | ALTO | POR VALIDAR | `ESC-06`/`D2-DEP-003`: el catálogo de comandos por familia depende del levantamiento y de C3. D2 no propone operar grúas, barreras ni báscula |
| `THR-022` | Segregación IEC 62443 con conducto único y mínimo flujo (Decisión 19); transporte limitado a eventos, metadatos o evidencia confirmada; ninguna ruta por defecto que permita video completo por la red operacional | `SEC-SIEM-01` verificación de rutas efectivamente permitidas contra las declaradas; alerta por volumen incompatible con metadatos | Cerrar la ruta, verificar la continuidad del VMS y registrar el hallazgo como afectación de protección; **evidencia esperada:** prueba de rutas denegadas y permitidas, y demostración de continuidad del VMS durante la migración de red | ALTO | POR VALIDAR | `D2-DEP-003`/`D2-DEP-005`: C3 y el CLIENTE definen el conducto permitido y las responsabilidades ISPS. Regla negativa 6 y 7 del Maestro |
| `THR-023` | `SEC-SUPPLY-01`/`SEC-ART-01` procedencia y firma verificadas antes de instalar; registro de intervención con los ocho campos y retorno probado; respeto del congelamiento y de la restricción de no intervenir durante nave ni cuatro horas antes | `SEC-SIEM-01` detección de versión distinta a la aprobada en el inventario de periferia; verificación posterior del comportamiento esperado | Revertir a la versión aprobada con el retorno registrado y revisar el período afectado; **evidencia esperada:** expediente de intervención completo y prueba de retorno ejecutada en preproducción | ALTO | POR VALIDAR | `ESC-06`/`D2-DEP-003`: la verificación de firma en firmware de terceros depende del fabricante. Donde no exista, deberá declararse control compensatorio, no suponerse cumplida |

#### B2.4 Cobertura inicial de las siete clases

B2.3 ya modeló buena parte de `CLS-EDG`, `CLS-BRK` y `CLS-EXT` desde la frontera. Este apartado **completa** las categorías STRIDE que aquellas fronteras no cubrieron y agrega las clases restantes. No se duplican amenazas: cuando una clase ya quedó cubierta por una frontera prioritaria, la tabla de cobertura B2.5 lo indica con el `THR-*` correspondiente.

##### B2.4.1 `CLS-CAN` — canal

Portal, app instalable y cabina o terminal compartido, con su dispositivo y su sesión. Fronteras típicas `TB-01`, `TB-03` y `TB-05`.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-024` | AST-003/006/010 | `CH-PORTAL`, `SRV-IAM` / `CLS-CAN` | TB-01 + TB-03 | S | Un tercero se hace pasar por un usuario externo del portal —transportista o representante de una empresa— y obtiene citas, estado de carga o documentación que no le corresponden | P3 | I3 | ALTO |
| `THR-025` | AST-006/002 | `CH-CAB`, terminal compartida, `SRV-IAM` / `CLS-CAN` | TB-03 + TB-05 | S | El relevo de turno ocurre sin cierre efectivo de sesión, o un eventual con acreditación vencida sigue operando porque la terminal está aislada; las acciones se atribuyen a la persona equivocada | P3 | I3 | ALTO |
| `THR-026` | AST-010/006/013 | `CH-APP`, cola local cifrada / `CLS-CAN` | TB-01 + TB-04 | I | Un dispositivo con la app instalable se pierde o es sustraído con operaciones pendientes en su cola local; el material queda fuera del recinto y la revocación depende del enlace | P2 | I3 | ALTO |
| `THR-027` | AST-002/003 | `CH-APP`, `CH-PORTAL`, `GW-API` / `CLS-CAN`, `CLS-GWY` | TB-01 + TB-02 | T | El cliente se manipula para enviar operaciones fuera del rol, de la zona o de la fase, aprovechando que una validación quedó solo en la capa de presentación | P2 | I3 | ALTO |
| `THR-028` | AST-003 | `CH-PORTAL`, `GW-EDGE` / `CLS-CAN`, `CLS-GWY` | TB-01 | D | Tráfico automatizado o abuso de funciones públicas satura el portal durante el peak de gate; el autoservicio deja de responder dentro de los 60 s y la cola se desplaza al mostrador o a la vía pública | P3 | I3 | ALTO |
| `THR-029` | AST-005/006 | `SRV-EVID`, `CH-APP`, `CH-CAB` / `CLS-CAN`, `CLS-SVC` | TB-03 + TB-11 | R | Uno de los cuatro actos que requieren firma se ejecuta sin vínculo suficiente entre identidad, momento y evidencia; la contraparte lo repudia y el hecho no puede sostenerse ante una objeción | P2 | I4 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-024` | `SEC-IAM-01` autenticación conforme al estándar exigido, con segundo factor para accesos externos; representación de empresa vinculada a expediente y no solo a un correo | `SEC-SIEM-01` casos de acceso anómalo: origen inusual, intento masivo, cambio de representación; `SEC-LOG-01` registro de acceso a dato sensible | Bloquear la cuenta, revocar sesiones activas y revisar lo consultado; **evidencia esperada:** casos de acceso, suplantación y revocación probados con auditoría asociada | ALTO | POR VALIDAR | `F3-ESC-001` y `D2-DEP-001`: directorio, roles y proceso de representación aún no confirmados |
| `THR-025` | `SEC-IAM-01` identidad individual también en terminal compartida, relevo sin detención, expiración y revocación; credencial temporal vinculada a nombrada, con zonificación | `SEC-LOG-01` registro de relevo y de sesión activa por terminal; alerta por sesión sin actividad y por credencial usada fuera de su zona o de su vigencia | Cerrar la sesión, reasignar el turno y marcar el período de atribución dudosa; **evidencia esperada:** prueba de relevo y de revocación durante aislamiento local | ALTO | ESCALADO | `F3-ESC-002`: la baja ≤24 h frente a 8 h sin cobertura sigue bloqueada externamente. B2 no declara cumplida la revocación inmediata |
| `THR-026` | `SEC-ENC-01`/`SEC-FIELD-01` cifrado de la cola local y del material sensible; sesión con expiración y desbloqueo del dispositivo; mínimo dato retenido offline | `SEC-END-01` telemetría del dispositivo y detección de ausencia prolongada; `SEC-SIEM-01` alerta por intento de uso tras la denuncia | Revocar identidad y material, invalidar la cola pendiente y auditar lo sincronizado; **evidencia esperada:** prueba de revocación con dispositivo fuera de línea y de que la cola no es legible fuera de la app | ALTO | POR VALIDAR | `D2-DEP-004`: alcance de lo que puede almacenarse offline depende del catálogo del Subdocumento 5 |
| `THR-027` | Validación de autorización en el servicio y en `GW-API`, nunca solo en el cliente; `SEC-API-01` validación de esquema, identidad y objeto; `RBAC`+`ABAC` con contexto de zona y fase | `SEC-SIEM-01` alerta por operación fuera de rol, zona o fase; registro de rechazo con motivo | Rechazar y registrar la operación, revisar el patrón y ajustar la política; **evidencia esperada:** pruebas de acceso a objeto ajeno y de operación fuera de contexto | ALTO | POR VALIDAR | `D2-DEP-001`/`D2-DEP-002`: A1 confirma roles y A2 los contratos por operación |
| `THR-028` | `SEC-EDGE-01`/`SEC-EDGE-02` protección de bots, límites y anti-DDoS en el único borde público; cuotas por consumidor; cola virtual como mecanismo funcional de contención | Medición del tiempo de respuesta del portal contra el umbral de 60 s; alerta por patrón automatizado y por saturación en ventana de gate | Aplicar contención en el borde, degradar funciones no críticas y comunicar el estado; **evidencia esperada:** prueba de carga a 1,5× el peak declarado con el portal dentro de umbral | ALTO | POR VALIDAR | `D2-DEP-003`: capacidad y dimensionamiento del borde dependen de C3/C4 |
| `THR-029` | `SRV-EVID` con sello de integridad y vínculo identidad–acto–momento; `SEC-KEY-01` material de firma protegido; retención conforme al plazo declarado para evidencia facturable | `SEC-LOG-01` verificación periódica de integridad de la evidencia; alerta por acto sin evidencia asociada | Reconstituir el expediente, escalar la objeción y conservar la traza; **evidencia esperada:** prueba de verificación de integridad y de sostenimiento del acto ante objeción | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-004`: A2/A3 definen el esquema del acto; el Subdocumento 5 la retención por conjunto |

##### B2.4.2 `CLS-GWY` — gateway y borde

`GW-EDGE` y `GW-API`. Fronteras típicas `TB-01`, `TB-02` y `TB-03`.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-030` | AST-002/003/010 | `GW-API` / `CLS-GWY` | TB-02 | E | Una credencial válida se usa para leer o modificar un objeto que pertenece a otra empresa o a otra zona, porque la autorización se resuelve por ruta y no por objeto | P3 | I3 | ALTO |
| `THR-031` | AST-007 | `GW-API` / `CLS-GWY` | TB-02 | T | Un mensaje que no cumple el esquema o que usa una versión no soportada se acepta y deja estado inválido aguas abajo, que después se propaga al legado o al ERP | P2 | I3 | ALTO |
| `THR-032` | AST-007/013 | `GW-API`, `GW-EDGE` / `CLS-GWY` | TB-01 + TB-02 | D | Un consumidor —tercero o reintento agresivo propio— consume la capacidad compartida del gateway durante una nave, y las operaciones críticas compiten con tráfico diferible | P3 | I3 | ALTO |
| `THR-033` | AST-010 | `GW-EDGE`, `GW-API` / `CLS-GWY` | TB-01 + TB-02 | I | Mensajes de error, cabeceras o trazas revelan estructura interna, identificadores de negocio o datos que permiten inferir contenido y ruta de la carga | P2 | I2 | MEDIO |
| `THR-034` | AST-006/012 | plano de gestión del borde y del gateway / `CLS-GWY` | TB-01 + TB-10 | E | Una ruta administrativa o de configuración del borde queda alcanzable desde Internet, y quien la alcanza modifica políticas de exposición sin tocar la aplicación | P1 | I4 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-030` | `SEC-API-01` autorización a nivel de objeto además de a nivel de ruta; `SEC-IAM-01` atributos de empresa, zona y fase en la decisión de acceso | `SEC-SIEM-01` alerta por acceso a objeto ajeno y por enumeración de identificadores; `SEC-LOG-01` registro con sujeto y objeto | Revocar la sesión, revisar lo accedido y corregir la política; **evidencia esperada:** prueba dirigida de acceso a objeto ajeno con resultado denegado | ALTO | POR VALIDAR | `D2-DEP-001`/`D2-DEP-002`: propietarios de objeto y contratos por operación provienen de A1/A2 |
| `THR-031` | `SEC-API-01` validación de esquema e inspección de payload; versionado explícito del contrato y rechazo de versión no soportada | Registro de rechazo por esquema y por versión; alerta por incremento de rechazos de un consumidor | Rechazar el mensaje con motivo trazable y notificar a la contraparte; **evidencia esperada:** pruebas de contrato por versión, incluidas las de rechazo | ALTO | POR VALIDAR | `D2-DEP-002`: catálogo de contratos y versiones por integración lo entrega A2 |
| `THR-032` | `SEC-API-01` cuota y límite de tasa por consumidor; bulkhead entre familias de tráfico; prioridad declarada para las operaciones críticas | Medición por consumidor y alerta por consumo desproporcionado; correlación con ventana de nave o gate | Aplicar el límite, aislar al consumidor y comunicar la degradación; **evidencia esperada:** prueba de carga con un consumidor abusivo sin afectación de nave ni gate | ALTO | POR VALIDAR | `D2-DEP-003`: límites y capacidad dependen del dimensionamiento de C4 |
| `THR-033` | Respuestas de error sin detalle interno; separación entre traza para operación y mensaje para la contraparte; `SEC-DATA-01` clasificación aplicada también a metadatos | Revisión de respuestas en pruebas de seguridad; alerta por respuesta con contenido no previsto | Corregir la respuesta y evaluar lo divulgado; **evidencia esperada:** verificación en pentest previo a producción de que no se filtra estructura ni dato sensible | MEDIO | POR VALIDAR | `D2-DEP-004`: qué constituye dato sensible en cada respuesta depende del catálogo del Subdocumento 5 |
| `THR-034` | `SEC-NET-01` plano de gestión separado y no expuesto; `SEC-ADM-01` MFA y elevación temporal; `SEC-EXP-01` inventario de exposición verificado desde fuera | `SEC-SIEM-01` alerta por acceso administrativo desde origen público y por cambio de política de exposición | Cerrar la exposición, revertir la política y revisar el cambio; **evidencia esperada:** verificación externa periódica de exposición y registro de cambios con aprobación | ALTO | POR VALIDAR | `D2-DEP-003`: la topología y el bastión los define C3. Ningún producto queda seleccionado en D2 |

##### B2.4.3 `CLS-SVC` — servicio de negocio y servicio común

Contextos `CTX-*` y servicios `SRV-IAM`, `SRV-NOTIF` y `SRV-EVID`. Fronteras típicas `TB-02`, `TB-03` y `TB-11`.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-035` | AST-001/006 | `CTX-*` con identidad técnica compartida / `CLS-SVC` | TB-02 + TB-11 | E | Un contexto llama a otro con una identidad técnica de privilegio amplio; cualquier falla en uno permite operar en dominios que no le corresponden, incluida la autoridad operacional | P2 | I3 | ALTO |
| `THR-036` | AST-012 | reglas y parámetros de patio, prioridad, cita e inspección / `CLS-SVC` | TB-11 | T | Una regla parametrizable se modifica sin aprobación ni versionado; las decisiones del sistema cambian sin que exista un cambio de software que auditar | P2 | I3 | ALTO |
| `THR-037` | AST-007/013 | llamadas entre contextos y hacia `SRV-NOTIF` / `CLS-SVC` | TB-02 + TB-11 | D | Una llamada remota sin timeout ni cortocircuito propaga la degradación de un servicio común hacia gate o nave, convirtiendo una falla parcial en una detención general | P3 | I3 | ALTO |
| `THR-038` | AST-008 | observabilidad correlacionada nube/on-premise / `CLS-SVC` | TB-04 + TB-11 | R | Falta correlación extremo a extremo entre nube y terminal; una operación no puede reconstruirse en quién, cuándo y con qué efecto, y el punto ciego aparece justamente en el tramo local | P2 | I3 | ALTO |
| `THR-039` | AST-004/006 | `SRV-NOTIF` y sus adaptadores de canal / `CLS-SVC` | TB-03 + TB-11 | S | Una notificación crítica de frío se emite o se recibe por un canal cuya identidad no se confirma; el escalamiento parece cumplido pero nadie identificable lo recibió | P2 | I4 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-035` | Identidad técnica por servicio con permisos por operación; `SEC-IAM-01` mínimo privilegio y segregación de funciones; `SEC-SECRET-01` secretos separados por servicio | `SEC-SIEM-01` alerta por uso de identidad técnica fuera de su catálogo de operaciones | Revocar y reemitir el secreto, acotar el permiso y revisar el histórico; **evidencia esperada:** matriz servicio→operación permitida y prueba de denegación | ALTO | POR VALIDAR | `D2-DEP-001`: los límites de contexto y su criticidad los cierra A1 |
| `THR-036` | Parámetro versionado con aprobador, ventana y retorno registrado; separación entre quien propone y quien aprueba; `SEC-ADM-01` para el cambio en producción | `SEC-LOG-01` historial completo del cambio; alerta por modificación fuera de ventana o sin aprobación asociada | Restituir la versión aprobada y revisar las decisiones tomadas con el valor alterado; **evidencia esperada:** historial de parámetros y prueba de retorno | ALTO | POR VALIDAR | `D2-DEP-001`/`D2-DEP-003`: repositorio de reglas, aprobadores y despliegue los definen A1–A3 y C3 |
| `THR-037` | Timeout explícito, reintento con backoff y jitter, circuit breaker, bulkhead y límite de tasa (Maestro §6.2); modo reducido declarado y visible | Medición de latencia y de error por dependencia; alerta por apertura de cortocircuito y por degradación sostenida | Activar el modo reducido declarado y aislar la dependencia; **evidencia esperada:** prueba de caos previa a producción con la dependencia degradada y sin detención de gate ni nave | ALTO | POR VALIDAR | `D2-DEP-002`: los parámetros por interfaz dependen del contrato real; D2 no fija valores |
| `THR-038` | Identificador de correlación propagado en toda la cadena, incluida la operación local; `SEC-LOG-01` registro con el mismo identificador en ambos dominios | `SEC-SIEM-01` verificación de trazas incompletas y de tramos sin correlación | Completar la instrumentación del tramo ciego y reprocesar la investigación; **evidencia esperada:** reconstrucción íntegra de un recorrido crítico que atraviese nube y terminal | ALTO | POR VALIDAR | `D2-DEP-001`/`D2-DEP-003`: el inventario de fuentes y su dimensionamiento provienen de A1 y C4 |
| `THR-039` | Canal redundante con confirmación identificada y escalamiento declarado; identidad del emisor verificable por el destinatario; `SEC-IAM-01` para el destinatario interno | Verificación de confirmación de recepción por evento; alerta por alarma sin confirmación dentro del plazo | Escalar por el canal alternativo y registrar la falta de confirmación como incidente operacional; **evidencia esperada:** prueba de escalamiento con confirmación identificada y con el canal primario caído | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-005`: adaptadores por audiencia y responsables de recepción los define el CLIENTE |

##### B2.4.4 `CLS-BRK` — broker, colas y adaptadores

`INT-HUB` e `INT-TOS`. Complementa lo ya modelado en `TB-06` (`THR-009`..`THR-016`) y en `TB-04` (`THR-001`, `THR-002`, `THR-006`, `THR-008`).

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-040` | AST-007 | `INT-HUB`, colas y DLQ / `CLS-BRK` | TB-11 | D | Un consumidor lento —ERP, autoridad o ferrocarril— retiene la capacidad compartida del bus y bloquea el intercambio de otras familias, incluidas las de nave y gate | P3 | I3 | ALTO |
| `THR-041` | AST-005/007 | reproceso desde DLQ / `CLS-BRK` | TB-07 + TB-11 | T | Un mensaje se reprocesa desde la cola de mensajes fallidos sin clave de idempotencia y genera un segundo hecho facturable; el ERP recibe dos veces lo mismo | P2 | I4 | ALTO |
| `THR-042` | AST-010 | mensajes retenidos en colas y DLQ / `CLS-BRK`, `CLS-DAT` | TB-11 | I | Mensajes con datos personales, comerciales o de ruta permanecen en colas y en la cola de fallidos por tiempo indefinido, fuera del ciclo de vida declarado para su conjunto de datos | P2 | I3 | ALTO |
| `THR-043` | AST-001/010 | adaptadores con acceso directo a almacenes / `CLS-BRK`, `CLS-DAT` | TB-11 | E | Un adaptador consulta o escribe directamente en el almacén en lugar de pasar por el servicio propietario, puenteando la autorización y las reglas de negocio | P2 | I3 | ALTO |
| `THR-044` | AST-002/007 | publicación de eventos en el bus / `CLS-BRK` | TB-11 | S | Un productor no autorizado publica un evento de movimiento o de gate que el resto del sistema consume como verdadero, sin que exista un origen físico correspondiente | P2 | I4 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-040` | Bulkhead por familia de integración; cuota por consumidor; cola durable con capacidad declarada por familia | Medición de profundidad y de antigüedad por cola; alerta por consumidor estancado | Aislar la familia afectada, aplicar el fallback declarado y conciliar al restablecer; **evidencia esperada:** prueba con un consumidor detenido y demostración de que las demás familias siguen operando | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-003`: las 21 contrapartes y las 7 familias requieren contrato y dimensionamiento reales |
| `THR-041` | Idempotencia con clave y ventana de deduplicación en todo reproceso; conciliación 1:1 hecho↔evidencia antes de entregar al ERP | Detección de duplicados por clave; conciliación periódica contra el ERP con diferencia esperada cero | Anular el duplicado con traza, notificar la objeción y corregir el reproceso; **evidencia esperada:** prueba de reproceso masivo desde DLQ sin duplicar hechos | ALTO | POR VALIDAR | `D2-DEP-002`: el contrato del ERP y su regla de conciliación los entrega A2 |
| `THR-042` | Ciclo de vida declarado también para colas y DLQ; `SEC-ENC-01`/`SEC-FIELD-01` cifrado en reposo y por campo; minimización del contenido del mensaje | `SEC-LOG-01` inventario de mensajes retenidos y su antigüedad; alerta por retención fuera de plazo | Purgar conforme al plazo declarado y revisar el contenido de los contratos; **evidencia esperada:** demostración de que la retención en cola respeta el plazo de su conjunto de datos | ALTO | POR VALIDAR | `D2-DEP-004`: sin catálogo campo→retención no puede fijarse el plazo por cola |
| `THR-043` | Acceso al almacén únicamente a través del servicio propietario; `SEC-DATA-01` autorización por servicio y no por red; credenciales de base separadas y acotadas | `SEC-SIEM-01` alerta por conexión directa no prevista al almacén; registro de consulta sensible | Cerrar el acceso directo, revisar lo consultado y reencaminar por el servicio; **evidencia esperada:** inventario de consumidores por almacén y prueba de denegación de acceso directo | ALTO | POR VALIDAR | `D2-DEP-001`/`D2-DEP-002`: propietario de cada almacén y consumidores autorizados provienen de A1/A2 |
| `THR-044` | Autorización de publicación por tópico y por productor; identidad técnica acotada; validación de esquema del evento | `SEC-SIEM-01` alerta por productor desconocido y por evento sin origen físico correlacionable | Invalidar el evento, revocar la identidad y reconciliar el inventario; **evidencia esperada:** prueba de publicación no autorizada rechazada y registrada | ALTO | POR VALIDAR | `D2-DEP-002`: catálogo de tópicos, productores y esquemas lo entrega A2 |

##### B2.4.5 `CLS-DAT` — datos, claves y evidencia

`DATA-CORE`, `DATA-TS`, `DATA-DOC`, `DATA-AN`, repositorio de logs, material criptográfico y respaldos. Fronteras típicas `TB-11`, `TB-13` y `TB-14`.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-045` | AST-010 | `DATA-CORE`, `DATA-AN` / `CLS-DAT` | TB-11 | I | Analítica, reportería o soporte consultan directamente el almacén operacional y acceden a campos personales, comerciales o que permiten inferir contenido y ruta | P3 | I3 | ALTO |
| `THR-046` | AST-004 | `DATA-TS` / `CLS-DAT` | TB-11 + TB-14 | T | Series de temperatura se alteran o se eliminan; la evidencia continua que debe conservarse durante el plazo declarado deja de sostener una reclamación por carga refrigerada | P2 | I4 | ALTO |
| `THR-047` | AST-008 | repositorio de logs / `CLS-DAT` | TB-11 + TB-14 | R | El registro de auditoría se altera, se trunca o pierde la ventana declarada de 12 meses en línea más 24 en archivo; una investigación posterior no puede sostenerse | P2 | I4 | ALTO |
| `THR-048` | AST-009 | KMS/HSM/vault y material de recuperación / `CLS-DAT` | TB-11 + TB-14 | I + E | El material criptográfico se expone o se exporta y permite suplantar servicios o descifrar datos; o bien se pierde y vuelve indescifrable información que la operación necesita | P1 | I4 | ALTO |
| `THR-049` | AST-009/013 | respaldo, archivo y DR / `CLS-DAT` | TB-14 | D | El respaldo no es restaurable, o está cifrado bajo una clave alcanzable por la misma autoridad que puede borrarlo; el escenario de pérdida se descubre en la restauración | P2 | I4 | ALTO |
| `THR-050` | AST-010 | ambientes DEV/QA/PREPROD / `CLS-DAT` | TB-13 | I | Datos productivos se usan en ambientes no productivos sin anonimización verificable, ampliando el conjunto de personas y sistemas que los alcanzan | P2 | I3 | ALTO |
| `THR-051` | AST-002/005 | migración y carga histórica / `CLS-DAT` | TB-11 | T | La migración rompe la relación 1:1 entre hecho y evidencia, o incorpora posiciones no verificadas al corte; el error se hereda como estado inicial y contamina la conciliación posterior | P2 | I4 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-045` | `SEC-DATA-01` acceso por clasificación y a través del servicio propietario; `SEC-FIELD-01` cifrado de campo sensible; conjuntos analíticos derivados y minimizados | `SEC-LOG-01` registro de consulta sensible; `SEC-SIEM-01` alerta por consulta directa o por volumen inusual | Cerrar el acceso, revisar lo consultado y sustituirlo por un conjunto derivado; **evidencia esperada:** inventario de consumidores por almacén y prueba de denegación de consulta directa | ALTO | POR VALIDAR | `D2-DEP-004`: la clasificación por campo la entrega el Subdocumento 5; D1 propone `PUB/INT/CONF/RES` |
| `THR-046` | Almacenamiento con integridad verificable y escritura no destructiva para la serie; `SEC-BKP-01` copia inmutable; separación entre quien opera y quien puede borrar | Verificación periódica de integridad y de continuidad de la serie; alerta por vacío o por corrección retroactiva | Restaurar desde copia inmutable y registrar la corrección con traza; **evidencia esperada:** prueba de restauración dirigida de un período de temperatura y verificación de integridad | ALTO | POR VALIDAR | `D2-DEP-003`/`D2-DEP-004`: capacidad, producto y plazo por conjunto dependen de C2/C4 y del Subdocumento 5 |
| `THR-047` | `SEC-LOG-01` registro inalterable con la ventana declarada; separación de funciones entre operación y custodia del registro; `SEC-KEY-01` claves de archivo separadas | `SEC-SIEM-01` verificación de continuidad e integridad; alerta por vacío de secuencia o por intento de modificación | Aislar la fuente, restaurar desde archivo y escalar como incidente de seguridad; **evidencia esperada:** prueba de inmutabilidad y de recuperación desde archivo dentro del plazo | ALTO | POR VALIDAR | `D2-DEP-003`/`D2-DEP-005`: dimensionamiento por C4; custodios y acceso los define el CLIENTE |
| `THR-048` | `SEC-KEY-01`/`SEC-SECRET-01` raíz no exportable, jerarquía y ámbitos separados nube/local, rotación declarada y separación de funciones; material de recuperación bajo custodia dividida | Registro de toda operación con claves; alerta por exportación, por uso fuera de ámbito y por acceso al material de recuperación | Rotar y reemitir, revocar lo derivado y evaluar el alcance de lo descifrable; **evidencia esperada:** prueba de rotación sin detención y prueba de recuperación con custodia dividida | ALTO | POR VALIDAR | `F3-DEC-002`/`ADR-009` sigue `PROPUESTO`: no hay producto, período de rotación ni custodios aprobados |
| `THR-049` | `SEC-BKP-01` esquema 3-2-1-1-0 con copia inmutable y fuera de línea; claves de respaldo fuera de la autoridad que puede borrar; restauración probada mensualmente | Verificación automática de la copia y de su integridad; alerta por respaldo no completado o no verificable | Recuperar desde la copia alternativa y activar el plan de DR; **evidencia esperada:** restauración documentada mensual y conmutación semestral con informe | ALTO | POR VALIDAR | `D2-DEP-003`: ubicación, producto, separación de autoridad, RPO/RTO y capacidad los definen C1–C4 |
| `THR-050` | `SEC-NPDATA-01` datos sintéticos por defecto y anonimización o seudonimización verificable; `SEC-PROD-01` separación de ambientes y prohibición de copia directa | Verificación del origen del conjunto usado en cada ambiente; alerta por conjunto no declarado | Eliminar el conjunto, revisar quién accedió y reemplazarlo por material sintético; **evidencia esperada:** demostración de no reversibilidad y registro de eliminación | ALTO | POR VALIDAR | `D2-DEP-004`: las técnicas aplicables por campo dependen del Subdocumento 5 |
| `THR-051` | Conciliación por universo antes de habilitar el estado inicial; posición verificada físicamente al corte como condición de carga; relación 1:1 verificada para hechos y evidencias | Contraste por universo migrado y por muestra dirigida; alerta por diferencia sobre el umbral declarado | Detener la habilitación, corregir el universo y repetir la conciliación; **evidencia esperada:** informe de conciliación por universo y prueba de recuperación dirigida | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-004`: el alcance y el umbral de diferencia aceptable los definen A2/A3 y el Subdocumento 5 |

##### B2.4.6 `CLS-EDG` — runtime local y buffer

Complementa lo ya modelado en `TB-04` (`THR-001`..`THR-008`) y en `TB-05` (`THR-017`..`THR-023`), con las condiciones propias del emplazamiento y del ciclo de cambio.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-052` | AST-009/013 | gabinete y nodo local / `CLS-EDG` | TB-05 + TB-10 | E + I | El acceso físico al gabinete o al nodo permite arranque alterno, extracción de almacenamiento o conexión de consola, y con ello alcanzar datos y material criptográfico locales | P2 | I4 | ALTO |
| `THR-053` | AST-012/013 | configuración del runtime local / `CLS-EDG` | TB-04 + TB-05 | T | Tras una intervención en terreno, la configuración local queda distinta de la aprobada y nadie lo detecta hasta el siguiente incidente; no existe expediente de retorno con los ocho campos exigidos | P2 | I3 | ALTO |
| `THR-054` | AST-013/015 | nodo local, energía y ambiente / `CLS-EDG` | TB-05 | D | El nodo local se pierde por energía, temperatura o corrosión durante el congelamiento, cuando el calendario impide intervenir; la autonomía de 72 h deja de existir justo cuando se la necesita | P2 | I4 | ALTO |
| `THR-055` | AST-010/014 | retención local posterior a la reconciliación / `CLS-EDG`, `CLS-DAT` | TB-04 + TB-14 | I | El nodo conserva datos operacionales y personales más allá de lo necesario tras sincronizar, ampliando la superficie expuesta en el ambiente menos controlado | P2 | I2 | MEDIO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-052` | Control de acceso físico a sala y gabinetes; `SEC-ENC-01` cifrado en reposo del almacenamiento local; `SEC-HARD-01` arranque y consola restringidos; material criptográfico local protegido | Registro de apertura y de acceso físico correlacionado con la intervención autorizada; `SEC-END-01` detección en el nodo | Aislar el nodo, rotar el material local y verificar integridad antes de reincorporarlo; **evidencia esperada:** prueba de que el almacenamiento extraído no es legible y registro de acceso físico | ALTO | POR VALIDAR | `D2-DEP-003`: sala, gabinetes y control de acceso físico son decisión de C1–C3 y del `ADR-005` aún abierto |
| `THR-053` | Configuración versionada y desplegada desde el repositorio aprobado; expediente de intervención con los ocho campos y retorno probado; `SEC-ADM-01` para el cambio local | Verificación periódica de la configuración efectiva contra la declarada; alerta por desviación | Restituir la configuración aprobada y completar el expediente; **evidencia esperada:** comparación configuración efectiva vs. declarada y prueba de retorno | ALTO | POR VALIDAR | `D2-DEP-003`: herramienta, repositorio y responsables los define C3 |
| `THR-054` | Redundancia efectiva del nodo y de su energía; protección marina por clase y emplazamiento; planificación de intervenciones fuera del congelamiento y fuera de ventana de nave | Monitoreo ambiental y de energía con aviso anticipado; verificación periódica de la redundancia real, no solo declarada | Conmutar al nodo redundante y activar el procedimiento manual declarado mientras se repone; **evidencia esperada:** prueba de pérdida de un nodo con continuidad de las cinco funciones críticas | ALTO | POR VALIDAR | `ESC-07`/`ESC-09` y `D2-DEP-003`: protección marina, sala y redundancia siguen abiertas. La independencia real se evalúa como SPOF en B4 |
| `THR-055` | Retención local mínima y purga tras la reconciliación confirmada; `SEC-DATA-01` clasificación aplicada al dato local | Inventario de lo retenido localmente y su antigüedad; alerta por retención fuera de plazo | Purgar conforme al plazo declarado y ajustar el conjunto que se replica al edge; **evidencia esperada:** demostración de purga posterior a la sincronización confirmada | MEDIO | POR VALIDAR | `D2-DEP-004`: qué debe permanecer localmente depende del catálogo del Subdocumento 5 |

##### B2.4.7 `CLS-EXT` — terceros y sistemas conservados

Navieras, autoridades, ferrocarril, concedente, ERP, VMS y periferia. Complementa lo modelado en `TB-06` para el TOS y en `TB-05` para la periferia. Ningún contrato, versión, plazo ni disponibilidad de tercero se supone: `ESC-06` y `ESC-14` siguen abiertos.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-056` | AST-016/007 | mensajería de nave con navieras / `CLS-EXT` | TB-08 | S | Un emisor se presenta como una naviera y entrega mensajería de nave que el sistema acepta como legítima; el plan o la orden resultante se ejecuta sobre carga real | P2 | I4 | ALTO |
| `THR-057` | AST-016 | intercambio EDIFACT por naviera / `CLS-EXT`, `CLS-BRK` | TB-08 | T | Un mensaje se altera o se repite, o la contingencia obliga a redigitar; el resultado rompe el compromiso de mensajería estándar exclusiva sin puente ni redigitación para las líneas de la alianza | P2 | I3 | ALTO |
| `THR-058` | AST-003/007 | autoridades y ferrocarril / `CLS-EXT` | TB-08 | D | Una autoridad o el ferrocarril no está disponible y no existe canal asistido trazable; el expediente queda incompleto y el camión no puede salir a ruta con documentación validada | P3 | I3 | ALTO |
| `THR-059` | AST-005 | ERP / `CLS-EXT` | TB-07 | R | Un hecho facturable se reenvía tras un error y el ERP lo repudia o lo duplica; la objeción no puede resolverse porque falta la conciliación 1:1 con la evidencia | P2 | I4 | ALTO |
| `THR-060` | AST-010 | contratos con terceros / `CLS-EXT` | TB-07 + TB-08 | I | Un contrato entrega más campos de los necesarios y expone datos comerciales o que permiten inferir contenido y ruta hacia una organización que no los requiere para su función | P2 | I3 | ALTO |
| `THR-061` | AST-015 | VMS conservado y red de protección / `CLS-EXT` | TB-09 | D | La integración o la migración de red degrada la disponibilidad del VMS o de la protección ISPS; la modernización termina restando capacidad de protección en lugar de sumarla | P2 | I4 | ALTO |
| `THR-062` | AST-006/011/012 | acceso remoto de proveedores y fabricantes / `CLS-EXT` | TB-05 + TB-10 | E | Un proveedor accede remotamente a periferia o a un sistema conservado con una vía permanente, sin ventana acotada, sin aprobación por sesión y sin grabación | P3 | I4 | CRÍTICO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-056` | Autenticidad del emisor verificable por contrato y por canal; `SEC-EDGE-02`/`SEC-API-01` en el punto de recepción; aceptación solo desde contrapartes inventariadas | `SEC-SIEM-01` alerta por emisor no inventariado y por mensaje fuera del patrón acordado con esa línea | Rechazar y aislar el mensaje, notificar a la contraparte y revisar lo ya aplicado; **evidencia esperada:** prueba extremo a extremo por contraparte, incluida la de rechazo de un emisor falso | ALTO | POR VALIDAR | `ESC-01`/`ESC-06` y `D2-DEP-002`: contratos, versiones por naviera y mecanismo de autenticidad no están levantados |
| `THR-057` | Versionado por naviera; cola durable con deduplicación; no repudio del intercambio; procedimiento de contingencia que preserve la traza sin convertirse en redigitación rutinaria | Conciliación por mensaje y por versión; alerta por repetición y por uso del procedimiento de contingencia | Reprocesar con la versión correcta, registrar el uso de contingencia y escalarlo como riesgo del programa 2029; **evidencia esperada:** pruebas por contraparte y por versión, con medición del uso de contingencia | ALTO | ESCALADO | `ESC-01`: fecha y líneas de la alianza siguen `PENDIENTE CLIENTE`; el compromiso de cero redigitación no se declara cumplido |
| `THR-058` | Canal asistido registrado como fallback declarado cuando no exista interfaz; cola durable con reintento; expediente trazable por trámite | Medición de disponibilidad por contraparte y de antigüedad del trámite pendiente; alerta antes del vencimiento operacional | Activar el canal asistido, registrar el expediente y comunicar el estado al transportista; **evidencia esperada:** prueba del fallback con expediente completo y trazable | ALTO | POR VALIDAR | `ESC-14`/`D2-DEP-005`: plazo e interfaz de cada autoridad se levantan en los primeros meses; D2 no supone ninguna |
| `THR-059` | Idempotencia en el reenvío; sello de integridad del hecho y de su evidencia; conciliación 1:1 antes y después de la entrega | Conciliación periódica con diferencia esperada cero; alerta por hecho sin evidencia y por evidencia sin hecho | Anular el duplicado o reemitir el faltante con traza, y resolver la objeción con el expediente; **evidencia esperada:** prueba de reenvío sin duplicación y de sostenimiento del hecho ante objeción | ALTO | POR VALIDAR | `D2-DEP-002`: el contrato del ERP, sus campos y su regla de objeción los entrega A2. El ERP no se reemplaza |
| `THR-060` | Mínimo conjunto de datos por contrato, justificado por finalidad; `SEC-DATA-01` clasificación aplicada al intercambio; revisión del contrato antes de habilitarlo | Revisión periódica de lo efectivamente enviado contra lo declarado; alerta por campo no previsto | Reducir el contrato, notificar y evaluar el alcance de lo divulgado; **evidencia esperada:** inventario campo→destinatario→finalidad por contrato | ALTO | POR VALIDAR | `D2-DEP-004`/`D2-DEP-005`: el catálogo de campos y la base de licitud dependen del Subdocumento 5 y del CLIENTE |
| `THR-061` | Segregación IEC 62443 con conducto mínimo; continuidad del VMS durante la migración de red como condición de la intervención; ninguna dependencia del VMS respecto de la plataforma nueva | Verificación de disponibilidad del VMS antes, durante y después de cada intervención; alerta por degradación de la red de protección | Revertir la intervención con el retorno registrado y restituir la protección antes de continuar; **evidencia esperada:** prueba de continuidad del VMS durante la migración, con informe | ALTO | POR VALIDAR | `D2-DEP-003`/`D2-DEP-005`: conducto, responsabilidades ISPS y ventana de intervención los definen C3 y el CLIENTE |
| `THR-062` | `SEC-ADM-01` acceso de terceros solo por elevación temporal, aprobada por sesión y grabada; sin vía permanente; `SEC-NET-01` origen acotado | `SEC-SIEM-01` alerta por sesión de proveedor fuera de ventana o sin aprobación; inventario de accesos vigentes revisado periódicamente | Cortar la sesión, revocar el acceso y revisar lo ejecutado; **evidencia esperada:** registro de sesión grabada con aprobación asociada y revisión periódica de accesos de terceros | CRÍTICO | ESCALADO | `ESC-06`/`D2-DEP-005`: los contratos de soporte de fabricantes y su modelo de acceso no están levantados. Es un riesgo de terceros, no una decisión de D2 |

##### B2.4.8 Complemento para cerrar la cobertura mínima por clase

La auditoría interna de B2.5 detectó cuatro casillas STRIDE sin amenaza propia. Se agregan aquí en lugar de declararlas cubiertas por analogía.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-063` | AST-006/008 | `GW-API`, `GW-EDGE` / `CLS-GWY` | TB-02 + TB-11 | R | El gateway no conserva la decisión de autorización asociada a la operación; después no puede demostrarse por qué se permitió o se denegó un acceso, y la contraparte lo discute | P2 | I3 | ALTO |
| `THR-064` | AST-002/003/006 | `CH-APP` en operación local / `CLS-CAN`, `CLS-EDG` | TB-04 + TB-05 | E | Una función habilitada durante la operación desconectada permite a un usuario de terreno actuar con un alcance que en línea requeriría un rol superior o una aprobación, y el exceso solo se descubre al reconciliar | P2 | I3 | ALTO |
| `THR-065` | AST-007/016 | `GW-EDGE` / `CLS-GWY`, `CLS-EXT` | TB-01 + TB-08 | S | El borde acepta tráfico como proveniente de una contraparte inventariada apoyándose en un atributo declarado por el propio emisor, en lugar de en una identidad verificable | P2 | I3 | ALTO |
| `THR-066` | AST-010 | respuestas y eventos entre contextos / `CLS-SVC` | TB-02 + TB-11 | I | Un contexto entrega en su respuesta o publica en su evento más atributos de los que el consumidor necesita; el dato sensible se propaga entre contextos y hacia analítica sin decisión explícita | P2 | I2 | MEDIO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-063` | `SEC-API-01` registro de la decisión de autorización junto a la operación; `SEC-LOG-01` conservación inalterable con la ventana declarada | Verificación de que toda operación sensible tiene decisión registrada; alerta por operación sin traza de autorización | Completar la instrumentación y reconstruir el caso con la evidencia disponible; **evidencia esperada:** reconstrucción de una decisión de acceso a partir del registro | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-003`: qué operaciones exigen decisión registrada depende de A2 y del dimensionamiento de C4 |
| `THR-064` | Catálogo explícito de funciones habilitadas offline y de su alcance por rol; aprobación diferida obligatoria para las que exceden el rol; `SEC-IAM-01` con contexto de zona y fase | Marcado del acto ejecutado en modo local y revisión obligatoria al reconciliar; alerta por acto fuera de alcance | Revertir o convalidar el acto con el responsable y registrar la excepción; **evidencia esperada:** prueba de 72 h con actos fuera de alcance detectados y resueltos al reconectar | ALTO | POR VALIDAR | `D2-DEP-002`/`D2-DEP-005`: A3 declara qué funciones quedan disponibles offline; el CLIENTE define quién convalida |
| `THR-065` | Identidad verificable de la contraparte en el punto de recepción; `SEC-EDGE-02`/`SEC-API-01`; ningún control de acceso basado solo en atributo autodeclarado | `SEC-SIEM-01` alerta por discordancia entre identidad verificada y atributo declarado | Rechazar, registrar y revisar lo aceptado previamente por esa vía; **evidencia esperada:** prueba de rechazo con atributo suplantado | ALTO | POR VALIDAR | `ESC-06`/`D2-DEP-002`: el mecanismo de identidad disponible depende del contrato de cada contraparte |
| `THR-066` | Contrato de salida por consumidor con el mínimo conjunto de atributos; `SEC-DATA-01` clasificación aplicada al evento y a la respuesta | Revisión periódica de atributos efectivamente publicados contra los declarados; alerta por atributo no previsto | Reducir el contrato y revisar los consumidores alcanzados; **evidencia esperada:** inventario atributo→consumidor→finalidad por contexto | MEDIO | POR VALIDAR | `D2-DEP-004`: la sensibilidad por atributo la entrega el Subdocumento 5 |

#### B2.5 Cobertura STRIDE alcanzada por clase

Cobertura del **método**, no del inventario final de componentes. Las casillas se cierran con amenazas concretas; una casilla sin `THR-*` propio se declara abierta en lugar de darse por cubierta.

| Clase | S | T | R | I | D | E |
|---|---|---|---|---|---|---|
| `CLS-CAN` | THR-024, THR-025 | THR-027, THR-067 | THR-029 | THR-026 | THR-028 | THR-064 |
| `CLS-GWY` | THR-065 | THR-031 | THR-063 | THR-033 | THR-032 | THR-030, THR-034 |
| `CLS-SVC` | THR-039 | THR-036 | THR-038 | THR-066 | THR-037 | THR-035 |
| `CLS-BRK` | THR-009, THR-044 | THR-010, THR-012, THR-016, THR-041 | THR-011 | THR-014, THR-042 | THR-013, THR-040 | THR-015, THR-043 |
| `CLS-DAT` | THR-072 | THR-046, THR-051 | THR-047, THR-070 | THR-045, THR-050, THR-055 | THR-049 | THR-048 |
| `CLS-EDG` | THR-001, THR-017, THR-069 | THR-002, THR-008, THR-018, THR-020, THR-023, THR-053 | THR-003 | THR-004, THR-052 | THR-005, THR-006, THR-019, THR-054, THR-068 | THR-007, THR-021, THR-069 |
| `CLS-EXT` | THR-056, THR-069 | THR-057 | THR-059, THR-070 | THR-022, THR-060 | THR-058, THR-061, THR-073 | THR-062, THR-069 |

**Nota de actualización.** Esta tabla incorpora `THR-067`..`THR-070`, agregadas en `B3.14`, y `THR-072/073`, agregadas en B6. `B2.6` conserva la distribución histórica del cierre de B2; el corte vigente queda en B6.8.

**Lecturas obligatorias de esta tabla**

- `CLS-DAT` / S queda cerrada a nivel de modelo por `THR-072`: la identidad falsa de un almacén o réplica es distinta de suplantar al productor (`THR-044`) o elevar privilegios sobre el almacén legítimo (`THR-043`). La implementación y prueba siguen pendientes.
- Tres amenazas registran dos categorías: `THR-048` (`I`+`E`), `THR-052` (`E`+`I`) y `THR-069` (`S`+`E`, agregada en B3). Se conservan unidas porque comparten activo, condición y control; separarlas produciría dos filas con la misma evidencia.
- Varias amenazas aparecen en más de una clase porque la frontera las cruza. La clase no reemplaza el inventario: `THR-013` contra el TOS y `THR-058` contra una autoridad comparten patrón de indisponibilidad, pero conservan contraparte, fallback y evidencia distintos.

#### B2.6 Distribución de riesgo y regla de no aceptación

| Nivel | Cantidad | Amenazas |
|---|---:|---|
| CRÍTICO | 5 | `THR-005`, `THR-011`, `THR-015`, `THR-019`, `THR-062` |
| ALTO | 58 | el resto, salvo las tres de nivel medio |
| MEDIO | 3 | `THR-033`, `THR-055`, `THR-066` |
| BAJO | 0 | — |

La ausencia de nivel `BAJO` no es un error de calibración: **el residual proyectado se mantiene igual al inherente en todas las filas**, porque ningún control citado tiene todavía producto, ubicación, responsable ni prueba ejecutada. Bajar un residual antes de eso convertiría un diseño documental en una mitigación acreditada.

Consecuencias que B2 deja fijadas y que B3–B8 no pueden relajar sin fundamento:

1. **Ningún riesgo queda aceptado.** No existe fila `ACEPTADO` y no puede crearse una sin aprobador nominado, fundamento, evidencia y condición de revisión.
2. **Las cinco amenazas críticas son entradas obligatorias de B4.** `THR-005`, `THR-011`, `THR-015`, `THR-019` y `THR-062` describen condiciones que, sin independencia real, se convierten en puntos únicos de falla; B4 debe evaluarlas como tales y no darlas por resueltas con la mención de un control.
3. **Ninguna amenaza puede cerrarla D2 por sí sola.** Las 66 dependen de un insumo externo: 62 `POR VALIDAR` y 4 `ESCALADO`. Estas últimas no dependen siquiera de los demás frentes: `THR-015` y `THR-062` por el modelo de privilegios y de acceso remoto de terceros (`ESC-04`, `ESC-06`); `THR-025` por la revocación durante aislamiento (`F3-ESC-002`); `THR-057` por la fecha y las líneas de la alianza (`ESC-01`).
4. **Un control citado no está implementado ni probado.** Todas las celdas de evidencia describen pruebas previstas. `SEC-PHYS-v0.1` sigue sin intercambiarse y `ADR-008`/`ADR-009`/`ADR-010` siguen sin aprobarse.

#### B2.7 Auditoría del bloque B2

| Comprobación | Resultado | Estado |
|---|---|---|
| escala de probabilidad e impacto definida antes de valorar | `B2.1` con cuatro niveles de cada eje, matriz de riesgo y criterio de asignación anclado a umbrales del caso | CONFORME |
| siete clases con cobertura STRIDE inicial | 7/7 clases con amenaza propia en las seis categorías, salvo `CLS-DAT` / S, declarada abierta y no simulada | CONFORME CON EXCEPCIÓN DECLARADA |
| fronteras prioritarias desarrolladas primero | `TB-04` (`THR-001`..`THR-008`), `TB-06` (`THR-009`..`THR-016`) y `TB-05` (`THR-017`..`THR-023`) | CONFORME |
| campos obligatorios por amenaza | 66/66 amenazas con activo, componente o clase, frontera, categoría, condición y escenario, probabilidad, impacto, control preventivo, control detectivo, respuesta con evidencia esperada, residual, estado y validación pendiente | CONFORME |
| identificadores estables y únicos | `THR-001`..`THR-066` correlativos, sin reutilización y sin renumeración de B1 | CONFORME |
| controles `SEC-*` existentes en D1 | todos los citados pertenecen al catálogo de D1; ninguno inventado | CONFORME |
| separación diseño / evidencia futura / evidencia ejecutada | ninguna celda declara evidencia ejecutada; toda prueba se enuncia como prevista | CONFORME |
| riesgos aceptados | ninguno; estados usados: `POR VALIDAR` (62) y `ESCALADO` (4). Ningún estado que D2 pueda cerrar por sí solo | CONFORME |
| ADR aprobados o SPOF cerrados en B2 | ninguno; `ADR-008` sigue `EN ANÁLISIS`, `ADR-009`/`ADR-010` siguen `PROPUESTO` | CONFORME |
| APIs, protocolos, puertos, productos, topología, historial, cantidades o precios inventados | no detectados; las cifras usadas provienen del Maestro y del Caso 06 y se citan como umbral, no como medición | CONFORME |
| dependencias visibles | `D2-DEP-001..005` citadas en las celdas de validación pendiente y conservadas íntegras en su tabla | CONFORME |
| diagrama final | no producido; corresponde a B8 | CONFORME |
| cobertura de RT-11.02 | existe metodología declarada y amenazas por clase e integración; **no** existe cobertura por componente real ni evidencia de actualización ante cambios | PARCIAL — `EN CURSO`, no cumplido |

**Hallazgo interno `B2-F01`:** la primera redacción de la cobertura por clase dejaba cuatro casillas STRIDE sin amenaza propia (`CLS-CAN`/E, `CLS-GWY`/S, `CLS-GWY`/R y `CLS-SVC`/I). Se corrigió agregando `THR-063`..`THR-066` en `B2.4.8` en lugar de declararlas cubiertas por analogía. `CLS-DAT`/S se mantiene abierta de forma explícita.

**Hallazgo interno `B2-F02`:** no se registró ninguna decisión de arquitectura nueva ni ninguna dependencia nueva. Las cuatro amenazas escaladas se apoyan en `ESC-01`, `ESC-04`, `ESC-06` y `F3-ESC-002`, ya existentes. Por eso `DECISIONES_Y_ESCALAMIENTOS.md` recibe únicamente el registro de avance de B2, sin crear `F3-DEC-*` ni `D2-DEP-*` adicionales.

#### B2.8 Salida de B2 y continuidad hacia B3

Esta sección es autosuficiente: permite continuar sin la conversación que originó el bloque.

**Qué quedó completado en B2**

- Escala cualitativa explícita de probabilidad (`P1`..`P4`) e impacto (`I1`..`I4`), matriz de riesgo y regla de residual proyectado (`B2.1`). La escala prioriza; no representa aceptación del CLIENTE.
- Método de numeración y forma de lectura de las tablas (`B2.2`).
- 66 amenazas `THR-001`..`THR-066`, cada una con los trece campos exigidos.
- Fronteras prioritarias desarrolladas: `TB-04` nube ↔ terminal y `EDGE-RUN`; `TB-06` plataforma nueva ↔ TOS 2012; `TB-05` zona operacional ↔ periferia de terreno.
- Cobertura inicial de las siete clases `CLS-CAN`, `CLS-GWY`, `CLS-SVC`, `CLS-BRK`, `CLS-DAT`, `CLS-EDG` y `CLS-EXT`, con la matriz de cobertura en `B2.5`.
- Distribución de riesgo y regla de no aceptación (`B2.6`); auditoría del bloque con dos hallazgos internos (`B2.7`).

**Qué queda cubierto y qué no**

- Cubierto: las seis categorías STRIDE en las siete clases, salvo `CLS-DAT`/S, que queda **marcada como abierta** y debe resolverse en B6 con componentes reales. *(Cifra de corte de B2. `B6` cerró esa casilla con `THR-072`; ver `B6.2` y `B7.3`.)*
- Cubierto parcialmente: los nueve recorridos críticos de `B1.5` están representados por amenazas, pero **sin la secuencia operacional completa**. Ese es el trabajo de B3.
- No cubierto por diseño: SPOF (B4), revisión de ADR (B5), sustitución de clases por IDs reales (B6), auditoría de cobertura total (B7) y diagrama de fronteras (B8).

**Qué sigue dependiendo de otros frentes**

- `D2-DEP-001` — A1: catálogo lógico, criticidad y responsables. Sin él no puede afirmarse cobertura por componente ni propietario de activo.
- `D2-DEP-002` — A2/A3: interfaces, contratos, autoridad TOS y degradación real. Afecta a `THR-009`..`THR-016`, `THR-030`..`THR-032`, `THR-040`..`THR-044` y `THR-056`..`THR-059`.
- `D2-DEP-003` — C1–C4: nodos, red, sala, productos, HA/DR y capacidad. Afecta a `THR-005`, `THR-006`, `THR-019`, `THR-049`, `THR-052` y `THR-054`.
- `D2-DEP-004` — D1/Subdocumento 5: catálogo campo→sensibilidad→retención→custodia. Afecta a toda amenaza de divulgación y de retención.
- `D2-DEP-005` — CLIENTE/terceros: contratos, SLA, directorio, site survey y aceptadores. Sin él, ninguna probabilidad puede apoyarse en historia y ningún residual puede aceptarse.
- Escalamientos vigentes que B3 no debe cerrar por su cuenta: `ESC-01`, `ESC-04`, `ESC-06`, `ESC-10`, `ESC-14` del Maestro y `F3-ESC-001`/`F3-ESC-002` del Frente 3.

**Qué estados cambiaron y por qué**

| Elemento | Antes | Después | Motivo |
|---|---|---|---|
| Bloque B2 | PENDIENTE | BORRADOR REDACTADO, no aprobado | existe contenido verificable con amenazas, controles y evidencia prevista |
| `RT-11.02` | PENDIENTE | EN CURSO | ya existe metodología declarada y amenazas por clase e integración; **falta** la cobertura por componente real y la evidencia de actualización ante cambios, que llegan con B6/B7 y con A1/A2/C1/C3 |
| `TRZ-D2-002` | PENDIENTE | EN CURSO | la traza de STRIDE deja de ser solo inventario y método |
| `TRZ-D2-013` | PENDIENTE | sin cambio | la revisión de ADR es trabajo de B5; B2 no aprueba ninguno |
| Riesgos y SPOF | ninguno aceptado | ninguno aceptado | B2 no acepta riesgo; B4 consolida SPOF y B8 el resumen residual |

**Siguiente bloque: B3 — Escenarios portuarios.** No corresponde iniciarlo automáticamente.

**Dónde debe comenzar exactamente el próximo agente**

En `B3.1`, tomando como entrada los nueve recorridos críticos de `B1.5` y las 66 amenazas de B2. B3 **reutiliza `THR-*`, no los renumera ni los duplica**: agrega la secuencia operacional del escenario, el punto exacto donde la amenaza se materializa, el efecto sobre el umbral del caso y la degradación declarada. El orden sugerido, por consecuencia operacional, es: 1) operación local 72 h y reconexión ≤90 min; 2) reefer → alarma → escalamiento; 3) OCR/barrera/camión → hecho de gate; 4) movimiento/posición → TOS; 5) hecho facturable → ERP; 6) naviera → mensajería de nave; 7) solicitud externa → gate; 8) cambio de software/configuración → producción y edge; 9) administración/SOC → componente o dato sensible.

Si durante B3 aparece una amenaza nueva, se numera desde `THR-067` y se agrega a la clase correspondiente en `B2.5`, sin reabrir la numeración usada.

**Qué archivos debe leer antes de editar**

1. `Celula3/README.md`.
2. `Celula3/00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md`, §§6–19.
3. `Celula3/00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`, reglas comunes y Frente 3.
4. `Celula3/03_Frente_Seguridad_Consolidacion/00_INDICE_DEL_FRENTE.md`.
5. Este archivo, `D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md`, con `B1` y `B2` completos.
6. `Celula3/03_Frente_Seguridad_Consolidacion/trazabilidad/TRZ_D2.md`.
7. `Celula3/03_Frente_Seguridad_Consolidacion/trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`.
8. `D1_ARQUITECTURA_DE_SEGURIDAD.md` y `trazabilidad/TRZ_D1.md`, para reutilizar correctamente los controles `SEC-*`.

**Qué debe conservar**

- Los identificadores `AST-001..016`, `TB-01..14`, `CLS-*` y `THR-001..066` sin renumerar.
- Las dependencias `D2-DEP-001..005` visibles y abiertas.
- La escala de `B2.1` sin cambiar sus umbrales; si se ajusta, debe revalorarse toda amenaza afectada y dejarlo registrado.
- La regla de no aceptación: nada pasa a `ACEPTADO` sin aprobador, fundamento, evidencia y condición de revisión.
- La distinción entre diseño propuesto, evidencia futura y evidencia ejecutada.
- Las prohibiciones vigentes: no inventar APIs, protocolos, productos, topología, historial de incidentes, cantidades, precios ni decisiones del CLIENTE; no aprobar ADR ni cerrar SPOF fuera de B4/B5; no producir el diagrama antes de B8; no modificar `90_Consolidado/` ni el T-11; no hacer commit ni push sin autorización explícita.

### B3. Escenarios portuarios — borrador inicial

**Estado del bloque: BORRADOR REDACTADO; propuesta no aprobada.** B3 no vuelve a modelar amenazas: toma las 66 de B2 y las sitúa en la secuencia real de trabajo del terminal, para mostrar **en qué paso concreto se materializan**, qué umbral del caso rompen y qué degradación queda declarada. Ninguna prueba está ejecutada, ningún SPOF se cierra y ningún riesgo se acepta.

#### B3.1 Alcance, cobertura exigida y método

**Revisión del plan antes de empezar.** El contrato de D2 y el Plan de entregables exigen cubrir **TOS, gate/OCR, reefer, app offline, VMS, radio, ERP/autoridades y sincronización**. Los nueve recorridos críticos de `B1.5` no representan tres de esas materias como recorrido propio: **app offline, VMS y radio**. Aparecen dentro de otros recorridos, pero disueltas, y eso impediría demostrar cobertura.

**Hallazgo de planificación `B3-F01`:** se conservan los nueve recorridos de `B1.5` como escenarios `SCN-01`..`SCN-09`, en el orden de consecuencia operacional fijado en `B2.8`, y se agregan tres escenarios `SCN-10`..`SCN-12` para las materias exigidas por contrato que no tenían recorrido propio. La numeración `SCN-*` es nueva y no colisiona con los escalamientos `ESC-*` del Maestro.

| Materia exigida por el contrato | Escenario que la cubre |
|---|---|
| sincronización | `SCN-01` |
| reefer | `SCN-02` |
| gate/OCR | `SCN-03`, con la parte externa en `SCN-07` |
| TOS | `SCN-04` |
| ERP | `SCN-05` |
| terceros / navieras | `SCN-06` |
| autoridades y ferrocarril | `SCN-07` |
| app offline | `SCN-10` |
| radio | `SCN-11` |
| VMS | `SCN-12` |
| cambio de software y configuración | `SCN-08` (no exigido nominalmente; se conserva por `RT-11.23/24` y Maestro §12) |
| administración y SOC | `SCN-09` (no exigido nominalmente; se conserva por Maestro §11.3) |

**Método**

1. Cada escenario presenta una **secuencia por pasos**. Cada paso declara frontera, activo, el resultado que no debe perderse, las amenazas de B2 que se materializan allí y el umbral o criterio del caso que queda en juego.
2. **B3 reutiliza `THR-001..066`; no los renumera ni los duplica.** Una misma amenaza aparece en varios escenarios cuando la secuencia la atraviesa: eso es cobertura, no repetición.
3. Cuando el escenario revela una amenaza que B2 no tenía, se numera **desde `THR-067`** y se registra en `B3.14`, con la clase y la categoría STRIDE que le corresponden, para que `B2.5` quede completa.
4. Cada escenario cierra con tres apartados fijos: **degradación declarada** —incluidas las funciones que no estarán disponibles y su reemplazo manual, exigencia del Maestro §9.1—, **evidencia esperada** y **pendiente de otros frentes**.
5. Los **candidatos a punto único de falla** se marcan como `SPOF-CAND` dentro del escenario. B3 no los evalúa ni los acepta: es material de entrada para B4.
6. No se inventan APIs, protocolos, puertos, productos, topología, historial de incidentes, cantidades, precios ni decisiones del CLIENTE. Las cifras citadas son umbrales del Caso 06 y del Maestro, no mediciones.
7. La secuencia describe **el trabajo del terminal**, no una implementación. Dónde ocurre cada paso —qué nodo, qué interfaz, qué producto— lo cierran A1/A2/A3 y C1–C4; por eso ningún paso nombra un componente que el Maestro no haya declarado.

#### B3.2 `SCN-01` — Operación local 72 h y reconexión ≤90 min

Pérdida del enlace exterior con el terminal operando. Las cinco funciones críticas —atención de nave y movimientos, posición e inventario con cruce de zonas, gate y tiempos, monitoreo y alarma reefer, hechos y evidencia facturable— deben sostenerse localmente sin pérdida, y la vuelta debe ser automática, auditable y determinista. Fuente: Maestro §9 y `RNF-DIS-02/03/04`.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-04 | AST-013 | detección de la pérdida de enlace y paso a modo local sin decisión manual ni interrupción de la operación en curso | `THR-006` en su origen | continuidad de las cinco funciones críticas |
| 2 | TB-04, TB-05 | AST-002/003/004/005/013 | las cinco funciones siguen operando con autoridad local declarada; las funciones no sostenibles quedan explícitas y con reemplazo manual | `THR-005`, `THR-064` | 72 h sin pérdida |
| 3 | TB-04, TB-11 | AST-013 | el buffer acumula sin descartar en silencio; la ocupación es visible antes del límite | `THR-005` | peak coincidente de dos naves y gate saturado |
| 4 | TB-04 | AST-006/008 | toda acción local queda atribuida a una persona y registrada de forma íntegra | `THR-003`, `THR-004`, `THR-052` | trazabilidad y registro sin puntos ciegos |
| 5 | TB-04 | AST-001/014 | al reconectar, ambos extremos se autentican mutuamente antes de intercambiar estado | `THR-001` | ninguna escritura desde un extremo no verificado |
| 6 | TB-04, TB-11 | AST-002/005/014 | el lote se aplica íntegro, ordenado y sin duplicar; los conflictos se resuelven de forma determinista | `THR-002`, `THR-008`, `THR-012` | sincronización automática ≤90 min |
| 7 | TB-04, TB-06, TB-07 | AST-001/005/007 | la reconciliación con TOS y ERP no genera doble movimiento ni doble hecho facturable | `THR-011`, `THR-041`, `THR-059` | conciliación 1:1 y autoridad única por dominio×zona×fase |
| 8 | TB-04 | AST-006/010 | los actos ejecutados fuera de alcance durante el aislamiento se detectan y se convalidan o revierten | `THR-064` | mínimo privilegio efectivo, no solo declarado |

**Degradación declarada.** El Maestro obliga a decir qué **no** estará disponible y con qué procedimiento manual se reemplaza. D2 no puede fijar esa lista: depende de qué funciones A3 declare sostenibles localmente y de qué capacidad demuestren C1–C4. B3 deja el requisito abierto y explícito, no lo rellena.

**Evidencia esperada.** Prueba de aislamiento de 72 h con peak coincidente declarado, midiendo ocupación del buffer, continuidad de las cinco funciones y ausencia de descarte silencioso; prueba de reconexión con medición real del tiempo hasta la reconciliación completa y con conflictos inducidos; prueba de rechazo de un extremo no autenticado; prueba de desviación temporal inducida.

**`SPOF-CAND`.** El propio `EDGE-RUN` y su almacenamiento local; el enlace exterior si no hay caminos y proveedores distintos; la referencia temporal si es única. B4 debe evaluar independencia real, no redundancia declarada.

**Pendiente de otros frentes.** `D2-DEP-002` (A2/A3: qué funciones son sostenibles localmente, autoridad, volumen y regla de conflicto); `D2-DEP-003` (C1–C4: nodos, enlaces, capacidad del buffer y holgura); `D2-DEP-005` (CLIENTE: quién convalida los actos fuera de alcance).

#### B3.3 `SCN-02` — Reefer: telemetría → alarma → escalamiento

La desviación de temperatura debe detectarse y notificarse en minutos, en cualquier turno, y el registro continuo debe servir después como evidencia. Fuente: Maestro §§9/15/18.1, `RN-11`, `RF-REF-04/07` y el criterio de aceptación 11.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-05 | AST-004 | la toma o el tablero reporta; la **ausencia** de dato es una condición alarmable y no un silencio normal | `THR-017`, `THR-019` | alarma ≤5 min |
| 2 | TB-05 | AST-004/012 | la banda y la duración de desviación son las aprobadas y versionadas | `THR-020` | parámetro que no impida alarmar (`RN-11`) |
| 3 | TB-05, TB-11 | AST-004/013 | la medición llega y persiste aunque el enlace exterior esté caído | `THR-019`, `THR-005` | continuidad local del monitoreo |
| 4 | TB-11 | AST-004 | la serie se conserva íntegra como evidencia por el plazo declarado | `THR-046` | registro continuo de temperatura |
| 5 | TB-11, TB-03 | AST-004/006 | la alarma se emite, escala y llega a un destinatario identificado que confirma recepción | `THR-039` | canal redundante con escalamiento y confirmación identificada |
| 6 | TB-05 | AST-004/012 | la acción correctiva en terreno queda registrada y asociada a la alarma | `THR-021` | trazabilidad de la respuesta |

**Degradación declarada.** Si el canal primario de notificación no confirma recepción, el escalamiento por el canal alternativo es obligatorio y el evento se registra como incidente operacional aunque la temperatura vuelva a la banda. La ausencia de confirmación no equivale a alarma atendida.

**Evidencia esperada.** Prueba extremo a extremo con patio cargado midiendo dato→alarma→confirmación dentro de los 5 min; prueba con silencio de sensor inducido; prueba de rechazo de un parámetro que haga imposible alarmar; prueba de restauración dirigida de un período de la serie.

**`SPOF-CAND`.** El medio de radio del patio si todas las tomas dependen de él sin failover real; el servicio de notificación si es único; el nodo local si concentra la función de alarma.

**Pendiente de otros frentes.** `D2-DEP-001` (A1: propietario de la alarma y responsables); `D2-DEP-003`/`ESC-10` (C1–C4 y site survey: cobertura, radioenlace y capacidad); `D2-DEP-005` (CLIENTE: banda, duración y destinatarios del escalamiento). Las cantidades de tomas y tableros las fija Célula 2; D2 no las repite como compromiso propio.

#### B3.4 `SCN-03` — Gate: OCR, barrera y camión → hecho de gate

El camión debe entrar, ser reconocido, operar y salir dentro del umbral, dejando un hecho que no puede reconstruirse después. Fuente: Maestro §§6.1/9, `MC-10/16`, criterios de aceptación 1–4.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-05 | AST-003 | la lectura del contenedor proviene de un equipo inventariado e identificable | `THR-017`, `THR-065` | reconocimiento automático en gate; OCR ≤3 s |
| 2 | TB-05 | AST-003/005 | la lectura no se repite ni se altera; una imagen no genera dos hechos | `THR-018` | cero diferencias no explicadas al cierre diario |
| 3 | TB-05, TB-11 | AST-003/013 | el hecho se registra localmente aunque el enlace exterior esté caído | `THR-005` | gate operativo durante 72 h |
| 4 | TB-11 | AST-003/006 | el hecho queda vinculado a identidad, momento y evidencia | `THR-029`, `THR-063` | no repudio del hecho de gate |
| 5 | TB-11, TB-06 | AST-002/003 | la posición y el movimiento resultantes se propagan sin duplicar y con autoridad única | `THR-012`, `THR-011` | posición posterior ≤30 s |
| 6 | TB-05 | AST-003/012 | la barrera solo actúa por una orden prevista y registrada | `THR-021` | ninguna operación remota fuera de catálogo |
| 7 | TB-11 | AST-003 | el tiempo de estadía se mide y se conserva como indicador | `THR-047` | camión completo ≤120 s; estadía hacia 45 min |

**Degradación declarada.** El carril de excepción existe y es más lento que el validado; su uso debe quedar registrado y medido, no naturalizado. Si el reconocimiento automático falla, la entrada por excepción no puede convertirse en la vía habitual sin que el indicador lo muestre.

**Evidencia esperada.** Prueba con lectura repetida que no duplica el hecho; prueba de rechazo de un emisor desconocido; prueba de cierre diario con cero diferencias no explicadas; prueba de gate operando durante el aislamiento; prueba de rechazo de un comando de barrera fuera de catálogo.

**`SPOF-CAND`.** El equipo de lectura por carril; el nodo local que sostiene el gate; la barrera y su control, que no se reemplazan y quedan como dependencia externa.

**Pendiente de otros frentes.** `D2-DEP-002` (A2/A3: levantamiento de barreras, lectura óptica y autoridad offline); `D2-DEP-003` (C1–C4: equipamiento, carriles y capacidad); `ESC-06` (contratos de periféricos).

#### B3.5 `SCN-04` — Movimiento y posición → TOS 2012

Durante la convivencia, cada movimiento debe tener una sola fuente de verdad según `dominio × zona × fase`, y el traspaso al cruzar zona debe ser transaccional. Fuente: Maestro §8, `MC-07/08/13/14`, Decisión 1.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-05, TB-11 | AST-002 | el movimiento se origina en una fuente identificable y se verifica de forma cruzada | `THR-017`, `THR-044` | posición conocida correcta; confirmación ≤1 s |
| 2 | TB-06 | AST-001 | está declarado qué sistema tiene autoridad sobre ese dominio, zona y fase | `THR-011`, `THR-016` | autoridad única |
| 3 | TB-06 | AST-002/007 | la traducción legado↔nuevo no altera contenedor, zona ni posición | `THR-009`, `THR-010` | integridad del movimiento |
| 4 | TB-06 | AST-002/007 | el reintento no produce un segundo movimiento | `THR-012` | idempotencia y deduplicación |
| 5 | TB-06 | AST-001/002 | el traspaso de autoridad al cruzar zona es transaccional, no parcial | `THR-011` | traspaso sin estado intermedio ambiguo |
| 6 | TB-06 | AST-002/003 | la conciliación por turno detecta temprano, no solo al cierre | `THR-013` | ventanas de investigación 48 h y 24 h |
| 7 | TB-06, TB-10 | AST-006/009 | la credencial técnica no permite operar fuera del contrato de coexistencia | `THR-015` | mínimo privilegio sobre el legado |
| 8 | TB-06 | AST-001 | el retorno se ejecuta con doble control y el break-glass queda auditado | `THR-016` | detección→operación restituida ≤30 min en marcha blanca crítica |

**Degradación declarada.** Si la lectura, la escritura o la conciliación con el TOS no resultan suficientemente confiables antes del hito H2/mes 4, la puerta de viabilidad del Maestro §8 obliga a replantear hacia reemplazo integral controlado. B3 no anticipa ese resultado: lo deja como condición vigente.

**Evidencia esperada.** Pruebas con contrato, stub o versión acordada —nunca modificando arbitrariamente el esquema del TOS—: rechazo de cliente no autorizado, mensaje alterado, reenvío masivo sin duplicar, escritura parcial detectada, traspaso de autoridad y ejercicio de retorno con expediente completo de los ocho campos.

**`SPOF-CAND`.** El propio TOS 2012 y su ventana de soporte; la capa anticorrupción si es única; la credencial técnica de integración.

**Pendiente de otros frentes.** `D2-DEP-002` (A2/A3: contrato, campos, matriz de autoridad y regla de conciliación); `ESC-04` (fin de soporte del TOS); `ESC-06` (contrato real); `D2-DEP-005` (CLIENTE: quién autoriza el break-glass).

#### B3.6 `SCN-05` — Hecho facturable → evidencia → ERP

El evento es la evidencia facturable y el ERP emite el documento tributario. La relación debe ser 1:1, sostenible ante objeción y no reconstruible después del hecho. Fuente: Maestro §§7/9/16, Decisión 11, regla negativa 16.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-05, TB-11 | AST-005 | el hecho se captura en el momento en que ocurre, con su evidencia asociada | `THR-018`, `THR-005` | hecho no reconstruible después |
| 2 | TB-03, TB-11 | AST-005/006 | el acto que requiere firma queda vinculado a identidad, momento y evidencia | `THR-029` | no repudio de los cuatro actos |
| 3 | TB-11 | AST-005/008 | la evidencia se conserva íntegra y verificable durante el plazo declarado | `THR-046`, `THR-047` | evidencia suficiente ante objeción |
| 4 | TB-11 | AST-005/007 | la entrega al ERP es idempotente; un reenvío no crea un segundo hecho | `THR-041` | conciliación 1:1 |
| 5 | TB-07 | AST-005 | el ERP no repudia ni duplica; la objeción tiene expediente | `THR-059` | objeción resoluble y reenvío sin duplicidad |
| 6 | TB-07 | AST-010 | el contrato entrega solo los campos necesarios | `THR-060` | minimización por finalidad |
| 7 | TB-04, TB-07 | AST-005/014 | tras un aislamiento, la conciliación no genera duplicados ni omisiones | `THR-002`, `THR-041` | sincronización determinista |

**Degradación declarada.** El ERP no se reemplaza. Si está indisponible, el hecho y su evidencia se acumulan localmente con orden preservado y se entregan al restablecer; lo que no puede ocurrir es capturar el hecho más tarde o reconstruirlo.

**Evidencia esperada.** Prueba de reenvío masivo desde la cola de fallidos sin duplicar hechos; conciliación con diferencia esperada cero; verificación de integridad de la evidencia; prueba de sostenimiento del hecho ante una objeción; inventario campo→destinatario→finalidad del contrato con el ERP.

**`SPOF-CAND`.** El servicio de evidencia y firma si es único; el material de firma; el enlace con el ERP sin fallback declarado.

**Pendiente de otros frentes.** `D2-DEP-002` (A2: contrato del ERP, campos, regla de objeción y conciliación); `D2-DEP-004` (Subdocumento 5: retención y sensibilidad por campo); `ESC-06`.

#### B3.7 `SCN-06` — Naviera → mensajería de nave → confirmación

Mensajería estándar internacional por naviera, con versión propia, sin puente ni redigitación para las líneas de la alianza al hito 2029. Fuente: Maestro §§7/14, Decisión 18, `MC-20/23/24/25`.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-01, TB-08 | AST-016 | el emisor es una contraparte inventariada y verificable, no un atributo autodeclarado | `THR-056`, `THR-065` | autenticidad del intercambio |
| 2 | TB-08 | AST-007/016 | la versión acordada con esa línea se respeta; una versión no soportada se rechaza con motivo | `THR-031`, `THR-057` | versión por naviera |
| 3 | TB-08, TB-11 | AST-016 | el mensaje no se altera ni se aplica dos veces | `THR-057`, `THR-041` | integridad y deduplicación |
| 4 | TB-11 | AST-016/007 | el plan u orden resultante entra a la operación con trazabilidad de origen | `THR-044` | ningún evento sin origen correlacionable |
| 5 | TB-08 | AST-016 | la confirmación de ventana se emite y queda registrada | `THR-058` | ≥72 h de anticipación; cumplimiento general >90 % |
| 6 | TB-08 | AST-016 | la contingencia preserva la traza y no se convierte en redigitación rutinaria | `THR-057` | cero redigitación y sin puente para la alianza |
| 7 | TB-11 | AST-007 | un tercero lento no bloquea a los demás | `THR-040` | aislamiento entre familias de integración |

**Degradación declarada.** Ante indisponibilidad de una contraparte, la cola durable retiene y reintenta con orden preservado. El uso del procedimiento de contingencia debe medirse: es un indicador de riesgo del programa 2029, no una solución permanente.

**Evidencia esperada.** Pruebas extremo a extremo por contraparte y por versión, incluida la de rechazo de un emisor falso y de una versión no soportada; medición del uso de contingencia; prueba con un consumidor detenido sin afectar a las demás familias.

**`SPOF-CAND`.** El bus de integración si es único; el conector por familia; la disponibilidad de cada contraparte, que es externa.

**Pendiente de otros frentes.** `D2-DEP-002` (A2: contratos, versiones e iniciadores por naviera); `ESC-01` (fecha y líneas de la alianza, `PENDIENTE CLIENTE`); `ESC-06`.

#### B3.8 `SCN-07` — Solicitud externa de cita y documentación → salida a ruta

Autoservicio sin teléfono ni mostrador, con documentación validada antes de que el camión salga a ruta, y con autoridades y ferrocarril como contrapartes que pueden no tener interfaz. Fuente: Maestro §§6.1/7, criterios de aceptación 2, 3 y 15, `ESC-14`.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-01, TB-03 | AST-006/010 | quien solicita es quien dice ser y representa a la empresa que declara | `THR-024` | autoservicio confiable |
| 2 | TB-01 | AST-003 | el portal responde durante el peak de gate y resiste tráfico automatizado | `THR-028`, `THR-032` | portal ≤60 s; ninguna fila hacia vía pública |
| 3 | TB-02 | AST-002/003 | la solicitud se valida en el servicio, no solo en el cliente, y respeta rol, zona y fase | `THR-027`, `THR-030` | autorización efectiva |
| 4 | TB-02, TB-11 | AST-003 | recibir una solicitud no equivale a confirmarla: la confirmación depende de la autoridad y de la frescura del dato | `THR-063`, `THR-067` | ninguna confirmación sobre estado obsoleto |
| 5 | TB-08 | AST-003/007 | el trámite ante autoridad o ferrocarril avanza, y si no hay interfaz existe canal asistido registrado | `THR-058` | documentación validada antes de salir a ruta |
| 6 | TB-01, TB-02 | AST-010 | las respuestas no revelan estructura interna ni datos de contenido o ruta | `THR-033`, `THR-066` | protección del dato sensible en el portal |
| 7 | TB-11 | AST-003 | la cita y la prioridad se reflejan en la cola virtual sin depender de una persona | `THR-036` | atención con cita ≥30 % más rápida |

**Degradación declarada.** Con el terminal aislado, el portal en nube puede seguir recibiendo solicitudes, pero **recibir no es confirmar**: la confirmación que depende del estado del terminal queda pendiente y debe mostrarse como tal. Esta distinción está propuesta en D1 B2.1 y sigue por validar con A2/A3/C3.

**Evidencia esperada.** Prueba de carga a 1,5× el peak declarado con el portal dentro de umbral; prueba de suplantación y de revocación; prueba de acceso a objeto ajeno denegado; prueba del canal asistido con expediente trazable; verificación en pentest de que las respuestas no filtran estructura ni dato sensible.

**`SPOF-CAND`.** El borde público como única exposición; el servicio de identidad; la contraparte de autoridad sin interfaz ni fallback acordado.

**Pendiente de otros frentes.** `D2-DEP-001` (A1: roles y representación de empresa); `D2-DEP-002` (A2/A3: autoridad y frescura durante el aislamiento); `D2-DEP-003` (C3/C4: capacidad del borde); `ESC-14` (plazo e interfaz de cada autoridad); `F3-ESC-001` (directorio y federación).

#### B3.9 `SCN-08` — Cambio de software o configuración → producción y edge

Toda intervención necesita retorno, y el artefacto que llega a producción debe ser el mismo que se probó. Fuente: Maestro §§11.3/12, `RT-11.22..27`, `F3-DEC-004`, y las restricciones de calendario del §13.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-12 | AST-011 | la dependencia y el artefacto provienen de fuentes aprobadas y quedan inventariados | `THR-023` | SBOM, firma y procedencia |
| 2 | TB-12, TB-13 | AST-009/011 | ningún secreto viaja en el artefacto ni en la configuración | `THR-048` | cero secretos embebidos |
| 3 | TB-13 | AST-010 | los ambientes no productivos no usan datos reales sin anonimización verificable | `THR-050` | separación de ambientes |
| 4 | TB-13 | AST-011/012 | se promueve el mismo artefacto probado, no una recompilación | `THR-007` | construcción única y promoción |
| 5 | TB-04, TB-05 | AST-012/013 | el despliegue en el nodo local verifica firma y procedencia antes de ejecutar | `THR-007`, `THR-023`, `THR-053` | integridad del runtime local |
| 6 | TB-13, TB-10 | AST-006 | el acceso a producción es excepcional, aprobado y grabado | `THR-062`, `THR-034` | acceso excepcional por PAM |
| 7 | TB-04, TB-05 | AST-012 | la intervención registra los ocho campos y su retorno está probado | `THR-053` | retorno de toda intervención |
| 8 | TB-05 | AST-013/015 | la ventana respeta congelamiento, nave y las cuatro horas previas | `THR-054` | 15-dic a 30-abr; invasivas listas al 14-dic-2027 |

**Degradación declarada.** Si una etapa obligatoria falla o aparece un hallazgo crítico, la promoción se bloquea. Un bloqueo no se resuelve ampliando la ventana ni interviniendo durante el congelamiento; se reprograma.

**Evidencia esperada.** Verificación de firma y procedencia en el despliegue; comparación entre configuración efectiva y declarada en el nodo local; expediente de intervención con los ocho campos y prueba de retorno ejecutada en preproducción; registro de sesión grabada con su aprobación.

**`SPOF-CAND`.** El registro de artefactos y la cadena de firma; el nodo local si el despliegue no es reversible sin presencia física en terreno.

**Pendiente de otros frentes.** `D2-DEP-003` (C3/C4: pipeline, ambientes, herramientas y responsables); `D2-DEP-004` (Subdocumento 5: técnicas de anonimización); `D2-DEP-005` (CLIENTE: aprobadores y custodia de excepciones).

#### B3.10 `SCN-09` — Administración, soporte y SOC → componente o dato sensible

El privilegio elevado y la organización de soporte, posiblemente externa, son una frontera propia. Fuente: Maestro §§11.2/11.3, `RT-11.17/11.27`.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-10 | AST-006 | el acceso administrativo exige segundo factor y no existe vía permanente | `THR-034`, `THR-062` | MFA para administradores y externos |
| 2 | TB-10 | AST-006/009 | la elevación es temporal, aprobada por sesión y grabada | `THR-062`, `THR-007` | PAM con elevación temporal |
| 3 | TB-10, TB-11 | AST-008/010 | el soporte no consulta el almacén directamente | `THR-043`, `THR-045` | acceso por el servicio propietario |
| 4 | TB-10, TB-11 | AST-008 | la actividad privilegiada queda registrada de forma inalterable y correlacionada | `THR-047`, `THR-038` | registro 12 meses en línea + 24 en archivo |
| 5 | TB-10, TB-14 | AST-009 | quien opera el respaldo no es quien custodia sus claves | `THR-048`, `THR-049` | separación de funciones; 3-2-1-1-0 |
| 6 | TB-10 | AST-006 | la baja o el cambio de rol se refleja efectivamente, también en terreno aislado | `THR-025` | baja efectiva ≤24 h |
| 7 | TB-10 | AST-008 | el SOC detecta y escala dentro de los plazos comprometidos | `THR-038` | incidente crítico ≤2 h; brecha ≤24 h; causa raíz ≤5 días hábiles |

**Degradación declarada.** El SOC con cobertura 24x7 es obligación directa de las Bases y debe ser operable con la dotación declarada; cuando requiera especialistas no disponibles, se refleja como servicio. D2 no presume un segundo SOC en la sala del terminal.

**Evidencia esperada.** Registro de sesión grabada con aprobación asociada; revisión periódica de accesos vigentes de terceros; prueba de inmutabilidad del registro y de recuperación desde archivo; prueba de revocación durante aislamiento; ejercicio de respuesta a incidente con medición de los plazos.

**`SPOF-CAND`.** El bastión de administración; el proveedor de SOC; el servicio de identidad si su caída impide también la operación de emergencia.

**Pendiente de otros frentes.** `D2-DEP-003` (C3: bastión, plataforma y ubicación); `D2-DEP-005` (CLIENTE: RACI, proveedor, contactos y suplencias); `F3-ESC-002` (revocación frente a terminal aislada).

#### B3.11 `SCN-10` — App instalable en operación desconectada

Aplicación única con cuatro perfiles y operación offline cifrada para perfiles internos, usada en terreno con guantes e intemperie, por tres turnos y con personal eventual. No se sustituye por web responsiva. Fuente: Maestro §§6.1/11.2, `MC-01/04/18`, reglas negativas 1 y 2.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-03, TB-05 | AST-006 | el usuario se identifica individualmente aunque el dispositivo o la terminal sean compartidos | `THR-025` | identidad individual en terreno |
| 2 | TB-01, TB-04 | AST-010/013 | el material que queda en el dispositivo es el mínimo y está cifrado | `THR-026`, `THR-004` | cifrado de datos personales, comerciales y de ruta |
| 3 | TB-04 | AST-002/003 | el usuario distingue lo confirmado de lo pendiente y no opera sobre un dato vencido creyéndolo vigente | `THR-067` | posición conocida correcta vs. por verificar |
| 4 | TB-04 | AST-002/006 | las funciones disponibles offline son las declaradas, con su alcance por rol | `THR-064`, `THR-027` | mínimo privilegio también sin enlace |
| 5 | TB-04, TB-11 | AST-005/014 | la cola local se sincroniza sin perder ni duplicar, con orden preservado | `THR-002`, `THR-008`, `THR-041` | reconciliación determinista |
| 6 | TB-03 | AST-006 | la credencial temporal expira y puede revocarse; el relevo no detiene la operación | `THR-025` | baja efectiva ≤24 h frente a 8 h sin cobertura |
| 7 | TB-05 | AST-013 | la app sigue siendo utilizable con guantes y a la intemperie, sin apartar la vista de la carga en cabina | — | criterio de aceptación 21 |

**Degradación declarada.** Las funciones no disponibles sin enlace deben estar declaradas en la propia interfaz, junto al procedimiento manual que las reemplaza. Mostrar un dato en caché sin marcarlo como tal es una degradación oculta, no una degradación elegante.

**Evidencia esperada.** Prueba de 72 h con la app operando y actos fuera de alcance detectados al reconectar; prueba de revocación con el dispositivo fuera de línea; verificación de que la cola local no es legible fuera de la app; prueba de relevo de turno sin detención; prueba de usabilidad con guantes e intemperie.

**`SPOF-CAND`.** El dispositivo asignado por turno si no hay reemplazo disponible; el servicio de identidad si su caída impide el relevo.

**Pendiente de otros frentes.** `D2-DEP-001` (A1: perfiles y roles); `D2-DEP-002` (A3: qué funciones quedan disponibles offline y con qué alcance); `D2-DEP-004` (Subdocumento 5: qué puede almacenarse en el dispositivo); `F3-ESC-002` (revocación en aislamiento); `D2-DEP-005` (CLIENTE: nombradas y acreditaciones durante las 72 h).

#### B3.12 `SCN-11` — Red de patio y radioenlace

La red de patio debe funcionar con el patio cargado, estar segregada y tener failover real del radioenlace. La red celular privada es alternativa primaria **sujeta a site survey**, no una decisión cerrada. Fuente: Maestro §§4.6/10.2, Decisión 9, `MC-10`, `ESC-10`, regla negativa 12.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-05 | AST-002/004/013 | la cobertura se sostiene con el patio cargado, que es la condición desfavorable real | `THR-019`, `THR-068` | radiopropagación con patio cargado |
| 2 | TB-05 | AST-013 | el failover del radioenlace es real y demostrable, no declarado | `THR-068` | failover con conmutación efectiva |
| 3 | TB-05 | AST-002/003/004 | la pérdida del medio no cae simultáneamente sobre posición, gate, reefer y cabina sin degradación declarada | `THR-068`, `THR-019` | continuidad de las funciones críticas |
| 4 | TB-05 | AST-013 | el alcance de la señal fuera del recinto no se convierte en superficie de acceso | `THR-069`, `THR-017` | segregación de redes |
| 5 | TB-05 | AST-002/012 | cada equipo de terreno tiene identidad propia; no se usa un identificador único para todos | `THR-017`, `THR-069` | regla negativa 12 del Maestro |
| 6 | TB-05, TB-11 | AST-002/013 | los terminales de patio soportan hasta 8 h fuera de cobertura sin pérdida | `THR-005`, `THR-064` | 8 h de aislamiento de terminal |

**Degradación declarada.** La cantidad y la ubicación de los puntos de radio dependen del site survey y deben expresarse como rango, nunca como un plano ficticio. D2 no fija cantidades ni tecnología: registra que la falta de site survey mantiene abierta la viabilidad del escenario.

**Evidencia esperada.** Prueba de cobertura con patio cargado; prueba de conmutación real del radioenlace midiendo el efecto sobre las funciones críticas; prueba de 8 h fuera de cobertura sin pérdida; verificación de identidad por dispositivo y de que la señal fuera del recinto no otorga acceso.

**`SPOF-CAND`.** El medio de radio compartido por posición, gate, reefer y cabina; el punto de agregación de la red de patio; el proveedor único de enlace si no hay caminos distintos.

**Pendiente de otros frentes.** `D2-DEP-003` (C1/C3/C4: diseño de red, cantidad, ubicación, failover y capacidad); `ESC-10` (site survey del patio); `ESC-06` (contrato de radio); Decisión 9 sigue condicionada.

#### B3.13 `SCN-12` — VMS, CCTV y red de protección ISPS

El VMS existente se conserva y sigue siendo la interfaz de video. La segregación IEC 62443 fue aprobada sin degradar protección, y la continuidad del VMS durante la migración de red es una condición, no un objetivo deseable. Fuente: Maestro §§7/10.2/19, Decisión 19, `MC-02`, reglas negativas 5, 6 y 7.

| Paso | Frontera | Activo | Resultado que no debe perderse | Amenazas que se materializan | Umbral o criterio en juego |
|---:|---|---|---|---|---|
| 1 | TB-09 | AST-015 | el VMS conserva su disponibilidad antes, durante y después de cualquier intervención de red | `THR-061` | continuidad del VMS/ISPS |
| 2 | TB-09 | AST-007/015 | solo circulan eventos, metadatos o evidencia confirmada; no video completo por la red operacional | `THR-022` | reglas negativas 6 y 7 |
| 3 | TB-09, TB-05 | AST-015 | la red de protección no queda alcanzable desde la red operacional | `THR-022`, `THR-069` | segregación IEC 62443 |
| 4 | TB-09, TB-11 | AST-015/005 | cuando se requiere evidencia asociada a un incidente o a una objeción, existe y es verificable | `THR-070`, `THR-047` | evidencia utilizable, no solo almacenada |
| 5 | TB-10 | AST-015 | el mantenimiento del sistema conservado no abre un acceso permanente de proveedor | `THR-062` | acceso de terceros acotado y grabado |
| 6 | TB-05 | AST-015 | la modernización no agrega carga operacional al personal de protección | — | la protección no se degrada por el proyecto |

**Degradación declarada.** Si la continuidad del VMS no puede garantizarse durante una intervención de red, la intervención se revierte con su retorno registrado y se reprograma. No existe la opción de degradar temporalmente la protección para avanzar en el calendario.

**Evidencia esperada.** Prueba de rutas permitidas y denegadas entre la red operacional y la de protección; verificación de disponibilidad del VMS antes, durante y después de la migración, con informe; prueba de recuperación de una evidencia asociada a un incidente; registro de accesos de proveedor con aprobación por sesión.

**`SPOF-CAND`.** El conducto único entre la plataforma y el VMS; el propio VMS conservado, que no se reemplaza y queda como dependencia externa.

**Pendiente de otros frentes.** `D2-DEP-003` (C3: conducto permitido, topología y prueba de continuidad); `D2-DEP-005` (CLIENTE: responsabilidades ISPS y ventanas de intervención); `ESC-06` (contrato del VMS).

#### B3.14 Amenazas nuevas surgidas de los escenarios

Los escenarios revelaron cuatro condiciones que B2 no tenía. Se numeran desde `THR-067`, conservan el formato de B2 y completan `B2.5`.

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-067` | AST-002/003 | `CH-APP`, `CH-CAB`, `CH-PORTAL` / `CLS-CAN` | TB-04 + TB-01 | T | Durante el aislamiento la interfaz presenta datos en caché sin distinguirlos de los vigentes; el operador o el transportista decide sobre un estado vencido creyéndolo actual, y la confirmación resultante contradice al terminal | P3 | I3 | ALTO |
| `THR-068` | AST-002/003/004/013 | red de patio y radioenlace / `CLS-EDG` | TB-05 | D | La degradación o la interferencia del medio de radio compartido afecta a la vez a posición, gate, reefer y cabina, porque todas dependen del mismo transporte y el failover no conmuta de forma efectiva con el patio cargado | P3 | I4 | CRÍTICO |
| `THR-069` | AST-002/006/013 | red de patio / `CLS-EDG`, `CLS-EXT` | TB-05 | S + E | La cobertura de la red de patio excede el recinto y se convierte en superficie de acceso; quien la alcanza intenta asociarse como equipo de terreno o alcanzar la zona operacional | P2 | I4 | ALTO |
| `THR-070` | AST-015/005/008 | VMS conservado y evidencia asociada / `CLS-EXT`, `CLS-DAT` | TB-09 + TB-11 | R | Cuando se requiere la evidencia de video o su metadato para sostener un incidente o una objeción, no está disponible, no es recuperable en plazo o no es verificable; el hecho no puede sostenerse | P2 | I3 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-067` | Marca de frescura y de origen en todo dato mostrado en modo local; bloqueo de las confirmaciones que dependan de estado no vigente; degradación visible en la interfaz | Medición de antigüedad del dato presentado; alerta por confirmación intentada sobre estado vencido | Invalidar la confirmación, recalcular contra el estado vigente y avisar al usuario; **evidencia esperada:** prueba de 72 h con decisiones sobre dato vencido bloqueadas y visibles | ALTO | POR VALIDAR | `D2-DEP-002`: A2/A3 definen qué operaciones dependen del estado del terminal y cuál es la frescura aceptable por operación |
| `THR-068` | Failover real por caminos o medios distintos; segregación de la red de patio; priorización de las funciones críticas sobre el medio compartido; continuidad local mientras el medio se restablece | Medición de calidad del medio con patio cargado; alerta por conmutación fallida y por degradación simultánea de varias funciones | Conmutar, degradar según lo declarado y activar el procedimiento manual; **evidencia esperada:** prueba de conmutación real con patio cargado midiendo el efecto sobre posición, gate, reefer y cabina | CRÍTICO | POR VALIDAR | `ESC-10`/`D2-DEP-003`: sin site survey no puede afirmarse cobertura ni independencia del failover. Es entrada obligatoria de B4 |
| `THR-069` | Identidad por dispositivo y no por alcance de señal; `SEC-NET-01` segregación de la zona operacional; control de asociación y de alcance físico según el diseño de red | `SEC-SIEM-01` alerta por intento de asociación de equipo no inventariado y por actividad desde ubicación no esperada | Bloquear la asociación, aislar y revisar el alcance del diseño; **evidencia esperada:** verificación de que el alcance fuera del recinto no otorga acceso y prueba de rechazo de equipo no inventariado | ALTO | POR VALIDAR | `ESC-10`/`D2-DEP-003`: alcance, tecnología y control de asociación dependen de C1/C3 y del site survey |
| `THR-070` | Retención y disponibilidad de la evidencia asociada acordadas con el responsable del VMS; integridad verificable del metadato transportado; ninguna dependencia del VMS respecto de la plataforma nueva | Verificación periódica de recuperabilidad de una muestra; alerta por evidencia solicitada y no disponible en plazo | Escalar al responsable del sistema conservado y registrar la imposibilidad como brecha de evidencia; **evidencia esperada:** prueba de recuperación de una evidencia asociada a un incidente dentro del plazo acordado | ALTO | POR VALIDAR | `ESC-06`/`D2-DEP-005`: la retención y el acceso a la evidencia del VMS los define su contrato y el CLIENTE, no D2 |

#### B3.15 Cobertura de escenarios y efecto sobre la cobertura STRIDE

**Materias exigidas.** 12/12 escenarios desarrollados; las ocho materias del contrato quedan cubiertas por un escenario propio y no disueltas dentro de otro. La correspondencia está en la tabla de `B3.1`.

**Recorridos críticos de `B1.5`.** 9/9 representados como `SCN-01`..`SCN-09`, con secuencia por pasos, punto de materialización, umbral afectado, degradación declarada y evidencia esperada. `B1.5` deja de ser una lista de recorridos y pasa a ser trazable paso a paso.

**Amenazas.** Las 66 de B2 se conservan sin renumerar. Se agregan `THR-067`..`THR-070`. El total pasa a **70 amenazas `THR-001..070`**.

| Clase | Categorías que suman amenazas nuevas |
|---|---|
| `CLS-CAN` | `T` incorpora `THR-067` |
| `CLS-EDG` | `D` incorpora `THR-068`; `S` y `E` incorporan `THR-069` |
| `CLS-EXT` | `S` y `E` incorporan `THR-069`; `R` incorpora `THR-070` |
| `CLS-DAT` | `R` incorpora `THR-070` |

`CLS-DAT`/S sigue **abierta**: ningún escenario reveló una suplantación propia del almacén distinta de la del productor (`THR-044`) o del acceso directo (`THR-043`). Se mantiene marcada para B6, cuando existan componentes reales. *(Cifra de corte de B3. `B6` la cerró con `THR-072`, que sí es una suplantación propia del almacén o de su réplica; ver `B7.3`.)*

**Distribución de riesgo actualizada**

| Nivel | B2 | B3 | Amenazas críticas |
|---|---:|---:|---|
| CRÍTICO | 5 | **6** | `THR-005`, `THR-011`, `THR-015`, `THR-019`, `THR-062`, `THR-068` |
| ALTO | 58 | 61 | — |
| MEDIO | 3 | 3 | — |
| BAJO | 0 | 0 | — |

Estados: **66 `POR VALIDAR` y 4 `ESCALADO`**. Ninguna amenaza puede cerrarla D2 por sí sola y ninguna queda aceptada.

#### B3.16 Candidatos a punto único de falla entregados a B4

B3 los identifica y **no los evalúa ni los acepta**. B4 debe determinar independencia real, mitigación, prueba, dueño y aceptabilidad. Un candidato con mitigación declarada sigue siendo candidato hasta que la independencia se demuestre.

| Candidato | Escenarios donde aparece | Por qué es candidato | Amenaza asociada |
|---|---|---|---|
| `SPOF-CAND-01` runtime local `EDGE-RUN` y su almacenamiento | `SCN-01`, `SCN-03`, `SCN-10` | concentra las cinco funciones críticas durante 72 h | `THR-005`, `THR-052`, `THR-054` |
| `SPOF-CAND-02` enlace exterior | `SCN-01`, `SCN-05` | si no hay caminos y proveedores distintos, la conmutación no es real | `THR-006` |
| `SPOF-CAND-03` medio de radio del patio | `SCN-02`, `SCN-03`, `SCN-11` | posición, gate, reefer y cabina comparten transporte | `THR-068`, `THR-019` |
| `SPOF-CAND-04` referencia temporal | `SCN-01` | si es única, la reconciliación deja de ser determinista | `THR-008` |
| `SPOF-CAND-05` TOS 2012 y su ventana de soporte | `SCN-04` | sistema conservado, con fin de soporte no confirmado | `THR-013`, `THR-015` |
| `SPOF-CAND-06` capa anticorrupción `INT-TOS` | `SCN-04` | único traductor entre autoridad nueva y legado | `THR-009`, `THR-010` |
| `SPOF-CAND-07` bus de integración `INT-HUB` | `SCN-05`, `SCN-06` | 21 contrapartes y 7 familias sobre un mismo intercambio | `THR-040`, `THR-044` |
| `SPOF-CAND-08` servicio de evidencia y firma | `SCN-05`, `SCN-03` | sostiene los cuatro actos y el hecho facturable | `THR-029`, `THR-046` |
| `SPOF-CAND-09` material criptográfico y su recuperación | `SCN-08`, `SCN-09` | su pérdida es indisponibilidad, su compromiso es suplantación | `THR-048`, `THR-049` |
| `SPOF-CAND-10` servicio de identidad `SRV-IAM` | `SCN-07`, `SCN-09`, `SCN-10` | su caída puede impedir incluso la operación de emergencia | `THR-024`, `THR-025` |
| `SPOF-CAND-11` borde público único | `SCN-07` | es la única exposición por diseño | `THR-028`, `THR-034` |
| `SPOF-CAND-12` registro de artefactos y cadena de firma | `SCN-08` | producción solo consume artefactos aprobados | `THR-023`, `THR-007` |
| `SPOF-CAND-13` bastión de administración y proveedor de SOC | `SCN-09` | privilegio y detección concentrados, posiblemente externos | `THR-062`, `THR-038` |
| `SPOF-CAND-14` VMS conservado y su conducto | `SCN-12` | no se reemplaza; dependencia externa de protección | `THR-061`, `THR-070` |
| `SPOF-CAND-15` contrapartes externas sin fallback acordado | `SCN-06`, `SCN-07` | autoridades, ferrocarril y navieras sin interfaz ni SLA levantados | `THR-058`, `THR-056` |
| `SPOF-CAND-16` equipamiento de gate por carril | `SCN-03` | lectura y barrera por carril, sin reemplazo dentro del alcance | `THR-018`, `THR-021` |

#### B3.17 Auditoría del bloque B3

| Comprobación | Resultado | Estado |
|---|---|---|
| materias exigidas por contrato y Plan | 8/8 con escenario propio: TOS, gate/OCR, reefer, app offline, VMS, radio, ERP/autoridades y sincronización | CONFORME |
| recorridos críticos de `B1.5` | 9/9 desarrollados como `SCN-01`..`SCN-09` en el orden fijado en `B2.8` | CONFORME |
| reutilización de amenazas | `THR-001..066` reutilizadas sin renumerar ni duplicar; solo se agregan `THR-067..070` | CONFORME |
| amenazas nuevas con formato completo | 4/4 con los trece campos de B2 | CONFORME |
| estructura fija por escenario | 12/12 con secuencia por pasos, degradación declarada, evidencia esperada, candidatos a SPOF y pendientes | CONFORME |
| funciones no disponibles durante desconexión | declaradas como requisito en `SCN-01` y `SCN-10`; **la lista concreta no se inventa**, depende de A3 y C1–C4 | ABIERTO POR DEPENDENCIA |
| SPOF | 16 candidatos identificados y entregados a B4; ninguno evaluado ni aceptado | CONFORME |
| riesgos aceptados o ADR aprobados | ninguno; `ADR-008` `EN ANÁLISIS`, `ADR-009`/`ADR-010` `PROPUESTO` | CONFORME |
| evidencia ejecutada | ninguna; todas las pruebas se enuncian como previstas | CONFORME |
| APIs, protocolos, productos, topología, historial, cantidades o precios inventados | no detectados; los umbrales citados provienen del Maestro y del Caso 06 | CONFORME |
| identificadores | `SCN-01..12` sin colisión con `ESC-*`; `SPOF-CAND-01..16` nuevos; `THR`, `AST`, `TB` y `CLS` dentro de rango | CONFORME |
| diagrama | no producido; corresponde a B8 | CONFORME |
| cobertura de `RT-11.02` | se amplía con escenarios por integración real del caso; sigue faltando la cobertura por componente e interfaz reales y la evidencia de actualización ante cambios | PARCIAL — `EN CURSO`, sin cambio de estado |

**Hallazgo `B3-F01`** (registrado en `B3.1`): el contrato exigía app offline, VMS y radio, que no tenían recorrido propio en `B1.5`. Se agregaron `SCN-10`, `SCN-11` y `SCN-12` en lugar de declararlos cubiertos dentro de otros escenarios.

**Hallazgo `B3-F02`:** `SCN-11` reveló que posición, gate, reefer y cabina pueden depender del mismo medio de radio. Eso convierte al medio en candidato a punto único con efecto simultáneo sobre cuatro funciones críticas, y por eso `THR-068` nace en nivel `CRÍTICO`. Es la única amenaza crítica que B2 no había visto, y su resolución depende del site survey (`ESC-10`), no de D2.

**Hallazgo `B3-F03`:** `SCN-01` y `SCN-10` exigen declarar las funciones no disponibles durante la desconexión y su reemplazo manual. D2 **no puede** producir esa lista sin A3 y C1–C4. Queda como requisito explícito y abierto, no como vacío silencioso; la regla negativa 13 del Maestro impide omitirlo.

#### B3.18 Salida de B3 y continuidad hacia B4

**Qué quedó completado en B3**

- 12 escenarios `SCN-01`..`SCN-12`, cada uno con secuencia por pasos, materialización de amenazas, umbral afectado, degradación declarada, evidencia esperada, candidatos a SPOF y pendientes de otros frentes.
- Cobertura de las ocho materias exigidas por el contrato y de los nueve recorridos de `B1.5`.
- Cuatro amenazas nuevas `THR-067`..`THR-070`, con el formato completo de B2; total `THR-001..070`.
- 16 candidatos a punto único de falla `SPOF-CAND-01..16`, identificados y no evaluados.
- Tres hallazgos internos `B3-F01`, `B3-F02` y `B3-F03`.

**Qué estados cambiaron y por qué**

| Elemento | Antes | Después | Motivo |
|---|---|---|---|
| Bloque B3 | PENDIENTE | BORRADOR REDACTADO, no aprobado | existen escenarios verificables con secuencia, materialización y evidencia prevista |
| Amenazas | `THR-001..066` | `THR-001..070` | los escenarios revelaron cuatro condiciones no modeladas |
| Riesgo crítico | 5 | 6 | `THR-068` nace crítico por dependencia simultánea del medio de radio |
| `RT-11.02` | EN CURSO | EN CURSO, sin cambio | B3 amplía cobertura por escenario, no por componente real; el cierre sigue dependiendo de B6/B7 |
| SPOF | ninguno registrado | 16 candidatos entregados a B4 | B3 identifica; B4 evalúa y decide |
| Riesgos aceptados | ninguno | ninguno | sin aprobador, fundamento, evidencia ni condición de revisión |

**Siguiente bloque: B4 — Registro consolidado de SPOF.** No corresponde iniciarlo automáticamente.

**Dónde debe comenzar exactamente el próximo agente**

En `B4.1`, tomando como entrada la tabla `B3.16` con los 16 `SPOF-CAND-*` y las seis amenazas críticas. B4 debe, para cada candidato: determinar si la independencia es real o solo declarada; registrar escenario, impacto, mitigación propuesta, por qué subsiste, prueba que lo demostraría, dueño y condición de revisión. El registro debe cubrir infraestructura, servicio, datos, personas y proceso, y terceros —las cinco familias del contrato—, y ningún candidato puede desaparecer del registro por tener mitigación: la regla negativa 14 del Maestro prohíbe ocultar puntos únicos. `ACEPTADO` exige aprobador nominado, fundamento, plazo o condición de revisión y evidencia; mientras falte, se usa `POR ACEPTAR` o `ESCALADO`.

Si B4 revela una amenaza nueva, se numera desde `THR-071` y se registra con el formato de B2.

**Qué archivos debe leer**

1. `Celula3/README.md`.
2. `Celula3/00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md`, §§6–19, con atención al §9 y a la regla negativa 14.
3. `Celula3/00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`, Frente 3 y sección D2.
4. `Celula3/03_Frente_Seguridad_Consolidacion/00_INDICE_DEL_FRENTE.md`.
5. Este archivo, con `B1`, `B2` y `B3` completos; en particular `B2.1` (escala), `B2.6` (regla de no aceptación) y `B3.16` (candidatos).
6. `trazabilidad/TRZ_D2.md` y `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`.
7. `D1_ARQUITECTURA_DE_SEGURIDAD.md` y `trazabilidad/TRZ_D1.md`, para los controles `SEC-*`.

**Qué debe conservar**

- Los identificadores `AST-001..016`, `TB-01..14`, `CLS-*`, `THR-001..070`, `SCN-01..12` y `SPOF-CAND-01..16`, sin renumerar.
- Las dependencias `D2-DEP-001..005` abiertas y visibles, y los escalamientos `ESC-01/04/06/10/14`, `F3-ESC-001/002`.
- La escala de `B2.1` y la regla de que el residual proyectado no baja mientras la evidencia sea futura.
- La distinción entre diseño propuesto, evidencia futura y evidencia ejecutada.
- Las prohibiciones vigentes: no inventar APIs, protocolos, productos, topología, historial, cantidades, precios ni decisiones del CLIENTE; no aprobar ADR fuera de B5; no producir el diagrama antes de B8; no modificar `90_Consolidado/` ni el T-11; no hacer commit ni push sin autorización explícita.

### B4. Registro consolidado de puntos únicos de falla — borrador inicial

**Estado del bloque: BORRADOR REDACTADO; propuesta no aprobada.** B4 consolida en un registro único los candidatos de `B3.16`. Se escribe en formato de registro, no de análisis extendido: una fila por punto único, para que la integración y la auditoría puedan leerlo sin recorrer los escenarios.

#### B4.1 Método y regla de aceptación

1. Los 16 candidatos `SPOF-CAND-01..16` se confirman como `SPOF-01..21`. B4 agrega cinco que B3 no tenía como entrada propia: sala técnica y energía, y los cuatro de la familia **personas y proceso**, que el contrato exige y que ningún escenario había aislado.
2. Se cubren las cinco familias del contrato: infraestructura, servicio, datos, personas y proceso, y terceros.
3. **Ningún punto desaparece del registro por tener mitigación** (regla negativa 14 del Maestro). La mitigación propuesta no elimina el punto: lo condiciona a una prueba.
4. `ACEPTADO` exige aprobador nominado, fundamento, plazo o condición de revisión y evidencia. Como ninguno los tiene, todos quedan en `POR ACEPTAR` o `ESCALADO`. La columna «Aceptación» indica **qué rol o frente debería aceptarlo**, no una persona: D2 no nombra responsables que el CLIENTE no ha designado.
5. La «Prueba» es la que demostraría independencia real. Todas son previstas; ninguna ejecutada.

#### B4.2 Registro — infraestructura

| SPOF | Vista/componente | Escenario | Impacto | Mitigación propuesta | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| `SPOF-01` | `EDGE-RUN` y su almacenamiento | `SCN-01`, `SCN-03`, `SCN-10` | pérdida de las cinco funciones críticas durante el aislamiento | nodo redundante con almacenamiento tolerante a un disco; cifrado en reposo | la redundancia está declarada, no demostrada; C1–C4 no han definido nodos | C1–C4 + CLIENTE | pérdida de un nodo con continuidad de las cinco funciones | POR ACEPTAR |
| `SPOF-02` | enlace exterior | `SCN-01`, `SCN-05` | sin conmutación real, el aislamiento se prolonga y el buffer se agota | enlaces por caminos y proveedores distintos, conmutación automática | proveedor y trazado no levantados; `THR-006` | C3/C4 + CLIENTE | corte de un camino con conmutación medida | POR ACEPTAR |
| `SPOF-03` | medio de radio del patio | `SCN-02`, `SCN-03`, `SCN-11` | posición, gate, reefer y cabina caen a la vez; impide alarma ≤5 min | failover real por medio o camino distinto; continuidad local mientras se restablece | sin site survey no hay evidencia de independencia; `THR-068` es la amenaza crítica nueva | C1/C3/C4 + levantamiento | conmutación con patio cargado midiendo las cuatro funciones | ESCALADO `F3-ESC-003` / `ESC-10` |
| `SPOF-04` | referencia temporal | `SCN-01` | si es única, la reconciliación deja de ser determinista | fuente de tiempo en ambos dominios y secuencia propia además de marca temporal | mecanismo no definido; `THR-008` | A2/A3 + C3 | reconciliación con desviación temporal inducida | POR ACEPTAR |
| `SPOF-05` | borde público único | `SCN-07` | es la única exposición por diseño; su caída deja sin autoservicio | servicio de borde con HA multi-zona; cola virtual como contención funcional | producto y capacidad no seleccionados; `THR-028`, `THR-034` | C3/C4 | carga a 1,5× peak con el portal dentro de umbral | POR ACEPTAR |
| `SPOF-06` | sala técnica, energía y ambiente | `SCN-08`, `SCN-11` | pérdida del cómputo local durante el congelamiento, cuando no se puede intervenir | UPS y generación según §10.3; protección marina por clase y emplazamiento | `ADR-005` sigue abierto con tres alternativas; `THR-054` | C1/C2/C3 + `ADR-005` | prueba de autonomía eléctrica y de recepción de protección marina | ESCALADO `ESC-07` / `ESC-09` |

#### B4.3 Registro — servicio

| SPOF | Vista/componente | Escenario | Impacto | Mitigación propuesta | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| `SPOF-07` | `INT-TOS`, capa anticorrupción | `SCN-04` | único traductor entre autoridad nueva y legado; su caída detiene la convivencia | instancias redundantes, cola durable y conciliación por turno | contrato y capacidad del TOS sin levantar; `THR-009`, `THR-010` | A2/A3 + CLIENTE | degradación del adaptador con contrato o stub acordado | POR ACEPTAR |
| `SPOF-08` | `INT-HUB`, bus de integración | `SCN-05`, `SCN-06` | 21 contrapartes y 7 familias sobre un mismo intercambio | bulkhead por familia, cuota por consumidor, DLQ | dimensionamiento pendiente; `THR-040`, `THR-044` | A2 + C4 | consumidor detenido sin afectar a las demás familias | POR ACEPTAR |
| `SPOF-09` | `SRV-EVID`, evidencia y firma | `SCN-03`, `SCN-05` | sostiene los cuatro actos y el hecho facturable; sin él no hay no repudio | HA del servicio; material de firma protegido y respaldado | producto y custodia no definidos; `THR-029`, `THR-046` | A2 + C2/C3 + CLIENTE | sostenimiento de un acto ante objeción con el servicio degradado | POR ACEPTAR |
| `SPOF-10` | `SRV-IAM`, identidad | `SCN-07`, `SCN-09`, `SCN-10` | su caída puede impedir incluso la operación de emergencia y el relevo de turno | identidad local para funciones críticas; credencial con vigencia y relevo sin detención | `ADR-008` `PROPUESTO` condicionado; directorio no confirmado | A1 + C2 + CLIENTE | relevo y operación de emergencia con el servicio central caído | ESCALADO `F3-ESC-001` / `F3-ESC-002` |
| `SPOF-11` | registro de artefactos y cadena de firma | `SCN-08` | producción solo consume artefactos aprobados; sin la cadena no hay despliegue verificable | registro con copia y HA; verificación de firma en el destino | plataforma no seleccionada; `THR-023`, `THR-007` | C3/C4 | despliegue con registro degradado y verificación de firma | POR ACEPTAR |

#### B4.4 Registro — datos

| SPOF | Vista/componente | Escenario | Impacto | Mitigación propuesta | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| `SPOF-12` | material criptográfico y de recuperación | `SCN-08`, `SCN-09` | su pérdida es indisponibilidad y su compromiso es suplantación | jerarquía con raíz no exportable, ámbitos separados, custodia dividida | `ADR-009` `PROPUESTO`; sin producto, período ni custodios | C1–C4 + CLIENTE | rotación sin detención y recuperación con custodia dividida | ESCALADO `F3-DEC-002` |
| `SPOF-13` | respaldo, archivo y DR | `SCN-09` | respaldo no restaurable, o borrable por la misma autoridad que lo custodia | 3-2-1-1-0 con copia inmutable y claves fuera de esa autoridad | ubicación, producto y separación no definidos; `THR-049` | C1–C4 + CLIENTE | restauración mensual documentada y conmutación semestral | POR ACEPTAR |

#### B4.5 Registro — personas y proceso

Familia exigida por el contrato que ningún escenario había aislado. Se apoya en los criterios de aceptación 7 y 22 del Caso 06 y en `MC-18`.

| SPOF | Vista/componente | Escenario | Impacto | Mitigación propuesta | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| `SPOF-14` | planificación dependiente de una persona | transversal; `SCN-04` | el retiro del planificador deja la planificación sin continuidad | captura de conocimiento desde el mes 1, primera versión antes de H2 y versión validada antes del mes 12; reglas explícitas y versionadas | la fecha de retiro sigue abierta y la captura no ha comenzado | CLIENTE + A3 | planificación operada por un tercero usando solo las reglas capturadas | ESCALADO `ESC-05` |
| `SPOF-15` | aprobador único de break-glass y de accesos privilegiados | `SCN-04`, `SCN-08`, `SCN-09` | sin suplencia, o se detiene la operación de emergencia o se comparte la credencial | doble control con suplente designado; elevación temporal grabada | el CLIENTE no ha designado aprobadores ni suplencias; `THR-071` | CLIENTE | ejercicio de retorno con el aprobador titular ausente | ESCALADO `D2-DEP-005` |
| `SPOF-16` | dotación de turno, suplencias y habilitación ISPS | `SCN-02`, `SCN-09`, `SCN-10` | tres turnos y personal eventual; sin suplencia no hay quien atienda una alarma o un incidente | RACI con suplencias, canal alternativo, SOC 24x7 como servicio cuando falten especialistas | dotación, contactos y proveedor sin definir; `RT-11.17` operable con TI=5 | CLIENTE + C3 | ejercicio de incidente en turno de noche midiendo los plazos comprometidos | ESCALADO `D2-DEP-005` |

#### B4.6 Registro — terceros y sistemas conservados

| SPOF | Vista/componente | Escenario | Impacto | Mitigación propuesta | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| `SPOF-17` | TOS 2012 y su ventana de soporte | `SCN-04` | sistema conservado con fin de soporte no confirmado; condiciona toda la convivencia | puerta de viabilidad en H2/mes 4 y escenario conservador desde 01-01-2028 | el fabricante y el CLIENTE no han confirmado fechas ni capacidad de escritura | CLIENTE + fabricante | prueba de lectura, escritura y conciliación con contrato o versión acordada | ESCALADO `ESC-04` |
| `SPOF-18` | VMS conservado y su conducto | `SCN-12` | no se reemplaza; su degradación afecta protección ISPS | conducto único y mínimo, continuidad como condición de toda intervención | contrato y responsabilidades ISPS sin levantar; `THR-061`, `THR-070` | C3 + CLIENTE | continuidad del VMS durante la migración de red, con informe | ESCALADO `ESC-06` |
| `SPOF-19` | contrapartes externas sin interfaz ni SLA | `SCN-06`, `SCN-07` | un trámite detenido impide que el camión salga a ruta con documentación validada | canal asistido registrado como fallback y cola durable | plazos e interfaces de autoridades y ferrocarril sin levantar | CLIENTE + levantamiento | fallback con expediente completo y trazable | ESCALADO `ESC-14` / `ESC-01` |
| `SPOF-20` | proveedor de SOC y soporte remoto | `SCN-09` | detección y privilegio concentrados en una organización externa | acceso por elevación temporal grabada, sin vía permanente; suplencias contractuales | contratos de soporte no levantados; `THR-062` es crítica | CLIENTE | revisión de accesos vigentes de terceros y ejercicio de respuesta | ESCALADO `ESC-06` |
| `SPOF-21` | equipamiento de gate por carril | `SCN-03` | sin lectura o sin barrera, el carril deja de operar dentro del umbral | carril de excepción declarado y medido; equipos por carril | no se reemplaza barrera ni báscula; cantidades las define C4 | C2/C4 + CLIENTE | operación con un carril degradado midiendo el efecto sobre ≤120 s | POR ACEPTAR |

#### B4.7 Amenaza agregada por B4

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-071` | AST-006/001 | funciones con un solo titular / `CLS-SVC`, `CLS-CAN` | TB-03 + TB-10 | E | Una función crítica queda con un solo titular —aprobador de emergencia, planificador, turno sin suplencia—; ante su ausencia, o se detiene la operación o se comparte la credencial para continuar, y la acción deja de ser atribuible | P3 | I3 | ALTO |

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-071` | Suplente designado para toda función crítica; `SEC-IAM-01` identidad individual sin credenciales compartidas; `SEC-ADM-01` elevación temporal en lugar de cuenta permanente | `SEC-SIEM-01` alerta por uso simultáneo o por credencial usada fuera del titular; revisión de funciones con un solo titular | Activar la suplencia y revocar el uso compartido; **evidencia esperada:** ejercicio con el titular ausente sin compartir credencial | ALTO | ESCALADO | `D2-DEP-005`: el CLIENTE designa titulares y suplencias; `ESC-05` para la planificación |

#### B4.8 Cierre de B4

| Comprobación | Resultado | Estado |
|---|---|---|
| candidatos de `B3.16` consolidados | 16/16 confirmados como `SPOF-01..21` | CONFORME |
| cinco familias del contrato | infraestructura (6), servicio (5), datos (2), personas y proceso (3), terceros (5) | CONFORME |
| puntos ocultos por tener mitigación | ninguno; todas las mitigaciones son propuestas y condicionadas a prueba | CONFORME |
| aceptaciones | 0 `ACEPTADO`; 10 `POR ACEPTAR` y 11 `ESCALADO` | CONFORME |
| pruebas ejecutadas | ninguna; todas previstas | CONFORME |
| amenazas | se agrega `THR-071`; total `THR-001..071` | CONFORME |

**Hallazgo `B4-F01`:** la familia **personas y proceso** no estaba representada en los candidatos de B3, que nacieron de recorridos técnicos. Se agregaron `SPOF-14`, `SPOF-15` y `SPOF-16`, y de ahí surgió `THR-071`. Es la brecha que un modelo construido solo desde componentes tiende a dejar.

**Hallazgo `B4-F02`:** 11 de 21 puntos están `ESCALADO`, es decir, su resolución no depende de ningún frente sino del CLIENTE, de un fabricante o del levantamiento. B5 no puede aprobar un ADR cuyo riesgo residual dependa de uno de ellos.

**Punto de continuación histórico al cerrar B4:** revisar `ADR-001..010` con las materias de la plantilla global. Este punto fue ejecutado en B5 y posteriormente revalidado con `ADR-011` tras integrar A1–A3/C1–C4. Se conserva para explicar la secuencia, no como instrucción vigente.

### B5. Revisión de ADR-001..011 — revalidada con insumos integrados

**Estado del bloque: REVALIDADO CON INSUMOS REALES; propuesta no aprobada.** El corte inicial de B5 se hizo cuando A1–A3/C1–C4 no estaban integrados en esta rama. La reapertura B0/B1 contrasta ahora su contenido efectivo. D2 **revisa y recomienda**; la aprobación la conserva el autor de cada decisión. Modo registro, igual que B4.

#### B5.1 Método y límite real de esta revisión

La integración cambia la premisa anterior. `ADR-001` está redactado en A1 §6.2; `ADR-002` y `ADR-004`, en A3 §10; `ADR-003`, en A2 §7. Los cuatro tienen alternativa seleccionada y estado `PROPUESTO` declarado por su autor. `ADR-005` tiene alternativas y recomendación preliminar en C1 §7; `ADR-006` tiene alternativas y criterios en C3 §13, pero depende del site survey; `ADR-007` reúne criterios de almacenamiento/HA/DR en C3 §13 y C4 §6.1, sin cerrar aún la selección. `ADR-011` surge en C2 §4 como decisión transversal que debe abrirse, todavía sin alternativa seleccionada. `ADR-008..010` conservan la materia de D1.

Por eso la revisión vigente distingue tres grados:

- **Decisión propuesta con materia real:** `ADR-001..004` y `ADR-008..010`. Se revisa lo efectivamente escrito; `PROPUESTO` no equivale a aprobado.
- **Candidato desarrollado parcialmente:** `ADR-005..007`. Se conserva lo útil y se identifica exactamente la condición que impide seleccionar o aprobar.
- **Candidato nuevo:** `ADR-011`. Se registra para evitar una decisión cloud sin ADR; D2 no escoge proveedor ni región.

Regla heredada de `B4-F02` que gobierna todo el bloque: **un ADR no puede aprobarse si su riesgo residual depende de un SPOF `ESCALADO`**, porque su resolución no está en manos de ningún frente.

#### B5.2 `ADR-001..007` y `ADR-011` — revisión sobre evidencia real

| ADR | Autor | Evidencia y alternativas observadas | Consecuencia/riesgo que permanece | SPOF y amenazas amarradas | Disparador de revisión | Efecto en T-11 | Estado recomendado |
|---|---|---|---|---|---|---|---|
| `ADR-001` estilo | A1 | A1 §6.2 compara monolito, microservicios distribuidos y núcleo modular híbrido con runtime de borde; selecciona el tercero | carga operacional con TI=5 y coherencia del runtime local; falta demostrar el despliegue físico sin romper la decisión | `SPOF-01`; `THR-035`, `THR-037` | si el estilo exige más operación de la que TI=5 sostiene o B6 revela un componente crítico sin capacidad local | nodos y licencias de ejecución | **PROPUESTO — mantener; no aprobado** |
| `ADR-002` frontera del runtime local | A3/C1 | A3 §7/§10 selecciona las cinco funciones críticas en `EDGE-RUN`, declara lo degradado y el respaldo manual; descarta replicar todo o nada | C1 ubica `CTX-VESSEL` solo en nube aunque A1 lo declara crítico; la capacidad/prueba de 72 h sigue pendiente | `SPOF-01`, `SPOF-02`, `SPOF-04`; `THR-005`, `THR-064`, `THR-008` | contradicción A1↔C1 no resuelta, buffer insuficiente o sincronización sobre 90 min | cómputo y almacenamiento local | **PROPUESTO CONDICIONADO** a conciliación física y prueba |
| `ADR-003` integración y eventos | A2 | A2 §7 compara bus persistente, punto a punto y ESB pesado; selecciona `INT-HUB` con adaptadores por contraparte | `INT-HUB` concentra coordinación; contratos/protocolos reales de terceros siguen sin levantarse | `SPOF-08`; `THR-040`, `THR-041`, `THR-044` | una familia bloquea a otra, el reproceso duplica un hecho o el contrato real invalida el adaptador | broker, conectores y adaptadores | **PROPUESTO — mantener; no aprobado** |
| `ADR-004` convivencia y autoridad del TOS | A3 | A3 §10 selecciona autoridad única por dominio×zona×fase y envolver+sustitución progresiva; descarta permanencia indefinida y big bang | doble fuente de verdad, escritura parcial y retorno; privilegios/contrato del TOS dependen del fabricante | `SPOF-07`, `SPOF-17`; `THR-011`, `THR-015`, `THR-016` | puerta H2/mes 4 si lectura, escritura o conciliación no son confiables | adaptadores y licencias de integración | **PROPUESTO CONDICIONADO** a `SPOF-17`/`ESC-04/06` |
| `ADR-005` sala técnica | C1/C2 | C1 §7 compara habilitar la sala actual y reemplazarla; la variante “edge mínimo+nube” solo es admisible como sala principal nueva/acotada, no como ausencia de sala | rutas físicas separadas y cumplimiento de la sala actual no están levantados; ambiente marino no desaparece | `SPOF-06`, `SPOF-01`; `THR-052`, `THR-054` | `F2-ESC-008/ESC-09` o incumplimiento de requisitos completos de sala principal | UPS, generación, racks, carga y protección marina | **CANDIDATO — mantener** |
| `ADR-006` red de patio | C3 | C3 §13 compara inalámbrica empresarial redensificada, celular privada LTE/5G y esquema mixto; LTE/5G es alternativa primaria condicionada | dependencia simultánea del medio y ausencia de site survey | `SPOF-03`; `THR-068`, `THR-069`, `THR-019` | el site survey invalida cobertura/handover o revela falta de independencia | cantidad y ubicación por rango validado | **CANDIDATO — mantener** |
| `ADR-007` almacenamiento, HA y DR | C2/C3/C4 | C3/C4 aportan activo-pasivo, RTO/RPO, 3 nodos y comparación de paridad doble vs espejo distribuido; falta consolidar una selección formal | autoridad de borrado, restauración y nivel exacto no probados | `SPOF-13`, `SPOF-12`; `THR-046`, `THR-049` | RTO 4 h/RPO 15 min o tolerancia de disco no alcanzables | almacenamiento, réplica, licencias y respaldo | **CANDIDATO — mantener** |
| `ADR-011` proveedor/regiones cloud | C2; transversal | C2 §4 identifica criterios: presencia regional/AZ, latencia, carbono, servicios, certificaciones/residencia y reversibilidad; todavía no compara proveedores concretos | elegir proveedor sin comparación afectaría físico, seguridad, residencia y T-11 | `SPOF-13`, `SPOF-22`; `THR-049`, `THR-073` | disponibilidad de ofertas/regiones y medición de latencia/carbono; independencia de fallos y salida demostrable | servicios cloud, conectividad y salida | **CANDIDATO — abrir, no seleccionar** |

#### B5.3 `ADR-008..010` — revisión completa

| ADR | Alternativas presentadas | Selección propuesta | ¿Cumple la regla de aprobación? | SPOF y amenazas amarradas | Residual en escala D2 | Qué falta para aprobar | Estado recomendado |
|---|---|---|---|---|---|---|---|
| `ADR-008` identidad y acceso | A: IAM solo nube con sesiones cacheadas; B: IAM gobernado localmente y publicado a nube; C: gobierno común con capacidad local delegada | C, con alcance local acotado | **Sí en forma**: tres alternativas reales, criterios ponderados cualitativos, consecuencias negativas, impacto en T-11 y condición de revisión | `SPOF-10`, `SPOF-15`; `THR-024`, `THR-025`, `THR-071` | ALTO | resolver `F3-ESC-001` (directorio y federación) y `F3-ESC-002` (revocación en aislamiento); confirmar que existen productos con las capacidades, sin nombrarlos aún | **`PROPUESTO` condicionado** por el autor D1 después del corte B5; no aprobable mientras sigan los escalamientos |
| `ADR-009` llaves, secretos y cifrado | A: KMS solo nube con caché local; B: jerarquías independientes nube y local; C: gobierno y política comunes con ámbitos separados, raíz no exportable y servicio local protegido | C | **Sí en forma**; las alternativas A y B quedan como justificación y condición de revisión, no como opciones abiertas al mismo nivel | `SPOF-12`; `THR-048`, `THR-049` | ALTO | producto o capacidad, emplazamiento, custodios y suplencias, período de rotación y prueba de recuperación con custodia dividida | **`PROPUESTO`** — mantener; residual atado a SPOF `ESCALADO` |
| `ADR-010` detección, evidencia y SOC | A: detección central solo nube; B: plataformas independientes por ámbito; C: detección híbrida federada con repositorio central inalterable, reglas críticas locales y SOC gestionado 24x7 | C | **Sí en forma**; declara explícitamente que no presume un segundo SOC en la sala | `SPOF-20`, `SPOF-16`; `THR-038`, `THR-062` | ALTO, con `THR-062` en CRÍTICO | reparto nube/local, dimensionamiento de buffer e ingesta, ubicación y residencia, dotación, proveedor y modelo de acceso remoto | **`PROPUESTO`** — mantener; residual atado a SPOF `ESCALADO` |

#### B5.4 Cierre de B5

| Comprobación | Resultado | Estado |
|---|---|---|
| ADR revisados | 11/11: siete propuestas con materia (`ADR-001..004`, `ADR-008..010`), tres candidatos parciales (`ADR-005..007`) y un candidato nuevo (`ADR-011`) | CONFORME |
| ADR promovidos o aprobados por D2 | D2 no aprueba ninguno. Sincroniza `ADR-002/003/004` a `PROPUESTO` porque sus autores ya los declaran así; registra `ADR-011` como `CANDIDATO` | CONFORME |
| alternativas inventadas para decisiones ajenas | ninguna; la revisión cita alternativas y selecciones escritas por cada autor y conserva como candidato lo incompleto | CONFORME |
| vínculo decisión → SPOF → amenaza | 11/11 con SPOF y amenazas amarradas | CONFORME |
| efecto en T-11 | 11/11 declarado como materia, sin cantidades ni precios | CONFORME |
| amenazas nuevas | ninguna; el total se mantiene en `THR-001..071` | CONFORME |

**Hallazgo `B5-F01`, corregido por integración:** la afirmación “siete ADR sin contenido” quedó superada. `ADR-001..004` sí tienen decisión propuesta; `ADR-005/006` tienen alternativas y criterios sin selección firme; `ADR-007` tiene aportes técnicos todavía dispersos. La brecha actual ya no es ausencia general de contenido, sino completar y aprobar `ADR-005..007` cuando lleguen sus validaciones.

**Hallazgo `B5-F02`, vigente:** **ninguno de los once se aprueba desde D2**. `ADR-005..007/011` no tienen selección completa; los demás son propuestas de sus autores y conservan riesgos, pruebas o escalamientos abiertos. Propuesta documentada no equivale a aceptación del riesgo.

**Hallazgo `B5-F03`, parcialmente corregido:** A3 §7 ya declara las funciones no disponibles y su respaldo manual. Lo que permanece abierto para `ADR-002` es la correspondencia física: A1 incluye `CTX-VESSEL` en la continuidad crítica, mientras C1 lo ubica solo en nube y lo clasifica como alta. Frente 2 debe conciliarlo; D2 lo conserva como observación de entrada para B6.

#### B5.5 Ajuste posterior de coordinación con D1

El autor D1 promueve `ADR-008` a **`PROPUESTO`** como línea base condicionada para que A1–A3/C1–C4 puedan integrar y dimensionar una capacidad IAM local. Este cambio no contradice el corte B5 —D2 no promovió ningún ADR— ni convierte la decisión en aprobada: `F3-ESC-001/002`, `SPOF-10` y las validaciones de producto, capacidad y operación siguen abiertos. D1 B5.2.1 también delimita la admisión de eventos de seguridad para el dimensionamiento de `T11-SEC-04`; C4 debe medir el volumen dominante y no asumir la ingestión completa de telemetría operacional.

**Punto histórico de continuación:** B0/B1 habilitaron el cruce que se ejecuta a continuación. Se conserva para explicar la secuencia; ya no es la instrucción vigente.

### B6. Cruce y refinamiento contra catálogos reales

**Estado del bloque: BORRADOR REDACTADO; no aprobado.** B6 no reemplaza ni renumera las clases y amenazas históricas: agrega una capa verificable `amenaza → componente A1 → contrato A2/A3 → nodo C1–C4`, incorpora los huecos revelados por ese cruce y deja toda contradicción en manos del frente autor. No demuestra implementación ni acepta residuales.

#### B6.1 Universo y reglas del cruce

| Universo recibido | Total cruzado | Regla aplicada | Resultado |
|---|---:|---|---|
| actores A1 | 16 | usados como responsables o contrapartes; no se inventan personas | 16/16 disponibles; `ACT-TI` conserva brecha de consola administrativa |
| componentes lógicos A1 | 24 | cada ID debe tener clase, amenazas aplicables y correspondencia física | 24/24 |
| sistemas canónicos conservados/externos A1 | 11 | variantes contractuales A2 vuelven al ID canónico | 11/11 |
| contraparte concedente A2 | 1 | `EXT-CON` se registra como contraparte, no como duodécimo sistema canónico | 1/1 |
| nodos físicos C1 | 21 | cada nodo debe quedar cubierto directamente o por su función de infraestructura | 21/21 |
| amenazas previas | 71 | se conservan IDs, valoración y estado | 71/71 cruzadas por grupo |

Las clases `CLS-*` permanecen como agrupación STRIDE y los `AST-*` como activos protegidos. “Cubierto” significa que existe una amenaza aplicable y una evidencia prevista; **no** significa que el control esté implementado, probado o que el riesgo esté aceptado.

#### B6.2 Amenazas nuevas reveladas por el cruce

**Tabla A — identificación y valoración**

| ID | Activos | Componente/clase | Frontera | STRIDE | Condición y escenario portuario | Prob. | Impacto | Riesgo inherente |
|---|---|---|---|---|---|---:|---:|---|
| `THR-072` | AST-001/002/005/010/014 | `DATA-CORE`, `DATA-TS`, `DATA-DOC`, `DATA-AN` / `CLS-DAT` | TB-11 + TB-14 | S | Una configuración, descubrimiento de servicio o identidad de réplica alterados hacen que un servicio se conecte a un almacén falso; consume estado fabricado o escribe datos autoritativos en un extremo controlado por un tercero | P2 | I4 | ALTO |
| `THR-073` | AST-007/008/013/014 | `PHY-CLD-01..10`, servicios cloud / `CLS-EXT` | TB-04 + TB-14 | D | La región primaria y la recuperación comparten proveedor, plano de control, identidad, facturación o capacidad no independiente; un fallo común o suspensión impide ambos caminos cloud y deja solo la autonomía local declarada | P2 | I4 | ALTO |

**Tabla B — controles, evidencia esperada y estado**

| ID | Control preventivo | Control detectivo | Respuesta correctiva y evidencia esperada | Residual proyectado | Estado | Validación pendiente |
|---|---|---|---|---|---|---|
| `THR-072` | autenticación mutua por endpoint; validación de identidad/certificado del servidor; destinos privados permitidos; configuración de conexión firmada y versionada; credencial separada por almacén con `SEC-KEY-01`/`SEC-SECRET-01` | alerta por cambio de endpoint, certificado, topología o identidad de réplica; detección de lector/escritor no inventariado | aislar el extremo, revocar/rotar identidad, contrastar con el almacén autoritativo y reconciliar operaciones; **evidencia esperada:** prueba en que un endpoint o réplica falsa es rechazada y registrada | ALTO | POR VALIDAR | `D2-DEP-003` y `ADR-011`: producto, descubrimiento, réplica, certificados y topología real aún no están seleccionados |
| `THR-073` | regiones y recuperación con dominios de fallo explícitos; autonomía local de 72 h; credenciales de emergencia separadas; exportación y redespliegue probados; plan de salida coherente con RT-03.07 | sondas independientes del proveedor; alerta por degradación simultánea de región, plano de control, identidad o cuenta | declarar modo local, conmutar solo si el destino es independiente e invocar recuperación/salida; **evidencia esperada:** ejercicio regional y de portabilidad que identifique dependencias comunes y mida RTO/RPO | ALTO | POR VALIDAR | `ADR-011` y `D2-DEP-005`: proveedor, regiones, términos, cuenta y mecanismo de salida requieren decisión y acuerdo externos |

`THR-072` cierra la casilla `CLS-DAT`/S a nivel de modelo. `THR-073` no impone multicloud: exige declarar y probar el dominio de fallo y la salida de la opción elegida.

#### B6.3 Cobertura por componente lógico A1

Para mantener compactas las tablas B6.3–B6.6, los números de la columna «Amenazas» conservan el prefijo implícito `THR-`: por ejemplo, `024` significa `THR-024` y `030–034` significa `THR-030..034`.

| Componente | Clase | Amenazas aplicables | Correspondencia C1 | Observación de cruce |
|---|---|---|---|---|
| `CH-PORTAL` | CLS-CAN | 024, 027, 028, 067 | `PHY-CLD-01` | sin contradicción material |
| `CH-APP` | CLS-CAN | 026, 027, 029, 064, 067 | dispositivo + `PHY-CLD-01`/`PHY-OPS-01` | capacidad local acotada por A3 |
| `CH-CAB` | CLS-CAN | 025, 029, 067, 068 | `PHY-EDG-04` | C1 lo ubica en muelle; A1 lo usa como canal de cabina/campo: revisar ubicación en F2 |
| `GW-EDGE` | CLS-GWY | 028, 032, 033, 034, 065 | `PHY-CLD-01` | criticidad A1 alta/C1 media |
| `GW-API` | CLS-GWY | 027, 030–034, 063 | `PHY-CLD-02` | criticidad A1 alta/C1 media |
| `CTX-OPS` | CLS-SVC | 011, 012, 035, 037, 044, 051 | `PHY-OPS-01`/`PHY-CLD-03` | autoridad se rige por A3 |
| `CTX-GATE` | CLS-SVC | 018, 027, 030, 035–037, 044, 067 | `PHY-OPS-01`+`PHY-EDG-01`/`PHY-CLD-03` | fallback manual declarado en A3 |
| `CTX-YARD` | CLS-SVC | 011, 017, 035–037, 044, 051, 068, 069 | `PHY-OPS-01`+`PHY-EDG-02`/`PHY-CLD-03` | sin contradicción material |
| `CTX-REEFER` | CLS-SVC | 019–021, 035–039, 044, 068 | `PHY-OPS-01`+`PHY-EDG-03`/`PHY-CLD-03` | alarma depende de cobertura/capacidad probada |
| `CTX-PLAN` | CLS-SVC | 036, 037, 071 | `PHY-CLD-03`/`PHY-OPS-01` lectura | respaldo impreso/radio declarado; persona única sigue como SPOF |
| `CTX-VESSEL` | CLS-SVC | 035, 037, 056, 057, 067 | `PHY-CLD-03` solamente | **contradicción:** A1 crítico/local y A3 incluye operación de nave; C1 alta/solo nube |
| `CTX-BILL` | CLS-SVC | 029, 035, 037, 041, 051, 059 | `PHY-OPS-01`/`PHY-CLD-03` | contrato ERP aún externo |
| `CTX-INSP` | CLS-SVC | 036, 037, 058, 060, 067 | `PHY-CLD-03`+`PHY-EDG-05` | criticidad A1 alta/C1 media |
| `CTX-EMIS` | CLS-SVC | 035, 037, 045, 060 | `PHY-CLD-03`/`PHY-EDG-02` captura | criticidad A1 alta/C1 media |
| `SRV-IAM` | CLS-SVC | 024, 025, 027, 030, 034, 035, 064, 071 | `PHY-CLD-03`/`PHY-OPS-01` caché | criticidad A1 alta/C1 crítica; alcance local condicionado por ADR-008 |
| `SRV-NOTIF` | CLS-SVC | 019, 037, 039 | `PHY-CLD-03`/`PHY-OPS-01` canal local | canal y escalamiento deben probarse |
| `SRV-EVID` | CLS-SVC | 029, 046, 059 | `PHY-CLD-03`/`PHY-OPS-01` sello local | evidencia prevista, no custodia demostrada |
| `INT-HUB` | CLS-BRK | 001, 002, 006, 008, 040–044, 056–060, 065 | `PHY-CLD-04`/`PHY-OPS-01` cola | bulkhead y capacidad pendientes de prueba |
| `INT-TOS` | CLS-BRK | 009–016 | `PHY-OPS-03` | contrato y soporte reales permanecen externos |
| `EDGE-RUN` | CLS-EDG | 001–008, 018–021, 052–055, 064, 067, 068 | `PHY-OPS-01` | frontera funcional de ADR-002 condicionada por `CTX-VESSEL` |
| `DATA-CORE` | CLS-DAT | 002, 008, 010–014, 043–045, 049, 051, 055, 072 | `PHY-CLD-05`/`PHY-OPS-01`+`PHY-OPS-02` | `THR-072` agrega identidad del almacén |
| `DATA-TS` | CLS-DAT | 019, 020, 042, 043, 046, 049, 055, 072 | `PHY-CLD-06`/`PHY-OPS-02` | sin contradicción material |
| `DATA-DOC` | CLS-DAT | 029, 042, 043, 045, 049, 050, 055, 060, 070, 072 | `PHY-CLD-07`/`PHY-OPS-02` | criticidad A1 alta/C1 media |
| `DATA-AN` | CLS-DAT | 042, 043, 045, 050, 060, 066, 072 | `PHY-CLD-08` | salida depende del catálogo de campos |

Los rangos representan amenazas aplicables ya definidas; no crean una amenaza por combinación. Las siete diferencias de criticidad observadas son `CTX-EMIS`, `CTX-INSP`, `CTX-VESSEL`, `DATA-DOC`, `GW-API`, `GW-EDGE` y `SRV-IAM`. B6 no decide cuál catálogo prevalece.

#### B6.4 Cobertura de sistemas, contrapartes y contratos A2/A3

| ID canónico o contraparte | Variantes A2 agrupadas | Amenazas aplicables | Paso físico principal | Resultado |
|---|---|---|---|---|
| `EXT-TOS12` | contrato TOS 2012 | 009–016 | `INT-TOS`/`PHY-OPS-03` | cubierto; contrato, versión y soporte externos |
| `EXT-ERP` | contrato ERP | 041, 059, 060 | `INT-HUB`/`PHY-CLD-04` | cubierto; regla de objeción externa |
| `EXT-GRU` | familia técnica grúas | 017, 021, 023, 062 | `PHY-EDG-04`/conducto de solo lectura | cubierto sin asumir control remoto |
| `EXT-ACC` | familia control de acceso | 017, 021, 025, 062 | `PHY-EDG-01`/red de protección | cubierto; no se reemplaza el sistema |
| `EXT-VMS` | VMS conservado | 022, 061, 062, 070 | TB-09/red de protección | cubierto sin transportar video por defecto |
| `EXT-VGM` | báscula/VGM | 017, 018, 021, 023 | `PHY-EDG-01` | cubierto sin inventar protocolo |
| `EXT-OCR` | lectura óptica | 017, 018, 021, 023 | `PHY-EDG-01` | cubierto; cantidad/equipo queda en F2 |
| `EXT-NAV` | `CP-NAV-01..14` | 056, 057, 065 | `INT-HUB`/`PHY-CLD-04` | cubierto por contrato/versionado por naviera |
| `EXT-AUT` | `EXT-AUT-ADU/SAG/SAN` | 058, 060, 065 | `INT-HUB`/`PHY-CLD-04` | cubierto; fallback asistido declarado |
| `EXT-FER` | ferrocarril | 058, 060, 065 | `INT-HUB`/`PHY-CLD-04` | cubierto; interfaz/plazo externo |
| `EXT-RAD` | radio/periferia de patio | 017, 019, 021, 068, 069 | `PHY-EDG-02/03` + red operacional | cubierto; independencia depende del site survey |
| `EXT-CON` contraparte | concedente/reportes | 058, 060, 065 | INT-HUB/DATA-AN | cubierta como contraparte; no suma sistema canónico |

Las 7 familias técnicas de A2 se absorben en los IDs conservados y nodos de periferia; “POR LEVANTAR” en protocolo o SLA se conserva en `D2-DEP-005`, no se interpreta como falta de amenaza.

#### B6.5 Cobertura de nodos de infraestructura C1

Los componentes anteriores cubren `PHY-CLD-01..08`, `PHY-OPS-01..03` y `PHY-EDG-01..05`. Los nodos que cumplen una función transversal, sin componente lógico exclusivo, se cruzan así:

| Nodos | Función C1 | Amenazas aplicables | Observación |
|---|---|---|---|
| `PHY-CLD-09` | observabilidad/SIEM | 003, 038, 047, 063 | revisar posible solape de capacidad `T11-C2-19`/`T11-SEC-04` |
| `PHY-CLD-10` | réplicas/DR | 049, 072, 073 | independencia real depende de ADR-011 y prueba de restauración/conmutación |
| `PHY-OPS-04` | núcleo de red operacional | 001, 006, 017, 021, 022, 068, 069 | rutas e independencia sujetas a site survey |
| `PHY-OPS-05` | custodia de medios | 048, 049 | custodios, separación e inventario pendientes |
| `PHY-OPS-06` | operación del personal | 025, 034, 052, 062, 071 | `ACT-TI`, suplencias y accesos privilegiados siguen observados |

Con esta tabla, los 21 nodos tienen al menos una amenaza y evidencia prevista. B7 debe auditar que el detalle físico no haya ocultado un subnodo o dominio de fallo adicional.

#### B6.6 Cruce completo por grupos de amenazas

| Amenazas | Dominio real refinado | Contratos/fronteras | Nodos principales | Estado del cruce |
|---|---|---|---|---|
| 001–008 | EDGE-RUN, INT-HUB, DATA-CORE | TB-04 | `PHY-OPS-01/02/04` + `PHY-CLD-04/05` | cerrado a nivel documental |
| 009–016 | INT-TOS, CTX-OPS/BILL, TOS 2012 | TB-06, EXT-TOS12 | `PHY-OPS-03` + `PHY-OPS-01` | externos visibles |
| 017–023 | gate, yard, reefer y periferia | TB-05/09/12 | `PHY-EDG-01..05` + `PHY-OPS-04` | site survey/protocolos pendientes |
| 024–029 | CH-PORTAL/APP/CAB, IAM/EVID | TB-01/03 | `PHY-CLD-01/03` + `PHY-OPS-01` + `PHY-EDG-04` | ubicación CH-CAB observada |
| 030–034 | GW-EDGE/GW-API | TB-01/02/10 | `PHY-CLD-01/02` | criticidad observada |
| 035–039 | CTX-* y servicios comunes | TB-02/03/11 | `PHY-CLD-03` + `PHY-OPS-01` | CTX-VESSEL observado |
| 040–044 | INT-HUB y contratos externos | TB-07/08/11 | `PHY-CLD-04` + `PHY-OPS-01` | contratos efectivos externos |
| 045–051 | DATA-* y evidencia | TB-11/14 | `PHY-CLD-05..08/10` + `PHY-OPS-02/05` | catálogo de campos pendiente |
| 052–055 | runtime/administración local | TB-05/10/14 | `PHY-OPS-01/04/06` | pruebas físicas pendientes |
| 056–062 | terceros y sistemas conservados | TB-07/08/09/10 | `PHY-CLD-04` + `PHY-OPS-04/06` + `PHY-EDG-*` | contratos/SLA externos |
| 063–066 | autorización, offline, identidad externa y minimización | TB-02/03/08/11 | `PHY-CLD-02/03/04/08/09` + `PHY-OPS-01` | campos y aprobadores pendientes |
| 067–070 | frescura, radio, alcance y evidencia VMS | TB-04/05/09 | `PHY-OPS-01/04` + `PHY-EDG-01..04` | site survey/retención externos |
| 071 | titulares y suplencias | TB-03/10 | `PHY-OPS-06` | aceptación CLIENTE pendiente |
| 072–073 | identidad de datos y fallo común cloud | TB-11/14/04 | `PHY-CLD-05..10` + `PHY-OPS-01/02` | amenazas nuevas condicionadas |

#### B6.7 SPOF y hallazgos del refinamiento

| SPOF | Vista/componente | Escenario | Impacto | Mitigación propuesta | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| `SPOF-22` | proveedor, regiones y plano de control cloud | recuperación cloud y `THR-073` | un fallo común impide producción y DR cloud; quedan solo funciones locales | dominios de fallo explícitos, credenciales separadas, portabilidad y salida probadas | `ADR-011` no tiene selección; independencia y reversibilidad no demostradas | C1–C4 + CLIENTE | ejercicio regional y de salida que mida RTO/RPO y dependencias comunes | POR ACEPTAR |

| Hallazgo | Resultado | Tratamiento |
|---|---|---|
| `B6-F01` | 24/24 componentes, 11/11 sistemas canónicos y 21/21 nodos tienen amenazas aplicables | llevar a auditoría B7; no equivale a control probado |
| `B6-F02` | `CLS-DAT`/S no estaba cubierta por amenaza propia | agregada `THR-072`; casilla cerrada a nivel de modelo |
| `B6-F03` | C1 no refleja la continuidad local crítica de `CTX-VESSEL` declarada por A1/A3 | corrección requerida a Frente 2; condiciona ADR-002 y cierre físico |
| `B6-F04` | hay seis diferencias adicionales de criticidad —las siete observadas en `B6.3` menos `CTX-VESSEL`, tratada aparte en `B6-F03`—, ubicación discutible de `CH-CAB` y brecha de actor `ACT-TI` | registrar para sus autores; D2 no altera A1/C1 |
| `B6-F05` | observabilidad/SIEM puede estar dimensionada dos veces como `T11-C2-19` y `T11-SEC-04` | C2/C4 deben aclarar alcance y evitar doble conteo |
| `B6-F06` | ADR-011 no tenía amenaza ni SPOF propios de fallo común/salida cloud | agregados `THR-073` y `SPOF-22`; no se prescribe proveedor ni multicloud |

#### B6.8 Cierre y transición de dependencias

| Comprobación | Resultado | Estado |
|---|---|---|
| componentes A1 | 24/24 con clase, amenaza y correspondencia física | CONFORME DOCUMENTAL |
| sistemas/contrapartes A2 | 11/11 canónicos + `EXT-CON`; variantes agrupadas sin inflar el catálogo | CONFORME DOCUMENTAL |
| nodos C1 | 21/21 con amenaza aplicable | CONFORME DOCUMENTAL CON OBSERVACIONES |
| cobertura STRIDE | `CLS-DAT`/S cerrada por `THR-072`; las siete clases tienen S/T/R/I/D/E | CONFORME DE MODELO |
| amenazas vigentes | 73: 6 CRÍTICO, 64 ALTO, 3 MEDIO; ninguna BAJO ni aceptada | CONFORME |
| SPOF vigentes | 22: 0 `ACEPTADO`, 11 `POR ACEPTAR`, 11 `ESCALADO` | CONFORME |
| entradas A1/A2/A3/C1–C4 | `D2-DEP-001/002` resueltas para diseño; `D2-DEP-003` cruzada con observaciones | CONFORME CON SALIDAS |
| controles/campos | D1 disponible; catálogo campo→sensibilidad→retención del Subdocumento 5 ausente | `D2-DEP-004` PARCIAL |
| contratos, site survey, pruebas y aceptadores | continúan fuera de los frentes | `D2-DEP-005` BLOQUEADO EXTERNO |
| `RT-11.02` | existe modelo refinado y regla de actualización; falta auditar cobertura/cambios en B7 | EN CURSO |

**Retomar exactamente aquí:** ejecutar B7 como auditoría documental del inventario, integraciones, trazabilidad, contradicciones y salidas accionables. No corregir documentos de Frente 1/2 desde D2 y no cerrar riesgos que dependan del CLIENTE o de pruebas. **B8 continúa diferido**: sin diagramas ni resumen residual final hasta terminar la auditoría.

### B7. Auditoría documental v0.5

**Veredicto: `CONFORME PARA v0.5 CON PENDIENTE ADR`, con seis correcciones aplicadas dentro de D2 y hallazgos dirigidos a sus autores.** Conforme significa que el modelo de amenazas es coherente, trazable y auditable como **diseño documental**. No significa que los once ADR estén completos: `ADR-011` conserva una brecha de alternativas/selección. Tampoco significa control implementado, prueba ejecutada, riesgo aceptado ni ADR aprobado. Modo registro.

#### B7.1 Alcance y método de la auditoría

Se auditó contra evidencia primaria —A1, A2, A3, C1–C4, D1, Maestro, Plan, Matriz global y Registro ADR—, no contra lo que B6 declara de sí mismo. Las comprobaciones de conteo, unicidad, saltos, referencias rotas y coherencia de valoración se ejecutaron de forma mecánica sobre el texto de D2; las de contenido, por lectura contrastada. D2 corrige solo lo suyo: **ningún documento de Frente 1 o Frente 2 fue modificado**; sus problemas quedan como hallazgo dirigido.

#### B7.2 Resultado de las doce comprobaciones exigidas

| # | Comprobación | Resultado verificado | Estado |
|---:|---|---|---|
| 1 | 24 componentes A1 cubiertos sin clase genérica como sustituto | 24/24 con amenazas nominadas propias y correspondencia física; la clase `CLS-*` acompaña pero nunca reemplaza al ID. Ningún componente citado en D2 es inexistente en A1, y ninguno de A1 falta en D2 | CONFORME |
| 2 | 11 canónicos, `EXT-CON` y variantes A2 correctamente agrupados | 11 canónicos (`EXT-ACC/AUT/ERP/FER/GRU/NAV/OCR/RAD/TOS12/VGM/VMS`), los once presentes en A1/A2/A3 y en el Maestro §5.2; `EXT-CON` registrado como contraparte y **no** como duodécimo sistema; variantes `CP-NAV-01..14` y `EXT-AUT-ADU/SAG/SAN` agrupadas en su ID canónico sin inflar el catálogo | CONFORME |
| 3 | 21 nodos C1 con amenazas aplicables | 21/21 `PHY-CLD-01..10`, `PHY-OPS-01..06`, `PHY-EDG-01..05` con al menos una amenaza y evidencia prevista. Ningún `PHY-*` citado en D2 es inexistente en C1–C4 | CONFORME CON OBSERVACIÓN |
| 4 | `THR-001..073` sin saltos, duplicaciones ni referencias rotas | 73 filas de identificación y 73 de control, correspondencia 1:1, cero duplicados, cero saltos, cero amenazas citadas sin definir. Valoración coherente con la matriz de `B2.1` en 73/73 y residual proyectado igual al inherente en 73/73 | CONFORME |
| 5 | `THR-072`, `THR-073` y `SPOF-22` independientes | Independientes. `THR-072` es suplantación **del almacén o su réplica** ante un consumidor legítimo, distinta de `THR-044` (productor no autorizado en el bus) y de `THR-043` (componente legítimo que puentea al servicio propietario). `THR-073` es pérdida **simultánea** de producción y recuperación cloud por fallo común, distinta de `THR-006` (saturación del enlace) y de `THR-049` (respaldo no restaurable) | CONFORME CON OBSERVACIÓN |
| 6 | Siete clases con las seis categorías STRIDE; cierre de `CLS-DAT`/S | Matriz 7 × 6 sin casilla vacía. `CLS-DAT`/S queda cerrada por `THR-072`, que es una suplantación propia del almacén y no una reasignación de `THR-043`/`THR-044` | CONFORME |
| 7 | 22 SPOF con mitigación, aceptación, prueba y estado, ninguno aceptado | 22/22 con las nueve columnas completas, sin celda vacía. **0 `ACEPTADO`**; 11 `POR ACEPTAR` y 11 `ESCALADO` | CONFORME |
| 8 | 11 ADR con alternativas, consecuencias, condición de revisión, efecto T-11 y vínculo amenaza/SPOF | 11/11 revisados y enlazados; 10 tienen alternativas suficientemente identificadas para este corte. `ADR-011` solo declara criterios y el riesgo `THR-073`/`SPOF-22`: falta comparar alternativas concretas y seleccionar una | PENDIENTE — autor C2/integrador |
| 9 | Las cinco observaciones no fueron corregidas en silencio | Las cinco persisten visibles y nominadas: contradicción `CTX-VESSEL`, seis diferencias adicionales de criticidad, ubicación de `CH-CAB`, brecha de `ACT-TI` y posible doble conteo `T11-C2-19`/`T11-SEC-04`. Ninguna fue resuelta desde D2 ni silenciada | CONFORME |
| 10 | Estados históricos y estado vigente no se contradicen | **No conforme al auditar**: cuatro lugares afirmaban en presente cifras de corte ya superadas. Corregido en `B7.4`; ver `B7-F01` a `B7-F04` | CORREGIDO |
| 11 | `RT-11.02` con modelo refinado y regla explícita de actualización | Modelo refinado: sí. Regla de actualización: **incompleta al auditar** —cubría solo componente e integración—. Ampliada a los cinco disparadores exigidos; ver `B7-F05` | CORREGIDO |
| 12 | Sin cantidades, productos, contratos, pruebas ni aceptaciones inventadas | El barrido y la revisión contextual encontraron cifras y capacidades trazadas a fuentes, pero ningún precio, producto seleccionado, contrato efectivo, prueba ejecutada ni aceptación presentada sin respaldo | CONFORME |

#### B7.3 Cifras vigentes al cierre de B7

Esta tabla es la **única fuente de cifras vigentes** de D2. Las cifras que aparecen dentro de B2, B3 y B4 son cortes fechados de esos bloques y así quedan marcadas.

| Universo | Cifra vigente | Nota |
|---|---|---|
| amenazas `THR-001..073` | 73 | 6 CRÍTICO, 64 ALTO, 3 MEDIO, 0 BAJO; 68 `POR VALIDAR` y 5 `ESCALADO`; ninguna aceptada |
| puntos únicos `SPOF-01..22` | 22 | 11 `POR ACEPTAR`, 11 `ESCALADO`, **0 `ACEPTADO`** |
| clases `CLS-*` × STRIDE | 7 × 6 completas | `CLS-DAT`/S cerrada por `THR-072` |
| componentes A1 cruzados | 24/24 | correspondencia física declarada |
| sistemas canónicos + contraparte | 11 + `EXT-CON` | variantes contractuales agrupadas |
| nodos C1 cruzados | 21/21 | con observación de subnodos y dominios de fallo |
| escenarios `SCN-01..12` | 12 | 8/8 materias del contrato |
| ADR revisados | 11/11 | 0 aprobados por D2 |
| activos `AST-001..016` y fronteras `TB-01..14` | 16 y 14 | sin cambios desde B1 |

#### B7.4 Hallazgos corregidos dentro de D2

| Hallazgo | Problema detectado | Corrección aplicada |
|---|---|---|
| `B7-F01` | La casilla de «Trabajo requerido» del contrato —texto vigente, no histórico— seguía declarando `CLS-DAT`/S abierta y pendiente de B6 | Reescrita para reflejar que B6 la cerró con `THR-072`, conservando que es cobertura de modelo y no control probado |
| `B7-F02` | `TRZ_D2.md` §3 mantenía la fila de amenazas por clase con «66 amenazas `THR-001..066`» y `CLS-DAT`/S abierta, en una tabla de estado vigente | Fila actualizada a las cifras vigentes con remisión a `B7.3` |
| `B7-F03` | `B2.8` y `B3.15` afirmaban en presente que `CLS-DAT`/S sigue abierta, sin marca de corte | Añadida marca de corte a ambos. **No se reescribió el historial**: el texto original se conserva y se anota qué bloque posterior lo superó |
| `B7-F04` | La fila de B4 en la tabla de bloques declaraba `SPOF-01..21` sin señalar la cifra vigente | Anotada como cifra de corte de B4, con la vigente `SPOF-01..22` junto a ella |
| `B7-F05` | La regla de actualización de `RT-11.02` cubría solo «componente o integración»; el requisito exige además contratos, nodos, controles y ADR | Regla ampliada a cinco disparadores (componente A1, integración A2/A3, nodo C1–C4, control `SEC-*` de D1 y estado o alternativa de un ADR), con obligación de registrar el cambio como corte fechado en `TRZ_D2` y prohibición de reescribir bloques cerrados |
| `B7-F06` | «Siete diferencias de criticidad» en `B6.3` frente a «seis diferencias adicionales» en `B6-F04` podía leerse como contradicción | Precisado: seis adicionales son las siete observadas menos `CTX-VESSEL`, que se trata aparte en `B6-F03` |

#### B7.5 Observaciones que la auditoría agrega

| ID | Observación | Destinatario |
|---|---|---|
| `B7-O01` | `SPOF-13` (respaldo, archivo y DR) y `SPOF-22` (proveedor, regiones y plano de control cloud) son adyacentes: el primero es la recuperabilidad del respaldo y la separación de autoridad de borrado; el segundo, el dominio de fallo común del proveedor. **No deben consolidarse ni contarse dos veces** en B8, en el T-11 ni en la integración | D2 B8, C2/C4, integrador |
| `B7-O02` | Los 21 nodos tienen amenaza aplicable, pero el nivel de detalle físico puede ocultar un subnodo o un dominio de fallo adicional —por ejemplo dentro de `PHY-OPS-04` o `PHY-CLD-10`—. La cobertura es 21/21 **sobre el catálogo declarado**, no sobre la instalación real | C1/C3; verificar en B8 |
| `B7-O03` | Las cinco observaciones dirigidas a Frentes 1 y 2 siguen abiertas y ninguna depende de D2. Mientras `CTX-VESSEL` no se concilie, `ADR-002` no puede cerrarse y la frontera funcional de `EDGE-RUN` queda condicionada | A1/A3, C1; `ADR-002` |

#### B7.6 Veredicto sobre `RT-11.02`

**Cubierto a nivel de diseño documental.** Existen los cuatro elementos que el requisito exige: metodología declarada (`B2.1`, `B2.2`), amenazas por cada componente e integración externa sobre catálogos reales (`B6.3`–`B6.6`), vínculo amenaza→control `SEC-*` y evidencia prevista, y —desde esta auditoría— una **regla explícita de actualización ante cambios** con sus cinco disparadores.

**Continúa `EN CURSO`, y no puede pasar a cumplido, por tres razones que no dependen de D2:** ninguna prueba está ejecutada; la revisión cruzada con D1, C1–C4 y el integrador no se ha hecho; y no existe aprobación del CLIENTE ni de un revisor independiente. Además, `D2-DEP-004` sigue parcial: sin el catálogo campo→sensibilidad→retención del Subdocumento 5, la cobertura sobre datos es de modelo y no de campo.

#### B7.7 Cierre de B7 y punto de continuación

| Comprobación de cierre | Resultado | Estado |
|---|---|---|
| doce comprobaciones exigidas | 9 conformes —2 con observación—, 2 no conformes corregidas dentro de D2 y 1 pendiente de autor (`ADR-011`) | CONFORME PARA v0.5 CON PENDIENTE ADR |
| documentos de Frente 1 y 2 modificados | ninguno | CONFORME |
| riesgos aceptados, SPOF cerrados o ADR aprobados en B7 | ninguno | CONFORME |
| diagramas | no producidos; B8 sigue diferido | CONFORME |
| D3 | no ejecutado | CONFORME |

**Retomar exactamente aquí: integración de D1 con D2.** El siguiente paso no es B8 ni D3, sino **conciliar D1 y D2 como un solo paquete de seguridad** antes de que el integrador toque `90_Consolidado/`. Concretamente:

1. Verificar que los 31 controles `SEC-*` de D1 tengan al menos una amenaza `THR-*` que los invoque, y al revés, que ningún `SEC-*` citado en D2 quede sin desarrollo en D1. D2 ya no cita ningún control inexistente; falta la dirección contraria.
2. Cruzar `SEC-PHYS-v0.1` (17 grupos) con `SPOF-01..22` y con `B7-O01`, para que C4 no genere filas T-11 duplicadas.
3. Sincronizar el estado de `RT-11.02` entre `TRZ_D1` y `TRZ_D2` con el veredicto de `B7.6`.
4. Resolver o escalar formalmente las cinco observaciones de `B7-O03` con A1, A3 y C1.
5. Solo después: `B8` —diagrama de fronteras y resumen de riesgo residual— y luego D3.

**Qué debe conservar quien continúe:** `AST-001..016`, `TB-01..14`, `CLS-*`, `THR-001..073`, `SCN-01..12`, `SPOF-01..22`, `ADR-001..011`, las dependencias `D2-DEP-001..005` con su estado vigente, los escalamientos `ESC-01/04/05/06/07/09/10/14` y `F3-ESC-001/002/003`, la escala de `B2.1`, la regla de no aceptación de `B2.6` y la regla de actualización ampliada del método. Ningún bloque cerrado se reescribe: los cambios se emiten como corte fechado en `TRZ_D2`.

#### B7.8 Corte de integración con D1 — controles de gobierno y aseguramiento

**Fecha: 2026-09-06.** Al ejecutar la revisión cruzada pedida por B7.7 se confirmó que D2 ya cita 24 de los 31 controles `SEC-*` de D1 dentro de las filas de tratamiento. Los siete restantes son controles de gobierno o aseguramiento que actúan sobre amenazas ya modeladas; no justifican crear amenazas duplicadas. Se enlazan en este corte, conforme a la regla de actualización de `B7-F05`.

| Control D1 | Amenazas D2 que gobierna o verifica | Relación | Estado |
|---|---|---|---|
| `SEC-GOV-01` | `THR-038`, `THR-047`, `THR-071`, `THR-073` | mantiene propietario, excepción, residual y evidencia por control/riesgo | ENLAZADO; responsable nominal pendiente |
| `SEC-CLOUD-01` | `THR-049`, `THR-060`, `THR-072`, `THR-073` | explicita responsabilidad, residencia, borrado, réplica y salida cloud | ENLAZADO; condicionado por `ADR-011` y Subdocumento 5 |
| `SEC-IR-01` | `THR-038`, `THR-047`, `THR-062`, `THR-070` | gobierna contención, comunicación, custodia y causa raíz | ENLAZADO; plan/RACI y ejercicio pendientes |
| `SEC-VULN-01` | `THR-023`, `THR-050`, `THR-053`, `THR-062` | detecta y conduce remediación de firmware, pipeline, IaC y acceso de terceros | ENLAZADO; herramienta y evidencia pendientes |
| `SEC-PENTEST-01` | `THR-030`, `THR-034`, `THR-043`, `THR-065` | verifica autorización, aislamiento y resistencia de interfaces antes de producción | ENLAZADO; tercero/alcance e informe pendientes |
| `SEC-SDLC-01` | `THR-023`, `THR-050`, `THR-053` | exige revisión y traza del cambio que podría introducir alteración o configuración insegura | ENLAZADO; ejecución pendiente |
| `SEC-SAMM-01` | `THR-050`, `THR-053` | mide que las prácticas de prevención no sean controles puntuales sin mejora sistemática | ENLAZADO; evaluación inicial/anual pendiente |

**Resultado del cruce bidireccional:** 31/31 controles D1 tienen al menos una amenaza D2 asociada y ningún `SEC-*` citado por D2 carece de desarrollo en D1. La relación no cambia valoración, residual ni aceptación de ninguna amenaza. `ADR-011` continúa `CANDIDATO` y este corte no sustituye su comparación de alternativas.

#### B7.9 Revisión conjunta D1–D2 y gobierno — bloque 5

La puerta conjunta B7-C verificó el modelo D2 contra D1, `TRZ_D1`, `TRZ_D2`, el registro ADR, la matriz global, las decisiones/escalamientos y la auditoría del frente. Resultado: 31/31 controles D1 enlazados; `THR-001..073` y `SPOF-01..22` definidos sin referencias huérfanas; estados ADR compatibles y ningún riesgo aceptado. No apareció un hallazgo interno nuevo que cambie probabilidad, impacto, residual o tratamiento.

El paquete queda **listo para auditoría independiente/general**, con los hallazgos externos ya conocidos: `ACT-TI`, `CTX-VESSEL`, criticidades A1/C1, `CH-CAB`, solape SIEM, Subdocumento 5, `ADR-011`, site survey, contratos/productos, responsables, pruebas y aprobaciones. Esto cierra la revisión conjunta, no D2: el entregable continúa `EN CURSO`, B8 sigue diferido y D3 no se inicia.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_D2.md`](trazabilidad/TRZ_D2.md).
