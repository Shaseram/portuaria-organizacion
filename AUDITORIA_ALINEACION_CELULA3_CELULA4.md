# Auditoría de alineación — Célula 3 y Célula 4

> **ACTUALIZACIÓN DE ESTADO.** Las correcciones de alineación ya fueron aplicadas y los cuatro gates están superados. Este archivo conserva el diagnóstico original y sus hallazgos como evidencia histórica; el estado operativo vigente está en [`PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md`](PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md). La base está habilitada para redacción conjunta, no equivale a Subdocumento 4 final ni incluye diagramas entregables.

> **DECISIÓN DE CIERRE APLICADA.** (1) Gobierna la baseline arquitectónica MA8 de C3 —carga y registro consolidado normales en AWS, con núcleo local autónomo que asume autoridad durante el corte—; y (2) la baseline contractual de I1 usa el peak actual de 21,9 GB / 32,5 Mbps / enlaces ≥35 Mbps, mientras 39 GB / 57,8 Mbps queda como escenario futuro 3× y disparador de ampliación.

**Estado del documento:** registro de la auditoría original y fuente de trazabilidad; las correcciones posteriores se gobiernan desde el plan maestro.

**Commit auditado:** `9b460ad9faf6876b677564bcbd884ec1fc22e58e` (`main`, después de `git pull --ff-only`).

**Fecha de corte:** 2026-09-06.
**Resultado original:** `APTO PARA EJECUTAR LA ALINEACIÓN`. **Resultado posterior:** alineación ejecutada y `GATE-01..04` superados; redacción editorial habilitada, no cerrada.

**Plan operativo para aplicar los hallazgos:** [`PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md`](PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md).

---

## 1. Objetivo, alcance y commit auditado

Esta auditoría identifica dependencias, contradicciones, duplicidades y vacíos entre la baseline arquitectónica MA0–MA8 de Célula 3 y los Subdocumentos 5 y 13 de Célula 4. Su propósito original fue preparar correcciones pequeñas y trazables antes de la redacción editorial y de D3.

Durante la auditoría original no se redactó el Subdocumento 4, no se construyeron diagramas, no se promovió ningún ADR y no se modificó ninguna fuente de ambas células. Posteriormente se ejecutaron las correcciones registradas en el plan maestro y se preparó una base técnica de redacción. Los bocetos visuales creados durante esa preparación fueron retirados del consolidado y archivados como referencia no entregable. Se revisaron los Markdown pertinentes. Los `.tex` de Célula 4 se clasificaron como fuentes editoriales/generadas del Subdocumento 13 y no se abrieron, porque el contenido necesario está representado en Markdown. El proyecto LaTeX declarado como fuente del Subdocumento 5 (`Documento terabyte SubDoc 5`) no existe en este repositorio.

### 1.1 Estado Git de partida

| Elemento | Resultado |
|---|---|
| Rama encontrada | `main` |
| Remoto | `origin` → `git@github.com:Shaseram/portuaria-organizacion.git` |
| Árbol antes de actualizar | limpio |
| Diferencia inicial con `origin/main` | local 0 commits adelante, 6 atrás |
| Actualización | fast-forward, sin conflictos |
| Commit base de auditoría | `9b460ad9faf6876b677564bcbd884ec1fc22e58e` |

### 1.2 Alcance material

- C3: gobierno MA0–MA8, frentes A/C/D, trazabilidad, consolidado y T-11.
- C4: índice raíz, Subdocumento 5, comunicados, decisiones y respaldos A00–A08; índice y piezas vigentes del Subdocumento 13.
- Fuente oficial: Bases Técnicas del Caso 06, únicamente para resolver el desacuerdo sobre continuidad y sincronización.
- Fuera de alcance: revisión normativa integral, reescritura de entregables, diagramas finales, costos, pruebas de campo, aprobación de ADR y decisiones de cliente.

### 1.3 Criterio rector acordado para la corrección

1. C3 gobierna arquitectura lógica/física, emplazamiento, continuidad, seguridad, integración, productos de referencia y T-11.
2. C4 gobierna el modelo detallado de datos, diccionario, calidad, linaje, retención y capacidad acumulada.
3. En materias cruzadas se adopta la baseline C3 y se incorpora el detalle C4 que no la contradiga; una diferencia de C4 se registra como propuesta de cambio, no como reemplazo silencioso.
4. La fuente oficial gobierna cuando una célula presenta una elección arquitectónica como requisito contractual.
5. Los estados `PROPUESTO`, `CONDICIONADO`, `VALIDADO` e `IMPLEMENTADO` no son intercambiables.

---

## 2. Resumen ejecutivo

### 2.1 Qué está alineado

- Ambas células sostienen operación local completa durante 72 horas sin enlace, reconciliación posterior, escritor único por dominio/zona/fase, ausencia de pérdida y degradación explícita de funciones externas.
- Son compatibles el enfoque relacional PostgreSQL con extensión temporal, el almacenamiento de objetos para evidencia y archivo, la separación analítica y el uso de eventos/colas con idempotencia y DLQ.
- Coinciden los dominios operativos principales, las 21 contrapartes y 7 familias de integración, la trazabilidad hasta evidencia, los controles de identidad y cifrado, y la necesidad de proteger campos sensibles sin duplicarlos.
- El tamaño local no se contradice si se distinguen conceptos: C3 calcula ≈183 GB útiles requeridos y provisiona ≈960 GB; C4 recomienda un orden de 1 TB útil para borde.
- Los horizontes de C4 —3,6 TB actuales y 9,9 TB a 3× de dato, 6,4/18,1 TB con copias— amplían el cálculo de largo plazo; no sustituyen automáticamente la baseline online de 2,5 TB de C3.

### 2.2 Qué está inconsistente

- C3 ubica el sistema de registro normal en AWS y transfiere autoridad al nodo local durante el corte; C4 elige un primario permanente en el borde y afirma que la alternativa cloud incumple.
- C3 dimensiona el corte al peak estacional actual (21,9 GB y 32,5 Mbps); C4 publica 13 GB actuales y 39 GB/57,8 Mbps a diseño 3×, y además permite que imágenes no esperen la misma prioridad. Falta una tabla común de escenarios y una interpretación compartida de la ventana de 90 minutos.
- C3 llama al `Contenedor` entidad central de su vista conceptual; C4 define `VISITA` como objeto operacional central. Es conciliable solo si se explicita que uno es entidad de negocio y el otro agregado por estadía.
- C3 expresa cuatro capacidades lógicas de datos (`DATA-CORE`, `DATA-TS`, `DATA-DOC`, `DATA-AN`); C4 anuncia tres almacenamientos, aunque su propia solución usa también objetos y finalmente dos familias de motor. La diferencia es taxonómica, pero hoy induce diagramas distintos.
- C4 conserva estados, recuentos y dependencias anteriores a MA8: 78/80 entidades, cuello de botella de ingesta/sincronización, pendientes propios ya cerrados y C3 descrita como nueve secciones inexistentes con ADR candidatos.
- C4 trata `CTX-SIM` como alta cerrada e incorporación al catálogo; C3 solo autorizó su uso provisional, sujeto a ratificación A1/C1 y sin convertirlo en baseline ni fila T-11.

### 2.3 Qué bloquea realmente

1. Resolver la topología de autoridad normal de `DATA-CORE` y registrar la decisión sin alterar artificialmente el estado de los ADR.
2. Congelar una matriz única de capacidad con escenarios, fórmulas y alcance del plazo de 90 minutos; recién después confirmar las filas de nube, almacenamiento y enlaces del T-11.

