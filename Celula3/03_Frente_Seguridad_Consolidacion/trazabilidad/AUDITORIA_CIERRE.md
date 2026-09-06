# Auditoría de cierre — Frente 3

> **Plantilla inicial conservada como historial.** Sus casillas no representan el corte vigente MA-4. Los cortes posteriores de este archivo y los registros `08_REGISTRO_CORRECCIONES_QUIRURGICAS_MA3.md`/`09_REVISION_ADR_BASELINE_I1_MA4.md` gobiernan hasta ejecutar D3.

| Control | D1 | D2 | D3 | Evidencia | Estado |
|---|---|---|---|---|---|
| contratos completos | ☐ | ☐ | ☐ | secciones | PENDIENTE |
| trazabilidad estable | ☐ | ☐ | ☐ | TRZ-D* | PENDIENTE |
| `SEC-PHYS-v0.1` entregado temprano | ☐ | n/a | ☐ | matriz | PENDIENTE |
| Zero Trust transversal | ☐ | ☐ | ☐ | vista/matriz | PENDIENTE |
| IAM/eventuales/terminal compartida | ☐ | ☐ | ☐ | pruebas | PENDIENTE |
| cifrado/llaves/secretos | ☐ | ☐ | ☐ | controles | PENDIENTE |
| STRIDE por componente/integración | ☐ | ☐ | ☐ | amenazas | PENDIENTE |
| SPOF declarados | ☐ | ☐ | ☐ | registro | PENDIENTE |
| ADR con alternativas/consecuencias | ☐ | ☐ | ☐ | registro global | PENDIENTE |
| consolidado cubre SD4/T21/T-11 | n/a | ☐ | ☐ | matriz/checklist | PENDIENTE |

**Resultado del frente:** `PENDIENTE`  
**Brechas abiertas:** POR COMPLETAR  
**Revisor:** POR ASIGNAR

## Auditoría intermedia D1 — B7 (2026-09-05)

Esta revisión no marca casillas de cierre: comprueba si el contenido de D1 puede intercambiarse como v0.1 sin presentarlo como aprobado.

| Comprobación B7 | Resultado | Evidencia | Estado |
|---|---|---|---|
| materias de D1 cubiertas | 11/11 con propuesta/control | D1 B1–B7 | CONFORME PARA v0.1 |
| FEP02 capítulo 11 | 27/28 en diseño; RT-11.02 depende de D2 | TRZ_D1 §§2/11 | EN CURSO |
| FEP02 capítulo 12 | 13/13 en diseño | TRZ_D1 §6 | EN CURSO |
| matriz control→componente→evidencia | 31 SEC-*; nodo/amenaza/responsable final pendientes | D1 matriz obligatoria | EN CURSO |
| paquete físico temprano | 17 grupos y tratamiento T-11 | D1 SEC-PHYS-v0.1/B7.6 | LISTO, NO ENTREGADO |
| ADR | 008 en análisis; 009/010 propuestos; ninguno aprobado | D1 B2.7/B4.8/B5.8/B7.5 | EN CURSO |
| montos/cantidades inventadas | no detectados | D1 B7-F12 | CONFORME |
| insumos A1–A3/C1–C4/D2/Subdoc. 5 | no disponibles con desarrollo suficiente | D1 B7-F04..09 | BLOQUEA CIERRE |
| diagramas/integración final | reservados a B8 tras cruce | D1 plan/B7.7 | PENDIENTE |

**Conclusión intermedia:** `SEC-PHYS-v0.1` y D1 B1–B7 son aptos para intercambio interno. D1 no es apto para aprobación ni cierre. Resultado detallado y correcciones: D1 B7 y TRZ-D1 §11. Revisión ejecutada por el Frente 3; revisor independiente/CLIENTE pendiente.

## Auditoría intermedia D2 — B7 (2026-09-06, corte histórico)

Esta revisión **no marca casillas de cierre del frente**: comprueba si D2 puede intercambiarse como `v0.5` sin presentarlo como aprobado. El resultado del frente sigue `PENDIENTE` y el revisor independiente sigue `POR ASIGNAR`.

