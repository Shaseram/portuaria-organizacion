# Subdocumento 5 — Modelo y gestión de datos

CÉLULA 4 · CASO 06 PORTUARIA · TERABYTE

**Esqueleto completo con estado, fuente y trazabilidad de dependencias**
Responsable: Valentina Guzmán (con Matías Reyes) · Entrega Informe 1: 7 de septiembre de 2026 · Elaborado: 6 de septiembre de 2026

* * *

## 0\. Cómo leer este documento

### 0\.1 Qué significa cada estado

El estado **no** describe si el texto ya está redactado — nada del Subdocumento 5 lo está todavía. Describe **la estabilidad del respaldo documental disponible hoy** para redactarlo:

| Estado | Significado operativo |
| --- | --- |
| `[COMPLETADO]` | Hay respaldo real y estable en las Bases, el Caso Portuaria o el cierre vigente de Célula 2. Se puede redactar y cerrar ahora. Se cita documento \+ capítulo/numeral \+ código \+ materia. |
| `[COMPLETADO PROVISIONAL — depende de Célula 3, entrega no cerrada]` | Se puede redactar, pero se apoya en material de Célula 3 que aún puede cambiar. Se indica el documento de apoyo, la decisión asumida y qué habría que rehacer. |
| `[PENDIENTE — falta información de Célula X]` | El vacío pertenece a otra célula y no se completa por cuenta propia. |
| `[PENDIENTE — decisión propia de Célula 4]` | El vacío es nuestro. Nadie lo va a resolver por nosotros. |

### 0\.2 Regla de cita obligatoria

Los códigos `RT` se repiten entre documentos con materias distintas. Ejemplo verificado en este trabajo: `RT-05.10` es **linaje automatizado (Deseable)** en `FEP02 BTT, Cap. 5`, pero es **retención de datos históricos y de auditoría (Según caso)** en `FEP03 CP, Cap. 15`. Lo mismo ocurre con `RT-05.15` y con `RT-03.24`. Ningún código se cita solo: siempre **documento \+ capítulo/numeral \+ código \+ materia**.

### 0\.3 Advertencia sobre la comparación pedida

No tengo acceso, en esta sesión, a la versión anterior del esqueleto que se te entregó: la carpeta `Células proyecto/Célula 4` está vacía y no hay documentos previos en el proyecto. Por eso este documento **no es un diff contra esa entrega**, sino una reconstrucción verificada contra las fuentes primarias, la guía de arranque adjunta y el estado real de Células 2 y 3 al 6 de septiembre. Si conservas el archivo anterior, puedo compararlo línea a línea.

* * *

## 1\. Revisión de la guía de arranque y del cambio de Daniel en Célula 2

### 1\.1 Veredicto sobre la guía

La guía de arranque **está sustancialmente correcta**. Verifiqué contra los PDF oficiales y todo lo siguiente resultó exacto:

| Afirmación de la guía | Verificación |
| --- | --- |
| El Subdocumento 5 tiene 6 exigencias en T\-7 (`T7-5.1` a `5.6`) | Correcto — `FEP01.26 BA, Form. T-7, Subdoc. 5`\: seis viñetas exactas |
| Pondera 11 % del Informe 1 | Correcto — `FEP01.26 BA, Form. T-21`, fila 5: 11 % / 6 % / 5 % |
| T\-22 incluye el Subdoc. 5 en el Informe 1 pero sin viñeta propia de presentación | Correcto — `FEP01.26 BA, Form. T-22`, Informe 1: la lista de subdocumentos incluye el 5; las viñetas de la presentación no lo mencionan |
| Retenciones de 7 clases (10/5/6/5/12m/5/2 años) | Correcto — `FEP03 CP, Cap. 15, RT-05.10 — retención`, y `C2 · RNF.md, RNF-CUM-14` |
| Logs de seguridad 12 meses en línea \+ 24 en archivo | Correcto, y la fuente es distinta de la anterior: `FEP02 BTT, Cap. 11, RT-11.14 — registro centralizado e inalterable` |
| Seis universos de migración con remanente consultable | Correcto — `FEP03 CP, Cap. 15, RT-05.15 — datos históricos a migrar`, `FEP02 BTT, Cap. 5, RT-05.15 — repositorio de consulta`, y `C2 · Decisión 1, §15.1` |
| Umbrales ≤1 s / ≤120 s / ≤3 s / ≤5 min / ≤1 h / 1,5× peak / ≤90 min | Correctos — `FEP03 CP, Cap. 15, RT-09.01, RT-05.29, RT-03.13`; `FEP02 BTT, Cap. 9, RT-09.06` |
| Los componentes `DATA-CORE/TS/DOC/AN` son descomposición inicial, no motores | Correcto — `C3 · Maestro §6.1` los define como catálogo lógico refinable |

### 1\.2 Lo que la guía **no** recoge: la actualización de Daniel

La guía está anclada a la línea base de Célula 2 del **4 de septiembre** (138 RF / 84 RNF). Daniel aplicó después dos rondas más, fechadas **5 de septiembre**, que están en los anexos del mismo archivo de cierre (`C2 · 00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md`, «Segunda ronda B1–B13» y «Tercera ronda C1–C7»). Célula 3 **ya se realineó** a esa versión (`C3 · README`\: «Célula 2 `c4756df` · 139 RF / 91 RNF / 11 reglas»; `C3 · Maestro §2.3 — Consecuencias del corte 2026-09-05`). Célula 4 debe trabajar sobre esa base, no sobre la del día 4.

| Conteo | Guía (04\-sep) | Vigente (05\-sep) |
| --- | ---: | ---: |
| RF | 138 | **139** (82 Etapa 1 / 57 Etapa 2) |
| RNF | 84 | **91** en 9 categorías |
| Reglas de negocio | 10 | **11** |
| Decisiones / Supuestos | 21 / 25 | 21 / 25 (sin cambio) |

**Impactos directos sobre el Subdocumento 5 que la guía no menciona:**

1. **`RNF-DES-09` a `RNF-DES-12` (nuevos, cambio B1).** Incorporan los umbrales de `FEP02 BTT, Cap. 9, num. 9.1` (portal ≤2 s, navegación ≤1 s, API consulta ≤500 ms, escritura ≤800 ms, búsqueda ≤3 s, informe ≤30 s, lotes ≥10.000 reg/min, archivo 100 MB ≤60 s, arranque en frío ≤60 s) y la prueba de carga a 1,5× peak con estrés hasta saturación. **Toda la sección 9 (desempeño de datos) debe derivarse también de estos**, no solo de los umbrales del Cap. 15.
2. **`RNF-DIS-13/14/15` (nuevos, cambio B1).** RTO ≤4 h, RPO ≤15 min, respaldo **3\-2\-1\-1\-0**, prueba de conmutación real semestral. Afectan las secciones 4 (disponibilidad) y 11 (archivo y recuperación). La guía no los cita.
3. **`RF-REF-07` corregido (B3 \+ C2).** La alarma por ausencia de dato se dispara a **tres intervalos de muestreo o cinco minutos, lo que ocurra primero**. Esto es una restricción dura sobre la frecuencia de muestreo que propongamos (sección 6).
4. **`RN-11` nueva (B4, corregida en C1 y C6).** Define la *tolerancia de desviación de temperatura* — banda y duración —, **sin fijar valores numéricos** porque el caso no los entrega, y prohíbe una parametrización que haga inalcanzable el plazo de `FEP03 CP, Cap. 15, RT-05.29`. Es un atributo del modelo de datos reefer que el diccionario debe recoger como parámetro, no como constante.
5. **Volumetría ampliada (B5).** Se incorporó el **factor estacional** (camiones ×1,79; volumen refrigerado mensual enero–marzo ×2,48) y la derivación del tiempo de sincronización (≈13 GB / 90 min ⇒ **≈19,3 Mbps sostenidos**). Sin esto, la sección 12 queda incompleta frente a `FEP03 CP, Cap. 14.2`, que sanciona «valores sin derivación» igual que las celdas vacías.
6. **`RF-POR-09` nuevo (B2, corregido en C3).** Presentación estructurada de la instrucción de embarque por embarcador o agencia; el 41 % de redigitación corresponde **íntegro** a ese flujo, no al de naviera→terminal. Introduce entidades documentales nuevas en el mapa de dominios (sección 1).
7. **Vacío declarado y no resuelto:** el universo instrumentable son 74 equipos actuales / 88 proyectados y **excluye las seis grúas de muelle** (`C2 · anexo 2ª ronda, "Queda abierto"`; `C3 · Maestro §18.1`). Nadie ha declarado qué evento produce el movimiento de muelle. Es un vacío de modelo de datos, no solo de integración.

