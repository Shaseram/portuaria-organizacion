# A3 — Procesos críticos y convivencia TOS

## Contrato del entregable

### Objetivo y destino

Explicar el comportamiento dinámico de los procesos críticos, la convivencia con el TOS y la continuidad local. Alimenta las secciones 4.1.7 y 4.2.9 del consolidado.

### Cumplimientos asignados

- `SD4-01`, `SD4-03`, `SD4-05`, `SD4-07`, `SD4-08`.
- `MC-07/08/09/13/14/23/24/25/27/30`.
- RF-CON-01..14, RNF-DIS-02/04/09/12 y requisitos críticos de nave/gate/reefer.

### Entradas obligatorias

- Maestro §§8–9, 12–14, 16–18.
- Decisión TOS 2012 completa.
- Reglas RN-01..10 y catálogos RF/RNF.
- A1/A2 `v0.1`; C3 refina nodos y D1 refina controles.

### Trabajo requerido

- [ ] Diagramar operación nave y mensajería.
- [ ] Diagramar cita/prevalidación/gate/excepción.
- [ ] Diagramar reefer: muestra→regla→alarma→confirmación→escalamiento.
- [ ] Diagramar inspección→remoción→acta→hecho facturable.
- [ ] Diagramar 72 h desconectado→reconexión≤90 min.
- [ ] Diagramar TOS nuevo→legado y legado→nuevo con fallo parcial.
- [ ] Crear matriz de autoridad `dominio × zona × fase`.
- [ ] Definir conciliación, umbrales, ventanas y clasificación de diferencias.
- [ ] Definir cruce de zona, cutover, retorno normal y break-glass.
- [ ] Declarar funciones indisponibles offline y respaldo manual.
- [ ] Reflejar congelamiento y programa 2029 en los escenarios.

### Matriz de autoridad obligatoria

| Dominio | Zona | Fase | Fuente de verdad | Escritura autorizada | Sincronización | Criterio de traspaso | Retorno |
|---|---|---|---|---|---|---|---|
| POR COMPLETAR | POR COMPLETAR | POR COMPLETAR | TOS/nuevo | único | POR DEFINIR | evento transaccional | POR DEFINIR |

### Catálogo de procesos obligatorio

| Proceso | Actores | Disparador | Camino normal | Fallo | Fallback | Datos/evidencia | Umbral | Diagrama |
|---|---|---|---|---|---|---|---|---|
| Operación desconectada | operación/TI | pérdida enlace | runtime local | dependencia externa | procedimiento declarado | cola/bitácora | 72 h/90 min | POR CREAR |

### Productos obligatorios

1. Cinco secuencias mínimas y detalle TOS.
2. Matriz de autoridad.
3. Tabla de conciliación/retorno.
4. Tabla de funciones disponibles/no disponibles offline.
5. Candidatos `ADR-002` y `ADR-004`.

### Aporte T-11/ADR

Informa capacidades necesarias para runtime local, colas/buffer y herramientas de reconciliación; no fija hardware.

### Salidas hacia otros frentes

- Frente 2: criticidad, continuidad, latencia, buffer y recuperación.
- Frente 3: operaciones privilegiadas, break-glass, trazas y fallos.

### Definición de terminado

- [ ] No existe autoridad simultánea ambigua.
- [ ] Ambas direcciones TOS y fallos parciales están resueltas.
- [ ] Las cinco funciones críticas sobreviven 72 h.
- [ ] Se declaran funciones no disponibles y procedimientos manuales.
- [ ] Retorno y reconciliación tienen responsables, disparadores y relojes.
- [ ] Escenarios y diagramas coinciden con A1/A2.
- [ ] `TRZ_A3.md` completo.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_A3.md`](trazabilidad/TRZ_A3.md).

