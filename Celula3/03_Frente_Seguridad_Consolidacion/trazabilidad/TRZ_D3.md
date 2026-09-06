# TRZ-D3 — Puerta final de auditoría y consolidación

**Estado:** `TRAZA PREPARADA — CONTROLES NO EJECUTADOS`

Esta traza separa la preparación del control de su resultado. `PREPARADO` significa que existe fuente, prueba y criterio; no significa que el Subdocumento 4 final ya haya sido auditado.

## 1. Matriz de control preparada

| ID | Control | Fuente/obligación | Universo a revisar | Evidencia de ejecución | Criterio de aceptación | Estado |
|---|---|---|---|---|---|---|
| `TRZ-D3-001` | cobertura formal 4.1/4.2 | FEP01 T-7/T-21/T-22 | consolidado + T-11 | secciones y tabla de correspondencia | todos los elementos exigidos son identificables | PREPARADO; NO EJECUTADO |
| `TRZ-D3-002` | solución propia y no genérica | T-7 4.8; T-22 | F1–F5 + narrativa | actores, sistemas y restricciones del Caso 06 | terminal/gate/patio/reefer/TOS/Programa 2029 visibles | PREPARADO; NO EJECUTADO |
| `TRZ-D3-003` | ocho capas y módulos | FEP02 RT-02.01; T-22 | 4.1.2, F2 y `T-SD4-01` | comparación contra A1 §§2–6 | capas, responsabilidades, contextos e interfaces comprensibles | PREPARADO; NO EJECUTADO |
| `TRZ-D3-004` | integración y procesos | T-7 4.3; FEP02 RT-02.03 | 4.1.3 y F3 | cruce A2/A3/C3 | contratos, TOS, autoridad, 72 h y retorno coherentes | PREPARADO; NO EJECUTADO |
| `TRZ-D3-005` | físico híbrido y Art. 16 | FEP01 Art. 16; T-21/T-22 | 4.2.1, F4 y `T-SD4-03` | cruce C1–C4 | componente/familia con ubicación y justificación; terminal+nube+DR | PREPARADO; NO EJECUTADO |
| `TRZ-D3-006` | seguridad y confianza | T-7 4.4; Art. 4 | 4.1.4, F5 y D1/D2 | muestreo control→componente→evidencia | Zero Trust, IAM local, cifrado, claves, logs/SIEM y administración coherentes | PREPARADO; NO EJECUTADO |
| `TRZ-D3-007` | lógico→físico→capacidad→T-11 | T-7 4.2/4.6; T-11 | A1/C1/C2/C4/D1 y 32 filas | matriz 1:1 y revisión de cantidades | ningún componente/caja/fila huérfano o duplicado | PREPARADO; NO EJECUTADO |
| `TRZ-D3-008` | datos y Subdocumento 5 | FEP02 RT-02.03/Cap. 5 | `V-DATA-01` + Subdoc. 5 | acta o diff de autoridad/almacén/retención | sin conflicto de fuente de verdad, protección o capacidad | PREPARADO; NO EJECUTADO |
| `TRZ-D3-009` | ADR y dependencias | FEP02 RT-02.04; Maestro §18 | 11 ADR + `T-SD4-07/08` | estado, alternativas, condición, fallback y efecto | 11 `PROPUESTO`, 0 `APROBADO`, salvo nueva evidencia; externos tratados | PREPARADO; NO EJECUTADO |
| `TRZ-D3-010` | Artículo 4 | FEP01 Art. 4 | síntesis 4.1.5 + MA-6 | estándar/norma→control→componente→evidencia | ninguna mera mención; evidencia futura diferenciada | PREPARADO; NO EJECUTADO |
| `TRZ-D3-011` | coherencia visual | T-7/T-22/RT-02.03 | F1–F5; F6 si aplica | revisión de IDs, flechas, ubicación y leyenda | texto y figuras cuentan la misma solución a tamaño página | PREPARADO; NO EJECUTADO |
| `TRZ-D3-012` | admisibilidad y ausencia de precios | FEP01 Art. 50.2 y T-11 | consolidado completo | búsquedas y revisión manual | cero información económica; T-11 con cinco columnas | PREPARADO; NO EJECUTADO |
| `TRZ-D3-013` | autonomía y trazabilidad editorial | T-22 + regla MA-7 | consolidado y referencias | lectura autónoma + muestreo inverso a fuentes | se entiende sin expediente y toda afirmación crítica vuelve a evidencia | PREPARADO; NO EJECUTADO |