### 1\.3 Un ajuste a la guía que conviene incorporar

La guía omite `RNF-DES-06` — **publicación del estado del contenedor en el portal ≤60 s** (`FEP03 CP, Cap. 15, RT-09.01` y `RT-16.30`) — en su lista de umbrales. Es un umbral de propagación hacia la capa de consulta y pertenece a las secciones 5 y 9.

* * *

## 2\. Resumen de estados

| \# | Punto oficial del checklist | Estado |
| ---: | --- | --- |
| 1 | Dominios y entidades principales | `[COMPLETADO]` |
| 2 | Fuentes oficiales y fuente de verdad | `[COMPLETADO]` (base Célula 2, sujeta a confirmación) |
| 3 | Paradigma de persistencia y motores propuestos | `[COMPLETADO PROVISIONAL — depende de Célula 3]` |
| 4 | Transaccionalidad, consistencia y disponibilidad | `[COMPLETADO]` |
| 5 | Separación transaccional / temporal / analítico | `[COMPLETADO PROVISIONAL — depende de Célula 3]` |
| 6 | Telemetría y frecuencia de muestreo | `[COMPLETADO]` |
| 7 | Integración e interoperabilidad de datos | `[PENDIENTE — falta información de Célula 3]` |
| 8 | Migración, saneamiento, validación y conciliación | `[COMPLETADO]` |
| 9 | Estrategia de desempeño (índices, particiones, caché, consultas) | `[COMPLETADO PROVISIONAL — depende de Célula 3]` |
| 10 | Calidad ISO/IEC 25012, auditoría y trazabilidad | `[PENDIENTE — decisión propia de Célula 4]` |
| 11 | Retención, archivo y eliminación segura | `[COMPLETADO]` |
| 12 | Volumetría actual, proyectada y de peak | `[COMPLETADO PROVISIONAL — depende de Célula 3]` |
| 13 | Modelo conceptual de datos y diccionario inicial | `[PENDIENTE — decisión propia de Célula 4]` |

**Recuento:** 5 completados · 4 completados provisionales (todos por Célula 3) · 1 pendiente por otra célula (Célula 3) · 2 pendientes propios de Célula 4 · **13 de 13 puntos cubiertos**.

**Lectura de riesgo:** ninguno de los cuatro provisionales depende de contenido *aprobado* de Célula 3 — dependen de su **Maestro de contexto y de sus contratos de trabajo**, porque los nueve entregables del Subdocumento 4 están literalmente marcados `PENDIENTE DE INTEGRAR` en `C3 · 90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`. Ese es el hecho central de coordinación de esta semana.

* * *

## 3\. Esqueleto del Subdocumento 5

### 5\.1 Dominios de información y entidades principales

**Estado:** `[COMPLETADO]`

**Qué debe contener:** mapa de dominios y sus fronteras; entidades, relaciones, agregados y eventos de negocio; propietario, productor, consumidor y autoridad del dato por dominio; clasificación del dato (operacional, maestro, personal, comercial sensible, evidencia, telemetría); invariantes derivadas de las reglas de negocio; tratamiento del cruce de zonas y fases sin autoridad doble.

**Fuentes:**

- `FEP01.26 BA, Form. T-7, Subdoc. 5` — viñeta «Dominio de información».
- `FEP01.26 BA, Art. 23° — Datos, integración e interoperabilidad`\: modelo documentado, diccionario entregable, **linaje y propietario de cada dominio**.
- `FEP02 BTT, Cap. 5, RT-05.01 — modelo y diccionario de datos`; `RT-05.09 — gestión de datos maestros sin duplicación`.
- `FEP03 CP, Caps. 4 a 10` — procesos, actores, dolores y restricciones; `Cap. 3` — zonas del recinto.
- `C2 · Catálogo RF partes 1–3` (139 RF vigentes) y `C2 · Registro reglas de negocio v2` (RN\-01 a RN\-11).

**Dominios candidatos (mínimo a evaluar):** contenedor y operación; patio y posición; gate y transporte; reefer; nave y planificación; inspecciones; evidencia y facturación; acceso e identidad; energía y emisiones; integración y auditoría. Se pueden fusionar o dividir con justificación; **no se crea una tabla ni un almacén por cada RF**.

**Ajuste obligatorio por el corte 05\-sep:** incorporar las entidades documentales de `RF-POR-09` (instrucción de embarque presentada por embarcador o agencia) y distinguirlas de `RF-INT-02` (orden COPRAR de naviera→terminal).

**Qué queda abierto:** los nombres definitivos de *bounded contexts* provienen de `A1` (Célula 3) y hoy no existen. Se usan identificadores propios estables y se mapean después. Ver riesgo `R-C3-01`.

* * *

### 5\.2 Fuentes oficiales y fuente de verdad

**Estado:** `[COMPLETADO]` — con la advertencia de que la fuente es una **decisión de célula par (revisable)**, no de las Bases.

**Respuesta a la pregunta planteada:** **Célula 3 todavía no ha definido la fuente de verdad de la posición del contenedor.** Lo que existe es una decisión **de Célula 2** que Célula 3 heredó y todavía no convirtió en matriz:

- `C2 · Decisión N° 1, §5.2`\: la autoridad se define por **`dominio × zona × fase`**. Antes del cutover de una zona manda el TOS 2012; durante la validación paralela el sistema nuevo es solo lector/sombra; después del cutover aprobado manda el sistema nuevo y el legado recibe réplica para retorno. El cruce de zona es una **transferencia transaccional**\: el sistema con autoridad emite un evento secuenciado e idempotente, el receptor confirma persistencia y solo entonces cambia la autoridad. Un fallo parcial mantiene la autoridad anterior. **Nunca dos sistemas aceptan escrituras autoritativas sobre el mismo contenedor y dominio.**
- Materializado en `C2 · Catálogo RF parte 1, RF-CON-14` y `RF-CON-13`.
- Fundamento normativo: `FEP01.26 BA, Art. 17.2, punto 2` — «única fuente de verdad para los datos compartidos», «evitar toda doble digitación».
- Célula 3 lo recogió en `C3 · Maestro §8` (once condiciones de coexistencia) pero su matriz operativa está **`POR COMPLETAR`** en `C3 · A3_PROCESOS_CRITICOS_Y_TOS.md`.

**Decisión de Célula 4:** se reutiliza `dominio × zona × fase` sin redefinirla. Queda **sujeta a confirmación** cuando `A3` publique su matriz con zonas y fases nombradas.

**Además debe contener:** matriz `dato → propietario → fuente de verdad → sensibilidad → retención`; distinción entre fuente de verdad actual, durante coexistencia y final; sistemas conservados que **no** son fuente de verdad de la solución (ERP emite el documento tributario — `FEP03 CP, Cap. 5`; control de grúas no se interviene; VMS/CCTV se conserva).

