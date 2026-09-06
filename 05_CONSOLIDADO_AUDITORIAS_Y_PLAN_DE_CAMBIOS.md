# Consolidado de las tres auditorías de Célula 3 y plan único de cambios

**Autor:** Frente 2 (Física y Despliegue).
**Fecha:** 2026-09-06.
**Rama:** `consolidacion_f2_f3`, commits `f0abf1c` (merge de Frente 3) y `702663f` (integración de sus hallazgos).
**Qué es:** el contraste de los tres documentos de auditoría que hoy existen sobre Célula 3, con verificación propia de cada hallazgo contra la fuente, y un plan de corrección único con dueño.

## 0. Antes de leer nada más: las tres auditorías miraron árboles distintos

Esto no es un detalle de Git; cambia el veredicto de siete hallazgos.

| Auditoría | Autor | Qué árbol leyó | Consecuencia |
|---|---|---|---|
| `04_AUDITORIA_CRUZADA_A_C_D.md` | Frente 1 | `frente_1` propia, `origin/frente_2` y `origin/frente_3` | leyó C1–C4 **sin** las correcciones del 06-09 |
| `AUDITORIA_GLOBAL_CELULA3_PRE_D3.md` | auditoría global pre-D3 | `frente_3`, commit `bb3da8a` | ídem: la copia de C1–C4 dentro de `frente_3` era una copia manual anterior |
| Este documento | Frente 2 | `consolidacion_f2_f3` tras `702663f` | árbol vigente, con Frentes 2 y 3 integrados |

Ninguna de las dos auditorías externas pudo ver las correcciones `F2-COR-005`, `F2-COR-006`, `F2-COR-007`, `F2-INT-003` ni `F2-ESC-017`, aplicadas ese mismo día. **Los hallazgos siguen siendo correctos; lo que cambia es su estado.** Cerrar esa diferencia primero evita que el equipo vuelva a trabajar sobre siete asuntos ya resueltos.

Regla que se aplicó aquí, tomada del numeral 11 de la auditoría global y compartida: no se cuenta por cantidad de hallazgos. **Cada hallazgo dirigido a este frente se verificó contra la fuente primaria antes de darlo por bueno o por cerrado**, y donde una auditoría se equivocó se dice cuál y por qué.

## 1. Cuadro maestro

Leyenda de verificación: `✔` verificado contra la fuente y confirmado · `≈` confirmado con matiz · `✘` no se confirma.

### 1.1 Ya cerrados en la rama vigente — no volver a trabajarlos

| # | Hallazgo | Quién lo levantó | Verif. | Estado hoy |
|---|---|---|---|---|
| 1 | `CTX-VESSEL` crítico y local en A1/A3, solo en nube en C1 | `AGC3-003` (CRÍTICO) · `F-1` · D2 `B6-F03` | ✔ | **CERRADO** `F2-COR-005`. `PHY-OPS-01` lo incorpora; C1 §5 y §5.1 |
| 2 | Seis diferencias de criticidad A1↔C1 | `AGC3-006` · `F-2` · D2 `B6-F04` | ✔ | **CERRADO** `F2-COR-006`. C1 adopta A1 y declara el criterio |
| 3 | `SRV-IAM` crítica en C1 / alta en A1 | ídem | ✔ | **CERRADO en la tabla**; abierto como propuesta `F2-ESC-017` hacia Frente 1 |
| 4 | `CH-CAB` reducido al muelle | `AGC3-007` · `F-3` · D2 `B6-F04` | ✔ | **CERRADO** `F2-COR-006`. `PHY-EDG-04` + `-02` + `-01` |
| 5 | Doble conteo `T11-C2-19` / `T11-SEC-04` | `AGC3-009` · `F-5` · D2 `B6-F05` | ✔ | **CERRADO por fusión** `F2-COR-007`. Ver 1.3 #16 y #17: dos partes de `AGC3-009` siguen abiertas |
| 6 | Colisión de IDs `SPOF-*` entre C1 y D2 | `X-1`, declarado «el hallazgo más importante que ningún frente había detectado» | ≈ | **YA ESTABA CERRADO** el 06-09 como `F2-ESC-014`: C1 renumeró a `F2-SPOF-01..10`. El fondo es correcto; la atribución de novedad no. Ver §3 |
| 7 | Lado físico de la brecha `ACT-TI` | `AGC3-008` · `F-4` · D2 `B6-F04` | ✔ | **CERRADO el lado físico** `F2-INT-003`, C1 §5.2: no hay nodo nuevo ni fila nueva de T-11. El lado A1 sigue abierto |
| 8 | `ADR-011` sin alternativas concretas | `AGC3-010` · D2 `B7.2 #8` | ✔ | **CERRADO hasta donde el Informe 1 permite**: C2 §4.1, seis alternativas en dos ejes. Queda 1.3 #18 |
| 9 | `SPOF-13` y `SPOF-22` no deben consolidarse | D2 `B7-O01` | ✔ | **CONFIRMADO y declarado** en C2 §4.1 |

