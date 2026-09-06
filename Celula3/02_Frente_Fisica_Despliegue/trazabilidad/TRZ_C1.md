# TRZ-C1 — Arquitectura física y emplazamiento

**Regla.** Una fila por afirmación verificable o agrupación homogénea (matriz global §3). Toda cita usa documento + capítulo/numeral + código + materia (Maestro §1.1). `CP` = FEP03 Caso 06; `BTT` = FEP02; `BA` = FEP01.

## 1. Trazas del entregable

| ID | Fuente | MC/decisión | RF/RNF | Componente/nodo | Decisión de ubicación | Criterios Art. 16 | Diagrama | T-11 | Estado |
|---|---|---|---|---|---|---|---|---|---|
| `TRZ-C1-001` | BA, Art. 16.1 — modelo híbrido obligatorio · BTT, Cap. 3, numeral 3.1 · BTT, Cap. 2, `RT-02.01` — capas obligatorias | — | *(se retira «RNF-ARQ»: esa familia no existe en Célula 2, según la propia Matriz Global `GTR-002`)* | plataforma completa | híbrida: nube principal + núcleo local + borde | los seis | §3 | n/a | PARA REVISIÓN |
| `TRZ-C1-002` | CP, Cap. 3 — «toda la operación ocurre en un solo emplazamiento» | — | — | `PHY-CLD-10` | secundario en región secundaria de nube, no en el terminal | continuidad, regulación | §3, §4 | C2 | PARA REVISIÓN |
| `TRZ-C1-003` | BTT, Cap. 7, `RT-07.02` — distancia al principal y análisis de amenazas comunes · CP, Cap. 6 — sala a <300 m de la costa | `F2-ESC-003` | RNF-DIS aplicables | `PHY-CLD-10` | amenaza común descarta un secundario dentro del recinto | continuidad, regulación | §1, §8 | C2 | PARA REVISIÓN |
| `TRZ-C1-004` | CP, Cap. 15, `RT-03.10` — operación desconectada 72 h · BTT, Cap. 3, `RT-03.10` — mínimo 24 h «o el mayor que fije el caso» | MC-09 | RNF-DIS-02/04 | `PHY-OPS-01` | cinco funciones críticas con cómputo y datos en el terminal | latencia, continuidad, acoplamiento | §3, §5, §6 | C4 | PARA REVISIÓN |
| `TRZ-C1-005` | CP, Cap. 15, `RT-09.01` — confirmación de movimiento ≤1 s y posición ≤30 s *(colisión: en el BTT `RT-09.01` es el cálculo de capacidad)* | `F2-ESC-006` | RF-PAT, RF-TRA | `PHY-OPS-01`, `PHY-EDG-02` | latencia determinista exige cómputo local | latencia | §4 | C4 | PARA REVISIÓN |
| `TRZ-C1-006` | CP, Cap. 15, `RT-05.29` — alarma reefer ≤5 min desde el evento físico · CP, Cap. 1 y 4.5 — falla del tablero del 18 de febrero | MC-09 | RF-REF-01..13, RN-11 | `PHY-EDG-03` | concentrador por tablero; alarma local sin depender del enlace | latencia, continuidad, acoplamiento | §3, §4 | C2/C4 | PARA REVISIÓN |
| `TRZ-C1-007` | CP, Cap. 15 — gate: camión ≤120 s, OCR ≤3 s · CP, Cap. 6 — caseta al aire libre, 8 entradas + 6 salidas | MC-10 | RF-POR, RF-ACC | `PHY-EDG-01` | acoplamiento físico directo con OCR, báscula y barrera | latencia, acoplamiento | §3, §4 | C2/C4 | PARA REVISIÓN |
| `TRZ-C1-008` | CP, Cap. 6 — Declaración Mandatoria, punto 2: red operacional segregada de administrativa y de protección · Decisión 19 (IEC 62443) | MC-10 | RNF-SEG aplicables | `PHY-OPS-04` | núcleo de red operacional propio, en HA | regulación/seguridad, continuidad | §3, §8 | C2/C3 | PARA REVISIÓN |
| `TRZ-C1-009` | CP, Cap. 6 — 142 cámaras en el mismo backbone degradan el acceso a operación · Maestro, reglas negativas 6 y 7 | MC-02 | — | `EXT-VMS` | VMS conservado, en zona de protección; sin video por la red operacional | regulación/seguridad, volumen | §3 | fuera de oferta | PARA REVISIÓN |
| `TRZ-C1-010` | BTT, Cap. 3, `RT-03.04` — subredes privadas y exposición restringida al borde · `RT-03.02` — multi-AZ | — | RNF-SEG/DIS | `PHY-CLD-01`..`08` | única superficie expuesta en `PHY-CLD-01` | regulación/seguridad | §3, §4 | C2 | PARA REVISIÓN |
| `TRZ-C1-011` | BTT, Cap. 3, `RT-03.17` — enlace redundante por caminos y proveedores distintos, conmutación automática con tiempo declarado · CP, Cap. 6 — hoy un proveedor de fibra | `F2-COR-001` | RNF-DIS-11 | enlace `PHY-OPS-04` ↔ nube | segundo camino obligatorio | continuidad, conectividad | §3, §8 | C3 | PARA REVISIÓN |
| `TRZ-C1-012` | BTT, Cap. 6, `RT-06.32` — rutas físicas distintas con ingreso al edificio por puntos separados | `F2-ESC-004`, `F2-ESC-008` | — | sala técnica | criterio potencialmente decisivo de `ADR-005` | continuidad, conectividad | §7 | C2 | **BLOQUEADO EXTERNO** |
| `TRZ-C1-013` | BTT, Cap. 6, `RT-06.29`/`RT-06.30` — espacio de operación separado de la sala de equipos · CP, Cap. 2.4 y restricción 11 — TI del CLIENTE de 5 personas | `F2-ESC-004` | — | `PHY-OPS-06` | recinto separado, dimensionado en C4 | TCO, regulación | §4, §7 | C2/C4 | PARA REVISIÓN |
| `TRZ-C1-014` | BTT, Cap. 6, `RT-06.26`..`RT-06.28` — custodia de medios con recinto, inventario, rotación y verificación de legibilidad | `F2-ESC-004` | RNF-DIS-14 (3-2-1-1-0) | `PHY-OPS-05` | soporta la copia «fuera de sitio» | regulación, continuidad | §3, §4 | C2 | PARA REVISIÓN |
| `TRZ-C1-015` | CP, Cap. 6 — ambiente salino, corrosión acelerada, gabinetes que se reemplazan antes de lo previsto · Maestro, regla negativa 11 | MC-11 | RNF-DIS-11 | `PHY-EDG-01`..`04`; dispositivo móvil en `LOC-INSP-01` | protección marina por clase y ubicación; no se presume que mover la sala la elimina | regulación, TCO | §4, §7 | C2/C4 | PARA REVISIÓN |
| `TRZ-C1-016` | CP, Cap. 6 — red de patio de 2013 con sombras móviles por pilas de hasta cinco alturas · Decisión 9 (celular privada LTE/5G) | MC-10 | RNF-DIS-11 | `PHY-EDG-02` | terminal autónomo hasta 8 h fuera de cobertura; cantidad por site survey | conectividad, continuidad | §4, §8 | C3/C4 | **BLOQUEADO EXTERNO** |
| `TRZ-C1-017` | CP, Cap. 6 — Declaración Mandatoria, punto 4 y restricción 3 · CP, Cap. 11 — exclusión explícita | MC-19 | RF-TRA | `PHY-EDG-04`, `EXT-GRU` | solo lectura autorizada; sin intervención del control del fabricante | acoplamiento, regulación | §3, §4 | fuera de oferta | PARA REVISIÓN |
| `TRZ-C1-018` | CP, Cap. 6 — el operador de grúa no puede manipular un dispositivo mientras opera · Decisión 14 · restricción 1 | MC-01 | RF-NAV-10/11 | `CH-CAB` en `PHY-EDG-04` | pantalla de despliegue, no terminal de captura | acoplamiento, seguridad de personas | §4, §5 | C2 | PARA REVISIÓN |
| `TRZ-C1-019` | CP, Cap. 14.2 — volumetría: imágenes OCR ≈1,4–1,6 TB/año; series reefer ≈68–82 GB/año | MC-12 | RNF-DES aplicables | `PHY-CLD-07`, `PHY-CLD-06` | el volumen alto y frío va a nube; la ventana caliente queda local | volumen, TCO | §4, §5 | C4 | PARA REVISIÓN |
| `TRZ-C1-020` | BTT, Cap. 3, `RT-03.16` — monitoreo on-premise integrado a la misma plataforma de observabilidad, sin puntos ciegos | `F2-COR-001` | RNF-OPE aplicables | `PHY-CLD-09` | observabilidad unificada nube + local | regulación, TCO | §3, §4 | C2/D1 | PARA REVISIÓN |
| `TRZ-C1-021` | BTT, Cap. 3, `RT-03.14` — redundancia y tolerancia a la falla de al menos un disco con nivel RAID justificado · `RT-08.03`/`RT-08.04` | — | RNF-DIS aplicables | `PHY-OPS-01`, `PHY-OPS-02`, `PHY-OPS-04` | equipos críticos redundantes, sin punto único | continuidad | §4, §8 | C2/C4 | PARA REVISIÓN |
| `TRZ-C1-022` | BTT, Cap. 3, `RT-03.07` — estrategia de reversibilidad y mitigación de bloqueo por proveedor | — | — | `F2-SPOF-09` | portabilidad declarada por componente | TCO, regulación | §8 | C2 | PARA REVISIÓN |
| `TRZ-C1-023` | CP, Cap. 10, restricción 9 — congelamiento 15-dic a 30-abr · Maestro §13 — todo lo invasivo listo el 14-dic-2027 | MC-30 | RNF-DES-09 | `ADR-005` | el plazo es criterio de comparación de las alternativas de sala | continuidad, TCO | §7 | C3 | PARA REVISIÓN |
| `TRZ-C1-025` | D1, `SEC-PHYS-v0.1`, B3.1 — nueve zonas de política · B7.6 y `F3-DEC-005` — regla de no duplicar filas T-11 | — | — | las nueve zonas sobre `PHY-CLD-*` y `PHY-OPS-*` | `Z-MGMT` sin nodo propio; `Z-DATA` repartida entre nube y sala; `Z-PROT` fuera del límite | regulación/seguridad | §6.bis | ver C4 §9.bis | PARA REVISIÓN |
| `TRZ-C1-024` | CP, Cap. 11 — no se construye infraestructura civil, sí se especifica para que el CLIENTE la ejecute | — | — | límite de oferta | obra civil como especificación, no como partida | — | §2 | fuera de oferta | PARA REVISIÓN |