El mapeo `Contenedor`/`VISITA`, los ocho índices cifrados y la taxonomía de almacenes bloquean el cierre de `V-DATA-01` y de la sección 4.1.4, pero pueden corregirse inmediatamente después de los dos puntos anteriores.

### 2.4 Qué puede quedar condicionado en Informe 1

Pueden declararse como condiciones verificables, sin fingir validación: contratos reales y versiones de interfaces externas; capacidad CDC del TOS; latencia LTE/5G con patio cargado; ancho de banda real de carriers; resolución/compresión de imágenes; catálogo/versiones cloud al congelar oferta; atributos cifrados y mecanismo por campo; custodios y disposición exacta de copias; validación de la metodología de emisiones; y ratificación futura de innovaciones que alteren arquitectura.

### 2.5 Primer bloque de corrección recomendado

Una sesión conjunta C3–C4 debe producir una sola página de decisión con: autoridad normal y durante corte, dirección de réplica, estados de transición, escenario de capacidad contractual, tratamiento de imágenes y alcance de la sincronización ≤90 minutos. Esa página actualiza primero `C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md`, `A05_ALTERNATIVAS_PERSISTENCIA.md`, `A08_ALMACENAMIENTO_ACUMULADO.md` y, si cambian cantidades, las dos fuentes del T-11.

---

## 3. Hallazgos críticos que bloquean la redacción

### AC34-001 — Autoridad operacional normal incompatible

| Campo | Contenido |
|---|---|
| ID | `AC34-001` |
| Severidad | **Crítico** |
| Tema | Arquitectura híbrida, autoridad del dato y emplazamiento |
| Afirmación C3 | `PHY-CLD-05` es el consolidado y sistema de registro fuera del corte; en operación normal la nube es autoridad con réplica local caliente y, durante el corte, la autoridad pasa a `PHY-OPS-01`. |
| Fuente C3 | `Celula3/02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md`, tabla §4 (`PHY-CLD-05`) y §6; `Celula3/90_Consolidado/02_FORMULARIO_T11_FINAL.md`, fila “Plataforma cloud primaria”. |
| Afirmación C4 | El motor relacional primario vive permanentemente en el borde y replica hacia la nube; sostiene que un primario cloud incumple la restricción de 72 h. |
| Fuente C4 | `Célula 4/A05_ALTERNATIVAS_PERSISTENCIA.md`, §§3.1–3.3 y resumen de familia; `Célula 4/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`, §§5.4–5.5 y Anexo G. |
| Fuente oficial | Bases Técnicas del Caso 06, Cap. 15, `RT-03.10` y `RT-03.13`: exigen operación completa local durante 72 h, sin pérdida, y sincronización posterior; no fijan que el primario normal deba residir permanentemente en el borde. |
| Impacto | Produce dos diagramas físicos, dos topologías de réplica, dos modelos de failover y posibles diferencias en T-11, seguridad, RPO y operación. La afirmación de incumplimiento de C4 convierte una elección arquitectónica en requisito contractual sin respaldo textual suficiente. |
| Resolución propuesta | Mantener provisionalmente la baseline MA8 de C3: cloud como sistema de registro normal y réplica local capaz de asumir autoridad. C4 debe reabrir solo `DEC-C4`/alternativa de emplazamiento afectada y puntuar la viabilidad real de transferencia de autoridad, no descartar cloud por definición. Si el equipo prefiere borde primario, debe emitir una decisión conjunta y propagarla a C1/C2/C4/T-11/ADR; no hacer un cambio silencioso. |
| Responsable | Ambas; C3 es propietaria de arquitectura y emplazamiento, C4 de consistencia/persistencia. |
| Estado | **Resolución acordada; propagación pendiente — bloqueante hasta aplicar `C4-02` y verificar `C3-01`** |

### AC34-002 — Capacidad y alcance de la reconciliación no comparten escenario

| Campo | Contenido |
|---|---|
| ID | `AC34-002` |
| Severidad | **Crítico** |
| Tema | Volumetría, enlace WAN, buffer, objetos y T-11 |
| Afirmación C3 | Promedio 72 h: 13,7 GB/20,3 Mbps; peak estacional: 21,9 GB/32,5 Mbps; baseline de cada camino WAN ≥35 Mbps. Supuesto de imagen 500 KB; sensibilidad a 1 MB: ≈40 GB/58 Mbps. |
| Fuente C3 | `Celula3/02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md`, §§2, 4, 5 y 8; `Celula3/90_Consolidado/02_FORMULARIO_T11_FINAL.md`, filas nube, almacenamiento y conectividad. |
| Afirmación C4 | Publica 13 GB/19,3 Mbps “actual” y 39 GB/57,8 Mbps en diseño 3×; declara que las invariantes no esperan a las imágenes durante saturación del enlace. |
| Fuente C4 | `Célula 4/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`, §5.10 y tabla “Buffer de la operación desconectada”; `Célula 4/A08_ALMACENAMIENTO_ACUMULADO.md`. |
| Fuente oficial | Bases Técnicas del Caso 06, Cap. 14.2 exige estimar datos generados durante 72 h y tiempo de sincronización; Cap. 15 `RT-03.13` exige sincronización ≤90 min, sin intervención manual ni pérdida de movimientos/hechos y con resolución determinista. El texto revisado no autoriza explícitamente transferir las imágenes fuera de la ventana ni aclara que todos los bytes deban concluir en ella. |
| Impacto | Un enlace de 35 Mbps es suficiente para la baseline C3 a peak actual, pero no para 57,8 Mbps de C4. La elección afecta T-11, SLA, buffer, pruebas, costos y cualquier promesa de sincronización. |
| Resolución propuesta | Publicar una matriz única con al menos: promedio actual, peak estacional actual, crecimiento 3× y sensibilidad de imagen a 1 MB. Separar claramente crecimiento de transacciones de cambio de tamaño de imagen. Hasta aclaración del cliente, usar como compromiso conservador el peak actual completo de C3 y declarar que el escenario 3× activa ampliación ≥58 Mbps o una política de prioridad expresamente condicionada. No afirmar que la evidencia binaria puede terminar después de 90 min como hecho contractual. |
| Responsable | Ambas; C4 entrega fórmulas/horizontes y C3 fija capacidad física/T-11. |
| Estado | **Resolución acordada; propagación pendiente — bloqueante hasta aplicar `C4-03` y verificar `C3-02`** |

---

## 4. Dependencias Célula 3 → Célula 4