### 1.2 Confirmados, abiertos, del Frente 2 — se corrigen aquí

| # | Hallazgo | Fuente | Verif. | Qué verifiqué exactamente |
|---|---|---|---|---|
| 10 | **La jerarquía contractual está invertida en nuestro registro** | `AGC3-001` (CRÍTICO) | ✔ | `02_Frente_Fisica_Despliegue/trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md` línea 3 dice: «`00_MAESTRO`, §1: ante contradicción prevalecen los PDF oficiales (`FEP03` > `FEP02` > `FEP01`)». El Maestro §1 dice **lo contrario**: «La precedencia contractual es la del FEP01, Art. 5.1–5.4. Las Bases Administrativas y sus anexos ocupan el primer lugar». No es solo un error: **le atribuimos al Maestro algo que el Maestro no dice** |
| 11 | `TRZ-C1-001` cita una familia `RNF-ARQ` que no existe | `AGC3-016` | ✔ | La propia Matriz Global `GTR-002` dice «no existe categoría RNF-ARQ en C2» |
| 12 | Enlace roto en C4 §10 | `AGC3-017.3` | ✔ | `../../90_Consolidado/…` desde `Celula3/02_Frente_Fisica_Despliegue/` resuelve fuera de `Celula3`. Correcto: `../90_Consolidado/…` |
| 13 | Doble «Definición de terminado» en C1–C4 | `AGC3-019` | ✔ | Dos bloques por documento: el del contrato (sin marcar) y el de estado (marcado). Un lector automático concluye pendiente y cumplido a la vez |
| 14 | `AUDITORIA_CIERRE.md` del Frente 2 es una plantilla vacía | `AGC3-013` · `G-5` | ✔ | 11 controles, todo `☐`/`PENDIENTE`, revisor `POR ASIGNAR` |
| 15 | Ninguna traza del Frente 2 está promovida | `AGC3-014` | ✔ | 98 filas `TRZ_C1..C4`, **0 en `APROBADO`** |
| 16 | C4 cuenta *todas* las transacciones de negocio como eventos de seguridad | `AGC3-009` (parte b) | ✔ | §9.ter suma ≈9.410/día de `DIM-01`. D1 `B5.2.1` admite al 100 % seguridad y auditoría, y prioriza fallos y anomalías. Sin esa línea el piso baja a ≈12.300 ev/día. **El error infla, no subestima** —es conservador para capacidad— pero el método no es el de D1 |
| 17 | La conclusión sobre los ≈50 GB locales es categórica sin base | `AGC3-009` (parte c) | ✔ | §9.ter afirma «no hay que reabrir el dimensionamiento» y en el párrafo siguiente reconoce que falta el término dominante. Las dos frases no pueden ser ciertas a la vez |
| 18 | Menciones desincronizadas de `ADR-011` | `AGC3-010` | ✔ | C2 §4 sigue diciendo «no existe un ADR asignado»; el DoD de C2 dice «propuesto, no abierto». El Registro ADR Global ya lo tiene como `CANDIDATO` |

### 1.3 Hallazgos nuevos de la capa mecánica — ninguna de las otras dos auditorías los tiene

La verificación mecánica se corrió sobre los 38 documentos de `Celula3/` (≈8.700 líneas) contra el texto de las tres bases. Cinco hallazgos y tres confirmaciones positivas.