| `TRZ-C1-026` | D2 §B5 y MA-4 — revisión de `ADR-005`: consecuencia negativa ineludible, anclajes `SPOF-06` y `SPOF-01`, amenazas `THR-052`/`THR-054`, disparador `ESC-09` | — | — | sala técnica | el residual sigue atado a `SPOF-06` `ESCALADO`; MA-4 promueve el ADR a `PROPUESTO` condicionado, sin aprobarlo | continuidad, regulación | §7 | C2 | EN CURSO — BASELINE I1 |
| `TRZ-C1-027` | A1 §3.1 — `CTX-VESSEL` `Crítica` e incluida en `EDGE-RUN` · A3 §7 — operación de nave entre las cinco críticas · `CP, Cap. 15, RT-03.10` — 72 h · D2 `B6-F03` | MC-08 | continuidad | **corrección:** `CTX-VESSEL` pasa a `PHY-OPS-01` con `PHY-CLD-03` como secundario; la mensajería EDIFACT queda en cola en `INT-HUB` | prueba de desconexión de 72 h con atención de nave en curso | vista física y de despliegue | dentro de `T11-C2-01` | PARA REVISIÓN |
| `TRZ-C1-028` | A1 §3.1 y su escala de criticidad · D2 `B6-F04` — siete diferencias de criticidad | — | criticidad | **la criticidad es atributo de A1, no de C1.** Seis valores se alinean con A1; el séptimo, `SRV-IAM`, **se resuelve elevándolo a `Crítica`** con partición dual, dando la razón a C1 (`F2-ESC-017` cerrado) | contraste tabla a tabla con A1 §3.1 | — | n/a | PARA REVISIÓN |
| `TRZ-C1-029` | A1 §2.1 — `CH-CAB` es canal de `ACT-GRU`, `ACT-GATE` y `ACT-EVT` · A1 §3.2 — umbral de 8 h de sombra de radio **en patio** · D2 `B6-F04` | — | canales | **corrección:** `CH-CAB` se ubica en `PHY-EDG-04` muelle, `PHY-EDG-02` patio y `PHY-EDG-01` gate, no solo en muelle | revisión de la vista física en la Puerta 2 | vista física | sin fila nueva; ya contado en `T11-C2-14`/`15` | PARA REVISIÓN |
| `TRZ-C1-030` | A1 `F1-OBS-002` — brecha de canal de `ACT-TI` · Maestro §4.3 — operable por 5 personas de TI · `RT-12.06` — PAM y grabación de sesión · `RT-06.30` — operación fuera del recinto técnico | — | administración | la consola administrativa **no genera nodo nuevo**: vive en `PHY-OPS-06` sobre `Z-MGMT`, vía `PHY-CLD-02` y `PHY-OPS-04` | si A1 nombra un `CH-ADM`, solo agrega fila en la matriz §5 | vista física y de seguridad | **ninguna fila nueva**; `T11-SEC-02` y `T11-C2-13` ya existen | PARA REVISIÓN |

