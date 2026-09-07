# Célula 4 — Subdocumento 5, Modelo y gestión de datos

**Caso:** 06 Portuaria — TERABYTE · **Informe 1** · ponderación 11 %
**Equipo:** V. Guzmán / M. Reyes
**Estado:** trece apartados cubiertos para diseño I1 · 21 decisiones editoriales C4 registradas · condiciones externas trazadas
**Actualizado:** 6 de septiembre de 2026

> Esta carpeta contiene el **conjunto canónico versionado** del Subdocumento 5:
> entregable legible, comunicaciones y material de respaldo. Las copias ubicadas
> fuera de esta carpeta se conservan solo por compatibilidad y no se editan.

---

## Qué hay en esta carpeta

### El entregable

| Archivo | Qué es |
|---|---|
| `Subdocumento_5.pdf` | Entregable compilado del corte anterior: 103 páginas, con los catorce diagramas y el diccionario completo |
| `CONTENIDO_SUBDOCUMENTO_5.md` | **Fuente canónica versionada para revisión y alineación**; se edita aquí antes de regenerar el PDF |

> El proyecto LaTeX `Documento terabyte SubDoc 5` citado en versiones anteriores no está presente en `main`. Mientras no se incorpore o se documente una regeneración reproducible, no se usa como autoridad invisible sobre el contenido versionado. Las correcciones de alineación se realizan en el Markdown canónico; el PDF se regenera después del cierre.

### `Comunicados/` — lo que sale hacia otras células

| Archivo | Para quién | Qué contiene |
|---|---|---|
| `00_PENDIENTES_CELULA4.md` | uso interno | Lo que falta para cerrar nuestra parte, y lo que falta de cada célula |
| `01_DECISIONES_CELULA4_PARA_OTRAS_CELULAS.md` | Células 1, 2 y 3 | Las 21 decisiones cerradas, con quién debería leer cada una |
| `02_SOLICITUD_A_CELULA_3.md` | Célula 3 | Doce peticiones ordenadas por urgencia, con lo que les entregamos a cambio |
| `03_SOLICITUD_A_CELULA_2.md` | Célula 2 | Cinco peticiones, con el `RNF-CAL-01` ya redactado |
| `04_CONSULTAS_AL_CLIENTE.md` | CLIENTE y terceros | Seis consultas, cada una con su tratamiento provisional declarado |

### `Documentos_de_trabajo/` — cómo se construyó

Material de respaldo. Todo su contenido está ya volcado en el Subdocumento 5; se conservan porque llevan el razonamiento completo, que el documento final resume.

| Archivo | Materia | Apartado del Subdoc. 5 |
|---|---|---|
| `00_ESQUELETO_SUBDOCUMENTO_5.md` | El esqueleto inicial, con el estado de cada apartado antes de desarrollarlos. Se conserva como registro del punto de partida; **está superado** por el documento final | punto de partida |
| `A00_REGISTRO_DECISIONES_CELULA4.md` | Las 21 decisiones y los 20 pendientes, con su fundamento | transversal |
| `A01_MODELO_CONCEPTUAL_DATOS.md` | Modelo conceptual: dominios, entidades, eventos e invariantes | § 5.2 y § 5.14 |
| `A02_DICCIONARIO_DE_DATOS.md` | 80 entidades y 451 atributos con sus ocho campos | § 5.14 y Anexo |
| `A03_CALIDAD_ISO25012.md` | 54 reglas de calidad, 12 indicadores y 12 pruebas | § 5.11 |
| `A05_ALTERNATIVAS_PERSISTENCIA.md` | 13 alternativas sobre 7 criterios ponderados | § 5.4 |
| `A06_MATRIZ_CAP_POR_OPERACION.md` | 6 particiones, 8 unidades transaccionales, 25 operaciones | § 5.5 |
| `A07_ESTRATEGIA_DESEMPENO.md` | 21 índices, particiones, caché y cuello de botella | § 5.10 |
| `A08_ALMACENAMIENTO_ACUMULADO.md` | Capacidad acumulada y cuatro escenarios de reposición | § 5.13 |

No hay un `A04`: esa numeración se saltó porque el diccionario absorbió el trabajo que iba a ser un documento aparte.

### `diagramas/` — fuentes históricas de la primera versión

Los once diagramas de la versión 1 en formato Mermaid. La versión 2.1 se atribuye históricamente a un proyecto externo no versionado. Los archivos de esta carpeta se conservan como historial de A-01 y no deben usarse para reconstruir diagramas finales de C3.

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

**Regla de vacíos.** Ante la duda, condicionado y con responsable. Un dato inventado en un modelo o en un diccionario es invisible: una celda con un valor plausible parece un hecho y nadie la vuelve a revisar. Los vacíos legítimos permanecen trazados a terceros o al CLIENTE.
