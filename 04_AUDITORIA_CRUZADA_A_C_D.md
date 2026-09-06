# Auditoría cruzada de consistencia — Frentes A (Lógica e Integración), C (Física y Despliegue) y D (Seguridad y Consolidación)

**Autor:** Frente 1 (Lógica e Integración), por pedido explícito de auditar los tres frentes, no solo el propio.
**Fecha:** 2026-09-06.
**Método:** lectura completa de los diez paquetes vigentes (A1-A3, C1-C4, D1-D3) y de sus trazabilidades, escalamientos y auditorías internas, comparando ramas vía `git show`/`git diff` de solo lectura — **no se trajo ningún archivo de otra rama al árbol de trabajo, no se hizo commit ni merge**. Fuentes exactas:

| Frente | Rama usada | Motivo |
|---|---|---|
| A1/A2/A3 | `frente_1` (local, la propia) | es la versión vigente, con las correcciones de la auditoría cruzada anterior ya aplicadas |
| C1-C4 | `origin/frente_2` | tiene v0.5 completo; `origin/consolidacion_f2_f3` está desactualizada frente a ella |
| D1-D3 | `origin/frente_3` | tiene la integración documental D1-D2 más reciente (bloque B7-R/B7-C), posterior a `origin/consolidacion_f2_f3` |
| Gobierno (Maestro, Matriz Global, Registro ADR) | `origin/frente_3` para lectura comparativa; `frente_1` es la que se edita | ver hallazgo G-1 sobre divergencia |

**Qué NO hace este documento:** no resuelve ningún conflicto de otro frente, no edita C1-C4 ni D1-D3, y no sustituye la auditoría propia de cada frente (`AUDITORIA_CIERRE.md` de C y de D) ni el trabajo del integrador. Es un insumo adicional, cruzado, para la puerta de integración. Los hallazgos que ya estaban documentados por Frente 2 o Frente 3 en sus propios archivos se citan como tales, no se readjudican como propios.

---

## 0. Resumen ejecutivo

| Frente | Madurez de contenido | Madurez de auto-auditoría | Traza completa | Observación |
|---|---|---|---|---|
| **A** (A1/A2/A3) | Alta — 3/3 entregables completos, con múltiples rondas de auditoría cruzada previas | Alta — auditado repetidamente por su propio autor contra fuentes primarias | Sí (`TRZ_A1/A2/A3.md`) | Ver hallazgos A-1..A-3 (propios, no resueltos aún) |
| **C** (C1-C4) | Alta — 4/4 entregables en `v0.5`, muy rigurosos | **Baja** — `trazabilidad/AUDITORIA_CIERRE.md` es una plantilla sin una sola casilla marcada | Sí (`TRZ_C1..C4.md`) | El frente nunca ejecutó su propio proceso de cierre; toda la calidad observada es la del contenido, no de una revisión formal propia |
| **D** (D1-D3) | D1/D2 altos (`v0.1`/`v0.5`); **D3 es un esqueleto, 0 % iniciado** | **Muy alta** — D1/D2 pasaron por B7, B7-R y B7-C, con hallazgos propios documentados y una lista explícita de pendientes dirigidos a otros frentes | Sí (`TRZ_D1/D2.md`); `TRZ_D3.md` vacío (10 líneas, plantilla) | El frente más auto-crítico de los tres; gran parte de este documento simplemente confirma y consolida lo que D2 ya encontró |

**Hallazgo más importante que ningún frente había detectado todavía:** el catálogo de puntos únicos de falla `SPOF-NN` existe **dos veces, con numeración idéntica y contenido distinto**, en C1 §8 (`SPOF-01..10`, propio y local) y en D2 (`SPOF-01..22`, consolidado transversal). Ver **hallazgo X-1**.

**Segundo hallazgo nuevo:** D1 cita `FEP02 Cap. 11, RT-11.27` (que trata exclusivamente del acceso de personas desarrolladoras a producción) como fuente de `SEC-IAM-01`, un control de identidad general que no tiene relación con esa materia. Ver **hallazgo X-2**.

