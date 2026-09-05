# D2 — Amenazas, ADR y puntos de falla

## Contrato del entregable

### Objetivo y destino

Modelar amenazas y fallos del caso, y consolidar decisiones con alternativas reales. Alimenta la sección 4.3.

### Cumplimientos asignados

- `SD4-04`, `SD4-07`, `SD4-08`.
- BTT RT-02.04/08/09/11; modelado STRIDE por componente e integración.
- Decisiones 1, 9, 19 y 20; riesgos derivados de MC-02/07/08/09/10/11/12/30.

### Entradas obligatorias

- Maestro §§6–19.
- Registro ADR global.
- Inicialmente clases genéricas; luego catálogos A1, A2, C1 y C3 `v0.1`.

### Trabajo requerido

- [ ] Identificar activos y fronteras de confianza.
- [ ] Aplicar STRIDE a canal, gateway, servicio, broker, datos, edge y tercero.
- [ ] Refinar después por componente e integración real.
- [ ] Cubrir TOS, gate/OCR, reefer, app offline, VMS, radio, ERP/autoridades y sincronización.
- [ ] Definir amenaza, condición, impacto, control preventivo/detectivo/correctivo y evidencia.
- [ ] Consolidar todos los SPOF y su aceptabilidad.
- [ ] Revisar ADR de estilo, runtime, integración, TOS, sala, red, datos e identidad.
- [ ] Registrar consecuencias negativas y disparadores de revisión.

### Matriz STRIDE obligatoria

| ID | Activo/componente | Frontera | S/T/R/I/D/E | Escenario portuario | Prob. | Impacto | Control preventivo | Detección | Respuesta/evidencia | Riesgo residual | Estado |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `THR-001` | app offline | dispositivo↔plataforma | POR CLASIFICAR | pérdida/robo + cola local | — | — | cifrado/sesión | telemetría | revocación/auditoría | — | PENDIENTE |

### Registro SPOF obligatorio

| SPOF | Vista/componente | Escenario | Impacto | Mitigación | Por qué subsiste | Aceptación | Prueba | Estado |
|---|---|---|---|---|---|---|---|---|
| POR IDENTIFICAR | — | — | — | — | — | — | — | PENDIENTE |

### Productos obligatorios

1. Modelo de amenazas por componente/integración.
2. Registro de SPOF.
3. ADR revisados y registro global actualizado.
4. Vista de fronteras de confianza.
5. Resumen de riesgo residual listo para consolidar.

### Aporte T-11/ADR

Valida que los controles físicos/licencias tengan respaldo en riesgo real y que ningún ADR omita impacto en T-11.

### Salidas hacia otros frentes

- Observaciones accionables por componente, no recomendaciones genéricas.
- Requisitos de redundancia, aislamiento, logging o retorno que deban incorporarse.

### Definición de terminado

- [ ] Todo componente/integración relevante tiene amenazas y controles.
- [ ] Todos los SPOF subsistentes están declarados.
- [ ] Cada ADR compara al menos dos alternativas y consecuencias.
- [ ] Riesgos residuales tienen aceptación o escalamiento.
- [ ] No se presentan controles sin evidencia verificable.
- [ ] `TRZ_D2.md` completo.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_D2.md`](trazabilidad/TRZ_D2.md).

