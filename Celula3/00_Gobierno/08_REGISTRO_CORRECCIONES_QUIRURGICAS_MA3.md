# Registro de correcciones quirúrgicas — MA-3

**Fecha:** 2026-09-06

**Fuente:** `06_AUDITORIA_FINAL_SEMANTICA_CONTRACTUAL_INFORME1.md`

**Alcance:** correcciones internas exigibles para estabilizar A1–D2 antes de revisar ADR, completar T-11 y redactar el Subdocumento 4.

**Estado:** `MA-3 COMPLETADA CON DERIVACIONES CONTROLADAS`.

## 1. Resultado del bloque

- Se cerró la contradicción crítica de continuidad local sin crear un componente lógico nuevo: `GW-API` conserva identidad única y tiene perfiles de despliegue central y local restringido.
- Se normalizaron inventario, criticidades, ubicación, capacidades, SPOF, referencias y estados posteriores a la integración.
- Ningún riesgo fue aceptado, ningún ADR fue aprobado y ninguna prueba futura fue presentada como ejecutada.
- Los asuntos que por secuencia corresponden a MA-4, MA-5, MA-7 o B8 permanecen abiertos con dueño explícito.

## 2. Registro hallazgo → cambio → verificación

| Hallazgo | Estado MA-3 | Cambio aplicado | Evidencia / verificación | Continuación legítima |
|---|---|---|---|---|
| `AFI1-001` — ruta local de 72 h sin gateway | **CERRADO EN DISEÑO** | perfil local restringido de `GW-API` dentro de `EDGE-RUN`/`PHY-OPS-01`; inventario canónico de funciones críticas y apoyos parciales; ruta única sin acceso directo | A1 §§3/5; A3 escenario de corte; C1 §§4–6; C3 continuidad; D1 `SEC-API-01`; D2 `SPOF-23`; `TRZ-A1-044`; `TRZ-C3-033` | prueba E2E de 72 h y producto/configuración final: `EVIDENCIA FUTURA` |
| `AFI1-002` — archivos finales vacíos | **DERIVADO A MA-5/MA-7** | no se rellenan antes de cerrar ADR y catálogo T-11 | plan maestro §6 | T-11 y Subdocumento 4 finales |
| `AFI1-003` — sala no dimensionada | **CERRADO COMO BASELINE I1** | baseline de servidores, RAID, racks, carga, UPS, generación/combustible, climatización, CCTV y PUE con supuestos y margen | C4 §6.2.bis/§9; `TRZ-C4-034` | ingeniería de detalle, producto y pruebas quedan condicionados |
| `AFI1-004` — línea base tecnológica/ofertable | **TRATADO PARA I1; DERIVADO A MA-4/MA-5** | C2 distingue selección principal de alternativa, política LTS/EOS y producto/familia de referencia; proveedor/región queda condicionado por `ADR-011` | C2 §§2/4/8; Registro ADR `ADR-011` | congelar filas ofertables y ubicación en MA-4/MA-5 |
| `AFI1-005` — hardware CLIENTE dentro/fuera de T-11 | **CERRADO COMO INTERPRETACIÓN** | todo hardware que TERABYTE debe especificar permanece en la matriz; la justificación distingue adquisición del CLIENTE; si el formulario se limita a provisión, se conserva anexo 1:1 | C2 alcance T-11; C4 §9/§10; Matriz Global | volcado definitivo en MA-5, sin precio ni duplicidad |
| `AFI1-006` — textos históricos como vigentes | **CERRADO EN EL CORTE VIGENTE** | los cortes B6/B7 se conservan como historia y los índices/trazas agregan estado MA-3 inequívoco | Índice F3; `TRZ_D1`; `TRZ_D2`; decisiones F1/F3 | D3 consumirá solo el corte vigente |
| `AFI1-007` — SPOF no consolidados/aceptación sin autoridad | **CERRADO COMO REGISTRO** | D2 agrega `SPOF-23..26`; mapea los candidatos físicos; `F2-SPOF-07` pasa a `POR ACEPTAR`; total 26, cero aceptados | D2 B4/B7.3; A1; C1; `TRZ_D2` | pruebas, aceptador y decisión residual permanecen pendientes |
| `AFI1-008` — estándar sin control/evidencia | **CERRADO A NIVEL DE DISEÑO I1** | Matriz Global vincula cada familia relevante a control, sección y evidencia prevista; continuidad distingue diseño de prueba; IA se marca `NO APLICA JUSTIFICADO` | Matriz Global §4; A2 contract-first; D1 controles | evidencia ejecutada corresponde a etapas posteriores |
| `AFI1-009` — 13 GB vs. 21,9/183 GB | **CERRADO** | 21,9 GB gobierna el buffer peak; 183 GB útiles gobiernan la capacidad local; ≥35 Mbps la reposición | Maestro; C1 `PHY-OPS-02`; C4 `DIM-15/16`; Matriz Global | tamaño real de imagen y enlace se validan externamente |
| `AFI1-010` — estados ADR desincronizados | **PARCIAL INTENCIONAL; DERIVADO A MA-4** | se retiraron contradicciones de insumo en `ADR-002/008`; no se promovieron estados | Registro ADR; A3/C2/D1/D2 | revisión uno por uno y baseline I1 en MA-4 |
| `AFI1-011` — planificación offline ambigua | **CERRADO** | solo se consulta el último plan vigente cacheado; no se genera ni recalcula uno nuevo; respaldo = plan impreso + radio | A1 `CTX-PLAN`; A3; C1/C3 | prueba operativa futura |
| `AFI1-012` — contract-first vs. code-first | **CERRADO** | especificación OpenAPI/AsyncAPI versionada es fuente; código, stubs y validadores se generan o verifican contra ella | A2; C2 | contratos reales de terceros permanecen externos |
| `AFI1-013` — 28 vs. 30 filas T-11 | **CERRADO MECÁNICAMENTE** | Matriz Global registra 30 candidatos: 20 C2 + 4 C3 + 6 SEC; `SEC-04` absorbida por C2-19 | Matriz Global y C4 | MA-5 decide filas finales, agrupaciones e inclusiones |
| `AFI1-014` — DoD/trazas con estados antiguos | **CERRADO EN ESTADO VIGENTE** | trazas D1/D2, índice y decisiones registran 20 nodos + ubicación, 26 SPOF y dependencias internas resueltas | Índice F3; TRZ A1/C1/C2/C3/C4/D1/D2; decisiones F1/F3 | dependencias externas continúan explícitas |
| `AFI1-015` — nodo ficticio `PHY-EDG-05` | **CERRADO** | se elimina como nodo; `LOC-INSP-01` es ubicación funcional servida por `PHY-EDG-02`, sin gabinete/cantidad propia | C1 §4/§5; C2; D2; `TRZ-C1-003/015` | site survey confirma ubicación/cobertura |
| `AFI1-016` — regiones cloud presentadas como declaradas | **CERRADO COMO CONDICIÓN** | C1/C2 distinguen patrón primario/secundario de proveedor/región ofertada; la selección depende de `ADR-011` | C1/C2; Registro ADR | MA-4 fija baseline condicionada y MA-5 la lleva a T-11 |
| `AFI1-017` — exceso de detalle futuro | **DERIVADO A MA-7** | se conserva evidencia fuente; no se mutilan paquetes técnicos durante corrección | plan maestro §§3/6 | síntesis editorial del Subdocumento 4 |
| `AFI1-018` — diagramas finales | **DIFERIDO SEGÚN SECUENCIA** | no se diagramó durante MA-3 | plan maestro; D1/D2/C1/C3 | B8 después de ADR/T-11 auditados |

