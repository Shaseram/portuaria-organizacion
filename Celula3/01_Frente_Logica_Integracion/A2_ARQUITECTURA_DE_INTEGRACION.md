# A2 — Arquitectura de integración

## Contrato del entregable

### Objetivo y destino

Definir contratos, mensajería, resiliencia y gobierno para todas las contrapartes. Alimenta la sección 4.1.6 y referencias de continuidad del consolidado.

### Cumplimientos asignados

- `SD4-03`, apoyo a `SD4-04`, `SD4-05`, `SD4-06` y `SD4-08`.
- T7-4.3; BTT RT-02.06/08/09 y requisitos de integración/versionado.
- `MC-02`, `MC-03`, `MC-07`, `MC-08`, `MC-12`, `MC-20`, `MC-21`, `MC-23`.

### Entradas obligatorias

- Maestro §§5–8, 14–16, 18–19.
- Volumetría C2 y su matriz 21+7.
- RF-CON, RF-INT, RF-POR, RF-FIR, RF-APP y RNF asociados.
- Catálogo lógico A1 `v0.1`; controles D1 `v0.1` para sensibilidad/autenticación.

### Trabajo requerido

- [ ] Inventariar las 21 contrapartes y 7 familias sin doble conteo.
- [ ] Definir propietario del dato, dirección, patrón y contrato por integración.
- [ ] Separar evento de negocio, documento, mensaje y sobre de red.
- [ ] Precisar BAPLIE, COPRAR, COARRI y CODECO por evento correcto.
- [ ] Definir versionado, compatibilidad y retiro de contrato.
- [ ] Completar timeout, reintento, backoff+jitter, breaker, bulkhead y rate limit.
- [ ] Completar idempotencia, deduplicación, orden, DLQ y replay.
- [ ] Definir disponibilidad, peak, sensibilidad, observabilidad y evidencia.
- [ ] Definir fallo/fallback y recuperación por contraparte.
- [ ] Diferenciar hechos confirmados de contratos `POR LEVANTAR`.

### Matriz obligatoria

| ID | Contraparte | Dueño dato | Dirección | Servicio/evento | Contrato/versión | Patrón | Frecuencia/peak | Timeout/retry | Idempotencia/DLQ | Sensibilidad | Fallback | Evidencia | Estado |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `INT-001` | TOS 2012 | variable dominio×zona×fase | bidireccional | POR DETALLAR | por levantar | async/sync por decidir | ver C2 | POR DEFINIR | obligatoria | operacional | conciliación/retorno | E2E | PENDIENTE |

### Restricciones obligatorias

- ERP conserva emisión tributaria.
- Grúas: solo lectura, sin intervenir control.
- VMS/CCTV: eventos/metadatos/evidencia confirmados; no portal de video.
- Autoridades: interfaz si existe; fallback asistido trazable si no.
- Alianza 2029: sin puente ni redigitación desde vigencia efectiva.
- Radio: adaptador al medio existente, no sistema nuevo sin fundamento.

### Productos obligatorios

1. Diagrama de integración.
2. Matriz completa anterior.
3. Política de gobierno/versionado.
4. Tabla de fallos y recuperación.
5. Candidato `ADR-003`.

### Aporte T-11/ADR

Propone, sin cantidades definitivas, gateway/broker/API management/adaptadores/licencias necesarias. C4 decide filas y cantidades físicas.

### Salidas hacia otros frentes

- Frente 2: protocolos/patrones, volúmenes, latencias y necesidades de conectividad.
- Frente 3: fronteras externas, identidad, sensibilidad y amenazas.

### Definición de terminado

- [ ] Todas las contrapartes/familias están presentes.
- [ ] No hay llamada remota sin timeout ni escritura reintentable sin idempotencia.
- [ ] Todo fallo tiene fallback y recuperación.
- [ ] Todos los desconocidos están marcados y tienen levantamiento.
- [ ] Diagrama, matriz y nombres coinciden con A1.
- [ ] `TRZ_A2.md` completo.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_A2.md`](trazabilidad/TRZ_A2.md).