* * *

### 5\.3 Paradigma de persistencia y motores propuestos

**Estado:** `[COMPLETADO PROVISIONAL — depende de Célula 3, entrega no cerrada]`

**Documento de apoyo de Célula 3:** `C3 · Maestro §6` (capa 6 «Datos»: transaccional, analítico, documental, series temporales y archivos separados según necesidad) y `C3 · Maestro §6.1` (componentes `DATA-CORE`, `DATA-TS`, `DATA-DOC`, `DATA-AN`).

**Decisión concreta asumida:** que la capa de datos se descompone en **cuatro familias** — operacional transaccional, series temporales, documental/objetos y analítica — más un repositorio histórico independiente, y que esa descomposición sobrevive al cierre de Célula 3.

**Qué habría que rehacer si cambia:** la matriz `familia → paradigma → consistencia → disponibilidad → CAP` completa, la sección 5.5 (separación de almacenamientos) y el mapeo del diccionario de datos a almacenes.

**Qué se puede cerrar ahora sin Célula 3:** la clasificación de cada familia de datos por necesidad dominante, la comparación de **al menos dos alternativas reales por familia**, la declaración de unidad transaccional e invariantes que exigen consistencia fuerte, y el análisis de comportamiento bajo partición de red y 72 h desconectado. Esto último es exigencia explícita: `FEP02 BTT, Cap. 5, RT-05.02 — paradigma, motor, garantías transaccionales y posición CAP por cada dominio de datos`.

**Familias e hipótesis a validar (no a copiar como decisión cerrada):**

| Familia | Necesidad dominante | Alternativas a comparar |
| --- | --- | --- |
| Estado operacional | ACID, integridad, consistencia fuerte | relacional gestionado vs. relacional operado localmente/híbrido |
| Reefer y telemetría de equipos | alta ingesta, orden temporal, retención diferenciada | extensión temporal sobre relacional vs. motor de series temporales |
| Imágenes, documentos y evidencia | objetos, metadatos, inmutabilidad | almacenamiento de objetos \+ índice vs. gestor documental |
| Analítica y KPI | lectura agregada sin cargar OLTP | réplica/modelo analítico vs. almacén analítico separado |
| Histórico no migrado | consulta de baja frecuencia, formato abierto | repositorio consultable abierto vs. motor de archivo dedicado |

**Restricción que condiciona toda la sección:** `FEP03 CP, Cap. 15, RT-03.10` — 72 horas continuas de operación completa sin enlace hacia el exterior, y las terminales de equipos de patio 8 horas fuera de cobertura sin pérdida de registro. Ninguna familia crítica puede depender de la nube para registrar.

`[PENDIENTE — decisión propia de Célula 4]` dentro de esta sección: la **recomendación de paradigma y motor por capacidades** todavía no está escrita, y ninguna comparación de alternativas está hecha. No se debe nombrar un producto comercial antes de esa comparación.

* * *

### 5\.4 Transaccionalidad, consistencia y disponibilidad

**Estado:** `[COMPLETADO]`

**Qué debe contener:** unidad transaccional por dominio; invariantes que exigen consistencia fuerte frente a las que toleran consistencia eventual; posición CAP **por operación**, no como elección global; idempotencia, control de concurrencia, versionado y resolución determinista de conflictos; comportamiento durante partición y durante las 72 h.

**Fuentes estables:**

- `FEP02 BTT, Cap. 5, RT-05.02` — CAP por dominio de datos, obligatorio.
- `FEP03 CP, Cap. 15, RT-03.10 / RT-03.13` — 72 h desconectado; sincronización ≤90 min **sin pérdida de ningún movimiento ni hecho facturable y con resolución determinista de los conflictos de posición**.
- `FEP02 BTT, Cap. 3, RT-03.11 / RT-03.12` — registro local íntegro y reconciliación determinista con bitácora auditable.
- `FEP02 BTT, Cap. 10, RT-10.01` — 99,9 % mensual para servicios críticos, medido de extremo a extremo.
- `C2 · RNF.md`\: `RNF-DIS-02/03/04` (operación desconectada y sincronización) y **`RNF-DIS-13/14/15`** (RTO ≤4 h, RPO ≤15 min, respaldo 3\-2\-1\-1\-0, prueba DR semestral con conmutación real) — nuevos del corte 05\-sep.

**Umbral que no puede diluirse:** `C2 · Decisión 1, §15.3` fija **cero diferencias no explicadas al cierre diario** en gate y hechos facturables, con ventana de investigación de 24 h; posición y movimientos usan ventana de 48 h. La regla direccional de `§15.2` clasifica cada divergencia contra verificación física: cuando el sistema nuevo resulta correcto **no computa** contra el umbral.

**Nota de coordinación:** RTO/RPO están replicados en `C3 · Maestro §9.2`. Coinciden con los RNF de Célula 2, de modo que la afirmación no depende de Célula 3; si Célula 3 los endurece, cambia el dimensionamiento de respaldo (sección 11), no la política.

* * *

### 5\.5 Separación entre almacenamiento transaccional, temporal y analítico

**Estado:** `[COMPLETADO PROVISIONAL — depende de Célula 3, entrega no cerrada]`

**Documento de apoyo de Célula 3:** `C3 · Maestro §6` (capa 6 y regla «sin acceso UI→BD») y `§6.1` (`DATA-CORE` / `DATA-TS` / `DATA-DOC` / `DATA-AN`).

**Decisión asumida:** que la analítica se alimenta por flujo desde eventos operacionales y que `DATA-AN` es un almacén separado del operacional. **Qué habría que rehacer si cambia:** el flujo OLTP→analítica, el modelo semántico y las latencias declaradas por indicador.

**Fuentes estables:**

- `FEP01.26 BA, Form. T-7, Subdoc. 5` — «Separación entre almacenamiento transaccional y analítico, y modelo de explotación de información».
- `FEP02 BTT, Cap. 5, RT-05.05` — separación obligatoria; ninguna consulta analítica puede degradar la operación. `RT-05.25/26/27/28` — tableros, *drill\-down* hasta la transacción de origen, autoservicio del CLIENTE con modelo semántico documentado, exportación e informes programables.
- `FEP03 CP, Cap. 15, RT-05.29 — latencia de la capa analítica`\: alarma reefer ≤5 min; posición visible ≤30 s tras el movimiento; productividad de grúa y estadía de camión en tiempo real con granularidad por hora y por equipo; indicadores del concedente ≤1 h tras el cierre de turno.
- `FEP03 CP, Cap. 10, restricción 14` y `Cap. 18, criterio 20` — los indicadores comprometidos con el concedente se producen de forma trazable, **no se reconstruyen**.
- `C2 · RNF.md`\: `RNF-DES-05` (≤30 s), `RNF-DES-06` (portal ≤60 s), `RNF-DES-07` (≤1 h), `RNF-OPE-02` (desfase ≤5 min en tableros, exportación CSV/XLSX).

**Productos de explotación mínimos:** gate y estadía; productividad por grúa/hora/equipo; posición e inventario; cadena de frío y alarmas; inspecciones; hechos, evidencias y objeciones; energía y emisiones por contenedor; indicadores del concedente.

**Distinción de tres almacenamientos, no dos:** el checklist oficial interno pide separar **transaccional, temporal y analítico**. El almacenamiento *temporal* (series de telemetría y estados intermedios de conciliación) se trata explícitamente, no se subsume en el analítico.

* * *

### 5\.6 Telemetría (tomas, tableros, equipos móviles) y frecuencia de muestreo

**Estado:** `[COMPLETADO]`

**Fuentes estables:**