## 2. Cobertura declarada

| Obligación | Cómo la cubre C1 | Sección |
|---|---|---|
| `SD4-02` emplazamiento híbrido y Art. 16 por componente | tabla de 20 nodos `PHY-*` + `LOC-INSP-01`, con los seis criterios | §4 |
| `SD4-05` parte física de ambientes, redes y continuidad | topología, autoridad del dato en el corte y SPOF; el detalle es de C3 | §3, §6, §8 |
| `SD4-07` decisiones registradas | insumo de `ADR-005` con tres alternativas y criterio de descarte por norma | §7 |
| `SD4-08` arquitectura propia del caso | emplazamiento único, sala a <300 m del mar, sombras móviles, cabina de grúa, 26 tableros, ambiente salino | §1, §4, §8 |
| `T21-4.2-A` arquitectura física | diagrama y narrativa | §3 |
| `T21-4.2-B` emplazamiento Art. 16 | tabla completa | §4 |
| Checklist BTT, Cap. C, N° 3 | tabla de emplazamiento nube/on-premise justificada | §4 |

## 3. Pendientes de esta traza

- Refinar `TRZ-C1-001` y `TRZ-C1-010` con los IDs definitivos del catálogo lógico `v0.1` del Frente 1.
- ~~Cruzar `TRZ-C1-008`, `TRZ-C1-009` y `TRZ-C1-020` con `SEC-PHYS-v0.1`~~ — **hecho** en §6.bis; ver `TRZ-C1-025`.
- Cerrar `TRZ-C1-012` y `TRZ-C1-016` cuando se levante el dato externo.
- ~~Asignar fila T-11 definitiva a cada nodo tras el dimensionamiento de C4~~ — **hecho en MA-5**; matriz bidireccional en `90_Consolidado/01_T11_TRABAJO_TRAZABLE.md`.