**Tercer hallazgo nuevo:** el registro ADR global (`00_Gobierno/03_REGISTRO_ADR_GLOBAL.md`) tiene **tres versiones distintas simultáneamente vigentes** en `main`, `frente_1` y `frente_3`, con estados de `ADR-002` a `ADR-011` que no coinciden entre sí. Ver **hallazgo G-1**.

El resto de los hallazgos de fondo (`CTX-VESSEL`, seis diferencias de criticidad, `CH-CAB`, `ACT-TI`, solape SIEM) ya estaban **correctamente identificados por D2** y, del lado de A1, ya fueron incorporados en la ronda de correcciones anterior de este frente (`F1-CONFLICTO-002`, `TRZ-A1-039`). Se listan aquí consolidados, con su trazabilidad completa, porque el pedido explícito fue reunir todo en un solo documento.

---

## 1. Hallazgos nuevos de esta auditoría cruzada (no detectados antes por ningún frente)

### X-1 — Colisión de numeración `SPOF-NN` entre C1 y D2 — **CRÍTICO**

**Qué pasa.** C1 §8 ("Registro inicial de puntos únicos de falla") numera su propio catálogo `SPOF-01` a `SPOF-10`. D2 §B4 numera, de forma independiente y para todo el proyecto, su propio catálogo `SPOF-01` a `SPOF-22`. Son **catálogos distintos, con propósito distinto, y usan el mismo prefijo desde el mismo número 1**.

| Código | Significado en C1 §8 | Significado en D2 §B4 |
|---|---|---|
| `SPOF-01` | fibra de un solo proveedor hacia el exterior | `EDGE-RUN` y su almacenamiento |
| `SPOF-02` | radioenlace de respaldo sin prueba desde 2022 | enlace exterior (sin conmutación real) |
| `SPOF-03` | operación/administración/CCTV sobre la misma conmutación | medio de radio del patio |
| `SPOF-06` | emplazamiento único (todo el terminal comparte sitio) | sala técnica, energía y ambiente |
| `SPOF-07` | sala técnica única durante el corte de 72 h | `INT-TOS`, capa anticorrupción |
| `SPOF-08` | `EXT-TOS12` como fuente de verdad durante coexistencia | `INT-HUB`, bus de integración |
| `SPOF-09` | proveedor de nube único | `SRV-EVID`, evidencia y firma |
| `SPOF-10` | red inalámbrica de patio con sombras móviles | `SRV-IAM`, identidad |

