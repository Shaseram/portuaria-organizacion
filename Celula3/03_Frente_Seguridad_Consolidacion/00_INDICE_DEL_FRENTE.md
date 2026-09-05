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
| 1 | [`D1_ARQUITECTURA_DE_SEGURIDAD.md`](D1_ARQUITECTURA_DE_SEGURIDAD.md) | Zero Trust y paquete físico temprano | `trazabilidad/TRZ_D1.md` | EN CURSO |
| 2 | [`D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md`](D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md) | STRIDE, ADR y SPOF | `trazabilidad/TRZ_D2.md` | PENDIENTE |
| 3 | [`D3_AUDITORIA_Y_CONSOLIDACION.md`](D3_AUDITORIA_Y_CONSOLIDACION.md) | auditoría y documento unido | `trazabilidad/TRZ_D3.md` | PENDIENTE |

## Trabajo independiente inmediato

Sin esperar a los otros frentes, producir:

- `SEC-PHYS-v0.1`: zonas, controles, identidades, cifrado, logging y componentes/licencias candidatos;
- modelo de amenazas por clases genéricas de componente, luego refinable con IDs;
- plantilla y control inicial de ADR/SPOF;
- matriz global y checklist de entrega;
- reglas de nombres, diagramas, trazabilidad y ausencia de precios.

## Secuencia acordada para D1

El [plan dentro de D1](D1_ARQUITECTURA_DE_SEGURIDAD.md) define el avance independiente y las dependencias de cierre. Se usan los actores ACT-* del Maestro; A1 valida su catálogo común y D1 propone roles/permisos vinculados a él. Primero contenido y matrices, luego diagramas. El paquete SEC-PHYS-v0.1 se comparte en texto/tablas para permitir el avance de Física. La planificación no cambia los entregables a aprobados ni inicia D2/D3.

## Apoyo al Frente 2

El Frente 3 valida segmentación, controles de sala/borde, administración, HA de componentes de seguridad, logging, licencias y justificaciones del T-11. Este apoyo no transfiere la propiedad de la arquitectura física.

**Avance D1 (2026-09-05):** bloque B1 de alcance, actores, roles y reglas de acceso en borrador. Próximo: sesiones y continuidad de identidad. Dependencias de cierre abiertas; SEC-PHYS-v0.1 aún no entregado.

**Avance D1 — bloque B2 (2026-09-05):** propuesta de sesiones, relevo, identidad local, offline/reconexión y emergencia; ADR-008 en análisis dentro de D1. Pendiente validar revocación en aislamiento (F3-ESC-002) y dependencias. Próximo bloque: zonas, conductos y exposición.

**Avance D1 — bloque B3 (2026-09-05):** zonas y conductos propuestos, controles de borde/gateway/TLS/bots, inventario preliminar de exposición y decisiones trazadas en B3.3. Pendientes redes/contratos reales y pruebas. Próximo bloque: **B4, datos, claves y secretos**, conforme al punto de continuación de D1.

**Avance D1 — bloque B4 (2026-09-05):** clasificación inicial `PUB/INT/CONF/RES`, cifrado total en reposo y adicional por campo sensible, jerarquía/custodia/rotación de claves y secretos, continuidad criptográfica local y alternativa C propuesta para ADR-009. Pendientes catálogo de campos de Subdocumento 5, productos/emplazamiento/capacidad, custodios y pruebas. Próximo bloque: **B5, detección y respuesta**.

**Avance D1 — bloque B5 (2026-09-05):** registro inalterable con retención 12 meses en línea + 24 adicionales en archivo, continuidad local de evidencia, fuentes híbridas, SIEM/EDR, nueve casos portuarios, SOC gestionado 24x7, respuesta a incidentes, vulnerabilidades y pentest. ADR-010 alternativa C queda `PROPUESTO`, no aprobado; productos, ubicación, dotación, capacidad, responsables y pruebas siguen pendientes. ADR-009 alternativa C también queda `PROPUESTO`.

**Avance D1 — bloque B6 (2026-09-05):** desarrollo seguro con revisión por pares y trazabilidad; puertas automáticas SAST/SCA/DAST/secretos/imágenes; construcción única, SBOM, firma y procedencia SLSA 3+; dependencias aprobadas; datos sintéticos por defecto; acceso excepcional a producción por PAM; SAMM inicial/anual y glosario breve. Herramientas, responsables, dimensionamiento y pruebas siguen pendientes. Próximo bloque: **B7, cobertura y paquete temprano**.

**Avance D1 — bloque B7 (2026-09-05):** auditoría intermedia ejecutada. Las 11/11 materias de D1 tienen diseño; FEP02 Cap. 11 queda 27/28 `EN CURSO` con RT-11.02 pendiente de D2, y Cap. 12 queda 13/13 `EN CURSO`. Se corrigieron estados rezagados, se agregaron SEC-GOV/CLOUD/HARD y `SEC-PHYS-v0.1` quedó consolidado en 17 grupos, listo pero no intercambiado. Sin montos/cantidades inventadas; D1 no puede cerrarse por dependencias, amenazas, productos, responsables, pruebas y diagramas. Próximo: evaluar commit/push e intercambio antes de **B8, integración, diagramas y cierre**.
