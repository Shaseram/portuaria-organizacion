# Frente 3 — Seguridad y consolidación

## Misión

Definir la seguridad transversal, desafiar las decisiones y asegurar que lógica, físico, capacidad y T-11 se integren sin brechas.

## Lectura obligatoria antes de comenzar

1. [`00_MAESTRO_CONTEXTO_ARQUITECTURA.md`](../00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md), completo.
2. [`01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`](../00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md), reglas comunes y sección del Frente 3.
3. [`Célula 2 — cierre corregido y auditoría`](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md). Consultar además RNF, decisiones TOS, supuestos, retenciones y reglas enlazados por el Maestro al auditar controles o afirmaciones.

El Maestro sintetiza el contexto, pero Célula 2 permanece disponible como evidencia primaria de trabajo. El Frente 3 debe rechazar cualquier afirmación sin fuente, decisión o supuesto explícito.

## Entregables y orden

| Orden | Paquete | Resultado | Trazabilidad | Estado |
|---:|---|---|---|---|
| 1 | [`D1_ARQUITECTURA_DE_SEGURIDAD.md`](D1_ARQUITECTURA_DE_SEGURIDAD.md) | Zero Trust y paquete físico temprano | `trazabilidad/TRZ_D1.md` | PENDIENTE |
| 2 | [`D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md`](D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md) | STRIDE, ADR y SPOF | `trazabilidad/TRZ_D2.md` | PENDIENTE |
| 3 | [`D3_AUDITORIA_Y_CONSOLIDACION.md`](D3_AUDITORIA_Y_CONSOLIDACION.md) | auditoría y documento unido | `trazabilidad/TRZ_D3.md` | PENDIENTE |

## Trabajo independiente inmediato

Sin esperar a los otros frentes, producir:

- `SEC-PHYS-v0.1`: zonas, controles, identidades, cifrado, logging y componentes/licencias candidatos;
- modelo de amenazas por clases genéricas de componente, luego refinable con IDs;
- plantilla y control inicial de ADR/SPOF;
- matriz global y checklist de entrega;
- reglas de nombres, diagramas, trazabilidad y ausencia de precios.

## Apoyo al Frente 2

El Frente 3 valida segmentación, controles de sala/borde, administración, HA de componentes de seguridad, logging, licencias y justificaciones del T-11. Este apoyo no transfiere la propiedad de la arquitectura física.