## 4. Correcciones posteriores

| Fecha | Traza | Corrección |
|---|---|---|
| 2026-09-05 | `TRZ-C1-007` y tabla §4 | `PHY-EDG-05` deja de tener gabinete propio. `CP, Cap. 15, RT-06.01` nombra gabinetes de borde en **muelle, patio, patio refrigerado y gate**, cuatro zonas, no cinco. La zona de inspección se sirve con dispositivo móvil sobre la red operacional del patio. Detectado al declarar la tipología por sitio en C2 §1 |
| 2026-09-06 | `TRZ-C1-004`, `027` y tablas §4–§6 | MA-3 completa la ruta de 72 h con el perfil local de `GW-API` dentro de `PHY-OPS-01`; `CTX-VESSEL`, identidad, datos, evidencia y apoyos parciales quedan en el inventario canónico de `EDGE-RUN` |
| 2026-09-06 | catálogo físico | El total vigente es 20 nodos `PHY-*`; `LOC-INSP-01` identifica una ubicación funcional atendida por `PHY-EDG-02` y no suma gabinete, servidor ni dominio físico independiente |
| 2026-09-06 | `TRZ-C1-002/003/010/022` | MA-5 fija AWS: `PHY-CLD-01..09` en `sa-east-1` y `PHY-CLD-10` en `us-east-1`; `ADR-011 PROPUESTO`. La validación pendiente no vuelve a dejar el lugar indefinido |
