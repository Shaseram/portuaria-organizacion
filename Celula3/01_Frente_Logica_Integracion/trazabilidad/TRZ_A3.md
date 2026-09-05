# TRZ-A3 — Procesos críticos y TOS

## Trazabilidad de secuencias y convivencia TOS

| ID | Fuente primaria | MC/decisión | RF/RNF/RN | Escenario | Umbral/regla | Sección/diagrama | Estado |
|---|---|---|---|---|---|---|---|
| `TRZ-A3-001` | BTT RT-03.10/13; Célula 2, Decisión 1 §7.2 | MC-09 | RF-OPD-01,02,05-08; RNF-DIS-03/04 | Operación desconectada 72 h → reconexión | 72 h sin pérdida; terminales de patio 8 h; sync ≤90 min sin intervención manual | §2.5 | PARA REVISIÓN |
| `TRZ-A3-002` | Célula 2, Decisión 1 §7.2, §15.1, §15.4 | MC-14 | RF-CON-14 | Retorno / reversión de dominio TOS | ≤30 min (dos relojes ≤15+≤15); doble control + break-glass; asimetría "ante la duda se revierte" | §5 | PARA REVISIÓN |
| `TRZ-A3-003` | Célula 2, Decisión 1 §5.2, §7.1, §15.2, §15.3 | MC-07/08 | RF-CON-13/14 | Autoridad dominio×zona×fase y conciliación | Posición/movimientos 0,2 %/0,5 %/48 h; gate/hechos cero/24 h; regla direccional de clasificación | §3, §4 | PARA REVISIÓN |
| `TRZ-A3-004` | Caso 06 Cap. 13.2; Célula 2 Decisión 1 §5.5, §9.1; Decisiones 18, 23 | MC-23/24/25 | RF-NAV-01..05, 12, 13 (conducta) — meta en catálogo RF parte 3 §11.2 | Programa 2029 (alianza, 34 %) | Cero redigitación; ventana ≥72 h; ≥30 mov/h; emisiones verificadas desde mes 1 | §8 | PARA REVISIÓN |
| `TRZ-A3-005` | Caso 06 Cap. 10 restricción 9; Célula 2 Decisión 1 §8 | MC-30 | RNF-DIS-09 | Calendario y colisión con congelamiento | Sin invasivas 15-dic–30-abr; candidata lista 14-dic-2027; producción Etapa 1 no antes de mayo 2028 | §9 | PARA REVISIÓN |
| `TRZ-A3-006` | Caso 06 Cap. 15 RT-05.29; Célula 2 Decisión 8; RN-11 | Decisión 8 | RF-REF-04; RF-REF-07; RN-11 | Desviación de temperatura y ausencia de dato | `RF-REF-07`: alarma tras 3 intervalos de muestreo sin lectura **o a los 5 min, lo que ocurra primero** (acotado por el techo `RT-05.29`); `RN-11` no fija banda numérica — la entrega el CLIENTE por familia de carga | §2.3 | PARA REVISIÓN |
| `TRZ-A3-007` | Caso 06 Cap. 17.1; Célula 2, catálogo RF parte 3 §11.2 | MC-24 | RF-NAV-03; RF-NAV-12/13; RF-INS-01..04,07 | Metas de negocio vs. criterio de aceptación funcional | El RF verifica **conducta del sistema** (mide/explica/reporta), no el resultado de negocio; ≥30 mov/h y ≤12 % inspecciones atrasadas son **metas**, viven en la tabla de indicadores de Célula 2, no se reinventan como RF | §8 | PARA REVISIÓN |
| `TRZ-A3-008` | Célula 2, Registro_supuestos_v3.md Decisiones 2-5; Caso 06 Cap. 4.1-4.3 | Decisiones 2, 3, 4-5 | RF-NAV-01..08, 12; RN-03, RN-09 | Secuencia nave y mensajería | BAPLIE→plan→aprobación/corrección→cabina→COARRI; ventana ≥72 h; prioridad nave salvo camión con gate iniciado | §2.1 | PARA REVISIÓN |
| `TRZ-A3-009` | Célula 2, Decisión 6-7; RN-05, RN-06, RN-07; Caso 06 Cap. 4.6 | Decisiones 6, 7 | RF-GAT-*; EXT-VGM (A1/A2) | Secuencia gate: cita/prevalidación/excepción/liberación | Ventana de cita ±15 min; VGM 5 %; liberación RN-06 (1-5) simultáneo; ≤120 s | §2.2 | PARA REVISIÓN |
| `TRZ-A3-010` | Célula 2, Decisión 8, 10; RN-08; Caso 06 Cap. 4.5, 7.2 | Decisión 8, 10 | RF-REF-01..13 | Secuencia reefer: muestra→alarma→escalamiento | Muestreo 1-5 min; reporte 5-15 min; alarma ≤5 min; notificación simultánea (operador+supervisor) + escalamiento automático a tercer contacto sin intervención manual | §2.3 | PARA REVISIÓN |
| `TRZ-A3-011` | Célula 2, Registro_supuestos_v3.md A.4 (Decisión 21); Caso 06 Cap. 18 criterios 8/10 | Decisión 21 | RF-INS completo; RF-PAT-10 (programación anticipada de remociones, mecanismo físico que ejecuta el desplazamiento conceptual); RF-PAT-11; RF-INT-10; RF-POR-06 | Secuencia inspección→remoción anticipada→acta→hecho facturable | Reserva de disponibilidad antes de que el inspector llegue; acta firmada (`RF-FIR-01`, acta conjunta autoridad+terminal — Supuesto N); meta 11 | §2.4 | PARA REVISIÓN |
| `TRZ-A3-012` | Célula 2, Decisión 1 §7.3, §15.9 (pendiente 4) | — | — | Verificación física de inventario | Barrido por bloques con congelamiento lógico; mayo-noviembre; fuera de peaks de gate; segmentación exacta abierta como supuesto de ingeniería (C4) | §6 | PARA REVISIÓN |
| `TRZ-A3-013` | A1 §2.4, §2.5; BTT RT-03.13, RT-10.08 | — | RF-ACC-08 | Cinco funciones críticas: qué no está disponible offline | Sin RTO/RPO crítico salvo lo ya declarado en A1 §2.4; conteo sin conectividad (`RF-ACC-08`) | §7 | PARA REVISIÓN |
| `TRZ-A3-014` | Maestro §3, §4.4, §9, §19; Célula 2 Decisión 1 completa | Decisiones 1-21 | RF-CON-13/14; BTT RT-05.20, RT-02.14 | ADR-002 (frontera runtime local) y ADR-004 (convivencia/autoridad TOS) | Frontera = 5 funciones de A1 §2.4; envolver+sustitución progresiva núcleo primero | §10 | Propuesto |
| `TRZ-A3-015` | A1 §4.1-4.2; A2 §6 | — | — | Diagrama de estados de autoridad por zona; coherencia de nombres con A1/A2 | Ningún `CTX-*` accede a `EXT-TOS12` salvo vía `INT-TOS` | §11 | PARA REVISIÓN |