| # | Hallazgo | Sev. | Evidencia |
|---|---|---|---|
| 19 | **`T11-C3-01` y `T11-C3-03` son identificadores huérfanos, y `T11-C3-02` no existe** | ALTO | C4 §9 y `TRZ_C4` los citan como origen de dos filas. **C3 nunca publica una tabla de candidatos T-11 con identificador**: su §13 los enumera en prosa, y son cinco, no tres. Tres de los cinco no tienen ID en ninguna parte. Esto **rompe el control 1:1 que C4 §10 declara «cumple»** en dos de sus seis filas |
| 20 | **C2 conserva el rango truncado `RT-06.01..24` en sus reglas normativas** | ALTO | Línea 58, bloque «Reglas importantes» del contrato: *«Si se propone sala principal sustantiva, aplicar RT-06.01..24 íntegros»*. `F2-COR-002` agregó una **nota** de corrección en la línea 16 pero **dejó la regla equivocada en pie**. Es el mismo defecto que `AGC3-019` describe para el DoD, aplicado al alcance del Capítulo 6, y es la cuarta aparición del rango truncado —Maestro §10.3, contrato de C2, D2 §B5 y esta— |
| 21 | **Cinco correcciones mayores de Célula 2 no las cita ningún frente de Célula 3** | ALTO | `MC-16`, `MC-17`, `MC-22`, `MC-28` y `MC-29`. Célula 3 cita 25 de las 30. Dos son materia directa nuestra: **`MC-16`** —«el congelamiento y la ventana de nave restringen intervenciones *técnicas*, no la asignación operacional de equipos»— es exactamente el calendario de C3 §12; **`MC-17`** creó `RNF-OPE-11` con tres clases críticas de soporte y respuesta diferenciada, que es materia de C3 §11 y de D1. `MC-28` toca la coexistencia del TOS en A3 |
| 22 | Citas ambiguas de códigos colisionados en cuerpo sustantivo | MEDIO | Contra la regla del Maestro §1.1, que exige *documento + capítulo + código + materia*. Casos reales, no de registro: C4 §9 «es una decisión de las bases (`RT-05.10`)» —materia del **caso**, no del BTT—; C4 §9.ter «`RT-09.01` obliga a presentar el cálculo» —materia del **BTT**, no del caso—; C1 §7 tabla de sala, fila `RT-06.01`; `TRZ-C4-017` y `TRZ-C4-031` |
| 23 | El enlace roto de `AGC3-017.1` apunta a un archivo que no existe en esta rama | MEDIO | `00_Gobierno/05_REGISTRO_ALINEACION_CELULA2.md` no está en `consolidacion_f2_f3`: `00_Gobierno/` tiene cuatro archivos, del `00_` al `03_`. O vive solo en otra rama, o la ruta es incorrecta. **No verificable aquí** |

