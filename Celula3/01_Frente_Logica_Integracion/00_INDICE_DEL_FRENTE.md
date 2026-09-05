# Frente 1 — Lógica e integración

## Misión

Definir qué es la solución, cómo se divide, quién interactúa con ella, cómo se comunican sus partes y cómo convive con el TOS y los terceros.

## Lectura obligatoria antes de comenzar

1. [`00_MAESTRO_CONTEXTO_ARQUITECTURA.md`](../00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md), completo.
2. [`01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`](../00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md), reglas comunes y sección del Frente 1.
3. [`Célula 2 — cierre corregido y auditoría`](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md). Consultar además los RF, RNF, decisiones y reglas enlazados por el Maestro cuando se funde una afirmación.

El Maestro sintetiza el contexto, pero Célula 2 permanece disponible como evidencia primaria de trabajo. Ante contradicción se aplica la jerarquía del Maestro; no se elige silenciosamente una versión.

## Entregables y orden

| Orden | Paquete | Resultado | Trazabilidad | Estado |
|---:|---|---|---|---|
| 1 | [`A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`](A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md) | contexto, ocho capas, componentes y dominio | `trazabilidad/TRZ_A1.md` | PARA REVISIÓN |
| 2 | [`A2_ARQUITECTURA_DE_INTEGRACION.md`](A2_ARQUITECTURA_DE_INTEGRACION.md) | contratos, eventos, gobierno y fallos | `trazabilidad/TRZ_A2.md` | PENDIENTE |
| 3 | [`A3_PROCESOS_CRITICOS_Y_TOS.md`](A3_PROCESOS_CRITICOS_Y_TOS.md) | secuencias, TOS, desconexión y retorno | `trazabilidad/TRZ_A3.md` | PENDIENTE |

## Primera entrega a los demás frentes (`v0.1`)

- catálogo de componentes con IDs y criticidad;
- catálogo de interfaces con dirección y sensibilidad;
- cinco funciones que deben sobrevivir 72 h;
- lista de decisiones o dependencias que podrían cambiar emplazamiento o seguridad.

## Regla local

Los diagramas fuente se guardan en `diagramas/`; su imagen exportada y versión deben citarse en el entregable. Las decisiones y bloqueos se anotan en `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`.