| ID | Qué necesita C3 | Fuente de C4 | Situación | Efecto y corrección mínima |
|---|---|---|---|---|
| `DEP-C3-01` | Dueño y detalle del modelo de datos para cerrar `V-DATA-01` sin duplicarlo | `CONTENIDO_SUBDOCUMENTO_5.md` §§5.2 y 5.14; `A01`; `A02` | Definido, con diferencia semántica | C3 conserva vista arquitectónica compacta; enlaza el modelo detallado C4 y agrega equivalencia `Contenedor` ↔ `VISITA`. |
| `DEP-C3-02` | Dominios, propietarios, productores, consumidores y fuentes de verdad | Subdoc 5 §§5.2–5.3 | Definido con condicionamientos externos | Consumir los diez dominios de C4 y mapearlos a los cuatro almacenes/capacidades y contextos C3. No copiar 80 entidades. |
| `DEP-C3-03` | Retención, archivo y eliminación por clase | Subdoc 5 §5.12; `DEC-C4-02/03/21` | Definido por C4; algunas clases requieren validación cliente | Actualizar `V-DATA-01`, seguridad y respaldo con clases, dejando validación como condición. |
| `DEP-C3-04` | Catálogo campo→sensibilidad→retención para acreditar cifrado de campo | `A02_DICCIONARIO_DE_DATOS.md` y `DEC-C4-12` | Catálogo de 28 campos definido; 8 búsquedas pendientes | D1 debe dejar de decir que el catálogo no existe, incorporarlo por referencia y acordar el mecanismo de los ocho atributos. |
| `DEP-C3-05` | Volumetría detallada, crecimiento y largo plazo | `A08_ALMACENAMIENTO_ACUMULADO.md`; Subdoc 5 §5.13 | Definido, pero no alineado por escenario | Resolver `AC34-002` antes de tocar T-11. Distinguir dato útil, online, archivo, copias y capacidad provisionada. |
| `DEP-C3-06` | Familias de persistencia y necesidades ACID/CAP | `A05`; `A06`; Subdoc 5 §§5.4–5.6 | Mayormente compatible; emplazamiento contradictorio | Conservar PostgreSQL/temporal/objetos/analítica; resolver autoridad normal y normalizar taxonomía. |
| `DEP-C3-07` | Política de calidad, linaje e indicadores | `A03`; Subdoc 5 §5.11 | Definido | Referenciar 54 reglas, 12 indicadores y 12 pruebas como propiedad de C4; C3 solo aporta controles/observabilidad. |
| `DEP-C3-08` | Método de emisiones y datos que alimentan `CTX-EMIS` | `DEC-C4-01`; Subdoc 5 dominios y diccionario | Definido como propuesta, pendiente verificador/cliente | C3 modela el flujo por movimientos ejecutados, sin presentar la metodología como validada. |
| `DEP-C3-09` | Decidir si innovaciones agregan componentes o filas T-11 | Subdoc 13 `B05`, `B11` | `CTX-SIM` solo condicionado | No incluir `CTX-SIM` en baseline/figuras/T-11 hasta ratificación A1/C1 y dimensionamiento; puede citarse como extensión futura sin autoridad. |
| `DEP-C3-10` | Alcance de objetos/evidencias dentro de la ventana de sincronización | Subdoc 5 §5.10; `PEN-18` | Ausente/condicionado | Formular política conjunta de captura, compresión, prioridad y completitud antes de cerrar enlace y pruebas. |

### Lectura de la dependencia

C4 ya entregó más de lo que los archivos antiguos de C3 reconocen: modelo detallado, diccionario, catálogo de 28 campos, retenciones, calidad y capacidad de largo plazo. La corrección de C3 no es copiar ese contenido, sino sustituir referencias “pendiente/por entregar” por referencias recibidas, validar las colisiones y mantener la propiedad editorial.

---

## 5. Dependencias Célula 4 → Célula 3

| ID | Qué usa o pide C4 | Fuente vigente de C3 | Situación | Ajuste necesario en C4 |
|---|---|---|---|---|
| `DEP-C4-01` | `PEN-01`: zonas y fases de autoridad | `A3_PROCESOS_CRITICOS_Y_TOS.md` y modelo A1; cierre MA8 | Definido | Marcar recibido y transcribir solo la tabla de equivalencia: bloque no migrado, validación paralela y postcorte; no mantenerlo como pendiente C3. |
| `DEP-C4-02` | `PEN-02`: búsquedas sobre ocho campos cifrados | D1 §B4.3, especialmente reglas de índices derivados/identificadores sustitutos | Parcial/condicionado | C3 entregó patrón, no decisión por atributo. Mantener abierto solo el dictamen de los ocho campos y eliminar la afirmación de ausencia total. |
| `DEP-C4-03` | `PEN-03`: quién publica modelo conceptual | README/MA7: Subdoc 4 publica `V-DATA-01`; Subdoc 5 es dueño del detalle | Definido | Cerrar el pendiente con esa regla y tabla de equivalencia; resolver centralidad semántica. |
| `DEP-C4-04` | `PEN-06`: eventos, DLQ, reproceso, réplica/CDC | `A2_ARQUITECTURA_DE_INTEGRACION.md`; `ADR-003 PROPUESTO` | Patrón definido; CDC/TOS condicionado | Marcar diseño propuesto, separar EventBridge/SQS de réplica/CDC y conservar como externo solo lo que requiere interfaz real. |
| `DEP-C4-05` | `PEN-07`: productos/versiones | C2 §4 y T-11 | Productos de referencia definidos; versiones condicionadas | Consumir AWS/RDS PostgreSQL/temporal/S3/EventBridge/SQS/Athena/Glue como baseline propuesta; dejar versión mayor LTS al congelamiento. |
| `DEP-C4-06` | `PEN-07b`: emplazamiento | C1 §§4–6 | Definido por C3 pero contradictorio con C4 | Resolver `AC34-001`; C4 no puede declarar su topología como hecho superior. |
| `DEP-C4-07` | `PEN-08`: 18 dimensiones | C4 de Frente Físico §§2–8 | Revalidadas; 15 confirmadas y 3 corregidas | Consumir 13,7/21,9 y 20,3/32,5 como escenarios actuales; conservar 3× como escenario de crecimiento separado. |
| `DEP-C4-08` | `PEN-10`: límite del runtime local | A1 §3.1/§4.1 y tabla `EDGE-RUN` | Definido | Cerrar inventario lógico, sin convertir `EDGE-RUN` en copia total de nube. |
| `DEP-C4-09` | `PEN-17`: red del patio y WAN | C3 despliegue/red; T-11 | Tecnología y piso de capacidad propuestos; mediciones pendientes | Usar LTE/5G privada, 2 rutas/proveedores y 35 Mbps para peak actual; mantener latencia/site survey y escenario 58 Mbps condicionados. No incorporar un tercer enlace sin una decisión posterior. |
| `DEP-C4-10` | `PEN-18`: política de imágenes | C4 dimensional de C3 §8 | Supuesto 500 KB y sensibilidad 1 MB; política real ausente | Mantener pendiente conjunto y declarar que resolución/compresión dependen del equipo OCR y aceptación. |
| `DEP-C4-11` | `PEN-19`: 3-2-1-1-0 | C2 §§5–6; T-11 custodia, S3 Object Lock y clave separada | Patrón definido; asignación de copias por clase incompleta | Sustituir “sin respuesta” por “patrón propuesto”; pedir únicamente la matriz copia/medio/ubicación/inmutabilidad por clase. |
| `DEP-C4-12` | Contratos de integración de §5.8 | A2: catálogo de 21 contrapartes + 7 familias, patrones y campos de contrato | Diseño suficiente para I1; protocolos reales bloqueados externos | Completar §5.8 como propuesta con contratos tipo y marcar interfaces reales/versions como condicionadas, no declarar todo el apartado vacío. |
| `DEP-C4-13` | `CTX-SIM` para IN-03 | Respuesta de coordinación §5 | Aceptación provisional, no alta de catálogo | Cambiar “RESUELTO/cerrado” por “CONDICIONADO A RATIFICACIÓN A1/C1”; no exigir inserción en Subdoc 4 aún. |
| `DEP-C4-14` | STRIDE de IN-01/IN-03 | D2 y respuesta de coordinación | Posterior al I1; C4 debe dar insumos | Mantener como trabajo posterior y entregar activos/datos/interfaces/flujo cuando se refine. |

---

## 6. Contradicciones y duplicidades

### AC34-003 — `Contenedor` y `VISITA` compiten como objeto central