## 2. Correspondencia de publicación

| Destino | Fuente canónica | Traza fuente | Recurso | Estado de producción |
|---|---|---|---|---|
| 4.1.1 | A1 §§1–1.5 | `TRZ_A1.md` | F1 | TEXTO/FIGURA PENDIENTES |
| 4.1.2 | A1 §§2–6 | `TRZ_A1.md` | F2 + `T-SD4-01` | TEXTO/FIGURA PENDIENTES |
| 4.1.3 | A2 §§1–7 + A3 §§2–10 | `TRZ_A2.md`/`TRZ_A3.md` | F3 + `T-SD4-02` | TEXTO/FIGURA PENDIENTES |
| 4.1.4 | D1 B1–B7 + D2 + A1/Subdoc. 5 | `TRZ_D1.md`/`TRZ_D2.md` | F5 + `V-DATA-01` | TEXTO/FIGURA/CRUCE PENDIENTES |
| 4.1.5 | Registro ADR + MA-4/MA-6 | matriz global | `T-SD4-07/08` | TEXTO PENDIENTE |
| 4.2.1 | C1 §§1–9 | `TRZ_C1.md` | F4 + `T-SD4-03` | TEXTO/FIGURA PENDIENTES |
| 4.2.2 | C2 §§3–4 | `TRZ_C2.md` | `T-SD4-04` | TEXTO PENDIENTE |
| 4.2.3 | C2 §§7–9 + C4 §§6/9/10 + D1 | `TRZ_C2.md`/`TRZ_C4.md`/`TRZ_D1.md` | resumen + T-11 | TEXTO PENDIENTE |
| 4.2.4 | C2 §5 + C4 §6.2.bis | `TRZ_C2.md`/`TRZ_C4.md` | F4 + `T-SD4-05` | TEXTO/FIGURA PENDIENTES |
| 4.2.5 | C2 §6 + C3 §9 | `TRZ_C2.md`/`TRZ_C3.md` | F4 | TEXTO/FIGURA PENDIENTES |
| 4.2.6 | C3 §§2–12 + A3/D1 | `TRZ_C3.md`/`TRZ_A3.md`/`TRZ_D1.md` | F3/F5; F6 condicional | TEXTO/FIGURA PENDIENTES |
| 4.2.7 | C4 §§3–10 | `TRZ_C4.md` | `T-SD4-06` | TEXTO PENDIENTE |
| 4.2.8 | T-11 trazable/final | matriz global | formulario | CONTENIDO LISTO; MAQUETACIÓN PENDIENTE |

## 3. Registro de ejecución

Completar una fila por control cuando exista versión auditable del consolidado.

| ID control | Versión/commit auditado | Evidencia observada | Resultado | Hallazgo/corrección | Responsable | Fecha |
|---|---|---|---|---|---|---|
| `TRZ-D3-001..013` | POR REGISTRAR | POR REGISTRAR | NO EJECUTADO | — | integrador D3 | — |

## 4. Regla de cierre

- No convertir `PREPARADO` en `CUMPLE` por existencia del expediente.
- No emitir veredicto sin consolidado redactado, F1–F5 y cruce `V-DATA-01`.
- Un hallazgo que cambie arquitectura se corrige en la fuente canónica y se propaga.
- Un hallazgo solo editorial se corrige directamente en el consolidado.
- El veredicto y el commit revisado deben quedar registrados en esta traza.