- `FEP03 CP, Cap. 14.2` — la frecuencia de muestreo es **una decisión de diseño con consecuencias de costo, red y almacenamiento, y debe justificarse**; la telemetría puede superar en órdenes de magnitud el volumen transaccional.
- `FEP03 CP, Cap. 16.1, decisión pendiente N° 8` — qué frecuencia y qué se transmite: dato crudo, agregado en el borde o solo desviaciones.
- `FEP03 CP, Cap. 15, RT-17.06` — instrumentación de las 2.400 tomas y de los 26 tableros; posicionamiento de equipos móviles; telemetría de grúas de muelle **solo lectura y sujeta a autorización del fabricante**.
- `FEP03 CP, Cap. 15, RT-05.29` — alarma de desconexión o desviación ≤5 min desde el evento físico.
- `C2 · Decisión N° 8`\: modelo de dos capas — **muestreo local de 1 a 5 min, agregación en gateway, reporte al núcleo de 5 a 15 min, más envío inmediato ante excepción**.
- `C2 · RF-REF-07` (corregido 05\-sep): alarma por ausencia de dato a **3 intervalos de muestreo o 5 minutos, lo que ocurra primero**.
- `C2 · RN-11` (nueva 05\-sep): banda y duración de la desviación de temperatura son **parametrizables sin valores fijados por el caso**, y se rechaza toda parametrización que haga inalcanzable el plazo de `RT-05.29`.
- `C2 · Volumetría, filas 3, 4 y 5`\: ≈7,2 ev/s reportados al núcleo (≈8,7 proyectado) y ≈35,8 ev/s locales (≈43,3); posición de equipos ≈37 ev/s (≈44) con **frecuencia de 2 s declarada como valor de diseño por validar**.

**Modelo de datos que esta sección debe fijar:** muestra, serie, consigna, umbral, evento de excepción, alarma, confirmación de recepción por persona identificada, y la distinción entre **dato de alta resolución local** y **dato agregado reportado**, con su retención diferenciada (2 años en línea, agregación posterior).

**Vacíos declarados, no completados:** (a) la frecuencia de 2 s del posicionamiento no está fijada por ninguna decisión — es supuesto de diseño; (b) el universo instrumentable de 74/88 equipos **excluye las seis grúas de muelle** y nadie ha declarado qué evento produce el movimiento de muelle.

* * *

### 5\.7 Integración e interoperabilidad de datos

**Estado:** `[PENDIENTE — falta información de Célula 3]` — depende de la arquitectura de integración (`A2`), a cargo de Célula 3.

**Lo que sí está cerrado y se puede escribir hoy:**

- Inventario de **21 contrapartes lógicas actuales** (14 navieras \+ 3 autoridades \+ operador ferroviario \+ concedente \+ TOS 2012 \+ ERP) y **7 familias de periferia/instrumentación** — `C2 · Volumetría, fila 12 y matriz controlable de integraciones`. Con 16 navieras proyectadas, 23 contrapartes.
- Volúmenes base: ≈972.000 registros de carga/descarga alimentan COARRI; ≈1.058.500 eventos de gate alimentan CODECO; **no se presume un sobre de red por movimiento**; autoridades 18.400 casos/año; ERP ≈115.200 documentos/año; TOS hasta ≈3.435.700 operaciones/año durante coexistencia.
- Estándares: `FEP03 CP, Cap. 15, RT-05.23` — mensajería marítima estándar (plano de estiba, orden de embarque, confirmación de carga y descarga, notificación de movimiento), norma internacional de codificación de contenedores, estándares con aduana y fitosanitaria, **con acreditación de factibilidad ante las 14 navieras**. `C2 · MC-20`\: COARRI para carga/descarga, CODECO para gate/custodia.
- Obligaciones transversales: `FEP02 BTT, Cap. 5, RT-05.16` (OpenAPI 3.1 / AsyncAPI 2.6\+), `RT-05.17` (versionado semántico, preaviso 6 meses), `RT-05.19` (**identificador de correlación común de extremo a extremo**), `RT-05.20` (capa anticorrupción frente a sistemas heredados), `RT-05.21` (modo, volumen, ventana y comportamiento ante no respuesta por integración), `RT-05.22` (carga/descarga masiva con informe de errores por registro).

**Lo que falta y por qué no se completa:** los contratos, eventos, versiones, claves de idempotencia y mecanismo de CDC están literalmente `POR DETALLAR` / `POR LEVANTAR` en `C3 · A2_ARQUITECTURA_DE_INTEGRACION.md`, y `ADR-003 (mecanismo de integración/eventos)` figura como `CANDIDATO` en `C3 · 03_REGISTRO_ADR_GLOBAL.md`. Además, `C3 · Maestro §18, ESC-06` mantiene abiertos los contratos de TOS, VMS, autoridades, ferrocarril, radio, grúas y periféricos. **No se inventa ninguna API, protocolo, versión ni disponibilidad de terceros** (`C3 · Maestro §19, regla negativa 9`).

* * *

### 5\.8 Estrategia de migración, saneamiento, validación y conciliación

**Estado:** `[COMPLETADO]`

**Fuentes estables:**

- `FEP02 BTT, Cap. 5, RT-05.11` (plan con alcance, origen, volumen, transformación, calidad, ejecución y reversión), `RT-05.12` (perfilado y saneamiento previo con informe de defectos y decisión sobre cada uno), `RT-05.13` (**al menos dos ensayos completos en Preproducción**), `RT-05.14` (conciliación cuantitativa: recuentos, sumas de control y muestreo dirigido; toda diferencia explicada), `RT-05.15` (histórico no migrado en repositorio de consulta durante la retención).
- `FEP03 CP, Cap. 15, RT-05.15 — datos históricos a migrar`\: inventario completo con posición verificada físicamente; movimientos 3 años; hechos facturables y evidencia 6 años; maestros completos; tarifario vigente; objeciones abiertas.
- `C2 · Decisión 1, §15.1` — matriz de los **seis universos** con conciliación y destino del remanente; **el hueco de siete años** entre lo que se retiene (10 años) y lo que se migra (3 años) vive en un repositorio consultable abierto; el sistema de 2012 **se apaga en el mes 22**, un mes después del hito H12, condicionado a acta de conformidad del repositorio histórico (completitud, legibilidad en formato abierto, prueba de recuperación dirigida).
- `C2 · Decisión 1, §5.3` — secuencia: descubrir y documentar → comprobar lectura/escritura/sincronización/reconciliación → capa anticorrupción → observabilidad de convivencia → prueba en zona acotada → migración progresiva. Los pasos 1 y 2 alimentan la **puerta de decisión del mes 4**.

**Matriz de alcance heredada que no se puede reducir:**

| Conjunto | Migración | Conciliación | Remanente retenido |
| --- | --- | --- | --- |
| Inventario | Completo, con posición verificada físicamente al corte | Recuento 100 %, unicidad y barrido por bloque | No aplica |
| Movimientos | 3 años | Recuento por período y día, integridad de secuencia, muestra de recuperación | Años 4–10 en repositorio consultable abierto |
| Hechos y evidencias | 6 años | Correspondencia 1:1, totales por período, recuperación dirigida | Repositorio durante la retención |
| Maestros | Completos y vigentes, con historial interpretativo | Recuento, claves, relaciones, validación por dueño de dato | Versión exportable documentada |
| Tarifario | Versión vigente al corte | Comparación 100 % de reglas, vigencias y excepciones | Versiones históricas ligadas a evidencias |
| Objeciones | Abiertas completas con expediente | Recuento 100 %, estado, responsable y documentos | Cerradas retenidas según plazo |

**Qué queda por confirmar externamente:** esquema, calidad y tamaño reales del TOS 2012 (`FEP03 CP, Cap. 5`\: el CLIENTE **no dispone de documentación del modelo de datos**); capacidad efectiva de extracción/CDC/escritura; fecha exacta de fin de soporte (`C3 · Maestro §18, ESC-04`\: escenario conservador desde 01\-01\-2028). La ausencia de esos datos **no impide diseñar la estrategia**\: obliga a registrar supuestos, puertas y pruebas.