| Campo | Contenido |
|---|---|
| ID | `AC34-003` |
| Severidad | Alto |
| Tema | Modelo conceptual y vocabulario |
| Afirmación C3 | “El Contenedor es la entidad central del dominio”; además usa “Visita de Nave”, que no equivale necesariamente a la estadía de un contenedor. |
| Fuente C3 | `Celula3/01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`, §5 y lectura del diagrama. |
| Afirmación C4 | `DEC-C4-07`: `VISITA` —una permanencia del contenedor en el terminal— es el objeto operacional central y contiene movimientos, posición, hechos y emisiones. |
| Fuente C4 | `Célula 4/A00_REGISTRO_DECISIONES_CELULA4.md`, `DEC-C4-07`; Subdoc 5, diccionario `CONTENEDOR`, `VISITA`, `MOVIMIENTO` y `POSICION_VIGENTE`. |
| Fuente oficial | No necesaria; es una decisión de modelado derivada de reglas y volumetría. |
| Impacto | Puede generar claves, eventos y diagramas incompatibles, y confundir “visita de nave” con “visita del contenedor”. |
| Resolución propuesta | Declarar `Contenedor` como maestro/activo de negocio reutilizable y `VisitaContenedor` como agregado operacional por estadía. Reservar `Recalada` o `VisitaNave` para la nave. C3 actualiza solo su modelo de alto nivel y eventos; C4 conserva el detalle. |
| Responsable | Ambas |
| Estado | Abierto |

### AC34-004 — Tres almacenamientos, cuatro capacidades y dos motores

| Campo | Contenido |
|---|---|
| ID | `AC34-004` |
| Severidad | Alto |
| Tema | Taxonomía de datos y diagramas |
| Afirmación C3 | Cuatro capacidades lógicas: transaccional, series, documentos/evidencia y analítica (`DATA-CORE/TS/DOC/AN`). |
| Fuente C3 | A1 catálogo lógico; D1 §B4; C2 tabla de tecnologías. |
| Afirmación C4 | Declara tres almacenamientos —transaccional, temporal y analítico—, pero evalúa también documentos/evidencia e histórico sobre objetos y concluye “dos motores, no cinco”. |
| Fuente C4 | Subdoc 5 §5.6; `A05_ALTERNATIVAS_PERSISTENCIA.md`, resumen. |
| Fuente oficial | No necesaria. |
| Impacto | Los diagramas y la narrativa pueden contar 3, 4 o 5 elementos para la misma solución. |
| Resolución propuesta | Adoptar tres niveles de vocabulario: cuatro capacidades lógicas; cinco familias de persistencia si se separa histórico; dos familias de motor (PostgreSQL y objetos). La obligación de separación operacional/analítica se conserva. |
| Responsable | Ambas |
| Estado | Abierto |

### AC34-005 — Catálogo de cifrado recibido pero no incorporado

| Campo | Contenido |
|---|---|
| ID | `AC34-005` |
| Severidad | Alto |
| Tema | Seguridad, desempeño y trazabilidad de campos |
| Afirmación C3 | D1 propone cifrado de campo y búsquedas mediante identificadores sustitutos, índices derivados o servicios autorizados; aún dice que Subdoc 5 entregará el catálogo final. |
| Fuente C3 | `D1_ARQUITECTURA_DE_SEGURIDAD.md`, §§B4.1–B4.3 y pendientes de B4. |
| Afirmación C4 | Identifica 28 atributos cifrables y ocho claves de acceso cuya búsqueda por igualdad debe resolverse. |
| Fuente C4 | `A00...`, `DEC-C4-12`/`PEN-02`; `A02_DICCIONARIO_DE_DATOS.md`; Subdoc 5 §5.10. |
| Fuente oficial | No necesaria para la colisión; ambos citan los requisitos de seguridad y desempeño. |
| Impacto | No puede acreditarse 100 % de cobertura ni garantizar búsquedas ≤1 s sin decidir índice/tokenización por atributo. |
| Resolución propuesta | D1 marca el catálogo como recibido y ambas células añaden una tabla de ocho filas: necesidad de igualdad, exposición admisible, mecanismo, propietario de clave, prueba y estado. |
| Responsable | Ambas |
| Estado | Abierto |

### AC34-006 — Fuente canónica de C4 ausente y copias idénticas

| Campo | Contenido |
|---|---|
| ID | `AC34-006` |
| Severidad | Alto |
| Tema | Gobierno documental |
| Afirmación C3 | Su README define rutas canónicas presentes en el repositorio y un único destino de redacción. |
| Fuente C3 | `Celula3/README.md`, §§3–6. |
| Afirmación C4 | Los índices declaran que la fuente de verdad del Subdoc 5 es un proyecto LaTeX externo/no versionado; simultáneamente existen copias idénticas A00–A08 en tres ubicaciones y comunicados/diagramas duplicados. |
| Fuente C4 | `Célula 4/00_INDICE.md`; `Célula 4/Subdocumento_5/00_INDICE.md`; comparación de hashes del commit auditado. |
| Fuente oficial | No aplica. |
| Impacto | No existe una ruta de edición reproducible en `main`; una corrección puede aplicarse a una copia y perderse al recompilar. |
| Resolución propuesta | Antes de editar contenido, C4 debe designar una ruta canónica versionada. Recomendación mínima: `Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md` como lectura/revisión canónica de I1 y una sola carpeta A00–A08 como evidencia; documentar el mecanismo de regeneración. No borrar duplicados durante esta auditoría. |
| Responsable | C4 |
| Estado | Abierto |

### AC34-007 — Estado de C3 y pendientes de C4 están obsoletos

| Campo | Contenido |
|---|---|
| ID | `AC34-007` |
| Severidad | Alto |
| Tema | Trazabilidad y estado de dependencias |
| Afirmación C3 | MA0–MA8 están completadas como preparación; 11 ADR `PROPUESTO`, 0 aprobados; componentes, zonas, capacidad y T-11 ya tienen baseline. |
| Fuente C3 | `Celula3/README.md`; MA7/MA8; registro ADR. |
| Afirmación C4 | Subdoc 5 §estado dice que nueve secciones C3 siguen “pendiente de integrar” y los ADR son candidatos; mantiene `PEN-01/03/07/08/10/17/19` como si no hubiera respuesta. |
| Fuente C4 | `CONTENIDO_SUBDOCUMENTO_5.md`, §§estado y Anexo F/G; `Comunicados/02_SOLICITUD_A_CELULA_3.md`. |
| Fuente oficial | No aplica. |
| Impacto | El Subdoc 5 parece provisional por información ya disponible y no distingue vacío externo de colisión real. |
| Resolución propuesta | Ejecutar una pasada de estados: `RECIBIDO`, `RECIBIDO CON CONFLICTO`, `CONDICIONADO EXTERNO` o `CERRADO I1`. No convertir `PROPUESTO` en aprobado. |
| Responsable | C4 con confirmación C3 |
| Estado | Abierto |

### AC34-008 — Trazas internas de C4 contradicen su propio cuerpo

| Campo | Contenido |
|---|---|
| ID | `AC34-008` |
| Severidad | Alto |
| Tema | Consistencia editorial y evidencia |
| Afirmación C3 | Usa la sincronización como cuello de botella de capacidad y espera un único valor trazable por artefacto. |
| Fuente C3 | C4 dimensional de Frente Físico y T-11. |
| Afirmación C4 | El cuerpo/`DEC-C4-20` identifica sincronización, pero Anexo G aún dice ingesta de series; el cuerpo afirma 80 entidades mientras una justificación dice 78; calidad y diccionario figuran completados en el resumen pero pendientes en la traza. Aparece además `PendienteTres`. |
| Fuente C4 | `CONTENIDO_SUBDOCUMENTO_5.md`, §§estado, 5.10, Anexo G y diccionario; `A05`; `A07`. |
| Fuente oficial | No aplica. |
| Impacto | Invalida búsquedas automáticas, conteos de cobertura y confianza en estados; puede arrastrar datos históricos al Subdoc 4. |
| Resolución propuesta | Corregir solo las ocurrencias canónicas tras `AC34-006`: 80 entidades totales/78 relacionales si ese es el reparto; sincronización como cuello vigente; estados de calidad/diccionario completados; normalizar `PendienteTres`. |
| Responsable | C4 |
| Estado | Abierto |