| Comprobación B7 | Resultado | Evidencia | Estado |
|---|---|---|---|
| componentes lógicos A1 cubiertos | 24/24 con amenazas nominadas; la clase no sustituye al ID | D2 B6.3 / B7.2 #1 | CONFORME |
| sistemas canónicos y contrapartes | 11 canónicos + `EXT-CON`; variantes A2 agrupadas sin inflar el catálogo | D2 B6.4 / B7.2 #2 | CONFORME |
| nodos físicos C1 | corte histórico B7: 21/21; vigente MA-3: 20/20 nodos `PHY-*` + `LOC-INSP-01`, todos con amenaza aplicable | D2 B6.5 / B7.2 #3 / MA-3 | CONFORME DOCUMENTAL; site survey pendiente |
| integridad de amenazas | `THR-001..073` sin saltos, duplicados ni referencias rotas; 73/73 coherentes con la escala | D2 B7.2 #4 | CONFORME |
| independencia de las filas nuevas | `THR-072`, `THR-073` y `SPOF-22` distintos de las filas previas | D2 B7.2 #5 | CONFORME CON OBSERVACIÓN `B7-O01` |
| cobertura STRIDE | 7 clases × 6 categorías completas; `CLS-DAT`/S cerrada por `THR-072` | D2 B2.5 / B6.2 / B7.2 #6 | CONFORME |
| SPOF | 22/22 completos; **0 `ACEPTADO`**, 11 `POR ACEPTAR`, 11 `ESCALADO` | D2 B4.2–B4.6 / B6.7 / B7.2 #7 | CONFORME |
| ADR | 11/11 revisados y enlazados; `ADR-011` aún no compara alternativas concretas ni selecciona una; ninguno aprobado por D2 | D2 B5.2/B5.3 / B7.2 #8 | PENDIENTE — autor C2/integrador |
| observaciones a Frentes 1 y 2 | las cinco persisten visibles y nominadas; ninguna corregida en silencio | D2 B6.7 / B7.2 #9 | CONFORME |
| coherencia histórico vs. vigente | cuatro afirmaciones de corte superadas se leían como vigentes | D2 B7-F01..F04 | CORREGIDO EN D2 |
| regla de actualización `RT-11.02` | cubría solo componente e integración; ampliada a cinco disparadores | D2 B7-F05 | CORREGIDO EN D2 |
| montos, productos, contratos, pruebas o aceptaciones inventadas | no se detectaron compromisos sin respaldo; las cifras presentes fueron revisadas en contexto y conservan fuente o carácter de corte | D2 B7.2 #12 | CONFORME |

**Conclusión intermedia:** D2 es **apto para intercambio interno como `v0.5`**. D2 **no** es apto para aprobación ni cierre: no hay pruebas ejecutadas, no hay revisión cruzada con D1/C1–C4/integrador, no hay aceptación del CLIENTE, `D2-DEP-004` sigue parcial y `D2-DEP-005` sigue bloqueada. `RT-11.02` queda cubierto a nivel de diseño documental y continúa `EN CURSO`. Los cinco hallazgos dirigidos a Frentes 1 y 2 permanecen abiertos. Revisión ejecutada por el Frente 3; revisor independiente y CLIENTE pendientes. Detalle en D2 B7 y `TRZ_D2` corte B7. **No se marca cierre final del frente.**

## Integración documental D1–D2 — B7-R (2026-09-06, corte histórico)

Esta comprobación actualiza las entradas de D1 después de B7; no marca casillas de cierre final ni reemplaza la auditoría independiente.