* * *

### 5\.9 Estrategia de desempeño: índices, particiones, caché y consultas

**Estado:** `[COMPLETADO PROVISIONAL — depende de Célula 3, entrega no cerrada]`

**Documento de apoyo de Célula 3:** `C3 · C4_DIMENSIONAMIENTO_Y_T11.md` y `C3 · Maestro §15`, que declaran las cifras heredadas como «insumos, no dimensionamiento final».

**Decisión asumida:** que el dimensionamiento de Célula 2 (18 dimensiones \+ factor estacional) se mantiene como base de cálculo. **Qué habría que rehacer si cambia:** la tabla `operación → volumen → latencia → técnica → evidencia`, la propuesta de particionamiento y la identificación del primer cuello de botella.

**Lo que se puede cerrar ahora:** inventario de consultas y escrituras críticas por proceso; claves de búsqueda y patrones de acceso; propuesta de indexación por contenedor, tiempo, ubicación, actor, estado y correlación; particionamiento por tiempo o dominio **solo cuando el volumen o el mantenimiento lo justifiquen**; caché **solo para lecturas tolerantes a desfase**, con política de invalidación y fuente de verdad declarada; aislamiento de imágenes, series y analítica respecto de la carga transaccional.

**Umbrales que la estrategia debe sostener** (`FEP03 CP, Cap. 15, RT-09.01` y `RT-05.29`; `FEP02 BTT, Cap. 9, num. 9.1` y `RT-09.06`; `C2 · RNF-DES-01..12`):

| Operación | Umbral | Origen |
| --- | --- | --- |
| Confirmación de movimiento desde equipo de patio | ≤1 s (p95) | CP Cap. 15, RT\-09.01 · `RNF-DES-03` |
| Consulta de posición | ≤1 s | CP Cap. 15, RT\-09.01 · `RNF-DES-03` |
| Camión completo en puesto de gate | ≤120 s | CP Cap. 15, RT\-09.01 · `RNF-DES-01` |
| Reconocimiento óptico del código | ≤3 s | CP Cap. 15, RT\-09.01 · `RNF-DES-02` |
| Alarma del patio refrigerado | ≤5 min desde el evento físico | CP Cap. 15, RT\-05.29 · `RNF-DES-04` |
| Posición visible tras el movimiento | ≤30 s | CP Cap. 15, RT\-05.29 · `RNF-DES-05` |
| Estado publicado en el portal | ≤60 s | CP Cap. 15, RT\-09.01 / RT\-16.30 · `RNF-DES-06` |
| Indicadores del concedente tras cierre de turno | ≤1 h | CP Cap. 15, RT\-05.29 · `RNF-DES-07` |
| API de consulta simple / escritura | ≤500 ms / ≤800 ms (p95 bajo peak) | BTT Cap. 9, num. 9.1 · **`RNF-DES-10`** |
| Portal, navegación, búsqueda, informe | ≤2 s / ≤1 s / ≤3 s / ≤30 s | BTT Cap. 9, num. 9.1 · **`RNF-DES-09`** |
| Lotes y carga de archivo | ≥10.000 reg/min; 100 MB ≤60 s | BTT Cap. 9, num. 9.1 · **`RNF-DES-11`** |
| Escenario de prueba | Carga a **1,5× peak** y estrés hasta saturación | BTT Cap. 9, RT\-09.06 · **`RNF-DES-12`** |
| Sincronización tras 72 h | ≤90 min, sin intervención manual | CP Cap. 15, RT\-03.13 · `RNF-DIS-04` |
| Crecimiento sin rediseño | ≥3× volumetría inicial a 3 años | BTT Cap. 9, RT\-09.03 · `RNF-DES-08` |

**Obligación adicional:** `FEP02 BTT, Cap. 9, RT-09.05` exige **identificar el componente que primero se convertirá en cuello de botella**, cómo se detectará y cómo se resolverá. Para datos, el candidato natural es la ingesta de telemetría, no la transaccional: 0,23 TPS de negocio frente a ≈37 ev/s de posicionamiento y ≈43 ev/s de reefer local.

**Qué queda para Célula 3:** métricas reales del motor y topología; capacidad por nodo, réplicas y holgura (`C2/C4`); latencia de red y borde (`C1/C3`). Y una consecuencia cruzada: el **cifrado a nivel de campo** de `RT-11.10` restringe qué campos sensibles pueden indexarse — depende de `D1`/`ADR-009`.

* * *

### 5\.10 Calidad conforme a ISO/IEC 25012, auditoría y trazabilidad

**Estado:** `[PENDIENTE — decisión propia de Célula 4]`

**Por qué es nuestro y no de otra célula:** la obligación es explícita y estable, pero **nadie la ha desarrollado todavía**. Verificado: el catálogo de RNF de Célula 2 (91 RNF) **no contiene ningún requerimiento de calidad de datos conforme a ISO/IEC 25012**; su propio inventario de RT lo clasifica como materia mixta pendiente (`C2 · inventario_RT_bases_tecnicas_transversales.md`, fila `RT-05.04`). Y Célula 3 lo declara `PENDIENTE` remitiéndolo expresamente a nosotros (`C3 · 02_MATRIZ_CUMPLIMIENTO_GLOBAL.md`, `STD-09`\: «calidad de software, datos y pruebas… cruce Subdoc. 5/T\-13»).

**Obligaciones que hay que satisfacer:**

- `FEP02 BTT, Cap. 5, RT-05.04` — calidad conforme a ISO/IEC 25012, **validación en el punto de captura**, indicadores de completitud, exactitud y consistencia, y **tablero de calidad disponible para el CLIENTE**. Obligatorio.
- `FEP01.26 BA, Art. 23°` — mismas exigencias más **proceso de saneamiento de los datos migrados**; `Art. 13°` lista ISO/IEC 25012 entre los estándares de calidad exigibles.
- `FEP02 BTT, Cap. 5, RT-05.03` — trazabilidad total: reconstruir **quién, qué, cuándo, desde qué dispositivo y con qué valores anteriores y posteriores**, para cualquier registro y en **cualquier momento del período de retención**.
- `FEP02 BTT, Cap. 5, RT-05.10 — catálogo de datos con linaje automatizado` (Deseable) que permita rastrear cada indicador hasta su fuente.
- `FEP02 BTT, Cap. 16, RT-16.07` — registro de auditoría inalterable, no modificable ni eliminable por ningún perfil, incluido el administrador.
- `FEP03 CP, Cap. 15, RT-16.09` — registro de consultas a información sensible: información comercial de clientes, **ubicación y contenido declarado de contenedores**, y datos personales de trabajadores y conductores. La consulta de la ubicación de un contenedor **es información sensible por seguridad de la carga**.

**Qué debemos producir nosotros:** las seis dimensiones aplicables de ISO/IEC 25012 (completitud, exactitud, consistencia, oportunidad, unicidad, trazabilidad) con **regla, umbral, propietario, responsable de corrección y evidencia por clase de dato**; el diseño del tablero de calidad; el modelo de linaje desde indicador hasta transacción de origen; y la política de datos no productivos anonimizados (`FEP03 CP, Cap. 12` y regla negativa de no usar datos productivos sin anonimización verificable).

**Regla que nos impusimos:** no mencionar ISO/IEC 25012 sin control asociado y evidencia. Una mención sin métrica se evalúa como incumplimiento.

* * *

### 5\.11 Retención, archivo y eliminación segura

**Estado:** `[COMPLETADO]`