### AC34-009 — `CTX-SIM` aparece cerrado antes de ratificación arquitectónica

| Campo | Contenido |
|---|---|
| ID | `AC34-009` |
| Severidad | Alto |
| Tema | Innovación, alcance I1 y catálogo de componentes |
| Afirmación C3 | `CTX-SIM` puede plantearse provisionalmente en nube, sin autoridad; A1/C1 deben ratificar componente y emplazamiento. Solo generaría T-11 si se oferta capacidad/licencia separada. |
| Fuente C3 | `Celula3/00_Gobierno/06_RESPUESTA_COORDINACION_SUBDOC5_INNOVACIONES.md`, §5. |
| Afirmación C4 | `B11` marca el alta como resuelta/cerrada y `B05` afirma que se incorpora al catálogo del Subdoc 4. |
| Fuente C4 | `Subdoc13/B11_PENDIENTES_POR_CELULA.md`, filas 3 y 6; `Subdoc13/B05_IN03_GEMELO_DE_OPERACION.md`, “Forma de implementación”. |
| Fuente oficial | No necesaria. |
| Impacto | Convierte una innovación condicionada en componente de baseline y podría forzar diagrama/T-11 sin capacidad ni ADR. |
| Resolución propuesta | Sustituir “cerrado/se incorpora” por “candidato condicionado a ratificación A1/C1; fuera de autoridad operacional; sin fila T-11 salvo oferta separada”. |
| Responsable | C4; ratificación futura C3 |
| Estado | Abierto, no bloquea I1 si se condiciona |

### AC34-010 — Estados `APROBADO` tienen alcances distintos

| Campo | Contenido |
|---|---|
| ID | `AC34-010` |
| Severidad | Medio |
| Tema | Gobierno de decisiones |
| Afirmación C3 | Ningún ADR está aprobado; `PROPUESTO` es baseline seleccionada pero no aceptación del cliente. |
| Fuente C3 | Registro ADR §2 y README. |
| Afirmación C4 | El índice de Subdoc 13 marca textos `APROBADO`; el registro de datos llama “cerradas” a 21 decisiones. |
| Fuente C4 | `Subdoc13/00_INDICE_SUBDOCUMENTO_13.md`, regla de estados; `A00_REGISTRO_DECISIONES_CELULA4.md`, §Cómo se lee. |
| Fuente oficial | No aplica. |
| Impacto | Un ensamblador puede interpretar aprobación editorial como decisión arquitectónica o aceptación contractual. |
| Resolución propuesta | Mantener los estados pero añadir siempre el ámbito: `APROBADO PARA INTEGRACIÓN EDITORIAL C4`, `DECIDIDO POR C4` o `CONDICIONADO A ARQUITECTURA/CLIENTE`. |
| Responsable | C4 |
| Estado | Abierto |

### AC34-011 — C3 conserva dependencias de datos ya recibidas

| Campo | Contenido |
|---|---|
| ID | `AC34-011` |
| Severidad | Medio |
| Tema | Actualización de referencias C3 |
| Afirmación C3 | D1 y otras trazas indican que Subdoc 5 “entrega” a futuro campos, propietario, sensibilidad y retención. |
| Fuente C3 | `D1_ARQUITECTURA_DE_SEGURIDAD.md`, §§B4 y pendientes; matrices/trazas relacionadas. |
| Afirmación C4 | El diccionario de 80 entidades/451 atributos, el catálogo de 28 campos y las clases de retención ya existen. |
| Fuente C4 | `A02`; `A00 DEC-C4-02/03/12`; Subdoc 5 §§5.12–5.14. |
| Fuente oficial | No aplica. |
| Impacto | C3 puede omitir cruces ya posibles y describir como vacío lo que en realidad requiere validación. |
| Resolución propuesta | Cambiar “pendiente de entrega” por “recibido, pendiente de contraste/validación” y enlazar fuentes C4. |
| Responsable | C3 |
| Estado | Abierto |

### AC34-012 — Cobertura 3-2-1-1-0 no está asignada por clase de dato

| Campo | Contenido |
|---|---|
| ID | `AC34-012` |
| Severidad | Medio |
| Tema | Respaldo, inmutabilidad y capacidad |
| Afirmación C3 | Define 3-2-1-1-0, S3 Object Lock, clave separada, custodia externa y prueba mensual de restauración. |
| Fuente C3 | C2 §§5–6; T-11 filas de nube/custodia/claves. |
| Afirmación C4 | Calcula capacidad con copias, pero mantiene `PEN-19` sobre cuántas, dónde y con qué inmutabilidad. |
| Fuente C4 | `A08`; `A00 PEN-19`; Subdoc 5 §5.12. |
| Fuente oficial | No necesaria para la brecha; la exigencia ya está trazada en ambas. |
| Impacto | Riesgo de doble conteo o de dejar una clase sin copia/inmutabilidad; afecta 6,4/18,1 TB. |
| Resolución propuesta | Crear matriz de clases con original, copia 2, copia 3, medios, sitio, inmutabilidad/offline, clave y prueba; después recalcular capacidad una sola vez. |
| Responsable | Ambas |
| Estado | Condicionado |

### AC34-013 — Integración está diseñada para I1, pero no contratada ni validada

| Campo | Contenido |
|---|---|
| ID | `AC34-013` |
| Severidad | Medio |
| Tema | Interoperabilidad, contratos y alcance |
| Afirmación C3 | Cataloga 21 contrapartes/7 familias, contratos tipo, eventos, reintentos y fallos; varias interfaces reales siguen `POR LEVANTAR` o `BLOQUEADO EXTERNO`. |
| Fuente C3 | `A2_ARQUITECTURA_DE_INTEGRACION.md`; A3; trazas de Frente 1. |
| Afirmación C4 | Marca §5.8 entero pendiente de C3 y pide contratos definitivos/CDC. |
| Fuente C4 | Subdoc 5 tabla de estados y §5.8; `PEN-06`. |
| Fuente oficial | No necesaria para clasificar el estado. |
| Impacto | O bien se deja incompleto un apartado que puede redactarse como diseño, o se inventan protocolos/versiones de terceros. |
| Resolución propuesta | C4 completa §5.8 con patrones y catálogo C3 en estado `PROPUESTO`; marca por contraparte los detalles externos. Contratos OpenAPI/AsyncAPI ejecutables y pruebas quedan posteriores. |
| Responsable | Ambas |
| Estado | Condicionado; no bloquea I1 |

### AC34-014 — No existe decisión formal sobre un tercer enlace

| Campo | Contenido |
|---|---|
| ID | `AC34-014` |
| Severidad | Bajo |
| Tema | Red y alcance T-11 |
| Afirmación C3 | Dos WAN con proveedores y rutas físicas distintas constituyen la baseline. No existe una decisión formal para un tercer enlace. |
| Fuente C3 | C3 despliegue/red, MA5 y T-11. |
| Afirmación C4 | Sus dependencias piden capacidad del enlace, sin necesidad de imponer tecnología; materiales históricos pueden sugerir alternativas. |
| Fuente C4 | `PEN-17` y estrategia de capacidad. |
| Fuente oficial | No aplica. |
| Impacto | Riesgo de añadir costo/compromiso no aceptado al T-11 al resolver capacidad. |
| Resolución propuesta | Toda actualización debe conservar dos proveedores y rutas físicas distintas como baseline. Un tercer enlace solo puede incorporarse mediante una decisión posterior trazable y su dimensionamiento. |
| Responsable | Ambas |
| Estado | Resuelto por baseline C3; control de no regresión |

