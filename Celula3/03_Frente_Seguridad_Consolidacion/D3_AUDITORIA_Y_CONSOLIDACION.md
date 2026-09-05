# D3 — Auditoría y consolidación

## Contrato del entregable

### Objetivo y destino

Controlar cobertura y consistencia desde el inicio, integrar contenido aprobado y emitir el cierre del Subdocumento 4.

### Cumplimientos asignados

- Auditoría de `SD4-01..08`, T21 4.1/4.2 y T-11.
- Control transversal de forma, trazabilidad, fuentes, supuestos y ausencia de precios.
- No sustituye la autoría técnica de A1–C4/D1–D2.

### Entradas obligatorias

- Maestro, Plan, Matriz Global y Registro ADR.
- Todos los paquetes `v0.1`, luego `v0.5` y `v1.0`.
- Trazas y auditorías locales de cada frente.

### Trabajo requerido desde la Puerta 0

- [ ] Congelar nomenclatura e IDs.
- [ ] Preparar matriz global y checklist.
- [ ] Definir orden del documento final y destino de cada paquete.
- [ ] Verificar que cada contrato tenga productos y DoD.
- [ ] Mantener control de pendientes/escalamientos.

### Trabajo en Puertas 1–3

- [ ] Verificar consistencia actores→lógico→integración.
- [ ] Verificar lógico→físico→seguridad→capacidad→T-11.
- [ ] Revisar que diagramas usen nombres y leyendas consistentes.
- [ ] Identificar cajas genéricas, flechas sin contrato y cifras sin fuente.
- [ ] Consolidar ADR y riesgos residuales.
- [ ] Separar hechos, decisiones, supuestos y pendientes.
- [ ] Rechazar precios o información económica.
- [ ] Integrar solo bloques `APROBADO`.
- [ ] Emitir veredicto y brechas externas.

### Matriz de integración obligatoria

| Paquete | Sección final | Figuras/tablas | Trazas | ADR | T-11 | Revisión cruzada | Estado integración |
|---|---|---|---|---|---|---|---|
| A1 | 4.1.1–4.1.5 | POR DEFINIR | TRZ-A1 | ADR-001 | candidatos | POR HACER | PENDIENTE |
| A2 | 4.1.6 | POR DEFINIR | TRZ-A2 | ADR-003 | candidatos | POR HACER | PENDIENTE |
| A3 | 4.1.7/4.2.9 | POR DEFINIR | TRZ-A3 | ADR-002/004 | candidatos | POR HACER | PENDIENTE |
| C1 | 4.2.1/4.2.2 | POR DEFINIR | TRZ-C1 | ADR-005 | sí | POR HACER | PENDIENTE |
| C2 | 4.2.3–4.2.6 | POR DEFINIR | TRZ-C2 | ADR-005/007 | sí | POR HACER | PENDIENTE |
| C3 | 4.2.7–4.2.10 | POR DEFINIR | TRZ-C3 | ADR-006/007 | sí | POR HACER | PENDIENTE |
| C4 | 4.2.11/T-11 | POR DEFINIR | TRZ-C4 | aportes | consolidado | POR HACER | PENDIENTE |
| D1 | 4.1.8/4.2.12 | POR DEFINIR | TRZ-D1 | ADR-008/009/010 | sí | POR HACER | PENDIENTE |
| D2 | 4.3 | POR DEFINIR | TRZ-D2 | todos | control | POR HACER | PENDIENTE |

### Productos obligatorios

1. Matriz global actualizada.
2. ADR global aprobado.
3. `90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md` completo.
4. T-11 de trabajo y final coherentes.
5. Checklist final y acta de brechas.

### Definición de terminado

- [ ] Los diez paquetes están aprobados o sus bloqueos externos están tratados.
- [ ] Ocho obligaciones SD4 tienen evidencia.
- [ ] No existe componente lógico sin tratamiento físico cuando corresponde.
- [ ] No existe caja física/T-11 sin necesidad y cálculo.
- [ ] Todos los controles relevantes tienen evidencia.
- [ ] Diagramas y texto cuentan la misma solución.
- [ ] El documento final se entiende por sí solo.
- [ ] `TRZ_D3.md` completo.

## Resultado de auditoría

**Estado:** PENDIENTE  
**Controles cumplidos:** 0/POR DETERMINAR  
**Brechas internas:** POR COMPLETAR  
**Bloqueos externos:** ver Maestro §18

## Trazabilidad

Ver [`trazabilidad/TRZ_D3.md`](trazabilidad/TRZ_D3.md).