**Y la lista definitiva de colisiones `RT`, que es un producto en sí mismo (#24).** Se extrajeron los 374 códigos del BTT y los 27 del Caso 06 y se compararon materia contra materia. Resultado: **los 27 códigos del Capítulo 15 reutilizan códigos del BTT, y en 11 la materia es distinta.** No cinco, como dice el Supuesto M de Célula 2; no diez, como decía nuestro recordatorio.

| Código | Materia en el BTT | Materia en el Caso 06, Cap. 15 |
|---|---|---|
| `RT-03.13` | declarar qué funciones **no** estarán disponibles offline | sincronización tras reconexión ≤90 min |
| `RT-03.24` | calidad de servicio y priorización de tráfico | rediseño de la red del patio |
| `RT-05.10` | catálogo de datos con linaje automatizado | retención de históricos y de auditoría |
| `RT-05.15` | históricos **no** migrados accesibles en repositorio | históricos **a** migrar |
| `RT-06.01` | encabezado de rango del numeral 6 | tipología del emplazamiento on-premise |
| `RT-09.01` | presentar el cálculo de capacidad con supuestos | transacción operacional crítica ≤1 s |
| `RT-15.02` | apagar ambientes no productivos fuera de horario | certificaciones sectoriales del adjudicatario (ISPS) |
| `RT-16.14` | motor de reglas sin recompilación | firma electrónica |
| `RT-16.21` | plantillas de notificación administrables | canales de notificación y escalamiento |
| `RT-16.30` | registro de exportación de información sensible | portal público |
| `RT-21.06` | SLA del centro de atención (80/20, FCR 70 %, abandono ≤5 %) | horario del centro de atención |

Dos casos que **no** son colisión pero deben registrarse aparte, porque un lector los tomaría por una:

- **`RT-13.12`** — el caso conserva la materia (multiidioma) pero **cambia su clasificación**: el BTT lo declara *Deseable* y el caso dice, literalmente, «Obligatorio, y no deseable como en el documento transversal». Es el único código del caso que reclasifica explícitamente al BTT.
- **`RT-21.16`** — el caso declara «no exigible en los términos del documento transversal» el traslado de especialistas a sitios alejados, porque toda la operación ocurre en un emplazamiento. Es una constatación fáctica, no un rebaje del piso transversal, pero conviene decirlo así para que nadie lo lea como una rebaja contraria a `FEP02 §1.3`.

**Confirmaciones positivas de la capa mecánica**, que valen tanto como los defectos porque acotan dónde *no* hay que buscar:

| # | Verificación | Resultado |
|---|---|---|
| 25 | 970 citas de código `RT` en Célula 3 | **0 códigos inexistentes.** Ninguno de los tres frentes inventó un código |
| 26 | Cifras del caso replicadas entre frentes | **consistentes**: 780.000 TEU, 486.000 contenedores, 620 naves, 1.450→2.600 camiones, 2.400 tomas, 26→32 tableros, 142 cámaras, 18 ha, 34 m², 74→88 equipos, TI = 5 personas. Sin discrepancia entre A, C y D |
| 27 | Integridad de tablas markdown en los 38 documentos | **0 tablas con columnas descuadradas** |
| 28 | Enlaces markdown, con des-escape de `%20` | **2 rotos reales**, no 3: `A2` línea 83 y `C4` línea 369. Los otros cinco que aparecen en un barrido ingenuo son falsos positivos por codificación de espacios |
| 29 | Continuidad de numeración de catálogos | `THR-001..073`, `SPOF-01..22`, `F2-SPOF-01..10`, `ADR-001..011`, `FL-01..11`, `SCN-01..12`, `DIM-01..18`, `GTR-001..019`, `STD-01..20`: **todos continuos, sin huecos ni duplicados**. La única excepción es `T11-C3-*`, hallazgo #19 |
| 30 | Los 16 actores `ACT-*` | los 16 existen y los 16 son usados por más de un frente |

## 2. Hallazgos dirigidos a otros frentes: verificación independiente

No los corrijo —no son míos— pero los verifiqué contra la fuente para que sus dueños no tengan que hacerlo dos veces.

| Hallazgo | Fuente | Verif. | Lo que dice el texto original |
|---|---|---|---|
| **A1 cuenta la baja de identidad desde la reconexión** | `AGC3-002` (CRÍTICO) | ✔ | `FEP02 RT-12.10`: *«baja efectiva en un plazo no superior a 24 horas **desde la desvinculación**»*. Con un corte de 72 h, contar desde la reconexión permite hasta 96 h. **Es un incumplimiento de requisito obligatorio, no una diferencia de criterio.** Toca a Frente 1 y condiciona `ADR-008` |
| **Célula 2 intercambió `RT-11.18` y `RT-11.19`** | `AGC3-011` · nuestro recordatorio, punto 6 | ✔ | `RT-11.18` = incidente **crítico** comunicado ≤2 h. `RT-11.19` = **brecha** notificada ≤24 h y causa raíz ≤5 días hábiles. `RNF.md` los tiene cruzados. Tercera confirmación independiente del mismo defecto |
| **`RT-11.27` mal aplicado a `SEC-IAM-01` en D1** | `X-2` | ✔ | `RT-11.27` trata **exclusivamente** del acceso de personas desarrolladoras a producción. `SEC-IAM-01` cubre identidad de todos los actores. La cita correcta para esa materia es `RT-12.01`, `RT-12.03`, `RT-12.05` y `RT-12.11`. Frente 1 tiene razón |
| **`FL-01..11` sin definición formal** | `X-3` | ✘ | **No se confirma como está enunciado.** `FL-01..11` **sí está definido**, en D1 §B3, con zona de origen, zona de destino, componentes y controles por flujo; C3 §5.bis lo consume por ID. Lo que no existe es el mapeo de los **22 flujos AS-IS del Anexo A que describe A2** a esos once. El hallazgo real es más chico y tiene otro dueño: A2 debe declarar la correspondencia, o decir que no la hay porque son cortes distintos —flujos de negocio frente a flujos de red— |
| **Tres versiones del Registro ADR Global** | `G-1` (CRÍTICO) | ≈ | El fondo es correcto y sigue vigo: nadie ha fusionado conscientemente. **Pero el cuadro de tres columnas ya quedó desactualizado**: al mergear Frente 3 se tomó su versión, que es la más desarrollada —incorpora `ADR-011` y los anclajes—, de modo que en la rama vigente hay **dos** versiones, no tres. Y el merge trajo un cambio que nadie discutió: `ADR-002`, `-003` y `-004` bajaron de `CANDIDATO` a `PROPUESTO`. Se deja registrado, no resuelto: es del integrador |
| **`Celula2/RECORDATORIO_ANTES_DE_ENTREGA.md` no existe** | `AGC3-018` | ✘ | **Sí existe**, desde el commit `5ba5c6d`. No estaba en `frente_3`, que es donde se auditó. La evidencia es reproducible en la rama de consolidación |
| **La Matriz Global no representa el avance** | `AGC3-005` | ✔ | 19 filas `GTR`, **12 celdas `POR DEFINIR` y 37 `PENDIENTE`**, mientras A1–C4 ya tienen componentes, nodos y cálculos. Es del integrador |
| **Faltan BA Art. 77 y 84–86 en la traza** | `AGC3-012` | ✔ | Reversibilidad, propiedad y licencias, tratamiento de datos e IA. Ningún frente los ancla. Afecta directamente a `ADR-011` y al T-11: el **escrow semestral del Art. 84** es una obligación con costo que hoy no tiene fila |

## 3. Dónde las auditorías se contradicen, y cuál gana

Cuatro casos. En todos se dice qué se verificó, no quién tiene más autoridad.

**a) La colisión `SPOF`.** Frente 1 la presenta como *«el hallazgo más importante que ningún frente había detectado todavía»*. El fondo es correcto y la tabla comparativa es buena. Pero el Frente 2 ya la había detectado y cerrado ese mismo día: `F2-ESC-014`, renumeración a `F2-SPOF-01..10`, con la razón declarada —D2 es dueño del registro consolidado porque es su producto obligatorio— y con cuatro puntos de falla suyos que faltaban en D2 identificados de vuelta. Frente 1 leyó `origin/frente_2`, que no tenía la corrección. **No cambia el hallazgo; cambia quién debe actuar: nadie, ya está hecho.**

