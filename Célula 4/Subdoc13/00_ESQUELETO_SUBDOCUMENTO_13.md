# Esqueleto — Subdocumento 13 · Innovaciones

> **Caso:** 06 Portuaria — TERABYTE · **Célula 4** · **Responsable:** Matías Reyes
> **Corte:** 2026-09-06 · **Estado:** estructura cerrada, contenido completo
> **Fuente de la estructura:** Formulario T-7 (contenido del Subdocumento 13), Formulario T-22 (alcance del Informe 1) y Capítulo 26 de las BTT.

Este archivo es el mapa de la sección. Cada numeral indica de qué archivo sale su contenido y en qué estado está. **No contiene texto: el texto vive en los archivos `B0x`.**

---

## 13. Innovaciones

| Numeral | Título | Contenido exigido | Archivo fuente | Estado |
|---|---|---|---|---|
| **13.1** | **Criterio de selección y coherencia con el caso** | | | |
| 13.1.1 | Cómo se eligieron estas cinco y no otras | El embudo de cuatro descartes y la tabla de los cinco huecos | `B01` | `APROBADO` |
| 13.1.2 | Síntesis de la cartera | Las cinco innovaciones y la herida del Cap. 7 que ataca cada una | `B01` | `APROBADO` |
| 13.1.3 | Pertinencia al Caso Portuaria | Art. 30.2 y Cap. 19: pertinencia por sobre novedad | `B01` | `APROBADO` |
| 13.1.4 | Diferencia entre innovación y funcionalidad obligatoria | Contraste de cada innovación contra el RF más próximo | `B02` | `APROBADO` |
| 13.1.5 | Coherencia conjunta de la cartera | Cómo se sostienen entre sí y qué exclusiones respetan | `B02` | `APROBADO` |
| 13.1.6 | Relación con las etapas y con el alcance | Materialización en el cronograma del Art. 17° | `B02` | `APROBADO` |
| **13.2** | **Innovación de producto o servicio** | IN-01 · Cadena de frío certificada Aconcagua | `B03` | `APROBADO` |
| **13.3** | **Innovación de proceso** | IN-02 · Cita convenida a tres bandas | `B04` | `APROBADO` |
| **13.4** | **Innovación tecnológica o de arquitectura** | IN-03 · Gemelo de operación | `B05` | `APROBADO` |
| **13.5** | **Innovación de modelo de negocio o contratación** | IN-04 · Servicio gestionado del equipamiento de terreno | `B06` | `APROBADO` |
| **13.6** | **Innovación de UX, sostenibilidad o impacto social** | IN-05 · Intensidad de carbono comprometida | `B07` | `APROBADO` |
| **13.7** | **Trazabilidad conjunta de las innovaciones** | | | |
| 13.7.1 | Resultados verificables esperados | Indicador, línea base y momento de medición por innovación | `B08` | `APROBADO` |
| 13.7.2 | Riesgos de adopción de la cartera | Tres riesgos comunes con la estructura obligatoria de enunciado | `B08` | `APROBADO` |
| **13.8** | **Alcance de esta entrega** | Qué se entrega ahora y qué en cada informe posterior | `B08` | `APROBADO` |
| **13.9** | **Referencias** | Once fuentes en APA 7.ª ed. más las normativas | `B12` | `APROBADO` |

---

## Los cinco ejes que exige el T-22 por innovación

Cada uno de los numerales 13.2 a 13.6 desarrolla, en este orden y con estos encabezados:

1. **Idea** — qué problema concreto del terminal resuelve.
2. **Tecnología que la sustenta** — descrita con precisión técnica, no como categoría genérica.
3. **Alcance** — qué cubre y, sobre todo, qué **no** cubre.
4. **Forma de implementación** — dónde se inserta en la arquitectura y de qué depende.
5. **Resultado esperado** — el beneficio, anclado a una cifra del caso.
6. **Investigación adicional declarada** — exigido expresamente por el T-22.

---

## Cobertura del Capítulo 26 de las BTT

| Código | Exigencia | Dónde se satisface |
|---|---|---|
| `RT-26.01` | Ubicación explícita en la arquitectura | Eje 4 de cada innovación (`B03`–`B07`) |
| `RT-26.02` | Paquetes de la EDT y mes del cronograma | Tabla de etapas en `B02`. La EDT se exige en el Informe 2 |
| `RT-26.03` | Nivel de madurez con escala y fuentes APA | Eje 6 de `B05` y `B07`; referencias en `B12` |
| `RT-26.04` | Riesgo, probabilidad, impacto, mitigación y contingencia | `B08` y fichas T-19 en `B09` |
| `RT-26.05` | Indicador con línea base, meta y momento | `B08` |
| `RT-26.06` | Innovaciones con IA cumplen el Cap. 18 | Declarado en `B05`: ninguna incorpora IA en su versión comprometida |
| `RT-26.07` | Modelado de amenazas propio | Declarado como dependencia en `B03` y `B05` |
| `RT-26.08` | *Deseable:* una innovación verificable antes del mes 16 | **IN-02**, medible en la marcha blanca de Etapa 1 (`B04`) |

---

## Reglas de redacción aplicadas

1. **Ninguna cifra sin fuente.** Toda cifra proviene del Capítulo 7 o 14 del Caso y fue verificada una a una (`B10`).
2. **Ninguna innovación puede ser una funcionalidad obligatoria.** Cada una se contrastó contra los 139 RF vigentes (`B02`).
3. **Sin información económica.** El Artículo 53° la declara causal de inadmisibilidad en la Oferta Técnica; la valorización va al Informe 3.
4. **Lo que no se sabe se declara, no se inventa.** Las metas que no pueden fijarse hoy quedan como investigación adicional declarada.
5. **Nada del lenguaje interno del equipo** —nombres de células, archivos internos— aparece en el texto que ve el cliente.
