# Frente 2 — Física y despliegue

## Misión

Materializar la solución lógica en una arquitectura híbrida concreta, dimensionada, segura y operable en el terminal, y consolidar el Formulario T-11.

## Lectura obligatoria antes de comenzar

1. [`00_MAESTRO_CONTEXTO_ARQUITECTURA.md`](../00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md), completo.
2. [`01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`](../00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md), reglas comunes y sección del Frente 2.
3. [`Célula 2 — cierre corregido y auditoría`](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md). Consultar además RNF, volumetría, decisiones y reglas enlazados por el Maestro antes de fijar cantidades o emplazamientos.

El Maestro sintetiza el contexto, pero Célula 2 permanece disponible como evidencia primaria de trabajo. Ningún supuesto de producto, contrato o sitio reemplaza una fuente faltante.

## Entregables y orden

| Orden | Paquete | Resultado | Trazabilidad | Estado |
|---:|---|---|---|---|
| 1 | [`C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md`](C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md) | topología híbrida y Art. 16 | `trazabilidad/TRZ_C1.md` | **PARA REVISIÓN** `v0.5` |
| 2 | [`C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md`](C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) | plataformas, equipos y recintos | `trazabilidad/TRZ_C2.md` | **PARA REVISIÓN** `v0.5` |
| 3 | [`C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md`](C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md) | ambientes, redes, HA, DR y 72 h | `trazabilidad/TRZ_C3.md` | **PARA REVISIÓN** `v0.5` |
| 4 | [`C4_DIMENSIONAMIENTO_Y_T11.md`](C4_DIMENSIONAMIENTO_Y_T11.md) | cálculos, cantidades y T-11 | `trazabilidad/TRZ_C4.md` | PENDIENTE |

## Primera entrega a los demás frentes (`v0.1`)

- topología híbrida preliminar y alternativas de sala;
- inventario de zonas, nodos, enlaces y sistemas conservados;
- criterios de emplazamiento Art. 16;
- zonas de red y fronteras físicas para el modelo de seguridad;
- dudas que afecten cantidades o productos.

## Regla local

Ningún producto o cantidad se cierra sin necesidad, cálculo y fuente. Cada caja física debe aparecer en el T-11 si corresponde a infraestructura, plataforma, licencia o hardware ofertado. Los diagramas fuente se guardan en `diagramas/`.