**Fuentes estables:** `FEP02 BTT, Cap. 5, RT-05.07` (política de retención, archivado y eliminación por dominio, con procedimiento verificable de eliminación segura), `RT-05.06` (exportación total en formatos abiertos, en cualquier momento, sin costo ni intervención del ADJUDICATARIO), `RT-05.08` (datos personales con seudonimización o cifrado de campo, conforme `FEP01.26 BA, Art. 85°` y Ley N° 21.719); `FEP03 CP, Cap. 15, RT-05.10 — retención`; `FEP02 BTT, Cap. 11, RT-11.14 — eventos de seguridad`; `C2 · RNF-CUM-14`, `RNF-CUM-08`, `RNF-POR-01`.

| Clase de información | Plazo y tratamiento | Fuente |
| --- | --- | --- |
| Movimientos y registros de operación | 10 años, eliminación controlada | CP Cap. 15, RT\-05.10 (régimen aduanero y vigencia de la concesión) |
| Series de temperatura reefer | 5 años, evidencia de cadena de frío | CP Cap. 15, RT\-05.10 · `RNF-CUM-08` |
| Evidencia de hechos facturables | 6 años, correspondencia 1:1 | CP Cap. 15, RT\-05.10 |
| Verificación de masa bruta (VGM) | 5 años | CP Cap. 15, RT\-05.10 |
| Imágenes de reconocimiento (contenedor y patente) | 12 meses; eliminación o anonimización controlada | CP Cap. 15, RT\-05.10 |
| Registros de acceso de personas | 5 años | CP Cap. 15, RT\-05.10 |
| Telemetría de equipos | 2 años en línea \+ agregación histórica por plazo declarado | CP Cap. 15, RT\-05.10 |
| Eventos y logs de seguridad | 12 meses en línea \+ 24 meses en archivo recuperable | **BTT Cap. 11, RT\-11.14** |

**Prohibición explícita:** no se aplica un plazo uniforme a toda la información (`RNF-CUM-14`). **Evidencia exigible por clase:** prueba en el límite de retención, recuperación dirigida y registro auditable de la eliminación, anonimización o agregación ejecutada.

**Archivo:** el remanente retenido no migrado vive en un repositorio consultable en formato abierto y documentado, **fuera del núcleo nuevo y fuera del sistema de 2012** (`C2 · Decisión 1, §15.1`, apartados b, c y d).

**Qué queda para Célula 3:** cifrado, KMS/HSM y gestión de secretos (`D1` / `ADR-009`); almacenamiento inmutable de archivo y respaldo (`C2`/`C3`); capacidad por clase de retención (`C4`).

* * *

### 5\.12 Volumetría actual, proyectada y de peak

**Estado:** `[COMPLETADO PROVISIONAL — depende de Célula 3, entrega no cerrada]`

**Documento de apoyo de Célula 3:** `C3 · Maestro §15` y `§15.1`, que reproducen las cifras de Célula 2 y advierten que son **insumos, no dimensionamiento final**, y `C3 · C4_DIMENSIONAMIENTO_Y_T11.md`, cuya cabecera pide «revalidar supuestos por dimensión antes de dimensionar; no son cálculos aprobados de Célula 3».

**Decisión asumida:** que las 18 dimensiones estimadas por Célula 2 sobreviven la revalidación de `C4`. **Qué habría que rehacer si cambian:** el dimensionamiento de almacenamiento por familia (sección 3), la retención en línea frente a archivo (sección 11) y la estrategia de particionamiento (sección 9).

**Base entregada por el CLIENTE** (`FEP03 CP, Cap. 14.1` — dato duro, no estimación): 780.000 TEU / 486.000 contenedores anuales → 920.000 / 570.000 a 3 años; 1.290.000 movimientos de patio → 1.480.000; 1.450 camiones/día promedio y hasta 2.600 en peak → 1.700 y 3.100; 2.400 tomas reefer → 2.900, con ≈2.150 conectadas simultáneamente en peak → ≈2.600; 26 tableros → 32; 74 equipos móviles a instrumentar → hasta 88; 14 navieras → 16; 142 cámaras → 190.

**Volumetría de sistema derivada** (`C2 · plantilla_volumetria_caso_portuaria.md` — 18 dimensiones del `CP, Cap. 14.2`, cada una con método y supuestos declarados):

| Dimensión | Actual | Proyección 3 años |
| --- | --- | --- |
| TPS de negocio en régimen normal | ≈0,11 | ≈0,13 |
| TPS en peak de coincidencia (dos naves \+ gate saturado) | ≈0,23 | ≈0,27 |
| Telemetría reefer reportada al núcleo | ≈7,2 ev/s | ≈8,7 ev/s |
| Telemetría reefer local (muestreo 1 min) | ≈35,8 ev/s | ≈43,3 ev/s |
| Posicionamiento de equipos móviles | ≈37 ev/s | ≈44 ev/s |
| Almacenamiento transaccional | ≈20 GB/año | ≈24 GB/año |
| Series temporales reefer | ≈68 GB/año (≈340 GB a 5 años) | ≈82 GB/año |
| Imágenes de reconocimiento | ≈1,4 TB/año | ≈1,6 TB/año |
| Histórico a migrar desde el TOS 2012 | ≈480 GB *(estimación gruesa, no verificada)* | — |
| Datos generados en 72 h sin enlace | ≈13 GB | \+15–20 % |
| Transferencia de sincronización implicada | ≈19,3 Mbps sostenidos para cumplir ≤90 min | igual |

**Factor estacional** (incorporado el 05\-sep, `CP, Cap. 14.2`, tercera particularidad): camiones ×1,79; volumen refrigerado mensual de enero a marzo ×2,48 frente al promedio. Aplica sobre las dimensiones dependientes del volumen operacional. **Consecuencia de calendario, no solo de capacidad:** la restricción no negociable N° 9 prohíbe intervenir entre el 15 de diciembre y el 30 de abril, de modo que toda holgura de almacenamiento debe estar instalada y verificada **antes del 15 de diciembre** de cada año.

**Los dos peaks son distintos y ambos deben declararse:** el de **coincidencia** fija el techo instantáneo; el **estacional** fija la carga sostenida durante cuatro meses y medio y es el que determina almacenamiento y retención en línea.

**Advertencia de honestidad:** ninguna de estas cifras es un dato del CLIENTE. Son estimaciones de Célula 2 con método declarado. El caso sanciona por igual la celda vacía y el valor sin derivación (`CP, Cap. 14.2`), pero también prohíbe presentar supuestos propios como hechos confirmados.

* * *

### 5\.13 Modelo conceptual de datos y diccionario inicial

**Estado:** `[PENDIENTE — decisión propia de Célula 4]`

**Obligación:** `FEP02 BTT, Cap. 5, RT-05.01` — modelo de datos documentado y **diccionario de datos con nombre, tipo, dominio de valores, obligatoriedad, propietario y sensibilidad de cada atributo**, con entregable asociado en el Sobre N° 2. Reforzado por `FEP01.26 BA, Art. 23°` (modelo normalizado donde corresponda, con linaje y propietario por dominio) y por el checklist interno del Subdocumento 5.

**Por qué es un pendiente propio:** el material no existe todavía en ninguna célula. Nadie más lo va a producir.

**Punto de coordinación que hay que resolver esta semana:** `C3 · A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md` incluye entre sus productos obligatorios un «Modelo conceptual de dominio y eventos», y el consolidado del Subdocumento 4 reserva la sección **4\.1.5 Modelo conceptual del dominio**. A la vez, `C3 · Maestro §16` declara que «**el Subdocumento 5 es propietario del modelo de datos detallado**, pero el Subdocumento 4 debe proveer almacenamiento, flujo, seguridad, despliegue, capacidad y continuidad coherentes». Hay que acordar explícitamente el corte: modelo conceptual de alto nivel en 4.1.5, modelo de datos y diccionario en el Subdocumento 5, **con los mismos nombres de negocio en ambos**. De lo contrario habrá dos modelos contradictorios en el mismo informe.

