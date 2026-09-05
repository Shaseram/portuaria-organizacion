# C4 — Dimensionamiento y T-11

## Contrato del entregable

### Objetivo y destino

Transformar la volumetría en capacidades y cantidades justificadas, y consolidar el T-11. Alimenta la sección 4.2.11 y los formularios de `90_Consolidado/`.

### Cumplimientos asignados

- `SD4-02`, `SD4-06`, `SD4-08`.
- T7-4.6; T21 4.2; Formulario T-11.
- BTT RT-08.01/03/04/05/10/11 y RT-09.02; pruebas a 1,5× peak.

### Entradas obligatorias

- Maestro §§2.1, 4, 7, 9–10 y 15–16.
- Volumetría completa de Célula 2.
- A1 componentes, A2 flujos/volúmenes, C1/C2/C3 nodos y D1 candidatos de seguridad.

### Trabajo requerido

- [ ] Revalidar las 18 dimensiones heredadas sin borrar sus supuestos.
- [ ] Declarar fórmulas, unidades, fuentes y calidad de dato.
- [ ] Dimensionar régimen normal y peak coincidente de dos naves+gate.
- [ ] Dimensionar ingesta local/central, almacenamiento, red, usuarios y crecimiento.
- [ ] Dimensionar buffer para 72 h y sincronización ≤90 min.
- [ ] Añadir replicación, respaldo, índices, logs, SO y holgura sin doble conteo.
- [ ] Declarar margen de crecimiento y procedimiento de ampliación.
- [ ] Identificar primer cuello de botella y sensibilidad.
- [ ] Convertir resultados a cantidades físicas verificables.
- [ ] Consolidar candidatos T-11 de los tres frentes.
- [ ] Revisar 1:1 físico→cálculo→T-11 y ausencia de precios.

### Hoja de cálculo narrativa obligatoria

| ID DIM | Variable | Actual | Horizonte | Peak | Fórmula/método | Supuestos | Fuente | Sensibilidad | Resultado de capacidad | Estado |
|---|---|---:|---:|---:|---|---|---|---|---|---|
| `DIM-01` | TPS negocio | 0,11 | 0,13 | 0,23/0,27 | ver C2 | revisar | Volumetría C2 | POR HACER | POR HACER | PENDIENTE |

### Conversión a cantidad obligatoria

| ID físico | Demanda base | Factor peak | HA/DR | Retención | Holgura | Capacidad por unidad | Cantidad calculada | Redondeo/razón | Fila T-11 |
|---|---:|---:|---:|---:|---:|---:|---:|---|---|
| POR COMPLETAR | — | — | — | — | — | — | — | — | — |

### Reglas T-11

- Una fila final contiene exactamente: Componente; Producto/servicio; Ubicación/lugar; Cantidad; Justificación.
- La tabla de trabajo puede tener trazas adicionales; la final no.
- No hay fila por cada módulo lógico, solo por componente físico/plataforma/licencia/hardware ofertado.
- Cada fila debe mapear al diagrama físico, cálculo, seguridad y fuente.
- No incluir precios ni información que permita inferirlos.
- Si una cantidad depende de site survey, usar cantidad/rango justificable y declarar el mecanismo de cierre; no inventar ubicación exacta.

### Productos obligatorios

1. Dimensionamiento reproducible.
2. Tabla de sensibilidad y holgura.
3. Matriz de cantidades.
4. `90_Consolidado/01_T11_TRABAJO_TRAZABLE.md` completo.
5. Propuesta de `02_FORMULARIO_T11_FINAL.md`.

### Salidas hacia otros frentes

- Frente 2: retroalimentación si un producto no soporta la demanda.
- Frente 3: datos para auditoría y control de seguridad/licencias.

### Definición de terminado

- [ ] Cálculos reproducibles y unidades coherentes.
- [ ] Supuestos propios diferenciados de hechos del CLIENTE.
- [ ] Se dimensionan normal, peak, crecimiento, 72 h, HA y DR.
- [ ] Primer cuello de botella y ampliación declarados.
- [ ] Cada cantidad llega al T-11 y cada fila vuelve a un cálculo.
- [ ] No hay precios.
- [ ] `TRZ_C4.md` completo.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_C4.md`](trazabilidad/TRZ_C4.md).