**b) `FL-01..11`.** Frente 1 dice que el identificador no tiene definición formal. Lo tiene, en D1. El hallazgo real es la ausencia de correspondencia entre los 22 flujos AS-IS de A2 y los once flujos de red de D1 — y no es seguro que deba existir, porque son cortes distintos. **Gana la verificación: el enunciado se corrige antes de accionarlo.**

**c) La madurez del Frente 2.** Frente 1 califica su auto-auditoría de «baja» porque `AUDITORIA_CIERRE.md` está vacío. Es literalmente cierto y el hallazgo se acepta (#14). El matiz: el frente sí corrió un proceso, solo que en otro archivo — `DECISIONES_Y_ESCALAMIENTOS.md` tiene 253 líneas con 17 escalamientos, 7 correcciones propias y 4 integraciones, cada una con su verificación. **Lo que falta no es la revisión, es el formato de cierre y, sobre todo, el revisor independiente**, que es lo que ninguna cantidad de auto-revisión sustituye.

**d) El estado de `ADR-011`.** La auditoría global pide «al menos dos alternativas reales con proveedor/regiones disponibles, latencia, dominios de fallo, residencia, intensidad de carbono, catálogo, costo cualitativo y salida». C2 §4.1 llega hasta donde el Informe 1 permite: seis alternativas nombradas en dos ejes, con la consecuencia que decide cada una, los tres datos que faltan y una recomendación condicionada. **No se nombran proveedores ni se inventan latencias**, porque ninguna de las tres bases los entrega y la regla 4 del Maestro lo prohíbe. La propia auditoría lo admite en su última frase: *«si el dato de mercado/CLIENTE aún falta, dejar criterios y consulta, sin promoverlo a PROPUESTO»*. Se acata: el ADR sigue `CANDIDATO`.