| Comprobación | Resultado | Evidencia | Estado |
|---|---|---|---|
| control D1 ↔ amenaza D2 | 31/31 controles asociados; 0 controles D2 inexistentes en D1 | D1 B7-R.2; D2 B7.8 | CONFORME DOCUMENTAL |
| SEC-PHYS ↔ físico | 17/17 grupos con nodo, servicio o proceso | D1 B7-R.3; C1 §6.bis | CONFORME DOCUMENTAL |
| SEC-PHYS ↔ T-11 | 7 candidatos `T11-SEC-*` y 10 incluidos/condicionales | C4 §9.bis; F3-DEC-005 | CONFORME CON PENDIENTES DE CANTIDAD/PRODUCTO |
| continuidad local IAM/llaves/logs | capacidad local declarada en `PHY-OPS-01` | D1 B7-R.4; C1/C2 | CONFORME DE DISEÑO; PRUEBA PENDIENTE |
| `RT-11.02` | cubierto a nivel de diseño documental | D2 B7.6; D1 B7-R/TRZ-D1 | EN CURSO por prueba/revisión/aprobación |
| dependencias D1 | F3-DEP-002 resuelta para diseño; 001/003 con observaciones; 004 parcial | D1 B7-R.5 | EN CURSO |
| ADR/riesgos | corte B7-R: 0 aprobados y 0 riesgos aceptados; `ADR-011` aún no tenía selección concreta | registro ADR; D2 B7 | CORTE HISTÓRICO; ver MA-4 |
| diagramas/D3 | no ejecutados | decisión de secuencia | DIFERIDOS |

**Conclusión B7-R:** D1 y D2 están integrados documentalmente y listos para la revisión conjunta previa a la auditoría general. Permanecen `ACT-TI`, `CTX-VESSEL`, criticidades, `CH-CAB`, solape SIEM, Subdocumento 5, site survey, contratos/productos, responsables y pruebas. El resultado del frente continúa `PENDIENTE`.

## Bloque 5 — revisión conjunta y paquete de auditoría (2026-09-06, corte histórico)

Esta puerta revisa conjuntamente D1, D2, `TRZ_D1`, `TRZ_D2`, el registro ADR global, la matriz global y el registro de decisiones/escalamientos. Su cierre significa que el paquete documental está estabilizado para revisión independiente; no equivale a aceptación del riesgo, prueba ejecutada, aprobación contractual ni cierre del frente.

| Control de auditoría | Resultado | Veredicto |
|---|---|---|
| controles de seguridad | 31 controles D1 y 31/31 con al menos una amenaza D2 asociada | CONFORME DOCUMENTAL |
| catálogo de amenazas | `THR-001..073` definidos; sin referencias huérfanas en el paquete | CONFORME DOCUMENTAL |
| catálogo SPOF | corte histórico B7: `SPOF-01..22`; vigente MA-3: `SPOF-01..26`, 14 `POR ACEPTAR`, 12 `ESCALADO`, 0 aceptados/cerrados | CONFORME COMO REGISTRO; ACEPTACIÓN PENDIENTE |
| ADR | corte histórico: 11 registrados, 7 propuestas y 4 candidatos; el reparto vigente está en MA-4 | SUPERADO POR MA-4 |
| físico y T-11 | 17/17 grupos SEC-PHYS tratados; 7 candidatos propios y 10 incluidos/condicionales | CONFORME DOCUMENTAL; PRODUCTO/CANTIDAD PENDIENTES |
| continuidad local | IAM, claves y evidencia local propuestos en `PHY-OPS-01` | CONFORME DE DISEÑO; PRODUCTO/CAPACIDAD/PRUEBA PENDIENTES |
| trazabilidad/gobierno | estados vigentes compatibles; dos rezagos de TRZ-D2 corregidos en este bloque | CONFORME TRAS CORRECCIÓN |
| enlaces del paquete | sin destinos Markdown inexistentes detectados en los ocho documentos revisados | CONFORME MECÁNICO |
| diagramas y D3 | no ejecutados por secuencia acordada | DIFERIDOS |

### Pendientes entregados a auditoría