## Trazabilidad de reglas de negocio (RN) aplicadas

| ID | Regla | Fuente | Sección A3 | Pendiente de validar (heredado de Célula 2) |
|---|---|---|---|---|
| `TRZ-A3-RN-01` | RN-03 — Prioridad nave vs. camión, con salvaguarda de gate ya iniciado | `Registro reglas de negocio v2.md` | §2.1 | Sí — de las más sensibles |
| `TRZ-A3-RN-02` | RN-05 — Tolerancia VGM 5 % | ídem | §2.2 | Sí, prioridad alta — tolerancia chilena real no confirmada (`ESC-13`) |
| `TRZ-A3-RN-03` | RN-06 — Criterios de liberación simultáneos (1-5) | ídem | §2.2 | Sí, punto 4 (deuda de facturación) |
| `TRZ-A3-RN-04` | RN-07 — Ventana de cita ±15 min, no-show sin multa | ídem | §2.2 | Sí — valor de referencia a ajustar en marcha blanca |
| `TRZ-A3-RN-05` | RN-08 — Escalamiento automático sin intervención manual | ídem | §2.3 | Parcialmente — validado en reefer, extensión a otras alarmas por confirmar |
| `TRZ-A3-RN-06` | RN-09 — Precedencia de restricciones del plan de estiba (5 niveles) | ídem | §2.1 | Sí, prioridad alta — orden de niveles 3-5 es criterio propio |
| `TRZ-A3-RN-07` | RN-11 — Banda y duración mínima de desviación de temperatura, parametrizable por familia de carga | ídem | §2.3 | Sí, prioridad alta — bandas por producto las debe entregar el CLIENTE |

## Trazabilidad de códigos verificados contra el catálogo real de Célula 2

*Todos los códigos `RF-*` de esta tabla fueron verificados contra `Celula2/01_Requerimientos/Catalogo rf definitivo parte1-3.md` antes de citarse — no se copiaron de memoria ni del Maestro.*

| Código citado | Verificado como | Nota |
|---|---|---|
| `RF-OPD-01,02,05,06,07,08` | Existen; `RF-OPD-03/04` fueron **eliminados** y sus códigos no se reutilizan (los cubren ahora `RNF-DIS-03/04`) | Confirmado en Decisión 1 §Nota; Catálogo parte 2, líneas 604-606 |
| `RF-CON-13/14` | Existen; 13 = "Incorporación de operaciones originadas en el sistema de 2012", 14 = "Transferencia de autoridad al cruzar zonas" | Coincide con el uso ya validado en A1 `TRZ-A1-002` |
| `RF-NAV-01..14` | Existen los 14; repartidos entre `CTX-VESSEL` (01-05,12-14), `CTX-PLAN` (06-09) y `CH-CAB` (10-11) — ver A1 `TRZ-A1-010/011/029` | No confundir con "RF-PLN", que no existe |
| `RF-GAT-*`, `RF-REF-01..13`, `RF-INS-01..07`, `RF-ACC-01..11`, `RF-FIR-01` | Existen (auditados previamente en A1) | — |
| Total del catálogo: 139 RF (Parte 1: 30 — `CON`,`GAT`; Parte 2: 49 — `PAT`,`TRA`,`REF`,`ACC`,`OPD`; Parte 3: 60 — `NAV`,`INT`,`FAC`,`POR`,`INS`,`EMI`,`APP`,`FIR`) | Catálogo RF parte 3, §11.3 "Cierre del catálogo" | Confirmado contra `main` (Maestro v1.1, corte 2026-09-05): 138→139 por `RF-POR-09`, nuevo. Ya no hay diferencia — la nota anterior ("no material") queda superada |
| `RF-VGM`, `RF-NOT`, `RF-PLN` | **No existen** — no se citan en A3 | Confirmado ausentes en el catálogo real |

Agregar filas si se identifican nuevas afirmaciones arquitectónicas. No citar códigos RF/RT sin verificar contra el catálogo o el documento fuente real.
