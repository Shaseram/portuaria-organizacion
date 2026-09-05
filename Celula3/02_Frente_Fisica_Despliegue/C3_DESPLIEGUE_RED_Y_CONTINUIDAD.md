# C3 — Despliegue, red y continuidad

## Contrato del entregable

### Objetivo y destino

Definir ambientes, redes, despliegue, alta disponibilidad, recuperación, respaldos y comportamiento ante desconexión. Alimenta las secciones 4.2.7–4.2.10.

### Cumplimientos asignados

- `SD4-04`, `SD4-05`, `SD4-07`, `SD4-08`.
- T7-4.4/4.5; BTT Cap. 3 completo (`RT-03.01..24`), Cap. 4, Cap. 7 completo (`RT-07.01..14`) y Cap. 10; Art. 20 y 24.
- Checklist del BTT, Cap. C, entregables N° 4 (funciones no disponibles en modo desconectado, con A3), N° 9 (plan de recuperación ante desastres y política de respaldo) y N° 12 (plan de continuidad del negocio conforme a ISO 22301, `RT-10.03`).

> *Corrección `F2-COR-003` (2026-09-05): el contrato no citaba el Capítulo 7 del BTT, que es la fuente de RTO/RPO, replicación, conmutación, retorno y respaldos, ni `RT-10.03`. Los entregables N° 9 y N° 12 del checklist no tenían producto asignado en ningún contrato del frente. Ver `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`, `F2-ESC-003` y `F2-ESC-005`.*
- `MC-09/10/11/27/30`, RNF-DIS y RNF-DES aplicables.

### Entradas obligatorias

- Maestro §§4.3, 9–13, 18–19.
- C1 topología, C2 catálogo y D1 `SEC-PHYS-v0.1`.
- A3 procesos críticos y operación desconectada.

### Trabajo requerido

- [ ] Definir DEV, QA, PREPROD, PROD y DR aislados.
- [ ] Demostrar equivalencia PREPROD/PROD.
- [ ] Definir IaC, CI/CD, rollback y despliegue progresivo sin interrupción.
- [ ] Diseñar zonas operacional, administrativa y protección, y conductos autorizados.
- [ ] Mantener VMS/ISPS durante la segregación.
- [ ] Diseñar enlaces redundantes por caminos/proveedores distintos y conmutación automática.
- [ ] Exigir site survey con patio cargado, sombras móviles y handover.
- [ ] Probar corte real de fibra/radioenlace sin pérdida transaccional.
- [ ] Definir HA, réplicas, balanceo y SPOF.
- [ ] Definir RTO/RPO, DR, 3-2-1-1-0 y restauración.
- [ ] Instrumentar la replicación con medición y alertamiento del retraso (`RT-07.03`).
- [ ] Documentar la conmutación de modo que sea **ejecutable por el personal del CLIENTE**, que son cinco personas (`RT-07.05`).
- [ ] Documentar y probar el retorno al sitio principal, con reconciliación de lo generado durante la contingencia (`RT-07.06`).
- [ ] Declarar, por dominio de dato, frecuencia de respaldo, retención y tiempo de restauración completa, cruzado con las siete retenciones del Maestro §16.1 (`RT-07.13`).
- [ ] Proteger las copias inmutables frente a credenciales administrativas comprometidas (`RT-07.10/11`).
- [ ] Resolver 72 h, buffer, recuperación y sincronización ≤90 min.
- [ ] Aplicar retorno a toda intervención y congelamiento/nave.

### Matriz de ambientes obligatoria

| Ambiente | Propósito | Aislamiento | Datos | Topología | Acceso | Despliegue | Retención/limpieza |
|---|---|---|---|---|---|---|---|
| DEV | desarrollo | obligatorio | sintéticos | proporcional | equipo autorizado | CI | POR DEFINIR |
| QA | pruebas | obligatorio | sintéticos | proporcional | QA | CI/CD | POR DEFINIR |
| PREPROD | validación | obligatorio | anonimizados/sintéticos | equivalente PROD | restringido | igual a PROD | POR DEFINIR |
| PROD | operación | obligatorio | reales | HA | mínimo privilegio | progresivo | según clase |
| DR | recuperación | obligatorio | réplica | capacidad RTO/RPO | emergencia/PAM | automatizable | según clase |

### Matriz de continuidad obligatoria

| Servicio/proceso | Criticidad | HA | Dependencia | RTO | RPO | 72 h local | Fallback manual | Prueba | SPOF residual |
|---|---|---|---:|---:|---:|---|---|---|---|
| nave/movimientos | crítica | POR DEFINIR | POR DEFINIR | ≤4 h contractual; operativo por definir | ≤15 min | sí | POR DEFINIR | E2E/DR | POR DEFINIR |

### Productos obligatorios

1. Vista de despliegue/red.
2. Matriz de ambientes.
3. Matriz HA/DR/respaldo/72 h.
4. Plan de recuperación ante desastres y política de respaldo (checklist N° 9).
5. Plan de continuidad del negocio conforme a ISO 22301 (checklist N° 12, `RT-10.03`).
6. Plan de pruebas de red, failover, DR y restauración.
7. Calendario de intervención y retorno.
8. Candidatos `ADR-006/007`.

### Aporte T-11/ADR

Entrega a C4 componentes de red, HA, respaldo, DR, monitoreo y sitio que requieran fila o cantidad.

### Salidas hacia otros frentes

- Frente 3: zonas, conductos, accesos administrativos y failover.
- Frente 1: restricciones de disponibilidad que requieran degradación lógica.

### Definición de terminado

- [ ] Cinco ambientes explícitos y aislados.
- [ ] Red de patio se valida en condición real; ubicación queda sujeta a site survey.
- [ ] VMS no se degrada durante segmentación.
- [ ] RTO/RPO, DR, respaldo y restauración tienen prueba.
- [ ] 72 h y 90 min están dimensionados y trazados.
- [ ] No se programa intervención prohibida.
- [ ] `TRZ_C3.md` completo.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_C3.md`](trazabilidad/TRZ_C3.md).