| Clase | Pendiente | Propietario primario | Efecto |
|---|---|---|---|
| corrección de autor | `ACT-TI`/consola, `CTX-VESSEL`, seis criticidades adicionales y ubicación de `CH-CAB` | Frentes 1 y 2 | impiden estabilizar responsables, continuidad y dimensionamiento físico |
| consolidación | posible doble conteo `T11-C2-19`/`T11-SEC-04`; conservar distinción `SPOF-13`/`SPOF-22` | C2/C4/integrador | evita costo duplicado o pérdida de un dominio de fallo |
| decisión | completar `ADR-011`; resolver `F3-ESC-001/002` y demás ADR condicionados | autores/integrador/CLIENTE | impide aprobar decisiones y residuales asociados |
| dato | catálogo campo→sensibilidad→retención→custodia del Subdocumento 5 | propietario Subdoc. 5 | impide validar privacidad y dimensionamiento dominante del SIEM |
| evidencia externa | contratos/SLA, productos, responsables nominales, site survey, capacidad y pruebas | adjudicatario/CLIENTE/terceros | impide aprobación y cierre contractual |
| representación | diagramas coherentes y resumen residual final | Frente 3, después de auditoría | obligatorio para B8/cierre de D1–D2 |

**Veredicto del bloque 5:** `COMPLETO PARA ENTREGA A AUDITORÍA INDEPENDIENTE`. No surgieron hallazgos internos nuevos; se corrigieron únicamente dos textos rezagados de `TRZ_D2` que aún anunciaban B7/integración como futuros. D1 y D2 continúan `EN CURSO` y el frente continúa `PENDIENTE` hasta resolver o aceptar formalmente los pendientes, ejecutar B8 y completar la aprobación correspondiente.

## Corte posterior a auditoría — MA-3 (2026-09-06)

El bloque 5 anterior es histórico. La auditoría semántica global sí encontró después una contradicción crítica y hallazgos altos, y MA-3 aplicó su corrección quirúrgica. Estado vigente:

| Comprobación | Resultado vigente | Estado |
|---|---|---|
| ruta local de 72 h | `CH-APP/CH-CAB → GW-API local → CTX crítico → DATA/evidencia/log local`, sin acceso directo ni nube | CERRADO EN DISEÑO; prueba futura |
| catálogo físico | 20 nodos `PHY-*` + `LOC-INSP-01` sobre `PHY-EDG-02` | CONFORME DOCUMENTAL |
| catálogo SPOF | `SPOF-01..26`; 14 `POR ACEPTAR`, 12 `ESCALADO`, 0 aceptados | CONFORME COMO REGISTRO |
| dependencias internas | `ACT-TI`, `CTX-VESSEL`, criticidades, `CH-CAB` y solape SIEM conciliados | CERRADAS |
| capacidad | 21,9 GB de buffer peak, ≈183 GB útiles locales y objetivo ≥35 Mbps; baseline física de sala documentada | BASELINE I1 |
| ADR | contradicciones de insumo retiradas; estados y suficiencia se revisan sin promoción automática | SUPERADO POR MA-4 |
| T-11, diagramas y D3 | no ejecutados en este bloque | MA-5 / B8 / D3 |

Detalle verificable en `00_Gobierno/08_REGISTRO_CORRECCIONES_QUIRURGICAS_MA3.md`.

## Corte vigente — MA-4 y puerta P2 (2026-09-06)

| Comprobación | Resultado vigente | Estado |
|---|---|---|
| revisión ADR | 11/11 contrastados contra contexto, alternativas, criterios, consecuencias, riesgo, efecto transversal/T-11 y condición de revisión | CONFORME PARA BASELINE I1 |
| estados de gobierno | 10 `PROPUESTO`, `ADR-011` `CANDIDATO`, 0 `APROBADO` | COHERENTE; no confunde propuesta con aprobación |
| decisiones físicas prioritarias | sala de 34 m² con puertas y fallback; LTE/5G privada condicionada; 3 nodos + RAID 10 + DR activo-pasivo + 3-2-1-1-0 | BASELINE I1; site survey/producto/pruebas pendientes |
| proveedor y regiones cloud | patrón recomendado documentado, sin proveedor ni región concreta inventados | `ADR-011` CANDIDATO |
| efecto sobre T-11 | existe base suficiente para consolidar filas, cantidades y condiciones | HABILITA MA-5 |
| riesgos/SPOF/pruebas | 0 riesgos aceptados, 0 SPOF cerrados y ninguna prueba presentada como ejecutada | PENDIENTES EXPLÍCITOS |
| diagramas/B8/D3 | no ejecutados | DIFERIDOS POR SECUENCIA |