## 4. Lo que está bien y debe defenderse tal como está

Un informe de auditoría que solo lista defectos deja al equipo sin saber qué proteger. Esto resistió las tres revisiones:

- **La cadena `fuente → componente → nodo → cálculo → T-11` existe de verdad**, con 970 citas verificadas y cero códigos inventados. Es lo que el `RT-09.01` del BTT y el Art. 16.2 de las BA piden demostrar, y es lo que la mayoría de las ofertas no puede.
- **Las cifras del caso son las mismas en los tres frentes.** No hay dos volumetrías compitiendo.
- **Ninguna auditoría encontró una cifra inventada.** D2 lo verificó explícitamente en `B7.2 #12`, Frente 1 no reportó ninguna, y la revisión de D1 `B7-F12` tampoco. Los rangos y supuestos están marcados como tales.
- **Los tres frentes declararon sus contradicciones en lugar de resolverlas en silencio**, que es la regla del README. Es la razón por la que estas tres auditorías tienen algo que cruzar.
- **Lo diferido se difirió por decisión, no por olvido**: los diagramas esperan a que los identificadores se estabilicen. Las tres auditorías coinciden en que es lo correcto, y `AGC3-020` lo dice mejor que nadie: dibujar antes cristalizaría las contradicciones.

## 5. Plan único de cambios

Se conserva la estructura de olas de la auditoría global, porque es buena, y se le agregan los hallazgos que faltaban con su dueño real.

### Ola 1 — Correcciones internas que no dependen de nadie

| # | Acción | Dueño | Origen |
|---|---|---|---|
| 10 | Sustituir `FEP03 > FEP02 > FEP01` por la regla real del Maestro §1 / `BA Art. 5.1–5.4` | **Frente 2** | `AGC3-001` |
| 20 | Corregir `RT-06.01..24` → `RT-06.01..34` en la línea 58 de C2, no solo en la nota | **Frente 2** | nuevo, #20 |
| 11 | Retirar `RNF-ARQ` de `TRZ-C1-001` y citar `RT-02.01` del BTT | **Frente 2** | `AGC3-016` |
| 12 | Corregir el enlace de C4 §10 a `../90_Consolidado/…` | **Frente 2** | `AGC3-017.3` |
| 22 | Desambiguar las citas de códigos colisionados en cuerpo sustantivo | **Frente 2** | nuevo, #22 |
| 24 | Publicar la lista verificada de **11 colisiones** + los 2 casos especiales, y reemplazar con ella el Supuesto M | Frente 2 → Célula 2 e integrador | nuevo, #24 |
| 13 | Rotular el DoD del contrato como plantilla normativa y dejar una sola tabla de estado vigente | **Frente 2** | `AGC3-019` |
| — | Corregir el reloj de baja de identidad en A1 (`RT-12.10`, desde la desvinculación) | **Frente 1** | `AGC3-002` |
| — | Retirar `RT-11.27` de `SEC-IAM-01` | **Frente 3** | `X-2` |
| — | Corregir el enlace de A2 §1.1 | **Frente 1** | `AGC3-017.2` |
| — | Actualizar el estado vigente del encabezado de D2 | **Frente 3** | `AGC3-015` |
| — | Intercambiar las referencias `RT-11.18`/`RT-11.19` en `RNF.md` | **Célula 2** | `AGC3-011`, recordatorio #6 |
| — | Maestro: rango `RT-06.01..34`, Cap. 7 completo, checklist de 28 entregables, commit de corte y cifras 139/91/11 | **Integrador** | `AGC3-004`, `G-2`, `G-3`, `F2-ESC-003/004/005/007` |

> **Estado de la Ola 1 al 2026-09-06.** Las siete acciones del Frente 2 —#10, #20, #11, #12, #22, #24 y #13— **ya están aplicadas** en `consolidacion_f2_f3`, registradas como `F2-COR-008` a `F2-COR-011` y `F2-ESC-006 bis`. Las demás filas siguen pendientes de sus dueños.

### Ola 2 — Consistencia semántica