---

## 7. Definiciones compatibles y reutilizables

| Tema | Definición común reutilizable | Fuente primaria recomendada |
|---|---|---|
| Continuidad | Cinco funciones críticas completas durante 72 h; equipos de patio hasta 8 h sin radio; sin pérdida y con reconciliación determinista | C3 A1/A3/C1/C3; C4 Subdoc 5 §5.5 |
| DR | Escenario distinto del corte WAN: activo-pasivo, RTO ≤4 h y RPO ≤15 min | C3 ADR-007/011, C2/C3 |
| Autoridad TOS | Escritor único por dominio × zona × fase; transferencia secuenciada e idempotente | C3 A3; C4 Subdoc 5 §5.3 |
| Datos | Diez dominios C4 mapeados a contextos C3; detalle de 80 entidades permanece en Subdoc 5 | C4 A01/A02 + tabla de equivalencia conjunta |
| Persistencia | PostgreSQL relacional, extensión temporal y objetos; analítica aislada del operacional | C3 C2; C4 A05/A06 |
| Integración | 21 contrapartes, 7 familias, eventos/colas, idempotencia, DLQ y contratos versionados | C3 A2; C4 §5.8 consume |
| Evidencia | Hechos facturables, actos firmados y datos de cadena de frío deben conservar vínculo reproducible con su origen | C3 A1/D1; C4 §§5.11–5.12 |
| Identidad | Gobierno común, mínimo privilegio y capacidad local para identidades vigentes durante corte | C3 A1/D1/T-11; C4 dominio acceso/identidad |
| Telemetría | Captura local y reporte agregado, sin convertir el SIEM en autoridad operacional | C3 A1/D1/C2; C4 §§5.7/5.10 |
| Emisiones | Atribución propuesta por movimientos ejecutados, con versión de algoritmo y validación externa pendiente | C4 `DEC-C4-01`; C3 `CTX-EMIS` |
| Nube | AWS `sa-east-1` multi-AZ y DR `us-east-1`, estados propuestos y verificaciones pendientes | C3 ADR-011/T-11 |
| Red | LTE/5G privada propuesta; dos WAN de carrier/ruta diferentes; medición pendiente | C3 C3/T-11 |

---

## 8. Pendientes legítimos del Informe 1

No son defectos mientras se formulen como supuestos o condiciones con responsable y prueba:

1. Interfaces reales, autenticación, versión de protocolo y capacidad CDC de TOS, ERP, navieras, autoridades, ferrocarril, concesionaria y equipos.
2. Site survey de LTE/5G: cobertura, handover, latencia y cantidad final de 6–8 estaciones base.
3. Capacidad contratada y conmutación efectiva de cada WAN; 35 Mbps es baseline de diseño actual, no medición del sitio.
4. Resolución, compresión, frecuencia y retención de imágenes OCR; 500 KB es supuesto, 1 MB una sensibilidad.
5. Decisión por cada uno de los ocho campos cifrados e indexados.
6. Validación del CLIENTE/verificador de la metodología de emisiones y de las clases propias de retención.
7. Versiones mayores de productos, catálogo regional, certificaciones, residencia, carbono y latencia al congelar la oferta.
8. Matriz final de copias, custodios de clave, rotación y prueba de restauración del 3-2-1-1-0.
9. Ratificación de `CTX-SIM` y cualquier término de emisiones en asignación de patio; pueden describirse como innovación condicionada.
10. Funciones externas no disponibles durante el corte y sus procedimientos de contingencia por contraparte.

---

## 9. Elementos que corresponden a entregas posteriores

| Elemento | Entrega/hito posterior | Tratamiento en I1 |
|---|---|---|
| OpenAPI/AsyncAPI definitivos y pruebas de contrato | Refinamiento/implementación | Patrón, inventario y condición externa |
| Site survey, medición RF y prueba de carrier | Diseño detallado/aceptación | Método, rango y criterio de cierre |
| Simulacro real 72 h, reposición ≤90 min y pruebas DR | Pruebas/aceptación | Escenario y criterio, no evidencia ejecutada |
| Benchmarks de cifrado e índices | Diseño/pruebas | Alternativa y umbral |
| Compra/contratación de productos y enlaces | Ejecución contractual | T-11 como especificación ofertada |
| STRIDE detallado de innovaciones | Refinamiento cuando cambien arquitectura/seguridad | Dependencia e insumos |
| EDT, cronograma detallado y nivelación | Informe 2 | Hipótesis declarada |
| T-19 completo y madurez final de innovaciones | Propuesta final | Idea, tecnología, alcance e investigación adicional |
| Costos, flujo de caja y valorización | Informe 3 | Inductores cualitativos, sin precio |
| Operación productiva de IN-05 | Etapa 2/meses definidos | Prototipo/prevalidación si corresponde; no implementación actual |

---

## 10. Matriz de acciones quirúrgicas

| ID | Prioridad | Propietario | Archivos afectados | Dependencias | Resultado esperado | Criterio verificable de cierre |
|---|---:|---|---|---|---|---|
| `ACT-01` | P0 | Ambas | C3 `C1...`; C4 `A05...`, `CONTENIDO...` | `AC34-001` | Una topología normal/corte/retorno | Mismo primario, dirección de réplica y autoridad en los tres archivos; ADR sigue `PROPUESTO` salvo evidencia formal. |
| `ACT-02` | P0 | Ambas | C3 `C4...`, T-11 trabajo/final; C4 `A08...`, `CONTENIDO...` | `AC34-002` | Matriz común de cuatro escenarios y política de imágenes | Los valores 13,7/21,9/39/≈40 y 20,3/32,5/57,8/≈58 aparecen con etiqueta/fórmula inequívoca; T-11 coincide con el escenario comprometido. |
| `ACT-03` | P1 | C4 | `00_INDICE.md`, `Subdocumento_5/00_INDICE.md` | `AC34-006` | Ruta canónica versionada | Un índice identifica exactamente qué archivo se edita y cómo se regenera; copias quedan explícitamente “no editar”. |
| `ACT-04` | P1 | Ambas | C3 A1/MA7; C4 A00/A01/A02/Subdoc 5 | `AC34-003/004` | Glosario y tabla de equivalencia | `Contenedor`, `VisitaContenedor`, `Recalada/VisitaNave`, 4 capacidades y 2 motores tienen un solo significado. |
| `ACT-05` | P1 | Ambas | C3 D1; C4 A02/A03/A00 | `AC34-005` | Dictamen de ocho búsquedas cifradas | Ocho filas con mecanismo, fuga evaluada y prueba; D1 referencia los 28 campos recibidos. |
| `ACT-06` | P1 | C4 | Subdoc 5, Anexo F/G, comunicados 00/02 | `AC34-007/008` | Dependencias y trazas vigentes | Ningún pendiente resuelto por MA8 figura ausente; 78/80 y cuello de botella son coherentes; no existe `PendienteTres`. |
| `ACT-07` | P1 | Ambas | C3 A2; C4 §5.8 y `PEN-06` | `AC34-013` | §5.8 redactable y honesto | Patrones C3 se marcan propuestos; cada detalle externo conserva `POR LEVANTAR/BLOQUEADO EXTERNO`. |
| `ACT-08` | P2 | Ambas | C3 C2/T-11; C4 A08/§5.12 | `AC34-012` | Matriz de copias por clase | 3 copias, 2 medios, off-site, inmutable/offline y prueba están asignados sin doble conteo. |
| `ACT-09` | P2 | C4 | Subdoc13 B05/B11/índice | `AC34-009/010` | Innovaciones sin promoción artificial | `CTX-SIM` queda condicionado y `APROBADO` se identifica como editorial, no ADR/aceptación. |
| `ACT-10` | P2 | C3 | D1, MA8, consolidado/checklist | `AC34-011` | Referencias de datos actualizadas | Todas las menciones a catálogo ausente pasan a recibido/por validar con enlace C4. |
| `ACT-11` | P3 | C4 | Fuente canónica definida por ACT-03 | `AC34-008` | Limpieza editorial puntual | Tablas duplicadas, encabezados repetidos y erratas corregidos sin alterar decisiones. |
| `ACT-12` | P3 | Ambas | Trazas/checklists | Todas | Control de no regresión | Búsqueda confirma 72 h, 90 min, RTO/RPO, AWS, dos WAN sin tercer enlace y 0 ADR aprobados consistentes. |