**Veredicto MA-4:** `COMPLETADA — PUERTA P2`. El siguiente bloque es MA-5/T-11, una vez confirmado este corte. Detalle verificable en `00_Gobierno/09_REVISION_ADR_BASELINE_I1_MA4.md`.

## Corte vigente — MA-5 y puerta P3 (2026-09-06)

| Comprobación | Resultado vigente | Estado |
|---|---|---|
| proveedor/regiones | AWS; primaria `sa-east-1` multi-AZ y secundaria `us-east-1` activo-pasivo | `ADR-011 PROPUESTO` |
| estados de gobierno | 11 `PROPUESTO`, 0 `APROBADO` | COHERENTE |
| T-11 de trabajo | 32 filas con ID, nodo, fuente, cantidad y control | COMPLETO PARA I1 |
| formulario contractual | exactamente cinco columnas, sin precios ni campos vacíos | LISTO PARA P3 |
| seguridad | seis filas propias, SIEM fusionado, capacidades incluidas sin doble conteo | COHERENTE |
| riesgos/SPOF/pruebas | 0 riesgos aceptados, 0 SPOF cerrados, evidencia futura explícita | PENDIENTE LEGÍTIMO |
| diagramas/B8/D3 | no ejecutados | DIFERIDOS |

**Veredicto MA-5:** `COMPLETADA — PUERTA P3`. Próximo bloque: MA-6 tras revisión del usuario. Detalle en `00_Gobierno/10_CONSOLIDACION_T11_MA5.md`.

## Corte vigente — MA-6 y Artículo 4 (2026-09-06)

| Control | Resultado | Estado |
|---|---|---|
| estándares obligatorios Art. 4.3 | 38/38 respondidos con aplicabilidad, control, componente y evidencia | CONFORME PARA I1 |
| normativa nacional/sectorial con efecto arquitectónico | 15 materias tratadas; condiciones externas con dueño | CONFORME PARA I1 |
| estándares condicionales de IA | NIST AI RMF e ISO/IEC 42001 | NO APLICA JUSTIFICADO |
| certificaciones y pruebas | separadas de la evidencia de diseño | EVIDENCIA FUTURA, NO FINGIDA |

**Veredicto MA-6:** `COMPLETADA`. `AFI1-008` queda cerrado para Informe 1. En ese corte el próximo bloque era MA-7; el estado vigente se registra a continuación. Detalle en `00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md`.

## Corte histórico — MA-7 y puerta P4 (2026-09-06)

| Control | Resultado | Estado |
|---|---|---|
| forma oficial | estructura restringida a 4.1/4.2 y T-11 dentro de 4.2 | CONFORME |
| extensión | 20–25 páginas orientativas, incluido T-11 | CONTROLADA |
| vistas | F1–F5 obligatorias; datos mediante `V-DATA-01`; F6 condicional | DISEÑADAS, NO DIBUJADAS |
| detalle avanzado | amenazas, SPOF, controles y RT completos permanecen en expediente | SIN SOBRECARGA |
| siguiente secuencia de ese corte | aprobación P4 → producción → D3 | SUPERADA POR MA-8 |

**Veredicto MA-7:** `COMPLETADA — PUERTA P4 ACTIVADA EN ESE CORTE`. La estructura quedó apta para revisión; MA-8 registra su aprobación posterior.

## Corte vigente — MA-8, preparación D3 (2026-09-06)

| Control | Resultado | Estado |
|---|---|---|
| mapa de llenado | 13/13 secciones con fuente, apoyo, recurso y prueba | COMPLETO |
| trazabilidad D3 | 13 controles con criterio de aceptación | PREPARADA, NO EJECUTADA |
| consolidado | esqueleto enlazado directamente a fuentes | LISTO PARA REDACTAR |
| producción | redacción, F1–F5, cruce Subdoc. 5 y maquetación | PENDIENTE |

**Veredicto MA-8:** `PREPARACIÓN COMPLETA`. No se emite veredicto D3 hasta revisar la versión ensamblada.