## 3. Corte canónico posterior a MA-3

| Universo | Estado vigente |
|---|---|
| componentes lógicos | 24 |
| nodos físicos | 20 `PHY-*` |
| ubicación de inspección | `LOC-INSP-01` sobre `PHY-EDG-02`; no suma nodo |
| controles de seguridad | 31/31 enlazados a amenazas |
| amenazas | `THR-001..073` |
| SPOF | `SPOF-01..26`: 14 `POR ACEPTAR`, 12 `ESCALADO`, 0 aceptados |
| ruta local autorizada | `CH-APP/CH-CAB → GW-API local → CTX crítico → DATA/evidencia/log local` |
| capacidad del corte | 21,9 GB de buffer peak; ≈183 GB útiles locales; reposición objetivo ≥35 Mbps disponibles |
| IA en Informe 1 | no se incorpora; `CTX-PLAN` es motor determinista de reglas; estándares de IA `NO APLICA JUSTIFICADO` |

## 4. Pendientes que no son contradicciones internas

- MA-4: suficiencia, estado y efecto de `ADR-001..011`, con prioridad en 005/006/007/008/011.
- MA-5: catálogo único y Formulario T-11; decidir fila propia, inclusión, condición y cantidad sin duplicidades.
- Subdocumento 5: catálogo campo→propietario→sensibilidad→retención→custodia.
- Externos: site survey, contratos/SLA, directorio/federación, productos exactos, responsables nominales y aceptadores.
- Evidencia futura: pruebas de corte 72 h, reconciliación ≤90 min, conmutación, restauración, carga, cobertura y hardening.
- B8/D3: diagramas, resumen residual y puerta final después de MA-5.

## 5. Criterio de lectura

Los bloques B1–B7 conservan el historial de cómo evolucionó el diseño. Cuando una cifra o pendiente histórico difiera de este archivo, gobierna el **corte canónico posterior a MA-3** y la traza vigente correspondiente. Esto no transforma una propuesta en implementación ni una dependencia externa en cumplimiento.
