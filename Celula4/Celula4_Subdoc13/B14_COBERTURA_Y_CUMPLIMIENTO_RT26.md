# B14 · Cobertura del checklist y cumplimiento del Capítulo 26 de las BTT

> **Caso:** 06 Portuaria — TERABYTE · **Célula 4** · **Subdocumento 13 — Innovaciones**
> **Responsable:** Matías Reyes · **Corte:** 2026-09-06 · **Estado:** APROBADO
> **Origen:** Numeral 1 del documento de trabajo de Célula 4.

---

## 1. Resumen: completado frente a pendiente

### 1.1 Cobertura del checklist narrativo del Subdocumento 13

| # | Contenido narrativo exigido | Estado |
|---:|---|---|
| 1 | Síntesis de la cartera | `[COMPLETADO]` |
| 2 | Pertinencia al Caso Portuaria | `[COMPLETADO]` |
| 3 | Diferencia entre innovación y funcionalidad obligatoria | `[COMPLETADO]` — verificada contra los 139 RF de Célula 2 |
| 4 | Inserción de cada innovación en la arquitectura | `[COMPLETADO]` contra el Maestro §6.1 · `[PENDIENTE — Célula 3]` confirmación final |
| 5 | Relación con las etapas y con el alcance | `[COMPLETADO]` para etapa · `[PENDIENTE — Célula 2]` confirmación del reparto por innovación |
| 6 | Resultados verificables esperados | `[COMPLETADO]` indicador, línea base y momento · `[PENDIENTE — Célula 4]` cuatro metas propias |
| 7 | Riesgos de adopción | `[COMPLETADO]` |
| 8 | Coherencia conjunta de la cartera | `[COMPLETADO]` |

### 1.2 Cobertura de los cinco T-19 · 17 campos × 5 fichas = 85 campos

> **Contexto tras el comunicado:** el T-19 completo se exige en la **propuesta final**, no en el Informe 1. Esta tabla mide, por lo tanto, **cuánto trabajo de la propuesta final ya está adelantado**, no una brecha de la entrega del 7 de septiembre. Los 35 campos con dependencia declarada corresponden mayoritariamente a la EDT (Informe 2) y a la valorización económica (Informe 3), que el propio calendario del comunicado sitúa después.

| Bloque de campos | Completados | Pendientes | Origen del pendiente |
|---|---:|---:|---|
| Tipo y nombre (2 × 5 = 10) | 10 | 0 | — |
| Problema, evidencia, tecnología, madurez, fuentes (5 × 5 = 25) | 24 | 1 | Célula 4 — escala de madurez de IN-04 |
| Inserción en la arquitectura (1 × 5 = 5) | 5 provisionales | 5 confirmaciones | Célula 3 |
| Paquetes de la EDT (1 × 5 = 5) | 0 | 5 | Ninguna célula — EDT es Informe 2 (T-14) |
| Mes del cronograma (1 × 5 = 5) | 5 como hipótesis | 5 confirmaciones | Célula 2 (etapa) + EDT del Informe 2 |
| Económicos (3 × 5 = 15) | 15 cualitativos | 15 valorizaciones | Informe 3 — Oferta Económica, Entregable 2 |
| Indicador, línea base y meta, momento (3 × 5 = 15) | 11 | 4 | Célula 4 — metas propias de IN-01, IN-03, IN-04, IN-05 |
| Riesgo, mitigación, contingencia (3 × 5 = 15) | 15 | 0 | — |
| **Total** | **85 campos escritos, ninguno vacío** | **35 con dependencia declarada** | — |

**Ningún campo quedó en blanco.** Los 35 con dependencia declarada tienen contenido de hipótesis explícito y trazado a su origen, conforme a la instrucción del T-22.

### 1.3 Cumplimiento de los requisitos del Capítulo 26 de las BTT

| Código | Requisito | Estado |
|---|---|---|
| `RT-26.01` | Ubicación explícita en la arquitectura: capa, componentes e interfaces | `[COMPLETADO]` provisional contra Maestro §6.1 · `[PENDIENTE — Célula 3]` |
| `RT-26.02` | Paquetes de la EDT y mes del cronograma | **No exigible en el Informe 1.** El comunicado sitúa la trazabilidad con la EDT en el Informe 2. Mes anclado al Art. 17° como hipótesis anticipada |
| `RT-26.03` | Nivel de madurez con escala declarada y fuentes en APA 7.ª ed. | `[COMPLETADO]` para IN-01, IN-02, IN-03, IN-05 · `[PENDIENTE — Célula 4]` escala de IN-04 |
| `RT-26.04` | Riesgo de adopción, probabilidad, impacto, mitigación y contingencia | `[COMPLETADO]` |
| `RT-26.05` | Indicador con línea base, meta y momento; impacto en inversión, opex y beneficio | `[COMPLETADO]` en lo verificable · **la dimensión económica se difiere al Informe 3 por instrucción expresa del comunicado**, no por omisión |
| `RT-26.06` | Innovaciones con IA cumplen íntegramente el Capítulo 18 de las BTT | `[COMPLETADO]` — ninguna de las cinco incorpora IA en su versión comprometida; IN-03 declara el gatillo |
| `RT-26.07` | Innovaciones que modifican la arquitectura de seguridad requieren modelado de amenazas propio | `[PENDIENTE — Célula 3]` — aplica a IN-01 y a IN-03 |
| `RT-26.08` | *Deseable:* al menos una innovación verificable antes del mes 16 | `[COMPLETADO]` — **IN-02**, medible en la marcha blanca de la Etapa 1 (meses 13 a 15) |

### 1.4 La cartera en una tabla

| ID | Tipo (Art. 28°) | Nombre | Inserción principal | Etapa / mes hipótesis |
|---|---|---|---|---|
| **IN-01** | 1 · Producto o servicio | Cadena de frío certificada: aviso proactivo al dueño de la carga y certificado de integridad verificable por embarque | `CTX-REEFER` → `SRV-NOTIF` → `SRV-EVID` → `CH-PORTAL` / `GW-API` | Fase A: meses 10 a 15 · Fase B: meses 19 a 21 |
| **IN-02** | 2 · Proceso | Cita convenida a tres bandas con reprogramación automática por confirmación de carga lista | `CTX-GATE` + `CH-PORTAL` + `SRV-NOTIF` | Etapa 1 · meses 8 a 15 |
| **IN-03** | 3 · Tecnología o arquitectura | Gemelo de operación del terminal: simulación de eventos discretos calibrada con telemetría real, sin autoridad operacional | `CTX-SIM` (nuevo, propuesto) alimentado por `DATA-AN` | Etapa 1 (v1) meses 6 a 12 · Etapa 2 (v2) meses 16 a 21 |
| **IN-04** | 4 · Modelo de negocio o contratación | Servicio gestionado del equipamiento de terreno con compromiso de resultado verificable, adicional al régimen del Art. 78° | No es un componente: es cláusula contractual sostenida por `CTX-EMIS`, `CTX-GATE`, `CTX-REEFER` y `RF-CON-11` | Vigente desde el mes 16 · plena en meses 21 a 56 |
| **IN-05** | 5 · Sostenibilidad | Meta de intensidad de carbono por contenedor con reducción verificada bajo la misma metodología del reporte a la alianza | `CTX-EMIS` + término de puntuación en `CTX-YARD` + `DATA-AN` | Medición Etapa 1 desde mes 1 · reducción desde mes 21 |