**Alcance mínimo del diccionario inicial:** para cada atributo — nombre, tipo, dominio de valores, obligatoriedad, propietario, sensibilidad, clase de retención y fuente de verdad. Debe cubrir al menos las entidades del núcleo de registro (contenedor, visita, movimiento, posición, custodia), reefer (toma, tablero, muestra, consigna, alarma), gate (camión, conductor, cita, documento, excepción), evidencia facturable y acceso e identidad.

* * *

## 4\. Supuestos identificados de Célula 4

Ninguno de estos está incrustado en el texto como hecho. Se declaran para poder retirarlos si cambian.

| ID | Supuesto | Origen | Si resulta falso |
| --- | --- | --- | --- |
| `SUP-C4-01` | La descomposición `DATA-CORE / DATA-TS / DATA-DOC / DATA-AN` sobrevive el cierre de Célula 3 | `C3 · Maestro §6.1` (catálogo lógico *inicial*, refinable) | Se rehace la matriz de familias, la separación de almacenamientos y el mapeo del diccionario |
| `SUP-C4-02` | La autoridad `dominio × zona × fase` de Célula 2 será la matriz que `A3` publique, sin cambiar la definición de zona ni de fase | `C2 · Decisión 1, §5.2`; `C3 · A3` (`POR COMPLETAR`) | Se rehace la sección de fuente de verdad y la conciliación de la migración |
| `SUP-C4-03` | El repositorio del histórico retenido es independiente del núcleo nuevo y del TOS apagado | `C2 · Decisión 1, §15.1`; `C3 · Maestro §8, punto 10` | Cambia la política de archivo y el dimensionamiento de retención |
| `SUP-C4-04` | Las cifras de volumetría de Célula 2 sobreviven la revalidación de `C4` | `C3 · C4`, cabecera de actualización | Cambia el dimensionamiento de almacenamiento, particiones y retención en línea |
| `SUP-C4-05` | RTO ≤4 h y RPO ≤15 min se mantienen como límites generales y no se endurecen | `C2 · RNF-DIS-13`; `C3 · Maestro §9.2` | Cambia la estrategia de replicación y respaldo, no la política de retención |
| `SUP-C4-06` | El muestreo reefer de dos capas (local 1–5 min / reporte 5–15 min) se mantiene como decisión vigente | `C2 · Decisión N° 8` | Cambian los volúmenes de series temporales y la sección de telemetría completa |
| `SUP-C4-07` | La frecuencia de 2 s del posicionamiento de equipos es un valor de diseño, no una decisión cerrada | `C2 · Volumetría, fila 5` (declarado «por validar») | Cambia el volumen de la familia de series temporales y el ancho de banda del patio |

* * *

## 5\. Información faltante, por célula

### Célula 3 — Arquitectura (entrega no cerrada)

| \# | Qué falta | Pregunta concreta que hay que hacerle |
| ---: | --- | --- |
| 1 | Matriz de autoridad `dominio × zona × fase` (`A3`, hoy `POR COMPLETAR`) | ¿Cuáles son las zonas y las fases nombradas de la matriz de autoridad, y confirman que la fuente de verdad de la posición del contenedor es la definida en la Decisión 1 §5.2 de Célula 2, sin redefinirla? |
| 2 | IDs definitivos de contextos lógicos (`A1`) | ¿Los identificadores `CTX-*` y `DATA-*` del Maestro §6.1 son los definitivos, o los van a refinar? Necesitamos congelar nombres de negocio comunes entre 4.1.5 y el Subdocumento 5. |
| 3 | Propiedad del modelo conceptual | ¿Quién publica el modelo conceptual de dominio: `A1` en la sección 4.1.5, o nosotros en el Subdocumento 5? Proponemos alto nivel en 4.1.5 y modelo de datos \+ diccionario en el 5, con nombres idénticos. |
| 4 | Mecanismo de integración y eventos (`A2` / `ADR-003`) | ¿Habrá bus/broker persistente con DLQ y *replay*, y CDC contra el TOS? De eso depende si el flujo hacia analítica es por eventos o por réplica. |
| 5 | Contratos por contraparte (`A2`, hoy `POR LEVANTAR`) | ¿Qué integraciones tendrán contrato confirmado antes del 7 de septiembre y cuáles quedan declaradas `POR LEVANTAR` en el Informe 1? |
| 6 | Emplazamiento (`C1` / `ADR-005`, Decisión 20 abierta) | ¿Qué almacenes quedan on\-premise, cuáles en nube y cuáles en el borde? Sin eso no podemos cerrar consistencia ni residencia de datos. |
| 7 | Productos y motores (`C2` / `ADR-007`) | ¿Van a nombrar productos de base de datos en el Informe 1, o solo capacidades? Nuestra sección 3 entrega la necesidad; el producto no debe elegirse antes. |
| 8 | Capacidad y almacenamiento por nodo (`C4`) | ¿Confirman las 18 dimensiones de volumetría de Célula 2 con el factor estacional, o las van a recalcular? |
| 9 | Cifrado de campo, KMS/HSM y logs inalterables (`D1` / `ADR-009/010`) | ¿Qué campos se cifran a nivel de campo y con qué mecanismo? Afecta directamente qué atributos podemos indexar. |
| 10 | Frontera del runtime local (`EDGE-RUN` / `ADR-002`) | ¿Qué datos persisten localmente durante las 72 h y cuál es el tamaño de buffer comprometido? |

### Célula 2 — Requerimientos (entrega cerrada, con vacíos declarados)

| \# | Qué falta | Pregunta concreta |
| ---: | --- | --- |
| 11 | No hay RNF de calidad de datos ISO/IEC 25012 | El catálogo de 91 RNF no cubre `FEP02 BTT, Cap. 5, RT-05.04`. ¿Lo asumimos íntegro en el Subdocumento 5, o crean un RNF de calidad para que quede trazado en el T\-12? |
| 12 | Catálogo de campos sensibles | `RNF-SEG-05` exige cifrar «el 100 % de los campos identificados como sensibles». ¿Existe esa lista, o la construimos nosotros en el diccionario de datos? |
| 13 | Banda y duración de `RN-11` | ¿La parametrización de la desviación de temperatura queda abierta en el Informe 1, o la acotamos a un rango justificado? |
| 14 | `RF-PAT-07` | Sigue declarado pendiente de validación interna. ¿Lo tratamos como vigente para el modelo de condiciones dinámicas del patio? |
| 15 | Evento del movimiento de grúa de muelle | El universo instrumentable de 74/88 equipos excluye las seis grúas de muelle. ¿De qué evento se deriva el movimiento de muelle en el modelo de datos? |

### Externos al equipo (CLIENTE, fabricantes)

| \# | Qué falta | Dónde está registrado |
| ---: | --- | --- |
| 16 | Esquema, calidad y tamaño reales de la base del TOS 2012 | `C2 · Registro de vacíos y consultas`; `C3 · Maestro §18, ESC-06` |
| 17 | Fecha exacta de fin de soporte del TOS | `C3 · Maestro §18, ESC-04` (escenario conservador 01\-01\-2028) |
| 18 | Existencia de interfaz por cada autoridad | `C3 · Maestro §18, ESC-14` |

* * *

## 6\. Riesgos por dependencia de Célula 3

