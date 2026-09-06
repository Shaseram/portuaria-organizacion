# Preparación D3 y mapa de ensamblado — MA-8

**Fecha:** 2026-09-06
**Estado:** `MA-8 COMPLETADA COMO PREPARACIÓN — D3 NO EJECUTADA`
**Decisión de puerta actualizada:** la alineación C3–C4 y los cuatro gates fueron superados. Existe una base técnica estructurada en trece subsecciones; la redacción editorial conjunta, los diagramas definitivos del equipo, el ensamblado T-11 y la ejecución D3 permanecen pendientes.

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
| base técnica de redacción | **completada** | `90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md` organizado en trece subsecciones |
| redacción editorial conjunta | **pendiente** | texto natural, autónomo y sin sobrecarga de referencias internas |
| diagramas definitivos | **pendientes a cargo del equipo** | bocetos F1–F5 archivados y excluidos del entregable |
| cruce con Subdocumento 5 | **completado para diseño I1** | `V-DATA-01`, semántica, capacidad, cifrado e integración alineados |
| selección visual final | **pendiente del equipo** | el equipo decide cantidad y contenido de los diagramas definitivos |
| ejecución D3 | control final, no desarrollo de contenido | resultados `TRZ-D3-001..013`, correcciones y veredicto |
| maquetación | presentación final | T-11 incorporado, numeración, referencias y legibilidad |

En términos de arquitectura y cruce con Subdocumento 5, la base está completa con condiciones externas trazadas. Restan la redacción editorial conjunta, los diagramas que apruebe el equipo, el ensamblado T-11, D3 y la maquetación. No se requieren nuevos paquetes de arquitectura para iniciar la escritura.

## 3. Regla contra pérdida de información

El consolidado aplica tres niveles:

| Nivel | Qué conserva | Dónde vive |
|---|---|---|
| base editorial | decisiones, explicaciones y cifras técnicas que alimentan la escritura conjunta | `90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md` |
| trazabilidad | requisito, afirmación, fuente, control y estado | Matriz Global, trazas y D3 |
| expediente técnico | alternativas, matrices completas, cálculos, amenazas, SPOF y razonamiento | A1–D2 y registros MA |

Por tanto, sintetizar no elimina evidencia. El lector recibe una respuesta completa; el equipo conserva una ruta verificable hacia el detalle.

## 4. Secuencia final de producción y control

1. **Redacción por bloques:** reescribir las trece subsecciones en lenguaje natural usando el mapa D3 y sin copiar el expediente literalmente.
2. **Diagramación del equipo:** preparar y aprobar únicamente las figuras que el equipo considere necesarias; los bocetos archivados son consulta opcional.
3. **Ensamblado:** integrar los diagramas aprobados y las 32 filas T-11 en el consolidado.
4. **D3:** ejecutar trece controles sobre una versión/commit exactos.
5. **Corrección y congelamiento:** aplicar hallazgos, contar checklist y emitir veredicto.
6. **Maquetación/verificación visual:** revisar documento exportado página por página.

La redacción y los diagramas pueden desarrollarse en paralelo, pero D3 solo se ejecuta cuando ambos cuentan la misma solución y el equipo ha aprobado el ensamblado.

## 5. Fuentes canónicas

| Artefacto | Función desde este corte |
|---|---|
| [`04_BASE_OBLIGATORIA_SUBDOCUMENTO_4.md`](../90_Consolidado/04_BASE_OBLIGATORIA_SUBDOCUMENTO_4.md) | punto de entrada editorial: estructura contractual, mínimos, fuentes y bosquejos no vinculantes |
| [`12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`](12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md) | índice, extensión, figuras y tablas publicables |
| [`D3_AUDITORIA_Y_CONSOLIDACION.md`](../03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md) | mapa detallado de llenado y contrato de auditoría |
| [`TRZ_D3.md`](../03_Frente_Seguridad_Consolidacion/trazabilidad/TRZ_D3.md) | registro de controles y evidencia de ejecución |
| [`00_BASE_TECNICA_SUBDOCUMENTO_4.md`](../90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md) | inventario técnico y destino de la redacción conjunta |
| [`02_FORMULARIO_T11_FINAL.md`](../90_Consolidado/02_FORMULARIO_T11_FINAL.md) | formulario T-11 que se incorpora sin reescribir |
| [`03_CHECKLIST_ENTREGA.md`](../90_Consolidado/03_CHECKLIST_ENTREGA.md) | control operativo y conteo final |

## 6. Condición de cierre

MA-8 queda cerrada como preparación porque el flujo final ya tiene destino, fuentes y pruebas definidos. No se marca D3 como ejecutado ni el Subdocumento 4 como entregable hasta contar con redacción editorial, diagramas aprobados por el equipo, T-11 ensamblado y cruce de datos conservado.
