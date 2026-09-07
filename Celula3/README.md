# Célula 3 — estado vigente y guía de continuidad

**Fecha de corte:** 2026-09-06

**Rama de integración:** `main`
**Estado:** MA-0–MA-8 completadas; alineación C3–C4 ejecutada y gates superados; base obligatoria y fuentes de escritura ordenadas. Redacción editorial conjunta, diagramas del equipo, ensamblado y D3 pendientes.

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
- Cruce C3–C4 cerrado para diseño I1: diez dominios mapeados a cuatro capacidades lógicas, semántica `Contenedor`/`VisitaContenedor`/`Recalada`, catálogo de 28 campos y ocho búsquedas sensibles, capacidad e integración conciliadas.
- Guía de contenido obligatorio preparada con la estructura contractual 4.1/4.2, fuentes por apartado y bosquejos no vinculantes.

## 2. Qué falta realmente

1. Reescribir en conjunto las trece subsecciones con lenguaje natural, usando el consolidado actual como base técnica y no como texto final.
2. Preparar y aprobar los diagramas definitivos que el equipo estime necesarios. Los bocetos previos están archivados y excluidos del entregable.
3. Ensamblar el T-11 final, ejecutar D3 sobre esa versión exacta, corregir hallazgos y emitir P5.
4. Maquetar y revisar visualmente la exportación final.

## 3. Orden de lectura obligatorio

| Orden | Archivo | Para qué se usa |
|---:|---|---|
| 1 | [`PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md`](../PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md) | decisiones compartidas, estado del cruce y orden de trabajo vigente |
| 2 | [`04_BASE_OBLIGATORIA_SUBDOCUMENTO_4.md`](90_Consolidado/04_BASE_OBLIGATORIA_SUBDOCUMENTO_4.md) | estructura contractual, mínimos, fuentes y bosquejos abiertos para escribir |
| 3 | [`07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md`](00_Gobierno/07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md) | alcance de Informe 1, reglas y plan `R1..R6` |
| 4 | [`13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md`](00_Gobierno/13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md) | fuentes canónicas y preparación del control final |
| 5 | [`12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`](00_Gobierno/12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md) | corte histórico de estructura, tablas y contratos visuales; no obliga a usar los bocetos archivados |
| 6 | [`D3_AUDITORIA_Y_CONSOLIDACION.md`](03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md) | mapa de llenado interno y criterio de auditoría |
| 7 | [`00_BASE_TECNICA_SUBDOCUMENTO_4.md`](90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md) | inventario técnico y destino de la redacción conjunta; no es prosa final |
| 8 | [`diagramas_archivados/README.md`](90_Consolidado/diagramas_archivados/README.md) | bocetos excluidos de la entrega; consulta opcional |
| 9 | [`02_FORMULARIO_T11_FINAL.md`](90_Consolidado/02_FORMULARIO_T11_FINAL.md) | tabla contractual que se incorpora sin reescribir |

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

La guía obligatoria agrupa este desglose interno dentro de los apartados oficiales `4.1 a/b` y `4.2 a–e + T-11`. El mapa detallado y los controles viven en D3.

## 5. Plan para quien continúe

Trabajar en este orden:

1. `R2 — Redacción conjunta`: transformar la base técnica en una explicación natural y autónoma, conservando las trece subsecciones.
2. `R3 — Diagramas y ensamblado`: incorporar solo los diagramas aprobados por el equipo e insertar las 32 filas del T-11.
3. `R4 — D3`: completar `TRZ-D3-001..013` con evidencia real y corregir primero la fuente canónica si cambia la solución.
4. `R5 — Cierre`: maquetar, exportar, revisar página por página y emitir el veredicto P5.

Los diagramas definitivos quedan a cargo del equipo. Nadie debe marcar D3 como ejecutado antes del ensamblado.

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

La alineación técnica C3–C4 está completa para comenzar a escribir. El entregable solo queda cerrado después de la redacción conjunta, la incorporación de los diagramas que apruebe el equipo, el ensamblado del T-11 y un veredicto D3 de `APTO PARA INFORME 1` o `APTO CON DEPENDENCIAS EXTERNAS TRATADAS`.