**Por qué no lo vio nadie.** D2 sí verificó colisiones de ID en su propio bloque (B7.2 #5: *"`SCN-01..12` sin colisión con `ESC-*`"*) pero nunca comparó su numeración `SPOF-*` contra la de C1 §8, que es anterior y de otro frente. C1, por su parte, no sabía que D2 iba a crear un catálogo consolidado con el mismo prefijo.

**Por qué importa.** El Formulario T-12 y cualquier referencia cruzada futura ("ver `SPOF-08`") es ambigua sin decir el documento de origen — exactamente el mismo patrón de error que ya obligó a resolver el Supuesto M de colisiones `RT-xx.xx`. Si alguien cita "`SPOF-08`" en el consolidado sin decir si es de C1 o de D2, el lector entiende una cosa por otra.

**Traza:** C1 `§8`, líneas de la tabla de SPOF; D2 `§B4` (líneas ~1186-1228 del documento); ninguna fila de `TRZ_C1.md` ni `TRZ_D2.md` documenta la colisión.

**Recomendación (no ejecutada aquí, es de C1/D2/integrador):** renombrar uno de los dos catálogos — por ejemplo, `SPOF-C1-NN` para el registro local de C1 (que en el fondo son riesgos físicos preexistentes del `CP, Cap. 6`, no puntos únicos de la arquitectura propuesta) y dejar `SPOF-NN` para el catálogo consolidado de D2, que es el que alimenta el T-12.

### X-2 — Cita fuera de alcance: `FEP02 Cap. 11, RT-11.27` aplicada a `SEC-IAM-01` — **ALTO**

**Verificación contra el texto real de `FEP02.26 Bases Tecnicas Transversales`, Cap. 11:**

> `RT-11.27`: *"Las personas desarrolladoras no tendrán acceso interactivo directo al ambiente de producción. Todo acceso excepcional será temporal, aprobado, registrado y con sesión grabada."*

Este código trata **exclusivamente** de acceso de desarrolladores a producción. D1 lo cita en tres controles distintos de su "Entrega temprana `SEC-PHYS-v0.1`" y en su matriz de controles:

| Control D1 | Cita RT-11.27 | ¿Corresponde? |
|---|---|---|
| `SEC-PROD-01` (desarrolladores/operadores/despliegues, acceso excepcional a producción) | sí | **Correcta** — coincide exactamente con la materia del código |
| `SEC-ADM-01` (privilegios administrativos generales) | sí, junto con `RT-12.03/06` | **Redundante/cuestionable** — `RT-12.03` (MFA para administradores/privilegiado) y `RT-12.06` (elevación temporal con grabación) ya cubren esta materia por completo; `RT-11.27` es más estrecho (solo developers→producción) y no aporta nada adicional aquí |
| `SEC-IAM-01` (identidad general: internos, externos, eventuales, roles/atributos, PAM) | sí, junto con `Maestro §11.2`, `RNF-SEG-01/09/10`, `RF-ACC-01..05`, `RF-POR-02` | **Incorrecta** — `SEC-IAM-01` cubre identidad de *todos* los actores (incluidos externos y eventuales de terreno), una materia que `RT-11.27` no toca en absoluto. Los códigos que sí cubren esto son `RT-12.01` (federación/directorio), `RT-12.03` (MFA), `RT-12.05` (RBAC/ABAC) y `RT-12.11` (credencial temporal eventuales) — ya usados correctamente en A1 `SRV-IAM`, ver `TRZ-A1` |

**Traza:** D1, matriz de controles, filas `SEC-IAM-01`, `SEC-ADM-01`, `SEC-PROD-01` (tabla "Entrega temprana `SEC-PHYS-v0.1`" y matriz obligatoria); FEP02, Cap. 11, líneas 615/641/644 del archivo fuente.

**Recomendación (de D1, no ejecutada aquí):** retirar `RT-11.27` de `SEC-IAM-01`; mantenerlo solo en `SEC-PROD-01`; en `SEC-ADM-01` es opcional mantenerlo como referencia complementaria pero no aporta materia nueva sobre `RT-12.03/06`.

### X-3 — El ID `FL-01..11` que D2 usa para los flujos de A2 no tiene definición formal en ningún catálogo — **MEDIO**

D2-DEP-002 y su avance B3 mencionan *"A2/A3 deben validar FL-01..11, iniciadores/contratos y autoridad nube/local. FL-06/08/10 requieren desglose"*. Ningún documento de A2 usa el prefijo `FL-*`: A2 describe sus 22 flujos AS-IS del Anexo A de forma narrativa y los traduce directamente a la tabla de 21 contrapartes de §2.1, sin asignarles un ID individual por flujo.

**Por qué importa, aunque sea menor.** D2 numera y refina "FL-06/08/10" sin que exista una tabla en A2 que diga qué flujo del Anexo A es cuál `FL-NN`. Si D2 y A2 hablan de "el flujo 6" pueden no estar hablando del mismo flujo. No es una colisión de código (como X-1) sino una **ausencia de correspondencia declarada** entre un ID que un frente usa activamente y un catálogo que el frente dueño de la materia no numera igual.

**Traza:** D2, avance B3 (*"F3-DEP-002: A2/A3 deben validar FL-01..11..."*); A2 §1 y §2.1 (22 flujos AS-IS, tabla de contrapartes sin ID de flujo individual).

**Recomendación (de A2/D2, no ejecutada aquí):** si D2 sigue necesitando referirse a flujos individuales del Anexo A, lo más simple es que A2 numere sus 22 flujos con el mismo criterio del Anexo A (p. ej. `AS-IS-01..22`) y D2 adopte esa numeración en vez de una propia.

### X-4 — Divergencia de tres versiones del Registro ADR Global — **CRÍTICO (bloquea consolidación)**

Ver detalle completo en **G-1** más abajo (se agrupa allí junto con el resto de hallazgos de gobierno para no duplicar).

---

## 2. Hallazgos de fondo ya identificados por D2, consolidados aquí con trazabilidad completa

Estos hallazgos **no son nuevos**: D2 los documentó en su propia auditoría (`B6.7`, `B7.2 #9`, `AUDITORIA_CIERRE.md` de Frente 3) y quedaron correctamente "vivos, no resueltos en silencio". Se listan aquí para que este documento sea la referencia única de la Célula, con la trazabilidad de los tres lados (A, C, D) en la misma fila.

### F-1 — `CTX-VESSEL`: contradicción de emplazamiento físico — **CRÍTICO, abierto**

| Lado | Afirmación | Fuente |
|---|---|---|
| A1 | `CTX-VESSEL` tiene un subconjunto de operación de muelle que es **Crítico** y debe replicarse en `EDGE-RUN` (on-premise) durante 72 h sin enlace | A1 §2.2 (`EDGE-RUN`), §3.1 (catálogo), `TRZ-A1-039` |
| C1 | `CTX-VESSEL` se ubica enteramente en `PHY-CLD-03` (nube); no tiene nodo secundario on-premise; distingue internamente "operación de muelle sí; mensajería no" pero no le asigna nodo físico local a esa parte | C1 §4 (tabla de emplazamiento), §5 (matriz lógico→físico, fila `CTX-VESSEL`) |
| D2 | Confirma la contradicción de forma independiente: *"`CTX-VESSEL` es crítico y con continuidad local en A1/A3, pero C1 lo ubica solo en nube"* | D2 `B6-F03`, `AUDITORIA_CIERRE` Frente 3 (bloque 5/B7-C) |

**Estado:** A1 ya precisó su propia posición (`TRZ-A1-039`, `F1-CONFLICTO-002` en `DECISIONES_Y_ESCALAMIENTOS.md` de Frente 1) — la pregunta que queda abierta es exclusivamente de C1: asignar (o justificar no asignar) un nodo `PHY-OPS-*` a la operación de muelle de `CTX-VESSEL`. `ADR-002` (frontera del runtime local) está `PROPUESTO CONDICIONADO` en D2 precisamente a esta conciliación.

### F-2 — Seis diferencias adicionales de etiqueta de criticidad A1 vs. C1 — **MEDIO, abierto**

| Componente | Criticidad en A1 §3.1 | Criticidad en C1 §5 | Traza |
|---|---|---|---|
| `GW-EDGE` | Alta | media | D2 `B6-F04a` |
| `GW-API` | Alta | media | D2 `B6-F04a` |
| `CTX-INSP` | Alta | media | D2 `B6-F04a` |
| `CTX-EMIS` | Alta | media | D2 `B6-F04a` |
| `DATA-DOC` | Alta | media | D2 `B6-F04a` |
| `SRV-IAM` | Alta | **crítica** | D2 `B6-F04a` — único caso donde C1 es *más* estricto que A1 |

**Aclaración ya incorporada por A1** (nota en A1 §3.1, "Escala de criticidad"): la escala de A1 mide comportamiento lógico (¿la función debe seguir sin enlace?), la de C1 mide redundancia física — son ejes distintos, no hay error de ninguno de los dos lados, pero tampoco existe una tabla de correspondencia formal entre ambas escalas. Queda pendiente de Puerta 2.

### F-3 — Ubicación de `CH-CAB`: "muelle" (C1) vs. "canal de cabina y campo" (A1) — **BAJO, abierto**

C1 ubica el nodo físico `PHY-EDG-04` de `CH-CAB` como "borde de muelle, 3 sitios". A1 describe `CH-CAB` como interfaz de cabina/terreno usada también en operaciones de patio (grúas de patio, no solo muelle). D2 lo registra como `B6-F04b`: *"afecta cobertura de radio, `SCN-11` y la exposición de `THR-025`/`THR-067`"*.

**Verificación propia de esta auditoría:** revisando A1 (`CH-CAB` — "Interfaz de cabina/terreno", componente transversal usado por operadores de grúa tanto en muelle como en patio) contra C1 (`PHY-EDG-04` = "borde de muelle, 3 sitios", único nodo físico declarado para `CH-CAB`) — **si `CH-CAB` también sirve a grúas de patio, C1 no le asignó nodo físico para esa parte**, de forma análoga (aunque de menor impacto) al patrón de `CTX-VESSEL` en F-1. No se profundiza más aquí porque D2 ya lo tiene registrado y dirigido a C1.

### F-4 — Brecha del actor `ACT-TI` / consola administrativa — **MEDIO, abierto (ya en trazabilidad de Frente 1)**

Ya documentado por Frente 1 como `F1-OBS-002` (`DECISIONES_Y_ESCALAMIENTOS.md`) antes de esta auditoría: A1 no tiene un componente de canal para "consola de administración", que es el recurso que `ACT-TI` necesita. D1 lo confirma de forma independiente (`ACT-TI | Operación TI habitual; administrador con elevación separada | SRV-IAM y plataformas asignadas`, B1.3) y D2 lo registra como `B6-F04c`: *"`THR-034`, `THR-062` y `SPOF-13` quedan sin actor responsable declarado"*. Las tres partes coinciden: es una brecha real de A1, no inventada por D1/D2.

### F-5 — Posible doble conteo de observabilidad/SIEM: `T11-C2-19` vs. `T11-SEC-04` — **MEDIO, abierto**

C2 declara la fila `T11-C2-19` ("observabilidad y SIEM... plataforma compatible OpenTelemetry... `RT-03.16`, D1"). D1 declara su propio candidato de SIEM en la tabla de `SEC-PHYS-v0.1` (`SEC-LOG-01/SEC-SIEM-01`). D2 lo registra como `B6-F05` / `B7-O01`, y aclara que además hay que distinguir `SPOF-13` (D2) de `SPOF-22` (D2) por ser "adyacentes pero distintos". Ninguna de las dos filas se ha corregido todavía; ambas están correctamente marcadas como pendientes en sus respectivos frentes (C2 `§9`, D1 matriz de controles).

---

## 3. Hallazgos propios de Frente 1 que siguen sin cerrarse (recordatorio, no nuevos)

Para que este documento sea la referencia completa, se listan también los conflictos que Frente 1 ya tiene registrados en su propio `DECISIONES_Y_ESCALAMIENTOS.md` y que siguen abiertos:

| ID | Tema | Estado |
|---|---|---|
| `F1-CONFLICTO-001` | Colisiones de código `RT-xx.xx` entre BTT y Cap. 15 del caso (Supuesto M) — 5 confirmadas por Célula 2, 5 más confirmadas por `RECORDATORIO_ANTES_DE_ENTREGA.md` y `F2-ESC-006` | PARA ENTREGAR A CÉLULA 2 |
| `F1-CONFLICTO-002` | `CTX-VESSEL` + 6 diferencias de criticidad (= F-1/F-2 de este documento) | CONFLICTO ABIERTO (Puerta 2) |
| `F1-ESC-004` | `ADR-011` (proveedor/región de nube) afecta a A1 sin que A1 lo decida | OBSERVADO |
| `F1-ESC-005` | Ambiente de DR operativo desde el mes 6 (`F2-ESC-010`) afecta la planificación de A1/A3 | OBSERVADO |
| `F1-OBS-001` | Estado de `ADR-001` divergente entre `main` y `frente_1` | OBSERVADO — ver ahora G-1, que lo amplía |
| `F1-OBS-002` | Brecha `ACT-TI`/consola administrativa (= F-4) | ABIERTO |
| `F1-OBS-003` | Catálogo de 16 actores no referenciado aguas abajo en A2/A3 | ABIERTO |

---

## 4. Hallazgos de gobierno (`00_Gobierno/`)

### G-1 — El Registro ADR Global tiene tres estados distintos en tres ramas — **CRÍTICO**

| ADR | `main` (`8307e1c`) | `frente_1` (propia) | `frente_3` (más avanzada) |
|---|---|---|---|
| `ADR-001` | CANDIDATO | **PROPUESTO** | PROPUESTO |
| `ADR-002` | CANDIDATO | CANDIDATO | **PROPUESTO** |
| `ADR-003` | CANDIDATO | CANDIDATO | **PROPUESTO** |
| `ADR-004` | CANDIDATO | CANDIDATO | **PROPUESTO** |
| `ADR-005`–`007` | CANDIDATO | CANDIDATO | CANDIDATO (coincide) |
| `ADR-008` | — | CANDIDATO | **PROPUESTO** |
| `ADR-009` | — | CANDIDATO | **PROPUESTO** |
| `ADR-010` | — | CANDIDATO | **PROPUESTO** |
| `ADR-011` | — (no existe) | — (no existe) | **CANDIDATO** (existe) |

Ninguna de las tres versiones es "la correcta" por estar en una rama u otra — cada frente actualizó su propia copia con su propio avance, y nadie ha hecho todavía la fusión que le corresponde al integrador. Es exactamente el escenario que `F1-OBS-001` ya anticipaba, pero more extenso de lo que se sabía entonces (ya no es solo `ADR-001`).

**Por qué es crítico y no solo una curiosidad de Git:** si la Puerta de integración toma la copia de cualquiera de las tres ramas como base sin fusionar conscientemente las tres, se pierde información real — por ejemplo, tomar la copia de `main` perdería que `ADR-008/009/010` ya están `PROPUESTO` con alternativas comparadas (D1 lo hizo con detalle, ver D1 B4.8/B5.8), y `ADR-011` directamente desaparecería.

**Recomendación (del integrador, no ejecutada aquí):** en la próxima puerta de integración, reconstruir el Registro ADR Global tomando el estado **más avanzado y mejor justificado** de cada fila, citando en cada una qué frente aportó la evidencia — no simplemente "quedarse con la copia de la rama que se fusiona primero".

### G-2 — El Maestro y la Matriz de Cumplimiento Global no registran el commit de corte de Célula 2 — **ALTO (ya documentado por Frente 2)**

Confirmado, ya en `F2-ESC-007`: el Maestro sigue declarando "138 RF / 84 RNF / 10 reglas" cuando el estado vigente es 139/91/11. La regla de lectura 5 del propio Maestro exige registrar el commit de congelamiento (`c4756df`) y no se ha hecho. No se repite el detalle aquí porque `F2-ESC-007` ya lo documenta de forma completa y correcta; se cita para que quede en el índice de este documento.

### G-3 — El checklist del Capítulo C del BTT (28 entregables) no está incorporado a la Matriz Global — **ALTO (ya documentado por Frente 2)**

Confirmado, ya en `F2-ESC-005`. Se cita por la misma razón que G-2.

### G-4 — El Capítulo 7 del BTT (site secundario/DR) no estaba citado en ningún cumplimiento hasta la corrección de Frente 2 — **Corregido por Frente 2, verificado aquí**

Ya resuelto dentro de C2/C3 (`F2-COR-002`, `F2-COR-003`). Se verificó que el Maestro central **todavía no** refleja el capítulo completo en su §9.2 (sigue con la tabla resumida sin cita de capítulo) — es la parte de `F2-ESC-003` que sigue pendiente del lado del Maestro, no de C2/C3.

---

## 5. Verificación de conteos y catálogos transversales (cuadre exacto)

Para dejar registrado que se verificó y no solo se asumió:

| Catálogo | Cifra vigente | Verificado en | Coincide en A / C / D |
|---|---|---|---|
| Actores (`ACT-*`) | 16 | Maestro §5.1, A1 §1.2 | Sí — D1 B1.3 usa los mismos 16 |
| Sistemas externos canónicos | 11 (+`EXT-CON` como canal, no sistema) | A1 §1.3, A2 §2.1 | Sí — D2 B6.4 confirma "11 canónicos + `EXT-CON`" |
| Componentes lógicos (`CTX-*`, `SRV-*`, etc.) | 24 | A1 §3.1 | Sí — C1 mapea 24/24, D2 B6.3 confirma 24/24 |
| Contrapartes de integración | 21 + 7 familias | A2 §2.1/§2.2 | Sí — D2 B6.4, C4 `DIM-12` |
| Nodos físicos (`PHY-*`) | 21 | C1 §4 | Sí — D2 B6.5/B7.2#3 confirma 21/21, con la advertencia `B7-O02` de que un subnodo interno podría quedar oculto (no detectado, solo advertido) |
| RF totales | 139 (82 Etapa 1 + 57 Etapa 2) | Catálogo RF Célula 2, corte `c4756df` | Sí en A1/A2/A3/D2; **no** en el Maestro (`G-2`) |
| RNF totales | 91 | `RNF.md` Célula 2 | Sí en A1; **no** en el Maestro (`G-2`) |
| Reglas de negocio | 11 | `Registro reglas de negocio v2.md` | Sí en A3; **no** en el Maestro (`G-2`) |
| Amenazas D2 | `THR-001..073` (6 críticas, 64 altas, 3 medias) | D2 §B6 | Sin colisión detectada con otros catálogos |
| SPOF D2 (consolidado) | `SPOF-01..22` | D2 §B4 | **Colide con C1 §8** — ver `X-1` |
| ADR | 11 (`ADR-001..011`) | Registro ADR Global | **Divergente entre ramas** — ver `G-1` |

---

## 6. Estado de trazabilidad por frente (completitud de los archivos `TRZ_*`)

| Archivo | Filas | Estado |
|---|---|---|
| `TRZ_A1.md` | 44 (36 principales + actores/sistemas/dominio) | Completo, con correcciones de auditorías previas |
| `TRZ_A2.md` | 17 + exclusiones | Completo |
| `TRZ_A3.md` | 15 + RN + códigos verificados | Completo |
| `TRZ_C1.md` | ~22 filas | Completo para v0.5 |
| `TRZ_C2.md` | ~25 filas | Completo para v0.5 |
| `TRZ_C3.md` | ~22 filas | Completo para v0.5 |
| `TRZ_C4.md` | ~20 filas | Completo para v0.5 |
| `TRZ_D1.md` | ~40 filas | Completo para v0.1, con cortes fechados |
| `TRZ_D2.md` | corte B7 | Completo, con regla de actualización de 5 disparadores (`B7-F05`) |
| `TRZ_D3.md` | **10 líneas, sin contenido real** | **Vacío** — D3 no ha comenzado, es coherente con que D3 mismo es 0 % (ver tabla §0) |

**Archivos de auto-auditoría (`AUDITORIA_CIERRE.md`):**

| Frente | Estado |
|---|---|
| A (Frente 1) | No tiene archivo `AUDITORIA_CIERRE.md` propio — el rol de auditoría intermedia lo cumplieron las rondas de revisión de este mismo frente, documentadas en `DECISIONES_Y_ESCALAMIENTOS.md` |
| C (Frente 2) | Existe, pero es una **plantilla sin marcar**: 11 controles, las cuatro columnas C1-C4 todas en `☐`/`PENDIENTE`, revisor `POR ASIGNAR` |
| D (Frente 3) | El más desarrollado de los tres: además de la tabla de control, contiene auditorías intermedias fechadas de B7 (D1), B7 (D2), B7-R (integración D1-D2) y bloque 5/B7-C (revisión conjunta), con hallazgos propios y veredictos explícitos |

Esta asimetría es en sí misma un hallazgo (**G-5**, abajo): dos de los tres frentes NO han corrido su propio proceso formal de auditoría de cierre, mientras que el tercero lo hizo cuatro veces con creciente profundidad. Cuando se llegue a la Puerta de integración, D1/D2 van a llegar con una lista de pendientes mucho más precisa y verificada que C1-C4 (que técnicamente están completos en contenido pero no auto-verificados), y que A1-A3 (auto-verificados, pero no con la metodología formal por bloques que usa D).

### G-5 — Asimetría de rigor de auto-auditoría entre frentes — **OBSERVACIÓN, no un defecto de contenido**

No implica que C1-C4 tenga peor contenido — de hecho, en la lectura completa de este documento, C1-C4 resultó tan riguroso como D1-D2 en su redacción. Lo que falta es que Frente 2 ejecute su propio checklist de cierre (`AUDITORIA_CIERRE.md`) con la misma disciplina de bloques que usó Frente 3, para que la Puerta de integración no tenga que descubrir por sí misma qué está realmente probado y qué solo está bien escrito.

---

## 7. Qué acciones le corresponden a quién (sin resolver nada aquí)

| Acción | Responsable | Prioridad |
|---|---|---|
| Decidir emplazamiento físico de la operación de muelle de `CTX-VESSEL` (F-1) | C1, con A1/A3 y `ADR-002` | Alta — bloquea cierre de `ADR-002` |
| Renombrar o diferenciar los catálogos `SPOF-*` de C1 y D2 (X-1) | C1 y D2, coordinado por integrador | Alta — afecta al T-12 |
| Corregir la cita `RT-11.27` en `SEC-IAM-01` de D1 (X-2) | D1 | Media |
| Numerar formalmente los 22 flujos de A2 para que D2 pueda referenciarlos sin ambigüedad (X-3) | A2 (este frente) | Media — **puede resolverse en la próxima ronda propia de A2** |
| Reconciliar el Registro ADR Global entre las tres ramas (G-1) | Integrador, en la puerta de integración | Alta — bloquea consolidación |
| Actualizar el Maestro con el commit de corte de Célula 2 y las cifras 139/91/11 (G-2) | Integrador (Maestro es gobierno transversal) | Alta |
| Incorporar el checklist de 28 entregables del Capítulo C del BTT a la matriz global (G-3) | Integrador | Media |
| Ejecutar el checklist de `AUDITORIA_CIERRE.md` propio de Frente 2 (G-5) | Frente 2 | Media |
| Asignar componente/canal a `ACT-TI` (F-4) | A1 (este frente) — **pendiente de decisión propia** | Media |
| Aclarar ubicación de `CH-CAB` para uso en patio, no solo muelle (F-3) | C1, con A1 | Baja |
| Resolver el posible doble conteo `T11-C2-19`/`T11-SEC-04` (F-5) | C2 y C4, con D1 | Media |

---

## 8. Nota final sobre alcance y honestidad de esta auditoría

Esta revisión cubrió el **contenido íntegro** de los diez paquetes (A1-A3, C1-C4, D1-D3) y sus trazabilidades, más los cuatro archivos de gobierno. No cubrió: los diagramas finales (todos los frentes los difieren a un pase único al final, por acuerdo transversal documentado en C1 §3, D1 y D3), la Oferta Económica, ni evidencia externa (contratos, site survey, productos finales) que los tres frentes coinciden en que está fuera de su alcance y bloqueada externamente. Tampoco se verificó el Subdocumento 5 (catálogo de datos), que no forma parte de Célula 3 y que D1/D2 señalan repetidamente como dependencia pendiente.

Ningún archivo de A1-A3, C1-C4 o D1-D3 fue modificado para producir este documento. Los únicos archivos nuevos son este mismo, dentro de `90_Consolidado/`, por pedido explícito de dejarlo aquí para la auditoría conjunta.