| # | Acción | Dueño | Origen |
|---|---|---|---|
| 19 | **Publicar en C3 §13 la tabla de candidatos T-11 con identificador**, cinco filas, y reconciliar `T11-C3-01..05` con lo que C4 §9 cita | **Frente 2** | nuevo, #19 |
| 16 | Separar en C4 §9.ter las transacciones con requisito de auditoría o no repudio del total de `DIM-01`, según la política de D1 `B5.2.1` | **Frente 2** | `AGC3-009b` |
| 17 | Retirar la conclusión categórica sobre los ≈50 GB y dejarla condicionada a la medición | **Frente 2** | `AGC3-009c` |
| 18 | Sincronizar todas las menciones de `ADR-011` con su estado `CANDIDATO` | **Frente 2** | `AGC3-010` |
| 21 | Incorporar `MC-16` y `MC-17` a C3 (calendario y clases de soporte); trasladar `MC-28` a A3 y `MC-22`/`MC-29` a D1 y a la oferta | **Frente 2 y quien corresponda** | nuevo, #21 |
| 3 | Resolver `F2-ESC-017`: ¿`SRV-IAM` sube a `Crítica`? | **Frente 1**, con D1 y `ADR-008` | `F2-ESC-017` |
| 7 | Cerrar el lado lógico de `ACT-TI`: cuarto canal o especialización declarada | **Frente 1**, con D1 | `F1-OBS-002`, `AGC3-008` |
| — | Declarar la correspondencia entre los 22 flujos AS-IS de A2 y `FL-01..11` de D1, o por qué no la hay | **Frente 1**, con D1 | `X-3` corregido |
| — | Reconstruir el Registro ADR Global fila por fila y explicar la baja de `ADR-002/003/004` a `PROPUESTO` | **Integrador** | `G-1`, observación del merge |
| — | Anclar `BA Art. 77, 84, 85 y 86`; el escrow semestral necesita fila de T-11 o exclusión justificada | **Integrador**, con C2/C4 y D1 | `AGC3-012` |

### Ola 3 — Trazabilidad, cierre y revisión independiente

| # | Acción | Dueño | Origen |
|---|---|---|---|
| 14 | **Ejecutar el `AUDITORIA_CIERRE.md` del Frente 2** con evidencia por control y veredicto | **Frente 2** | `AGC3-013`, `G-5` |
| 15 | Revisar las 98 trazas y promover solo las comprobadas; el resto, `BLOQUEADO EXTERNO TRATADO` con dueño, hito y fallback | **Frente 2** | `AGC3-014` |
| — | Lo mismo en Frente 1 | **Frente 1** | `AGC3-013` |
| — | **Nombrar revisores cruzados**: hoy los tres frentes se auto-revisan. La tabla de control del Plan sigue en `POR ASIGNAR` | **Líder de proyecto** | `G-5`, `AGC3-013` |
| — | Actualizar `GTR-001..019`: 12 `POR DEFINIR` y 37 `PENDIENTE` | **Integrador** | `AGC3-005` |
| — | Construir el T-11 de trabajo con las 29 filas candidatas y su control 1:1 bidireccional | **Integrador**, con C2/C4/D1 | `AGC3-022` |
| — | Formalizar los 22 SPOF: aceptación o escalamiento, nunca «cerrado» por estar descrito | **Frente 3** y CLIENTE | `AGC3-021` |

### Ola 4 — Representación y cierre

Sin cambios respecto de la auditoría global: diagramas con identificadores ya estables, B8 de D1/D2, D3, y solo entonces el Subdocumento 4 y el T-11 final de cinco columnas.

## 6. Lo que este consolidado no hace

No corrige ningún archivo de otro frente. No aprueba ni cierra nada: los tres frentes siguen sin revisor independiente, y eso no lo arregla una cuarta auditoría escrita por uno de ellos. No sustituye a D3, que es la puerta formal. Y no toca el Subdocumento 5 ni la Oferta Económica, que están fuera de Célula 3.

Tres asuntos quedan **registrados sin resolver, a propósito**, porque resolverlos aquí sería exactamente lo que el README prohíbe: la baja de `ADR-002/003/004` a `PROPUESTO` que trajo el merge; si `SRV-IAM` sube a `Crítica`; y si los 22 flujos de A2 deben mapearse a los `FL-*` de D1.