### Archivos que debería corregir cada célula

**Célula 3, mínimo:**

- `Celula3/01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`
- `Celula3/01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md` — solo si el cruce revela cambios de estado
- `Celula3/02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md`
- `Celula3/02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md`
- `Celula3/03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md`
- `Celula3/00_Gobierno/12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md` o una tabla de equivalencia enlazada desde allí
- `Celula3/90_Consolidado/01_T11_TRABAJO_TRAZABLE.md` y `02_FORMULARIO_T11_FINAL.md` solo si cambia la baseline cuantitativa/topológica

**Célula 4, mínimo:**

- `Célula 4/00_INDICE.md`
- `Célula 4/Subdocumento_5/00_INDICE.md`
- la copia canónica que C4 designe de `A00_REGISTRO_DECISIONES_CELULA4.md`, `A05_ALTERNATIVAS_PERSISTENCIA.md` y `A08_ALMACENAMIENTO_ACUMULADO.md`
- `Célula 4/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`
- la copia canónica de `Comunicados/00_PENDIENTES_CELULA4.md` y `02_SOLICITUD_A_CELULA_3.md`
- `Célula 4/Subdoc13/B05_IN03_GEMELO_DE_OPERACION.md`
- `Célula 4/Subdoc13/B11_PENDIENTES_POR_CELULA.md`
- `Célula 4/Subdoc13/00_INDICE_SUBDOCUMENTO_13.md`

---

## 11. Plan maestro de alineación

### Bloque 0 — Fijar la ruta de edición

- **Prioridad:** P0 administrativa.
- **Propietario:** C4.
- **Entrada:** índices C4 y copias existentes.
- **Acción:** designar fuente canónica versionada y marcar duplicados como solo lectura/históricos.
- **Salida:** ningún agente necesita adivinar qué archivo corregir.
- **Cierre:** una sola ruta editable por artefacto, visible desde `Célula 4/00_INDICE.md`.

### Bloque 1 — Resolver autoridad y réplica

- **Prioridad:** P0 técnica.
- **Propietario:** C3 lidera; C4 valida consistencia.
- **Entrada:** `AC34-001`, C3 C1/C2/ADR-002/007/011 y C4 A05/A06.
- **Acción:** decidir estado normal, corte, reconexión, conflicto y retorno; registrar consecuencias.
- **Salida:** una topología coherente reutilizable en Subdocs 4 y 5.
- **Cierre:** no hay ocurrencias canónicas de “primario cloud” y “primario borde” aplicadas al mismo estado; ADR conservan su estado correcto.

### Bloque 2 — Congelar escenarios de capacidad

- **Prioridad:** P0 técnica/contractual.
- **Propietario:** C4 de datos calcula; C3 de arquitectura dimensiona/T-11.
- **Entrada:** `AC34-002`, supuestos 500 KB/1 MB, peak y 3×.
- **Acción:** tabla de escenarios, fórmula, alcance del 90 min, tráfico concurrente, margen y disparador de ampliación.
- **Salida:** una baseline I1 y sensibilidades explícitas.
- **Cierre:** T-11, C3 C4 y C4 A08 dan el mismo piso de enlace para el mismo escenario.

### Bloque 3 — Cerrar `V-DATA-01`

- **Prioridad:** P1.
- **Propietario:** ambas.
- **Entrada:** `AC34-003/004`, A1 C3, A01/A02 C4.
- **Acción:** acordar nombres y alcance; mapear diez dominios a contextos y cuatro capacidades sin copiar el diccionario.
- **Salida:** tabla arquitectónica con dominio, autoridad, flujo, almacén, protección, retención y dueño del detalle.
- **Cierre:** cada fila enlaza C4 y no existe entidad con dos nombres sin equivalencia.

### Bloque 4 — Cerrar seguridad de campos

- **Prioridad:** P1.
- **Propietario:** D1 C3 + Datos C4.
- **Entrada:** 28 campos/8 accesos y patrón de cifrado C3.
- **Acción:** dictamen por campo e índice, con prueba de latencia y exposición.
- **Salida:** catálogo de protección referenciado, no duplicado.
- **Cierre:** 28/28 clasificados y 8/8 búsquedas con mecanismo o condición.

### Bloque 5 — Actualizar estados e integración

- **Prioridad:** P1.
- **Propietario:** C4, con respuestas C3.
- **Entrada:** MA8, A2/A3, `PEN-*` y anexos C4.
- **Acción:** cerrar solicitudes ya respondidas, completar §5.8 como propuesta y aislar datos externos.
- **Salida:** matriz de dependencias realista.
- **Cierre:** “pendiente C3” solo aparece donde falta una decisión o dato concreto.

### Bloque 6 — Encapsular innovaciones

- **Prioridad:** P2.
- **Propietario:** C4; C3 ratifica solo si se incorpora.
- **Entrada:** `AC34-009/010`.
- **Acción:** ajustar verbos y estados de `CTX-SIM`, IN-05 y STRIDE.
- **Salida:** Subdoc 13 describe valor futuro sin reescribir la baseline MA8.
- **Cierre:** ninguna innovación aparece como implementada, aprobada por arquitectura o cuantificada en T-11 sin decisión.

### Bloque 7 — Control final de alineación

- **Prioridad:** P2.
- **Propietario:** ambas; D3 verifica C3.
- **Entrada:** archivos corregidos.
- **Acción:** búsqueda cruzada de cifras, estados, nombres, ubicaciones, retenciones y enlaces.
- **Salida:** autorización para redacción y figuras.
- **Cierre:** `AC34-001/002` resueltos; altos resueltos o condicionados con dueño; D3 puede ejecutar sobre el ensamblado.

---

## 12. Criterios de cierre

La alineación está lista para pasar a redacción cuando se cumplan todos estos criterios:

