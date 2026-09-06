# Célula 3 — estado vigente y guía de continuidad

**Fecha de corte:** 2026-09-06

**Rama de integración:** `main`
**Estado:** MA-0–MA-8 completadas; P4 aprobada; producción final y ejecución D3 pendientes.

Este archivo es el punto de entrada para personas y agentes. Resume el estado actual; los documentos MA conservan la historia y los frentes A/C/D conservan el expediente técnico.

## 1. Qué está cerrado

- Arquitectura lógica, integración, procesos, arquitectura física, seguridad y capacidad conciliadas como baseline del Informe 1.
- Ruta local de las cinco funciones críticas diseñada para operar hasta 72 h sin enlace y reconciliar en ≤90 min.
- AWS definido como baseline: `sa-east-1` primaria multi-AZ y `us-east-1` secundaria activo-pasivo.
- 11 ADR en estado `PROPUESTO`; 0 `APROBADO`. Esto es deliberado y defendible para el Informe 1.
- T-11 consolidado con 32 filas, exactamente cinco columnas en el formulario y cero precios.
- Artículo 4 trazado como estándar/norma → control → componente → evidencia de I1 → evidencia futura.
- Estructura final fijada en trece subsecciones: `4.1.1..4.1.5` y `4.2.1..4.2.8`.
- D3 y sus trece controles están preparados, pero no ejecutados.

## 2. Qué falta realmente

1. Redactar por completo el Subdocumento 4 en [`90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`](90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md).
2. Contrastar `V-DATA-01` con el Subdocumento 5 sin duplicar su modelo detallado.
3. Producir F1–F5: esquema, lógica, integración/proceso, física híbrida y seguridad.
4. Ensamblar texto, tablas, figuras y el T-11 final.
5. Ejecutar D3 sobre esa versión exacta, corregir sus hallazgos y emitir P5.
6. Maquetar y revisar visualmente la exportación final.

F6 de continuidad es condicional: solo se crea si F3/F4 no explican claramente operación normal, corte de 72 h, reconciliación ≤90 min y DR.

## 3. Orden de lectura obligatorio

| Orden | Archivo | Para qué se usa |
|---:|---|---|
| 1 | [`07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md`](00_Gobierno/07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md) | alcance de Informe 1, reglas y plan `R1..R6` |
| 2 | [`13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md`](00_Gobierno/13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md) | estado exacto, fuentes canónicas y secuencia final |
| 3 | [`12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`](00_Gobierno/12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md) | índice, extensión, tablas publicables y contratos F1–F6 |
| 4 | [`D3_AUDITORIA_Y_CONSOLIDACION.md`](03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md) | mapa de llenado de las trece secciones y criterio de auditoría |
| 5 | [`00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`](90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md) | único destino de la redacción entregable |
| 6 | [`02_FORMULARIO_T11_FINAL.md`](90_Consolidado/02_FORMULARIO_T11_FINAL.md) | tabla contractual que se incorpora sin reescribir |

Si hace falta justificar una afirmación, recién entonces se baja al Maestro, Matriz Global, Registro ADR, A1–A3, C1–C4, D1–D2 y sus trazas.

## 4. Mapa editorial vigente

| Sección | Fuente principal |
|---|---|
| 4.1.1 Esquema de solución | A1 |
| 4.1.2 Arquitectura lógica | A1 |
| 4.1.3 Integración y procesos críticos | A2 + A3 |
| 4.1.4 Datos y seguridad | D1 + A1 + Subdocumento 5 |
| 4.1.5 Decisiones y cumplimiento | Registro ADR + MA-4 + MA-6 + D2 |
| 4.2.1 Arquitectura física y emplazamiento | C1 |
| 4.2.2 Tecnologías de software | C2 |
| 4.2.3 Implementos HW/SW | C2 + C4 + D1 |
| 4.2.4 Data center primario | C2 + C4 + ADR-005/007 |
| 4.2.5 Data center secundario | C2 + C3 + ADR-007/011 |
| 4.2.6 Despliegue, redes y continuidad | C3 + A3 + D1 |
| 4.2.7 Dimensionamiento y capacidad | C4 |
| 4.2.8 Formulario T-11 | T-11 final + matriz trazable |

El mapa detallado y los controles por sección viven en D3. Esta tabla solo sirve para orientación rápida.

## 5. Plan para quien continúe

Trabajar en este orden:

1. `R1 — Redacción`: llenar las trece subsecciones con conclusiones, cifras decisivas y referencias; no copiar matrices completas.
2. `R2 — Datos`: validar `V-DATA-01` con el Subdocumento 5 y propagar solo cambios reales.
3. `R3 — Figuras`: dibujar F1–F5 usando los mismos IDs, ubicaciones y cifras del texto.
4. `R4 — Ensamblado`: incorporar figuras, tablas publicables y las 32 filas del T-11.
5. `R5 — D3`: completar `TRZ-D3-001..013` con evidencia real y corregir primero la fuente canónica si cambia la solución.
6. `R6 — Cierre`: maquetar, exportar, revisar página por página y emitir el veredicto P5.

Un agente puede preparar las figuras mientras otro redacta, pero nadie debe marcar D3 como ejecutado antes del ensamblado.

## 6. Reglas que no se deben romper

- No aprobar ADR sin nueva evidencia formal; `PROPUESTO` no significa indecisión ni aceptación del CLIENTE.
- No inventar site survey, capacidad de enlaces, AHT, compatibilidad de fabricantes, certificaciones ni pruebas.
- No presentar evidencia futura como ejecutada.
- No modificar la selección AWS sin una nueva decisión registrada.
- No crear precios, tarifas, costos unitarios ni montos en el Informe 1.
- No duplicar las matrices completas de 73 amenazas, 26 SPOF, 31 controles o 53 filas normativas en el documento final.
- No volver a la numeración antigua (`4.1.6+`, `4.2.9+` o `4.3`); solo puede aparecer dentro de historia claramente rotulada.
- No versionar PDFs de apoyo, ZIP, temporales, `.DS_Store`, carpetas de bases o material de continuidad ajeno al cierre.

## 7. Baseline que todos deben conservar

| Elemento | Valor vigente |
|---|---|
| proveedor/región primaria | AWS `sa-east-1`, al menos dos AZ |
| región secundaria | AWS `us-east-1`, activo-pasivo |
| continuidad local | hasta 72 h |
| sombra móvil de patio | hasta 8 h |
| reconciliación tras retorno | ≤90 min |
| DR | RTO ≤4 h; RPO ≤15 min |
| capacidad local útil calculada | ≈183 GB |
| buffer de 72 h en peak | 21,9 GB |
| enlace de reposición | 32,5 Mbps calculados; baseline ≥35 Mbps disponibles |
| arquitectura física | 20 nodos `PHY-*` + `LOC-INSP-01` como ubicación funcional |
| riesgos técnicos | 73 amenazas; 26 SPOF; 0 riesgos aceptados |
| ADR | 11 `PROPUESTO`; 0 `APROBADO` |
| T-11 | 32 filas; cinco columnas; sin precios |

## 8. Condición de entrega

La Célula 3 está lista para **producir** el Subdocumento 4, no para declararlo terminado. Solo queda cerrada cuando el consolidado sea autónomo, F1–F5 estén incorporadas, `V-DATA-01` coincida con el Subdocumento 5, T-11 esté ensamblado y D3 emita `APTO PARA INFORME 1` o `APTO CON DEPENDENCIAS EXTERNAS TRATADAS`.
