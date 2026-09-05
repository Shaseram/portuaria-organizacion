# C2 — Tecnologías, hardware y data centers

## Contrato del entregable

### Objetivo y destino

Especificar las tecnologías y los implementos que materializan la arquitectura, incluido recinto primario y secundario/DR. Alimenta las secciones 4.2.3–4.2.6.

### Cumplimientos asignados

- T21 4.2 b), c), d), e) y Formulario T-11.
- `SD4-02`, `SD4-05`, `SD4-06`, `SD4-08`.
- BTT Cap. 6 completo: `RT-06.01` a `RT-06.34`. BTT Cap. 7 completo: `RT-07.01` a `RT-07.14`. BTT Cap. 3 y Cap. 8; `MC-09/10/11/12`.
- Checklist del BTT, Cap. C, entregables N° 8 (site principal y secundario, **con planos**) y N° 10 (hardware y dispositivos de terreno).

> *Corrección `F2-COR-002` (2026-09-05): el contrato declaraba `RT-06.01..24` y no mencionaba el Capítulo 7. El numeral 3.2 del BTT dice «se aplican íntegramente los requisitos **RT-06.01 a RT-06.34**»; los diez omitidos son tres subcapítulos de este frente —6.7 custodia de medios, 6.8 espacio de operación del personal y 6.9 rutas de comunicaciones—. El Capítulo 7, site secundario y recuperación ante desastres, no estaba citado en ninguna parte de Célula 3 pese a que `T21-4.2-E` es elemento evaluado. Ver `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`, `F2-ESC-003` y `F2-ESC-004`.*

### Entradas obligatorias

- C1 topología `v0.1`, C4 cálculos preliminares y D1 controles/componentes.
- Maestro §§4.3, 9–12, 15–16, 18–19.
- BTT infraestructura on-premise, hardware de terreno, seguridad y continuidad.

### Trabajo requerido

- [ ] Definir tecnologías de software, versiones o política de vigencia/EOS.
- [ ] Comparar productos/servicios de referencia cuando la elección sea relevante.
- [ ] Justificar gestionado vs. autogestionado y reversibilidad.
- [ ] Especificar cómputo, memoria, almacenamiento, interfaces, consumo y redundancia.
- [ ] Definir almacenamiento/RAID con tolerancia y capacidad.
- [ ] Especificar switches, firewalls, balanceadores y energía en HA.
- [ ] Detallar data center/sala primario y secundario/DR.
- [ ] Detallar racks, UPS, generación, climatización, incendio, acceso y monitoreo.
- [ ] Especificar custodia de medios de respaldo: recinto, condiciones ambientales, inventario y rotación (`RT-06.26..28`).
- [ ] Especificar el espacio de operación del personal, separado de la sala de equipos, y declarar qué instalaciones existentes se reutilizan (`RT-06.29..31`).
- [ ] Especificar rutas de comunicaciones físicamente distintas con ingreso al edificio por puntos separados, y las canalizaciones requeridas (`RT-06.32/33`).
- [ ] Especificar el site secundario: modalidad activo-activo o activo-pasivo justificada, distancia al principal y análisis de amenazas comunes (`RT-07.01/02`).
- [ ] Declarar la disponibilidad mensual por componente del recinto —energía, climatización, red, cómputo, motor de base de datos y portal— conforme al numeral 7.2 del BTT.
- [ ] Declarar las dos tensiones registradas: biometría del recinto (`F2-DEC-002`) y CCTV propio del recinto frente al VMS conservado (`F2-DEC-003`).
- [ ] Especificar gabinetes/dispositivos por clase marina y ubicación.
- [ ] Incluir puestos de trabajo/monitores duales solo donde el dimensionamiento lo justifique.
- [ ] Entregar candidatos T-11 sin precios.

### Catálogo tecnológico obligatorio

| ID | Componente físico | Producto/servicio o referencia | Versión/vigencia | Especificación mínima | Ubicación | Cantidad/criterio | HA/energía | Operación/mantenimiento | Alternativa | Justificación | T-11 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| POR COMPLETAR | — | — | — | — | — | — | — | — | — | — | — |

### Tabla marina obligatoria

| Clase/ubicación | Riesgos | IP/NEMA | Anticorrosión/material | Temperatura/humedad | Energía/UPS | Vida útil/reposición | Prueba de recepción | Cantidad |
|---|---|---|---|---|---|---|---|---|
| gabinete de borde | salinidad/intemperie | POR DEFINIR | POR DEFINIR | POR DEFINIR | POR DEFINIR | POR DEFINIR | POR DEFINIR | C4 |

### Reglas importantes

- Si se propone sala principal sustantiva, aplicar RT-06.01..24 íntegros.
- UPS ≥30 min a plena carga y generación ≥24 h donde aplique.
- Separar racks de cómputo y comunicaciones; declarar kW, factor de potencia y PUE.
- Equipamiento nuevo y con garantía.
- Marca/modelo son referencias justificadas, no relleno comercial.
- No sobredimensionar: toda capacidad debe volver a C4.
- No incluir costos unitarios en Informe 1 pese a que la base técnica los mencione; registrar la tensión y mantener solo especificación/cantidad.

### Productos obligatorios

1. Catálogo tecnológico completo.
2. Especificación del primario y secundario/DR.
3. Plano conceptual de sala/racks o distribución aplicable.
4. Tabla de protección marina.
5. Candidatos de T-11 y aportes `ADR-005/007`.

### Salidas hacia otros frentes

- Frente 3: productos, superficies de administración, logs, identidades y actualizaciones.
- C4: SKU/referencia, unidad de cantidad y variables de cálculo.

### Definición de terminado

- [ ] Todo producto materializa una caja física o control obligatorio.
- [ ] Versiones y soporte están declarados o existe criterio de vigencia.
- [ ] Sala y equipos cumplen ambiente, energía, HA y mantenimiento.
- [ ] Cantidades se vinculan a C4; no hay precios.
- [ ] Primario/secundario y responsabilidades están diferenciados.
- [ ] `TRZ_C2.md` completo.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_C2.md`](trazabilidad/TRZ_C2.md).

