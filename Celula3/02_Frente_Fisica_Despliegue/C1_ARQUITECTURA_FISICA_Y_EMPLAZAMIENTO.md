# C1 — Arquitectura física y emplazamiento

## Contrato del entregable

### Objetivo y destino

Ubicar cada componente desplegable en nube, on-premise o borde y justificarlo conforme al Artículo 16. Alimenta las secciones 4.2.1 y 4.2.2 del consolidado.

### Cumplimientos asignados

- `SD4-02`, `SD4-05`, `SD4-07`, `SD4-08`.
- T7-4.2, T7-4.5, T7-4.7 y T7-4.8.
- BTT Cap. 3; RT-03.01..15; Decisión 20; `MC-09/10/11`.

### Entradas obligatorias

- Maestro §§3–6, 9–10, 15, 17–19.
- A1 catálogo lógico `v0.1` para refinar el mapeo.
- A3 funciones críticas y D1 paquete `SEC-PHYS-v0.1`.
- Condiciones físicas y volumetría de Célula 2.

### Trabajo requerido

- [ ] Dibujar límite de oferta y topología híbrida completa.
- [ ] Identificar nube primaria/secundaria y al menos dos zonas de disponibilidad.
- [ ] Identificar sala, edge de gate/patio/reefer/muelle y sistemas conservados.
- [ ] Mapear cada componente lógico desplegable a uno o más nodos.
- [ ] Justificar cada ubicación por seis criterios Art. 16.
- [ ] Mostrar zonas, redes, enlaces, redundancia y protocolos.
- [ ] Comparar sala actual, nueva/reconstruida y edge mínimo+nube.
- [ ] Declarar SPOF residuales y dependencia de terceros.
- [ ] Delimitar qué queda fuera de la oferta o sujeto a levantamiento.

### Tabla de emplazamiento obligatoria

| ID físico | Componente lógico | Función | Ubicación | Latencia | Continuidad | Volumen | Regulación/seguridad | Conectividad/acoplamiento | TCO cualitativo | Justificación final | Estado |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `PHY-001` | POR ASIGNAR | — | nube/on-prem/edge | — | — | — | — | — | — | — | PENDIENTE |

### Reglas del diagrama físico

- nombres de producto sí son permitidos, si están justificados;
- mostrar capacidades relevantes, redundancia, protocolos y fronteras;
- distinguir zona pública, privada, operacional, administrativa y protección;
- mostrar correspondencia con lógico mediante IDs;
- toda caja ofertada debe tener candidato T-11;
- no dibujar ubicación física inexistente ni ocultar dependencias.

### Productos obligatorios

1. Diagrama físico híbrido.
2. Tabla de emplazamiento Art. 16.
3. Matriz lógico→físico.
4. Comparación de alternativas de sala y candidato `ADR-005`.
5. Registro inicial de SPOF.

### Decisiones permitidas y escalamiento

Puede proponer topología y ubicación. Debe escalar contratos no confirmados, datos de sitio ausentes, cambios al plan de protección, infraestructura fuera del recinto no declarada o cualquier solución que reduzca las 72 h.

### Aporte T-11/ADR

Entrega a C4 el inventario de cajas físicas y su ubicación. Cada una se clasifica como fila T-11, parte interna de otra fila o elemento fuera de oferta, siempre con razón.

### Salidas hacia otros frentes

- Frente 1: restricciones físicas que cambien dependencia o flujo.
- Frente 3: nodos, zonas, exposición, administración y fronteras de confianza.

### Definición de terminado

- [ ] Todos los componentes desplegables tienen ubicación y justificación.
- [ ] La solución es realmente híbrida y multi-AZ.
- [ ] Se ven sala, borde, nube, DR, enlaces y sistemas conservados.
- [ ] Las 72 h no dependen de nube.
- [ ] No se presume que el ambiente marino desaparece.
- [ ] Físico, catálogo lógico y T-11 usan los mismos IDs.
- [ ] `TRZ_C1.md` completo.

## Contenido listo para integrar

> Incorporar aquí narrativa, tabla y enlace al diagrama aprobados.

## Trazabilidad

Ver [`trazabilidad/TRZ_C1.md`](trazabilidad/TRZ_C1.md).

