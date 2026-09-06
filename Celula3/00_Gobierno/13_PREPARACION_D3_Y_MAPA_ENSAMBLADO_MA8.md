# Preparación D3 y mapa de ensamblado — MA-8

**Fecha:** 2026-09-06
**Estado:** `MA-8 COMPLETADA COMO PREPARACIÓN — D3 NO EJECUTADA`
**Decisión de puerta:** el usuario aprueba avanzar desde P4 con la estructura MA-7; diagramas y redacción total permanecen deliberadamente pendientes.

## 1. Resultado del bloque

MA-8 deja preparado el mecanismo para convertir A1–D2 en un único Subdocumento 4 y auditar posteriormente la versión que se entregará. No emite un veredicto sin documento ni figuras.

Se completaron cinco resultados:

1. D3 fue actualizado desde la numeración antigua a las secciones vigentes `4.1.1..4.1.5` y `4.2.1..4.2.8`.
2. Cada sección final tiene afirmación mínima, fuente principal, fuente de contraste, recurso visual/tabular y control D3.
3. `TRZ_D3.md` contiene trece controles preparados con criterio de aceptación y espacio de evidencia.
4. El esqueleto consolidado enlaza directamente a sus fuentes de llenado.
5. Se separó preparación de auditoría: un control diseñado no se marca como cumplido hasta revisar el artefacto final.

## 2. Qué queda realmente pendiente

| Pendiente | Naturaleza | Salida |
|---|---|---|
| redacción total | producción editorial | `90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md` autónomo |
| diagramas F1–F5 | producción visual | esquema, lógica, proceso/integración, físico y seguridad |
| cruce fino con Subdocumento 5 | ajuste de consistencia | `V-DATA-01` y, si cambia una cifra, capacidad/almacenamiento |
| F6 | condicional | solo si F3/F4 no explican bien continuidad |
| ejecución D3 | control final, no desarrollo de contenido | resultados `TRZ-D3-001..013`, correcciones y veredicto |
| maquetación | presentación final | T-11 incorporado, numeración, referencias y legibilidad |

En términos de contenido, las brechas productivas son la **redacción** y los **diagramas**. El cruce con Subdocumento 5 es un ajuste fino esperado. D3 y la maquetación son controles posteriores necesarios, no nuevos paquetes de arquitectura.

## 3. Regla contra pérdida de información

El consolidado aplica tres niveles:

| Nivel | Qué conserva | Dónde vive |
|---|---|---|
| documento entregable | decisión, explicación, cifras decisivas, tablas y figuras | `90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md` |
| trazabilidad | requisito, afirmación, fuente, control y estado | Matriz Global, trazas y D3 |
| expediente técnico | alternativas, matrices completas, cálculos, amenazas, SPOF y razonamiento | A1–D2 y registros MA |

Por tanto, sintetizar no elimina evidencia. El lector recibe una respuesta completa; el equipo conserva una ruta verificable hacia el detalle.

## 4. Secuencia final de producción y control

1. **Redacción por bloques:** llenar las trece subsecciones usando el mapa D3 y no copiar el expediente literalmente.
2. **Diagramación B8:** producir F1–F5 desde las mismas fuentes; decidir F6 por legibilidad.
3. **Cruce Subdocumento 5:** validar fuente de verdad, almacén, retención y protección en `V-DATA-01`.
4. **Ensamblado:** integrar figuras y las 32 filas T-11 en el consolidado.
5. **D3:** ejecutar trece controles sobre una versión/commit exactos.
6. **Corrección y congelamiento:** aplicar hallazgos, contar checklist y emitir veredicto.
7. **Maquetación/verificación visual:** revisar documento exportado página por página.

La redacción y los diagramas pueden desarrollarse en paralelo, pero D3 solo se ejecuta cuando ambos cuentan la misma solución.

## 5. Fuentes canónicas

| Artefacto | Función desde este corte |
|---|---|
| [`12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`](12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md) | índice, extensión, figuras y tablas publicables |
| [`D3_AUDITORIA_Y_CONSOLIDACION.md`](../03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md) | mapa detallado de llenado y contrato de auditoría |
| [`TRZ_D3.md`](../03_Frente_Seguridad_Consolidacion/trazabilidad/TRZ_D3.md) | registro de controles y evidencia de ejecución |
| [`00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`](../90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md) | único destino de la redacción entregable |
| [`02_FORMULARIO_T11_FINAL.md`](../90_Consolidado/02_FORMULARIO_T11_FINAL.md) | formulario T-11 que se incorpora sin reescribir |
| [`03_CHECKLIST_ENTREGA.md`](../90_Consolidado/03_CHECKLIST_ENTREGA.md) | control operativo y conteo final |

## 6. Condición de cierre

MA-8 queda cerrada como preparación porque el flujo final ya tiene destino, fuentes y pruebas definidos. No se marca D3 como ejecutado ni el Subdocumento 4 como entregable hasta contar con redacción, figuras y cruce de datos.
