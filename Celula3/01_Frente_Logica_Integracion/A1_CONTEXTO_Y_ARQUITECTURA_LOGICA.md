# A1 — Contexto y arquitectura lógica

## Contrato del entregable

### Objetivo y destino

Producir el esquema de solución y la arquitectura lógica oficial. Alimenta las secciones 4.1.1–4.1.5 de `90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`.

### Cumplimientos asignados

- `SD4-01`, `SD4-07`, `SD4-08`.
- T7-4.1, T7-4.7 y T7-4.8.
- T21 4.1 a) Esquema de solución y b) Arquitectura lógica.
- BTT RT-02.02, 02.03, 02.04, 02.09, 02.11 y 02.13.

### Entradas obligatorias

1. Maestro de Contexto §§2–6, 17–19.
2. Catálogos RF vigentes y RNF de Célula 2.
3. Registro de decisiones/supuestos y reglas de negocio.
4. `A2` para interfaces detalladas y `D1` para controles lógicos, cuando exista `v0.1`.

### Trabajo requerido

- [ ] Delimitar TERABYTE frente a actores y sistemas conservados.
- [ ] Dibujar esquema de solución de alto nivel.
- [ ] Dibujar arquitectura lógica con ocho capas obligatorias.
- [ ] Confirmar/refinar los IDs del Maestro sin crear un componente por RF.
- [ ] Definir bounded context, responsabilidad, dato/evento y propietario.
- [ ] Declarar dependencias permitidas y prohibidas.
- [ ] Representar seguridad y observabilidad como transversales.
- [ ] Incorporar app instalable, portal, cabina/terreno y canales compartidos.
- [ ] Elaborar modelo conceptual mínimo y eventos principales.
- [ ] Comparar núcleo modular con alternativa distribuida.
- [ ] Explicar por qué las vistas son específicas del puerto.

### Reglas de diagramación

- una dirección de lectura dominante;
- actores/sistemas externos fuera del límite;
- capas como bandas y módulos agrupados por contexto;
- leyenda de colores, tipos de flecha y alcance;
- nombres de negocio idénticos en todas las vistas;
- máximo aproximado de 15–20 elementos principales por página; usar detalle aparte si se excede;
- sin marcas de producto en la vista lógica;
- cada flecha relevante debe tener significado, no decoración.

### Productos obligatorios

1. Diagrama de contexto/esquema de solución.
2. Diagrama lógico por capas.
3. Catálogo: ID, nombre, capa, contexto, responsabilidad, criticidad, datos, interfaces, continuidad y dueño.
4. Modelo conceptual de dominio y eventos.
5. Tabla de comparación de estilos y candidato `ADR-001`.
6. Narrativa lista para insertar, no solo notas.

### Decisiones permitidas y escalamiento

Puede ajustar límites lógicos si conserva todas las capacidades y justifica el cambio. Debe escalar cualquier cambio que altere la Decisión TOS, las 72 h, el Programa 2029, sistemas conservados o alcance de Célula 2.

### Aporte T-11/ADR

No llena cantidades físicas. Identifica plataformas/licencias que podrían materializar componentes y entrega candidatos a C4. Redacta `ADR-001` como propuesta.

### Salidas hacia otros frentes

- Frente 2: catálogo lógico `v0.1` y criticidad.
- Frente 3: componentes, fronteras de confianza, usuarios y sensibilidad.

### Definición de terminado

- [ ] Dos diagramas coherentes y legibles.
- [ ] Ocho capas visibles.
- [ ] Todos los componentes tienen responsabilidad y límite.
- [ ] No hay acceso UI→BD ni caja física en la vista lógica.
- [ ] Actores, TOS, ERP, VMS, autoridades, ferrocarril y concedente visibles.
- [ ] Catálogo y modelo conceptual acompañan los diagramas.
- [ ] `TRZ_A1.md` completo y revisión cruzada resuelta.

## Contenido listo para integrar

> Sustituir este bloque por la narrativa aprobada y los enlaces a los diagramas. No borrar el contrato hasta que D3 confirme la integración.

## Trazabilidad

Ver [`trazabilidad/TRZ_A1.md`](trazabilidad/TRZ_A1.md).

