# Célula 4 — Subdocumento 5, Modelo y gestión de datos

**Caso:** 06 Portuaria — TERABYTE · **Informe 1** · ponderación 11 %
**Equipo:** V. Guzmán / M. Reyes
**Estado:** trece apartados cubiertos para diseño I1 · 21 decisiones editoriales C4 registradas · condiciones externas trazadas
**Actualizado:** 6 de septiembre de 2026

---

## Qué hay en esta carpeta

### Regla de edición dentro de `main`

Para la alineación con Célula 3 se usa **una sola ruta editable** por artefacto:

- entregable legible: `Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`;
- razonamiento y matrices: `Subdocumento_5/Documentos_de_trabajo/A00..A08`;
- comunicaciones: `Subdocumento_5/Comunicados/`;
- innovaciones: `Subdoc13/B*.md`.

Los A00–A08, comunicados y diagramas repetidos en la raíz o en `Documentos_de_trabajo/` se conservan como copias históricas o de compatibilidad y **no se editan**. No se deben corregir varias copias a mano.

### `Subdocumento_5/` — el entregable

| Archivo | Qué es |
|---|---|
| `Subdocumento_5.pdf` | El documento compilado: 103 páginas, con los catorce diagramas del modelo conceptual y el diccionario completo |
| `CONTENIDO_SUBDOCUMENTO_5.md` | El mismo contenido en Markdown, para leer, buscar y citar sin compilar |

> **Fuente canónica versionada para revisión y alineación:** `Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md`. `Subdocumento_5.pdf` es el entregable compilado del corte anterior. El proyecto `Documento terabyte SubDoc 5` citado históricamente no está versionado en este repositorio y no puede gobernar correcciones hasta que sea incorporado o se documente un mecanismo reproducible de regeneración.

### `Comunicados/` — copias de compatibilidad, no editar

| Archivo | Para quién | Qué contiene |
|---|---|---|
| `00_PENDIENTES_CELULA4.md` | uso interno | Lo que falta para cerrar nuestra parte, y lo que falta de cada célula |
| `01_DECISIONES_CELULA4_PARA_OTRAS_CELULAS.md` | Células 1, 2 y 3 | Las 21 decisiones cerradas, con quién debería leer cada una |
| `02_SOLICITUD_A_CELULA_3.md` | Célula 3 | Doce peticiones ordenadas por urgencia, con lo que les entregamos a cambio |
| `03_SOLICITUD_A_CELULA_2.md` | Célula 2 | Cinco peticiones, con el `RNF-CAL-01` ya redactado |
| `04_CONSULTAS_AL_CLIENTE.md` | CLIENTE y terceros | Seis consultas, cada una con su tratamiento provisional declarado |

### `Documentos_de_trabajo/` — copias de compatibilidad, no editar

Son copias idénticas del material canónico bajo `Subdocumento_5/Documentos_de_trabajo/`. Se conservan para no romper referencias anteriores; todo cambio debe aplicarse en la ruta canónica.

| Archivo | Materia | Apartado del Subdoc. 5 |
|---|---|---|
| `A00_REGISTRO_DECISIONES_CELULA4.md` | Las 21 decisiones y los 20 pendientes, con su fundamento | transversal |
| `A01_MODELO_CONCEPTUAL_DATOS.md` | Modelo conceptual: dominios, entidades, eventos e invariantes | § 5.2 y § 5.14 |
| `A02_DICCIONARIO_DE_DATOS.md` | 80 entidades y 451 atributos con sus ocho campos | § 5.14 y Anexo |
| `A03_CALIDAD_ISO25012.md` | 54 reglas de calidad, 12 indicadores y 12 pruebas | § 5.11 |
| `A05_ALTERNATIVAS_PERSISTENCIA.md` | 13 alternativas sobre 7 criterios ponderados | § 5.4 |
| `A06_MATRIZ_CAP_POR_OPERACION.md` | 6 particiones, 8 unidades transaccionales, 25 operaciones | § 5.5 |
| `A07_ESTRATEGIA_DESEMPENO.md` | 21 índices, particiones, caché y cuello de botella | § 5.10 |
| `A08_ALMACENAMIENTO_ACUMULADO.md` | Capacidad acumulada y cuatro escenarios de reposición | § 5.13 |

### `diagramas/` — historial, no editar

Los once diagramas de la primera versión en formato Mermaid. El índice histórico atribuye la versión 2.1 a un proyecto externo que no está en `main`; por ello estos archivos sirven como evidencia histórica y no como fuente vigente de edición.

### `00_ESQUELETO_SUBDOCUMENTO_5.md`

El esqueleto inicial del 6 de septiembre, con el estado de cada apartado antes de desarrollarlos. Se conserva como registro del punto de partida; **está superado** por el Subdocumento 5 y por el registro de decisiones.

---

## Estado por apartado

| § | Materia del checklist oficial | Estado |
|---|---|---|
| 5.2 | Dominios y entidades principales | completado |
| 5.3 | Fuentes oficiales y fuente de verdad | completado |
| 5.4 | Paradigma de persistencia y motores propuestos | completado |
| 5.5 | Transaccionalidad, consistencia y disponibilidad | completado |
| 5.6 | Separación transaccional, temporal y analítica | completado |
| 5.7 | Telemetría y frecuencia de muestreo | completado |
| 5.8 | Integración e interoperabilidad de datos | completado para diseño I1; contratos externos condicionados |
| 5.9 | Migración, saneamiento, validación y conciliación | completado |
| 5.10 | Estrategia de desempeño de datos | completado |
| 5.11 | Calidad ISO/IEC 25012, auditoría y trazabilidad | completado |
| 5.12 | Retención, archivo y eliminación segura | completado |
| 5.13 | Volumetría actual, proyectada y de peak | completado |
| 5.14 | Modelo conceptual y diccionario inicial de datos | completado |

---

## Lo que falta, en una línea por destinatario

- **Nosotras:** revisión cruzada, compilar en Overleaf, subir el control de versiones a 1.0 e integrar con los demás subdocumentos del Informe 1.
- **Célula 3:** baseline recibida; quedan condicionadas las pruebas de ocho índices, contratos/CDC reales, site survey, política de imagen y matriz exacta de copias.
- **Célula 2:** cinco peticiones, incluido el evento del que se deriva el movimiento de grúa de muelle y las bandas de desviación de temperatura.
- **CLIENTE:** seis consultas, todas con tratamiento provisional declarado.

El detalle está en `Comunicados/00_PENDIENTES_CELULA4.md`.

---

## Dos reglas que gobiernan todo este material

**Regla de cita.** Ninguna afirmación cita un código `RT` aislado: la referencia mínima es documento + capítulo + código + materia. Los códigos se repiten entre documentos designando materias distintas —`RT-05.10` es *linaje* en las Transversales y *retención* en el Caso—, de modo que citar el código suelto puede invertir el sentido de la obligación.

**Regla de vacíos.** Ante la duda, pendiente. Un dato inventado en un modelo o en un diccionario es invisible: una celda con un valor plausible parece un hecho y nadie la vuelve a revisar. Quedan tres vacíos declarados en 451 atributos, y ninguno es de Célula 4.