- [ ] Existe una sola autoridad operacional declarada para régimen normal, corte y retorno.
- [ ] La dirección de réplica y los términos “primario”, “réplica caliente” y “sistema de registro” significan lo mismo en ambos subdocumentos.
- [ ] Existe una tabla única de escenarios de 72 h y cada cifra indica promedio/peak/crecimiento/sensibilidad.
- [ ] El T-11 usa el escenario acordado y conserva las condiciones de medición/aceptación.
- [ ] La ventana ≤90 min declara qué datos comprende y qué tratamiento condicionado reciben los objetos, sin inventar una interpretación contractual.
- [ ] `V-DATA-01` mapea los diez dominios C4, las cuatro capacidades C3 y el dueño del detalle.
- [ ] `Contenedor`, `VisitaContenedor` y `Recalada/VisitaNave` no se confunden.
- [ ] Los 28 campos sensibles están referenciados y los ocho campos de búsqueda tienen resolución o condición.
- [ ] C4 reconoce las respuestas MA8 y conserva como externos solo datos realmente no disponibles.
- [ ] §5.8 distingue diseño propuesto de contratos/protocolos confirmados.
- [ ] `CTX-SIM` e IN-05 no aparecen como baseline implementada o aprobada.
- [ ] Los 11 ADR siguen `PROPUESTO` y 0 `APROBADO`, salvo nueva evidencia formal posterior a esta auditoría.
- [ ] AWS `sa-east-1`/`us-east-1`, 72 h, 8 h, RTO/RPO, dos WAN y LTE/5G permanecen coherentes; no se agregó un tercer enlace.
- [ ] C4 tiene una fuente canónica versionada y los duplicados no son rutas activas de edición.
- [ ] Conteos y trazas internas de C4 coinciden con el cuerpo vigente.

---

## 13. Inventario y fuentes consultadas

### 13.1 Clasificación de fuentes Célula 3

| Ruta o conjunto | Clasificación | Uso en esta auditoría |
|---|---|---|
| `Celula3/README.md` | **Canónico** | Punto de entrada, baseline y orden de lectura. |
| `00_Gobierno/07_...`, `12_...`, `13_...` | **Canónico** | Alcance I1, estructura, figuras pendientes, `V-DATA-01` y cierre D3. |
| `00_Gobierno/00_...` a `06_...`, `08_...` a `11_...` | Evidencia o apoyo vigente | Maestro, cumplimiento, ADR, alineaciones y decisiones MA. |
| `01_Frente_Logica_Integracion/A1..A3` | **Canónico técnico** | Componentes, procesos, integración, autoridad, `EDGE-RUN`. |
| `02_Frente_Fisica_Despliegue/C1..C4` | **Canónico técnico** | Emplazamiento, tecnologías, red, continuidad y capacidad. |
| `03_Frente_Seguridad_Consolidacion/D1..D3` | **Canónico técnico/control** | Seguridad, amenazas/SPOF y auditoría de ensamblado. |
| Carpetas `trazabilidad/` | Evidencia o apoyo | Requisitos, correcciones, estados y escalaciones; no fuente editorial principal. |
| `90_Consolidado/00_CONTENIDO...` | Borrador/destino canónico | Esqueleto aún no redactado; no es evidencia de entrega terminada. |
| `90_Consolidado/01_T11...` y `02_FORMULARIO...` | **Canónico** | Matriz trazable y formulario contractual actual. |
| `90_Consolidado/03_CHECKLIST...` | Evidencia/control | Criterios pendientes de producción. |
| `05_CAMBIOS_SIN_COMMIT...` | Histórico | Registro de una etapa previa; no gobierna la baseline. |
| `COMPLEMENTO_AUDITORIA...` | Evidencia o apoyo | Auditoría anterior del catálogo tecnológico. |
| PDFs dentro de `Celula3/` | Evidencia externa/apoyo | No fueron necesarios para el contraste C3–C4. |
| `.DS_Store` | Ruido técnico | Sin contenido documental. |

### 13.2 Clasificación de fuentes Célula 4

| Ruta o conjunto | Clasificación | Uso en esta auditoría |
|---|---|---|
| `Célula 4/00_INDICE.md` | Navegación general | Orienta hacia las rutas editables y clasifica las copias históricas; debe mantenerse sincronizado con el índice canónico anidado. |
| `Subdocumento_5/00_INDICE.md` | **Canónico de navegación de Subdoc. 5** | Define la ruta editable, el estado vigente y el tratamiento de respaldos y copias. |
| `Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md` | **Canónico de lectura y edición** | Contenido completo disponible y base principal del análisis. |
| `Subdocumento_5/Subdocumento_5.pdf` | Generado/entregable compilado | Autoridad de discrepancia según índice; no fue necesario releerlo porque el conflicto se resolvió con fuente oficial y Markdown. |
| `Subdocumento_5/Documentos_de_trabajo/A00..A08` | **Apoyo técnico canónico** | Conserva decisiones, modelos, reglas y cálculos que sustentan el Markdown entregable. |
| `A00..A08` en raíz y `Documentos_de_trabajo/A00..A08` | Histórico/compatibilidad | Copias del corte anterior; no editar ni usar para gobernar nuevas correcciones. |
| `Subdocumento_5/Comunicados/00..04` | **Evidencia operativa vigente** | Dependencias, decisiones y condiciones comunicadas desde la ruta canónica. |
| `Comunicados/00..04` en raíz | Histórico/compatibilidad | Copias anteriores; se conservan para no romper referencias, pero no se editan. |
| `00_ESQUELETO_SUBDOCUMENTO_5.md` y copia anidada | Histórico | Declarado superado por el índice. |
| `diagramas/*.mmd` y copia anidada | Histórico/redundante | Versión 1; el índice declara vigente una v2.1 externa que no está versionada. |
| `Subdoc13/00_INDICE_SUBDOCUMENTO_13.md` | **Canónico de navegación** | Alcance I1, estados y cartera. |
| `Subdoc13/B01..B08` y `B12` | **Canónico editorial C4** | Texto que va al PDF; `APROBADO` significa integrable editorialmente. |
| `Subdoc13/B00`, `B09..B11`, `B13`, `B14` | Evidencia o apoyo | Decisiones, trabajo anticipado, verificación, dependencias y alcance. |
| `Subdoc13/Documentos_de_trabajo/*` | Histórico | Consolidados anteriores, declarados como historial. |
| `Subdoc13/Subdocumento_13/*.tex` y `general/*.tex` | Generado/editorial auxiliar | Plantilla/fuente de compilación; no aportó contenido exclusivo necesario y no se consultó. |
| `Subdoc13/...PREVIEW.pdf` | Generado | Vista previa compilada. |

### 13.3 Observación sobre `.tex`

No se encontró una contradicción que exigiera abrir los `.tex`. Para Subdoc 13 existe Markdown canónico por pieza. Para Subdoc 5, el índice menciona un proyecto LaTeX externo, pero ese proyecto no está en `main`; por tanto, no puede actuar como fuente reproducible dentro del repositorio. Esta ausencia es un hallazgo de gobierno (`AC34-006`), no una razón para inferir contenido.

### 13.4 Fuentes oficiales consultadas

- *FEP03.06.26 Caso 06 — Portuaria (Bases Técnicas del Caso)*, capítulos 14.2 y 15, especialmente `RT-03.10` y `RT-03.13`. Se consultó únicamente para resolver `AC34-001/002`. Cada integrante debe usar la copia oficial de las bases disponible en su entorno; ninguna ruta local forma parte de la referencia.

### 13.5 Precedencia aplicada

1. Bases oficiales para obligaciones y parámetros contractuales.
2. README/índices para vigencia y rutas.
3. Entregables/consolidados canónicos.
4. Registros de decisión y frentes técnicos para razonamiento.
5. Trazas/comunicados como evidencia de estado.
6. Históricos, generados y duplicados solo para detectar deriva; nunca para reemplazar una fuente vigente.

---

## Registro de cambios de esta auditoría

La auditoría se creó inicialmente sin alterar las fuentes de las células. Las correcciones posteriores de alineación sí fueron aplicadas de manera quirúrgica y están registradas en `PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md`. No se hizo commit ni push durante esta preparación.