| ID | Decisión asumida | Documento de origen | Qué pasa si cambia | Secciones afectadas | Mitigación de Célula 4 |
| --- | --- | --- | --- | --- | --- |
| `R-C3-01` | La capa de datos se descompone en `DATA-CORE / DATA-TS / DATA-DOC / DATA-AN` | `C3 · Maestro §6.1` | Se rehace la matriz de familias y el mapeo de cada entidad a su almacén | 5\.3, 5.5, 5.13 | Usar identificadores propios de Célula 4 (`DOM-*`) y mantener una tabla de equivalencia de una sola columna con los IDs de `A1` |
| `R-C3-02` | La matriz de autoridad `dominio × zona × fase` se publicará tal como la definió Célula 2 | `C3 · A3` (matriz `POR COMPLETAR`); `C2 · Decisión 1, §5.2` | Cambia la fuente de verdad durante coexistencia y la conciliación de la migración | 5\.2, 5.8, 5.4 | Escribir la fuente de verdad citando a Célula 2 como origen y a `A3` como confirmante; dejar zonas y fases parametrizadas, no enumeradas |
| `R-C3-03` | Habrá bus/broker persistente con DLQ y eventos como mecanismo de integración | `C3 · Maestro §6` capa 5; `ADR-003` en estado `CANDIDATO` | Si se opta por réplica/CDC sin eventos, cambia el flujo OLTP→analítica y la latencia declarada por indicador | 5\.5, 5.7, 5.9 | Declarar la latencia por indicador como requisito y no comprometer el mecanismo; presentar ambas rutas como alternativas |
| `R-C3-04` | El emplazamiento de los almacenes será híbrido con núcleo local para las cinco funciones críticas | `C3 · Maestro §§3 y 9.1`; `ADR-002` y `ADR-005` `CANDIDATO`; Decisión 20 abierta | Cambian consistencia, residencia de datos, replicación y el análisis CAP por operación | 5\.3, 5.4, 5.9, 5.12 | Escribir el análisis CAP por operación y no por producto; declarar la exigencia de que la operación de 72 h no dependa de la nube como restricción de entrada |
| `R-C3-05` | El repositorio del histórico retenido es independiente y consultable en formato abierto | `C2 · Decisión 1, §15.1`; `C3 · Maestro §8, punto 10` | Si se decide conservarlo dentro del núcleo, se rehace la política de archivo y el dimensionamiento | 5\.8, 5.11, 5.12 | Anclar la exigencia a `FEP02 BTT, Cap. 5, RT-05.06` y `RT-05.15`, que son normativas y no dependen de Célula 3 |
| `R-C3-06` | El cifrado a nivel de campo se resolverá con KMS/HSM sin restringir la indexación de campos operacionales | `C3 · D1`, `SEC-KEY-01`; `ADR-009` `CANDIDATO` | Si se cifran campos usados como clave de búsqueda, cae la estrategia de índices y los umbrales de ≤1 s | 5\.9, 5.10, 5.11 | Declarar explícitamente qué atributos son clave de acceso y pedir a `D1` una respuesta escrita antes de comprometer índices |
| `R-C3-07` | Las 18 dimensiones de volumetría de Célula 2 sobreviven la revalidación de `C4` | `C3 · C4`, cabecera; `C3 · Maestro §15` («insumos, no dimensionamiento final») | Cambia el dimensionamiento de almacenamiento por familia y la frontera entre retención en línea y archivo | 5\.11, 5.12, 5.9 | Presentar la volumetría como rango con método declarado; no convertir estimaciones propias en cifras del CLIENTE |
| `R-C3-08` | RTO ≤4 h / RPO ≤15 min y respaldo 3\-2\-1\-1\-0 se mantienen | `C3 · Maestro §9.2`; `C2 · RNF-DIS-13/14/15` | Un endurecimiento cambia replicación y capacidad de respaldo, no la política de retención | 5\.4, 5.11 | Separar en el texto la *política* (nuestra) de la *materialización* (de Célula 3) |
| `R-C3-09` | El modelo conceptual de 4.1.5 y el del Subdocumento 5 usarán los mismos nombres de negocio | `C3 · A1`, productos obligatorios; `C3 · Maestro §16` | Dos modelos contradictorios en el mismo Informe 1, penalizado como incoherencia | 5\.1, 5.13 | Acordar el corte por escrito antes del 7 de septiembre y fijar un glosario común de una página |
| `R-C3-10` | Célula 3 alcanzará a integrar contenido aprobado antes de la entrega | `C3 · 90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md` (nueve secciones `PENDIENTE DE INTEGRAR`) | Si el Subdocumento 4 llega incompleto, todo lo provisional del 5 queda sin confirmante | 5\.3, 5.5, 5.9, 5.12 | Redactar cada sección provisional de modo que se sostenga por sí sola con fuentes normativas, y marcar la dependencia como supuesto declarado, nunca como hecho |

* * *

## 7\. Verificación final

### 7\.1 Cobertura del checklist oficial

Contrastado uno a uno contra `FEP01.26 BA, Form. T-7, Subdoc. 5` (seis viñetas) y contra el checklist interno de 20 casillas de `informe_1_requisitos_y_estructura.md, §5.5`\:

| Casilla del checklist interno | Sección de este esqueleto |
| --- | --- |
| Identificación de dominios de información | 5\.1 |
| Modelo conceptual de datos | 5\.13 |
| Diccionario inicial de datos | 5\.13 |
| Fuente oficial y propietario de cada dominio | 5\.2 |
| Fuente de verdad de la posición del contenedor | 5\.2 |
| Paradigma de persistencia y motores propuestos | 5\.3 |
| Justificación relacional o no relacional | 5\.3 |
| Transaccionalidad, consistencia y disponibilidad | 5\.4 |
| Estrategia de migración | 5\.8 |
| Saneamiento, validación y conciliación | 5\.8 |
| Índices, particiones, caché y consultas | 5\.9 |
| Separación transaccional / temporal / analítico | 5\.5 |
| Telemetría de tomas, tableros y equipos móviles | 5\.6 |
| Frecuencia de muestreo | 5\.6 |
| Retención por tipo de dato | 5\.11 |
| Calidad conforme a ISO/IEC 25012 | 5\.10 |
| Auditoría y trazabilidad | 5\.10 |
| Archivo y eliminación segura | 5\.11 |
| Volumetría actual, proyectada y de peak | 5\.12 |
| Integración e interoperabilidad de datos | 5\.7 |

**20 de 20 casillas cubiertas. Ningún ítem quedó fuera.** El punto de integración e interoperabilidad (5.7) no aparece como casilla propia en el checklist interno pero sí en `FEP02 BTT, Cap. 5, num. 5.3`, y se conserva.

### 7\.2 Ningún `[COMPLETADO]` sin cita verificable

Las cinco secciones marcadas `[COMPLETADO]` (5.1, 5.2, 5.4, 5.6, 5.8, 5.11) citan documento \+ capítulo/numeral \+ código \+ materia. Las citas fueron verificadas abriendo los archivos, no reproducidas de memoria. La única cita de segunda mano es la retención de logs de seguridad, que la guía de arranque atribuía a la matriz de retención general: su fuente real es `FEP02 BTT, Cap. 11, RT-11.14`, y así queda corregida.

### 7\.3 Nada apoyado en Célula 3 quedó como definitivo

Las cuatro secciones provisionales (5.3, 5.5, 5.9, 5.12) declaran documento de apoyo, decisión asumida y consecuencia del cambio. Los siete supuestos de la sección 4 están enunciados como supuestos, no incrustados en el texto. Los diez riesgos de la sección 6 tienen mitigación asignada a Célula 4, no a Célula 3.

### 7\.4 Contenido no inventado

No se propone ningún motor de base de datos, producto comercial, cifra de volumetría, contrato de integración ni política de emplazamiento que no esté respaldado por una fuente citada. Donde el respaldo no existe, la sección quedó marcada como pendiente en lugar de completarse por cuenta propia.
